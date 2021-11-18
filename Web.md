## 第二章、简单的API调用
API:Application Programming Interface,应用程序接口。本质上就是一个url。
### 2.1 Get请求—无参数
无参数指代的是请求的url是无参数的。
开始前先要在pom.xml中安装依赖。

（1）步骤：
1. 实例化OkHttpClient。使用` OkHttpClient okHttpClient = new OkHttpClient();`

1. 实例化一个`Request`对象，作用是定义请求的各种参数。
    `Request request = new Request.Builder().url(url).build();`

1. 构建调用对象
    `Call call = okHttpClient.newCall(request);`

1. 执行调用，由于调用失败可能抛出异常，所以必须抓取异常。`call.execute()就是执行调用的代码`

1. call.execute()返回的其实是一个执行的结果对象，调用对象的方法即可获取返回的字符串内容：
    `call.execute().body().string();` 

### 2.4 POST表单数据
是先向要爬取的网址提交数据，然后再获得一个返回结果。
（1）步骤：
1. 实例化OkHttpClient。使用` OkHttpClient okHttpClient = new OkHttpClient();`

1. 创建post方式要提交的数据
`Builder builder = new FormBody.Builder();`//该句话定义一个空的表单数据容器。

1. 放入表单数据
由于在方法中会以Map数组形式传入一组数据，所以要用到for循环遍历Map对象formData来放入表单数据。
```
for(String key:formData.keySet()){//keySet()是自带方法
    builder.add(key,formData.get(key));

}
```

1. 构建FromBody 对象
`FormBody formBody = builder.build();`

1. 实例化一个`Request`对象，作用是定义请求的各种参数。指定**post方式提交FormBody** //多了个post(fromBody)

    `Request request = new Request.Builder().url(url).post(fromBody).build();`

1. 构建调用对象
    `Call call = okHttpClient.newCall(request);`

1. 执行调用，由于调用失败可能抛出异常，所以必须抓取异常。`call.execute()就是执行调用的代码`

1. call.execute()返回的其实是一个执行的结果对象，调用对象的方法即可获取返回的字符串内容：
    `call.execute().body().string();` 

1.传入的fromData的构造方式
```
Map<String,String> fromBody = new HashMap<>();

fromBody.put("","");

//调用
String content = poster.postContent(url,formBody);
```
