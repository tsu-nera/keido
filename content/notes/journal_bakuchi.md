+++
title = "📓仮想通貨Bot開発日誌"
tags = ["JOURNAL", "bakuchi"]
draft = false
+++

Twitterにつぶやいてもいいんだけど, Twitterがきらいであまりアプリを開きたくないのでとりあえずここにプレーンテキストでつぶやきをためていく実験をしてみる.

使いみちはTwitterのように思いついたものをただ書くだけなので単なるアイデアにすぎない.


## 2022 {#3a8241}


### 2022-W28 {#b0dbf5}


#### 2022-07-15 Friday {#e1f807}

<!--list-separator-->

-  org-captureの設定を整えた

    Captured On: <span class="timestamp-wrapper"><span class="timestamp">&lt;2022-07-15 Fri 15:01&gt;</span></span>

<!--list-separator-->

-  2022のトレンドは自分の知っている状況よりももっと多様かもしれない.

    そもそもTwitterを眺めていても知らない単語がとても多い. まずは情報収集をしつつ, 知らない単語を勉強していくことにするか. そもそも, なにかを理解しようとしたときに, 専門用語がわからないと入口に立てないし, 逆に言えばまずは概念を理解していくことから始まる.
    Captured On: <span class="timestamp-wrapper"><span class="timestamp">&lt;2022-07-15 Fri 17:24&gt;</span></span>

<!--list-separator-->

-  dexってなに？

    <https://twitter.com/yamasakasan/status/1536816703329382400>

    DeFi 完全初心者への徹底解説: 画期的な分散型金融の実像入門 仮想通貨の作り方 プログラミングで学ぶブロックチェーン技術・ハッシュ・P2Pのしくみ

    Captured On: <span class="timestamp-wrapper"><span class="timestamp">&lt;2022-07-15 Fri 17:33&gt;</span></span>

<!--list-separator-->

-  思いついたアイデアをキャプチャする.

    アイデアはIssue Treeで構造化する. 構造化することによりMECEな視点や優先順位が見える. 論点が見えたらそれをひっくり返して逆算して考える.

    Kindleの無料の書籍とnoteから論点をピックアップしてもいいな. Issue TreeでMECEに整理する. どうしようかな, 仮説だけでまずは知りたいことを洗い出してそれから調査するのが筋かな. なにを知りたいのか？

    Captured On: <span class="timestamp-wrapper"><span class="timestamp">&lt;2022-07-15 Fri 17:37&gt;</span></span>

<!--list-separator-->

-  なぬ？botterのdiscordってなに？

    -   ref. <https://twitter.com/yseeker0/status/1520386304428883968>
        -   botterのdiscord、非同期化とか並列化とか無限に有益な情報があってとても勉強になる。

    Captured On: <span class="timestamp-wrapper"><span class="timestamp">&lt;2022-07-15 Fri 17:47&gt;</span></span>

<!--list-separator-->

-  まさかrichmanbtc本によってbotter界隈にkagger勢きてる？

    <https://twitter.com/yseeker0/status/1488149672422088710>

    そして, mlbotはそのままでは稼げなくて, kaggleガチ勢が改良することによって稼げている? そのまま動かしました破ってみました系の人の情報が気になる. ここは論点になりそう.

    kindleの書評をみると知識がないけどとりあえず読みましたがぼくには難しかったですという感想があまりにも多いが, JupyterNotebookとかみてもkaggleをやっている人からすればなにも難しくないレベルなきがする.

    Captured On: <span class="timestamp-wrapper"><span class="timestamp">&lt;2022-07-15 Fri 17:54&gt;</span></span>

<!--list-separator-->

-  richmanbtcさん2ヶ月くらいつぶやいてない...

    なんか他のひとからの陰口が多い気が... 嫌われているのかな?

    普通に考えると手法を無料で公開してしまい, 感謝が多い気がするのだが.

    Captured On: <span class="timestamp-wrapper"><span class="timestamp">&lt;2022-07-15 Fri 18:06&gt;</span></span>

<!--list-separator-->

-  botter界隈がネガティブサムゲームならば,

    書籍出版によって養分を参加させて掠め取るという戦略ならば頭いいな.

    <https://twitter.com/richmanbtc2/status/1466669162735222786>

    Captured On: <span class="timestamp-wrapper"><span class="timestamp">&lt;2022-07-15 Fri 20:47&gt;</span></span>

<!--list-separator-->

