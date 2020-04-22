---

---

# Maven介绍

可以用于构建和管理任何基于Java的项目的工具

## maven解决问题？

1.jar包冲突

2.maven管理单元测试一次完成，运行来检验代码质量

3.maven管理WEB项目部署

## maven依赖管理

maven工程来构建，会发现总体上工程的大小会少很多。

![](..\img\maven05.png)

![](...\img\maven01.png)

**核心功能**

 1、依赖管理：maven工程队jar包的管理过程/

 2、项目一键构建 

```
mvn tomcat:run
```

## 安装maven

http://maven.apache.org/download.cgi

1、环境变量设置

```
![maven02](..\img\maven02.png)MAVEN_HOME

D:\apache\apache-maven-3.6.3
```

2、编辑系统变量 **Path**，添加变量值：**;%MAVEN_HOME%\bin**

3、cmd  测试成功 mvn -v

## maven仓库的种类和彼此关系



仓库分三类：本地仓库、远程仓库（私服），中央仓库。

![](..\img\maven02.png)

maven工程 根据jar包坐标，在本地仓库找到，如果本地仓库找不到，到远程仓库私服找，再到中央仓库jar找(必须连网)

本地仓库路径更改

```
  <!-- localRepository
   | The path to the local repository maven will use to store artifacts.
   |
   | Default: ${user.home}/.m2/repository
  <localRepository>/path/to/local/repo</localRepository>
  -->
<localRepository>C:\my_java\maven_repository</localRepository>
```

## maven目录结构

![](..\img\maven03.png)

## maven 常用命令

mvn clean ： 清除 //项目中的target目录删除

mvn compile  编译 //项目编译重新生成target

mvn test   测试 //target文件中测试代码 +java代码编译  test-classes

mvn install  安装 项目打包到本地仓库

mvn package 打包

mvn deploy 发布

## maven生命周期

![](..\img\maven04.png)

## maven 概念模型

maven核心：依赖管理和一键构建

![](..\img\maven06.png)

## idea集成maven

![](..\img\idea01.png)

![](..\img\idea02.png)

-DarchetypeCatalog=internal

已经下载的jar，在不能连网情况下不需要重新下载。

## idea 创建maven的Java工程

使用骨架  quickstart创建工程 （开发中不建议使用）

![](..\img\idea03.png)

![](..\img\idea06.png)



![](..\img\idea04.png)

![](..\img\idea05.png)
