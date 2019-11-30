---
title: Jenkins搭建-简单使用
date: 2019-08-20 14:52:30
categories:
	Jenkins
tags:
	Jenkins
cover: http://r.photo.store.qq.com/psb?/V13Zm3q236IRIM/ylOpNCMFHaniFkfdtToodrPBqngZmuHOK.RAN0lWWrY!/r/dL8AAAAAAAAA
mp3: https://api.uomg.com/api/rand.music
---

### Jenkins搭建&数据备份&简单使用

通过获取代码仓库中最新代码，进行自动化部署，而省去手动打包、上传服务器、部署这一系列步骤

https://jenkins.io/ 官网下载最新版本Jenkins.war

#### 1.准备软件，安装jenkins

- ​	jdk-8u221-linux-x64.tar.gz
- ​	apache-maven-3.3.9-bin.tar.gz
- ​    apache-tomcat-8.5.43.tar.gz
- ​	nginx-1.16.0.tar.gz

解压压缩包，配置/usr/profile环境变量

```bash
tar -zxvf jdk-8u221-linux-x64.tar.gz -C /usr/local
tar -zxvf apache-maven-3.3.9-bin.tar.gz -C /usr/local
tar -zxvf apache-tomcat-8.5.43.tar.gz -C /usr/local
tar -zxvf nginx-1.16.0.tar.gz -C /usr/local
```

环境变量

```bash
export JAVA_HOME=/usr/local/jdk1.8.0_221
export CLASSPATH=$:CALSSPATH:$JAVA_HOME/lib/
export PATH=$PATH:$JAVA_HOME/bin

export MAVEN_HOME=/usr/local/apache-maven-3.3.9
export PATH=${MAVEN_HOME}/bin:$PATH
```

将jenkins.war放入Tomcat的webapps目录下，运行tomcat

```bash
cp jenkins.war /usr/local/apache-tomcat-8.5.43/webapps/
cd /usr/local/apache-tomcat-8.5.43/bin
./startup.sh
```

浏览器访问http://目的ip:8080/jenkins

![image](https://cdn.jsdelivr.net/gh/Jibny/study/picture/jenkins1565683483075.png)

从服务器cat /root/.jenkins/secrets/initialAdminPassword 查看密码输入

#### 

如果卡在登入界面，修改源重启tomcat

```bash
vim /root/.jenkins/hudson.model.UpdateCenter.xml
#把http://updates.jenkins-ci.org/update-center.json改成http://mirror.xmission.com/jenkins/updates/update-center.json

vim /root/.Jenkins/updates/default.json
#把www.google.com改成www.baidu.com
```

#### 2.数据迁移

进入要迁移数据的主机

打包jenkins目录下的工作文件和配置文件

拷贝到新主机再重启tomcat服务器



注：jenkins的工作目录地址配置文件在jenkins/config.xml中

 

```bash
tar -zcvf /home/jenkins.tar.gz /install/jenkins 
```

scp root@要拷贝的主机IP:/home/jenkins.tar.gz /home/jenkins

```bash
scp root@172.18.24.207:/home/jenkins.tar.gz /home/jenkins

#将文件解压
tar -zxvf jenkins.tar.gz -C /home

#修改配置文件里面jenkins/config.xml里面工作空间
<workspaceDir>${JENKINS_HOME}/workspace/${ITEM_FULL_NAME}</workspaceDir>
 <buildsDir>${ITEM_ROOTDIR}/builds</buildsDir>

#重启服务器
 cd /usr/local/apache-tomcat-8.5.43/bin
./startup.sh
```

#### 3.配置nignx反向代理（单台jenkins可以不用配置）

解压nignx，配置/etc/nginx/nginx.conf，启动nginx

```bash
tar -zxvf nginx-1.16.0.tar.gz -C /usr/local/

#安装nginx依赖
yum install curl-devel expat-devel gettext-devel openssl-devel zlib-devel
yum install  gcc perl-ExtUtils-MakeMaker

cd /usr/local/nginx-1.16.0
#编译安装
./configure
make && make install

#修改配置文件，添加下面一段进去
vim /etc/nginx/nginx.conf

 server {
        listen       80;
        server_name  localhost;
        #access_log /var/log/jenkins_access_log main;
        #error_log  /var/log/jenkins_error_log  debug_http;
        client_max_body_size 60M;
        client_body_buffer_size 512k;
        location / {
            proxy_pass      http://localhost:8080/jenkins;
            proxy_redirect  off;
            proxy_set_header Host $host;
            proxy_set_header X-Real-IP $remote_addr;
            proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
         }
     }

#测试配置成功
nginx -t
#进入nginx可执行目录sbin下
./nginx start
```

注:Jenkins URL需要配置成自己IP![image](https://cdn.jsdelivr.net/gh/Jibny/study/picture/jenkins1565693461526.png)

#### 4.git安装

```bash
#前面有安装过就不用了
yum install curl-devel expat-devel gettext-devel openssl-devel zlib-develyum install  gcc perl-ExtUtils-MakeMaker

# 将陈旧版本的git删除
yum remove git

#进入下载的保存位置
cd /usr/local/src
# 进行下载
wget https:#mirrors.edge.kernel.org/pub/software/scm/git/git-2.19.0.tar.gz
# 之后解压
tar -zxvf git-2.19.0.tar.gz
#编译安装，进入解压的文件夹
cd git-2.19.0
#编译源码
make prefix=/usr/local/git all
# 安装至指定目录
make prefix=/usr/local/git install
# 打开环境变量配置文件。
vim /etc/profile
# 在文件底部添加以下配置
PATH=$PATH:/usr/local/git/bin   # git 的目录
export PATH
# 刷新环境变量
source /etc/profile
#再查看git的版本
git --version
#这是git的版本已经变成了2.19.0
git version 2.19.0

```

创建git用户，不建议root用户直接使用（新增git账号其实就是添加一个系统用户，可以设置权限）

```bash
adduser git
passwd git1234566
chmod 740 /etc/sudoers
vim /etc/sudoers
#打开上面的文件后找到
root    ALL=(ALL)       ALL
#在它的后面新增一句
git ALL=(ALL) ALL
#保存并退出
:wq

# 将权限修改回来
chmod 400 /etc/sudoers

```

可以测试使用git

```bash
# 注意哦，这句是在本地机器（如windows电脑上）执行的，本地机器也要安装git
mkdir ~/.ssh

# 进入该目录下执行
ssh-keygen -t rsa
# 一路回车，就会生成如下的文件
会生成一个id_rsa.pub的公钥,将里面的内容复制后，切换到远程控制端的git用户，在远程控制端创建.ssh文件夹 和.ssh/authorized_keys文件，打开authorized_keys文件并将刚才在本地机器复制的内容拷贝其中并保存

#登入刚刚的git服务器，将复制的RSA公钥粘贴进~/.ssh/authorized_keys
su git
mkdir ~/.ssh
vim ~/.ssh/authorized_keys


#yourIp为远程服务器的ip地址，免密登入成功
ssh -v git@yourIp

```



#### 5.Jenkins的使用

简单创建Hello World流水线

https://jenkins.io/zh/doc/pipeline/tour/hello-world/