-  おや, cryptoの値動きをMLで予測するkaggleコンペ

    <https://www.kaggle.com/competitions/g-research-crypto-forecasting/>

    これ, twitter界隈での話題はどうなんだろう.

    Captured On: <span class="timestamp-wrapper"><span class="timestamp">&lt;2022-07-15 Fri 21:04&gt;</span></span>

<!--list-separator-->

-  bybitしらなかった, けっこう話題なので調べる

    Captured On: <span class="timestamp-wrapper"><span class="timestamp">&lt;2022-07-15 Fri 21:16&gt;</span></span>

<!--list-separator-->

-  仮想通貨Botにkaggleで拾った知識をt混ぜてみるのは面白そうだしわたしは機械学習に抵抗がないのは強みになる. しかし問題はPythonを捨ててClojureでやりたいと考えたときのClojureと機械学習の相性だな.

    Captured On: <span class="timestamp-wrapper"><span class="timestamp">&lt;2022-07-15 Fri 22:01&gt;</span></span>


#### 2022-07-16 Saturday {#e9f043}

<!--list-separator-->

-  作業開始.

    Captured On: <span class="timestamp-wrapper"><span class="timestamp">&lt;2022-07-16 Sat 10:27&gt;</span></span>

<!--list-separator-->

-  気になる発言. 過去１年でレッドオーシャンでの努力ほど虚しいことを知ったのでオワコンに恐怖を感じる. 行動の前によく調べる必要がある.

    最近の高頻度損益、マジでオワコンになってきていて、勝ってる人はどうやって勝ってるの感isある
    <https://twitter.com/muzineco/status/1544871942083072000>

    Captured On: <span class="timestamp-wrapper"><span class="timestamp">&lt;2022-07-16 Sat 10:31&gt;</span></span>

<!--list-separator-->

-  まずはBotの種類を再確認して方針を決めることがビッグイシュー.

    少ない資金を元手でコストが安いという観点からの絞り込が必要.

    正直ここが狂うとその後の調査かやり直しになる分岐点.

    仮にDex Botを選択したばあい, Rustの技術可能性は一つのサブイシューになる. MLBotの場合, Clojureで果たしていけるのかPythonとの比較がサブイシューとなる.

    まずは見極めのための情報収集を. Botの特徴を手早くまとめないと. richmanbtc出ない可能性も検討なので, mlbotに時間を割くのを保留.

    Captured On: <span class="timestamp-wrapper"><span class="timestamp">&lt;2022-07-16 Sat 10:41&gt;</span></span>

<!--list-separator-->

-  dex botも市場が傾いた？

    <https://twitter.com/sazan_dev/status/1532598715290034177>

    要約すると、既存の狩場は終了のお知らせ.

    ---
    Captured On: <span class="timestamp-wrapper"><span class="timestamp">&lt;2022-07-16 Sat 11:38&gt;</span></span>

<!--list-separator-->

-  dex botは競プロスキル, mlbotはkaggleスキル？

    <https://twitter.com/sazan_dev/status/1532885093777145857>

    お金儲けだけならML botで本気だすのも、DeFi bot攻略するのも同じくらい儲かりそうなのに、なんでMLやる気でないのかなーと思ってたんだけど、、、

    結局もうML飽きてるってのが答えな気がしてきた。賞味期限15年くらい

    でも超絶儲かりそうとかだったらやる

    Captured On: <span class="timestamp-wrapper"><span class="timestamp">&lt;2022-07-16 Sat 11:40&gt;</span></span>

<!--list-separator-->

-  Twitterのスキルを活かしてBot作成できないかな？

    Captured On: <span class="timestamp-wrapper"><span class="timestamp">&lt;2022-07-16 Sat 12:09&gt;</span></span>

<!--list-separator-->

-  資金面で選択肢がHFTかもしれん. 圧倒的に資金ないから.

    Captured On: <span class="timestamp-wrapper"><span class="timestamp">&lt;2022-07-16 Sat 14:04&gt;</span></span>

<!--list-separator-->

-  solana botはC言語低レベルしかでなきかったわたしには相性いいかも

    Python botterがほとんどな世の中で, どちらかというとC言語と低レイヤでもがき続けてきたことしかしてないわたしはここしか強みがでないのでは？Rustも面白そうだしいつかはやってみたいと思っている.

    ただ, 小さなリスクで確実にいこうとするとdex botは今は見送りかな...

    今日はいろいろ情報収集をしてbot作成のための解像度が上がった. 明日は意思決定をしていく.

    戦略的に仮説思考しようとしたものの, たいしたことはできてないが, wikiにまとめる力だけがフル回転している.

    Captured On: <span class="timestamp-wrapper"><span class="timestamp">&lt;2022-07-16 Sat 23:57&gt;</span></span>


