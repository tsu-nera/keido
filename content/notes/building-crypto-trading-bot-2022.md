+++
title = "✅WIP:仮想通貨Botの自動売買で稼ぐ方法(2022)"
lastmod = 2022-07-17T10:13:18+09:00
tags = ["WIP", "FUTURISMO", "BML"]
draft = false
+++

<div class="ox-hugo-toc toc">

<div class="heading">Table of Contents</div>

- [仮説ベースで考えてみる.](#7bd9bf)
- [✅勝てるBot仮説](#a1b50f)
    - [✅2022に稼げる仮想通貨Botのマーケットはxxx](#2c66f1)
    - [✅開発するBotはmm bot -&gt; ml bot](#bf3382)
    - [✅mlbotの改造ポイントはxxx](#b820e3)
    - [✅勝てる取引所はxxx](#919de3)
    - [✅勝てる開発言語はxxx](#376b17)
- [✅結論: ClojureでCEX(xxx)でのml botを作成](#2b38e1)
- [🔗References](#3b90d2)

</div>
<!--endtoc-->

2022からでも仮想通貨Botの自動売買は稼げるかを開発前に仮説ベースで検証していきます.

-   url: <https://futurismo.biz/building-crypto-trading-bot-2022/>
-   tags.
    -   [🔖CryptBot]({{< relref "20220603152137.md" >}})


## 仮説ベースで考えてみる. {#7bd9bf}

過去1年稼げないマーケットで努力してすごく無駄な努力をした. 先月ガッツリ[📝仮説思考]({{< relref "20220527175824.md" >}})の本を読んだ. なので, 今回はその知識の実践も兼ねて, 開発をする前に仮説ベースである程度戦略を立てて見ようと思う.

とりあえずやってみない. [稼げてる人は稼げると言わない]({{< relref "20220716112627.md" >}}).


## ✅勝てるBot仮説 {#a1b50f}


### ✅2022に稼げる仮想通貨Botのマーケットはxxx {#2c66f1}

-   📍勝てる市場を見極める.

これが最重要イシュー. 釣りの名人でも魚がいなければ魚は釣れない. どんなに技術が優れていてもマーケットがだめだと駄目. とくにネガティブサムゲームはオワコンの隣の世界はヌルゲーの可能性が高い.

しかし閑散期とバブル期の観点だと, 閑散期の次にくるバブルも考慮するか. どうせ駆け出しは稼げるようになるまで数ヶ月は学習のほうが多いので.


#### 🔍過去1年の参入者での実績を出した事例 {#1870ec}


#### 🔍ビットコイン冬の時代の検証 {#a10182}

2022/05前半LUNAショック後, 相場が低迷.

-   [冬の時代のbotterの歩き方｜Hoheto (仮想通貨botter)｜note](https://note.com/hht/n/n8f4afa2ec02a)


#### 🔍高頻度Botオワコン説の検証 {#de2e5a}

ref. <https://twitter.com/muzineco/status/1544871942083072000>


### ✅開発するBotはmm bot -> ml bot {#bf3382}

-   📍勝てるBotの種類を見極める
-   📍勝てる戦略を見極める.

仮想通貨Botにはいろんな種類がある.

このなかで, なぜxxbotを開発するのかを明確にする. 流行ではなく今の自分の状況と強みを考慮した最適戦略の意思決定がしたい.

-   [🔍仮想通貨bot手法]({{< relref "20220603152137.md#73d718cb-a2fb-4add-8d46-41485ffc4db1" >}})


#### 📊元手が少ない場合の回収までのスピード {#47eb80}

個人的に大きなイシューは, 元の資金が少ないのでリターンのインパクトよりも利益までの速さが重要となる.


#### 📊開発の難易度のマトリックス {#26a388}

T.B.D.


#### 🔍MLbotの現状2022 {#1ea9c9}

りっちまん本によって参入した人の大半は機械学習がわからない. それはKindleの評価欄の感想とTwitterから観測した. ぼくには難しいと言っていた人が多い.

そして単純な予測ではみんなが仲良く稼げるわけがない. 特徴量か裁定ロジックで差別化が必要.

稼げている人がTwitterでたまにいた. 私の仮説では, 稼げている人はKaggleガチ勢のBotter参入なのでは? そしてrichmanbtc関係なくもともと持っている機械学習の知識と技術を仮想通貨botに適用して稼げているのだと.

さらに, 書籍発売12月の１ヶ月前にkaggleコンペで仮想通貨市場の予測が開かれたのもKaggler参入のタイミングにちょうどよい.

[G-Research Crypto Forecasting | Kaggle](https://www.kaggle.com/competitions/g-research-crypto-forecasting/)


#### 💡アビトラBotよりもむしろmlbot {#38eb77}


#### 💡dex botよりもむしろ mlbot {#2c1179}


#### 💡mmbotよりもむしろmlbot {#15e7b9}


### ✅mlbotの改造ポイントはxxx {#b820e3}

-   📍勝てる戦略を見極める.

mlbotを開発しようとしたときに, チュートリアル通りにやっても稼げない. そこで, 改造ポイントを見極める.

選択肢は以下のようなものがある.

-

-


### ✅勝てる取引所はxxx {#919de3}

-   📍勝てる取引所を選定する.


### ✅勝てる開発言語はxxx {#376b17}

宗教上の理由でClojureでやりたいものの, 果たしてその選択をしていいのかを検索ベースで検証する.

-   Python
-   JavaScript
-   Rust
-   Clojure
-   Common Lisp


#### <span class="org-todo todo _">🔬</span> Trading BotのPoC {#9e6818}

実際にかんたんなサンプルプログラムを組んで見る.


## ✅結論: ClojureでCEX(xxx)でのml botを作成 {#2b38e1}


## 🔗References {#3b90d2}

-   [システムトレードで億万長者になるぞ! coursera で Computational Investing Part I を受けた | Futurismo](https://futurismo.biz/archives/2678/)
-   [夏休みの自由研究 は OANDA APIを利用して FX システムトレード | Futurismo](https://futurismo.biz/archives/4392/)
-   [pybitflyer をつかって Python で ビットコインレートを取得してみた | Futurismo](https://futurismo.biz/archives/6401/)
