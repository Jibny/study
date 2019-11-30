---
title: SAM中Restful接口开发
date: 2019-08-14 19:57:13
categories:
	project
tags:
	SAM-API
cover: http://r.photo.store.qq.com/psb?/V13Zm3q236IRIM/*PeCzHzhx2hyKKTXBrfPh2xQ1xGb9mP9vCO4mS1ydWQ!/r/dLgAAAAAAAAA
mp3: https://api.uomg.com/api/rand.music
---

# 1.SAM端API接口

Fixed Account 账号认证上网模块

![img](https://cdn.jsdelivr.net/gh/Jibny/study/picture/SAMAPI/SAMAPI1.png)

![img](https://cdn.jsdelivr.net/gh/Jibny/study/picture/SAMAPI/SAMAPI2.png)



参考profile配置模板项目调用关系

![img](<https://cdn.jsdelivr.net/gh/Jibny/study/picture/SAMAPI/SAMStruct.png>)

​	

## 1.1API规范

**API****请求地址规范：**

采用26个英文小写字母，英文单词之间采用“_”连接。

例：GET请求

http://server_ip:port/sam-boot/api/macc/account/get/{uuid}?access_token=token_for_test_ABCDEFG&ishttps=false&tenantId=1

 

**API****请求请求参数及返回参数规范：**

Ø  均使用Json对象格式传送

Ø  字段名称采用驼峰法。

Ø  字段命名使用正确的英文单词，并尽量正确表达该字段的含义。

例：新建网络请求，POST请求（注意红色字段值均为驼峰法）

 





# 2.     API开发

## 2.1 Rest实现(Web)

### 2.1.1 Spring-cxf.xml配置

 

根据url确定，该接口实现为Fixed Account模块，所以该接口在sam-macc中实现

其中 address=”/macc” 表示该server地址路径

![img](https://cdn.jsdelivr.net/gh/Jibny/study/picture/SAMAPI/SAMAPI3.png)

 

### 2.1.2 AccountRest类实现

 

![img](https://cdn.jsdelivr.net/gh/Jibny/study/picture/SAMAPI/SAMAPI4.png)

 

 

### 2.1.3    Spring-Dubbo.xml配置

调用common.dubbo.provider中定义好的方法将数据从SAM中传过来

![img](https://cdn.jsdelivr.net/gh/Jibny/study/picture/SAMAPI/SAMAPI5.png)

 

## 2.2 AccountService类实现（Service）

### 2.2.1 对BeanPo封装

对于SAM中的FixedAccount实体bean过滤不需要要的属性

![img](https://cdn.jsdelivr.net/gh/Jibny/study/picture/SAMAPI/SAMAPI6.png)

 

### 2.2.2    AccountService类实现

实现业务逻辑方便2.1.2中Rest中调用，返回响应

![img](https://cdn.jsdelivr.net/gh/Jibny/study/picture/SAMAPI/SAMAPI7.png)

 

 

## 2.3 common模块中定义服务（DAO）

### 2.3.1 定义提供服务接口

Dubbo分布式提供服务原理

![img](https://cdn.jsdelivr.net/gh/Jibny/study/picture/SAMAPI/SAMAPI8.png)

![img](https://cdn.jsdelivr.net/gh/Jibny/study/picture/SAMAPI/SAMAPI9.png)

### 2.3.2 Data中注册服务xml配置

![img](https://cdn.jsdelivr.net/gh/Jibny/study/picture/SAMAPI/SAMAPI10.png)

 

### 2.3.3 实现2.21provider接口服务

![img](https://cdn.jsdelivr.net/gh/Jibny/study/picture/SAMAPI/SAMAPI11.png)

 

### 2.3.4 新增Dao中sql操作

![img](https://cdn.jsdelivr.net/gh/Jibny/study/picture/SAMAPI/SAMAPI12.png)

 

 

 

# 3.API测试

使用Postman进行测试，软件自行百度安装

打开Postman 后可以导入如下链接：

<https://www.getpostman.com/collections/065a4e6acc8c04e43fbe>

 

注意：增加和修改应该加上提交表单FixAccountPo对象

![img](https://cdn.jsdelivr.net/gh/Jibny/study/picture/SAMAPI/SAMAPI13.png)

## 3.1 查询

http://server_ip:port/sam-boot/api/macc/account/get/{uuid}?access_token=token_for_test_ABCDEFG&ishttps=false&tenantId=1



http://localhost:8081/sam_boot_war_exploded/api/macc/account/get/iIemrWuXvlfghehCLUyygKkaERuhjYcR?access_token=token_for_test_ABCDEFG&ishttps=false&tenantId=1

![img](https://cdn.jsdelivr.net/gh/Jibny/study/picture/SAMAPI/SAMAPI14.png)

 

 

 

 

 

## 3.2 增加

http://server_ip:port/sam-boot/api/macc/account/create/{tenantName}/{userName}/{groupId}?access_token=token_for_test_ABCDEFG&ishttps=false&tenantId=1

 

http://localhost:8081/sam_boot_war_exploded/api/macc/account/create/super_tenant/admin/186?access_token=token_for_test_ABCDEFG&ishttps=false&tenantId=1

![img](https://cdn.jsdelivr.net/gh/Jibny/study/picture/SAMAPI/SAMAPI15.png)

![img](https://cdn.jsdelivr.net/gh/Jibny/study/picture/SAMAPI/SAMAPI16.png)

 

需要账号同步，才能新增

![img](https://cdn.jsdelivr.net/gh/Jibny/study/picture/SAMAPI/SAMAPI17.png)

![img](https://cdn.jsdelivr.net/gh/Jibny/study/picture/SAMAPI/SAMAPI18.png)

 

 

 

## 3.3 删除

http://server_ip:port/sam-boot/api/macc/account/delete/{uuid}?access_token=token_for_test_ABCDEFG&ishttps=false&tenantId=1



http://localhost:8081/sam_boot_war_exploded/api/macc/account/delete/81540331814175274503276383691486?access_token=token_for_test_ABCDEFG&ishttps=false&tenantId=1

![img](https://cdn.jsdelivr.net/gh/Jibny/study/picture/SAMAPI/SAMAPI19.png)

![img](https://cdn.jsdelivr.net/gh/Jibny/study/picture/SAMAPI/SAMAPI20.png)

## 3.4 修改

http://server_ip:port/sam-boot/api/macc/account/update/{tenantName}/{userName}/{groupId}?access_token=token_for_test_ABCDEFG&ishttps=false&tenantId=1

 

http://localhost:8081/sam_boot_war_exploded/api/macc/account/update/super_tenant/admin/186?access_token=token_for_test_ABCDEFG&ishttps=false&tenantId=1

 

![img](https://cdn.jsdelivr.net/gh/Jibny/study/picture/SAMAPI/SAMAPI21.png)

 

 