- 1、Maven 核心概念：坐标
  - [①数学中的坐标](http://heavy_code_industry.gitee.io/code_heavy_industry/pro002-maven/chapter03/verse01.html#_1数学中的坐标)
  - [②Maven中的坐标](http://heavy_code_industry.gitee.io/code_heavy_industry/pro002-maven/chapter03/verse01.html#_2maven中的坐标)
  - [③坐标和仓库中 jar 包的存储路径之间的对应关系](http://heavy_code_industry.gitee.io/code_heavy_industry/pro002-maven/chapter03/verse01.html#_3坐标和仓库中-jar-包的存储路径之间的对应关系)
- 2、实验操作
  - [①创建目录作为后面操作的工作空间](http://heavy_code_industry.gitee.io/code_heavy_industry/pro002-maven/chapter03/verse01.html#_1创建目录作为后面操作的工作空间)
  - [②在工作空间目录下打开命令行窗口](http://heavy_code_industry.gitee.io/code_heavy_industry/pro002-maven/chapter03/verse01.html#_2在工作空间目录下打开命令行窗口)
  - [③使用命令生成Maven工程](http://heavy_code_industry.gitee.io/code_heavy_industry/pro002-maven/chapter03/verse01.html#_3使用命令生成maven工程)
  - [④调整](http://heavy_code_industry.gitee.io/code_heavy_industry/pro002-maven/chapter03/verse01.html#_4调整)
  - [⑤自动生成的 pom.xml 解读](http://heavy_code_industry.gitee.io/code_heavy_industry/pro002-maven/chapter03/verse01.html#_5自动生成的-pom-xml-解读)
- 3、Maven核心概念：POM
  - [①含义](http://heavy_code_industry.gitee.io/code_heavy_industry/pro002-maven/chapter03/verse01.html#_1含义)
  - [②模型化思想](http://heavy_code_industry.gitee.io/code_heavy_industry/pro002-maven/chapter03/verse01.html#_2模型化思想)
  - [③对应的配置文件](http://heavy_code_industry.gitee.io/code_heavy_industry/pro002-maven/chapter03/verse01.html#_3对应的配置文件)
- 4、Maven核心概念：约定的目录结构
  - [①各个目录的作用](http://heavy_code_industry.gitee.io/code_heavy_industry/pro002-maven/chapter03/verse01.html#_1各个目录的作用)
  - [②约定目录结构的意义](http://heavy_code_industry.gitee.io/code_heavy_industry/pro002-maven/chapter03/verse01.html#_2约定目录结构的意义)
  - [③约定大于配置](http://heavy_code_industry.gitee.io/code_heavy_industry/pro002-maven/chapter03/verse01.html#_3约定大于配置)



# [#](http://heavy_code_industry.gitee.io/code_heavy_industry/pro002-maven/chapter03/verse01.html#第一节-实验一-根据坐标创建-maven-工程)第一节 实验一：根据坐标创建 Maven 工程

## [#](http://heavy_code_industry.gitee.io/code_heavy_industry/pro002-maven/chapter03/verse01.html#_1、maven-核心概念-坐标)1、Maven 核心概念：坐标

### [#](http://heavy_code_industry.gitee.io/code_heavy_industry/pro002-maven/chapter03/verse01.html#_1数学中的坐标)①数学中的坐标

![./images](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAh0AAAHGCAYAAADQcTmWAAAAAXNSR0IArs4c6QAAAARnQU1BAACxjwv8YQUAAAAJcEhZcwAAFxEAABcRAcom8z8AAA2sSURBVHhe7d0/jyTVFcbhBYdOsDZxiMgcgRxaSCZxQmIyE0JEipNNnKwsIdnREpFuuo4g88oJtuwMWfABkLD8ARb4BPienr6otj3/dqfOu1PdzyMddXdNMySj5kfdW9U/uQO3xztjfj7mP7tXAAANXhnz5Zhvdq8AAJrcH/PDft6rAwAAa3t1zLdjZnTU8zrzAQCwqgdjZnDMeTgGAGA1b42ZZzcOw+ONMQAAq/h8TAXGck9HneWox/oZAMCNfTim4qKuWKk9HDM66nkdq+d1GS0AwHOrsJhLKvNqlRkdpY7V83oPAMBzm8spyyWUZXSUum9Hva73AgA8s+UlsrWRdDqMjtpIWq/rvfXPAAA8k0/HVEzUpbJLh9FR5qbS+mcAAK6tNobOsxeHNwA7LzqWG0yXZ0UAAC5UAXHZPo3zoqPM/R++lwUAuJZ5I7B5ieyhi6KjzEtone0AAK6l7s1x0abQy6KjNpXWZbTnxQoAwDO5LDoA2LiX948AAK1EBwAQIToAgAjRwTG5N+bxft6sA1f4aMx8/906AACchptuJH13zPwdn9SBS1RkzPdWdAAAJ2RGwE08GVO/ox4vO3uxDJR6DgCckDWio5ZMrhMTX4yp91ScAAAnZo3oeH3M/D2P6sA5Xhsz33PVMgwAcIRmCNzUPItRc94SS204nT+vSAEATswMgZu6ar/G12PqZxUnAMAJWis66uzG3FB6uMSyXH6xgRQATtRa0VFqr8b8fbWHY5rHr7q6BQA4YmtGx/KMxgd1YG+eAbGBFABO2JrRUeaG0rl34+0x899hAykAnLC1o6POcMzfWUsstb+jnttACgAnbu3oWN7qfBkgNpACwImbUbCm5cbR+fttIAWAE9cRHfVts/P31thACgC0REeZNwOruc5X3gMAR647OuoRAKAlOpaXyS7v1wEAnLCO6Hg8Zv5eG0gBgJ21o2O5idQGUgDgRzeNjjqTMc9mVHDMy2Trcfn9KwDAibtpdBxeHjun9nUAAPxoRsLzOoyOOsMhOABuiZf2j3AbzOB43r/LWlr5xdnTnX/tHwEAnjLPUABwhF7ePwIAtBIdAECE6AAAIkQHABAhOgCACNEBAESIDgAgQnQAABGiAwCIEB0AQIToAAAiRAcAECE6AIAI0QEARIgOACBCdAAAEaIDAIgQHQBAhOgAACJEBwAQIToAgAjRAQBEiA4AIEJ0AAARogMAiBAdAECE6AAAIkQHABAhOgCACNEBAESIDgAgQnQAABGiAwCIEB0AQIToAAAiRAcAECE6AIAI0QEARIgOACBCdAAAEaIDAIgQHQBAhOgAACJEBwAQIToAgAjRAQBEiA4AIEJ0AAARogMAiBAdAECE6AAAIkQHABAhOgCACNEBAESIDgAgQnQAABGiAwCIEB0AQIToAAAiRAcAECE6AIAI0QEARIgOACBCdAAAEaIDAIgQHQBAhOgAACJEBwAQIToAgAjRAQBEiA4AIEJ0AAARogMAiBAdAECE6AAAIkQHABAhOgCACNEBAESIDgAgQnQAABGiAwCIEB0AQIToAAAiRAcAECE6AIAI0QEARIgOACBCdAAAEaIDAIgQHQBAhOgAACJEBwAQIToAgAjRAQBEiA4AIEJ0AAARogMAiBAdAECE6AAAIkQHABAhOgCACNEBAESIDgAgQnQAABGiAwCIEB0AQIToAAAiRAcAECE6AIAI0QEARIgOACBCdAAAEaIDAIgQHQBAhOgAACJEBwAQIToAgAjRAQBEiA4AIEJ0AAARogMAiBAdAECE6AAAIkQHABAhOgCACNEBAESIDgAgQnQAABGiAwCIEB0AQIToAAAiRAcAECE6AIAI0QEARIgOACBCdAAAEaIDAIgQHQBAhOgAACJEBwAQIToAgAjRAQBEiA4AIEJ0AAARogMAiBAdAECE6AAAIkQHABAhOgCACNEBAESIDgAgQnQAABGiAwCIEB0AQIToAAAiRAcAECE6AIAI0QEARIgOACBCdAAAEaIDAIgQHQBAhOgAACJEBwAQIToAgAjRAQBEiA4AIEJ0AAARogMAiBAdAECE6AAAIkQHABAhOgCACNEBAESIDgAgQnQAABGiAwCIEB0AQIToAAAiRAcAECE6AIAI0QEARIgOACBCdAAAEaIDAIgQHQBAhOgAACJEBwAQIToAgAjRAQBEiA4AIEJ0AAARogMAiBAdAECE6AAAIkQHABAhOgCACNEBAESIDgAgQnQAABGiAwCIEB0AQIToAAAiRAcAECE6AIAI0QEARIgOACBCdAAA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)

使用 x、y、z 三个**『向量』**作为空间的坐标系，可以在**『空间』**中唯一的定位到一个**『点』**。

### [#](http://heavy_code_industry.gitee.io/code_heavy_industry/pro002-maven/chapter03/verse01.html#_2maven中的坐标)②Maven中的坐标

#### [#](http://heavy_code_industry.gitee.io/code_heavy_industry/pro002-maven/chapter03/verse01.html#_1-向量说明)[1]向量说明

使用三个**『向量』**在**『Maven的仓库』**中**唯一**的定位到一个**『jar』**包。

- **groupId**：公司或组织的 id
- **artifactId**：一个项目或者是项目中的一个模块的 id
- **version**：版本号

#### [#](http://heavy_code_industry.gitee.io/code_heavy_industry/pro002-maven/chapter03/verse01.html#_2-三个向量的取值方式)[2]三个向量的取值方式

- groupId：公司或组织域名的倒序，通常也会加上项目名称
  - 例如：com.atguigu.maven
- artifactId：模块的名称，将来作为 Maven 工程的工程名
- version：模块的版本号，根据自己的需要设定
  - 例如：SNAPSHOT 表示快照版本，正在迭代过程中，不稳定的版本
  - 例如：RELEASE 表示正式版本

举例：

- groupId：com.atguigu.maven
- artifactId：pro01-atguigu-maven
- version：1.0-SNAPSHOT

### [#](http://heavy_code_industry.gitee.io/code_heavy_industry/pro002-maven/chapter03/verse01.html#_3坐标和仓库中-jar-包的存储路径之间的对应关系)③坐标和仓库中 jar 包的存储路径之间的对应关系

坐标：

```xml
  <groupId>javax.servlet</groupId>
  <artifactId>servlet-api</artifactId>
  <version>2.5</version>
```



上面坐标对应的 jar 包在 Maven 本地仓库中的位置：

```text
Maven本地仓库根目录\javax\servlet\servlet-api\2.5\servlet-api-2.5.jar
```

一定要学会根据坐标到本地仓库中找到对应的 jar 包。

## [#](http://heavy_code_industry.gitee.io/code_heavy_industry/pro002-maven/chapter03/verse01.html#_2、实验操作)2、实验操作

### [#](http://heavy_code_industry.gitee.io/code_heavy_industry/pro002-maven/chapter03/verse01.html#_1创建目录作为后面操作的工作空间)①创建目录作为后面操作的工作空间

例如：D:\maven-workspace\space201026

WARNING

此时我们已经有了三个目录，分别是：

- Maven 核心程序：中军大帐
- Maven 本地仓库：兵营
- 本地工作空间：战场

### [#](http://heavy_code_industry.gitee.io/code_heavy_industry/pro002-maven/chapter03/verse01.html#_2在工作空间目录下打开命令行窗口)②在工作空间目录下打开命令行窗口

![./images](http://heavy_code_industry.gitee.io/code_heavy_industry/assets/img/img010.7f3addf6.png)

### [#](http://heavy_code_industry.gitee.io/code_heavy_industry/pro002-maven/chapter03/verse01.html#_3使用命令生成maven工程)③使用命令生成Maven工程

![images](http://heavy_code_industry.gitee.io/code_heavy_industry/assets/img/img008.be45c9ad.png)

运行 **mvn archetype:generate** 命令

下面根据提示操作

> TIP

> Choose a number or apply filter (format: [groupId:]artifactId, case sensitive contains): 7:【直接回车，使用默认值】
>
> Define value for property 'groupId': com.atguigu.maven
>
> Define value for property 'artifactId': pro01-maven-java
>
> Define value for property 'version' 1.0-SNAPSHOT: :【直接回车，使用默认值】
>
> Define value for property 'package' com.atguigu.maven: :【直接回车，使用默认值】
>
> Confirm properties configuration: groupId: com.atguigu.maven artifactId: pro01-maven-java version: 1.0-SNAPSHOT package: com.atguigu.maven Y: :【直接回车，表示确认。如果前面有输入错误，想要重新输入，则输入 N 再回车。】

### [#](http://heavy_code_industry.gitee.io/code_heavy_industry/pro002-maven/chapter03/verse01.html#_4调整)④调整

Maven 默认生成的工程，对 junit 依赖的是较低的 3.8.1 版本，我们可以改成较适合的 4.12 版本。

自动生成的 App.java 和 AppTest.java 可以删除。

```xml
<!-- 依赖信息配置 -->
<!-- dependencies复数标签：里面包含dependency单数标签 -->
<dependencies>
	<!-- dependency单数标签：配置一个具体的依赖 -->
	<dependency>
		<!-- 通过坐标来依赖其他jar包 -->
		<groupId>junit</groupId>
		<artifactId>junit</artifactId>
		<version>4.12</version>
		
		<!-- 依赖的范围 -->
		<scope>test</scope>
	</dependency>
</dependencies>
```

### [#](http://heavy_code_industry.gitee.io/code_heavy_industry/pro002-maven/chapter03/verse01.html#_5自动生成的-pom-xml-解读)⑤自动生成的 pom.xml 解读

```xml
  <!-- 当前Maven工程的坐标 -->
  <groupId>com.atguigu.maven</groupId>
  <artifactId>pro01-maven-java</artifactId>
  <version>1.0-SNAPSHOT</version>
  
  <!-- 当前Maven工程的打包方式，可选值有下面三种： -->
  <!-- jar：表示这个工程是一个Java工程  -->
  <!-- war：表示这个工程是一个Web工程 -->
  <!-- pom：表示这个工程是“管理其他工程”的工程 -->
  <packaging>jar</packaging>

  <name>pro01-maven-java</name>
  <url>http://maven.apache.org</url>

  <properties>
	<!-- 工程构建过程中读取源码时使用的字符集 -->
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
  </properties>

  <!-- 当前工程所依赖的jar包 -->
  <dependencies>
	<!-- 使用dependency配置一个具体的依赖 -->
    <dependency>
	
	  <!-- 在dependency标签内使用具体的坐标依赖我们需要的一个jar包 -->
      <groupId>junit</groupId>
      <artifactId>junit</artifactId>
      <version>4.12</version>
	  
	  <!-- scope标签配置依赖的范围 -->
      <scope>test</scope>
    </dependency>
  </dependencies>
```



## [#](http://heavy_code_industry.gitee.io/code_heavy_industry/pro002-maven/chapter03/verse01.html#_3、maven核心概念-pom)3、Maven核心概念：POM

### [#](http://heavy_code_industry.gitee.io/code_heavy_industry/pro002-maven/chapter03/verse01.html#_1含义)①含义

POM：**P**roject **O**bject **M**odel，项目对象模型。和 POM 类似的是：DOM（Document Object Model），文档对象模型。它们都是模型化思想的具体体现。

### [#](http://heavy_code_industry.gitee.io/code_heavy_industry/pro002-maven/chapter03/verse01.html#_2模型化思想)②模型化思想

POM 表示将工程抽象为一个模型，再用程序中的对象来描述这个模型。这样我们就可以用程序来管理项目了。我们在开发过程中，最基本的做法就是将现实生活中的事物抽象为模型，然后封装模型相关的数据作为一个对象，这样就可以在程序中计算与现实事物相关的数据。

### [#](http://heavy_code_industry.gitee.io/code_heavy_industry/pro002-maven/chapter03/verse01.html#_3对应的配置文件)③对应的配置文件

POM 理念集中体现在 Maven 工程根目录下 **pom.xml** 这个配置文件中。所以这个 pom.xml 配置文件就是 Maven 工程的核心配置文件。其实学习 Maven 就是学这个文件怎么配置，各个配置有什么用。

## [#](http://heavy_code_industry.gitee.io/code_heavy_industry/pro002-maven/chapter03/verse01.html#_4、maven核心概念-约定的目录结构)4、Maven核心概念：约定的目录结构

### [#](http://heavy_code_industry.gitee.io/code_heavy_industry/pro002-maven/chapter03/verse01.html#_1各个目录的作用)①各个目录的作用

![./images](http://heavy_code_industry.gitee.io/code_heavy_industry/assets/img/img011.621b1ac3.png)

另外还有一个 target 目录专门存放构建操作输出的结果。

### [#](http://heavy_code_industry.gitee.io/code_heavy_industry/pro002-maven/chapter03/verse01.html#_2约定目录结构的意义)②约定目录结构的意义

Maven 为了让构建过程能够尽可能自动化完成，所以必须约定目录结构的作用。例如：Maven 执行编译操作，必须先去 Java 源程序目录读取 Java 源代码，然后执行编译，最后把编译结果存放在 target 目录。

### [#](http://heavy_code_industry.gitee.io/code_heavy_industry/pro002-maven/chapter03/verse01.html#_3约定大于配置)③约定大于配置

Maven 对于目录结构这个问题，没有采用配置的方式，而是基于约定。这样会让我们在开发过程中非常方便。如果每次创建 Maven 工程后，还需要针对各个目录的位置进行详细的配置，那肯定非常麻烦。

目前开发领域的技术发展趋势就是：约定大于配置，配置大于编码。



- [1、主体程序](http://heavy_code_industry.gitee.io/code_heavy_industry/pro002-maven/chapter03/verse02.html#_1、主体程序)
- [2、测试程序](http://heavy_code_industry.gitee.io/code_heavy_industry/pro002-maven/chapter03/verse02.html#_2、测试程序)



# [#](http://heavy_code_industry.gitee.io/code_heavy_industry/pro002-maven/chapter03/verse02.html#第二节-实验二-在-maven-工程中编写代码)第二节 实验二：在 Maven 工程中编写代码

## [#](http://heavy_code_industry.gitee.io/code_heavy_industry/pro002-maven/chapter03/verse02.html#_1、主体程序)1、主体程序

![./images](http://heavy_code_industry.gitee.io/code_heavy_industry/assets/img/img012.0bcc2c5d.png)

主体程序指的是被测试的程序，同时也是将来在项目中真正要使用的程序。

```java
package com.atguigu.maven;
	
public class Calculator {
	
	public int sum(int i, int j){
		return i + j;
	}
	
}
```

## [#](http://heavy_code_industry.gitee.io/code_heavy_industry/pro002-maven/chapter03/verse02.html#_2、测试程序)2、测试程序

![./images](http://heavy_code_industry.gitee.io/code_heavy_industry/assets/img/img013.8b57a581.png)

```java
package com.atguigu.maven;
	
import org.junit.Test;
import com.atguigu.maven.Calculator;
	
// 静态导入的效果是将Assert类中的静态资源导入当前类
// 这样一来，在当前类中就可以直接使用Assert类中的静态资源，不需要写类名
import static org.junit.Assert.*;
	
public class CalculatorTest{
	
	@Test
	public void testSum(){
		
		// 1.创建Calculator对象
		Calculator calculator = new Calculator();
		
		// 2.调用Calculator对象的方法，获取到程序运行实际的结果
		int actualResult = calculator.sum(5, 3);
		
		// 3.声明一个变量，表示程序运行期待的结果
		int expectedResult = 8;
		
		// 4.使用断言来判断实际结果和期待结果是否一致
		// 如果一致：测试通过，不会抛出异常
		// 如果不一致：抛出异常，测试失败
		assertEquals(expectedResult, actualResult);
		
	}
	
}
```



- [1、要求](http://heavy_code_industry.gitee.io/code_heavy_industry/pro002-maven/chapter03/verse03.html#_1、要求)
- [2、清理操作](http://heavy_code_industry.gitee.io/code_heavy_industry/pro002-maven/chapter03/verse03.html#_2、清理操作)
- [3、编译操作](http://heavy_code_industry.gitee.io/code_heavy_industry/pro002-maven/chapter03/verse03.html#_3、编译操作)
- [4、测试操作](http://heavy_code_industry.gitee.io/code_heavy_industry/pro002-maven/chapter03/verse03.html#_4、测试操作)
- [5、打包操作](http://heavy_code_industry.gitee.io/code_heavy_industry/pro002-maven/chapter03/verse03.html#_5、打包操作)
- [6、安装操作](http://heavy_code_industry.gitee.io/code_heavy_industry/pro002-maven/chapter03/verse03.html#_6、安装操作)



# [#](http://heavy_code_industry.gitee.io/code_heavy_industry/pro002-maven/chapter03/verse03.html#实验三-执行-maven-的构建命令)实验三：执行 Maven 的构建命令

## [#](http://heavy_code_industry.gitee.io/code_heavy_industry/pro002-maven/chapter03/verse03.html#_1、要求)1、要求

运行 Maven 中和构建操作相关的命令时，必须进入到 pom.xml 所在的目录。如果没有在 pom.xml 所在的目录运行 Maven 的构建命令，那么会看到下面的错误信息：

```java
The goal you specified requires a project to execute but there is no POM in this directory
```

1

TIP

mvn -v 命令和构建操作无关，只要正确配置了 PATH，在任何目录下执行都可以。而构建相关的命令要在 pom.xml 所在目录下运行——操作哪个工程，就进入这个工程的 pom.xml 目录。

## [#](http://heavy_code_industry.gitee.io/code_heavy_industry/pro002-maven/chapter03/verse03.html#_2、清理操作)2、清理操作

mvn clean

效果：删除 target 目录

## [#](http://heavy_code_industry.gitee.io/code_heavy_industry/pro002-maven/chapter03/verse03.html#_3、编译操作)3、编译操作

主程序编译：mvn compile

测试程序编译：mvn test-compile

主体程序编译结果存放的目录：target/classes

测试程序编译结果存放的目录：target/test-classes

## [#](http://heavy_code_industry.gitee.io/code_heavy_industry/pro002-maven/chapter03/verse03.html#_4、测试操作)4、测试操作

mvn test

测试的报告存放的目录：target/surefire-reports

## [#](http://heavy_code_industry.gitee.io/code_heavy_industry/pro002-maven/chapter03/verse03.html#_5、打包操作)5、打包操作

mvn package

打包的结果——jar 包，存放的目录：target

## [#](http://heavy_code_industry.gitee.io/code_heavy_industry/pro002-maven/chapter03/verse03.html#_6、安装操作)6、安装操作

mvn install

```log
[INFO] Installing D:\maven-workspace\space201026\pro01-maven-java\target\pro01-maven-java-1.0-SNAPSHOT.jar to D:\maven-rep1026\com\atguigu\maven\pro01-maven-java\1.0-SNAPSHOT\pro01-maven-java-1.0-SNAPSHOT.jar
[INFO] Installing D:\maven-workspace\space201026\pro01-maven-java\pom.xml to D:\maven-rep1026\com\atguigu\maven\pro01-maven-java\1.0-SNAPSHOT\pro01-maven-java-1.0-SNAPSHOT.pom
```



安装的效果是将本地构建过程中生成的 jar 包存入 Maven 本地仓库。这个 jar 包在 Maven 仓库中的路径是根据它的坐标生成的。

坐标信息如下：

```xml
  <groupId>com.atguigu.maven</groupId>
  <artifactId>pro01-maven-java</artifactId>
  <version>1.0-SNAPSHOT</version>
```



在 Maven 仓库中生成的路径如下：

```log
D:\maven-rep1026\com\atguigu\maven\pro01-maven-java\1.0-SNAPSHOT\pro01-maven-java-1.0-SNAPSHOT.jar
```

另外，安装操作还会将 pom.xml 文件转换为 XXX.pom 文件一起存入本地仓库。所以我们在 Maven 的本地仓库中想看一个 jar 包原始的 pom.xml 文件时，查看对应 XXX.pom 文件即可，它们是名字发生了改变，本质上是同一个文件。



- [1、说明](http://heavy_code_industry.gitee.io/code_heavy_industry/pro002-maven/chapter03/verse04.html#_1、说明)
- [2、操作](http://heavy_code_industry.gitee.io/code_heavy_industry/pro002-maven/chapter03/verse04.html#_2、操作)
- [3、生成的pom.xml](http://heavy_code_industry.gitee.io/code_heavy_industry/pro002-maven/chapter03/verse04.html#_3、生成的pom-xml)
- [4、生成的Web工程的目录结构](http://heavy_code_industry.gitee.io/code_heavy_industry/pro002-maven/chapter03/verse04.html#_4、生成的web工程的目录结构)
- 5、创建 Servlet
  - [①在 main 目录下创建 java 目录](http://heavy_code_industry.gitee.io/code_heavy_industry/pro002-maven/chapter03/verse04.html#_1在-main-目录下创建-java-目录)
  - [②在 java 目录下创建 Servlet 类所在的包的目录](http://heavy_code_industry.gitee.io/code_heavy_industry/pro002-maven/chapter03/verse04.html#_2在-java-目录下创建-servlet-类所在的包的目录)
  - [③在包下创建 Servlet 类](http://heavy_code_industry.gitee.io/code_heavy_industry/pro002-maven/chapter03/verse04.html#_3在包下创建-servlet-类)
  - [④在 web.xml 中注册 Servlet](http://heavy_code_industry.gitee.io/code_heavy_industry/pro002-maven/chapter03/verse04.html#_4在-web-xml-中注册-servlet)
- [6、在 index.jsp 页面编写超链接](http://heavy_code_industry.gitee.io/code_heavy_industry/pro002-maven/chapter03/verse04.html#_6、在-index-jsp-页面编写超链接)
- [7、编译](http://heavy_code_industry.gitee.io/code_heavy_industry/pro002-maven/chapter03/verse04.html#_7、编译)
- [8、配置对 servlet-api.jar 包的依赖](http://heavy_code_industry.gitee.io/code_heavy_industry/pro002-maven/chapter03/verse04.html#_8、配置对-servlet-api-jar-包的依赖)
- [9、将 Web 工程打包为 war 包](http://heavy_code_industry.gitee.io/code_heavy_industry/pro002-maven/chapter03/verse04.html#_9、将-web-工程打包为-war-包)
- [10、将 war 包部署到 Tomcat 上运行](http://heavy_code_industry.gitee.io/code_heavy_industry/pro002-maven/chapter03/verse04.html#_10、将-war-包部署到-tomcat-上运行)



# [#](http://heavy_code_industry.gitee.io/code_heavy_industry/pro002-maven/chapter03/verse04.html#实验四-创建-maven-版的-web-工程)实验四：创建 Maven 版的 Web 工程

## [#](http://heavy_code_industry.gitee.io/code_heavy_industry/pro002-maven/chapter03/verse04.html#_1、说明)1、说明

使用 mvn archetype:generate 命令生成 Web 工程时，需要使用一个专门的 archetype。这个专门生成 Web 工程骨架的 archetype 可以参照官网看到它的用法：

![./images](http://heavy_code_industry.gitee.io/code_heavy_industry/assets/img/img014.942770a3.png)

参数 archetypeGroupId、archetypeArtifactId、archetypeVersion 用来指定现在使用的 maven-archetype-webapp 的坐标。

## [#](http://heavy_code_industry.gitee.io/code_heavy_industry/pro002-maven/chapter03/verse04.html#_2、操作)2、操作

注意：如果在上一个工程的目录下执行 mvn archetype:generate 命令，那么 Maven 会报错：不能在一个非 pom 的工程下再创建其他工程。所以不要再刚才创建的工程里再创建新的工程，**请回到工作空间根目录**来操作。

然后运行生成工程的命令：

```log
mvn archetype:generate -DarchetypeGroupId=org.apache.maven.archetypes -DarchetypeArtifactId=maven-archetype-webapp -DarchetypeVersion=1.4
```

下面的操作按照提示执行：

TIP

Define value for property 'groupId': com.atguigu.maven Define value for property 'artifactId': pro02-maven-web Define value for property 'version' 1.0-SNAPSHOT: :【直接回车，使用默认值】

Define value for property 'package' com.atguigu.maven: :【直接回车，使用默认值】 Confirm properties configuration: groupId: com.atguigu.maven artifactId: pro02-maven-web version: 1.0-SNAPSHOT package: com.atguigu.maven Y: :【直接回车，表示确认】

## [#](http://heavy_code_industry.gitee.io/code_heavy_industry/pro002-maven/chapter03/verse04.html#_3、生成的pom-xml)3、生成的pom.xml

确认打包的方式是war包形式

```xml
<packaging>war</packaging>
```

1

## [#](http://heavy_code_industry.gitee.io/code_heavy_industry/pro002-maven/chapter03/verse04.html#_4、生成的web工程的目录结构)4、生成的Web工程的目录结构

![./images](data:image/png;base64,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)

webapp 目录下有 index.jsp

WEB-INF 目录下有 web.xml

## [#](http://heavy_code_industry.gitee.io/code_heavy_industry/pro002-maven/chapter03/verse04.html#_5、创建-servlet)5、创建 Servlet

### [#](http://heavy_code_industry.gitee.io/code_heavy_industry/pro002-maven/chapter03/verse04.html#_1在-main-目录下创建-java-目录)①在 main 目录下创建 java 目录

![./images](data:image/png;base64,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)

### [#](http://heavy_code_industry.gitee.io/code_heavy_industry/pro002-maven/chapter03/verse04.html#_2在-java-目录下创建-servlet-类所在的包的目录)②在 java 目录下创建 Servlet 类所在的包的目录

![./images](data:image/png;base64,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)

### [#](http://heavy_code_industry.gitee.io/code_heavy_industry/pro002-maven/chapter03/verse04.html#_3在包下创建-servlet-类)③在包下创建 Servlet 类

```java
package com.atguigu.maven;
	
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import javax.servlet.ServletException;
import java.io.IOException;
	
public class HelloServlet extends HttpServlet{
	
	protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		
		response.getWriter().write("hello maven web");
		
	}
	
}
```

### [#](http://heavy_code_industry.gitee.io/code_heavy_industry/pro002-maven/chapter03/verse04.html#_4在-web-xml-中注册-servlet)④在 web.xml 中注册 Servlet

```xml
  <servlet>
	<servlet-name>helloServlet</servlet-name>
	<servlet-class>com.atguigu.maven.HelloServlet</servlet-class>
  </servlet>
  <servlet-mapping>
	<servlet-name>helloServlet</servlet-name>
	<url-pattern>/helloServlet</url-pattern>
  </servlet-mapping>
```

## [#](http://heavy_code_industry.gitee.io/code_heavy_industry/pro002-maven/chapter03/verse04.html#_6、在-index-jsp-页面编写超链接)6、在 index.jsp 页面编写超链接

```html
<html>
<body>
<h2>Hello World!</h2>
<a href="helloServlet">Access Servlet</a>
</body>
</html>
```



TIP

JSP全称是 Java Server Page，和 Thymeleaf 一样，是服务器端页面渲染技术。这里我们不必关心 JSP 语法细节，编写一个超链接标签即可。

## [#](http://heavy_code_industry.gitee.io/code_heavy_industry/pro002-maven/chapter03/verse04.html#_7、编译)7、编译

此时直接执行 mvn compile 命令出错：

DANGER

程序包 javax.servlet.http 不存在

程序包 javax.servlet 不存在

找不到符号

符号: 类 HttpServlet

……

上面的错误信息说明：我们的 Web 工程用到了 HttpServlet 这个类，而 HttpServlet 这个类属于 servlet-api.jar 这个 jar 包。此时我们说，Web 工程需要依赖 servlet-api.jar 包。

![./images](http://heavy_code_industry.gitee.io/code_heavy_industry/assets/img/img018.f836f056.png)

## [#](http://heavy_code_industry.gitee.io/code_heavy_industry/pro002-maven/chapter03/verse04.html#_8、配置对-servlet-api-jar-包的依赖)8、配置对 servlet-api.jar 包的依赖

对于不知道详细信息的依赖可以到https://mvnrepository.com/网站查询。使用关键词搜索，然后在搜索结果列表中选择适合的使用。

![./images](http://heavy_code_industry.gitee.io/code_heavy_industry/assets/img/img019.46741083.png)

比如，我们找到的 servlet-api 的依赖信息：

```xml
<!-- https://mvnrepository.com/artifact/javax.servlet/javax.servlet-api -->
<dependency>
    <groupId>javax.servlet</groupId>
    <artifactId>javax.servlet-api</artifactId>
    <version>3.1.0</version>
    <scope>provided</scope>
</dependency>
```



这样就可以把上面的信息加入 pom.xml。重新执行 mvn compile 命令。

## [#](http://heavy_code_industry.gitee.io/code_heavy_industry/pro002-maven/chapter03/verse04.html#_9、将-web-工程打包为-war-包)9、将 Web 工程打包为 war 包

运行 mvn package 命令，生成 war 包的位置如下图所示：

![./images](data:image/png;base64,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)

## [#](http://heavy_code_industry.gitee.io/code_heavy_industry/pro002-maven/chapter03/verse04.html#_10、将-war-包部署到-tomcat-上运行)10、将 war 包部署到 Tomcat 上运行

将 war 包复制到 Tomcat/webapps 目录下

![./images](data:image/png;base64,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)

启动 Tomcat：

![./images](data:image/png;base64,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)

![./images](data:image/png;base64,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)

通过浏览器尝试访问：http://localhost:8080/pro02-maven-web/index.jsp



- [1、观念](http://heavy_code_industry.gitee.io/code_heavy_industry/pro002-maven/chapter03/verse05.html#_1、观念)
- [2、操作](http://heavy_code_industry.gitee.io/code_heavy_industry/pro002-maven/chapter03/verse05.html#_2、操作)
- 3、在 Web 工程中，编写测试代码
  - [①补充创建目录](http://heavy_code_industry.gitee.io/code_heavy_industry/pro002-maven/chapter03/verse05.html#_1补充创建目录)
  - [②确认 Web 工程依赖了 junit](http://heavy_code_industry.gitee.io/code_heavy_industry/pro002-maven/chapter03/verse05.html#_2确认-web-工程依赖了-junit)
  - [③创建测试类](http://heavy_code_industry.gitee.io/code_heavy_industry/pro002-maven/chapter03/verse05.html#_3创建测试类)
- 4、执行Maven命令
  - [①测试命令](http://heavy_code_industry.gitee.io/code_heavy_industry/pro002-maven/chapter03/verse05.html#_1测试命令)
  - [②打包命令](http://heavy_code_industry.gitee.io/code_heavy_industry/pro002-maven/chapter03/verse05.html#_2打包命令)
  - [③查看当前 Web 工程所依赖的 jar 包的列表](http://heavy_code_industry.gitee.io/code_heavy_industry/pro002-maven/chapter03/verse05.html#_3查看当前-web-工程所依赖的-jar-包的列表)
  - [④以树形结构查看当前 Web 工程的依赖信息](http://heavy_code_industry.gitee.io/code_heavy_industry/pro002-maven/chapter03/verse05.html#_4以树形结构查看当前-web-工程的依赖信息)



# [#](http://heavy_code_industry.gitee.io/code_heavy_industry/pro002-maven/chapter03/verse05.html#实验五-让-web-工程依赖-java-工程)实验五：让 Web 工程依赖 Java 工程

## [#](http://heavy_code_industry.gitee.io/code_heavy_industry/pro002-maven/chapter03/verse05.html#_1、观念)1、观念

明确一个意识：从来只有 Web 工程依赖 Java 工程，没有反过来 Java 工程依赖 Web 工程。本质上来说，Web 工程依赖的 Java 工程其实就是 Web 工程里导入的 jar 包。最终 Java 工程会变成 jar 包，放在 Web 工程的 WEB-INF/lib 目录下。

## [#](http://heavy_code_industry.gitee.io/code_heavy_industry/pro002-maven/chapter03/verse05.html#_2、操作)2、操作

在 pro02-maven-web 工程的 pom.xml 中，找到 dependencies 标签，在 dependencies 标签中做如下配置：

```xml
<!-- 配置对Java工程pro01-maven-java的依赖 -->
<!-- 具体的配置方式：在dependency标签内使用坐标实现依赖 -->
<dependency>
	<groupId>com.atguigu.maven</groupId>
	<artifactId>pro01-maven-java</artifactId>
	<version>1.0-SNAPSHOT</version>
</dependency>
```

## [#](http://heavy_code_industry.gitee.io/code_heavy_industry/pro002-maven/chapter03/verse05.html#_3、在-web-工程中-编写测试代码)3、在 Web 工程中，编写测试代码

### [#](http://heavy_code_industry.gitee.io/code_heavy_industry/pro002-maven/chapter03/verse05.html#_1补充创建目录)①补充创建目录

pro02-maven-web**\src\test\java\com\atguigu\maven**

### [#](http://heavy_code_industry.gitee.io/code_heavy_industry/pro002-maven/chapter03/verse05.html#_2确认-web-工程依赖了-junit)②确认 Web 工程依赖了 junit

```xml
    <dependency>
      <groupId>junit</groupId>
      <artifactId>junit</artifactId>
      <version>4.12</version>
      <scope>test</scope>
    </dependency>
```

### [#](http://heavy_code_industry.gitee.io/code_heavy_industry/pro002-maven/chapter03/verse05.html#_3创建测试类)③创建测试类

把 Java 工程的 CalculatorTest.java 类复制到 pro02-maven-wb**\src\test\java\com\atguigu\maven** 目录下

## [#](http://heavy_code_industry.gitee.io/code_heavy_industry/pro002-maven/chapter03/verse05.html#_4、执行maven命令)4、执行Maven命令

### [#](http://heavy_code_industry.gitee.io/code_heavy_industry/pro002-maven/chapter03/verse05.html#_1测试命令)①测试命令

mvn test

说明：测试操作中会提前自动执行编译操作，测试成功就说明编译也是成功的。

### [#](http://heavy_code_industry.gitee.io/code_heavy_industry/pro002-maven/chapter03/verse05.html#_2打包命令)②打包命令

mvn package

![./images](http://heavy_code_industry.gitee.io/code_heavy_industry/assets/img/img024.91b00e04.png)

通过查看 war 包内的结构，我们看到被 Web 工程依赖的 Java 工程确实是会变成 Web 工程的 WEB-INF/lib 目录下的 jar 包。

![./images](data:image/png;base64,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)

### [#](http://heavy_code_industry.gitee.io/code_heavy_industry/pro002-maven/chapter03/verse05.html#_3查看当前-web-工程所依赖的-jar-包的列表)③查看当前 Web 工程所依赖的 jar 包的列表

mvn dependency:list

> TIP

> [INFO] The following files have been resolved:
> [INFO] org.hamcrest:hamcrest-core:jar:1.3:test
> [INFO] javax.servlet:javax.servlet-api:jar:3.1.0:provided
> [INFO] com.atguigu.maven:pro01-maven-java:jar:1.0-SNAPSHOT:compile
> [INFO] junit:junit:jar:4.12:test

说明：javax.servlet:javax.servlet-api:jar:3.1.0:provided 格式显示的是一个 jar 包的坐标信息。格式是：

> TIP

> groupId:artifactId:打包方式:version:依赖的范围

这样的格式虽然和我们 XML 配置文件中坐标的格式不同，但是本质上还是坐标信息，大家需要能够认识这样的格式，将来从 Maven 命令的日志或错误信息中看到这样格式的信息，就能够识别出来这是坐标。进而根据坐标到Maven 仓库找到对应的jar包，用这样的方式解决我们遇到的报错的情况。

### [#](http://heavy_code_industry.gitee.io/code_heavy_industry/pro002-maven/chapter03/verse05.html#_4以树形结构查看当前-web-工程的依赖信息)④以树形结构查看当前 Web 工程的依赖信息

mvn dependency:tree

> TIP

> [INFO] com.atguigu.maven:pro02-maven-web:war:1.0-SNAPSHOT
> [INFO] +- junit:junit:jar:4.12:test
> [INFO] | \- org.hamcrest:hamcrest-core:jar:1.3:test
> [INFO] +- javax.servlet:javax.servlet-api:jar:3.1.0:provided
> [INFO] \- com.atguigu.maven:pro01-maven-java:jar:1.0-SNAPSHOT:compile

我们在 pom.xml 中并没有依赖 hamcrest-core，但是它却被加入了我们依赖的列表。原因是：junit 依赖了hamcrest-core，然后基于依赖的传递性，hamcrest-core 被传递到我们的工程了。



- 1、依赖范围
  - [①compile 和 test 对比](http://heavy_code_industry.gitee.io/code_heavy_industry/pro002-maven/chapter03/verse06.html#_1compile-和-test-对比)
  - [②compile 和 provided 对比](http://heavy_code_industry.gitee.io/code_heavy_industry/pro002-maven/chapter03/verse06.html#_2compile-和-provided-对比)
  - [③结论](http://heavy_code_industry.gitee.io/code_heavy_industry/pro002-maven/chapter03/verse06.html#_3结论)
- 2、测试
  - [①验证 compile 范围对 main 目录有效](http://heavy_code_industry.gitee.io/code_heavy_industry/pro002-maven/chapter03/verse06.html#_1验证-compile-范围对-main-目录有效)
  - [②验证test范围对main目录无效](http://heavy_code_industry.gitee.io/code_heavy_industry/pro002-maven/chapter03/verse06.html#_2验证test范围对main目录无效)
  - [③验证test和provided范围不参与服务器部署](http://heavy_code_industry.gitee.io/code_heavy_industry/pro002-maven/chapter03/verse06.html#_3验证test和provided范围不参与服务器部署)
  - [④验证provided范围对测试程序有效](http://heavy_code_industry.gitee.io/code_heavy_industry/pro002-maven/chapter03/verse06.html#_4验证provided范围对测试程序有效)



# [#](http://heavy_code_industry.gitee.io/code_heavy_industry/pro002-maven/chapter03/verse06.html#实验六-测试依赖的范围)实验六：测试依赖的范围

## [#](http://heavy_code_industry.gitee.io/code_heavy_industry/pro002-maven/chapter03/verse06.html#_1、依赖范围)1、依赖范围

标签的位置：dependencies/dependency/**scope**

标签的可选值：**compile**/**test**/**provided**/system/runtime/**import**

### [#](http://heavy_code_industry.gitee.io/code_heavy_industry/pro002-maven/chapter03/verse06.html#_1compile-和-test-对比)①compile 和 test 对比

|         | main目录（空间） | test目录（空间） | 开发过程（时间） | 部署到服务器（时间） |
| ------- | ---------------- | ---------------- | ---------------- | -------------------- |
| compile | 有效             | 有效             | 有效             | 有效                 |
| test    | 无效             | 有效             | 有效             | 无效                 |

### [#](http://heavy_code_industry.gitee.io/code_heavy_industry/pro002-maven/chapter03/verse06.html#_2compile-和-provided-对比)②compile 和 provided 对比

|          | main目录（空间） | test目录（空间） | 开发过程（时间） | 部署到服务器（时间） |
| -------- | ---------------- | ---------------- | ---------------- | -------------------- |
| compile  | 有效             | 有效             | 有效             | 有效                 |
| provided | 有效             | 有效             | 有效             | 无效                 |

### [#](http://heavy_code_industry.gitee.io/code_heavy_industry/pro002-maven/chapter03/verse06.html#_3结论)③结论

compile：通常使用的第三方框架的 jar 包这样在项目实际运行时真正要用到的 jar 包都是以 compile 范围进行依赖的。比如 SSM 框架所需jar包。

test：测试过程中使用的 jar 包，以 test 范围依赖进来。比如 junit。

provided：在开发过程中需要用到的“服务器上的 jar 包”通常以 provided 范围依赖进来。比如 servlet-api、jsp-api。而这个范围的 jar 包之所以不参与部署、不放进 war 包，就是避免和服务器上已有的同类 jar 包产生冲突，同时减轻服务器的负担。说白了就是：“**服务器上已经有了，你就别带啦！**”

## [#](http://heavy_code_industry.gitee.io/code_heavy_industry/pro002-maven/chapter03/verse06.html#_2、测试)2、测试

### [#](http://heavy_code_industry.gitee.io/code_heavy_industry/pro002-maven/chapter03/verse06.html#_1验证-compile-范围对-main-目录有效)①验证 compile 范围对 main 目录有效

TIP

main目录下的类：HelloServlet 使用compile范围导入的依赖：pro01-atguigu-maven

验证：使用compile范围导入的依赖对main目录下的类来说是有效的

有效：HelloServlet 能够使用 pro01-atguigu-maven 工程中的 Calculator 类

验证方式：在 HelloServlet 类中导入 Calculator 类，然后编译就说明有效。

### [#](http://heavy_code_industry.gitee.io/code_heavy_industry/pro002-maven/chapter03/verse06.html#_2验证test范围对main目录无效)②验证test范围对main目录无效

测试方式：在主体程序中导入org.junit.Test这个注解，然后执行编译。

具体操作：在pro01-maven-java\src\main\java\com\atguigu\maven目录下修改Calculator.java

```java
package com.atguigu.maven;

import org.junit.Test;

public class Calculator {
	
	public int sum(int i, int j){
		return i + j;
	}
	
}
```

1
2
3
4
5
6
7
8
9
10
11

执行Maven编译命令：

```java
[ERROR] /D:/maven-workspace/space201026/pro01-maven-java/src/main/java/com/atguigu/maven/Calculator.java:[3,17] 程序包org.junit不存在
```

1

### [#](http://heavy_code_industry.gitee.io/code_heavy_industry/pro002-maven/chapter03/verse06.html#_3验证test和provided范围不参与服务器部署)③验证test和provided范围不参与服务器部署

其实就是验证：通过compile范围依赖的jar包会放入war包，通过test范围依赖的jar包不会放入war包。

![./images](http://heavy_code_industry.gitee.io/code_heavy_industry/assets/img/img026.0ad36150.png)

### [#](http://heavy_code_industry.gitee.io/code_heavy_industry/pro002-maven/chapter03/verse06.html#_4验证provided范围对测试程序有效)④验证provided范围对测试程序有效

测试方式是在pro02-maven-web的测试程序中加入servlet-api.jar包中的类。

修改：**pro02-maven-web**\src\**test**\java\com\atguigu\maven\**CalculatorTest.java**

```java
package com.atguigu.maven;

import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import javax.servlet.ServletException;

import org.junit.Test;
import com.atguigu.maven.Calculator;

// 静态导入的效果是将Assert类中的静态资源导入当前类
// 这样一来，在当前类中就可以直接使用Assert类中的静态资源，不需要写类名
import static org.junit.Assert.*;

public class CalculatorTest{
	
	@Test
	public void testSum(){
		
		// 1.创建Calculator对象
		Calculator calculator = new Calculator();
		
		// 2.调用Calculator对象的方法，获取到程序运行实际的结果
		int actualResult = calculator.sum(5, 3);
		
		// 3.声明一个变量，表示程序运行期待的结果
		int expectedResult = 8;
		
		// 4.使用断言来判断实际结果和期待结果是否一致
		// 如果一致：测试通过，不会抛出异常
		// 如果不一致：抛出异常，测试失败
		assertEquals(expectedResult, actualResult);
		
	}
	
}
```

然后运行Maven的编译命令：mvn compile

然后看到编译成功。