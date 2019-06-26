# rammus

阿里云推送Flutter插件.

## Getting Started


> Rammus是在一位热心网友的赞助下开发的并将其开源。在此特别感谢这位朋友。
> 欢迎加入QQ群：892398530共同交流。

## 麻烦先读一下官方文档

[麻烦读下推送官方文档](https://help.aliyun.com/document_detail/51056.html?spm=a2c4g.11186623.6.623.47bf59abvM9j25)

## Android上的配置

### 设置appKey,appSecret

在`AndroidManifest.xml`设置appKey,appSecret

```
        <meta-data
            android:name="com.alibaba.app.appkey"
            android:value="" /> <!-- 请填写你自己的- appKey -->
        <meta-data
            android:name="com.alibaba.app.appsecret"
            android:value="" /> <
```

> 也可以动态设置，具体方式看官方文档

### 初始化SDK

好吧，由于SDK的限制，用户只能在`Application`中的`onCreate`里初始化：

```
        PushServiceFactory.init(applicationContext)
        val pushService = PushServiceFactory.getCloudPushService()
        val callback = object : CommonCallback {
            override fun onSuccess(response: String?) {
                Log.e("TAG","success $response")

            }

            override fun onFailed(errorCode: String?, errorMessage: String?) {
            Log.e("TAG","error $errorMessage")

            }
        }

        pushService.register(applicationContext,callback)
        pushService.setPushIntentService(RammusPushIntentService::class.java)

```

`pushService.setPushIntentService(RammusPushIntentService::class.java)`千万不要忘记设置了。

> Application在Android原生项目里。不会创建的自行百度。