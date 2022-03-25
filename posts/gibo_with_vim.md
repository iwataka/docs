# giboなるものが流行っているらしいのでVimでやる

この記事ではUbuntu15.10を使っていますが、基本的にはVimがあればOSなどを問わず再現できます。

## giboについて

`.gitignore`を自動的に生成することができるコマンドラインツール[gibo](https://github.com/simonwhitaker/gibo)が流行っているらしいので試してみました。例えば、Javaのプロジェクトを開発しているときは、以下のようにして`.gitignore`を生成します。

```sh
gibo Java > .gitignore
```

生成される.gitignoreは以下のようになります。

```
### https://raw.github.com/github/gitignore/cc542de017c606138a87ee4880e5f06b3a306def/Java.gitignore

*.class

# Mobile Tools for Java (J2ME)
.mtj.tmp/

# Package Files #
*.jar
*.war
*.ear

# virtual machine crash logs, see http://www.java.com/en/download/help/error_hotspot.xml
hs_err_pid*
```

また、`gibo-completion.bash`, `gibo-completion.zsh`, `gibo-completion.fish`のうち、適当なスクリプトを読み込むことによって、簡単にタブ補完を行うことができるようになります。

この記事より詳しいものが他にあるので、興味のある人はご覧になってください。

- [気づいたら.gitignoreはgiboで自動生成する時代になっていた](http://qiita.com/tmknom/items/c4bcebe17d25381fa45d)

この記事の本題は[gibo](https://github.com/simonwhitaker/gibo)ではありません。

## gitignore.vim

とても便利な[gibo](https://github.com/simonwhitaker/gibo)ですが、Vimで同じことができたら（Vimmerにとっては）もっと便利なのではないかと思い、[gitignore.vim](https://github.com/iwataka/gitignore.vim)というプラグインを作成しました。

インストールする場合は、自分の好きなプラグインマネージャを使ってください。
私は[vim-plug](https://github.com/junegunn/vim-plug)派なので、以下のものを`.vimrc`に追加するとインストールすることができます。

```vim
Plug 'iwataka/gitignore.vim'
```

そして、インストールすると、以下のようなコマンドが使えるようになります。

```vim
:Gitignore " 引数のリストを表示する
:Gitignore Java " もともとある.gitignoreに対して、Javaプロジェクト用のパターンを追加する
:Gitignore! Java " もともとある.gitignoreを削除して、新しくJava用の.gitignoreを生成する
:GitignoreUpdate " テンプレートコレクションを更新する
```

`.gitignore`ファイルの場所を指定しなくとも、カレントバッファから辿ってプロジェクトルートを探し、そこに`.gitignore`を生成します。

## giboとの比較

### メリット

- プロジェクトルートの`.gitignore`を自動的に探すこと

    [gibo](https://github.com/simonwhitaker/gibo)の場合、`.gitignore`の場所を指定するのが少し面倒ですが、`gitignore.vim`を使う場合はそれがありません。

- Vimのプラグインであること

    Vimから出たくない人には適していると思います。

### デメリット

- **Vimのプラグインであること**

    Vim使ってない人は[gibo](https://github.com/simonwhitaker/gibo)のほうが適しています。
