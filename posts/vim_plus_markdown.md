# Vim + Markdown

Markdownは現在、プロジェクトのドキュメントを書くために利用されたり、[Jekyll](https://jekyllrb.com/)や[Hugo](https://gohugo.io/)などを用いた静的サイトに利用されたりしており、編集する機会は多いと思います。
Vim界隈でも、たくさんのプラグインが作成されており、便利な機能が提供されているので、ここでまとめたいと思います。

## 基本的なプラグイン

ます紹介するのは、Markdown編集に必要不可欠な、基本的な機能を提供するプラグインです。
共通の機能として、以下のようなものがあります。

- Markdownファイルタイプの自動設定
- 一般的なMarkdown記法のシンタックスハイライト
- オートインデント

このような機能を持っているプラグインとして代表的なのものを以下にリスト化しました。

- [plasticboy/vim-markdown](https://github.com/plasticboy/vim-markdown)

    GitHub上で一番多くスターがついており、開発も最も活発なプラグインです。
    例として、以下のような機能があります。

    - 一般的なMarkdown記法以外のシンタックスハイライト
        - LaTex math
        - JekyllやHugoで使用されているFront Matter
    - 隣接するヘッダへのモーション
    - TOC(Table of contents)の生成
    - テーブルの整形

    **ただし**、私のWindows上で使用していたところ、Fenced code blockのハイライトを行う際に、少し動作が遅くなる問題が見受けられました（少し前の話なので、今は改善されているかもしれません）。
    InsertEnter, InsertLeave, CursorHold, CursorHoldIなどのグループに属するオートコマンドを使っているためだと思われます(詳細は[こちら](https://github.com/plasticboy/vim-markdown/blob/master/ftplugin/markdown.vim#L720-L727))。

- [tpope/vim-markdown](https://github.com/tpope/vim-markdown)

    [pathogen](https://github.com/tpope/pathogen)や[vim-fugitive](https://github.com/tpope/vim-fugitive)など、有名なVimプラグインを数多く作っている[tpope](https://github.com/tpope)作のプラグインです。
    特筆すべき機能は追加されていませんが、余計な動作がなく、私もこれをMarkdownの編集に使用しています。

- [gabrielelana/vim-markdown](https://github.com/gabrielelana/vim-markdown)

    `vim markdown`でGoogle検索を行っても上位に出てこないので、上の2つと比べると知名度が低いかもしれませんが、GitHubスタイルのMarkdownを強く意識しており、便利な機能をたくさん実装しているプラグインです。
    例としては、以下のような機能があります。

    - Focus Mode (Markdownファイルの中身の一部を別バッファで編集する)
    - テーブルの自動整形
    - Jekyllのファイルの自動検知と、Liquidテンプレートのサポートの自動追加
    - GitHubスタイルのチェックボックスの追加、チェック、削除
    - リストアイテムのインデント、アンインデント

私個人の感想としては、ある程度の処理負荷があっても便利な機能を使いたいならば[plasticboy/vim-markdown](https://github.com/plasticboy/vim-markdown)、最低限の機能で快適に使いたいならば[tpope/vim-markdown](https://github.com/tpope/vim-markdown)、その中間ならば[gabrielelana/vim-markdown](https://github.com/gabrielelana/vim-markdown)という気がします。

## プレビュー

次に紹介するのは、Markdownファイルの内容をブラウザにレンダリングするためのプラグインで、数多くの種類があります。

まずは、ブラウザの内容をどのタイミングで更新するのかという観点で個々のプラグインによって違いがあり、次の2つのタイプに別れると思います。

- バッファの書き込み時
- 文字の挿入時

また、外部依存の有無の観点からもいくつかのタイプに分けることができます。

- Node.jsで書かれた外部パッケージを必要とするもの
- VimのRubyサポートもしくはPythonサポートを必要とするもの
- 外部依存がないもの

このようなプラグインのうち代表的なものを以下にリスト化しました。

- [vim-instant-markdown](https://github.com/suan/vim-instant-markdown)

    - `npm install -g instant-markdown-d`を実行し、外部パッケージをインストールする必要がある。
    - 文字を挿入する度にブラウザの内容が更新される。

- [vim-livedown](https://github.com/shime/vim-livedown)

    - `npm install -g livedown`を実行し、外部パッケージをインストールする必要がある。
    - 書き込み時にブラウザの内容を更新する。

- [vim-preview](https://github.com/greyblake/vim-preview)

    - Rubyサポートが有効になっている必要がある
    - Markdown以外のフォーマットも対応している
        * rdoc ([github-markup](https://github.com/github/markup)というruby gemに依存)
        * textile ([RedCloth](https://github.com/vmg/redcarpet)に依存)
        * html
        * ronn ([ronn](https://github.com/rtomayko/ronn)に依存)
        * reStructuredText ([RbSt](https://github.com/alphabetum/rbst)及び[rst2html](http://docutils.sourceforge.net/)に依存)

- [vim-markdown-preview](https://github.com/Jamshedvesuna/vim-markdown-preview)

    - [markdown](https://pypi.python.org/pypi/Markdown)もしくは[grip](https://github.com/joeyespo/grip)に依存している

- [markdown-preview.vim](https://github.com/iamcco/markdown-preview.vim)

    - PythonまたはPython3サポートが有効になっている必要がある。
    - 文字を挿入する度にブラウザの内容が更新される。

- [previm](https://github.com/kannokanno/previm)

    - 外部依存がない
    - Markdown以外のフォーマットも対応している
        * reStructuredText
        * textile
    - Markdownファイルの中で[mermaid](http://knsv.github.io/mermaid/index.html)記法を使うことができる。

また、私は試したことが無いですが、[quickrun](https://github.com/thinca/vim-quickrun)を利用したプレビュー方法もあるらしいです

- [markdownの編集環境をいい感じの整えてみた[vim + quickrun + pandoc]](http://qiita.com/ssh0/items/b68263a7866b4ce9eaf1)。
- [VimでMarkdown, ブラウザでプレビュー](http://qiita.com/us10096698/items/1ac05c5c9543d2f79fa3)

### [minidown.vim](https://github.com/iwataka/minidown.vim)

Markdownファイルのプレビューを行うプラグインは、上で見たとおり外部依存が多いのが特徴ですが、私はNode.jsやPython、Rubyなどが使えない環境でも使用することができるプラグインが欲しかったので、すごく簡単なものを作成することにしました。

特徴としては以下のようなものがあります。

- [pandoc](http://pandoc.org/)を利用しており、PATH上に実行可能ファイルを置くだけで使用できる。
- 同梱されているCSSを適用することによって、ある程度GitHubのスタイルを再現している。
- `:Minidown`コマンドを実行するだけでブラウザ上にレンダリングできる。

リロードを自分で行わなければならないのが少し面倒ですが、自分は頻繁にレンダリングの結果を見たいというわけではないので、これで十分役立っています。

[previm](https://github.com/kannokanno/previm)は外部依存がないので使いたいのですが、Windowsで実行するにあたって少し[問題](https://github.com/kannokanno/previm/issues/46)があるような気がするので、保留という感じです。

## その他

最後に紹介するのは、上記の2つに分類されない、便利機能を実装したプラグインです。
下に2つ載せていますが、これ以外にも探せばたくさん見つかるんじゃないかと思います。

- [vim-textobj-markdown](https://github.com/pocke/vim-textobj-markdown)

    Fenced code block用のテキストオブジェクトを実装しています。

- [vim-checkbox](https://github.com/jkramer/vim-checkbox)

    GitHubスタイルのチェックボックスのチェック、アンチェックを簡単に行えるようになります。

    **ただし**、同様の機能が[gabrielelana/vim-markdown](https://github.com/gabrielelana/vim-markdown)にも実装されており、しかも挿入と削除が行えるので、こちらの機能はやや劣っている感じを受けます。

### [vim-markdown-ex](https://github.com/iwataka/vim-markdown-ex)

色々な便利プラグインを調べた後、自分でもMarkdown編集用にプラグインを作成しました。
[vim-markdown-ex](https://github.com/iwataka/vim-markdown-ex)という名前で、Markdown編集に便利なサブ機能を集めたものになっており、[tpope/vim-markdown](https://github.com/tpope/vim-markdown)と一緒に使用しています。

機能としては以下のようになっています。

- GitHubスタイルのチェックボックスの挿入、チェック、削除 ([vim-repeat](https://github.com/tpope/vim-repeat/)のサポート付き)

    チェックボックスの編集をする機能を提供しているプラグインは、私が知る中では、[vim-checkbox](https://github.com/jkramer/vim-checkbox)と[gabrielelana/vim-markdown](https://github.com/gabrielelana/vim-markdown)がありますが、前者はチェック、アンチェックのみしか提供しておらず、後者は同じ機能を提供していますが、[vim-repeat](https://github.com/tpope/vim-repeat)をデフォルトでサポートしていないということが、このプラグインと異なる点です。

- 前後のリンクへのジャンプ

    `Ctrl+N`と`Ctrl+P`で、前後のリンクへジャンプすることができます。
    ちなみにこの機能は、[vim-github-dashboard](https://github.com/junegunn/vim-github-dashboard/)に影響を受けています。

- リンクをブラウザ上で開く`gx`の強化

    既存の`gx`に対して、以下の点が強化されています。

    - URL上に直接カーソルが乗っていなくても、現在行に存在すれば、それを探してブラウザ上で開くことができる。
    - `[Header Title](#header-title)`のように、特定のヘッダへのリンクに対して使用すると、そのヘッダにジャンプすることができる。

- Fenced code blockを選択するテキストオブジェクト

    この機能はほぼ[vim-textobj-markdown](https://github.com/pocke/vim-textobj-markdown)と同じものです。
    しかし、[vim-textobj-markdown](https://github.com/pocke/vim-textobj-markdown)は[vim-textobj-user](https://github.com/kana/vim-textobj-user/)に依存しているのに対し、このプラグインは外部のプラグインに依存していません。

- ヘッダーのサーチをコマンド補完付きで行う (2016/5/21 追記)

- `gx`で開いたリンクの履歴から、再度リンクを開くことができる (2016/5/22 追記)

また、[vader.vim](https://github.com/junegunn/vader.vim/)を用いてテストを行っているので、ある程度の信頼性は担保できていると思います。

## まとめ

Markdown編集用のVimプラグインは数多く作成されているので、自分の環境や用途に合わせて選択する必要があります。

良かったら、私が作ったプラグインも試してみてください。
