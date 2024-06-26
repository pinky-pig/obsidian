
首先定义配置文件有几种方式，很简单。

application.yaml 这个很简单，默认就扫描到了，只管写就好了。

PropertySource 引入 .property 的配置文件，也是可以直接用。

但是自定义的 yaml 文件，就不能直接用了，因为 PropertySource 是解析 property 文件的，解析 yaml 自然有点问题。所以就需要自定义重写一个类。

只要成功引入 yaml 文件，那么无论是 @Value 还是 ConfigurationProperties 都是可以的。

```java
@Component  
@Configuration  
@ConfigurationProperties(prefix = "cat")  
@PropertySource(value = "classpath:dog.yaml", encoding = "utf-8",factory = YamlPropertySourceFactory.class)  
public class Dog {  
    private int id;  
    private String name;  
    private int age;  
}
```

 或者这样都可以。
 
```java
public class Dog {  
    @Value("${dog.id}")  
    private int id;  
    @Value("${dog.name}")  
    private String name;  
    @Value("${dog.age}")  
    private int age;  
}
```

自定义的类：

```java
// 文件路径: src/main/java/com/example/demo/config/YamlPropertySourceFactory.java
package com.example.demo.config;  
  
import org.springframework.beans.factory.config.YamlPropertiesFactoryBean;  
import org.springframework.core.env.PropertiesPropertySource;  
import org.springframework.core.env.PropertySource;  
import org.springframework.core.io.support.EncodedResource;  
import org.springframework.core.io.support.PropertySourceFactory;  
  
import java.io.IOException;  
import java.util.Properties;  
  
public class YamlPropertySourceFactory implements PropertySourceFactory {  
  
    @Override  
    public PropertySource<?> createPropertySource(String name, EncodedResource encodedResource)  
            throws IOException {  
        YamlPropertiesFactoryBean factory = new YamlPropertiesFactoryBean();  
        factory.setResources(encodedResource.getResource());  
  
        Properties properties = factory.getObject();  
  
        return new PropertiesPropertySource(encodedResource.getResource().getFilename(), properties);  
    }  
}
```