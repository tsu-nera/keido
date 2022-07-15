+++
title = "✅WIP:仮想通貨Botの自動売買で稼ぐ方法(2022)"
lastmod = 2022-07-15T21:46:01+09:00
tags = ["WIP", "FUTURISMO", "BML"]
draft = false
+++

<div class="ox-hugo-toc toc">

<div class="heading">Table of Contents</div>

- [✅勝てるBot仮説](#a1b50f)
    - [✅2022からでも仮想通貨Botで稼げる](#d14cd0)
    - [✅開発するBotはmlbot](#fffb4f)
    - [✅勝てる取引所はBitflyer](#fc8e38)
    - [✅勝てる戦略はxxx](#cbeb3f)
- [✅開発言語はPythonではなくClojure](#b3a8a8)
    - [🔍Clojureでのtrading bot開発事例](#5753e9)
    - [🔍Clojureで開発するメリット](#7bfe2e)
    - [🔍Clojureで開発するデメリット](#ed4401)
    - [💡デメリットが大きくてもClojureを選ぶ理由](#8e43cb)
    - [<span class="org-todo todo _">🔬</span> Clojure Trading BotのPoC](#b5262e)
- [✅結論: ClojureでBitflyerを取引所にしたmlbotを作成する](#b97f61)
- [🔗References](#3b90d2)

</div>
<!--endtoc-->

2022からでも仮想通貨Botの自動売買は稼げるかを開発前に仮説ベースで検証していきます.

-   url: <https://futurismo.biz/building-crypto-trading-bot-2022/>
-   tags.
    -   [🔖CryptBot]({{< relref "20220603152137.md" >}})


## ✅勝てるBot仮説 {#a1b50f}


### ✅2022からでも仮想通貨Botで稼げる {#d14cd0}

-   📍強い既存Botterだけでなく新規参入者でも勝てるか？


#### 🔍過去1年の参入者での実績を出した事例 {#1870ec}


### ✅開発するBotはmlbot {#fffb4f}

-   📍勝てるBotの種類を見極める

仮想通貨Botにはいろんな種類がある.

このなかで, なぜmlbotを開発するのかを明確にする.


#### 🔍主な仮想通貨Botの種類 {#b0d34e}

-

-

-

ref.


#### 📊元手が少ない場合の回収までのスピード {#47eb80}

個人的に大きなイシューは, 元の資金が少ないのでリターンのインパクトよりも利益までの速さが重要となる.


#### 📊開発の難易度のマトリックス {#26a388}

T.B.D.


#### 🔍mlbotの現状2022 {#082c97}

richmanbtcによって参入した人の大半は機械学習がわからない. それはKindleの評価欄の感想とTwitterから観測した. ぼくには難しいと言っていた人が多い.

そして単純な予測ではみんなが仲良く稼げるわけがない. 特徴量か裁定ロジックで差別化が必要.

稼げている人がTwitterでたまにいた. 私の仮説では, 稼げている人はKaggleガチ勢のBotter参入なのでは? そしてrichmanbtc関係なくもともと持っている機械学習の知識と技術を仮想通貨botに適用して稼げているのだと.

さらに, 書籍発売12月の１ヶ月前にkaggleコンペで仮想通貨市場の予測が開かれたのもKaggler参入のタイミングにちょうどよい.

[G-Research Crypto Forecasting | Kaggle](https://www.kaggle.com/competitions/g-research-crypto-forecasting/)


#### 💡どてんBotよりもむしろmlbot {#c88676}


#### 💡アビトラBotよりもむしろmlbot {#38eb77}


### ✅勝てる取引所はBitflyer {#fc8e38}

-   📍勝てる取引所を選定する.


#### 🔍多くのbotterがbitflyerを選ぶ人気理由 {#efb0e4}


### ✅勝てる戦略はxxx {#cbeb3f}

-   📍勝てる戦略を見極める.

mlbotを開発しようとしたときに, チュートリアル通りにやっても稼げない. そこで, 改造ポイントを見極める.

選択肢は以下のようなものがある.

-

-


## ✅開発言語はPythonではなくClojure {#b3a8a8}

-   📍Clojureの優位性を見極める.
-   📍ClojureでPythonのようなデータ分析が可能かを見極める.


### 🔍Clojureでのtrading bot開発事例 {#5753e9}


### 🔍Clojureで開発するメリット {#7bfe2e}


### 🔍Clojureで開発するデメリット {#ed4401}


### 💡デメリットが大きくてもClojureを選ぶ理由 {#8e43cb}


### <span class="org-todo todo _">🔬</span> Clojure Trading BotのPoC {#b5262e}

実際にかんたんなサンプルプログラムをClojureで組んで見る. 既存のサンプルプログラムをClojureにポーティングをすることで実装可能性を検証する.


## ✅結論: ClojureでBitflyerを取引所にしたmlbotを作成する {#b97f61}


## 🔗References {#3b90d2}

-   [システムトレードで億万長者になるぞ! coursera で Computational Investing Part I を受けた | Futurismo](https://futurismo.biz/archives/2678/)
-   [夏休みの自由研究 は OANDA APIを利用して FX システムトレード | Futurismo](https://futurismo.biz/archives/4392/)
-   [pybitflyer をつかって Python で ビットコインレートを取得してみた | Futurismo](https://futurismo.biz/archives/6401/)
