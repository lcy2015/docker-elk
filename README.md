# Docker ELK stack
##一、运行elk服务
  docker-compose up
##二、后台运行elk服务
  docker-compose up -d
##三、配置应用，
   ###1.依赖jar
            <dependency> 
			<groupId>net.logstash.logback</groupId>
			<artifactId>logstash-logback-encoder</artifactId>
			<version>4.4</version>
		</dependency>
              
    ###2. 贴出相应的配置，相应的位置依次填入logstash的配置文件里面的host和端口号，以及相应的应用名称（可以自己适当做添加）
    ` `` java
        LogstashSocketAppender logstashAppender = new LogstashSocketAppender();
    ` `` 
    ` `` java    
        logstashAppender.setName("LOGSTASH");
    ` `` 
    ` `` java
    logstashAppender.setContext(context);
   ` `` 
   ` `` java
    String customFields = "{\"app_name\":\"" + appName + "\"}";  
    ` `` 
    ` `` java
        // Set the Logstash appender config from senthink properties
    ` `` 
    ` `` java
    logstashAppender.setSyslogHost(loggingProperties.getLogging().getLogstash().getHost());
    ` `` 
    ` `` java    
        logstashAppender.setPort(loggingProperties.getLogging().getLogstash().getPort());
    ` `` 
    ` `` java     
        logstashAppender.setCustomFields(customFields);
   ` `` 
   ` `` java
        // Limit the maximum length of the forwarded stacktrace so that it won't exceed the 8KB UDP limit of logstash
   ` `` 
   ` `` java     
        ShortenedThrowableConverter throwableConverter = new ShortenedThrowableConverter();
   ` `` 
   ` `` java     
        throwableConverter.setMaxLength(7500);
   ` `` 
   ` `` java     
        throwableConverter.setRootCauseFirst(true);
   ` `` 
   ` `` java     
        logstashAppender.setThrowableConverter(throwableConverter);
   ` `` 
   ` `` java
        logstashAppender.start();
   ` `` 
   ` `` java
        // Wrap the appender in an Async appender for performance
  ` `` 
  ` `` java    
       AsyncAppender asyncLogstashAppender = new AsyncAppender();
   ` `` 
   ` `` java     
        asyncLogstashAppender.setContext(context);
   ` `` 
   ` `` java     
        asyncLogstashAppender.setName("ASYNC_LOGSTASH");
   ` `` 
   ` `` java    
       asyncLogstashAppender.setQueueSize(loggingProperties.getLogging().getLogstash().getQueueSize());
   ` `` 
   ` `` java     
        asyncLogstashAppender.addAppender(logstashAppender);
   ` `` 
   ` `` java  
     asyncLogstashAppender.start();
   ` `` 
   ` `` java
        context.getLogger("ROOT").addAppender(asyncLogstashAppender);
    ` ``
    ###3.启动应用，访问http://localhost:5601，就能查看应用的相应日志。
 有任何问题欢迎咨询634603080    
  
