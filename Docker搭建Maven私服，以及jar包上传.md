### Docker搭建Maven私服，以及jar包上传

#### 1-Docker安装

```bash
 #通过 **uname -r** 命令查看你当前的内核版本，内核版本要高于3.10
 $ uname -r
 
 #使用 root 权限登录 Centos。确保 yum 包更新到最新。
 $ sudo yum update
 
 #卸载旧版本(如果安装过旧版本的话)
 $ sudo yum remove docker  docker-common docker-selinux docker-engine
 
 #安装需要的软件包， yum-util 提供yum-config-manager功能，另外两个是devicemapper驱动依赖的
 $ sudo yum install -y yum-utils device-mapper-persistent-data lvm2
 
 #设置yum源
 $ sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
 
 #可以查看所有仓库中所有docker版本，并选择特定版本安装
 $ yum list docker-ce --showduplicates | sort -r
 
 #安装docker，例如sudo yum install docker-ce-17.12.1.ce
 $ sudo yum install <FQPN>
 
 #启动并加入开机启动
 $ sudo systemctl start docker
 $ sudo systemctl enable docker
 
 #验证安装是否成功(有client和service两部分表示docker安装启动都成功了)
 $ docker version

```

#### 2-Docker安装nexus

```bash
 #搜索镜像
 $ docker search nexus;

 #拉取nexus镜像,选stars多的
 $ docker pull sonatype/nexus; 
 
 #运行pull的nexus
-id 创建守护式容器
--privileged=true 授予root权限（挂载多级目录必须为true，否则容器访问宿主机权限不足）
--name=名字 给你的容器起个名字
-p 宿主机端口：容器端口映射
-v 宿主机目录：容器目录 目录挂载

docker run -d -p 8081:8081 --name nexus -v /root/nexus-data:/var/nexus-data --restart=always sonatype/nexus3


```

sonatype/nexus3.0以后密码文件查看，进入容器，cat /nexus-data/admin.password

```bash
 #docker常用命令
 $ docker ps					#查看运行实例 
 $ docker ps -a				#查看全部实例
 $ docker inspect 容器id		   #查询容器信息
 $ docker stop/start 容器id 	   #停止/开始容器id
 $ docker rm 容器id 			   #删除容器id
 $ docker exec -it 容器id bash  #进去容器内部 Exit退出
 $ docker stop nexus  			#停止nexus
 $ docker start nexus 			#启动nexus 启动时间大约1分钟
 $ docker cp 容器ID/容器name:容器目录 当前宿主机的文件  	#文件从容器复制到宿主机
 $ docker cp 当前宿主机的文件 容器ID或者容器name:容器目录		#宿主机文件到容器
 
```



#### 3-访问nexus

http://172.31.193.203:8081/  #http://私服ip:8081/

点击右上方的`Sign in`进行登录，初始账号密码为前面进容器看的一长串哈希值，登录后修改密码

nexus3.0 以上版本，没有内置的3rd_part,所以不支持直接在界面上传jar包

可以手动创建一个3rd_part，也可以直接用maven-pubic（反正私服局域网）

![img](https://cdn.jsdelivr.net/gh/Jibny/study@master/picture/nexus3.1.png)

#### 4-配置本地Maven的settings.xml

```xml
  <servers>
    <!--ID名字随意，需要和下面pom.xml一样，账号密码和nexus创建user一样，admin管理员-->
	<server>
      <id>deploy-release</id>
      <username>admin</username>
      <password>admin123</password>
    </server>
    <server>
      <id>deploy-snapshot</id>
      <username>admin</username>
      <password>admin123</password>
    </server>
      
  
    <!-- 私服地址 -->
  	<mirror>
          <id>deploy-release</id>
          <mirrorOf>central</mirrorOf>
          <name>deploy central</name>
          <url>http://172.31.193.203:8081/repository/maven-public/</url>
    </mirror>
    
```

​	

#### 5-配置pom.xml测试打包上传jar包

distributionManagement将jar包推到指定的远程仓库

```xml
	<distributionManagement>
		<repository>
            <!-- id要和settings.xml中server的一致 -->
			<id>deploy-release</id>
			<url>http://172.31.193.203:8081/repository/maven-releases/</url>
		</repository>

		<snapshotRepository>
			<id>deploy-snapshot</id>
			<url>http://172.31.193.203:8081/repository/maven-snapshots/</url>
		</snapshotRepository>
	</distributionManagement>

	<build>
		<plugins>
			<!--发布代码Jar插件-->
			<plugin>
				<groupId>org.apache.maven.plugins</groupId>
				<artifactId>maven-deploy-plugin</artifactId>
				<version>2.7</version>
			</plugin>
			<!--发布源码插件-->
			<plugin>
				<groupId>org.apache.maven.plugins</groupId>
				<artifactId>maven-source-plugin</artifactId>
				<version>2.2.1</version>
				<executions>
					<execution>
						<phase>package</phase>
						<goals>
							<goal>jar</goal>
						</goals>
					</execution>
				</executions>
			</plugin>
			<plugin>
				<groupId>org.springframework.boot</groupId>
				<artifactId>spring-boot-maven-plugin</artifactId>
			</plugin>
		</plugins>
	</build>
```

IDEA-run deploy（IDEA中将jar包推送到maven私服）

![image](https://cdn.jsdelivr.net/gh/Jibny/study/picture/IDEA-uploadjar.png)

Eclipse-run deploy（Eclipse中将jar包推送到maven私服）

run as ==> maven build ==> Goals:clean package deploy ==> run

![image](https://cdn.jsdelivr.net/gh/Jibny/study@master/picture/Eclipse-uploadjar.png)



#### 6-测试jar包

访问http://主机ip:8081/service/rest/repository/browse/maven-public/

![image](https://cdn.jsdelivr.net/gh/Jibny/study@master/picture/testjardependency.png)



将右边dependency导入本地项目pom.xml依赖中替换本地依赖























