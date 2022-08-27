#### Spotify非中文歌词翻译 Surge和Loon需要iOS15 

#### 采用百度翻译接口进行翻译,需要先免费申请百度翻译api的id和密钥,然后根据不同软件进行不同配置

##### -----------申请百度翻译(有标准版和高级版 建议申请高级版)api--------------

**标准版(很可能不够用):单次最长请求1000字符,免费调用量5万字符/月,QPS=1**
**高级版:单次最长请求6000字符,免费调用量100万字符/月,QPS=10**

​    **注册百度翻译个人开发者: http://api.fanyi.baidu.com/register**
​    **注册后如果需要认证可自行选择是否实人认证(高级版需要验证)**
​    **开通(通用翻译)API服务: https://fanyi-api.baidu.com/choose**
​    **成功后即可看到自己的appid和密钥(不要泄露给任何人): http://api.fanyi.baidu.com/manage/developer**

~~------------软件配置(在文本模式下,填入下方内容)--------------~~
~~如果软件已经加载过Spotify解锁脚本(https://github.com/app2smile/rules#spotify),可不配置MITM域名~~

##### 1.Surge:

[MITM]
hostname = %APPEND% spclient.wg.spotify.com
[Script]

修改下方argument中的appid和securityKey,填入自己的appid和密钥

spotify歌词翻译 = type=http-response,pattern=^https:\/\/spclient\.wg\.spotify\.com\/color-lyrics\/v2\/track\/,requires-body=1,binary-body-mode=1,max-size=0,script-path=https://raw.githubusercontent.com/app2smile/rules/master/js/spotify-lyric.js,argument=appid=111&securityKey=xxx

##### 2.Loon:

[Mitm]
hostname =spclient.wg.spotify.com
[Script]

修改下方argument中的appid和securityKey,填入自己的appid和密钥

http-response ^https:\/\/spclient\.wg\.spotify\.com\/color-lyrics\/v2\/track\/ script-path=https://raw.githubusercontent.com/app2smile/rules/master/js/spotify-lyric.js, requires-body=true, binary-body-mode=true, timeout=10, tag=Spotify歌词翻译, argument=appid=111&securityKey=xxx

##### 3.quantumultx:

   - 自行配置MITM域名: spclient.wg.spotify.com
   - 手动修改填入下方的appid和securityKey密钥, 并配置重写,类型为script-response-body,
     正则填入^https:\/\/spclient\.wg\.spotify\.com\/color-lyrics\/v2\/track\/

// 注意: QX用户需要手动填入appid和securityKey密钥, Surge和Loon用户无需填入!!!!

