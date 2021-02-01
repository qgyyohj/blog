---
title: Maven配置阿里云仓库
date: 2021-01-31 22:54:00
tags:
---

> 默认配置下，maven速度慢得要死，替换镜像可以改善这个问题

查看maven的位置

```shell
echo $M2_HOME
```

查看maven的配置文件

```shell
cat $M2_HOME/config/settings.xml
```

查看生效的配置文件，

```shell
mvn help:effective-settings
```

查看当前目录下合并了所有父pom的最终pom

```shell
mvn help:effective-pom
```

maven的配置文件会放在`${maven.home}/conf/settings.xml`和` ${user.home}/.m2/settings.xml`两个目录下，前者是全局配置，后者是用户配置，用户配置会合并并覆盖全局配置

maven从主仓库拉镜像会非常慢，所以可以让maven去阿里的仓库中去拉依赖，在全局配置中用阿里云覆盖默认配置即可，mirrors中添加

```xml
<mirror>
    <id>alimaven</id>
    <name>aliyun maven</name>
    <url>http://maven.aliyun.com/nexus/content/groups/public/</url>
    <mirrorOf>central</mirrorOf>          
</mirror>
```
