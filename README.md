# 宜立方商城

## 1、项目介绍

### 1.1 、项目简介

- 宜立方商城是一个基于SOA架构的购物网站，宜立方网上商城是一个综合性的B2C平台，类似京东商城、天猫商城。会员可以在商城浏览商品、下订单，以及参加各种活动。
- 管理员、运营可以在平台后台管理系统中管理商品、订单、会员等。
- 客服可以在后台管理系统中处理用户的询问以及投诉。

### 1.2、系统架构

宜立方商城系统架构缩略图

![商城系统架构图](C:\Users\lenovo\Desktop\商城系统架构图.jpg)



### 1.3、功能列表

功能列表系统图

![商城功能列表](C:\Users\lenovo\Desktop\商城功能列表.jpg)



整个商城分为如下几个子系统

- 后台管理系统：管理商品、订单、类目、商品规格属性、用户管理以及内容发布等功能。

- 前台系统：用户可以在前台系统中进行注册、登录、浏览商品、首页、下单等操作。

- 会员系统：用户可以在该系统中查询已下的订单、收藏的商品、我的优惠券、团购等信息。

- 订单系统：提供下单、查询订单、修改订单状态、定时处理订单。

  搜索系统：提供商品的搜索功能。

- 单点登录系统：为多个系统之间提供用户登录凭证以及查询登录用户的信息。

  

### 1.3、技术选型

- 基于soa架构的使用ssm整体后台框架的商城项目
- 使用dubbo服务治理工具，实现系统之间通信。使用zookeeper实现注册中心
- 使用FastDFS图片服务器保存图片，使用nginx访问图片服务器
- 采用KindEditor富文本编辑器
- 使用redis集群做缓存
- 使用solr服务作为搜索功能的实现
- 使用MQ实现系统之间通信
- 采用sso系统，主要解决的是Session共享的问题，使用redis管理Session。
- 采用mysql数据库
- 使用mycat实现数据分片，使用mycat实现数据库读写分离
- 项目采取伪分布式部署







