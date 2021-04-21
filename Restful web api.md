# Web API

* Web API通常是指“使用HTTP协议并通过网络调用的API”,由于它使用了HTTP协议，所以需要通过URI信息来指定端点。
* Web API就是一个Web系统，通过访问URI可以于其进行信息交互。

Tip:
    URI 统一资源标识
    URL 统一资源定位符

## 大多数的Web API并不是RESTful API

* Roy Fielding为REST风格的API指定了一套约束规范或者叫` 架构风格 `

## MVC模式

* MVC 是一种主要用来构建UI的架构模式
* 松耦合
* 关注点分离(separation of concerns)
* MVC不是一个完整的应用程序架构

## 如何MVC映射为API呢

* Model，它负责处理程序数据的逻辑
* View，它是程序里负责展示数据的那部分。在构建API的时候，View就是数据或资源的展示。现在通常使用JSON格式
* Controller，它负责View和Model之间的交互




# 2. 对外合约

## API消费者需要使用到三个概念

* 资源的标识
    * 可以找到资源的uri,uri就是标识
* HTTP方法
    * GET POST 等(也是HTTP协议的一部分)
* 有效载荷（可选）,英文就是Payload
    * 比如有Head里包含的一部分Media Type

## 资源命名

* 使用名词，而不是动词
    * 需求：获取所有用户
    * 错误做法：api/getusers
    * 正确做法：GET api/user

## 人类能读懂
* 能够直观通过命名理解


## 要体现资源的结构/关系
* 假设如果后端Api系统里面有若干种资源，而用户这个资源与其它的资源并没有直接的关系，这样的话获取用户资源的uri应该是api/users。而不是api/product/users，也不是api/catalogs/products/users，因为user和product或者catalog没有直接的关系。
* 通过id获取单个用户的uri应该是：api/users/{userId}，而不是api/userid/users。
* 这样写的好处是可以让api具有很好的可预测性和一致性。

>> 例子1
* 需求： 获取某个公司下的员工信息
* 建议做法： GET ` api/companies/{companyId}/employees `

>> 例子2
* 需求：我想获取某个公司的某个员工信息
* 建议做法：GET ` api/companies/{companyId}/employees/{employeeId} `

## 自定义查询怎么命名
* 需求：排序后返回所有user信息
* 建议做法：GET ` api/users?orderby=name `

## 例外

* 有一些需求总是无法满足的达到RESTful的约束
* 需求：获取所有用户的数量
* 妥协的做法：GET ` api/users/totalamountofuser `

## [ApiController]

* 这个属性是应用于Controller的，它其实并不是强制的。
* 会启用以下行为：
  * 要求使用属性路由(Attribute Routing)
  * 自动HTTP 400响应 (Model错误信息返回400)
  * 推断参数的绑定源
  * Multipart/form-data请求推断
  * 错误状态代码的问题详细信息

# 内容协商

## Accept Header
* Media Type（媒体类型）
  * application/json
  * application/xml
  * ...
* 406 Not Acceptable
* 输出格式
* ASP.NET Core里面对应的就是Output Formatters

## Content-Type Header
* Media Type(媒体类型)
  * application/json
  * application/xml
  * ...
* 输入格式
* ASP.NET Core里面对应的就是Input Formmatters


# Entity Model VS 面向外部的Model

## Entity Model
* Entity Framework Core使用的Entity Model是用来标识数据库里面的记录的。
## 面向外部的Model
* 而面向外部的model则标识了要传输的东西。这类model有时候叫做Dto，有时候叫做ViewModel。

## Entity Model 和 面向外部的Model应该分开
* 更佳健壮、可靠和更易于进化。


# ActionResult<T>
返回类型可以用它，可以不用IActionResult

# 添加AutoMapper

## Nuget
AutoMapper.Extensions.Microsoft.DependencyInjection
