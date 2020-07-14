## 索引创建

``` SQL
IF EXISTS(SELECT * FROM xxxxx WHERE name='索引名')
DROP INDEX 表名.索引名
GO

CREATE [UNIQUE] [CLUSTERED] [NONCLUSTERED]
INDEX 索引名
ON 表名(列明)
[WITH FILLFACTOR=x]
```

* UNIQUE:唯一索引
* CLUSTERED | NONCLUSTERED: 聚集索引或非聚集索引
* FILLFACTOR: 填充因子(系数):指定一个0~100之间的数，表示索引页填充的百分比


## 如何使用索引

* 用户地址是河北的有哪些
``` SQL
SELECT * FROM UserInfo
WITH(INDEX=IX_UserInfo_UserAddress)
WHERE UserAddress LIKE '%河北%'
```

## 存储过程

存储过程

* 预编译SQL语句的集合
* 代替了传统的逐条执行SQL语句的方式
* 可包含查询，插入，删除，更新等操作的一系列SQL语句
* 存储在SQL Server中
* 通过名称和参数执行
* 可带参数，也可返回结果
* 可包含数据操纵语句，变量，逻辑空军语句

存储过程的优点

* 执行速度更快
* 允许模块化程序设计
* 提高系统安全性
* 减少网络流通量

重要优点： 安全且执行速度快


## 存储过程的分类

* 系统存储过程
  * sp_开头
* 扩展存储过程
  * xp_开头
* 自定义存储过程
  * usp_开头

## 存储过程的调用

``` SQL
EXECUTE 过程名[参数]
或
EXEC 过程名[参数]
```

## 创建不带参数的存储过程

语法

``` SQL
CREATE PROC[EDURE] 存储过程名
AS
    SQL语句
GO  -- 必须要加批处理
```

例：题目【查看xiangxiang所购买的商品信息，包括用户号，付款方式，购买数量，商品名称】
``` SQL
IF EXISTS(SELECT * FROM sysobjects WHERE name='usp_GetCommodityInfo')
DROP PROC usp_GetCommodityInfo
GO

CREATE PROC usp_GetCommodityInfo
AS
    SELECT O.UserId AS 用户号, PayWay AS 付款方式, O.Amount AS 购买数量, C.CommodityName AS 商品名
    FROM OrderInfo AS O
    INNER JOIN CommodityInfo AS C ON O.CommodityId=C.CommodityId
    INNER JOIN CommoditySort AS S ON C.SortId
    WHERE O.UserId='xiangxiang'
GO
```

如何使用不带参数的存储过程
``` SQL
EXEC usp_GetCommodityInfo
GO
```

## 创建带输入参数的存储过程

语法

``` SQL
CREATE PROC 存储工程名
    @参数1 数据类型=默认值,
    @参数2 数据类型=默认值
AS
    SQL语句
GO --必须要加批处理
```

例：题目【查询指定的用户在指定的时间段内的下单信息，如果结束日期没有指定的话，那么查询的是到今天为止的下单信息】

``` SQL
IF EXISTS(SELECT * FROM sysobjects WHERE name='usp_GetOrderInfo')
GO

CREATE PROC usp_GetOrderInfo
    @startDate datetime, -- 开始时间
    @endDate datetime=null, -- 结束时间
    @userId varchar(20)=null --指定的用户
AS
    IF @endDate IS NULL -- 判断结束日期是否为空
        BEGIN
            SET @endDate=GETDATE() --赋当前日期
        END
    IF @userId IS NULL -- 查询指定时间段内的所有订单信息
        BEGIN
            SELECT C.CommodityName AS 商品名称, S.SortName AS 类别名称, O.UserId AS 用户名, O.OrderTime AS 下单时间
            FROM OrderInfo AS O
            INNER JOIN Commodity AS C ON O.CommodityId=C.CommodityId
            INNER JOIN CommoditySort AS S ON C.SortId=S.SortId
            WHERE O.OrderTime BETWEEN @startDate AND @endDate
        END
    ELSE
        BEGIN
            SELECT C.CommodityName AS 商品名称, S.SortName AS 类别名称, O.UserId AS 用户号, O.OrderTime AS 订单时间 FROM OrderInfo AS O
            INNER JOIN CommodityInfo AS C ON O.CommodityId=C.CommodityId
            INNER JOIN CommoditySort AS S ON S.SortId=C.SortId
            WHERE(O.OrderTime BETWEEN @startDate AND @endDate) AND O.UserId=@userId
        END
GO
```

