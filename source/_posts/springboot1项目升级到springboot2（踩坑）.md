---
title: springboot1项目升级到springboot2（踩坑）
date: 2019-07-08 17:35:44
tags:
password:
cotegories:
photos:
---
一：首先需要把pom.xml中的parent节点中version改为2.X版本，我这里改为2.1.5.RELEASE
接下来修改application.yml文件，先把yml文件中的spring上传文件大小限制的配置进行修改：

```
  #文件上传配置 1.5.9
   spring:
       http:
          multipart:
              enabled: true
              max-file-size: 100Mb
              max-request-size:100Mb
```

```
  ##文件上传配置 2.1.5
   spring:
     servlet:
       multipart:
         enabled: true
         max-file-size: 100Mb
         max-request-size: 100Mb
```
修改redis相关配置：

```
 #redis部分配置 1.5.9
redis:
   pool:
     max-idle: 60
     min-idle: 30
     max-wait: -1
     max-active: 200
```

```
 ##redis部分配置 2.1.5
redis:
    jedis:
      pool:
        max-idle: 60
        min-idle: 30
        max-wait: -1
        max-active: 200
```

yml配置文件修改完毕了，启动以下项目报错：
org.springframework.boot.context.embedded.ConfigurableEmbeddedServletContainer;
org.springframework.boot.context.embedded.EmbeddedServletContainerCustomizer;这两个类找不到：查了资料发现在springboot2以后使用 org.springframework.boot.web.server.WebServerFactoryCustomizer;替换了
org.springframework.boot.context.embedded.EmbeddedServletContainerCustomizer;使用org.springframework.boot.web.server.ConfigurableWebServerFactory;替换了org.springframework.boot.context.embedded.ConfigurableEmbeddedServletContainer，所以这个地方把这两个类换掉基本就可以了


再次启动有报错：找不到groovy.util.logging.Slf4j;这里直接把这个引入删除就可以了，不知道这个以前是干什么的，不管了，先进行下一步

再次启动有报错：

```
Error:(31, 37) java: 对于RedisCacheManager(org.springframework.data.redis.core.RedisTemplate<capture#1, 共 ?,capture#2, 共 ?>), 找不到合适的构造器
    构造器 org.springframework.data.redis.cache.RedisCacheManager.RedisCacheManager(org.springframework.data.redis.cache.RedisCacheWriter,org.springframework.data.redis.cache.RedisCacheConfiguration,java.lang.String...)不适用
      (参数不匹配; org.springframework.data.redis.core.RedisTemplate<capture#1, 共 ?,capture#2, 共 ?>无法转换为org.springframework.data.redis.cache.RedisCacheWriter)
    构造器 org.springframework.data.redis.cache.RedisCacheManager.RedisCacheManager(org.springframework.data.redis.cache.RedisCacheWriter,org.springframework.data.redis.cache.RedisCacheConfiguration,boolean,java.lang.String...)不适用
      (参数不匹配; org.springframework.data.redis.core.RedisTemplate<capture#1, 共 ?,capture#2, 共 ?>无法转换为org.springframework.data.redis.cache.RedisCacheWriter)
```
我的redis相关配置类如下：

```
@Configuration
@EnableCaching
public class RedisConfig {

    /**
     *  缓存管理器
     */
    @Bean
    public CacheManager cacheManager(RedisTemplate<?,?> redisTemplate) {
        CacheManager cacheManager = new RedisCacheManager(redisTemplate);
        return cacheManager;
    }

    /**
     *  RedisTemplate
     */
    @Bean
    public RedisTemplate<String, Object> redisTemplate(RedisConnectionFactory factory) {
        RedisTemplate<String, Object> template = new RedisTemplate<String, Object>();
        template.setConnectionFactory(factory);
        Jackson2JsonRedisSerializer jackson2JsonRedisSerializer = new Jackson2JsonRedisSerializer(Object.class);
        ObjectMapper om = new ObjectMapper();
        om.setVisibility(PropertyAccessor.ALL, JsonAutoDetect.Visibility.ANY);
        om.enableDefaultTyping(ObjectMapper.DefaultTyping.NON_FINAL);
        jackson2JsonRedisSerializer.setObjectMapper(om);
        StringRedisSerializer stringRedisSerializer = new StringRedisSerializer();

        // key采用String的序列化方式
        template.setKeySerializer(stringRedisSerializer);
        // hash的key也采用String的序列化方式
        template.setHashKeySerializer(stringRedisSerializer);
        // value序列化方式采用jackson
        template.setValueSerializer(jackson2JsonRedisSerializer);
        // hash的value序列化方式采用jackson
        template.setHashValueSerializer(jackson2JsonRedisSerializer);
        template.afterPropertiesSet();

        return template;
    }

}

```
主要原因在这里：

```
    @Bean
    public CacheManager cacheManager(RedisTemplate<?,?> redisTemplate) {
        CacheManager cacheManager = new RedisCacheManager(redisTemplate);
        return cacheManager;
    }
```
需要修改为这样的：

```
   @Bean
    public CacheManager cacheManager(RedisConnectionFactory factory) {
        RedisCacheManager build = RedisCacheManager.builder(factory).build();
        return build;
    }
```
ok，再重新启动：
又报错了：

