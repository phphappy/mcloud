# MCloud - 微服务基础设施
[![Build Status](https://www.travis-ci.org/heyuxian/mcloud.svg?branch=master)](https://www.travis-ci.org/heyuxian/mcloud)
[![Coverage Status](https://coveralls.io/repos/github/heyuxian/mcloud/badge.svg?branch=master)](https://coveralls.io/github/heyuxian/mcloud?branch=master)
## 项目简介

MCloud 基于Spring Cloud进行开发，提供了项目中常用的基础设施：

- **mcloud-eureka** 服务注册与发现中心。
- [**mcloud-oauth-server**](https://github.com/heyuxian/mcloud-oauth2-server) 基于Spring OAuth2实现的OAuth2认证服务端，其它服务需要依赖此服务进行认证。
- **mcloud-uia** API 统一登录中心。
- **mcloud-apigw** 基于Spring cloud zuul 实现的api网关 。
- **mcloud-config** 统一配置中心。
- **mcloud-monitoring** 基于 Spring boot admin 实现系统监控。
- **mcloud-file-storage** 文件存储中心。
- **mcloud-logs** 基于 `Kafka` 以及 `ElasticSearch` 实现服务的日志分析。
- **mcloud-blog** Demo Project

其他模块：

- [mcloud-parent](https://github.com/heyuxian/mcloud-parent) maven 公用依赖。
- [mcloud-common](https://github.com/heyuxian/mcloud-common) 项目公用工具类。
- [mcloud-data](https://github.com/heyuxian/mcloud-data) 数据存储相关。
- [mcloud-web](https://github.com/heyuxian/mcloud-web) web相关依赖及公共类。
- [Code Generator](https://github.com/heyuxian/code-generator) 用于 Intellij-IDEA 的代码生成器插件。

UI界面:

- 基于 [AdminBSBMaterialDesign](https://github.com/gurayyarar/AdminBSBMaterialDesign) ，使用 `thymeleaf` 实现的后台管理界面。
- [mcloud-blog-ui](https://github.com/heyuxian/mcloud-blog-ui) 基于[CoPilot](https://github.com/misterGF/CoPilot) ，使用 `node` + `vue`实现的博客前端。 

## 环境依赖

- **JDK** 1.8 以上
- **IDE** 请安装对应IDE的**lombok**插件
- **数据库** 使用flywaydb进行数据库脚本的版本管理，需执行flywaydb的相关maven命令


## 快速使用

**下载项目**

```
git clone https://github.com/heyuxian/mcloud.git
cd 项目目录/mcloud
```

**创建数据库**

使用mysql客户端或其它你喜欢的工具创建数据库(默认数据库名称为db_blog):

```shell
CREATE DATABASE IF NOT EXISTS db_blog DEFAULT CHARSET utf8 COLLATE utf8_general_ci;  
```

**使用 flywaydb 初始化数据库**

- mcloud-blog/pom.xml

```xml
<plugin>
  <groupId>org.flywaydb</groupId>
  <artifactId>flyway-maven-plugin</artifactId>
  <version>4.2.0</version>
  <configuration>
    <user>root</user>
    <password>root</password>
    <driver>com.mysql.jdbc.Driver</driver>
    <url>jdbc:mysql://localhost:3306/db_blog</url>
  </configuration>
</plugin>
```

修改Spring 配置文件中的数据库用户名及密码:

- mcloud-blog: application-dev.yml

执行flywaydb相关命令初始化数据库：

```shell
mvn flyway:clean flyway:migrate
```

**启动OAuth Server:**   [详细配置](https://github.com/heyuxian/mcloud-oauth2-server)

```
git clone https://github.com/heyuxian/mcloud-oauth2-server
mvn clean install
mvn flyway:clean flyway:migrate
mvn spring-boot:run
```

访问地址: http://localhost:8043/uaa/swagger-ui.html

**启动认证中心:**  [详细配置](mcloud-uia/README.md)

```
cd mcloud-uia
mvn clean install
mvn spring-boot:run
```
访问地址: http://localhost:8443/uia/swagger-ui.html 

**启动博客服务:** [详细配置](mcloud-blog/README.md)

```
cd mcloud-blog
mvn clean install
mvn spring-boot:run
```
访问地址: http://localhost:8081/swagger-ui.html 

## 问题及建议

若是对于本项目有任何问题或建议,请提[Issue](https://github.com/heyuxian/mcloud/issues/new)。同时,如果你愿意参与开发,欢迎提PR.

## License

```
Copyright 2017 http://www.javaroad.me

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
```
