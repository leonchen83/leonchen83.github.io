---
layout: page
title: "编译hadoop-2.5.2 native以及spark-1.3.0"
categories : "大数据，数据大"
description: ""
---
{% include JB/setup %}
## 1. 系统,软件,源码

    系统
    centos6.6

    软件
    maven-3.3.1
    jdk-8u20
    protobuf-2.5.0
    zlib-devel
    cmake
    gcc gcc-c++
    openssl-devel

    源码
    hadoop-2.5.2-src
    spark-1.3.0

## 2. root用户创建目录与软件下载  

    $:mkdir /usr/local/softwares
    $:pwd
    /usr/local/softwares
    $:ls
    apache-maven-3.3.1-bin.tar.gz jdk-8u20-linux-x64.tar.gz protobuf-2.5.0.tar.gz spark-1.3.0.tgz hadoop-2.5.2-src.tar.gz

## 3. 软件安装与解压

    $:yum install gcc gcc-c++
    $:yum install zlib-devel
    $:yum install cmake
    $:yum install openssl-devel

    $:cd /usr/local/softwares
    $:tar -xzvf apache-maven-3.3.1-bin.tar.gz
    $:tar -xzvf jdk-8u20-linux-x64.tar.gz
    $:tar -xzvf protobuf-2.5.0.tar.gz
    $:tar -xzvf spark-1.3.0.tgz
    $:tar -xzvf hadoop-2.5.2-src.tar.gz

    $:cd protobuf-2.5.0
    $:./configure
    $:make
    $:make install
    $:ldconfig

## 4. 设置环境变量

    $:vi ~/.bashrc

    export JAVA_HOME=/usr/local/softwares/jdk1.8.0_20
    export M2_HOME=/usr/local/softwares/apache-maven-3.3.1
    export M2=$M2_HOME/bin
    export MAVEN_OPTS="-Xmx2g -XX:MaxPermSize=512M -XX:ReservedCodeCacheSize=512m"
    export PATH=$JAVA_HOME/bin:$M2:$PATH

    $:source ~/.bashrc

## 5. Build hadoop 与spark

    $:cd hadoop-2.5.2-src
    $:mvn package -Pdist,native,src -DskipTests -Dtar -Dmaven.javadoc.skip=true

    $:cd spark-1.3.0 
    $:mvn -Pyarn -Phadoop-2.4 -Dhadoop.version=2.5.2 -DskipTests clean package

## 6. references

    hadoop-2.5.2-src/BUILDING.txt  
    http://spark.apache.org/docs/latest/building-spark.html