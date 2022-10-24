--- 
title: "TsukuCTF 2022 writeup" 
emoji: "📝" 
type: "tech" 
topics: ["ctf", "TsukuCTF", "OSINT", "Web"] 
published: true
--- 

みなさん、こんにちは．cork（コルク）です．
c0rkとしてcyseclabとして研究室の先輩と2人で参加しました．
僕は少し遅れて参加したのですが，先輩がかなり解いていたので残っているやつ頑張りました．
※この記事にはFlagが含まれています．

![](https://storage.googleapis.com/zenn-user-upload/0799c641db27-20221024.png)
![](https://storage.googleapis.com/zenn-user-upload/5cfd9f049d08-20221024.png)

# writeup
解いた問題
- [[OSINT] banana](#osint-banana)
- [[OSINT] TakaiTakai](#osint-takaitakai)
- [[OSINT] TsukuCTF Big Fan 1](#osint-tsukuctf-big-fan-1)
- [[OSINT] TsukuCTF Big Fan 3](#osint-tsukuctf-big-fan-3)
- [[OSINT] Robot](#osint-robot)
- [[OSINT] Bus POWER](#osint-bus-power)
- [[Web] bughunter](#web-bughunter)

## [OSINT] banana
Google lensにつっこみましたががでなかったので，色々な検索エンジンの画像検索を使ってみました．https://yandex.com/images/ で検索したらどうやらグアムであることがわかりました．
そこからGoogleで「グアム 壁画 バナナ」で調べたところ，デデドの朝市という場所であることがわかったのであとはGoogleMapで緯度と経度を調べるだけです．

`TsukuCTF22{13.5210_144.8287}`

## [OSINT] TakaiTakai
![](https://storage.googleapis.com/zenn-user-upload/c29229f1086c-20221024.jpg)
都会っぽいけど，個人的に自然が好きで都会に旅行を行かないのでどこかわからんということで特徴的な建物を探すことにしました．
ある程度高くてちょっと特徴がありそうな右上の建物をGoogle lensさんに調べてもらったところ中目黒アストラタワーであることがわかったのであとは，中央の黒い特徴的な団地？などを目安にGoogle Earthで探すとなんかそれっぽいところにきました．

![](https://storage.googleapis.com/zenn-user-upload/fbedf765bcde-20221024.png)

建物の名前が渋谷ソラスタであることがわかったので，あとは開業日を調べるだけなのですが「渋谷ソラスタ 開業日」と検索したところ渋谷ソラスタを管理しているっぽい東急不動産が公式で出しているのが下の2つだったので両方入れてみたものの違うと言われあれ？？と思っていました．
- https://www.tokyu-land.co.jp/news/92b9de3e94206f6a7e94d40da9d65473_1.pdf
- https://www.tokyu-land.co.jp/news/2019/001012.html

検索のトップにはWikipediaが開業日としている日付が書かれていたのですが，個人的にWikipediaをあまり信用していないので公式で出しているのを頑張って探していました．一応この日付はなんだろうと思い調べたところ施工日であることがわかりました．
もしや、、と思って施工日を入れたところいけました．

`TsukuCTF22{2019/03/29}`

※運営の方に報告したところ先ほどのリンクの1つ目に記載されている日付も正解にしてくださるということになりました．僕がひねくれてたのが悪いんですけど，お忙しい中対応いただきありがとうございました．

## [OSINT] TsukuCTF Big Fan 1
![](https://storage.googleapis.com/zenn-user-upload/353723ab57e2-20221024.png)

大ファンというからにはTwitterぐらいはフォロワーしてるやろということで[TsukuCTFのTwitterアカウント](https://twitter.com/tsukuctf)のフォロワー欄を探しているとそれらしき人がいました．

![](https://storage.googleapis.com/zenn-user-upload/581bfadcefcd-20221024.png)

あとは，[便利なツール](https://lab.syncer.jp/Tool/Twitter-Start-Date-Checker/)使ってこの人のアカウント作成日を調べて終わりです．

`TsukuCTF22{2021/11/29}`

## [OSINT] TsukuCTF Big Fan 3
Big Fan 1が終わった段階で2，3と続いていくので先に解こうと思ってヒントを探していると，怪しい投稿を発見しました．

![](https://storage.googleapis.com/zenn-user-upload/4c0fe6b990c7-20221024.png)

アーカイブ残ってないかなと思い，[Wayback Machine](https://archive.org/)で調べてみるとありました．

![](https://storage.googleapis.com/zenn-user-upload/e77033a10b88-20221024.png)

ここにアクセスするとREADME.txtとdummy.csvがありました．dummy.csvには個人情報がいくつも書かれており，README.txtはこれが偽の個人情報ですよっていう注意書きでした．
ここから誰が串田つよしさんなのかを探したのですが，ツイートをもう少しみてみると気になる投稿をしていました．

![](https://storage.googleapis.com/zenn-user-upload/e14c27b54a94-20221024.png)

これより，dummy.csvに「byu」で検索をかけると串田つよしさんを名乗る人が出てきました．

`TsukuCTF22{1980/01/10}`

## [OSINT] Robot
見た感じ中国っぽいのでGoogle lensでは厳しそうだと思い，[baidu.comのマップ](https://map.baidu.com/)で画像に書かれてある文字列を検索することにしました．

![](https://storage.googleapis.com/zenn-user-upload/a446b69945ff-20221024.png)

华南理工大学という文字が見えたので英語名を検索して終わりです．

`TsukuCTF22{South China University of Technology}`

## [OSINT] Bus POWER
![](https://storage.googleapis.com/zenn-user-upload/061844471139-20221024.jpg)

まず関西人パワーで230円が見えた時点で京都市内を走るバスであることは特定しました．

![](https://storage.googleapis.com/zenn-user-upload/dea5e61970b7-20221024.png)

次に，条河という文字が見えたのでおそらく四条河原町行きのバスであることがわかりました．
先輩と協力して解いていて，最初は2人とも脳筋戦法で四条河原町行きのバスを始発から全て辿っていくということをしていたのですが，僕は途中で嫌すぎて他にヒントがないか見ていました．

![](https://storage.googleapis.com/zenn-user-upload/f56b845d567d-20221024.png)

写真の中央らへんに大きな看板があることに気づいて，最初は手前の2文字が本栄に見えたので検索していましたが，見つからず．
そこらへんに転がってる鮮明化ツールで画像を少し鮮明化して画像とにらめっこしていると，〇〇〇工所かなと思い自分の思いつく限り鐵工所か鉄工所の2択だったので京都市内で調べると見つかりました．
なぜか子供の頃から友達の汚い字を解読する才能があったので，それが活きたかもしれません．

![](https://storage.googleapis.com/zenn-user-upload/3e536d80af83-20221024.png)
![](https://storage.googleapis.com/zenn-user-upload/99f920b3361a-20221024.png)

あとは交差点まで進んで名前を調べるだけです．

`TsukuCTF22{千本今出川}`

## [Web] bughunter
タグになにやらRFC9116という文字があったので，調べてみるとこんな感じで描かれていました．

> 研究者によってセキュリティの脆弱性が発見されると、適切な報告チャネルが不足していることがよくあります。その結果、脆弱性は報告されていないままになる可能性があります。このドキュメントでは、組織が脆弱性の開示慣行を説明して、研究者が脆弱性を容易に報告できるようにするために、マシンと並ぶ形式（ "Security.txt"）を定義します。（https://tex2e.github.io/rfc-translater/html/rfc9116.html）

要するに脆弱性を見つけた場合ここに連絡したらいいよっていうのが定義されている感じっぽい．
どうやら`.well-known/security.txt`に置かれるらしいので，見てみます．

http://133.130.103.51:31415/.well-known/security.txt

![](https://storage.googleapis.com/zenn-user-upload/35bf10bbb314-20221024.png)

全然知らなかったので，勉強になりました．

`TsukuCTF22{y0u_c4n_c47ch_bu65_4ll_y34r_r0und_1n_7h3_1n73rn37}`

# 感想
OSINTは全問題かなり楽しかったです．特に，Bus POWERはあんな感じの京都の道って山ほどあるのでわかりそうでわからないって感じがしてとても解きごたえのある問題でした．
解けなかった問題も近いところまでは行ってるけど解けないみたいなところがあって全部解いてる~~高度ネトスト人材の~~方はすごいなと思いました．
運営の方もいろいろ大変だったとは思いますが，お疲れ様でした．ありがとうございました．
