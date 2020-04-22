# Elasticsearch

## 第一章  介绍

ElasticSearch 搜索ES，全文检索数据，底层就是luch

https://www.elastic.co/cn/what-is/elasticsearch

### ES对比Solr

Solr利用zookeeper进行分布式管理，而EX自身有分布式协调管理功能
Solr支持多格式数据，Es只支持json
ES处理实时搜索效率比solr高。

## 第二章 安装插件

### ES 安装

 https://www.elastic.co/cn/downloads/past-releases/elasticsearch-5-6-8
最低版本java 1.8以上版本

http://localhost:9200/

9200 是ES节点与外部通讯接口 HTTP协议
9300 是ES节点之间通讯接口 TCP通讯接口

### 图形界面插件，head插件

https://github.com/mobz/elasticsearch-head

elasticsearch-head-master Node.js开发

### 安装node.js   node -v

cmd打开elasticsearch-head-master 路径
grunt 安装命令（npm install -g grunt-cli）  grunt基于node.js 的项目构建工具。
cmd打开 elasticsearch-head-master 路径，npm install 和 	grunt server(启动)

如果不能成功连接ES服务，需要修改elasticsearch的config目录下的 elasticsearch.yml
增加以下两句命令：

http.cors.enabled: true
http.cors.allow-origin: "*"

然后重启启动elasticsearch服务。



## 第三章：elasticsearch 概念

elasticsearch 面向文档，里面的索引indices，也有多张表Types, 多个文档document，多个fieds

elasticsearch 和数据库对比
DB->Databases->tables->rows->columns
ES->indices  ->Types-->documents->fields

1.索引：索引库，多个types集合，类似于数据库，可以存储无数个文档，
类型type：表
文档：一行数据
字段field：字段
映射，每个表中的域，字段是否分词、表结构的定义
集群：es
节点：就是一台服务器，每个节点都有一个名词
分片和复制：一片，每个节点都有一个备份节点。

## 第四章：postman工具

### postman插件安装

https://www.postman.com/downloads/

### 1.创建索引index和

```
{
	"mappings":{
		"article":{
			"properties":{
				"id":{
					"type":"long",
					"store":true					
				},
				"title":{
					"type":"text",
					"store":true,
					"index":true,
					"analyzer":"standard"				
					

				},
				"content":{
					"type":"text",
					"store":true,
					"index":true,
					"analyzer":"standard"
				}
			}
		}
	
	}

}
```

### 索引库添加mappings

 http://127.0.0.1:9200/eachonline1/hello/_mappings

```
{
	"hello":{
			"properties":{
				"id":{
					"type":"long",
					"store":true					
				},
				"title":{
					"type":"text",
					"store":true,
					"index":true,
					"analyzer":"standard"				
					

				},
				"content":{
					"type":"text",
					"store":true,
					"index":true,
					"analyzer":"standard"
				}
			}
		}

}
```

### 关键字查询

http://127.0.0.1:9200/eachonline1/hello/_search

```
{
	"query":{
		"term":{
			"title":"修" //分词器只有有一个字查询
		}
	}
}
```

### queryString查询

http://127.0.0.1:9200/eachonline1/hello/_search

```
{
	"query":{
		"query_string":{
			"default_field":"title",
			 "query":"文档"
		}
	}
}
```

## 第五章 IK分词器

### 安装插件：

https://github.com/medcl/elasticsearch-analysis-ik/releases?after=v6.2.4

v5.6.8

IK提供两种算法
ik_smart(为最少切分)  
ik_max_word（为最细粒度划分）拆分比较细，关键字比较多



## 第六章 Es集群

集群 cluster：多个服务器组织的结构，，一个集群都有一个唯一的标识。也就是名字

节点node： 某一台服务器就是一个节点

分片和复制：es默认分片是5片，某个节点都有一个备份节点，这种叫做复制节点。

集群配置信息elasticsearch.yml

#节点1的配置信息：
#集群名称，保证唯一
cluster.name: my-elasticsearch
#节点名称，必须不一样
node.name: node-1
#必须为本地的IP地址
network.host: 127.0.0.1
#服务器端口，在同一个机器下必须不一样
http.port: 9201
#集群间通信端口号，在同一个机器侠必须不一样呀
transport.tcp.port: 9301
#设置集群自动发现机器IP集合
discovery.zen.ping.unicast.hosts: ["127.0.0.1:9301","127.0.0.1:9302","127.0.0.1:9303"]



## JAVA客户端管理ES

1.创建索引库
	步骤
	1.创建java工程      
	2.添加jar包，添加maven的坐标
	3.编写测试方法实现
		1.创建一个setting对象，配置信息，配置集群的名称
		2.创建一个客户端client对象
		3.使用client对象创建一个索引库
		4.关闭client对象
		