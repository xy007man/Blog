# XX上网
```
XX上网的方案有很多,我选用的是目前相对比较稳定不易被墙的v2ray方案,目前已经用将近半年了,仍然可以稳定使用,搭建教程和安装脚本
```
[v2ray搭建教程](https://github.com/xiaoming2028/FreePAC)
[v2ray安装脚本](https://github.com/233boy/v2ray)  
```
我使用的服务器是vultr的,但是访问youtobe的网速感人,通过优选IP和反向代理方式可以提升网速,即使在晚高峰也可以看4K youtobe视频
```
## 优选IP
```
我选取的CDN厂商是cloudflare,优选IP的主要用途是找到在你的网络状况下优质的cloudflare 
IP, 通过这些IP访问一些使用cloudflare cdn的网站, 起到加速的作用.
```
[优选IP可以参考这个github工程](https://github.com/badafans/better-cloudflare-ip)

## 反向代理
```
在cloudflare中添加自定义的worker,代码如下:其中hostname是v2ray服务器的伪装网址
```
```javascript
addEventListener('fetch',event => {
  let url=new URL(event.request.url);
  url.hostname='xxxx.xx';
  let request=new Request(url,event.request);
  event.respondWith(
    fetch(request)
  )
})
```