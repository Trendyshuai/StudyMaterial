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


