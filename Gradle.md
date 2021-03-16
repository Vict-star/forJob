
# Gradle

## 例子

一个spring boot的gradle配置文件

```groovy

// buildscript 代码块中脚本优先执行
buildscript {
 
	// ext 用于定义动态属性
	ext {
		springBootVersion = '1.5.2.RELEASE'
	}
			
	// 自定义  Thymeleaf 和 Thymeleaf Layout Dialect 的版本
	ext['thymeleaf.version'] = '3.0.3.RELEASE'
	ext['thymeleaf-layout-dialect.version'] = '2.2.0'
	
	// 自定义  Hibernate 的版本
	ext['hibernate.version'] = '5.2.8.Final'
 
	// 使用了 Maven 的中央仓库（你也可以指定其他仓库）
	repositories {
		//mavenCentral()
		maven {
			url 'http://maven.aliyun.com/nexus/content/groups/public/'
		}
	}
	
	// 依赖关系
	dependencies {
		// classpath 声明说明了在执行其余的脚本时，ClassLoader 可以使用这些依赖项
		classpath("org.springframework.boot:spring-boot-gradle-plugin:${springBootVersion}")
	}
}
 
// 使用插件
apply plugin: 'java'
apply plugin: 'eclipse'
apply plugin: 'org.springframework.boot'
 
// 打包的类型为 jar，并指定了生成的打包的文件名称和版本
jar {
	baseName = 'springboot-test'
	version = '1.0.0'
}
 
// 指定编译 .java 文件的 JDK 版本
sourceCompatibility = 1.8
 
// 默认使用了 Maven 的中央仓库。这里改用自定义的镜像库
repositories {
	//mavenCentral()
	maven {
		url 'http://maven.aliyun.com/nexus/content/groups/public/'
	}
}
 
// 依赖关系
dependencies {
 
	// 该依赖对于编译发行是必须的
	compile('org.springframework.boot:spring-boot-starter-web')
 
	// 添加 Thymeleaf 的依赖
	compile('org.springframework.boot:spring-boot-starter-thymeleaf')
 
	// 添加  Spring Security 依赖
	compile('org.springframework.boot:spring-boot-starter-security')
	
	// 添加 Spring Boot 开发工具依赖
 	//compile("org.springframework.boot:spring-boot-devtools")
 
	// 添加 Spring Data JPA 的依赖
	compile('org.springframework.boot:spring-boot-starter-data-jpa')
	
	// 添加 MySQL连接驱动 的依赖
	compile('mysql:mysql-connector-java:6.0.5')
	
	// 添加   Thymeleaf Spring Security 依赖，与 Thymeleaf 版本一致都是 3.x
	compile('org.thymeleaf.extras:thymeleaf-extras-springsecurity4:3.0.2.RELEASE')
	
	// 添加  Apache Commons Lang 依赖
	compile('org.apache.commons:commons-lang3:3.5')
	
	// 该依赖对于编译测试是必须的，默认包含编译产品依赖和编译时依
	testCompile('org.springframework.boot:spring-boot-starter-test')
	
}
```


## 依赖管理
### 什么是依赖管理?

通俗来讲，依赖管理由如下两部分组成。首先，Gradle 需要知道项目构建或运行所需要的一些文件，以便于找到这些需要的文件。我们称这些输入的文件为项目的依赖。其次，你可能需要构建完成后自动上传到某个地方。我们称这些输出为发布。下面来仔细介绍一下这两部分：  

大部分工程都不太可能完全自给自足，一般你都会用到其他工程的文件。比如我工程需要 Hibernate 就得把它的类库加进来，比如测试的时候可能需要某些额外 jar 包，例如 JDBC 驱动或 Ehcache 之类的 Jar 包。  

这些文件就是工程的依赖。Gradle 需要你告诉它工程的依赖是什么，它们在哪，然后帮你加入构建中。依赖可能需要去远程库下载，比如 Maven 或者 Ivy 库。也可以是本地库，甚至可能是另一个工程。我们称这个过程叫依赖解决。  

通常，依赖的自身也有依赖。例如，Hibernate 核心类库就依赖于一些其他的类库。所以，当 Gradle 构建你的工程时，会去找到这些依赖。我们称之为依赖传递。  

大部分工程构建的主要目的是脱离工程使用。例如，生成 jar 包，包括源代码、文档等，然后发布出去。  

这些输出的文件构成了项目的发布内容。Gralde 也会为你分担这些工作。你声明了发布到到哪，Gradle 就会发布到哪。“发布”的意思就是你想做什么。比如，复制到某个目录，上传到 Maven 或 Ivy 仓库。或者在其它项目里使用，这些都可以称之为发行。  

### 依赖的几种类型
- compile

    编译范围依赖在所有的 classpath 中可用，同时它们也会被打包
    
- runtime

    runtime 依赖在运行和测试系统的时候需要，但在编译的时候不需要。比如，你可能在编译的时候只需要 JDBC API JAR，而只有在运行的时候才需要 JDBC 驱动实现
    
- testCompile

    测试期编译需要的附加依赖
    
- testRuntime

    测试运行期需要
    不同的插件提供了不同的标准配置，你甚至也可以定义属于自己的配置项。
