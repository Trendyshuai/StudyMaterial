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




