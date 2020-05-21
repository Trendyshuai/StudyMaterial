# <center>在` ASP.NET MVC `中使用PayPal</center>
1. 在Paypal官网注册测试用的商家账号
   * 在 https://developer.paypal.com/developer/accounts/ 中获取你的ClientID和ClientSecret。
2. 在ASP.NET项目中安装paypal NuGet 包
   * 用Visual Studio打开项目
   * 工具->NuGet包管理器->管理解决方案的NuGet程序包->浏览
   * 搜索Paypal安装即可
3. 在` Web.config `文件中添加配置
``` xml
<configuration>
  <configSections>
    <section name="paypal" type="PayPal.SDKConfigHandler, PayPal" />
  </configSections>
  <!-- PayPal SDK settings -->
  <paypal>
    <settings>
      <add name="mode" value="sandbox"/>
      <add name="connectionTimeout" value="360000" />
      <add name="requestRetries" value="1" />
      <add name="clientId" value="你的ID"/>
      <add name="clientSecret" value="你的密钥"/>
    </settings>
  </paypal>
</configuration>
```

4. 添加Paypal配置类 (` PaypalConfiguration.cs `)
``` C#
using PayPal.Api;
using System.Collections.Generic;

namespace SingleStore.Helpers
{
    public class PaypalConfiguration
    {
        public readonly static string clientId;
        public readonly static string clientSecret;

        // 构造函数
        static PaypalConfiguration()
        {
            var config = GetConfig();
            clientId = config["clientId"];
            clientSecret = config["clientSecret"];
        }

        // 从web.config里得到属性
        private static Dictionary<string, string> GetConfig()
        {
            return ConfigManager.Instance.GetProperties();
        }

        // 从paypal得到AccessToken
        private static string GetAccessToken()
        {
            string accessToken = new OAuthTokenCredential(clientId, clientSecret, GetConfig()).GetAccessToken();
            return accessToken;
        }

        // 通过调用accesstoken来返回apicontext对象
        public static APIContext GetAPIContext()
        {
            APIContext apiContext = new APIContext(GetAccessToken())
            {
                Config = GetConfig()
            };
            return apiContext;
        }
    }
}
```

5. 在Controller中创建` PaypalWithPayPal `、` ExecutePayment `、` CreatePayment `方法(` PaymentController.cs `)
``` C#
using PayPal.Api;
using SingleStore.Helpers;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Web.Mvc;

namespace SingleStore.Controllers
{
    public class PaymentController : Controller
    {
        public ActionResult PaymentWithPaypal(string Cancel = null)
        {
            APIContext apiContext = PaypalConfiguration.GetAPIContext();

            try
            {
                string payerId = Request.Params["PayerID"];
                if (string.IsNullOrEmpty(payerId))
                {
                    // payerId被执行，因为为空
                    string baseUri = Request.Url.Scheme + "://" + Request.Url.Authority +
                        "/en-us/Payment/PaymentWithPaypal?";

                    // 生成一个guid，用来存放付款的请求
                    var guid = Convert.ToString((new Random()).Next(100000000));

                    // paypal返回付款批准的请求
                    var createdPayment = CreatePayment(apiContext, baseUri + "guid=" + guid);

                    var links = createdPayment.links.GetEnumerator();

                    string paypalRedirectUrl = null;

                    while (links.MoveNext())
                    {
                        Links lnk = links.Current;

                        if (lnk.rel.ToLower().Trim().Equals("approval_url"))
                        {
                            paypalRedirectUrl = lnk.href;
                        }
                    }
                    // session里存guid
                    Session.Add(guid, createdPayment.id);
                    // paypal付款页面
                    return Redirect(paypalRedirectUrl);
                }
                else
                {
                    var guid = Request.Params["guid"];
                    
                    var executePayment = ExecutePayment(apiContext, payerId, Session[guid] as string);

                    if (executePayment.ToString().ToLower() != "approved")
                    {
                        return View("FailureView");
                    }
                }
            }
            catch (Exception)
            {
                return View("FailureView");
                //throw;
            }

            return View("SuccessView");
        }

        private Payment payment;

        private Payment ExecutePayment(APIContext apiContext, string payerId, string paymentId)
        {
            var paymentExecution = new PaymentExecution()
            {
                payer_id = payerId,
            };

            payment = new Payment() { id = paymentId };

            var executedPayment = payment.Execute(apiContext, paymentExecution);

            return executedPayment;
        }


        private Payment CreatePayment(APIContext apiContext, string redirectUrl)
        {
            // 商品明细
            var itemList = new ItemList()
            {
                items = new List<Item>()
            };

            // 判断，根据业务需求，判断购物车是否为空等。
            if (true)
            {
                //foreach (var item in 1)
                //{

                //}

                // 增加明细的细节
                itemList.items.Add(new Item()
                {
                    name = "产品名",
                    currency = "USD",
                    price = "1",
                    quantity = "1",
                    sku = "sku"
                });

                var payer = new Payer()
                {
                    payment_method = "paypal"
                };

                var redirUrls = new RedirectUrls()
                {
                    cancel_url = redirectUrl + "&Cancel=true",
                    return_url = redirectUrl
                };

                // 税，运费，折扣等
                var details = new Details()
                {
                    tax = "1",
                    shipping = "1",
                    subtotal = "1" // 商品总计
                };

                // 费用合计
                var amount = new Amount()
                {
                    // 货币，应取出货币格式
                    currency = "USD",
                    // 总额必须等于税金、运费和小计之和
                    total = "3",

                    details = details
                };

                var transacationList = new List<Transaction>();
                transacationList.Add(new Transaction()
                {
                    description = "Transaction Description",
                    // 发票号，注意不要重复，否则Paypal会返回400
                    invoice_number = "#1000000",
                    amount = amount,
                    item_list = itemList,
                });

                payment = new Payment()
                {
                    intent = "sale",
                    payer = payer,
                    transactions = transacationList,
                    redirect_urls = redirUrls
                };
            }

            // 使用APIContext创建支付
            var apicon = payment.Create(apiContext);

            return apicon;
        }
    }
}
```
6. 建立两个视图
   * Failure.cshtml
   * Success.cshtml
