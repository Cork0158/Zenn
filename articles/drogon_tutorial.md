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

## 1. Drogonとは
![](https://storage.googleapis.com/zenn-user-upload/11bf5cd4b3fc-20211223.jpg)
[公式HP](https://drogon.docsforge.com/)によると
> Drogonは、C++14/17ベースのHTTPアプリケーションフレームワークです。

と書かれています。
**Drogon**はC++を用いてさまざまなWebアプリケーションサーバープログラムを書けることが特徴であり、Linux・macOS・FreeBSD・OpenBSD・HaikuOS・Windowsなど幅広いOSに対応しているクロスプラットフォームのフレームワークです。

ちなみに、**Drogon**の由来はアメリカのテレビアニメ"Game of Thrones"に出てくるドラゴンの名前だそうです。
※ドラゴンの綴りは"Dragon"ですが、**Drogon**はこう言った由来からtypoではありません。

詳しくは**Drogon**の[Getting Started](https://drogon.docsforge.com/master/)を見てください。

## 2. 概要
**Drogon**をインストールして使ってみました。**Drogon**は2018年4月に発表された、比較的新しいフレームワークのため、日本語の文献がかなり少ないです。そのため、これから**Drogon**を使ってみようという人向けにこの記事を執筆しました。私はそこまで知識のある技術者ではないので、解釈が間違っている部分があるかと思います。訂正などはコメントで随時受け付けています。
また、Macで開発をおこなったためMacの使用を前提に記事を書いています。（Linux・Windowsの人ごめんなさい）


## 3. 開発環境
- macOS Monterey 12.0.1
- intel Core i5
- dorogon 1.7.4

## 4. 環境構築
### 4.1 必要ツール
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

### 4.2 インストール
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

## 5. サーバーを立ち上げる

### 5.1 プロジェクトを作成する

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

### 5.2 ローカルサーバーを立ち上げる
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

### 5.3 中身を表示させる
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

## 6. Controller入門
### 6.1 Controllerとは
先ほど「testctrl」というコントローラを作成して、URLにアクセスした時にレスポンスが返ってくるようにしましたが、そもそもControllerとはどのような役割を持っているのでしょうか。

[公式HP](https://drogon.docsforge.com/master/controller-introduction/)によると、
>コントローラはブラウザから送られたリクエストを処理し、ブラウザへのレスポンスを生成します

と書かれています。要するに**送られてきたHTTPリクエストによってどういった処理を行うかを決定する**重要な部分であるといえます。
先ほどは**Drogon**がサポートしているコントローラの中で、最もシンプルな`HttpSimpleController`を使用しました。今回はより実用的なコントローラである`HttpController`を使用したいと思います。

今回は[公式ドキュメント](https://drogon.docsforge.com/master/controller-introduction/controller-httpcontroller/)を参考に説明していくので、細かい部分で気になるところがあればこちらを参照してください。

### 6.2 HttpControllerの生成
`HttpSimpleController`を生成した時と同じように`drogon_ctl`コマンドを用いて生成します。
通常のコントローラ生成コマンドは`-h`オプションをつけた、以下のようなコマンドで生成します。

```shellsession
$ drogon_ctl create controller -h <[namespace::]class_name>
```
名前空間は省略可能ですが、名前空間の衝突を避けるために設定することをおすすめします。

また、**Drogon**では名前空間がそのままURLに反映されます。今回は[公式ドキュメント](https://drogon.docsforge.com/master/controller-introduction/controller-httpcontroller/)に従って以下のコマンドを叩いてコントローラを作成しました。

```shellsession
$ cd controllers
$ drogon_ctl create controller -h demo::v1::User
```
これで、今から編集するコントローラは`http://localhost/demo/v1/user/{ルーティングしたパス}`にアクセスしたときの処理を行います。

`controllers`のディレクトリを見てみると`demo_v1_User.cc`と`demo_v1_User.h`という2つのファイルが新たに出来ていると思います。

```cpp:demo_v1_User.cc
#include "demo_v1_User.h"
using namespace demo::v1;
// add definition of your processing function here
```

```cpp:demo_v1_User.h
#pragma once
#include <drogon/HttpController.h>
using namespace drogon;
namespace demo {
namespace v1 {
class User : public drogon::HttpController<User> {
   public:
    METHOD_LIST_BEGIN
    // use METHOD_ADD to add your custom processing function here;
    // METHOD_ADD(User::get,"/{2}/{1}",Get);//path is
    // /demo/v1/User/{arg2}/{arg1}
    // METHOD_ADD(User::your_method_name,"/{1}/{2}/list",Get);//path is
    // /demo/v1/User/{arg1}/{arg2}/list
    // ADD_METHOD_TO(User::your_method_name,"/absolute/path/{1}/{2}/list",Get);//path
    // is /absolute/path/{arg1}/{arg2}/list

    METHOD_LIST_END
    // your declaration of processing function maybe like this:
    // void get(const HttpRequestPtr& req,std::function<void (const
    // HttpResponsePtr &)> &&callback,int p1,std::string p2); void
    // your_method_name(const HttpRequestPtr& req,std::function<void (const
    // HttpResponsePtr &)> &&callback,double p1,int p2) const;
};
}  // namespace v1
}  // namespace demo
```

### 6.3 ファイルの編集
公式ドキュメントでは`「/info/{userId}」`でユーザ ID と名前を JSON で返すという処理を行うプログラムを書いているので、実装してみようと思います。
（公式ドキュメントでは`login`も行っていますが、説明を簡略化するために省いています）

まず、ヘッダファイルを編集します。

```diff cpp:demo_v1_User.h
    #pragma once
    #include <drogon/HttpController.h>
    using namespace drogon;
    namespace demo {
    namespace v1 {
    class User : public drogon::HttpController<User> {
    public:
        METHOD_LIST_BEGIN
        // use METHOD_ADD to add your custom processing function here;
        // METHOD_ADD(User::get,"/{2}/{1}",Get);//path is
        // /demo/v1/User/{arg2}/{arg1}
        // METHOD_ADD(User::your_method_name,"/{1}/{2}/list",Get);//path is
        // /demo/v1/User/{arg1}/{arg2}/list
        // ADD_METHOD_TO(User::your_method_name,"/absolute/path/{1}/{2}/list",Get);//path
        // is /absolute/path/{arg1}/{arg2}/list

+       METHOD_ADD(User::getInfo, "/info/{1}", Get);

        METHOD_LIST_END
        // your declaration of processing function maybe like this:
        // void get(const HttpRequestPtr& req,std::function<void (const
        // HttpResponsePtr &)> &&callback,int p1,std::string p2); void
        // your_method_name(const HttpRequestPtr& req,std::function<void (const
        // HttpResponsePtr &)> &&callback,double p1,int p2) const;

+       void getInfo(const HttpRequestPtr &req,
+                  std::function<void(const HttpResponsePtr &)> &&callback,
+                  std::string userId) const;
    };
    }  // namespace v1
    }  // namespace demo
```

これでGETでアクセスされた場合、`User::getInfo()`に処理を投げるようになります。
次にソースファイルを編集していきます。

```diff cpp:demo_v1_User.cc
    #include "demo_v1_User.h"
    using namespace demo::v1;
    // add definition of your processing function here

+  void User::getInfo(
+       const HttpRequestPtr &req,
+       std::function<void(const HttpResponsePtr &)> &&callback,
+       std::string userId
+   ) const {
+       // LOG_DEBUGでコンソール上に、ログが表示される
+       LOG_DEBUG << "User " << userId << " get his information";
+
+       // ここでトークンを参照したり、データを取得する処理が入ったりする
+
+       Json::Value ret;
+
+       // JSONにデータを格納
+       ret["result"] = "ok";
+       ret["user_name"] = "Jack";
+       ret["user_id"] = userId;
+       ret["gender"] = 1;
+
+       auto resp = HttpResponse::newHttpJsonResponse(ret);
+       callback(resp);
+   }
```

これで編集は完了です。実際に動作確認をして見ましょう。

### 6.4 動作確認
以下のコマンドを叩いてビルドしてください。
```shellsession
$ cd ..
$ cd build
$ cmake ..
$ make
$ ./sample
```
[http://localhost/demo/v1/user/info/123](http://localhost/demo/v1/user/info/123)にアクセスすると以下のようになると思います。

![](https://storage.googleapis.com/zenn-user-upload/080fe9b34117-20211222.png)*/demo/v1/user/info/123*

このように、JSON形式のデータとして`{"gender":1,"result":"ok","user_id":"123","user_name":"Jack"}`が返ってきます。
また、シェルにはログとして
```
20211222 06:55:26.984065 UTC 2622569 DEBUG [getInfo] User 123 get his information - demo_v1_User.cc:11
```
が出力されていると思います。（時間は読者のみなさんに依存します。）

### 6.5 URLパラメータのさまざまな記法

UserIDをURLで表現する時によく使われる`/info?userId={xxx}`のようなURLも`demo_v1_User.h`に以下の処理を追加することで`/info/{xxx}`と同様に処理できます。

```cpp
METHOD_ADD(User::getInfo,"/info?userId={1}",Get);
```

ここで公式ドキュメントに書いてあるURLパラメータの記法を紹介します。

1. `{}` : 通常のパラメータマッピング
2. `{1}, {2}`  : 数字が含まれたパラメータ
3. `{anything}` : `{}` と同じで可読性向上のために何かしら文字列を入れることができる
4. `{1:anything}, {2:xxx}` : `{1}, {2}` と同じで可読性向上のためのもの

公式ドキュメントでは3番目の記法が推奨されています。

これを踏まえると以下の4つはすべて同じルーティングが行われます。

- "/users/{}/books/{}"
- "/users/{}/books/{2}"
- "/users/{user_id}/books/{book_id}"
- "/users/{1:user_id}/books/{2}"

これをみてわかるように、3番目がかなり可読性が高いことがわかります。開発者目線でも3番目を使用したほうがいいでしょう。

### 6.6 multiple path mapping
以下のルーティングを行えば、複数のURLリクエストを1つのコントローラで処理できます。
```cpp
ADD_METHOD_TO(UserController::handler1,"/users/.*",Post);
ADD_METHOD_TO(UserController::handler2,"/{name}/[0-9]+",Post); 
```
まず、上のルーティングでは`/users/`が先頭にあるすべてのURLの処理を行い、下のルーティングでは`/{文字列}/{数字}`で表現されるすべてのURLの処理を行います。

ただ、これだけでなくもっと複雑な設定を行いたい場面も出てくると思います。そんな時は正規表現を用いて記述することができます。

### 6.7 Regular expression（正規表現）
公式ドキュメントには以下のような例が載っています。
```cpp
ADD_METHOD_VIA_REGEX(UserController::handler1,"/users/(.*)",Post);
ADD_METHOD_VIA_REGEX(UserController::handler2,"/.*([0-9]*)",Post);
ADD_METHOD_VIA_REGEX(UserController::handler3,"/(?!data).*",Post);
```
1番目のルーティングでは、`/users/`を先頭とするすべてのURLの処理を行い、2番目のルーティングでは末尾が数字となるすべてのURLの処理を行い、3番目のルーティングでは`/data`で始まらないすべてのURLの処理を行います。
これをうまく使えば任意のURLに対してもれなく処理を行うことができます。だたし、競合しないように注意しましょう。

正規表現については解説している本やサイトが無数にあるので自分にあった文献を参考に調べて見てください。

## 7. View入門

### 7.1 Viewとは
[公式ドキュメント](https://drogon.docsforge.com/master/view/)によると、
> バックエンドのレンダリング技術を提供し、サーバープログラムがHTMLページを動的に生成できるようにする部分

と書かれています。要するに**見た目(View)の部分を動的に生成することのできる**のです。
**Drogon**はJSPと同じようにプログラムコードにHTMLを埋め込むことで直感的にコーディングすることができます。

今回も[公式ドキュメント](https://drogon.docsforge.com/master/view/)に沿って話していくのでわからないことがあればこちらを参考にしてください。

### 7.2 Viewのコントローラの生成
今回は受け取ったGETパラメータを展開するようにしたいと思います。
まずは、コントローラが必要不可欠なので「ListParameters」という名前のコントローラを作成します。
以下のコマンドを叩いてください。

```shellsession
$ cd controllers
$ drogon_ctl create controller ListParameters
```

まずは、ヘッダファイルを編集します。
「/list_para」というURLをルーティングします。

```diff cpp:ListParameters.h
    #pragma once
    #include <drogon/HttpSimpleController.h>
    using namespace drogon;
    class ListParameters : public drogon::HttpSimpleController<ListParameters> {
    public:
        virtual void asyncHandleHttpRequest(
            const HttpRequestPtr &req,
            std::function<void(const HttpResponsePtr &)> &&callback) override;
        PATH_LIST_BEGIN
        // list path definitions here;
        // PATH_ADD("/path","filter1","filter2",HttpMethod1,HttpMethod2...);
+       PATH_ADD("/list_para", Get);

        PATH_LIST_END
    };
```
次にソースファイルを実装します。
ここではCSP（後述）にどのようなデータをどのように渡すかを記述しています。

```diff cpp:ListParameters.cc
    #include "ListParameters.h"
    void ListParameters::asyncHandleHttpRequest(
        const HttpRequestPtr &req,
        std::function<void(const HttpResponsePtr &)> &&callback) {
        // write your application logic here
        
+       // CSPに渡すデータを格納
+       auto para = req->getParameters();
+       HttpViewData data;
+       data.insert("title", "list parameters");
+       data.insert("parameters", para);
+
+       // ListParaCsp.cspにデータを渡す
+       auto res =
+           drogon::HttpResponse::newHttpViewResponse("ListParaCsp.csp", data);
+       callback(res);
    }
```
※`ListParameters.cc`は参考記事とは少し異なります。

### 7.3 CSPとは
CSPとは、「C++ Server Pages」の略で、**サーバサイドでC++ライクな構文を処理し、HTMLを生成するもの**です。
JavaにおけるJSPのC++版と考えるとわかりやすいと思います。

CSPは**HTML内のあるスコープにおいてはC++を記述できる**ことが特徴です。
以下にCSPに記法を紹介したいと思います。

#### I. `<%inc %>`
`<%inc %>`内では、 `#include`することが可能です。
例：`<%inc#include "xx.h" %>`

#### II. `<%c++ %>`
`<%c++ %>`内では、**`#include`を除くC++のコード**が記述可能です。
例：`<c++ std:string name="drogon"; %>`

#### Ⅲ. `@@`
`@@`は**コントローラから渡されるデータ変数**を表します。
先ほどの`ListParameters.cc`の`date`がそれにあたります。
逆に、CSPから`data`という名前では呼び出せません。

#### Ⅳ. `$$`
`$$`は`<<`と組み合わせることでページに出力することができます。
C++でいう`std::cout`みたいなものです。

#### Ⅴ. `[[ ]]`
`[[ ]]`内の文字列をキーとして、**コントローラから渡されたデータから対応するものを見つけ出し、表示させます。**
ただし、対応している文字列データ型は`const char *`、`std::string`、`const std::string`の3つであることに注意してください。また、同じ行の中で囲まなければいけません。

#### Ⅵ. `{% %}`
`{% %}`内では、あらかじめ`<%c++ %>`などで宣言された変数を表示できます。
すなわち、`{%val.xx%}`と`<%c++ $$<<val.xx; %>`は同義です。
ただし、同じ行の中で囲まなければいけません。

#### Ⅶ. `<%view %>`
`<%view %>`内では**サブビューとして、他のCSPファイルを展開できます。**
`header.csp`が存在すれば、`<%view header %>`と記述することでその場に`header.csp`を展開することができます。
これにより、各ページの共通部分を1つのページにまとめることが可能です。

### 7.4 CSPの生成
では、実際にCSPを実装してみましょう。
「ListParaCsp.csp」という名前のCSPファイルを生成して編集します。

```shellsession
$ cd views
$ touch ListParaCsp.csp
```

```html:ListParaCsp.csp
<!DOCTYPE html>
<html>
<%c++
// dataからunorder_mapとしてパラメータを取得
auto para = @@.get<std::unordered_map<std::string, std::string>>("parameters");

// 適当に変数宣言する
auto name = "Drogon Inc.";
auto date = "2021.12.25";
%>
<head>
    <meta charset="UTF-8">
    <title>[[ title ]]</title>
</head>
<body>

<!-- 変数展開はどちらでも良い -->
<p>Hello, {% name %}</p>
<p>Date: <%c++ $$ << date; %></p>

<%c++ if(para.size()>0){%>
<H1>Parameters</H1>
<table border="1">
    <tr>
        <th>name</th>
        <th>value</th>
    </tr>
    <!-- イテレーションループでパラメータを展開 -->
    <%c++ for(auto iter:para){ %>
    <tr>
        <td>{% iter.first %}</td> 
        <td><%c++ $$<<iter.second;%></td>
    </tr>
    <%c++ } // endfor%>
</table>
<%c++ }else{ %>
<H1>no parameter</H1>
<%c++ } // endif %>
</body>
</html>
```

コーディングが終わったらビルドして実行してみましょう。
```shellsession
$ cd ..
$ cd build
$ cmake ..
$ make
$ ./sample
```

動作確認のために、[http://localhost/list_para?p1=a&p2=b&p3=c](http://localhost/list_para?p1=a&p2=b&p3=c)にアクセスしてみると、以下のような画面が表示されると思います。（日付がクリスマスになっているのは執筆時の日付がクリスマスだったからです。これ以上はなにも聞かないでください。）

![](https://storage.googleapis.com/zenn-user-upload/8bf8d3646f20-20211224.png =300x)

また、以下のコマンドを叩くことでC++ソースファイルを生成するコントローラ（`ListParaCsp.h`と`ListParaCsp.cc`）を、view ディレクトリ下に自動生成してくれる機能もあります。

```shellsession
$ drogon_ctl create view ListParaCsp.csp
```

#### 余談
CSPファイルを`ListParameters.csp`とせず、`ListParaCsp.csp`にしていますが前者のファイル名ではビルドが失敗したため、後者のファイル名に変更しました。（リンカのエラーが出てたのですが調べても解決策がわからなかったので、渋々名前を変更しました。この変更は現段階では問題ないですが、あまり良くない変更だと思います。）

## 8. 最後に
みなさん、やって見ていかがでしたでしょうか。C++に慣れていない人にとっては少し難しかったかもしれませんが、使って見てもいいのではないでしょうか。
また、僕自身も調べながら執筆しているので言葉が間違っていたり、理解が間違ったりしている部分もあるかと思います。その点については随時指摘していただけるとありがたいです。

また、この記事の執筆にあたり下記の記事には大変おせわになりました。この場をお借りして感謝申し上げます。ただ、この記事のコードを参考にはしているものの変更している部分の多々あるので、両方を参考にしながら作業することはおすすめしません。
https://rightcode.co.jp/blog/information-technology/fastest-c-web-framework-drogon-quick-start
https://rightcode.co.jp/blog/information-technology/fastest-c-web-framework-drogon-controller
https://rightcode.co.jp/blog/information-technology/fastest-c-web-framework-drogon-view