#### 2022-07-17 Sunday {#7aaab6}

<!--list-separator-->

-  今日はどんなBotを作成するか意思決定をしたい. そのためには比較軸で比較する.

    Captured On: <span class="timestamp-wrapper"><span class="timestamp">&lt;2022-07-17 Sun 08:20&gt;</span></span>

    [📝ドテン君]({{< relref "20220717083642.md" >}})の調査完了. これは深堀しなくてもいいかな.

<!--list-separator-->

-  元手を軸にしたストラテジの選択がキモ

    Captured On: <span class="timestamp-wrapper"><span class="timestamp">&lt;2022-07-17 Sun 10:15&gt;</span></span>

    どんなbotをつくるかは結局ストラテジであり, その判断のための1番の軸は少ない資金という制約条件. ここの解像度を上げて意思決定をする. たぶんここが１番のイシュー.

<!--list-separator-->

-  Google検索でなんだよこれとおもったら自分の文章だったwww

    Captured On: <span class="timestamp-wrapper"><span class="timestamp">&lt;2022-07-17 Sun 17:58&gt;</span></span>

    <https://github.com/tsu-nera/bakuchi/wiki>


### 2022-W29 {#3977fe}


#### 2022-07-18 Monday {#517667}

<!--list-separator-->

-  binanceの手数料解禁は最近?これによりmmbotのハックができる？

    後発組としては新規市場は注目に値する.

    -   <https://twitter.com/misanfx/status/1544999480088461316?t=U54-YsA-dl7hMVXZrLWzXw&s=19>
    -   <https://www.binance.com/en/support/announcement/10435147c55d4a40b64fcbf43cb46329>

    Captured On: <span class="timestamp-wrapper"><span class="timestamp">&lt;2022-07-18 Mon 08:29&gt;</span></span>

    色々やったのにBINANCE手数料無料現物だけじゃんワロタ
    <https://twitter.com/hanahira_ri/status/1546382085031870465>

<!--list-separator-->

-  現物と先物をもう一度復習する

    Captured On: <span class="timestamp-wrapper"><span class="timestamp">&lt;2022-07-18 Mon 08:53&gt;</span></span>

<!--list-separator-->

-  FTX JP口座開設キャンペーン

    <https://help-jp.ftx.com/hc/ja/articles/7297768019737>

    -   [X] 新規口座開設手続きを完了
    -   [ ] アカウントの承認が完了
    -   [ ] FTX JP販売所にて100円以上の暗号資産を取引する

<!--list-separator-->

-  FTX JPは手数料無料のための10万が払えないので諦めてbitflyerにする. APIの自作が必要そうだな...

    Captured On: <span class="timestamp-wrapper"><span class="timestamp">&lt;2022-07-18 Mon 20:12&gt;</span></span>

<!--list-separator-->

-  clojureでのbitflyer api wrapperを作成していく

    Captured On: <span class="timestamp-wrapper"><span class="timestamp">&lt;2022-07-18 Mon 20:20&gt;</span></span>


#### 2022-07-19 Tuesday {#3f0b18}

<!--list-separator-->

-  httpkitはwebsocketをサポートしているけど, なにもwebsocket libraryはそれだけではないのでとりあえず慣れたclj-httpをつかう

    Captured On: <span class="timestamp-wrapper"><span class="timestamp">&lt;2022-07-19 Tue 06:49&gt;</span></span>

<!--list-separator-->

-  clojureでイベントドリブンな状態遷移ってどうかけばいいの？

    Captured On: <span class="timestamp-wrapper"><span class="timestamp">&lt;2022-07-19 Tue 19:13&gt;</span></span>


#### 2022-07-20 Wednesday {#854f0e}

<!--list-separator-->

-  bitflyerのprivate apiが気軽に叩けないことに気づいたので認証を実装する.

    Captured On: <span class="timestamp-wrapper"><span class="timestamp">&lt;2022-07-20 Wed 06:25&gt;</span></span>

    <https://github.com/knowm/XChange/blob/develop/xchange-bitflyer/src/main/java/org/knowm/xchange/bitflyer/service/BitflyerDigest.java>

    ---

    <https://github.com/after-the-sunrise/bitflyer4j/blob/master/src/main/java/com/after_sunrise/cryptocurrency/bitflyer4j/core/impl/HttpClientImpl.java>
    <https://github.com/knowm/XChange/blob/develop/xchange-core/src/main/java/org/knowm/xchange/utils/DigestUtils.java>

<!--list-separator-->

