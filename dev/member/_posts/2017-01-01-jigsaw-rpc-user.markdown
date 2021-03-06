---
layout: post 
title: "用户服务模块"  
subtitle: "infra文档"  
date: 2017-01-01 20:00:00  
author: "innkl"  
header-img: "img/home-bg-post.jpg"  
catalog: true  
chapter : "1.3" 
tag: [user]  
---

> 注意，这个文件必须以UTF-8无BOM格式编码。 


## 三户模型简介
  
三户模型最早是在增强型电信运营图（Enhanced Telecom Operations Map，eTOM）中提出，在电信行业中得到广泛使用。 
三户指客户（Customer）、用户（User）和账户(Account)。eTOM引入是电信行业营销模型转向“以客户为中心”的理念而产生的成果。
围绕客户建立用户和账户， 这三个是相互关联的实体。近年来，金融行业也逐步接受和采用了三户模型。

- **客户**，指自然人或者法人。法人一般被称之为企业客户。如无特指，一般客户指个人客户。
- **用户**，指通过注册的方式进入系统，使用系统提供的服务的实体， 也称为登录账户，即用户在系统中登录凭证和个人信息。 对应的， 
- **商户**，法人客户在系统中注册后，被称之为商户。
- **账户**，这里特指支付账户， 指用户在支付系统中用于交易的资金所有者权益的凭证。


本次主要从以下几个维度来分析下用户体系做什么？怎么做？为什么这么做？

我们先来看一张用户的生命周期图：
![](http://static.cocolian.org/img/rpc-user/smzq.png)

### 用户概念

用户，其实就是系统的使用者，一个登录账号就是一个用户，比如微博账号、微信账号、QQ账号等；
用户是账户的操作实体，它是由客户来注册到系统中来的。 虽然用户通过客户间接的拥有了资金账户，但这种关系并不是绝对的，
比如，一个用户可以授权另一个用户进行账户的余额查询。所以，用户与资金账户之间我们可以抽象出一种授权关系，
凡是授权用户，都可以操作资金账户，当然，这种授权包括客户自己的用户。用户的建立比较简单，一般自助注册后就可以生成用户实体了。

### PDM模型

1. PDM模型是这样的,手机号是通过映射关系，关联到用户。也就是说，用户是用户，手机号是手机号，这是两个维度，用户不变，手机号可变手机号，我们只是将它作为用户注册 和登录的标识而已，是个外部标识，比如用户可以换号，手机号也可以易主，所以，在建立用户模型时，手机号不能作为用户这个主体的系统主键，用户的系统主键我们用用户ID来标识
2. 用户表的主键是USER_ID，这是一个非常重要的表，主键将来都是要分区，分表的，设计时候很关键。



## 接口1：用户开户
> 接口模板要素:在文档设计的时候，要有接口名称，功能说明，入参列表、出参列表。对于用户开户这个功能来说，我们前面已经说过了，入参有两个，一个是手机号，一个是手机动态验证码，这两个是必须的，在文档中要写明，不能为空，在编码的时候，这两个字段是要有@NotNull的注解的。有了注解后，非空字段的校验就可以由系统框架系统处理了.

### 功能说明

用户开户，也就用户注册，是用户系统最基本的功能。用户开户，其实就是将用户的账号信息登记到系统中的一次交易。最简单一个用户注册，至少要有一个账号，也就是用户名，现在大部分系统在设计的时候，都是手机号走天下，主推用户手机号注册，有不少公司称之为获客，由此可见，开户功能对于企业的重要性。其实，手机号看似不起眼，就是一串数，企业要的不是手机号，而是手机号后面这个真实的人，也就是客户。所以，开户必须支持手机号注册，同时为了验证手机号的有效性（此手机号归属于客户本人），要通过验证码来核实，所以，同时引深出用户系统的另外几个功能：验证码短信下发＼验证码重发＼验证码验证等功能。同时引深的内部功能还有手机号是不是已经被使用，这个手机号是不是虚拟号，是哪个运营商的，是不是在黑名单列表等。所以，一个最简单的注册接口（简易接口），至少要上送两个字段：手机号与验证码。

### 输入参数

### 输出参数

### 处理逻辑

## 接口2：XXX

### 功能说明

### 输入参数

### 输出参数

### 处理逻辑

