> 提醒： 滥用可能导致账户被BAN！！！ 

### 部署Kintohub空间

点开 https://app.kintohub.com/ 新建一个APP，点击 Create Service ,然后创建 Web App；Improt URL填上本项目链接 ( https://github.com/moosetk/yingsuo ) ；Build Settings 项随便修改 Service Name；
也可以在 Environment Variables 标签修改以下变量(密码-加密方式-路径)：
```
ONE=ENO
TWO=rc4-md5
THREE=/sspath
```
最后点击 Deploy 部署。部署成功会生成一个域名，记下域名，后面客户端会用到。

### 客户端配置

首先下载 v2ray-plugin 插件到电脑，下载解压后移动到常用文件夹，记住插件所在文件夹路径，待会会用到。

v2ray-plugin 插件下载页：https://github.com/shadowsocks/v2ray-plugin/releases

然后，下载ss客户端，比如[Windows客户端](https://github.com/shadowsocks/shadowsocks-windows/releases/)，这个不多讲。配置如下：

* 服务器地址: xxx.xxx.kinto.io  //此处填写服务端生成的域名
* 端口: 443
* 密码：ENO
* 加密：rc4-md5
* 插件程序：D:\APP\v2ray-plugin_windows_amd64.exe  //此处要填插件在电脑上的绝对路径
* 插件选项: path=/sspath;host=xxx.xxx.kinto.io;tls //此处填上域名和路径

### Workers反代

```
addEventListener(
    "fetch",event => {
        let url=new URL(event.request.url);
        url.hostname="xxx.xxx.kinto.io";
        let request=new Request(url,event.request);
        event. respondWith(
            fetch(request)
        )
    }
)
```



这次kintohub上ss和v2ray起死回生要特别感谢 Alice（ https://twitter.com/alicesu55 ）的condom项目（ https://github.com/alicesu55/condom ）。