-  bitflyerのエラーがわからないな, これってエラーがよく変える前提でつくるのかな...

    Captured On: <span class="timestamp-wrapper"><span class="timestamp">&lt;2022-07-20 Wed 09:53&gt;</span></span>

    <https://note.com/wanna_be_free/n/n009968671ed6>

    magitoサンプルはリトライしている.

    とりあえずさきに進むか...

<!--list-separator-->

-  xchangeのライブラリをつかうことにする. 自前はいいや...

    Captured On: <span class="timestamp-wrapper"><span class="timestamp">&lt;2022-07-20 Wed 13:30&gt;</span></span>

<!--list-separator-->

-  だめだな, xchangeのdtoがウザい.

    Captured On: <span class="timestamp-wrapper"><span class="timestamp">&lt;2022-07-20 Wed 14:25&gt;</span></span>

<!--list-separator-->

-  おかしいなさっきはやっても取得できて, 今はなんどやっても取得エラーする

    Captured On: <span class="timestamp-wrapper"><span class="timestamp">&lt;2022-07-20 Wed 19:03&gt;</span></span>

<!--list-separator-->

-  もくしかして署名はリクエストごとに使い回さないといけないのか?一定時間立つと問題ないな.

    Captured On: <span class="timestamp-wrapper"><span class="timestamp">&lt;2022-07-20 Wed 19:16&gt;</span></span>

<!--list-separator-->

-  ついにわかった...

    Captured On: <span class="timestamp-wrapper"><span class="timestamp">&lt;2022-07-20 Wed 19:33&gt;</span></span>

    ```clojure
    (defn toHexString
      "Convert bytes to a String"
      [bytes]
      (apply str (map #(format "%02x" %) bytes)))
    ```

    %xを%02xに変更したらできた.
    これで１日潰れるとは...


#### 2022-07-21 Thursday {#8d0ac8}

<!--list-separator-->

-  とりあえずorderがやっとapiからできた. 一歩前進した.

    Captured On: <span class="timestamp-wrapper"><span class="timestamp">&lt;2022-07-20 Wed 20:05&gt;</span></span>

<!--list-separator-->

-  botのloopをつくっていく. Clojureでloopはどうやるんだろう.

    Captured On: <span class="timestamp-wrapper"><span class="timestamp">&lt;2022-07-21 Thu 13:25&gt;</span></span>

<!--list-separator-->

-  おそらくintegrantがstart/stopの機能を気軽に提供する点でよいんだ. 問題は, loopの部分. serverのようなフレームワークではなくてもっと気軽なものがいい.

    Captured On: <span class="timestamp-wrapper"><span class="timestamp">&lt;2022-07-21 Thu 13:30&gt;</span></span>

<!--list-separator-->

-  integrationにchimeを組み込む

    <https://ilyaletre.hatenablog.com/entry/2018/04/15/175037>
    Captured On: <span class="timestamp-wrapper"><span class="timestamp">&lt;2022-07-21 Thu 13:33&gt;</span></span>

<!--list-separator-->

-  chimeの無限ループを停止するにはどうすればいいの？

    Captured On: <span class="timestamp-wrapper"><span class="timestamp">&lt;2022-07-21 Thu 15:25&gt;</span></span>

<!--list-separator-->

-  フォワードテスト的なデモトレードがしたいな... 実際のお金をかけると損しそうなので.

    Captured On: <span class="timestamp-wrapper"><span class="timestamp">&lt;2022-07-21 Thu 20:02&gt;</span></span>

<!--list-separator-->

-  ぜんぜんspreadとしきい値があわないな. eff tickがいけないのかな...

    Captured On: <span class="timestamp-wrapper"><span class="timestamp">&lt;2022-07-21 Thu 20:28&gt;</span></span>

<!--list-separator-->

-  マーケットメイクの原理が理解できてないからそれを見えるようにしないとな. 紙上で理解するのがいいのかも.

    Captured On: <span class="timestamp-wrapper"><span class="timestamp">&lt;2022-07-21 Thu 21:02&gt;</span></span>

<!--list-separator-->

-  マーケットメイクを正しく理解するとともにeffの算出を正確に実装する必要がある.

    Captured On: <span class="timestamp-wrapper"><span class="timestamp">&lt;2022-07-21 Thu 21:10&gt;</span></span>

<!--list-separator-->

-  とりあえずこれで１週間経過か... まだまだ先が長そうだ...

    Captured On: <span class="timestamp-wrapper"><span class="timestamp">&lt;2022-07-21 Thu 21:12&gt;</span></span>
