--- 
title: "ksnctf basic is secure? write-up" 
emoji: "📝" 
type: "tech" 
topics: ["ctf", "Wireshark"] 
published: true 
--- 

みなさん、こんにちは。
cork（コルク）です。
セキュリティの勉強としてctfをやっていますが、記録のためにwrite-upを書いていこうと思います。

# Basic is secure? (50 points)

## 概要
有名な常設CTFである[ksnctf](https://ksnctf.sweetduet.info/)の[第8問](https://ksnctf.sweetduet.info/problem/8)の解説です。
PCAPファイルを解析する問題です。

## 問題
以下のPCAPファイルが与えられます。
[q8.pcap](https://ksnctf.sweetduet.info/q/8/q8.pcap)

## 解説
とりあえず、PCAPファイルなのでみんな大好き[Wireshark](https://www.wireshark.org/)で解析します。

![](https://storage.googleapis.com/zenn-user-upload/b5493b6a2fd7-20211213.png)*Wireshark*

いろんなパケットが飛び交ってますが、HTTPプロトコルのパケットを見てみると、9行目に`Authorization Required`という文字が見えます。
9行目のパケットの中身を見てみると、どうやら7行目のGETでサーバーにリクエストを送ったものの認証に失敗して、それに対するサーバーの応答のようです。
（参考までに9行目のパケットのtextdataを貼りつけておきます）

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

ここで、**認証情報がFLAGではないか**と推測できます。
そこで、認証が成功している通信がどこかにあるはずなので探してみると、16行目で認証が成功していることがわかりました。
13行目のGETでのリクエストに対して16行目で認証成功のレスポンスをしているので、13行目に認証情報が含まれていると考え、パケットのHTTPプロトコルの中身を見てみます。

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
上記の6行目を見てみるみるとFLAGがありました。
Wiresharkの機能で自動的にデコードされていますが、元々はbase64で暗号化されたものです。

```
FLAG_5ux7zK2NKSH8fSGA
```

## 補足
思ったよりも簡単に見つかったので、認証に使われている[Basic認証](https://ja.wikipedia.org/wiki/Basic%E8%AA%8D%E8%A8%BC)について自分なりに勉強しました。ここにメモとして残します。

### Basic認証とは
>[Apache](https://ja.wikipedia.org/wiki/Apache_HTTP_Server)と呼ばれるOSSのWebサーバーソフトウェアのユーザ認証に使われてる認証の一つで、パスワードが平文で送られる（正確にはBase64でエンコードされる）ため、安全性の低い認証である。

HTTPSプロトコルを用いれば第三者に見られる危険性は低くなるが、今回の問題のようにHTTPプロトコルを使用しての通信は全く暗号化されないため、第三者に見られる可能性が極めて高い。そのため、もう一つの認証技術である[Digest認証](https://ja.wikipedia.org/wiki/Digest%E8%AA%8D%E8%A8%BC)を使用するとよいらしい[^1]（平文をそのまま送らないという点でBasic認証よりもすぐれていますが、安全性が低いことに変わりはないです）。

[^1]: [Basic認証とDigest認証](https://qiita.com/hyuy/items/3a7ee467cd7ce2748e48)