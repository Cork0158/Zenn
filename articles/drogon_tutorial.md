--- 
title: "「Drogon」入門" 
emoji: "📝" 
type: "tech" 
topics: ["Drogon", "Web", "framework"] 
published: false 
--- 

みなさん、こんにちは。
cork（コルク）です。
今日はWeb フレームワーク**Drogon**を使う機会があったので、チュートリアルとして自分がどのようなことを行ったかを書き残したいと思います。

# 「Drogon」入門

## Drogonとは
[公式HP](https://drogon.docsforge.com/)によると
> Drogonは、C++14/17ベースのHTTPアプリケーションフレームワークです。

と書かれています。
**Drogon**はC++を用いてさまざまなWebアプリケーションサーバープログラムを書けることが特徴であり、Linux・macOS・FreeBSD・OpenBSD・HaikuOS・Windowsなど幅広いOSに対応しているクロスプラットフォームのフレームワークです。

ちなみに、**Drogon**の由来はアメリカのテレビアニメ"Game of Thrones"に出てくるドラゴンの名前だそうです。
※ドラゴンの綴りは"Dragon"ですが、**Drogon**はこう言った由来からtypoではありません。

詳しくは**Drogon**の[Getting Started](https://drogon.docsforge.com/master/)を見てください。

## 概要
**Drogon**をインストールして使ってみました。**Drogon**は2018年4月に発表された、比較的新しいフレームワークのため、日本語の文献がかなり少ないです。そのため、これから**Drogon**を使ってみようという人向けにこの記事を執筆しました。私はそこまで知識のある技術者ではないので、解釈が間違っている部分があるかと思います。訂正などはコメントで随時受け付けています。
また、Macで開発をおこなったためMacの使用を前提に記事を書いています。（Linux・Windowsの人ごめんなさい）


## 開発環境
- macOS Monterey 12.0.1
- intel Core i5
- dorogon 1.7.4

## 環境構築
### 必要ツール
MacOSを使用する場合は以下の環境が必要です。
- git
- gcc/g++
- cmake
- jsoncpp
- uuid
- OpenSSL
- zlib

MacOSを使用しているのであれば、すべてHomebrewでインストールが可能です。まだ、Homebrewをインストールしたことがないという人は[こちら](https://qiita.com/zaburo/items/29fe23c1ceb6056109fd)を参考にインストールしてみてください。

```shellsession
$ brew update
$ brew install git
$ brew install gcc
$ brew install cmake
$ brew install jsoncpp
$ brew install ossp-uuid
$ brew install openssl
$ brew install zlib
```

### インストール
ワークスペースを作って、Githubからソースをクローンし、ビルドします。
この記事ではワークスペースの名前を「drogon-test」をします。

```shellsession
$ mkdir drogon-test
$ cd drogon-test
$ git clone https://github.com/an-tao/drogon
$ cd drogon
$ git submodule update --init
$ mkdir build
$ cd build
$ cmake ..
$ make && sudo make install
```
上記のコマンドを叩くとインストール完了です。
正常にインストールが出来ていたら`$ drogon-ctl -v`とコマンドを叩くと以下の写真のような表示がされると思います。

![](https://storage.googleapis.com/zenn-user-upload/14aa1271b5b1-20211221.png)*dorogonのバージョンとロゴ*

これで環境構築は終了です。
次からは実際にdrogonを使っていきます。

## サーバーを立ち上げる

### プロジェクトを作成する

まず、`drogon-test`のディレクトリまで戻ります。
以下のコマンドを打つことで、プロジェクトが作成できます。
```shellsession
$ drogon_ctl create project [YOUR_PROJECT_NAME]
$ cd [YOUR_PROJECT_NAME]
```
この記事ではプロジェクト名を「sample」とします。
プロジェクトを作成するとだいたい以下のようなディレクトリ構成でファイルが生成されると思います。

```markdown
.sample
├── build               # ビルド用ディレクトリ
├── CMakeLists.txt      # cmake用 (Makefile生成用)
├── config.json         # Drogonアプリの設定ファイル
├── controllers         # コントローラ管理用
├── filters             # フィルタ管理用
├── main.cc             # アプリ メインファイル
├── models              # モデル管理用
│   └── model.json
└── views               # ビュー管理用
```

`main.cc`はこんな感じになっていると思います。

```cpp:main.cc
#include <drogon/drogon.h>
int main() {
    //Set HTTP listener address and port
    drogon::app().addListener("0.0.0.0",80);
    //Load config file
    //drogon::app().loadConfigFile("../config.json");
    //Run HTTP framework,the method will block in the internal event loop
    drogon::app().run();
    return 0;
}
```

ここでは`drogon`という名前空間が使われていますが、`using namespace drogon`で省略可能です。名前空間についてわからない方は調べてみてください。

### ローカルサーバーを立ち上げる
以下のコマンドを叩いてローカルサーバーを立ち上げてみましょう。
```shellsession
$ cd build      # ビルド用ディレクトリへ移動
$ cmake ..      # Makefile生成
$ make          # ビルドとコンパイル
$ ./sample      # 実行
```

[http://localhost](http://localhost)にアクセスすると、以下のように表示されます。

![](https://storage.googleapis.com/zenn-user-upload/afee4b04f6cc-20211222.png)

htmlファイルを何も作ってないので`404 Not Found`と表示され、フッターには**Drogon**のバージョンが表示されます。

### 中身を表示させる
コントローラを一つ作成し、URLにアクセスしたときになにかが返ってくるようにします。
以下のコマンドを叩き、「testctrl」という名前のコントローラを作成します。

```shellsession
$ cd ..
$ cd controllers
$ drogon_ctl create controller testctrl
```
これで、`testctrl.h`と`testctrl.cc`が作成されたと思います。

**Drogon**では、**ヘッダファイルにルーティングし、ソースファイルに処理を書く**ため両方のファイルを修正していきます。
URLにアクセスされたときにルーティングされるようにヘッダファイルに`「/」`と`「/test」`という2つのパスを追加します。

```diff cpp: testctrl.h
    #pragma once //インクルードカード
    #include <drogon/HttpSimpleController.h>
    using namespace drogon;
    class testctrl:public drogon::HttpSimpleController<testctrl>
    {
    public:
        virtual void asyncHandleHttpRequest(const HttpRequestPtr& req, std::function<void (const HttpResponsePtr &)> &&callback) override;
        PATH_LIST_BEGIN
        //list path definitions here;
        //PATH_ADD("/path","filter1","filter2",HttpMethod1,HttpMethod2...);

+       PATH_ADD("/", Get, Post);
+       PATH_ADD("/test", Get);

        PATH_LIST_END
    };
```

続いて、`testctrl.cc`も修正していきます。

```diff cpp:testctrl.cc
    #include "testctrl.h"
    void testctrl::asyncHandleHttpRequest(const HttpRequestPtr& req, std::function<void (const HttpResponsePtr &)> &&callback)
    {
        //write your application logic here
+       auto resp = HttpResponse::newHttpResponse();  // 新しいレスポンスインスタンスを生成
+       resp->setStatusCode(k200OK);  // HTTPステータスコード 200に設定
+       resp->setContentTypeCode(CT_TEXT_HTML);  // Header: Content typeをHTMLにする
+       resp->setBody("<h1>Hello World!</h1>");  // Body:
+       callback(resp);
    }
```

では、以下のコマンドを叩いて実行してみましょう。

```shellsession
$ cd ..
$ cd build
$ cmake ..
$ make
$ ./sample
```
[http://localhost](http://localhost)と[http://localhost/test](http://localhost/test)のどちらにアクセスしても"Hello World!"と表示されていると思います。

このようにたった数行コードを変更するだけで、コントローラの設定が完了します。



