2020-3-15

### <font color='aadd'>页面上加载局部视图</font>

一、` @Html.Action("action", "controller", new { param1 = "ok", param2 = 2 }); ` 通过Action 返回  return View("局部视图", Model);将Model对象通过局部视图呈现到页面

二、` @Html.Partial("~/Views/Shared/compontent/_header_nav.html", Model) `，把父页面数据，通过局部视图，呈现页面到页面

三、` $("#selector").load(@Url.Action("action", "controller",参数) ` 局部无刷新呈现 ，Action 返回： return View("局部视图", Model);


### <font color='aadd'>正常的页面结构：</font>

``` html
@model SingleStore.Models.Account.LoginViewModel
@{
    ViewBag.Title = "Product List";
    ViewBag.KeyWords = "";
    ViewBag.Description = "";
}
    <div class="content">
      
        <!--上部-->
        <!--主体部分-->
        <!--左侧部分-->
        <!--右侧部分 -->
        <!--下部-->
        
    </div>

<!--每个页面自定义脚本与css，没有可以不添加-->
@section styles{
    <link rel="stylesheet" href="../Content/product.css" type="text/css" />
    <style>
    </style>
}

@section scripts{
    <script src="../scripts/product.js"></script>
    <script>
            //自定义js
    </script>
}
```

### <font color='aadd'>返回语言切换列表：</font>

``` C#
   @foreach (var l in CultureSiteInfoProvider.GetSiteCultures(SiteContext.CurrentSiteName))
    {
        @Html.CultureLink(l.CultureShortName, l.CultureName)<br />
    }
```

### <font color='aadd'>当前语言：</font>

``` C#
    @Html.CultureLink(Culture, Culture)
    @foreach (var l in CultureSiteInfoProvider.GetSiteCultures(SiteContext.CurrentSiteName))
    {
        @Html.CultureLink(l.CultureName, l.CultureCode)<br />
    }
```

### <font color='aadd'>主模板：正常格式如下</font>
``` html
@using Kentico.PageBuilder.Web.Mvc
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>@ViewBag.Title</title>
    <link rel="icon" href="@Url.Content("~/content/images/favicon.png")" type="image/png" />
    <meta name="keywords" content="@ViewBag.KeyWords" />
    <meta name="description" content="@ViewBag.Description" />
    <link rel="canonical" href="@Url.CanonicalUrl()" />
    @Styles.Render("~/Content/bootstrap")
    @Html.Kentico().ABTestLoggerScript()
    @RenderSection("styles", required: false)<!--子页面自定义CSS位置-->
</head>
<body>

    @Html.Action("Header", "Home")<!--头部视图-->

    @RenderBody()

    @Html.Action("Footer", "Home")
    <!--尾部视图--  视图局部视图名规则(前面加_)如 "~/Views/Shared/_footer.chtml">

       @Scripts.Render("~/bundles/jquery")
       @Scripts.Render("~/bundles/bootstrap")
       @Scripts.Render("~/bundles/Main.js")   <!--头部和底部js逻辑放在这里-->
    @RenderSection("scripts", required: false) <!--子页面自定义脚本位置-->
    @Html.Kentico().ActivityLoggingScript()
</body>
</html>
```

### <font color='aadd'>根据路由生成链接</font>
```
@Url.RouteUrl("Product", new {guid = Model.ProductPageGUID, productAlias = Model.ProductPageAlias})
```
### <font color='aadd'>生成不同尺寸图片，对于生成缩略图有用</font>
```
@Html.Image(@Model.ImagePath, @Model.Name, null, SizeConstraint.Size(452, 452))  
```

### <font color='aadd'>（方便货币切换）商品价格显示：</font>
```
String.Format(currency.CurrencyFormatString, price.Price)
```

可以看下QueryHelper 这个类获取URL参数（view和controller 中都可以用）， 如： @QueryHelper.GetInteger("参数名",默认值)，可以获取不同类型的数据，如@QueryHelper.GetInteger("orderid",0) ,



