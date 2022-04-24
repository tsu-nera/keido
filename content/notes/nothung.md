+++
title = "⚡My Emacs Config - Nothung"
author = ["Tsunemichi Harada"]
tags = ["Emacs"]
draft = false
+++

Emacsを極限まで叩き上げ, なによりも強靭な刃にする. [一つのことを極める](https://www.youtube.com/watch?v=04L18rQiIgw).

副題のノートォング(Nothung)とは勇者ジークフリートの持つ伝説の剣である.

-   <https://www.youtube.com/watch?v=B6wChr_geAg>
-   <https://www.youtube.com/watch?v=v31N8zxGhQY>

---

packageの並び順は [Doom Emacs](https://github.com/hlissner/doom-emacs) の [Molule Index](https://github.com/hlissner/doom-emacs/blob/develop/docs/modules.org) (アルファベット順)に従う.

ref: <https://github.com/tsu-nera/nothung>

いつも忘れるDoom Emacs Configuration記法は [ここ](https://github.com/hlissner/doom-emacs/blob/master/docs/getting_started.org#configuring-doom).

-   use-package! は:defer, :hook, :commands, or :after が省略されると起動時に loadされる.
-   after! は package が load されたときに評価される.
-   add-hook! は mode 有効化のとき. setq-hook!は equivalent.

どれを使うかの正解はないがすべて use-package!だと起動が遅くなるので場合によってカスタマイズせよ，とのこと.

ref. 過去の設定は[こちら](https://github.com/tsu-nera/dotfiles/tree/master/.emacs.d/inits).

```emacs-lisp
;;; $DOOMDIR/config.el -*- lexical-binding: t; -*-
(load-file "~/.doom.d/private/config.el")
```


## App {#app}


### Twitter {#twitter}

```emacs-lisp
;; App
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;

;; twittering-mode
;; この設定がないと認証が失敗した.
;; twittering-oauth-get-access-token: Failed to retrieve a request token
(use-package! twittering-mode
  :init
  (setq twittering-allow-insecure-server-cert t))
```


### eww {#eww}

Emacsのテキストブラウザ([Manual](https://www.gnu.org/software/emacs/manual/html_mono/eww.html))

notes:

-   ewwを起動しただけだとminibufferなのでC-gで消えてしまうので大きくC-x 1とかで大きくする.
-   C-u M-x ewwでひとつのbufferを使いまわすのではなく別のBufferでewwを開く.
-   M-RETでURLを新しいBufferで開く.
-   Doom EmacsだとC-c s o(online)でいろいろと検索できる(w/Chrome). helm-google-suggest的な.

<!--listend-->

```emacs-lisp
(use-package! eww
  :bind
  ("C-c s w" . eww-search-words)
  ("C-c o w" . eww-open-in-new-buffer))
```

-   ace-linkをつかうとewwのlinkをインタラクティブに選択できて便利.

<!--listend-->

```emacs-lisp
(use-package! ace-link
  :config
  (eval-after-load 'eww '(define-key eww-mode-map "f" 'ace-link-eww))
  (ace-link-setup-default))
```


### org-web-tools {#org-web-tools}

ewwとorgを便利にするツール群(<https://github.com/alphapapa/org-web-tools>).

```emacs-lisp
(use-package! org-web-tools
  :bind
  ("C-c i l" . org-web-tools-insert-link-for-url))
```


### Pocket {#pocket}

あとで読むサービス.

```emacs-lisp
(global-set-key (kbd "C-x w p") 'pocket-reader)
(use-package! pocket-reader
  :bind
  ("C-x w l" . pocker-reader-add-link)
  :config
  (setq pocket-reader-open-url-default-function #'eww)
  (setq pocket-reader-pop-to-url-default-function #'eww))
```


### RSS(Elfeed) {#rss--elfeed}

```emacs-lisp
;; elfeed
(global-set-key (kbd "C-x w w") 'elfeed)
(use-package! elfeed
  :config
  (setq elfeed-feeds
        '(
          ("https://yuchrszk.blogspot.com/feeds/posts/default" blog) ; パレオな男
          ("https://www.youtube.com/feeds/videos.xml?channel_id=UCFo4kqllbcQ4nV83WCyraiw" youtube) ; 中田敦彦
          ("https://www.youtube.com/feeds/videos.xml?channel_id=UCFdBehO71GQaIom4WfVeGSw" youtube) ;メンタリストDaiGo
          ("https://www.youtube.com/feeds/videos.xml?playlist_id=PL3N_SB4Wr_S2cGYuI02bdb4UN9XTZRNDu" youtube) ; 与沢の流儀
          ("http://www.aaronsw.com/2002/feeds/pgessays.rss" blog) ; Paul Graham
          ))
  (setq-default elfeed-search-filter "@1-week-ago +unread ")
  (defun elfeed-search-format-date (date)
    (format-time-string "%Y-%m-%d %H:%M" (seconds-to-time date)))
  )
```


### Habitica {#habitica}

```emacs-lisp
(use-package! habitica
  :commands habitica-tasks
  :init
  (bind-key "C-x t g" 'habitica-tasks)
  :config
  (setq habitica-show-streak t)
  (setq habitica-turn-on-highlighting nil))
```


## Checkers {#checkers}

```emacs-lisp
;; Checkers
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;

```


## Completion {#completion}

```emacs-lisp
;; Completion
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
(use-package! avy
  :bind
  ("M-g c" . avy-goto-char) ;; doom の keybind 上書き.
  ("M-g l" . avy-goto-line) ;; doom の keybind 上書き.
  ("M-g g". avy-goto-word-1))

;; うまく動かないので封印 doom との相性が悪いのかも.
;; ひとまず migemo したいときは isearch で対応.
;; (use-package! avy-migemo
;;  :after migemo
;;  :bind
;;  ("M-g m m" . avy-migemo-mode)
;;  ("M-g c" . avy-migemo-goto-char-timer) ;; doom の keybind 上書き.
;;  :config
;;  (avy-migemo-mode 1)
;;  (setq avy-timeout-seconds nil))

(use-package! swiper
  :bind
;  ("C-s" . swiper) ;; migemo とうまく連携しないので isearch 置き換えを保留. C-c s s で swiper 起動.
  :config
  (ivy-mode 1))

;; avy-migemo-e.g.swiper だけバクる
;; https://github.com/abo-abo/swiper/issues/2249
;;(after! avy-migemo
;;  (require 'avy-migemo-e.g.swiper))

;; org-roam の completion-at-point が動作しないのはこいつかな...
;; (add-hook! 'org-mode-hook (company-mode -1))
;; company はなにげに使いそうだからな，TAB でのみ補完発動させるか.
(setq company-idle-delay nil)
(global-set-key (kbd "TAB") #'company-indent-or-complete-common)
```


### affe {#affe}

fuzzy find. あいまい検索 for consult.

<https://github.com/minad/affe>

```emacs-lisp
(use-package! affe
  :after consult
  :config
  (defun affe-orderless-regexp-compiler (input _type)
    (setq input (orderless-pattern-compiler input))
    (cons input (lambda (str) (orderless--highlight input str))))
  (setq affe-regexp-compiler #'affe-orderless-regexp-compiler))
```


### all-the-icons-completion {#all-the-icons-completion}

<https://github.com/iyefrat/all-the-icons-completion>

```emacs-lisp
(use-package! all-the-icons-completion
  :init
  (all-the-icons-completion-mode))
(add-hook! marginalia-mode-hook #'all-the-icons-completion-marginalia-setup)
```


## Config {#config}

```emacs-lisp
;; Config
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
;;
;; doom specific config
;; (setq user-full-name "John Doe"
;;      user-mail-address "john@doe.com")
(setq confirm-kill-emacs nil) ; 終了時の確認はしない.

;; フルスクリーンで Emacs 起動
;; ブラウザと並べて表示することが多くなったのでいったんマスク
;; (add-to-list 'initial-frame-alist '(fullscreen . maximized))

;; This is to use pdf-tools instead of doc-viewer
(use-package! pdf-tools
  :config
  (pdf-tools-install)
  ;; This means that pdfs are fitted to width by default when you open them
  (setq-default pdf-view-display-size 'fit-width)
  :custom
  (pdf-annot-activate-created-annotations t "automatically annotate highlights"))
```


## Editor {#editor}

```emacs-lisp
;; Editor
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;

;; 英数字と日本語の間にスペースをいれる.
(use-package! pangu-spacing
  :config
  (global-pangu-spacing-mode 1)
  ;; 保存時に自動的にスペースを入れるのを抑止.あくまで入力時にしておく.
  (setq pangu-spacing-real-insert-separtor nil))

;; 記号の前後にスペースを入れる.
(use-package! electric-operator)
(add-hook! 'org-mode-hook #'electric-operator-mode)
```


### 改行(newline)と折り返し(wrap) {#改行--newline--と折り返し--wrap}

まず改行(newline)と折り返し(wrap)の２つの概念があることに注意.

方針として自動改行は無効, 自動折り返しは許す.

auto-fill-modeで自動改行される. これは無効にする.

追記: 方針変更. コードではauto-fillを許す. そして単に(auto-fill-mode -1)をところでmodeのhookによって再度有効になる気がする.

```emacs-lisp
;; (auto-fill-mode -1)
```

問題はMarkdownやOrg-modeでautl-fillが発動して改行されるところ. org-modeで再度hookが走り有効になる気がするのでコレで息を止める.

->息が止まらないので諦めた. いくら無効にしてもorg-mode-hookの延長でauto-fill-modeをonにしてしまう人がいる. そしてその犯人が誰か２時間追求しても結局わからない. Doom Emacsの設定の仕業はある.

```emacs-lisp
(auto-fill-mode -1)
(remove-hook 'org-mode-hook #'auto-fill-mode)
;; (remove-hook 'org-mode-hook #'turn-on-auto-fill)
;; (remove-hook 'text-mode-hook #'auto-fill-mode)
;; (remove-hook 'text-mode-hook #'turn-on-auto-fill)
;; (add-hook 'org-mode-hook #'turn-off-auto-fill)
;; (add-hook 'text-mode-hook #'turn-off-auto-fill)
;; (add-hook 'org-roam-mode-hook #'turn-off-auto-fill)
```

これによって折り返しの限界を80から99999にすることにして回避する.

```emacs-lisp
(setq-default fill-column 99999)
(setq fill-column 99999)
```

これにより折り返しで / や $ 記号が表示される. 以下の設定で消す.

```emacs-lisp
;; / を削除
(set-display-table-slot standard-display-table 'wrap ?\ )
;; $ を削除
(set-display-table-slot standard-display-table 0 ?\ )
```

さらに折り返しの次のラインにインデントが挿入される. これはelectric-indent-modeの仕業. 現在org-modeのみで無効中.

折り返しoff/onは, M-x toggle-truncate-linesで切り替えることができる.


### visual-line-mode {#visual-line-mode}

単語単位での折り返しをするEmacs標準実装のモード.

Emacsはウィンドウの右端の近くの単語の境界で折り返すよう試みる. これは単語の途中で折り返さないことにより可読性を高めるため.

<https://ayatakesi.github.io/emacs/25.1/Visual-Line-Mode.html>

この設定はスクリーンの幅によって判定されるためたとえば文字列80で折り返すとかではない.

日本語と英語が入り交じるときの解釈が変なので以下を設定した.

```emacs-lisp
(setq word-wrap-by-category t)
```

ref: [Word-wrap problem with Chinese or Japanese characters : emacs](https://www.reddit.com/r/emacs/comments/ov2s2r/wordwrap_problem_with_chinese_or_japanese/h76ipjy/)


### visual-fill-column {#visual-fill-column}

Doomだといらないかもだけど.

```emacs-lisp
;; (add-hook! visual-line-mode 'visual-fill-column-mode)
```

-> perfect-marginとの相性が悪い気がするのでいったん無効.

-   ref.
    -   [memo: Emacs の visual-fill-column.el が便利だった](http://sleepboy-zzz.blogspot.com/2015/12/emacs-visual-fill-columnel_29.html)


### perfect-margin {#perfect-margin}

いい感じにmarginをとってくれる (<https://github.com/mpwang/perfect-margin>)

```emacs-lisp
(use-package! perfect-margin
  :config
  (perfect-margin-mode 1))
```


### ターミナルの縦分割線をUTF-8できれいに描く {#ターミナルの縦分割線をutf-8できれいに描く}

ref: [How do I make the vertical window divider more pretty? : emacs](https://www.reddit.com/r/emacs/comments/3u0d0u/how_do_i_make_the_vertical_window_divider_more/)

```emacs-lisp
(unless (display-graphic-p)
  ;; ターミナルの縦分割線をUTF-8できれいに描く
  (defun my-change-window-divider ()
    (interactive)
    (let ((display-table (or buffer-display-table
           standard-display-table
           (make-display-table))))
      (set-display-table-slot display-table 5 ?│)
      (set-window-display-table (selected-window) display-table)))
  (add-hook 'window-configuration-change-hook 'my-change-window-divider))
```


### whitespace {#whitespace}

余分な空白/タブに色づけ.

```emacs-lisp
(use-package! whitespace
  :config
  ;; limit lie length -> display-fill-column-indicator-modeを使うためマスク.
  ;; (setq whitespace-line-column 80)
  (setq whitespace-style '(face
                           ;;lines-tail
                           ))
  ;; 全角スペースを可視化
  (setq whitespace-space-regexp "\\(\u3000+\\)")
  (global-whitespace-mode 1))
```


### display-fill-column-indicator-mode {#display-fill-column-indicator-mode}

Emacsの画面に1行80文字のところに線を薄く引く.

プログラミングの世界では昔から80 columns ruleがあり, Emacsで80文字目を表示する機能もいろいろあったものの, Emacs 27.0.90からdefault機能として提供されるようになった.

(最も80charは昔の話で, 最近のディスプレイの大きさだと100charがいいという議論もある).

今つかっているモニタで縦に３分割すると74がちょうどいいことがわかった. (先頭に行番号表示4char+1charのmarginあり).

```emacs-lisp
(setq-default display-fill-column-indicator-column 74)
(global-display-fill-column-indicator-mode)
```


## Emacs {#emacs}

```emacs-lisp
;; Emacs
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
(pixel-scroll-precision-mode)

;; doomだとhelpが割り当てられていたがdoomのhelpはF1をつかう.

(global-set-key (kbd "C-h") 'backward-delete-char)
(global-set-key (kbd "C-c h r") 'doom/reload)

;; Emacs起動時にいちいち質問されるのはうざい.
;; default tではなぜか無視できないので:allを設定しておく.
(setq enable-local-variables :all)
```


### ace-window {#ace-window}

-   3つ以上のwindowの選択が番号でできる. defaultでC-x oを上書きしてる?
-   C-u C-x o だとwindowをswapできる(ace-swap-window).


## Email {#email}

```emacs-lisp
;; Email
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;

```


## Input {#input}

```emacs-lisp
;; Input
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
(set-language-environment "Japanese")
(prefer-coding-system 'utf-8)
(set-default 'buffer-filecoding-system 'utf-8)

;; migemo
(use-package! migemo
  :config
  (setq migemo-command "cmigemo")
  (setq migemo-options '("-q" "--emacs" "-i" "\a"))
  (setq migemo-dictionary "/usr/share/migemo/utf-8/migemo-dict")
  (setq migemo-user-dictionary nil)
  (setq migemo-regex-dictionary nil)
  (setq migemo-coding-system 'utf-8-unix)
  (migemo-init))
```


### fcitx {#fcitx}

```emacs-lisp
(use-package! fcitx
  :config
  (setq fcitx-remote-command "fcitx5-remote")
  (fcitx-aggressive-setup)
  ;; Linux なら t が推奨されるものの、fcitx5 には未対応なためここは nil
  (setq fcitx-use-dbus nil))
```


### artist mode {#artist-mode}

[EmacsWiki: Artist Mode](https://www.emacswiki.org/emacs/ArtistMode)

Emacs上でカーソルやマウスを使って線が書ける.

-   M-x artist-modeで起動.
-   C-c C-c で終了.
-   defaultでは **.** を描写, Shiftで **-** になる.

昔なんちゃってelispを書いたけど, なんだdefaultであったのか.

ref: [秀丸のような罫線マクロないかなと思ってelisp作成した | Futurismo](https://futurismo.biz/archives/1972/)


## Lang {#lang}

編集補助の中でも特にコーディング支援をまとめる.


### Generals {#generals}

言語に依存しないコーディング支援ツール.


#### smartparens {#smartparens}

<https://github.com/Fuco1/smartparens>

Emacsでカッコの対応を取りつつ編集をするminor-mode. pareditを新しくrewriteした.

refs:

-   <https://ebzzry.com/en/emacs-pairs/>
-   <http://kimi.im/2021-11-27-sexp-operations-in-emacs>

[doom emacsのsmartparens定義](https://github.com/hlissner/doom-emacs/blob/master/modules/config/default/%2Bemacs-bindings.el). +bindings +smartparensで有効.

```emacs-lisp
;;; smartparens
(:after smartparens
  :map smartparens-mode-map
  "C-M-a"           #'sp-beginning-of-sexp
  "C-M-e"           #'sp-end-of-sexp
  "C-M-f"           #'sp-forward-sexp
  "C-M-b"           #'sp-backward-sexp
  "C-M-n"           #'sp-next-sexp
  "C-M-p"           #'sp-previous-sexp
  "C-M-u"           #'sp-up-sexp
  "C-M-d"           #'sp-down-sexp
  "C-M-k"           #'sp-kill-sexp
  "C-M-t"           #'sp-transpose-sexp
  "C-M-<backspace>" #'sp-splice-sexp)
```

足りないのは自分で定義する必要あり. というかいろいろ再定義するか...

```emacs-lisp
(use-package! smartparens-config
  :bind
  ("C-<right>" . sp-forward-slurp-sexp)
  ("M-<right>" . sp-forward-barf-sexp)
  ("C-<left>"  . sp-backward-slurp-sexp)
  ("M-<left>"  . sp-backward-barf-sexp)
  ("C-M-w" . sp-copy-sexp)
  ("M-[" . sp-backward-unwrap-sexp)
  ("M-]" . sp-unwrap-sexp)
  :config
  (add-hook! 'clojure-mode-hook 'smartparens-strict-mode))
```


#### symbol-overlay {#symbol-overlay}

シンボルのハイライトをキー入力で制御できる.

<https://github.com/wolray/symbol-overlay/>

使ってないし companyとkeybindがかぶったのでいったん封印.

```emacs-lisp
(use-package! symbol-overlay
  :config
  (global-set-key (kbd "M-i") 'symbol-overlay-put)
  (global-set-key (kbd "M-n") 'symbol-overlay-switch-forward)
  (global-set-key (kbd "M-p") 'symbol-overlay-switch-backward)
  (global-set-key (kbd "<f7>") 'symbol-overlay-mode)
  (global-set-key (kbd "<f8>") 'symbol-overlay-remove-all))
```


#### codic {#codic}

よい変数名を教えてくれるwebサービスcodicクライアント.

[codic - プログラマーのためのネーミング辞書](https://codic.jp/)

-   M-x codic: 英語 => 日本語
-   M-x codic-translate => 日本語 => 英語(要token)

codic-translateを使うにはtokenを codic-api-tokenに設定する必要がある.
現状は"private/config.el"に書いて読み込んでいる.

```emacs-lisp
(use-package! codic)
```

-   [codic - GitHub](https://github.com/emacsorphanage/codic)
-   [英語力を向上させたいのでまずは Emacs からはじめた | Futurismo](https://futurismo.biz/archives/2538/)


### Clojure {#clojure}

ref: [doom-emacs/README.org - GitHub](https://github.com/hlissner/doom-emacs/blob/develop/modules/lang/clojure/README.org)

とりあえず，doomのclojureモジュール有効.

-   cider
-   clj-refactor
-   flycheck-clj-kondo

その他，

-   rainbow-delimiters, smartparensはdoomのcoreパッケージとしてすでにはいっている.
-   pereditはciderの中に入っている.

<!--listend-->

```emacs-lisp
;; やりすぎindent mode
(add-hook! 'clojure-mode-hook 'aggressive-indent-mode)
;; 自動でalign整形.
(setq clojure-align-forms-automatically t)

(use-package! cider
  :bind
  ;; desing journal用にbinding追加
  ("C-c C-v C-p" . cider-pprint-eval-defun-to-comment)
  ("C-c C-v M-p" . cider-pprint-eval-last-sexp-to-comment)
  :config
  ;; connectとともにREPL bufferを表示.
  (setq  cider-repl-pop-to-buffer-on-connect t)
  ;; replに 出力しすぎてEmacsがハングするのを防ぐ.
  (setq  cider-repl-buffer-size-limit 100)

  ;; companyでのあいまい補完.
  (add-hook 'cider-repl-mode-hook #'cider-company-enable-fuzzy-completion)
  (add-hook 'cider-mode-hook #'cider-company-enable-fuzzy-completion)

  ;; stack-frame表示をプロジェクトに限定
  (setq cider-stacktrace-default-filters '(project))

  ;; cider-connectで固定portを選択候補に表示.
  ;; 固定port自体は tools.depsからのnrepl起動時optionで指定.
  (setq cider-known-endpoints '(("kotori" "0.0.0.0" "34331")))
)
```


#### clj-refactor {#clj-refactor}

Emacs CIDERでClojureを書くための便利なファクタツール提供.

<https://github.com/clojure-emacs/clj-refactor.el>

```emacs-lisp
(add-hook! clojure-mode
  (clj-refactor-mode 1)
  (yas-minor-mode 1) ; for adding require/use/import statements
  ;; This choice of keybinding leaves cider-macroexpand-1 unbound
  (cljr-add-keybindings-with-prefix "C-c C-m"))
```

-   cljr-clean-nsでnamespaceを整理, cljr-project-cleanでプロジェクト全体に適用.


#### cljstyle: formatter for Clojure {#cljstyle-formatter-for-clojure}

ref: [GitHub](https://qiita.com/lagenorhynque/items/a5d83b4a36a1cf1cacbe)

Doom Emascの editor/format moduleと連携可能.
Clojureだとdefaultが node-cljfmtなのでcljstyleを使うには設定が必要.

```emacs-lisp
(add-hook! clojure-mode
  (set-formatter! 'cljstyle "cljstyle pipe" :modes '(clojure-mode))
  (add-hook 'before-save-hook 'format-all-buffer t t))
```


#### clj-kondo: linter for Clojure {#clj-kondo-linter-for-clojure}

ref: [GitHub](https://qiita.com/lagenorhynque/items/dd9d6a1d97cbea738bc0)


#### portal {#portal}

Data Visualization for Clojure.

ref. <https://github.com/djblue/portal>

```emacs-lisp
(defun portal.api/open ()
  (interactive)
  (cider-nrepl-sync-request:eval
   "(require 'portal.api) (portal.api/tap) (portal.api/open)"))

(defun portal.api/clear ()
  (interactive)
  (cider-nrepl-sync-request:eval "(portal.api/clear)"))

(defun portal.api/close ()
  (interactive)
  (cider-nrepl-sync-request:eval "(portal.api/close)"))
```


### rest {#rest}

```emacs-lisp
(use-package! restclient
  :mode (("\\.rest\\'" . restclient-mode)
         ("\\.restclient\\'" . restclient-mode)))
(use-package! ob-restclient
  :after org restclient
  :init
  (org-babel-do-load-languages
   'org-babel-load-languages
   '((restclient . t))))
```


## Os {#os}

```emacs-lisp
;; OS
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
```


### EXWM {#exwm}

EmacsのWindow Manager.

もはやこれをつかうと世界がEmacsになりEmacs 引きこもり生活が完成する.

```emacs-lisp
(use-package! exwm
  :after counsel
  :init
  (setq counsel-linux-app-format-function
        #'counsel-linux-app-format-function-name-only)
  (map!
        :leader
        :prefix ("z" . "exwm")
        "c" #'exwm-reset
        "o" (lambda (command)
                         (interactive (list (read-shell-command "$ ")))
                         (start-process-shell-command command nil command))
        "z" #'exwm-workspace-switch
        "m" #'exwm-workspace-move-window
        "a" #'counsel-linux-app
        "s" #'counsel-search  ;; open chrome and search
        )
  (add-hook 'exwm-input--input-mode-change-hook
            'force-mode-line-update)
  (add-hook 'exwm-update-class-hook
            (lambda ()
              (exwm-workspace-rename-buffer exwm-class-name)))
  ;; どうもChromeを立ち上げるとハングするので無効にしておく.
  (winner-mode -1)

  :config
  (require 'exwm-randr)
  (setq exwm-randr-workspace-output-plist '(0 "HDMI-1"))
  (add-hook
   'exwm-randr-screen-change-hook
   (lambda ()
     (start-process-shell-command
      "xrandr" nil "xrandr --output HDMI-1 --primary --right-of eDP-1 --auto")))
  (exwm-randr-enable)

  (require 'exwm-systemtray)
  (exwm-systemtray-enable)

  ;; edit-server的な. C-c 'で編集できるのでよりbetter
  ;; 一度入力したものを再度開くと文字化けする.
  (require 'exwm-edit)
  (setq exwm-edit-split t)

  (setf epg-pinentry-mode 'loopback)
  (defun pinentry-emacs (desc prompt ok error)
    (let ((str (read-passwd
                (concat (replace-regexp-in-string
                         "%22" "\""
                         (replace-regexp-in-string
                          "%0A" "\n" desc)) prompt ": "))))
      str))

  ;; from https://github.com/ch11ng/exwm/wiki/Configuration-Example
  (menu-bar-mode -1)
  (tool-bar-mode -1)
  (scroll-bar-mode -1)
  (fringe-mode 1)

  ;; google-chromeを起動するとmouse on menu-barがpopupしてハングする対策
  ;; https://stackoverflow.com/questions/17280845/emacs-disable-pop-up-menus-on-mouse-clicks
  (fset 'menu-bar-open nil)
  (fset 'x-menu-bar-open nil)

  ;; Turn on `display-time-mode' if you don't use an external bar.
  (setq display-time-default-load-average nil)
  (display-time-mode t)
  (display-battery-mode 1)

  (setq exwm-workspace-number 2)

  (setq exwm-input-simulation-keys
        '(([?\C-b] . [left])
          ;; Chromeページ内検索のために空ける
          ;; ([?\C-f] . [right])
          ;; 2022.03.23 やっぱり解除. どうもC-fがスムーズな操作を阻害する.
          ;; ページ内検索はSurfingkeysというExtensionを利用(/).
          ([?\C-f] . [right])
          ([?\C-p] . [up])
          ([?\C-n] . [down])
          ([?\C-a] . [home])
          ([?\C-e] . [end])
          ([?\M-v] . [prior])
          ([?\C-v] . [next])
          ([?\C-d] . [delete])
          ([?\C-m] . [return])
          ([?\C-h] . [backspace])
          ([?\C-k] . [S-end delete])))

  (exwm-enable))
```


## Org-mode {#org-mode}

ご存知！

-   [doom-emacs/README.org at develop · hlissner/doom-emacs · GitHub](https://github.com/hlissner/doom-emacs/blob/develop/modules/lang/org/README.org)
    -
-   [dotfiles/50_org-mode.org at master · tsu-nera/dotfiles · GitHub](https://github.com/tsu-nera/dotfiles/blob/master/.emacs.d/inits/50_org-mode.org)
    -   昔の設定. すこしずつ移植したい.

<!--listend-->

```emacs-lisp
;; Org mode
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;

;; スマホとの共有のため, github を clone したものを Dropbox に置いて$HOME に symlink している.
(after! org
  (setq org-directory "~/keido")
  (setq org-default-notes-file "gtd/gtd_projects.org")

  (setq org-return-follows-link t) ;; Enter でリンク先へジャンプ
  (setq org-use-speed-commands t)  ;; bullet にカーソルがあると高速移動
  (setq org-hide-emphasis-markers t) ;; * を消して表示.
  (setq org-pretty-entities t)

  (setq org-footnote-section "Notes") ;; defaultではFootnotesなので変える.
  (setq org-footnote-auto-adjust t)

  ;; M-RET の挙動の調整
  ;; t だと subtree の最終行に heading を挿入, nil だと current point に挿入
  ;; なお，C-RET だと subtree の最終行に挿入され, C-S-RET だと手前に挿入される.
  (setq org-insert-heading-respect-content nil)

  (setq org-startup-indented t)
  (setq org-indent-mode-turns-on-hiding-stars nil)

  (setq org-startup-folded 'show2levels);; 見出しの階層指定
  (setq org-startup-truncated nil) ;; 長い文は折り返す.

  ;; electric-indent は org-mode で誤作動の可能性があることのこと
  ;; たまにいきなり org-mode の tree 構造が壊れるから，とりあえず設定しておく.
  ;; この設定の効果が以下の記事で gif である.
  ;; https://www.philnewton.net/blog/electric-indent-with-org-mode/
  (add-hook! org-mode (electric-indent-local-mode -1))

  ;; org-agenda
  (setq org-refile-targets '((org-agenda-files :maxlevel . 3)))
  (setq org-agenda-time-leading-zero t) ;; 時間表示が 1 桁の時, 0 をつける
  (setq calendar-holidays nil) ;; 祝日を利用しない.
  (setq org-log-done 'time);; 変更時の終了時刻記録.

  ;; スケジュールやデッドラインアイテムは DONE になっていれば表示する
  (setq org-agenda-skip-deadline-if-done nil)
  (setq org-agenda-skip-scheduled-if-done nil)

  (setq org-agenda-include-inactive-timestamps t) ;; default で logbook を表示
  (setq org-agenda-start-with-log-mode t) ;; ;; default で 時間を表示

  ;; org-agenda speedup tips
  ;; https://orgmode.org/worg/agenda-optimization.html

  ;; 何でもかんでも agenda すると思いので厳選.
  (setq org-agenda-files '("~/Dropbox/keido/notes/gtd/gtd_projects.org"
                           "~/Dropbox/keido/notes/journals/journal.org"))
                           ;; projectsディレクトリにある.orgをみる.
                           ;; その配下のorgファイルは対象にはならない.
                           ;; "~/Dropbox/keido/notes/gtd/projects")

  ;; 期間を限定
  (setq org-agenda-span 7)
                                        ; Inhibit the dimming of blocked tasks:
  (setq org-agenda-dim-blocked-tasks nil)
  ;; Inhibit agenda files startup options:
  (setq org-agenda-inhibit-startup nil)
  ;; Disable tag inheritance in agenda:
  (setq org-agenda-use-tag-inheritance nil)

  )

;; org-mode で timestamp のみを挿入するカスタム関数(hh:mm)
(after! org
  (defun my/insert-timestamp ()
    "Insert time stamp."
    (interactive)
    (insert (format-time-string "%H:%M")))
  (map! :map org-mode-map "C-c C-." #'my/insert-timestamp))

;; +pretty(org-superstar-mode)関連
;;; Titles and Sections
;; hide #+TITLE:
;; (setq org-hidden-keywords '(title))
;; set basic title font
;; (set-face-attribute 'org-level-8 nil :weight 'bold :inherit 'default)
;; Low levels are unimportant => no scaling
;; (set-face-attribute 'org-level-7 nil :inherit 'org-level-8)
;; (set-face-attribute 'org-level-6 nil :inherit 'org-level-8)
;; (set-face-attribute 'org-level-5 nil :inherit 'org-level-8)
;; (set-face-attribute 'org-level-4 nil :inherit 'org-level-8)
;; Top ones get scaled the same as in LaTeX (\large, \Large, \LARGE)
;; (set-face-attribute 'org-level-3 nil :inherit 'org-level-8 :height 1.2) ;\large
;; (set-face-attribute 'org-level-2 nil :inherit 'org-level-8 :height 1.44) ;\Large
;; (set-face-attribute 'org-level-1 nil :inherit 'org-level-8 :height 1.728) ;\LARGE
;; Only use the first 4 styles and do not cycle.
(setq org-cycle-level-faces nil)
(setq org-n-level-faces 4)
;; Document Title, (\huge)
;; (set-face-attribute 'org-document-title nil
;;                    :height 2.074
;;                    :foreground 'unspecified
;;                    :inherit 'org-level-8)

;; (with-eval-after-load 'org-superstar
;;  (set-face-attribute 'org-superstar-item nil :height 1.2)
;;  (set-face-attribute 'org-superstar-header-bullet nil :height 1.2)
;;  (set-face-attribute 'org-superstar-leading nil :height 1.3))
;; Set different bullets, with one getting a terminal fallback.
(setq org-superstar-headline-bullets-list '("■" "◆" "●" "▷"))
;; (setq org-superstar-special-todo-items t)

;; Stop cycling bullets to emphasize hierarchy of headlines.
(setq org-superstar-cycle-headline-bullets nil)
;; Hide away leading stars on terminal.
;; (setq org-superstar-leading-fallback ?\s)
(setq inhibit-compacting-font-caches t)

;; 読書のためのマーカー（仮）
;; あとでちゃんと検討と朝鮮しよう.
;; (setq org-emphasis-alist
;;   '(("*" bold)
;;     ("/" italic)
;;     ("_" underline))
;;     ("=" (:background "red" :foreground "white")) ;; 書き手の主張
;;     ("~" (:background "blue" :foreground "white")) cddddd;; 根拠
;;     ("+" (:background "green" :foreground "black")))) ;; 自分の考え

```


### org-capture {#org-capture}

<https://orgmode.org/manual/Capture-templates.html>

```emacs-lisp
(after! org
  (defun my/create-timestamped-org-file (path)
    (expand-file-name (format "%s.org" (format-time-string "%Y%m%d%H%M%S")) path))
  (defun my/create-date-org-file (path)
    (expand-file-name (format "%s.org" (format-time-string "%Y-%m-%d")) path))

  (defconst my/captured-notes-file "~/keido/inbox/inbox.org")

  (setq org-capture-templates
        '(("i" "📥 Inbox" entry
           (file "~/keido/inbox/inbox.org") "* %?\nCaptured On: %U\n"
           :klll-buffer t)
          ("I" "📥+🌐 Inbox+Browser" entry
           (file "~/keido/inbox/inbox.org")
           "* %?\nSource: [[%:link][%:description]]\nCaptured On: %U\n"
           :klll-buffer t)
          ("q" "📥+🌐 Inbox+Browser(quote)" entry
           (file "~/keido/inbox/inbox.org")
           "* %?\nSource: [[%:link][%:description]]\nCaptured On: %U\n%i\n"
           :klll-buffer t)
          ("c" "☑ Planning" plain
           (file+headline (lambda () (my/create-date-org-file "~/keido/notes/journals/daily"))
                          "Planning")
           "%?"
           :unnarrowed t
           :kill-buffer t)
          ("t" "🤔 Thought" entry
           (file+headline (lambda () (my/create-date-org-file "~/keido/notes/journals/daily"))
                          "Thoughts")
           "* 🤔 %?\n%T"
           :empty-lines 1
           :unnarrowed t
           :kill-buffer t)
          ("T" "🤔+📃 Thought+Ref" entry
           (file+headline (lambda () (my/create-date-org-file "~/keido/notes/journals/daily"))
                          "Thoughts")
           "* 🤔 %?\n%T from %a\n"
           :empty-lines 1
           :unnarrowed t
           :kill-buffer t)
          ("l" "🤔+🌐 Thought+Browser" entry
           (file+headline (lambda () (my/create-date-org-file "~/keido/notes/journals/daily"))
                          "Thoughts")
             "* 🤔 %?\n%T from [[%:link][%:description]]\n"
           :empty-lines 1
           :unnarrowed t
           :kill-buffer t)
          ("p" "🍅 Pomodoro" entry
           (file+headline (lambda () (my/create-date-org-file "~/keido/notes/journals/daily"))
                          "DeepWork")
           "* 🍅 %?\n%T"
           :empty-lines 1
           :unnarrowed t
           :kill-buffer t)
          ("j" "🖊 Journal" plain
           (file (lambda () (my/create-date-org-file "~/keido/notes/journals/daily")))
           "%?"
           :empty-lines 1
           :unnarrowed t
           :kill-buffer t)
          ("J" "🖊+📃 Journal+Ref" plain
           (file (lambda () (my/create-date-org-file "~/keido/notes/journals/daily")))
           "%?\n%a"
           :empty-lines 1
           :unnarrowed t
           :kill-buffer t)
          ("L" "🖊+🌐 Journal+Browser" plain
           (file (lambda () (my/create-date-org-file "~/keido/notes/journals/daily")))
             "%?\nSource: [[%:link][%:description]]\nCaptured On: %U\n"
           :empty-lines 1
           :unnrrowed t
           :kill-buffer t)))
)
```


#### Google Chrome Extention: Org Capture {#google-chrome-extention-org-capture}

Google Chromeにを入れることでWeb Pageがorg-captureと連携([link](https://chrome.google.com/webstore/detail/org-capture/kkkjlfejijcjgjllecmnejhogpbcigdc?hl=ja)).

ChromeでCtrl + Shift + Lで起動.


### org-babel {#org-babel}

Org-modeのなかでLiterature Programming.

基本操作:

-   C-c C-, コードブロックの挿入テンプレート呼び出し(org-insert-structure-tempate)
-   C-c C-c コード実行(org-babel-execute-src-block)
-   C-c C-o コード実行結果を開く(org-babel-open-src-block-result)
-   C-c ' ソースコード編集(org-edit-src-code)
    -   どうもEoom Emacsだと keybindingが外れいてる.
    -   C-c l '(org-edit-special)で開く.

<!--listend-->

```emacs-lisp
(after! org
  ;; https://stackoverflow.com/questions/53469017/org-mode-source-editing-indents-code-after-exiting-source-code-block-editor
  ;; インデント. default 2になっているとへんな隙間が先頭に入る.
  (setq org-edit-src-content-indentation 0)
  (setq org-src-preserve-indentation t)
  ;; TABの挙動
  (setq org-src-tab-acts-natively t)
  ;; org-babel のソースをキレイに表示.
  (setq org-src-fontify-natively t)
  (setq org-fontify-whole-heading-line t)

  ;; 評価でいちいち質問されないように.
  (setq org-confirm-babel-evaluate nil)

  ;; org-babel で 実行した言語を書く. デフォルトでは emacs-lisp だけ.
  (org-babel-do-load-languages
   'org-babel-load-languages
   '((lisp . t)
     (shell . t)
     (clojure . t)))
  (org-defkey org-mode-map "\C-u\C-x\C-e" 'cider-eval-last-sexp)
)
```

refs:

-   [org-babel Key bindings and Useful Functions (The Org Manual)](https://orgmode.org/manual/Key-bindings-and-Useful-Functions.html)
-   [org-modeのコードブロック(Babel)の使い方 | Misohena Blog](https://misohena.jp/blog/2017-10-26-how-to-use-code-block-of-emacs-org-mode.html)


### org-export {#org-export}

Org-modeのファイルをエクスポートする機能.

サブパッケージが数多くあるが, ここでは共通情報まとめ.

org-export-with-xxxという設定項目でいろいろ制御できる.

[Export Settings (The Org Manual)](https://orgmode.org/manual/Export-Settings.html)

しかし, 以下が自動的に変換されてしまう...この文字に対する制御方法が見つからない...

-   > &gt;
-   < &lt;
-   & &amp;

どうもHTML tagとかHTML Entitiesと呼ばれている(ref. [The Org Manual](https://orgmode.org/org.html#Headlines-in-HTML-export)).

> The HTML export back-end transforms ‘<’ and ‘>’ to ‘&lt;’ and ‘&gt;’.

ただox-html.elにはこういう設定がdefaultでされている. 他のexportへの移植が必要.

```emacs-lisp
(setq org-export-html-protect-char-alist
  '(("&" . "&amp;")
    ("<" . "&lt;")
    (">" . "&gt;"))
```

[Advanced Export Configuration (The Org Manual)](https://orgmode.org/manual/Advanced-Export-Configuration.html)

おそらく, exportをかけたあとにhook関数によって文字列変換が必要.

```emacs-lisp
(defun my-hugo-filter-html-amp (text backend info)
  (when (org-export-derived-backend-p backend 'hugo)
    (replace-regexp-in-string "&amp;" "&" text)))
(defun my-hugo-filter-html-gt (text backend info)
  (when (org-export-derived-backend-p backend 'hugo)
    (replace-regexp-in-string "&gt;" ">" text)))
(defun my-hugo-filter-html-lt (text backend info)
  (when (org-export-derived-backend-p backend 'hugo)
    (replace-regexp-in-string "&lt;" "<" text)))
(add-to-list
'org-export-filter-plain-text-functions 'my-hugo-filter-html-amp)
(add-to-list
'org-export-filter-plain-text-functions 'my-hugo-filter-html-gt)
(add-to-list
'org-export-filter-plain-text-functions 'my-hugo-filter-html-lt)
```


### ox-hugo {#ox-hugo}

Org-modeで書いたブログ記事をHugoにあったMarkdown形式に変換する.

ブログFuturismoはOrg-modeで執筆してこれを利用してMarkdownに変換している.

```emacs-lisp
(use-package! ox-hugo
  :after 'ox
  :config
  ;; なんか.dir-locals.elに書いても反映してくれないな. ココに書いとく.
  (setq org-export-with-author nil))
```

このox-hugoで出力されるMarkdownはどうもリスト表示でスペースが4つ入ってしまう. GitHub Favorite Markdownのようにリストでのスペース２であって欲しいものの解決方法が見つからない.


### ox-rst {#ox-rst}

Org-modeで書いたWiki用のページをSphinxで公開するためにreST形式に変換する.

リンク形式がうまく変換できないのでけっこう強引に変換している(もう少しうまく改善したい).

```emacs-lisp
(use-package! ox-rst
  :after 'ox)

(after! ox
  (defun my/rst-to-sphinx-link-format (text backend info)
    (when (and (org-export-derived-backend-p backend 'rst) (not (search "<http" text)))
      (replace-regexp-in-string "\\(\\.org>`_\\)" ">`" (concat ":doc:" text) nil nil 1)))
  (add-to-list 'org-export-filter-link-functions
               'my/rst-to-sphinx-link-format))
```


### ob-html {#ob-html}

[org-modeのコードブロックでHTMLを「実行」する | Misohena Blog](https://misohena.jp/blog/2021-08-03-execute-html-in-org-mode-code-blocks.html)

```emacs-lisp
(use-package! ob-html
  :after org
  :config
  ;; C-c C-o でブラウザで開く.
  (org-babel-html-enable-open-src-block-result-temporary))
```


### org-toggl {#org-toggl}

org-modeをTogglと連携させる.
<https://github.com/mbork/org-toggl>

```emacs-lisp
(use-package! org-toggl
  :after org
  :config
  (setq org-toggl-inherit-toggl-properties t)
  (toggl-get-projects)
  (setq toggl-default-project "GTD")
  (org-toggl-integration-mode))
```


### org-journal {#org-journal}

<https://github.com/bastibe/org-journal>

```emacs-lisp
(use-package! org-journal
  :after org
  :bind
  ("C-c r d n" . org-journal-new-entry)
  ("C-c r d d" . org-journal-open-current-journal-file)
  :custom
  (org-journal-date-prefix "#+TITLE: ✍")
  (org-journal-file-format "%Y-%m-%d.org")
  (org-journal-dir (file-truename "~/keido/notes/journals/daily"))
  (org-journal-date-format "%Y-%m-%d")
  :config
  (setq org-journal-enable-agenda-integration t)
  (defun org-journal-file-header-func (time)
     "Custom function to create journal header."
     (concat
      (pcase org-journal-file-type
        (`daily "#+STARTUP: showeverything"))))
  ;;     ;; (`weekly "#+TITLE: Weekly Journal\n#+STARTUP: folded")
  ;;     ;;(`monthly "#+TITLE: Monthly Journal\n#+STARTUP: folded")
  ;;     ;; (`yearly "#+TITLE: Yearly Journal\n#+STARTUP: folded"))))
  (setq org-journal-file-header 'org-journal-file-header-func)

  ;; org-roamに対応させるためにorg-idを生成
  (defun org-create-new-id-journal ()
    (goto-char (point-min))
    (org-id-get-create)
    (goto-char (point-max)))
  (add-hook 'org-journal-after-header-create-hook 'org-create-new-id-journal)
)
```


### org-roam {#org-roam}

Zettelkasten MethodのOrg-roam実装.

org-roam-dialiesよりもorg-journalを利用する(org-agendaの都合).

```emacs-lisp
;; org-roam
(setq org-roam-directory (file-truename "~/keido/notes"))
(setq org-roam-db-location (file-truename "~/keido/db/org-roam.db"))

(use-package! org-roam
  :after org
  :init
  (setq org-roam-v2-ack t)
  (map!
        :leader
        :prefix ("r" . "org-roam")
        "f" #'org-roam-node-find
        "i" #'org-roam-node-insert
        "l" #'org-roam-buffer-toggle
        "t" #'org-roam-tag-add
        "T" #'org-roam-tag-remove
        "a" #'org-roam-alias-add
        "A" #'org-roam-alias-remove
        "r" #'org-roam-ref-add
        "R" #'org-roam-ref-remove
        "o" #'org-id-get-create
        "u" #'my/org-roam-update
        )
  :custom
  ;;ファイル名を ID にする.
  (org-roam-capture-templates
   '(("z" "🎓 Zettelkasten" plain "%?"
      :target (file+head "zk/%<%Y%m%d%H%M%S>.org"
                         "#+title:🎓${title}\n#+filetags: :CONCEPT:\n")
      :unnarrowed t)
     ("w" "📝 Wiki" plain "%?"
      :target (file+head "zk/%<%Y%m%d%H%M%S>.org"
                         "#+title:📝${title}\n#+filetags: :WIKI:\n")
      :unnarrowed t)
     ("t" "🏷 Tag" plain "%?"
      :target (file+head "zk/%<%Y%m%d%H%M%S>.org"
                         "#+title:List of ${title} (alias 🏷${title}) \n#+filetags: :TAG:\n")
      :unnarrowed t)
     ("i" "📂 TOC" plain "%?"
      :target (file+head "zk/%<%Y%m%d%H%M%S>.org"
                         "#+title:Index of {title} (alias 📂${title})\n#+filetags: :TOC:\n")
      :unnarrowed t)
     ("m" "🏛 MOC" plain "%?"
      :target (file+head "zk/%<%Y%m%d%H%M%S>.org"
                         "#+title:🏛${title} \n#+filetags: :MOC:\n")
      :unnarrowed t)
     ("i" "💡 Issue" plain "%?"
      :target (file+head "zk/%<%Y%m%d%H%M%S>.org"
                         "#+title:💡${title} \n#+filetags: :ISSUE:\n")
      :unnarrowed t)
     ("d" "🗒 DOC" plain "%?"
      :target (file+head "zk/%<%Y%m%d%H%M%S>.org"
                         "#+title:🗒${title}\n#+filetags: :DOC:\n")
      :unnarrowrd t)
     ("f" "🦊 Darkfox" plain "%?"
      :target (file+head "darkfox/%<%Y%m%d%H%M%S>.org"
                         "#+title:🦊${title}\n#+filetags: :DARKFOX:\n")
      :unnarrowed t)
     ("b" "📚 Book" plain
      "%?

- title: %^{title}
- authors: %^{author}
- date: %^{date}
- publisher: %^{publisher}
- url: http://www.amazon.co.jp/dp/%^{isbn}
"
      :target (file+head "zk/%<%Y%m%d%H%M%S>.org"
                         "#+title:📚${title} - ${author}(${date})\n#+filetags: :BOOK:SOURCE:\n")
      :unnarrowed t)
     ("s" "🎙‍ Talk" plain
      "%?

- title: %^{title}
- editor: %^{editor}
- date: %^{date}
- url: %^{url}
"
      :target (file+head "zk/%<%Y%m%d%H%M%S>.org"
                         "#+title:🎙 ${title} - ${editor}(${date})\n#+filetags: :TALK:SOURCE:\n")
      :unnarrowed t)
     ("o" "💻 Online" plain
      "%?

- title: %^{title}
- authors: %^{author}
- url: %^{url}
"
      :target (file+head "zk/%<%Y%m%d%H%M%S>.org"
                         "#+title:💻${title}\n#+filetags: :ONLINE:SOURCE:\n")
      :unnarrowed t)))
  (org-roam-extract-new-file-path "%<%Y%m%d%H%M%S>.org")
  ;;        :map org-mode-map
  ;;        ("C-M-i"    . completion-at-point)
  :config
  (defun my/org-roam-update ()
    (interactive)
    (org-roam-update-org-id-locations)
    (org-roam-db-sync))

  (setq +org-roam-open-buffer-on-find-file nil)
  (org-roam-db-autosync-mode))


(use-package! websocket
    :after org-roam)
(use-package! org-roam-ui
    :after org-roam ;; or :after org
;;         normally we'd recommend hooking orui after org-roam, but since org-roam does not have
;;         a hookable mode anymore, you're advised to pick something yourself
;;         if you don't care about startup time, use
    ;; :hook (after-init . org-roam-ui-mode)
    :config
    (setq org-roam-ui-sync-theme t
          org-roam-ui-follow t
          org-roam-ui-update-on-save t
          org-roam-ui-open-on-start t))

(use-package! org-roam-timestamps
   :after org-roam
   :config
   (org-roam-timestamps-mode)
   (setq org-roam-timestamps-remember-timestamps nil)
   (setq org-roam-timestamps-remember-timestamps nil))


;; 今どきのアウトライナー的な線を出す.
;; Terminal Mode ではつかえないので一旦無効化する.
;; (require 'org-bars)
;; (add-hook! 'org-mode-hook #'org-bars-mode)

;; 空白が保存時に削除されると bullet 表示がおかしくなる.
;; なお wl-bulter は doom emacs のデフォルトで組み込まれている.
(add-hook! 'org-mode-hook (ws-butler-mode -1))
```


#### Org-roam管理下のノートの全文検索 {#org-roam管理下のノートの全文検索}

[Using consult-ripgrep with org-roam for searching notes - How To - Org-roam](https://org-roam.discourse.group/t/using-consult-ripgrep-with-org-roam-for-searching-notes/1226)

consult-ripgrepを [deft](https://jblevins.org/projects/deft/) の代わりに使う. より高速.

```emacs-lisp
(defun my/org-roam-rg-search ()
  "Search org-roam directory using consult-ripgrep. With live-preview."
  (interactive)
  (counsel-rg nil org-roam-directory))
(global-set-key (kbd "C-c r s") 'my/org-roam-rg-search)
```


#### org-publish(Org-roamのノートをサイトへ公開) {#org-publish--org-roamのノートをサイトへ公開}

```emacs-lisp
(setq org-publish-project-alist
      (list
       (list "keido"
             :recursive t
             :base-directory (file-truename "~/keido/notes/wiki")
             :publishing-directory "~/repo/keido-hugo/content/notes"
             :publishing-function 'org-hugo-export-wim-to-md)))
```


### bibtex関連(Org-ref) {#bibtex関連--org-ref}

文献管理. Zoteroと連携して，論文というよりは書籍やYoutube動画やWeb記事のメモに利用.

-   org-ref
-   ivy-bibtex
    -   ivyのactionは ivy-bibtexでC-SPCで選択-> C-M-oでaction選択候補を出し，pとかeとか押す.
-   org-roam-bibtex

<!--listend-->

```emacs-lisp
(use-package! org-ref
  :config
  (setq bibtex-completion-bibliography (list (file-truename "~/keido/references/zotLib.bib")))

  (setq bibtex-completion-additional-search-fields '(keywords))
  (setq bibtex-completion-display-formats
    '((online       . "${=has-pdf=:1}${=has-note=:1} ${=type=:6} ${year:4} ${author:24} ${title:*}")
      (book         . "${=has-pdf=:1}${=has-note=:1} ${=type=:6} ${year:4} ${author:24} ${title:*}")
      (video        . "${=has-pdf=:1}${=has-note=:1} ${=type=:6} ${year:4} ${editor:24} ${title:*}")
      (paper        . "${=has-pdf=:1}${=has-note=:1} ${=type=:6} ${year:4} ${author:24} ${title:*}")
      (t            . "${=has-pdf=:1}${=has-note=:1} ${=type=:6} ${year:4} ${author:24} ${title:*}")))
  (setq bibtex-completion-pdf-symbol "📓")
  (setq bibtex-completion-notes-symbol "📝")

  (setq bibtex-completion-pdf-field "file")
  ;; (setq bibtex-completion-pdf-open-function
  ;;	(lambda (fpath)
  ;;	  (call-process "open" nil 0 nil fpath)))

  ;; Create fields for Film type
  (add-to-list 'bibtex-biblatex-field-alist
               '(("video" "Video or Audio(like YouTube)")))

  (add-to-list 'bibtex-biblatex-entry-alist
               '("video" "A Video"
                 ("video", "title" "editor" "date" "url" "urldate" "abstract" "editortype")
                 nil
                 "keywords"))
  (bibtex-set-dialect 'biblatex))

(use-package! ivy-bibtex
  :after org-ref
  :init
  (map!
   :leader
   :prefix ("b" . "org-ref")
     "b" #'org-ref-bibtex-hydra/body
     "v" #'ivy-bibtex
     "c" #'org-ref-insert-cite-link
     "a" #'orb-note-actions
     "i" #'orb-insert-link)
  :config
  (setq ivy-re-builders-alist
        '((ivy-bibtex . ivy--regex-ignore-order)
          (t . ivy--regex-plus)))
  (setq ivy-bibtex-default-action #'ivy-bibtex-open-url-or-doi)
  (ivy-set-actions
   'ivy-bibtex
   '(("p" ivy-bibtex-open-any "Open PDF, URL, or DOI" ivy-bibtex-open-any)
     ("e" ivy-bibtex-edit-notes "Edit notes" ivy-bibtex-edit-notes)))
  )

(use-package! org-roam-protocol
  :after org-protocol)

(use-package! org-roam-bibtex
  :after org-roam ivy-bibtex
  :hook (org-mode . org-roam-bibtex-mode)
  :custom
  (orb-insert-interface 'ivy-bibtex)
  :config
    (setq orb-preformat-keywords '("author" "date" "url" "title" "isbn" "publisher" "urldate" "editor" "file"))
    (setq orb-process-file-keyword t)
    (setq orb-attached-file-extensions '("pdf")))
```


### Org-noter {#org-noter}

PDFの注釈を管理する. [:link:weirdNox/org-noter](https://github.com/weirdNox/org-noter)

はじめの起動がどうやればいいのかワカラなかった.
特定のファイルに記録を残したい場合はPDFのBufferではなく,
適当なheading作成してM-x org-noterを起動するとPDFを選択できる.

M-x org-noter-create-skeltonという関数がヤばい. [🔗Youtube動画(1:08)](https://youtu.be/lCc3UoQku-E?t=68)
PDFからOutlineを抜き出してOrg fileに生成して，あとはそのOrg-fileのBulletのカーソルを移動するとPDFのほうもシンクロして移動できる.

凄すぎて笑った😂

```emacs-lisp
(use-package! org-noter
  :after (:any org pdf-view)
  :config
  (setq
   ;; I want to see the whole file
   org-noter-hide-other nil
   ;; Everything is relative to the main notes file
   org-noter-notes-search-path (list (file-truename "~/keido/notes/wiki"))
   ))
```


### org-anki {#org-anki}

Org-modeとAnkiをつなぐ．
<https://github.com/eyeinsky/org-anki>

今までanki-editorを利用していたものの，その記法とwikiの相性が悪かった（冗長）.
これならorg-modeのheadlineがそのままつかえるのでよさそう.

```emacs-lisp
(use-package! org-anki
  :after org
  :custom
  ;; one big deckの原則に従う.
  ;; ref: http://augmentingcognition.com/ltm.html
  (org-anki-default-deck "Default")
  :config
  (define-key org-mode-map (kbd "C-c n A s") #'org-anki-sync-entry)
  (define-key org-mode-map (kbd "C-c n A u") #'org-anki-update-all)
  (define-key org-mode-map (kbd "C-c n A d") #'org-anki-delete-entry))
```


### org-modern {#org-modern}

[GitHub - minad/org-modern: Modern Org Style](https://github.com/minad/org-modern)

開発途中なのかいまいち, コードブロックの線もでない...様子見かな...

```emacs-lisp
(after! org-modern
  (setq
   ;; Agenda styling
   org-agenda-block-separator ?─
   org-agenda-time-grid
   '((daily today require-timed)
     (800 1000 1200 1400 1600 1800 2000)
     " ┄┄┄┄┄ " "┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄")
   org-agenda-current-time-string
   "⭠ now ─────────────────────────────────────────────────"))

(add-hook 'org-mode-hook #'org-modern-mode)
(add-hook 'org-agenda-finalize-hook #'org-modern-agenda)
```


## Term {#term}

```emacs-lisp
;; Term
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
```


## Tools {#tools}

```emacs-lisp
;; Tools
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
```


### forge {#forge}

magit拡張, EmacsとGitHubを連携.

doom emacsだと [(magit +forge)](https://github.com/hlissner/doom-emacs/blob/develop/modules/tools/magit/README.org) のオプションでインストールできる.

ref: [Forge User and Developer Manual](https://magit.vc/manual/forge/)

```emacs-lisp
(after! magit
  (setq auth-sources '("~/.authinfo"))
  (setq magit-revision-show-gravatars '("^Author:     " . "^Commit:     "))
  ;; (setq magit-diff-refine-hunk 'all)
)
```

リポジトリ名を変更した場合はissueやPRの作成が失敗する.
これは .git/configの問題なのでローカルのファイルを修正する.


### git-link {#git-link}

現在のバッファの位置のGitHubのurlを取得.

[sshaw/git-link](https://github.com/sshaw/git-link)

```emacs-lisp
(global-set-key (kbd "C-c g l") 'git-link)
(use-package! git-link
  :config
  ;; urlにbranchではなくcommit番号をつかう.
  ;; org-journalへの貼り付けを想定しているのでこの設定にしておく.
  (setq git-link-use-commit t))
```


## UI {#ui}

みため周りの設定.


### Doom {#doom}

```emacs-lisp
;; UI
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
;; どうもフォントが奇数だと org-table の表示が崩れる.
;; Source Han Code JP だとそもそも org-table の表示が崩れる.
;; terminal だと大丈夫な模様.そもそも Terminal はこの設定ではなくて
;; Terminal Emulator の設定がきく.

;; (setq doom-font (font-spec :family "Source Han Code JP" :size 12 ))
(setq doom-font (font-spec :family "Ricty Diminished" :size 15))
;; doom-molokaiやdoom-monokai-classicだとewwの表示がいまいち.
(setq doom-theme 'doom-molokai)
(doom-themes-org-config)

;; counselとdoom-modelineが相性悪いようなので
;; workspace name表示のためには追加で設定.
;; https://github.com/hlissner/doom-emacs/issues/314
(after! doom-modeline
  (setq doom-modeline-icon (display-graphic-p))
  (setq doom-modeline-major-mode-icon t))
```

<https://github.com/seagle0128/doom-modeline>


### emojify {#emojify}

Emacsで絵文字をつかう.

どうもemojifyの絵文字辞書は，emojione-v2.2.6-22というものでやや古い.
Twitterが好きなのでTwitterのオープンソース辞書のtwemojiに変更.

<https://github.com/iqbalansari/emacs-emojify/blob/master/data/emoji-sets.json>

```emacs-lisp
(after! emojify
  (setq emojify-emoji-set "twemoji-v2-22"))
```

ただ，2022現在twemojiはv13なのでv2は古いな..というかでないやつもおおい.

Emacsの機能でemoji-searchがあるのでこれも設定しておこう.
こっちの辞書のほうが扱える文字か多い.

```emacs-lisp
;; doomだと C-c i eでemojify-insert-emoji
(global-set-key (kbd "C-c i E") 'emoji-search)
```


### svg-tag-mode {#svg-tag-mode}

TODOほかラベルを美しく.

[GitHub - rougier/svg-tag-mode](https://github.com/rougier/svg-tag-mode)

```emacs-lisp
(use-package! svg-tag-mode
  :config
  (setq svg-tag-tags
        '(
          ;; :XXX:
          ("\\(:[A-Z]+:\\)" . ((lambda (tag)
                                 (svg-tag-make tag :beg 1 :end -1))))
          ;; :XXX|YYY:
          ("\\(:[A-Z]+\\)\|[a-zA-Z#0-9]+:" . ((lambda (tag)
                                                (svg-tag-make tag :beg 1 :inverse t
                                                              :margin 0 :crop-right t))))
          (":[A-Z]+\\(\|[a-zA-Z#0-9]+:\\)" . ((lambda (tag)
                                                (svg-tag-make tag :beg 1 :end -1
                                                              :margin 0 :crop-left t))))
          ;; :#TAG1:#TAG2:…:$
          ("\\(:#[A-Za-z0-9]+\\)" . ((lambda (tag)
                                       (svg-tag-make tag :beg 2))))
          ("\\(:#[A-Za-z0-9]+:\\)$" . ((lambda (tag)
                                       (svg-tag-make tag :beg 2 :end -1))))
          )))
```


### Others {#others}

```emacs-lisp
(setq display-line-numbers-type t) ; 行番号表示

;; less でのファイル閲覧に操作性を似せる mode.
;; view-mode は emacs 内蔵. C-x C-r で read-only-mode でファイルオープン
;; doom emacs だと C-c t r で read-only-mode が起動する.
(add-hook! view-mode
  (setq view-read-only t)
  (define-key ctl-x-map "\C-q" 'view-mode) ;; assinged C-x C-q.

  ;; less っぼく.
  (define-key view-mode-map (kbd "p") 'view-scroll-line-backward)
  (define-key view-mode-map (kbd "n") 'view-scroll-line-forward)
  ;; default の e でもいいけど，mule 時代に v に bind されてたので,
  ;; emacs でも v に bind しておく.
  (define-key view-mode-map (kbd "v") 'read-only-mode))

;; EXWMの場合suspend-frameでハングするのはたちが悪いので封印.
(use-package! frame
  :bind
  ("C-z" . nil))

;; 実験, どうもマウス操作でEmacsの制御が効かなくなることがあるので.
(setq make-pointer-invisible nil)
```