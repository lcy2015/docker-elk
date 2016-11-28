# Docker ELK stack
##一、环境
     安装docker、docker-compose
     使用logback日志框架（其它的可以自己尝试，原理差不多）。
##二、运行elk服务
  docker-compose up
##三、后台运行elk服务
  docker-compose up -d
##四、配置应用，
   1.依赖jar
   logstash-logback-encoder     
   2. 贴出相应的配置，相应的位置依次填入logstash的配置文件里面的host和端口号，以及相应的应用名称（可以自己适当做添加）
        参照logbackConfiguration里的代码。
   3.启动应用，访问http://localhost:5601，就能查看应用的相应日志。
 有任何问题欢迎咨询634603080    
  
