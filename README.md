## 简介

基于[SpringBoot](https://github.com/spring-projects/spring-boot)搭建的开源个人博客系统，前台界面基于 Hexo 主题[hexo-theme-gal](https://github.com/ZEROKISEKI/hexo-theme-gal)进行修改，管理后台界面基于[vue-element-admin](https://github.com/PanJiaChen/vue-element-admin)进行修改。

技术栈：SpringBoot、Thymeleaf、MySQL、MyBatis-Plus、Lombok、Gson、caffeine、validation、Bootstrap、jQuery、FontAwesome、Jsoup……

示例博客：[周华个人博客](https://www.iszhouhua.com)

## 快速开始

1. 下载本项目，并使用 IDE 打开
2. 新建数据库 blog 并运行项目

   > 现在运行项目会自动运行 SQL 脚本建表和插入初始数据

3. 修改`application-dev.yml`中的数据库配置信息
4. 运行`BlogApplication.java`，启动项目
5. 浏览器访问`http://127.0.0.1:8080/`

> 使用 Idea，Eclipse 等 IDE 运行需要安装 Lombok 插件，JDK 版本要求 1.8+。

## 部署

### jar 部署

配置好`application-prod.yml`中的配置信息，然后打包：

```bash
mvn clean package -Dmaven.test.skip=true
```

将打包好的`blog.jar`和`blog.sh`放到同一文件夹下，执行命令：

```bash
# 使脚本具有执行权限
chmod +x ./blog.sh
# 启动项目
./blog.sh start
# 或者直接使用sh命令运行脚本
sh blog.sh start
```

### tomcat 部署

修改`application.yml`中`spring.profiles.active`为`prod`，并配置好`application-prod.yml`中的配置信息。

直接修改`pom.xml`中的打包方式为 war 后进行打包，或直接运行命令：

```bash
clean package war:war -Dmaven.test.skip=true
```

然后将打包好的`blog.war`丢进 tomcat 中运行即可！

### docker 部署

配置好`application-prod.yml`中的配置信息，然后执行`build-docker.sh`：

```bash
# docker打包
sh build-docker.sh
# 运行项目
docker run -d --name blog -p 8080:8080 --add-host=host.docker.internal:host-gateway -v /data/logs:/app/logs -v /data/upload:/app/src/main/resources/static/upload blog
```

- --add-host=host.docker.internal:host-gateway: 使镜像可通过 host.docker.internal 连接到宿主机的端口
- -v /data/logs:/app/logs: 日志挂载
- -v /data/upload:/app/src/main/resources/static/upload 上传图片挂载，非本地存储无需挂载

> 注：build-docker.sh 脚本会自动将 vue 代码也编译进 docker 镜像中，无需单独处理 vue 的内容

## 后台管理

后台采用前后端分离的方式实现，源码位于 vue 文件夹下<https://github.com/iszhouhua/blog/tree/master/vue>

---
