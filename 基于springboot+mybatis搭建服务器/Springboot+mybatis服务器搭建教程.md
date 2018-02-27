# 一、运行环境
1、eclipse，sts(spring tool suite)
2、eclipse中已经安装mybatis generator插件

# 二、搭建步骤
## 1、新建Spring Starter Project项目

 1. New Project->Spring Boot->Spring Starter Project->点击Next
![https://gitee.com/lidechenyan/images/raw/master/springboot+mybatis.png](https://gitee.com/lidechenyan/images/raw/master/springboot+mybatis.png)
 2. 设置包路径，项目坐标，项目名
![https://gitee.com/lidechenyan/images/raw/master/springboot+mybatis1.png](https://gitee.com/lidechenyan/images/raw/master/springboot+mybatis1.png)
 3. 添加依赖
![https://gitee.com/lidechenyan/images/raw/master/springboot+mybatis2.png](https://gitee.com/lidechenyan/images/raw/master/springboot+mybatis2.png)

## 2、配置application.properties

 1. 配置数据库连接

    spring.datasource.url: jdbc:mysql://localhost:3306/数据库名称?useUnicode=true&characterEncoding=utf-8&useSSL=false
    spring.datasource.username: 账号
    spring.datasource.password: 密码

 2. 服务器启动端口设置

    server.port: 8010

 3. 项目路径设置

    adminPath: /demo

 4. application.properties配置信息如下。

```
spring.datasource.url: jdbc:mysql://localhost:3306/demo?useUnicode=true&characterEncoding=utf-8&useSSL=false
spring.datasource.username: root
spring.datasource.password: dabby@2011

server.port: 8010

adminPath: /demo

mybatis.mapper-locations: classpath:mapping/*.xml
mytabis.type-aliases-package: self.lide.demo.entity
```
## 3、项目三层结构目录创建
1. dao/service/controller三层结构
2. 新建实体类存放目录entity，映射文件存放目录mapping
3. 最终目录结构如下。
![https://gitee.com/lidechenyan/images/raw/master/springboot+mybatis3.png](https://gitee.com/lidechenyan/images/raw/master/springboot+mybatis3.png)
## 4、mybatisGenerator配置generatorConfig.xml自动生成Dao/Entity/Mapping

    <?xml version="1.0" encoding="UTF-8"?>
    <!DOCTYPE generatorConfiguration PUBLIC "-//mybatis.org//DTD MyBatis Generator Configuration 1.0//EN" "http://mybatis.org/dtd/mybatis-generator-config_1_0.dtd">
    <generatorConfiguration>
      <context id="DB2Tables">
        <jdbcConnection connectionURL="jdbc:mysql://127.0.0.1:3306/demo" driverClass="com.mysql.jdbc.Driver" password="dabby@2011" userId="root" />
        <javaModelGenerator targetPackage="self.lide.demo.entity" targetProject="demo-springboot-mybatis" />
        <sqlMapGenerator targetPackage="mapping" targetProject="demo-springboot-mybatis/src/main/resources" />
        <javaClientGenerator targetPackage="self.lide.demo.dao" targetProject="demo-springboot-mybatis" type="XMLMAPPER" />
        <table tableName="demo_table" domainObjectName="DemoTable" enableCountByExample="false" enableUpdateByExample="false" enableDeleteByExample="false" enableSelectByExample="false" selectByExampleQueryId="false"></table>
      </context>
    </generatorConfiguration>
## 5、Springboot连接mybatis
1. 在application.properties中配置mybatis信息

    mybatis.mapper-locations: classpath:mapping/*.xml
    mytabis.type-aliases-package: self.lide.demo.entity

2. 在启动类中开启对Dao层的扫描

    @MapperScan("self.lide.demo.dao")

## 6、测试Dao层是否可用
1. 在测试目录src/test/java下新建子目录self.lide.demo.dao
2. 添加测试类DemoTableMapperTest.java

    package self.lide.demo.dao;
    import org.junit.Test;
    import org.junit.runner.RunWith;
    import org.springframework.beans.factory.annotation.Autowired;
    import org.springframework.boot.autoconfigure.EnableAutoConfiguration;
    import org.springframework.boot.test.context.SpringBootTest;
    import org.springframework.test.context.junit4.SpringRunner;
    import junit.framework.Assert;
    import self.lide.demo.DemoSpringbootMybatisApplication;
    
    @RunWith(SpringRunner.class)
    @SpringBootTest(classes = DemoSpringbootMybatisApplication.class, webEnvironment = SpringBootTest.WebEnvironment.RANDOM_PORT)
    @EnableAutoConfiguration
    public class DemoTableMapperTest {
    
	    @Autowired
	    private DemoTableMapper demotableMapper;
	    
	    @Test
	    public void testSelect() {
	    	Long id = 1L;
	    	Assert.assertNotNull(demotableMapper.selectByPrimaryKey(id));
		}
    }
JUnit Test 通过测试用例testSelect说明springboot成功连接mybatis，mybatisGenerator自动生成有效。
## 7、开发service层
1. 编写接口类DemoSerive.java与实现类DemoServiceImpl.java
a）DemoService类
```
package self.lide.demo.service;

import self.lide.demo.entity.DemoTable;

public interface DemoService {

	public boolean findOne(DemoTable demoTable);
}
```
b）DemoServiceImpl类，在类上添加注解@Service，开启扫描

```
package self.lide.demo.service.impl;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;

import self.lide.demo.dao.DemoTableMapper;
import self.lide.demo.entity.DemoTable;
import self.lide.demo.service.DemoService;

@Service
public class DemoServiceImpl implements DemoService {

	@Autowired
	private DemoTableMapper demotableMapper;
	
	@Override
	public boolean findOne(DemoTable demoTable) {
		// TODO Auto-generated method stub
		Long id = demoTable.getId();
		DemoTable db_demoTable = demotableMapper.selectByPrimaryKey(id);
		
		return db_demoTable==null ? false:true;
	}

}
```

2. 在src/test/java目录下新建子目录self.lide.demo.service，并添加测试类DemoServiceTest.java

```
package self.lide.demo.service;

import org.junit.Assert;
import org.junit.Test;
import org.junit.runner.RunWith;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.autoconfigure.EnableAutoConfiguration;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.test.context.junit4.SpringRunner;

import self.lide.demo.entity.DemoTable;

@RunWith(SpringRunner.class)
@SpringBootTest
@EnableAutoConfiguration
public class DemoServiceTest {
	
	@Autowired
	private DemoService demoService;
	
	@Test
	public void testSelect() {
		DemoTable demoTable = new DemoTable();
		demoTable.setId(1L);
		
		Assert.assertFalse(demoService.findOne(demoTable));
	}
}
```
测试通过，说明接口类与实现类编写无误。
## 8、编写Controller层，服务器API测试

```
package self.lide.demo.controller;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.PathVariable;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.ResponseBody;
import org.springframework.web.bind.annotation.RestController;

import com.fasterxml.jackson.core.JsonProcessingException;
import com.fasterxml.jackson.databind.ObjectMapper;

import self.lide.demo.entity.DemoTable;
import self.lide.demo.service.DemoService;

@RestController
@RequestMapping(value="${adminPath}/demo")
public class DemoController {
	
	@Autowired
	private DemoService demoService;
	
	@ResponseBody
	@RequestMapping("/find/{id}")
	public String FindOne(@PathVariable("id") Long id) {
		DemoTable demoTable = new DemoTable();
		demoTable.setId(id);
		if (demoService.findOne(demoTable)) {
			try {
				return (new ObjectMapper()).writeValueAsString(demoTable)+", is exist";
			} catch (JsonProcessingException e) {
				// TODO Auto-generated catch block
				e.printStackTrace();
			}
		}
			
		return String.valueOf(false);
	}
}
```
注意：使用到fastxml.jackson，将demoTable对象转化为json格式输出，在springboot中默认使用Jackson。

浏览器访问链接：http://localhost:8010/demo/demo/find/1
输出以下两种结果，说明API编写成功

```
{"id":1,"status":null,"message":null,"createtime":null}, is exist
false
```

项目源码下载：https://github.com/lidegithub/stu-doc/blob/master/%E5%9F%BA%E4%BA%8Espringboot%2Bmybatis%E6%90%AD%E5%BB%BA%E6%9C%8D%E5%8A%A1%E5%99%A8/demo-springboot-mybatis.zip


