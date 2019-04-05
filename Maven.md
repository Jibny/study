### Maven

#### maven使用为了解决jar依赖冲突，便于管理，其次增加了jar包的复用性

#### 一.安装步骤

##### 1.下载http://maven.apache.org/download.cgi

bin的是可执行包，src是源码

##### 2.解压完配置MAVEN_HOME以及path环境变量（和jdk差不多）

cmd

mvn -version

##### 3.maven的本地仓库repository

D:\WebPath\apache-maven-3.6.0\conf\settings中默认目录Default: ${user.home}/.m2/repository中找jar包

jar包-->本地仓库-->远程仓库(局域网私服)-->中央仓库

##### 4.仓库换源

```
<mirrors>
    <mirror>
        <id>aliyun-public</id>
        <mirrorOf>*</mirrorOf>
        <name>aliyun public</name>
        <url>https://maven.aliyun.com/repository/public</url>
    </mirror>
    <mirror>
        <id>aliyun-central</id>
        <mirrorOf>*</mirrorOf>
        <name>aliyun central</name>
        <url>https://maven.aliyun.com/repository/central</url>
    </mirror>
    <mirror>
        <id>aliyun-spring</id>
        <mirrorOf>*</mirrorOf>
        <name>aliyun spring</name>
        <url>https://maven.aliyun.com/repository/spring</url>
    </mirror>
    <mirror>
        <id>aliyun-spring-plugin</id>
        <mirrorOf>*</mirrorOf>
        <name>aliyun spring-plugin</name>
        <url>https://maven.aliyun.com/repository/spring-plugin</url>
    </mirror>
    <mirror>
        <id>aliyun-apache-snapshots</id>
        <mirrorOf>*</mirrorOf>
        <name>aliyun apache-snapshots</name>
        <url>https://maven.aliyun.com/repository/apache-snapshots</url>
    </mirror>
    <mirror>
        <id>aliyun-google</id>
        <mirrorOf>*</mirrorOf>
        <name>aliyun google</name>
        <url>https://maven.aliyun.com/repository/google</url>
    </mirror>
    <mirror>
        <id>aliyun-gradle-plugin</id>
        <mirrorOf>*</mirrorOf>
        <name>aliyun gradle-plugin</name>
        <url>https://maven.aliyun.com/repository/gradle-plugin</url>
    </mirror>
    <mirror>
        <id>aliyun-jcenter</id>
        <mirrorOf>*</mirrorOf>
        <name>aliyun jcenter</name>
        <url>https://maven.aliyun.com/repository/jcenter</url>
    </mirror>
    <mirror>
        <id>aliyun-releases</id>
        <mirrorOf>*</mirrorOf>
        <name>aliyun releases</name>
        <url>https://maven.aliyun.com/repository/releases</url>
    </mirror>
    <mirror>
        <id>aliyun-snapshots</id>
        <mirrorOf>*</mirrorOf>
        <name>aliyun snapshots</name>
        <url>https://maven.aliyun.com/repository/snapshots</url>
    </mirror>
    <mirror>
        <id>aliyun-grails-core</id>
        <mirrorOf>*</mirrorOf>
        <name>aliyun grails-core</name>
        <url>https://maven.aliyun.com/repository/grails-core</url>
    </mirror>
    <mirror>
        <id>aliyun-mapr-public</id>
        <mirrorOf>*</mirrorOf>
        <name>aliyun mapr-public</name>
        <url>https://maven.aliyun.com/repository/mapr-public</url>
    </mirror>
</mirrors>
```

#### 二.Maven目录结构和常用命令

##### 目录结构

核心代码部分（打包成jar包，发布成产品，供用户使用）

配置文件部分（避免不断升级时重新打包，频繁修改部分）

测试代码部分（单元测试部分）

测试配置文件部分



Maven项目结构

    src/main/java 核心代码部分
    src/main/resources 配置文件部分
    src/test/java 测试代码部分
    src/test/resources 测试配置文件
    
    web项目中
    src/main/webapp 页面资源,js，css，图片资源...


##### 常用命令

进入到项目根目录

mvn clean	修改了代码后用这个清除原来target

mvn compile	编译src/main/java 核心代码部分到classes

mvn test	编译src/main/java到classes && 编译src/test/java到test-classes里

mvn package	打包成war包，pom.xml中设置 <package>war</package>

mvn install	相当于mvn compile+mvn test+mvn package，再把war复制进本地仓库



#### 三.Maven的生命周期以及概念模型

清除编译信息	|	编译		测试	打包		安装 	   发布

​	clean      	|	compile          test        package          install	 deploy

 清理生命周期       |       	 默认生命周期（执行后面命令前面自动执行了一遍）

每一个构建项目的信息都对应底层的一个插件



##### 概念模型

![image](https://raw.githubusercontent.com/Jibny/study/master/picture/1554389185290.png)

pom.xml（项目对象模型）

项目自身描述信息

项目运行依赖jar包信息<dependencies></dependencies>

项目构建环境信息<build></build>



Dependency（依赖管理模型）

	<dependency>
		
			<groupId>javax.servlet.jsp</groupId>	//公司组织名称
			<artifactId>jsp-api</artifactId>		//项目名
			<version>2.1</version>					//版本号
			<scope>provided</scope>			//构件包ProjectABC.war后，在其下的WEB-INF/lib中
											//会包含我们被标注为scope=compile的构件的jar包，而不会包</dependency>						 //含我们被标注为scope=provided的构件的jar包。这也避免了										  //此类构件当部署到目标容器后产生包依赖冲突
	  <build>
	    <plugins>
	      <plugin>
	        <groupId>org.apache.tomcat.maven</groupId>
	        <artifactId>tomcat7-maven-plugin</artifactId>
	        <version>2.2</version>
	        <configuration>
	          <port>8888</port>
	        </configuration>
	      </plugin>
	      <plugin>
	          <groupId>org.apache.maven.plugins</groupId>
	          <artifactId>maven-compiler-plugin</artifactId>
	          <configuration>
	            <target>1.8</target>
	            <source>1.8</source>
	            <encoding>UTF-8</encoding>
	          </configuration>
	        </plugin>
	    </plugins>
	  </build>


####  四.IDEA配置Maven

File-->settings-->Maven中 Maven home directory和user settings file

File-->settings-->Maven-->runner 中 VM Options:-DarchetypeCatalog=internal（没网时本地创建Maven工程）

如果不用maven中自带tomcat插件run:tomcat的话，还应该在本地tomcat配置中build输出war包

##### 创建maven工程

选择骨架创建

![image](https://raw.githubusercontent.com/Jibny/study/master/picture/1554457790305.png)

空的maven项目需要自己新建添加资源目录





























