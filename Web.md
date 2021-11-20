## 第二章、简单的API调用
**API:Application Programming Interface,应用程序接口。本质上就是一个url。**
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

1. 传入的fromData的构造方式
    ```
    Map<String,String> fromBody = new HashMap<>();

    fromBody.put("","");

    //调用
    String content = poster.postContent(url,formBody);
    ```

### 2.5 post提交JSON格式

可以将Map直接转换为JSON，但首先需要添加json的操作库。groupId为`com.alibaba`。
```
<groupId>com.alibaba</groupId>
<artifactId>fastjson</artifactId>
<version>1.2.62</version>
```

然后调用`String a = JSON.toJSONString(fromData);`

接着调用`RequestBody resquestBody = RequestBody.create(JSON_TYPE,a);`
>这边的JSON_TYPE是定义的常量：`private static final MediaType JSON_TYPE = MediaType.parse("application/json; charset=utf-8");`

之后将requestBody作为参数，像上一节中的fromBody传给Request request = new Request.Builder().url(url).post(requestBody).build();

### 3.1 Response

（1）`call.execute().code()`能够返回网页的请求响应状态码，如404表示出错，200表示成功
（2）由于执行请求只能进行一次，而有可能既需要状态码，又需要具体的内容，所以可以将代码优化如下：
```
import okhttp3.Response;
// 执行请求
Response rep = call.execute();
// 获取响应状态码
int code = rep.code();
// 获取响应内容
String content = rep.body().string();
```

### 3.2 Response-非文本文件
非文本文件指的是图片、excel等各种文件。
图片的内容是二进制编码，需要软件解析图片的二进制编码数据，才能还原成图像显示。所以请求图片等非字符文本文件时，要使用：`response.body().bytes();`

具体为`byte[] bytes =response.body().bytes(); `

### 3.3 Response-JSON
将爬取的JSON格式数据反序列化为对象。以Map为例子
`Map content = JSON.parseObject(content,Map.class);`
>其中content为爬取的String类型的网页内容（是JSON）

### 3.4 解析JSON对象
```
Map contentObj = JSON.parseObject(content, Map.class);
Map dataObj = (Map)contentObj.get("data");
String city = (String)dataObj.get("city");
```

## 第四章、headers
### 4.1 User-Agent
HTTP消息头Headers是HTTP协议的一项重要内容，作用是在发起请求的时候，除了请求参数外，可以附加更多的信息。

User-Agent解决程序请求HTTP不成功的情况。

### 4.2 Referer
图片防盗链，爬取图片无法访问的问题。
解决：把Referer信息设置为图片原始使用的网站。
在后面章节中会指定如何使用工具查找Referer值。