如何调用带参数的存储过程
``` SQL
-- 隐式调用
EXEC usp_GetOrderInfo '2014-11-1'
-- 显式调用
EXEC usp_GetOrderInfo @startDate='2014-11-1'
-- 通过声明变量调用
DECLARE @d1 datetime, @d2 datetime, @uid varchar(20)
SET @d1='2014-11-1'
SET @d2='2014-12-1'
SET @uid='xiangxinag'
EXEC usp_GetOrderInfo @d1, @d2, @uid
```

## 创建带输出参数的存储过程

语法
``` SQL
CREATE PROC[EDURE] 存储过程名
    @参数1 数据类型=默认值 OUTPUT,
    @参数2 数据类型=默认值 OUTPUT
AS
    SQL语句
GO -- 必须加批处理
```

例：题目【向母婴用品这个类别添加一种商品，要求成功后把商品的编号输出】

``` SQL
IF EXISTS(SELECT * FROM sysobjects WHERE name='usp_InsertCommodity')
DROP PROC usp_InsertCommodity
GO

CREATE PROC usp_InsertCommodity
    @SortName varchar(50),
    @CommodityName varchar(100),
    @Inprice money,
    @Outprice money,
    @Amount int,
    @Commodity int output -- 输出参数
AS 
    DECLARE @SortId int
    SELECT @SortId=SortId FROM CommoditySort WHERE SortName=@SortName
    IF @SortId IS NULL
        BEGIN
            PRINT '对不起，输入的类别不存在！'
            RETURN -- 后面的代码无条件，退出了创建存储过程
        END
    INSERT INTO CommodityInfo(SortId,CommodityName,InPrice,OutPrice,Amount) VALUES(@SortId,@CommodityName,@Inprice,@Outpirce,@Amount)

    IF @@ERROR > 0
        BEGIN
            PRINT '插入信息失败！'
            RETURN
        END
    
    SET @CommodityId=@@IDENTITY
GO
```

使用带输入输出参数的存储过程
``` SQL
DECLARE @sortName varchar(50), @commodityName varchar(100), @inprice money, @outprice money, @mount int, @commodityId int
SELECT @sortName='母婴用品', @commodityName='星飞帆1段', @inrpice=23, @outprice=245, @mount=1000

EXEC usp_InsertCommodity @sortName, @commodityName, @inprice, @outprice, @mount, @commodityId output
PRINT '添加商品成功，商品编号为：'+CONVERT(varchar(5),@commidityId)
```

## 带返回值的存储过程

* 使用<font color='blue'>RETURN</font>关键字进行返回

* 遇到<font color='blue'>RETURN</font>关键字存储过程中的后续代码无条件不执行，即退出了当前的存储过程

* 根据返回值对存储过程的结果做出相应的处理

``` SQL
IF EXISTS(SELECT * FROM sysobjects WHERE name='usp_InsertCommodityReturn')
DROP PROC usp_InsertCommodityReturn
GO

CREATE PROC usp_InsertCommodityReturn
    @sortName varchar(50),
    @commodityName varchar(100),
    @inprice money,
    @outprice money,
    @amount int,
    @commodityId int output
AS
    DECLARE @sortid int
    SELECT @sortid=SortId FROM CommoditySort WHERE SortName=@sortName
    IF @sortid IS NULL
        BEGIN 
            RETURN -1 -- 用-1来代表类别名称不正确
        END
    INSERT INTO CommodityInfo(SortId,CommodityName,InPrice,OutPrice,Amount) VALUES(@SortId,@CommodityName,@Inprice,@Outpirce,@Amount)

    IF @@ERROR > 0
        BEGIN
            RETURN 0 -- 用0来代表插入信息失败
        END
    ELSE
        BEGIN
            RETURN @@IDENTITY
        END
GO
```

使用返回值
@Result

## 创建和使用存储过程的注意事项

注意事项
* 有多个参数时，<font color='red'>有默认值的参数放在存储过程参数列表的最后</font>
* 在创建存储过程的代码结束时，要加上批处理go，如果不加go，那么调用存储过程的语句将被包含在创建存储过程的代码中，造成存储过程被递归调用
* 在调用带多个参数的存储过程的时候，要求按照存储过程的参数顺序一次传递，如果不按照顺序传递那么必须指定参数名
* 一旦某一个参数按“@参数名=参数值”格式传递参数，那么该参数之后的其他参数都必须以同样的格式传递参数值


