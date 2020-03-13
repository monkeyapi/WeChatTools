# WeChatTools
实时微信域名检测API接口应用场景及代码分享 http://www.monkeyapi.com/
#微信域名检测API接口的应用场景
>>由于微信对外部链接内容规范比较严格，所以可能一不小心就会被判定为是违反内容规范的，或被同行恶意举报投诉之类的。那么此时就要用到微信域名检测接口，实时检测域名的状态，实时查询域名是否被微信拦截，从而才可以防患于未然，不影响推广。下面分享微信域名检测API接口，是采用微信官方接口打造，并有第三方协作支持，可以实时检测微信域名安全，有异常及时通知，非常稳定，准确率达99.9999%。需要可以联系VX:mkapi001，QQ:1401806571

#### 使用说明
###### 接口地址：[http://www.monkeyapi.com/](http://www.monkeyapi.com/)
###### 请求方式：http get/post
###### 返回格式：json
###### 请求示例：[http://api.monkeyapi.com?appkey=appkey&url=www.baidu.com](http://api.monkeyapi.com?appkey=appkey&url=www.baidu.com)
##### 1、在线使用 
将请求示例地址中的“http://www.baidu.com”换成你需要检测的域名（带不带http://都可以），这里可以是域名，也可以是链接，然后复制完整接口地址前往浏览器粘贴打开即可返回结果。这里需要一个appkey，需要的可以登陆猴子数据官网获取
#####   2、请求接口
如果觉得在线使用很麻烦，或者需要实时查询，那么需要将接口对接到服务器程序中，设置返回参数，即可实时检测并返回域名在微信内的状态。jeson返回示列如下：
##### JSON返回示例
域名正常
```
{"code":200,"msg":"域名正常","data":0}
```
非官方网址，请确认是否继续访问
```
{"code":200,"msg":"非官方网址，请确认是否继续访问","data":1}
```
域名已封杀
```
{"code":200,"msg":"域名已封杀","data":2}
```
提示如需浏览，请长按网址复制后使用浏览器打开
```
{"code":200,"msg":"提示如需浏览，请长按网址复制后使用浏览器打开","data":3}
```
网页存在诱导或误导下载/跳转的内容，请长按网址复制后使用浏览器访问
```
{"code":200,"msg":"网页存在诱导或误导下载/跳转的内容，请长按网址复制后使用浏览器访问","data":4}
```
##### PHP代码分享

```
$url = "http://api.monkeyapi.com";
 $params = array('appkey' =>'appkey',//您申请的APPKEY'url' =>'www.monkeyapi.com',//需要查询的网站);
 $paramstring = http_build_query($params);
 $content = Curl($url, $paramstring);
 $result = json_decode($content, true);if($result) {
     var_dump($result);
 }else {    //请求异常}/**
     * 请求接口返回内容
     * @param    string $url [请求的URL地址]
     * @param    string $params [请求的参数]
     * @param    int $ipost [是否采用POST形式]
     * @return    string
 */function Curl($url, $params = false, $ispost = 0){
     $httpInfo = array();
     $ch = curl_init();
     curl_setopt($ch, CURLOPT_HTTP_VERSION, CURL_HTTP_VERSION_1_1);
     curl_setopt($ch, CURLOPT_CONNECTTIMEOUT, 60);
     curl_setopt($ch, CURLOPT_TIMEOUT, 60);
     curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
     curl_setopt($ch, CURLOPT_FOLLOWLOCATION, true);    if ($ispost) {
         curl_setopt($ch, CURLOPT_POST, true);
         curl_setopt($ch, CURLOPT_POSTFIELDS, $params);
         curl_setopt($ch, CURLOPT_URL, $url);
     }else {        if ($params) {
             curl_setopt($ch, CURLOPT_URL, $url.'?'.$params);
         } else {
             curl_setopt($ch, CURLOPT_URL, $url);
         }
     }
     $response = curl_exec($ch);        if ($response === FALSE) {        //echo "cURL Error: " . curl_error($ch);
         return false;
     }
     $httpCode = curl_getinfo($ch, CURLINFO_HTTP_CODE);
     $httpInfo = array_merge($httpInfo, curl_getinfo($ch));
     curl_close($ch);    return $response;
 }
```

 





