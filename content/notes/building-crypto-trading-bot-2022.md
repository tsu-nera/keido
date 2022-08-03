+++
title = "🖊仮想通貨Botの自動売買で稼ぐ方法(2022/07)"
lastmod = 2022-08-03T07:35:21+09:00
tags = ["FUTURISMO", "BML"]
draft = false
+++

<div class="ox-hugo-toc toc">

<div class="heading">Table of Contents</div>

- [仮説ベースで考えてみる](#仮説ベースで考えてみる)
- [<span class="org-todo todo _">💡</span> 勝てるBot仮説](#勝てるbot仮説)
    - [✅高頻度mmbotで小さな成功体験を目指す](#高頻度mmbotで小さな成功体験を目指す)
    - [✅戦う取引所はFTX JP](#戦う取引所はftx-jp)
    - [✅開発言語はClojure](#開発言語はclojure)
- [✅結論: ClojureでFTXJPでのmmbotを作成](#結論-clojureでftxjpでのmmbotを作成)
- [🔗References](#references)

</div>
<!--endtoc-->

2022/07からでも仮想通貨Botの自動売買は稼げるかを開発前に仮説ベースで検証していく.

-   up: [🖊Futurismo]({{< relref "20220624083448.md" >}})
-   url: <https://futurismo.biz/building-crypto-trading-bot-2022/>
-   tags.
    -   [🔖CryptBot]({{< relref "20220603152137.md" >}})


## 仮説ベースで考えてみる {#仮説ベースで考えてみる}

過去1年稼げないマーケットで努力してすごく無駄な努力をした. 先月ガッツリ[📝仮説思考]({{< relref "20220527175824.md" >}})の本を読んだ. なので, 今回はその知識の実践も兼ねて, 開発をする前に仮説ベースである程度戦略を立てて見ようと思う. とりあえずやってみない. [稼げてる人は稼げると言わない]({{< relref "20220716112627.md" >}}).


## <span class="org-todo todo _">💡</span> 勝てるBot仮説 {#勝てるbot仮説}


### ✅高頻度mmbotで小さな成功体験を目指す {#高頻度mmbotで小さな成功体験を目指す}

-   📍勝てるBotの種類を見極める
-   📍勝てる戦略を見極める.

仮想通貨Botにはいろんな種類がある.

このなかで, なぜmmbotを開発するのかを明確にする. 流行ではなく今の自分の状況と強みを考慮した最適戦略の意思決定がしたい.

-   [🔍仮想通貨bot手法]({{< relref "20220603152137.md#仮想通貨bot手法" >}})

現在, けっこう元手がない. そのため最も大事な論点は **少ない元手でまずは小さい利益を上げること**. 100円でいいのでまずは小さな成功体験がほしい.


#### <span class="org-todo todo _">✅</span> スイングbotではなく高頻度bot {#スイングbotではなく高頻度bot}

ref. [高頻度(HFT)botとスイングbot比較]({{< relref "20220603152137.md#高頻度--hft--botとスイングbot比較" >}})

小さく確実な成功体験という軸を考えると, スイングbotより高頻度botのほうが適切.

さらに2022/05から[冬の相場](https://note.com/hht/n/n8f4afa2ec02a)と喩えられる換算相場なのも気になるのでこれを考えてもスイングは不適切.


#### <span class="org-todo todo _">✅</span> Dex BotよりもCEX bot {#dex-botよりもcex-bot}

ゼロサム・ゲームであるので競争を避けるという点でDex市場にはとても魅力を感じるが, 小さな成功体験という点では大きなリスクになってしまうので, まずは過去の再現性を考えてCEXを相手にするbotを作成する.


#### <span class="org-todo todo _">✅</span> アビトラbotではなくmmbot {#アビトラbotではなくmmbot}

元手が少ない状態から小さな成功体験を目指す時, アビトラbotよりも高頻度botがよいと考えた.

CEX botでいこうとした場合, イベントのような歪みで大きく稼ぐアビトラbotは小さな成功体験という点で適切ではない.

いろいろな前提抜きにすると, 2年前にアビトラbotを開発していたというのもあり, 今回は別の方法を試したいという思いもある.


#### <span class="org-todo todo _">✅</span> mlbotではなくmmbot {#mlbotではなくmmbot}

ここまで絞れたらmmbotとmlbotが選択肢として上がる.

ここでも小さな成功体験を軸にmmbotを選ぶ. mlbotの場合はモデル構築というひと手間が加わる. りっちまんチュートリアルの模倣のレールに乗るのは安心感があるものの, 同じ特徴量だと稼げないのでモデル改善による差別化が必須.

りっちまん本によって参入した人の大半は機械学習がわからない. それはKindleの評価欄の感想とTwitterから観測した. ぼくには難しいと言っていた人が多い.

稼げている人がTwitterでたまにいた. 私の仮説では, 稼げている人はKaggleガチ勢のBotter参入なのでは? そしてrichmanbtc関係なくもともと持っている機械学習の知識と技術を仮想通貨botに適用して稼げているのだと. さらに, 書籍発売12月の１ヶ月前にkaggleコンペで仮想通貨市場の予測が開かれたのもKaggler参入のタイミングにちょうどよい.

[G-Research Crypto Forecasting | Kaggle](https://www.kaggle.com/competitions/g-research-crypto-forecasting/)

---

しかし高頻度botですら試してみて稼げるのか怪しさはある. とにかくレッドオーシャンは駄目.

> ;; <https://twitter.com/muzineco/status/1544871942083072000>
>
> 最近の高頻度損益、マジでオワコンになってきていて、勝ってる人はどうやって勝ってるの感isある

幸いわたしもMLの知識は初歩ならばありモデルも構築できるので, mmbotでだいたい雰囲気がわかったらmlbotに進化させる. 敵がいない方向にいかないと...


### ✅戦う取引所はFTX JP {#戦う取引所はftx-jp}

-   📍勝てる取引所を選定する.

mmbot(HFTbot)作成の場合, 取引所の手数料が１番厄介な気がする. 4年前2年前でそれぞれいろいろ口座開設済のものもあるが2022現在の最新の適切な取引所を選びたい.

そこそこ比較検討候補が多いものの, 一つ一つ調べていると面倒なのでTwitterから観測できる最近使われている取引所で絞り込みをかけて検討する. ということで候補に上げたのは以下3つ.

-   bitFlyer
-   GMOコイン
-   FTX Japan

bitFlyerとGMOは昔からよく使われていてFTX Japanは2022/04ごろ?から日本上陸とかでこれから宣伝かかっていきそうな勢い(さっき作成したてのYoutubeチャンネル登録した(2022/07/18)). 過去のネット記事ならばbitFlyerやGMOが多そうだがこれからはFTXJPが多そう. そして過去mmbotをすでに作成している人たちは当然横展開でFTXJPにもきそうな気がする.

まあしかし最近流行りという意味でFTXJPでとりあえずいってみようかな(あまり戦略的な意思決定ではない... ).

---

BINANCEが手数料無料化という発表が少し気になっているが今回はまだ飛びつかないで選択肢から外した.

-   [Binance Launches Zero-Fee Bitcoin Trading | Binance Support](https://www.binance.com/en/support/announcement/10435147c55d4a40b64fcbf43cb46329)

---

いずれにしろ取引所を柔軟に切り替えられるようなソフトウェアのつくりにしておこう.


### ✅開発言語はClojure {#開発言語はclojure}

[仮想通貨bot開発言語]({{< relref "20220717145220.md#仮想通貨bot開発言語" >}})

Clojureでやりたいものの果たしてその選択をして地獄落ちしないか確認. たぶん実際のところつくってみないとわからないかも.

データ分析がネックならそこだけPythonで分析すればいい. Clojureの遅延シーケンスと並行プログラミングのシンタックスに強い可能性を感じている.


## ✅結論: ClojureでFTXJPでのmmbotを作成 {#結論-clojureでftxjpでのmmbotを作成}

今までの考察をまとめると,

**ClojureでFTXJPのmmbotを作成**

という結論になった. とはいえ, このあとClojureでのPoC的なものを作成しつつ, もう少し手数料周りの深堀調査が必要とは思っている.


## 🔗References {#references}

-   [システムトレードで億万長者になるぞ! coursera で Computational Investing Part I を受けた | Futurismo](https://futurismo.biz/archives/2678/)
-   [夏休みの自由研究 は OANDA APIを利用して FX システムトレード | Futurismo](https://futurismo.biz/archives/4392/)
-   [pybitflyer をつかって Python で ビットコインレートを取得してみた | Futurismo](https://futurismo.biz/archives/6401/)
