
﻿
一些特殊场景下应用需要分别访问两个数据源实现业务功能。
Spring Boot可以通过指定数据源配置来实现。
具体做法如下：
建立两个数据源配置，分别对应不同的mybatis mapper上。
注意：数据源配置建立在启动类的包下面，这样能自动加载上。



注意数据源maser和数据源second中对应的mybatis映射需要在不通的dao下面，并且这些dao目录没有父子/交集关系。
比如：master对应的是com.test.dao，secnod对应的是com.test.dao.second，则master会覆盖second，这样是错误的；必须设置成没有交集，将master的改为com.test.dao.master。




数据源代码自动化添加好后，就是添加数据源配置项：
注意password可以用“{cipher}加密”这种方式来进行加密解密。
#主数据源
spring.datasource.driverClassName=com.mysql.jdbc.Driver
spring.datasource.url=jdbc:mysql://127.0.0.1:3306/rwl_test
spring.datasource.username=root
spring.datasource.password=root

#第二数据源
spring.datasource.second.driverClassName=com.mysql.jdbc.Driver
spring.datasource.second.url=jdbc:mysql://127.0.0.1:3306/rwl_test2
spring.datasource.second.username=root
spring.datasource.second.password=root

注意事务控制：
默认的@Transactional控制的是第一个数据源的事务，数据源2的事务是@Transactional("secondTransactionManager")