```
org.springframework.beans.factory.UnsatisfiedDependencyException: Error creating bean with name 'scheduledTask': Unsatisfied dependency expressed through field 'visitorService'; nested exception is org.springframework.beans.factory.UnsatisfiedDependencyException: Error creating bean with name 'visitorServiceImpl': Unsatisfied dependency expressed through field 'visitorMapper'; nested exception is org.springframework.beans.factory.UnsatisfiedDependencyException: Error creating bean with name 'visitorMapper' defined in file [D:\javaProject\MyBlog-1-master\target\classes\com\zhy\mapper\VisitorMapper.class]: Unsatisfied dependency expressed through bean property 'sqlSessionFactory'; nested exception is org.springframework.beans.factory.UnsatisfiedDependencyException: Error creating bean with name 'sqlSessionFactory' defined in class path resource [org/mybatis/spring/boot/autoconfigure/MybatisAutoConfiguration.class]: Unsatisfied dependency expressed through method 'sqlSessionFactory' parameter 0; nested exception is org.springframework.beans.factory.BeanCreationException: Error creating bean with name 'druidDataSource' defined in class path resource [com/zhy/config/DruidDataSourceConfig.class]: Bean instantiation via factory method failed; nested exception is org.springframework.beans.BeanInstantiationException: Failed to instantiate [javax.sql.DataSource]: Factory method 'dataSource' threw exception; nested exception is java.lang.NumberFormatException: null
	at org.springframework.beans.factory.annotation.AutowiredAnnotationBeanPostProcessor$AutowiredFieldElement.inject(AutowiredAnnotationBeanPostProcessor.java:596) ~[spring-beans-5.1.7.RELEASE.jar:5.1.7.RELEASE]
	at org.springframework.beans.factory.annotation.InjectionMetadata.inject(InjectionMetadata.java:90) ~[spring-beans-5.1.7.RELEASE.jar:5.1.7.RELEASE]
	at org.springframework.beans.factory.annotation.AutowiredAnnotationBeanPostProcessor.postProcessProperties(AutowiredAnnotationBeanPostProcessor.java:374) ~[spring-beans-5.1.7.RELEASE.jar:5.1.7.RELEASE]
	at org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory.populateBean(AbstractAutowireCapableBeanFactory.java:1411) ~[spring-beans-5.1.7.RELEASE.jar:5.1.7.RELEASE]
	at org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory.doCreateBean(AbstractAutowireCapableBeanFactory.java:592) ~[spring-beans-5.1.7.RELEASE.jar:5.1.7.RELEASE]
	at org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory.createBean(AbstractAutowireCapableBeanFactory.java:515) ~[spring-beans-5.1.7.RELEASE.jar:5.1.7.RELEASE]
	at org.springframework.beans.factory.support.AbstractBeanFactory.lambda$doGetBean$0(AbstractBeanFactory.java:320) ~[spring-beans-5.1.7.RELEASE.jar:5.1.7.RELEASE]
	at org.springframework.beans.factory.support.DefaultSingletonBeanRegistry.getSingleton(DefaultSingletonBeanRegistry.java:222) ~[spring-beans-5.1.7.RELEASE.jar:5.1.7.RELEASE]
	at org.springframework.beans.factory.support.AbstractBeanFactory.doGetBean(AbstractBeanFactory.java:318) ~[spring-beans-5.1.7.RELEASE.jar:5.1.7.RELEASE]
	at org.springframework.beans.factory.support.AbstractBeanFactory.getBean(AbstractBeanFactory.java:199) ~[spring-beans-5.1.7.RELEASE.jar:5.1.7.RELEASE]
	at org.springframework.beans.factory.support.DefaultListableBeanFactory.preInstantiateSingletons(DefaultListableBeanFactory.java:843) ~[spring-beans-5.1.7.RELEASE.jar:5.1.7.RELEASE]
	at org.springframework.context.support.AbstractApplicationContext.finishBeanFactoryInitialization(AbstractApplicationContext.java:877) ~[spring-context-5.1.7.RELEASE.jar:5.1.7.RELEASE]
	at org.springframework.context.support.AbstractApplicationContext.refresh(AbstractApplicationContext.java:549) ~[spring-context-5.1.7.RELEASE.jar:5.1.7.RELEASE]
	at org.springframework.boot.web.servlet.context.ServletWebServerApplicationContext.refresh(ServletWebServerApplicationContext.java:142) ~[spring-boot-2.1.5.RELEASE.jar:2.1.5.RELEASE]
	at org.springframework.boot.SpringApplication.refresh(SpringApplication.java:775) [spring-boot-2.1.5.RELEASE.jar:2.1.5.RELEASE]
	at org.springframework.boot.SpringApplication.refreshContext(SpringApplication.java:397) [spring-boot-2.1.5.RELEASE.jar:2.1.5.RELEASE]
	at org.springframework.boot.SpringApplication.run(SpringApplication.java:316) [spring-boot-2.1.5.RELEASE.jar:2.1.5.RELEASE]
	at org.springframework.boot.SpringApplication.run(SpringApplication.java:1260) [spring-boot-2.1.5.RELEASE.jar:2.1.5.RELEASE]
	at org.springframework.boot.SpringApplication.run(SpringApplication.java:1248) [spring-boot-2.1.5.RELEASE.jar:2.1.5.RELEASE]
	at com.zhy.MyBlogApplication.main(MyBlogApplication.java:19) [classes/:na]
```
从抛出的异常可以发现是自己的配置类DruidDataSourceConfig无法进行实例化，发现是我把yml中的数据源的配置字符串和阿里数据源的配置类中的字符串不对应