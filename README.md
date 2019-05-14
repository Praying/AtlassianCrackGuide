# AtlassianCrackGuide
Jira, Confluence crack install guide

Jira, Confluence 破解安装教程

- 安装JDK8.0或以上版本

- 安装MySQL

- 下载mysql-connector-java, 版本要在8以下，8亲测是会出问题，

- 下载并解压[atlassian-agent](atlassian-agent), 感谢作者@pengzhile

- Mysql分别建立jira数据库和confluence数据库
```
create database jira default character set utf8 collate utf8_bin;

grant all on jira.* to jira@'%' identified by 'jirapasswd';

create database confluence default character set utf8 collate utf8_bin;

grant all on confluence.* to 'confluence'@'%' identified by 'confluencepasswd';

flush privileges;
```

- 下载jira和confluence安装包，Linux 64位bin,下面以confluence为例，进行按照，confluence类似
```
//可能存放路径各有不同，自行修改
sudo ./atlassian-confluence-6.15.4-x64.bin

sudo cp mysql-connector-java-5.1.39-bin.jar /opt/atlassian/confluence/confluence/WEB-INF/lib

sudo cp atlassian-agent-v1.2.2/atlassian-agent.jar /opt/atlassian/confluence/

```

- 修改  /opt/atlassian/confluence/bin/setenv.sh, 
```
sudo vim bin/setenv.sh
```
```
# 添加这一行到 export CATALINA_OPTS 前面
CATALINA_OPTS="-javaagent:/opt/atlassian/jira/atlassian-agent.jar ${CATALINA_OPTS}" 
```
- 进入/opt/atlassian/confluence/bin目录，执行
```
sudo ./start-confluence.sh
```

- 安装到需要输入License的那一步，记下上面的服务器ID，比如BNSS-82Q4-VNGO-PWE5，和你的服务器IP，如192.168.97.30  执行atlassian-agent.jar包进行破解
```
 java -jar atlassian-agent.jar -d -m test@test.com -n BAT -p conf -o http://192.168.97.30 -s BNSS-82Q4-VNGO-PWE5
```
将输出的license 拷贝粘贴上去即可，如果装了confluence的Team Team Calendars插件和Questions插件，继续执行
```
 java -jar atlassian-agent.jar -d -m test@test.com -n BAT -p tc -o http://192.168.97.30 -s BNSS-82Q4-VNGO-PWE5
 java -jar atlassian-agent.jar -d -m test@test.com -n BAT -p questions -o http://192.168.97.30 -s BNSS-82Q4-VNGO-PWE5
```
- 共享目录，可以自己创建一个目录，然后所有者改为confluence即可
```
sudo chown confluence /var/atlassian/application-data/confluence_share
```
- 数据库连接方面，jdbc的url后面加上 
```
?useSSL=false
```
- 剩下基本就没啥问题了，Mysql如果还有问题，搜一下应该就能解决，改一下配置重启MySQL就行了。Jira安装基本类似，更为简单，有时间再更。有问题提issue!基本的坑都踩过了。
- 欢迎star!
