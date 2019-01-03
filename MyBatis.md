###各种持久层框架的比较
- Hibernate

它具有很好的面向对象，提供了相应的映射，但是不是万能的，例如索引、存储过程、函数等，对数据库查询的性能有很大的帮助，可以优化sql 语句；当表的结构很复杂的时候，Hibernate 自动生成的sql 语句，也相应的更复杂，在一些大数据量、高并发的场景下，并不适合。

- Spring JDBC

严格的说，它并不能算是持久层框架，它只是使用模板对JDBC 封装，在它里面没有映射文件、对象查询语言，缓存的概念。

- Mybatis

我们是直接在配置文件中编写原生的sql语句，这给我们优化sql语句，提供了便利。由于使用原生的sql语句，它的数据库的可移植性就会降低。

###SqlSessionFactory 

每一个Mybatis 应用都必须要有一个是SqlSessionFactory实例，它是从SqlSessionFactoryBuilder去创建，这个SqlSessionFactory是从xml 配置文件中加载的一个实例。

###The configuration XML

配置文件是MyBatis的核心，包含了数据库连接对象信息、事务管理等配置。
    
      <?xml version="1.0" encoding="UTF-8"?>
    <!DOCTYPE configuration
      PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
      "http://mybatis.org/dtd/mybatis-3-config.dtd">//配置标签文件
    <configuration>
    	<environments default="development">
    		<environment id="development">
    			<transactionManager type="JDBC">//指定Mybatis的事务类型
    			</transactionManager>
    			<dataSource type="POOLED">//配置数据源
    				<property name="driver" value="com.mysql.jdbc.Driver"></property>
    				<property name="url" value="jdbc:mysql://localhost:3306/mybatistest"></property>
    				<property name="username" value="root"></property>
    				<property name="password" value="123456"></property>
    			</dataSource>
    		</environment>
    	</environments>
    	<typeAliases >
		<!-- //设置别名，使用user 就代表com.example.test.javabean.User 该类 -->
		<typeAlias type="com.example.test.javabean.User" alias="user"/>
		</typeAliases>
		<mappers>
	    <!-- 设置映射路径，因为是在类路径（也就是src下），如果是在其他包下，必须去设置文件目录如:com/example/xxx.xml -->
		<mapper resource="UserMapper.xml"></mapper>
		</mappers>
    </configuration>

这里只是指出了配置文件中比较重要的配置。其他的用到的时候在进行讲解。

这里配置Mybatis配置文件，还可以通过Java代码去进行配置，这里还是推荐使用xml。

###加载MyBatis的配置文件

如果配置文件在src ，也就是类路径下，会自动进行加载。

如果配置在其他的路径下，可以通过通用类Resources，通过流去读取：

    String resource = "org/mybatis/example/mybatis-config.xml";
    InputStream inputStream = Resources.getResourceAsStream(resource);
    SqlSessionFactory sqlSessionFactory =
    new SqlSessionFactoryBuilder().build(inputStream);

