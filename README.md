# 拟酷网络登陆计费SDK服务器接入帮助文档 #


## 1. 登陆验证  ##

#### 登陆验证地址  ####

http://new.login.nikugame.com/json

#### 请求方式	####

POST

#### 请求参数	 ####

数据类型 ： json 

名称|数据类型|含义
------|----------|----------
uuid| string|用户唯一标识符
token| string | 登陆返回的验证密码

示例： 

	{"uuid":"nk_di29IOxx12xase21l", "token":"ei9234kxac821daDDaae1223"}

#### 返回参数 ####

数据类型： json

名称|数据类型|含义
----|----|----
success | string | true:成功; false:失败 

## 2. 充值回调 ##

充值回调地址，由游戏运维方在游戏接入时提供，配置错误可导致充值不到账。

#### 请求方式	####

POST

#### 请求参数	 ####

数据类型 ： json 

名称|数据类型|含义
------|----------|----------
cporderid | string|拟酷网络充值订单号
uuid| string | 用户唯一标识符
amount| float64 | 充值金额
extra| string | 游戏透传参数（长度不要超过200字符）
sign| string | 数据签名（[签名方式](#jump)）

示例： 

	{ "cporderid":"o12345678", "uuid":"12345667899" "amount":648.00 "extra":"cp透传参数" "sign":"asdfasdfasdfasdfasdfasd" }

#### 返回参数 ####

数据类型： body-data

SUCCESS: 游戏成功收到充值通知
FAILURE: 游戏充值失败，充值服务器会按照固定周期进行重复尝试，直到游戏响应正确的返回或者周期结束

* 注意： 游戏需要对重复充值的回调进行处理！


## 3. 签名方式 ##
<span id="jump">

对 cporderid，uuid，amount（浮点数模式，保留小数点后两位），extra透传参数，游戏拿到的PayKey，拼接的字符串进行MD5加密得到的加密串，(拼接不要添加任何字符串在中间，只需要对参数的值进行拼接)

	sign=md5(cporderid+uuid+amount+extra+PayKey)

PayKey需要在平台创建游戏时生成，登陆拟酷网络发行平台后台管理系统获取

</span>



<div class="footer">
	&copy; 2016 nikugame, Inc.
</div>
