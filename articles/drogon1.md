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

### インストール
MacOSを使用しているのであれば、すべてHomebrewでインストールが可能です。まだ、Homebrewをインストールしたことがないという人は[こちら](https://qiita.com/zaburo/items/29fe23c1ceb6056109fd)を参考にインストールしてみてください。

```shell
$ brew update
$ brew install git
$ brew install gcc
$ brew install cmake
$ brew install jsoncpp
$ brew install ossp-uuid
$ brew install openssl
$ brew install zlib
```
