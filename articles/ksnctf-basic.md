--- 
title: "ksnctf basic is secure? write-up" 
emoji: "ð" 
type: "tech" 
topics: ["ctf", "Wireshark"] 
published: true 
--- 

ã¿ãªãããããã«ã¡ã¯ã
corkï¼ã³ã«ã¯ï¼ã§ãã
ã»ã­ã¥ãªãã£ã®åå¼·ã¨ãã¦ctfããã£ã¦ãã¾ãããè¨é²ã®ããã«write-upãæ¸ãã¦ãããã¨æãã¾ãã

# Basic is secure? (50 points)

## æ¦è¦
æåãªå¸¸è¨­CTFã§ãã[ksnctf](https://ksnctf.sweetduet.info/)ã®[ç¬¬8å](https://ksnctf.sweetduet.info/problem/8)ã®è§£èª¬ã§ãã
PCAPãã¡ã¤ã«ãè§£æããåé¡ã§ãã

## åé¡
ä»¥ä¸ã®PCAPãã¡ã¤ã«ãä¸ãããã¾ãã
[q8.pcap](https://ksnctf.sweetduet.info/q/8/q8.pcap)

## è§£èª¬
ã¨ãããããPCAPãã¡ã¤ã«ãªã®ã§ã¿ããªå¤§å¥½ã[Wireshark](https://www.wireshark.org/)ã§è§£æãã¾ãã

![](https://storage.googleapis.com/zenn-user-upload/b5493b6a2fd7-20211213.png)*Wireshark*

ããããªãã±ãããé£ã³äº¤ã£ã¦ã¾ãããHTTPãã­ãã³ã«ã®ãã±ãããè¦ã¦ã¿ãã¨ã9è¡ç®ã«`Authorization Required`ã¨ããæå­ãè¦ãã¾ãã
9è¡ç®ã®ãã±ããã®ä¸­èº«ãè¦ã¦ã¿ãã¨ãã©ããã7è¡ç®ã®GETã§ãµã¼ãã¼ã«ãªã¯ã¨ã¹ããéã£ããã®ã®èªè¨¼ã«å¤±æãã¦ãããã«å¯¾ãããµã¼ãã¼ã®å¿ç­ã®ããã§ãã
ï¼åèã¾ã§ã«9è¡ç®ã®ãã±ããã®textdataãè²¼ãã¤ãã¦ããã¾ãï¼

```html
    <!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN">\n
    <html>
        <head>\n
            <title>401 Authorization Required</title>\n
        </head>
        
        <body>\n
            <h1>Authorization Required</h1>\n
            <p>This server could not verify that you\n
            are authorized to access the document\n
            requested.  Either you supplied the wrong\n
            credentials (e.g., bad password), or your\n
            browser doesn't understand how to supply\n
            the credentials required.</p>\n
            <hr>\n
            <address>Apache/2.2.15 (CentOS) Server at ctfq.sweetduet.info Port 10080</address>\n
        </body>
    </html>\n
```

ããã§ã**èªè¨¼æå ±ãFLAGã§ã¯ãªãã**ã¨æ¨æ¸¬ã§ãã¾ãã
ããã§ãèªè¨¼ãæåãã¦ããéä¿¡ãã©ããã«ããã¯ããªã®ã§æ¢ãã¦ã¿ãã¨ã16è¡ç®ã§èªè¨¼ãæåãã¦ãããã¨ããããã¾ããã
13è¡ç®ã®GETã§ã®ãªã¯ã¨ã¹ãã«å¯¾ãã¦16è¡ç®ã§èªè¨¼æåã®ã¬ã¹ãã³ã¹ããã¦ããã®ã§ã13è¡ç®ã«èªè¨¼æå ±ãå«ã¾ãã¦ããã¨èãããã±ããã®HTTPãã­ãã³ã«ã®ä¸­èº«ãè¦ã¦ã¿ã¾ãã

```
Hypertext Transfer Protocol
    GET /~q8/ HTTP/1.1\r\n
    Host: ctfq.sweetduet.info:10080\r\n
    Connection: keep-alive\r\n
    Authorization: Basic cTg6RkxBR181dXg3eksyTktTSDhmU0dB\r\n
        Credentials: q8:FLAG_5ux7zK2NKSH8fSGA
    User-Agent: Mozilla/5.0 (Windows NT 5.1) AppleWebKit/535.19 (KHTML, like Gecko) Chrome/18.0.1025.162 Safari/535.19\r\n
    Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8\r\n
    Accept-Encoding: gzip,deflate,sdch\r\n
    Accept-Language: ja,en-US;q=0.8,en;q=0.6\r\n
    Accept-Charset: Shift_JIS,utf-8;q=0.7,*;q=0.3\r\n
    \r\n
    [Full request URI: http://ctfq.sweetduet.info:10080/~q8/]
    [HTTP request 1/1]
    [Response in frame: 16]
```
ä¸è¨ã®6è¡ç®ãè¦ã¦ã¿ãã¿ãã¨FLAGãããã¾ããã
Wiresharkã®æ©è½ã§èªåçã«ãã³ã¼ãããã¦ãã¾ãããåãã¯base64ã§æå·åããããã®ã§ãã

```
FLAG_5ux7zK2NKSH8fSGA
```

## è£è¶³
æã£ããããç°¡åã«è¦ã¤ãã£ãã®ã§ãèªè¨¼ã«ä½¿ããã¦ãã[Basicèªè¨¼](https://ja.wikipedia.org/wiki/Basic%E8%AA%8D%E8%A8%BC)ã«ã¤ãã¦èªåãªãã«åå¼·ãã¾ãããããã«ã¡ã¢ã¨ãã¦æ®ãã¾ãã

### Basicèªè¨¼ã¨ã¯
>[Apache](https://ja.wikipedia.org/wiki/Apache_HTTP_Server)ã¨å¼ã°ããOSSã®Webãµã¼ãã¼ã½ããã¦ã§ã¢ã®ã¦ã¼ã¶èªè¨¼ã«ä½¿ããã¦ãèªè¨¼ã®ä¸ã¤ã§ããã¹ã¯ã¼ããå¹³æã§éãããï¼æ­£ç¢ºã«ã¯Base64ã§ã¨ã³ã³ã¼ããããï¼ãããå®å¨æ§ã®ä½ãèªè¨¼ã§ããã

HTTPSãã­ãã³ã«ãç¨ããã°ç¬¬ä¸èã«è¦ãããå±éºæ§ã¯ä½ããªãããä»åã®åé¡ã®ããã«HTTPãã­ãã³ã«ãä½¿ç¨ãã¦ã®éä¿¡ã¯å¨ãæå·åãããªããããç¬¬ä¸èã«è¦ãããå¯è½æ§ãæ¥µãã¦é«ãããã®ãããããä¸ã¤ã®èªè¨¼æè¡ã§ãã[Digestèªè¨¼](https://ja.wikipedia.org/wiki/Digest%E8%AA%8D%E8%A8%BC)ãä½¿ç¨ããã¨ããããã[^1]ï¼å¹³æããã®ã¾ã¾éããªãã¨ããç¹ã§Basicèªè¨¼ããããããã¦ãã¾ãããå®å¨æ§ãä½ããã¨ã«å¤ããã¯ãªãã§ãï¼ã

[^1]: [Basicèªè¨¼ã¨Digestèªè¨¼](https://qiita.com/hyuy/items/3a7ee467cd7ce2748e48)