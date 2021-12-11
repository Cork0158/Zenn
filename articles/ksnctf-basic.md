--- 
title: "ksnctf basic is secure? write-up" 
emoji: "📝" 
type: "tech" 
topics: ["ctf", "Wireshark"] 
published: false 
--- 

みなさん、こんにちは。
cork（コルク）です。
セキュリティの勉強としてctfをやっていますが、記録のためにwrite-upを書いていこうと思います。

# Basic is secure? (50 points)

## 概要
有名な常設CTFである[ksnctf](https://ksnctf.sweetduet.info/)の[第8問](https://ksnctf.sweetduet.info/problem/8)の解説です。
ネタバレするとPCAPファイルを解析する問題です。

## 問題
以下のPCAPファイルが与えられます。
[q8.pcap](https://ksnctf.sweetduet.info/q/8/q8.pcap)

## 解説
とりあえず、PCAPファイルなのでみんな大好き[Wireshark](https://www.wireshark.org/)で解析します。