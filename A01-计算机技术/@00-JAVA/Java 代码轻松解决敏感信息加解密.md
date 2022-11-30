Java 代码轻松解决敏感信息加解密

关注

出于安全考虑，现需要将数据库的中敏感信息加密存储到数据库中，但是正常业务交互还是需要使用明文数据，所以查询返回我们还需要经过相应的解密才能返回给调用方。

ps:日常开发中，我们要有一定的安全意识，对于密码，金融数据等敏感信息进行加密存储保护。

这个需求说起来不是很难，我们只需要在执行 sql 之前，提前将指定数据进行加密。执行 sql 之后，获取返回结果，再进行的相应的解密。稍微改造下原有代码，很快完成需求。

![](https://pics1.baidu.com/feed/838ba61ea8d3fd1f6cddcef41e13da1797ca5f89.jpeg@f_auto?token=8f00141ca819db1c0026b4e2b6e05686)

现有加密算法如 RSA2 ，AES 等，密文长度将会是明文好几倍。上线加解密方案一定要评估数据库现有字段长度是否满足加密之后长度。

如果这是一张新建的表，上面的实现方案并没有什么问题。但是这次我们改造是几张已有已有**「千万级」**的存量的数据的表，这些数据都未被加密存储。

如果使用上述代码，使用加密之后的密文信息查询历史数据，当然查询不到任何结果。另外当查询返回的结果是明文，解密明文数据库也可能会导致相应的解密错误。

所以为了兼容历史数据，需要进行如下改造：

-   增加新字段存放对应的加密数据，sql 等值条件查询修改成 in 查询
    
-   查询返回的记录首先判断是否是密文，如果是密文再去解密
    

代码改造如下：

![](https://pics1.baidu.com/feed/42166d224f4a20a41a71a7caa10f672a720ed032.jpeg@f_auto?token=e9875717e6a263ba766908466e71f2b9)

上述代码虽然解决业务需求，但是这个解决方案不是很优雅，业务代码改动较大，加解密的代码不能通用，所有涉及到相关字段的方法都需要改动，且几乎都是重复代码，代码侵入性很强，不是很友好。

有经验的同学可能会想到使用 Spring AOP 解决上述问题。

在切面的前置方法**「beforeMethod」**统一拦截查询参数，配合自定义的注解，加密指定的字段。

然后在切面的后置方法**「afterReturn」**拦截返回值，配合自定义注解，解密指定的字段。

但是 Spring AOP 方案也并不通用，如果其他的应用也有相同的需求，同样的代码，又需要重复实现，还是很费时费力。

最终我们参考一个 github 开源项目**「typehandlers-encrypt」**，借助 mybatis 的 **「TypeHandler」**，实现通用的数据加解密解决方案。使用方只需要引入相关依赖，**「无需改动一行业务代码」**，仅需少量配置即可实现指定字段加解密操作，省时省力。

### 实现原理

mybatis 利用内置类型转换器（**「typeHandler」**），实现 Java 类型与 JDBC 类型的相互转换，我们正好可以利用这个特性，在转换之前加入加解密步骤。

`typeHandler` 底层原理不是复杂，如果我们没有使用 Mybatis，而是直接使用最原始的 JDBC 执行查询语句，相关代码如下：

![](https://pics5.baidu.com/feed/94cad1c8a786c917feb8619ffc608fc73ac75746.jpeg@f_auto?token=d6629159bdd72c02fd79cac383ded24e)

我们需要手动判断 Java 类型，然后调用 `PreparedStatement`设置合适类型参数。获取返回结果之后，又需要手动调用 `ResultSet` 结果集获取相应类型的数据，这个过程十分繁琐。

使用 mybatis 之后，上述步骤就无需我们再实现了。mybatis 可以通过识别 Java/JDBC 类型，调用相应，自动实现转换逻辑。

为 mybatis 内置类型转换器，基本涵盖了所有 **「Java/JDBC」** 数据类型。

![](https://pics6.baidu.com/feed/f603918fa0ec08faed3b67006db3c26554fbdac0.jpeg@f_auto?token=018a320925ed0f6e33db2f52a8bd7d4c)

### 通用解决方案

### 自定义 typeHandler

下面我们来实现带有加解密功能的类型转换器，实现方式也比较简单，只要继承 `org.apache.ibatis.type.BaseTypeHandler`，重写相关方法。

![](https://pics4.baidu.com/feed/b7fd5266d016092423ebb05fe45acaf2e7cd3409.jpeg@f_auto?token=e04cac8d4d08493d9e74b00f5deb095e)

其中加密转换将在 `setNonNullParameter` 中执行，解密转换将在 `getNullableResult`中执行。

`CryptTypeHandler` 使用一个 `MappedTypes` 注解，包含一个 `CryptType` 类，这个类使用 mybatis 别名功能，可以极大简化 sqlmap 相关配置。

![](https://pics6.baidu.com/feed/242dd42a2834349bd8f217f8e7b7eac637d3beb9.jpeg@f_auto?token=e95012ac71a1874651989d54d8499a6e)

### 注册 typeHandler

使用方必须将 和 `alias` 注册到 mybatis 中，否则无法生效。

下面提供三种方式,可以根据项目情况选择其中一种即可：

**「单独使用 mybatis」**

这种场景需要在 **「mybatis-config.xml」** 配置，mybatis 启动时将会加载该配置文件。

```
<typeHandlers> <!--类型转换器包路径--> <package name="com.xx.xx"/></typeHandlers> <!-- 别名定义 --><typeAliases> <!-- 针对单个别名定义 type:类型的路径 alias:别名 --> <typeAlias type="xx.xx.xx" alias="xx"/></typeAliases>
```

**「使用 Spring 配置 Mybatis Bean」**

配合 Spring 使用时需要将 注入 `SqlSessionFactoryBean` ，配置方式如下：

```
<!-- MyBatis 工厂 --><bean id="sqlSessionFactory" class="org.mybatis.spring.SqlSessionFactoryBean">   <property name="dataSource" ref= />   <!--alias 注入-->   <property name="typeAliasesPackage" value=/>   <!-- typeHandlers 注入   -->   <property name="typeHandlersPackage" value=/></bean>
```

**「SpringBoot」**

SpringBoot 方式就最简单了，只要引入 `mybatis-starter`，配置文件加入如下配置即可:

```
## mybatis 配置# 类型转换器包路径mybatis.type-handlers-package=com.xx.xx.xmybatis.type-aliases-package=com.xx.xx
```

### 修改 mapper sql 配置

最后我们只要简单修改 mapper 中 `resultMap` 或 sql s配置就可以实现加解密。

假设我们对现有一张 **「bank\_card」** 表进行加解密，表结构如下：

```
CREATE TABLE bank_card (id int primary key auto_increment,gmt_create timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP,gmt_update timestamp NOT NULL DEFAULT  ON UPDATE ,card_no varchar(256) NOT NULL DEFAULT '' COMMENT '卡号',phone varchar(256) NOT NULL DEFAULT '' COMMENT '手机号',name varchar(256) NOT NULL DEFAULT '' COMMENT '姓名',id_no varchar(256) NOT NULL DEFAULT '' COMMENT '证件号');
```

**「insert 加密」**

现需要对 `card_no`，`phone`，`name`，`id_no` 进行加密，**「insert」** 语句加密示例：

```
<insert id="insertBankCard" keyProperty="id" useGeneratedKeys="true" parameterType="org.demo.pojo.BankCardDO">  INSERT INTO bank_card (card_no, phone,name,id_no)  VALUES  (#{card_no,javaType=crypt},   #{phone,typeHandler=org.demo.type.CryptTypeHandler},   #{name,javaType=crypt},   #{id_no,javaType=crypt})</insert>
```

我们只需要在 **「#{}」** 指定 typeHandler，传入参数最后将被加密。使用 需要使用类的全路径，比较繁琐，我们可以使用 **「javaType」** 属性，直接使用上面我们的定义别名 **「crypt」**。

数据库最终执行sql 如下：

```
INSERT INTO bank_card (card_no, phone,name,id_no) VALUES ('NjQzMjEyMzEyMzE=', 'MTM1Njc4OTEyMzQ=', '5rWL6K+V5Y2h', 'MTIzMTIzMTIzMQ==');
```

> ps:推荐一款 IDEA 的插件 **「mybatis-log-plugin」**，可以自动将 mybatis sql 日志还原成真实执行 sql

**「查询加解密」**

普通查询解密示例如下：

```
<resultMap id="bankCardXml" type=>       <result property="card_no" column= typeHandler="org.demo.type.CryptTypeHandler"/>       <result property="name" column= typeHandler=/>       <result property="id_no" column= typeHandler=/>       <result property="phone" column= typeHandler=/></resultMap><select id="queryById" resultMap=>      select * from bank_card where id=#{id}</select>
```

这里我们在 **「select」** 配置中只能使用 属性，指定 。

数据库明文、密文共存的情况，查询解密示例如下：

```sql
<!-- resultMap 同上   -->
<select id="queryByPhone" resultMap=>    select * from bank_card where phone in(#{card_no,javaType=crypt},#{card_no})
</select>
```

最后我们可以将自定义的 单独打包发布，其他业务方只需要引用，改造相关配置文件，即可完成数据加解密。