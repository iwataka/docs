# ソースコードやドキュメントを速攻で参照するctrlp-quickref.vimを作ってみた

今回始めてVimプラグインを作って見たので、宣伝も兼ねて投稿させていただきます。
この記事を読んだ人はぜひ一度使ってみて、何か意見や要望がある方はお知らせしてもらえると嬉しいです。

https://github.com/iwataka/ctrlp-quickref.vim

## イントロダクション

Vimでプログラムを書いていると、自分が使っているライブラリのソースコードを確認したくなったり、過去に書いたプログラムを参照したくなったり、その他PDFのドキュメントを開きたくなったりすることがよくあります。
そういったときにVimの中から一瞬で目的のファイルを開くことができるような機能が欲しいと思い、プラグインを作成しました。
[ctrlp-quickref.vim](https://github.com/iwataka/ctrlp-quickref.vim)という名前で、その名の通り、[CtrlP](https://github.com/ctrlpvim/ctrlp.vim)の機能をベースにした拡張プラグインです。

## デモンストレーション

`CtrlP`のインターフェースを2回続けて利用します。
1回目は自分が登録したパスが表示され、そこから検索したいパスを選択します。
2回目は先ほど選択したパスを検索した結果が表示されるので、後は自分が開きたいファイルを選択するだけです!

![CtrlP Quickref demo](../assets/quickref.gif)

## 使い方

このプラグインをインストールしたら、1回目の`CtrlP`のインターフェースに表示されるパスを登録しなければなりません。登録する方法は2つあり、1つは自分の`.vimrc`(`init.vim`)に以下のように`g:ctrlp_quickref_paths`変数を作成します。

```
let g:ctrlp_quickref_paths = [
    \ '/directory1/library_or_something_else/src',
    \ '/directory2/*/src',
    \ '/directory3/*',
    " You want to exclude specified directory, put '!' at the head.
    \ '! /directory3/library_or_something_else/'
]
```

複数のパスを登録するためにワイルドカードが使用でき、除外したいパスがあれば"!"を先頭において指定することができます。

2つ目の登録方法は、`~/.ctrlp-quickref`ファイルを作成し、そこにパスを書き込むというものです。例としては以下のようになります。

```
# Write
# Some
# Comments
/directory1/library_or_something_else/src
/directory2/*/src

# Additional comment
/directory3/*

# You can also exclude specified directory by writing like this
! /directory3/library_or_something_else
```

`.gitignore`などの構文を意識しています。

上の2つのうちのどちらかの方法でパスを登録したら、後は`:CtrlPQuickRef`コマンドを実行するだけです。`CtrlP`インターフェースが開き、自分が登録したパスの中から一つを選択します。
再度`CtrlP`インタフェースが開き、選択したパスにおける検索結果が今度は表示されます。

### 例

例えば、`~/.ctrlp-quickref`に以下のような内容を記述します。

```
~/.vim/bundle/*
```

すると、使っているVimプラグインのパスがすべて指定されたことになり、そのすべてのソースコードに簡単にアクセスすることが出来るようになります。Vimスクリプトを書いている時には便利だと思います。また、

```
~/projects/*
```

のように、自分のプロジェクトを保存しているディレクトリを指定すると、すべてのプロジェクトのソースコードやドキュメントを即座に見ることができます。

## コマンド

- `:CtrlPQuickRef`

    `CtrlP`のインタフェースを開き、自分が登録したパスを選択肢として表示します。

- `:CtrlPQuickRefLastDir`

    `CtrlP`を、自分が最後に選択したパスを引数として実行します。

- `:CtrlPQuickRefEdit`

    自分のパスを登録しているファイル(デフォルトでは`~/.ctrlp-quickref`)を開きます
    。自分の`.vimrc`に全て登録している場合は何も起こりません。

## オプション

- `g:ctrlp_quickref_readonly_enabled`

    デフォルトではreadonlyフラグをつけてファイルを開きますが、この変数の値を0にするとreadonlyフラグをつけずにファイルを開くことができます。

- `cg:trlp_quickref_open_extensions`

    このリストに含まれている拡張子のファイルを開く場合は、Macではopen、Linuxではxdg-openで自動的に開かれます。デフォルトでは`['html', 'pdf']`となっています。

- `cg:trlp_quickref_configuration_file`

    パスを登録するファイルを指定します。デフォルトでは`~/.ctrlp-quickref`です。

- `cg:trlp_quickref_paths`

    パスの登録を`.vimrc`(`init.vim`)内で行う場合、この変数にリストとして登録します。

## 必要なプラグインなど

- [ctrlp.vim](https://github.com/ctrlpvim/ctrlp.vim)

- `xdg-open` command (Linuxユーザのみ)

- [ctrlp-py-matcher](https://github.com/FelikZ/ctrlp-py-matcher)

    これは任意ですが、大きなプロジェクトなどに適用する場合には絞り込みが早くなるのでおすすめです。

- [the_silver_searhcer](https://github.com/ggreer/the_silver_searcher)

    これも任意です。`CtrlP`ユーザの多くが使っているかもしれませんが、おすすめしておきます。
