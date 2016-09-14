


举个荔枝:
```
request({
    url: './test.json',
    method: 'get'
}, {
    standalone:"test2",
    hook:"ooo",
    cache: true
}).then(function(res) {
    console.log("success",res);
}).fail(function (err, msg) {
    console.log("fail",err,msg);
}).always(function (resp) {
    console.log("always do something");
});
```

url和method 为请求参数
```
{
    url: './test.json',
    method: 'get'
}
```

standalone,hook,cache为附加功能参数
```
{
    standalone:"test2",
    hook:"ooo",
    cache: true
}
```



then,fail,always分别是成功,失败,不论成败的 callback回调.
```
then(function(res) {
    console.log("success",res);
}).fail(function (err, msg) {
    console.log("fail",err,msg);
}).always(function (resp) {
    console.log("always do something");
})
```


这里只说比较重要的standalone,hook,cache三个参数的意思

- `standalone` string 或者 number标识, 两个standalone值相同的请求同时发出,后者请求失败
- `cache` cach为true时,相同的请求数据会被缓存
- `cache` cach为funtion(resp){...}时,返回值为true会被缓存
- `hook` string标识.

通过request.setHookFunction 设置hook function
如果有返回值,返回值为请求的返回数据
hook可以作为debug时塞入测试数据

举个荔枝:
```
request.setHookFunction("ooo",function(data){
    console.log("debug");
    return {msg:"hoooook"};
});
```


依赖于reqwest
所以支持一下请求参数

## Options

  * `url` a fully qualified uri
  * `method` http method (default: `GET`)
  * `headers` http headers (default: `{}`)
  * `data` entity body for `PATCH`, `POST` and `PUT` requests. Must be a query `String` or `JSON` object
  * `type` a string enum. `html`, `xml`, `json`, or `jsonp`. Default is inferred by resource extension. Eg: `.json` will set `type` to `json`. `.xml` to `xml` etc.
  * `contentType` sets the `Content-Type` of the request. Eg: `application/json`
  * `crossOrigin` for cross-origin requests for browsers that support this feature.
  * `success` A function called when the request successfully completes
  * `error` A function called when the request fails.
  * `complete` A function called whether the request is a success or failure. Always called when complete.
  * `jsonpCallback` Specify the callback function name for a `JSONP` request. This value will be used instead of the random (but recommended) name automatically generated by reqwest.

## Security

IE6/7需要引入JSON3 [JSON3](https://bestiejs.github.io/json3/)

``` html
<script>
(function () {
  if (!window.JSON) {
    document.write('<scr' + 'ipt src="http://cdnjs.cloudflare.com/ajax/libs/json3/3.3.2/json3.min.js"><\/scr' + 'ipt>')
  }
}());
</script>
```

## Browser support

- IE6+
- Chrome 1+
- Safari 3+
- Firefox 1+
- Opera
