## Spring-database项目简介
0、基于Springboot框架开发，基础了druid，Mybatis等开源框架

1、提供多数据源切换功能，使用spring AOP进行数据源的切换操作

2、提供了REST服务接口功能（后期需要Spring Security Oauth2.0 进行安全认证）

3、提供Mybatis持久化层

4、提供服务打包成tar.gz,可以直接进行打包，部署到服务器上即可

5、添加Spring security Oauth2.0 进行身份验证

6、通过mvn assembly.xml, 添加Wrapper打包功能，可直接打包发布

## Spring Security Oauth2.0的使用介绍：
   过程如下： 1、（获得access_token和refresh_token, GET或Post方法） http://127.0.0.1:8080/oauth/token?client_id=mobile_1&client_secret=secret_1&grant_type=password&username=aa&password=aa 
   2、（通过access_token进行访问，GET方法） http://localhost:8080/admin/ds1?access_token=${access_token} 或 http://localhost:8080/admin/ds1?access_token=${access_token} 
   3、（通过refresh_token 进行刷新token，GET 或 Post方法） http://localhost:8080/oauth/token?client_id=mobile_1&client_secret=secret_1&grant_type=refresh_token&refresh_token=${refresh_token}

注：在单机部署的环境下，将产生的token信息，直接保存到内存，便于单个节点访问，进行用户信息的认证。

<beans:bean id="tokenStore" class="org.springframework.security.oauth2.provider.token.store.InMemoryTokenStore" />

注：在集群的部署环境下，需要将产生的token信息，保存到数据库，便于集群中不同的服务节点，进行用户信息的认证。

<beans:bean id="tokenStore" class="org.springframework.security.oauth2.provider.token.store.JdbcTokenStore" > <beans:constructor-arg index="0" ref="dataSource"/> </beans:bean>

## Spring-database项目运行
1、mvn clean && mvn package -Dmaven.test.skip

2、编译成功后，会在 target目录下面生成一下代码

3、spring-database-1.0.0-assembly.tar.gz

4、直接上传到 Linux服务器上，配置好数据库信息 （详细参考 database1.sql 和database2.sql）

5、tar -zxvf spring-database-1.0.0-assembly.tar.gz

6、linux赋予文件运行权限

chmod -R u+x spring-database-1.0.0

7、启动服务：

 cd bin
 
./spring-database start
