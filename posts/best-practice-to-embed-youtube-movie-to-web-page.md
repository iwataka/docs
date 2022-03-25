# YouTubeをWEBページに埋め込むためのベストプラクティス

YouTubeの動画をWEBページに埋め込むことはいくつかのメリットがあります。

  - 文字を尽くすことなく手軽に情報を伝えることができる
  - 文字ばかりのページよりも見栄えが良くなる

しかし、埋め込みには以下のような難しい点があります。

  - いかにしてレスポンシブにするか
  - たくさん動画を埋め込んだ場合のページの読み込み速度をどうやって改善するか

この記事では、以上の点を解決しつつ、YouTubeの動画をきれいに埋め込むための自分のベストプラクティスについて紹介します。

## TL;DR

- [fitVids.js](http://fitvidsjs.com/)を使ってレスポンシブに埋め込む
- [blazy](https://github.com/dinbror/blazy/)を使って遅延読み込みを実現する
- その2つを組み合わせて使うとYouTube動画の埋め込みとしてはベスト

## 使い方

まず、以下のように[fitVids.js](http://fitvidsjs.com/)と[blazy](https://github.com/dinbror/blazy/)の読み込みと初期化を実施します。

```html
<script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/3.2.1/jquery.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/fitvids/1.2.0/jquery.fitvids.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/blazy/1.8.2/blazy.min.js"></script>
<script>
  var bLazy = new Blazy({
    success: function(element) {
      $("div#" + element.parentNode.id).fitVids();
    }
  });
</script>
```

この2つを組み合わせて使うためには、[blazy](https://github.com/dinbror/blazy/)を初期化して遅延読み込みの際の処理を記述する際に、[fitVids.js](http://fitvidsjs.com/)を使って埋め込み動画のサイズの調整処理を加えるということが必要です。

また、以下のように動画埋め込みのためのHTMLを記述します。

```html
<div id="youtube-Y2VF8tmLFHw-wrapper">
  <iframe
    class="b-lazy"
    data-src="https://www.youtube.com/embed/Y2VF8tmLFHw?autohide=1&fs=1"
    frameborder="0"
    allowfullscreen>
  </iframe>
</div>
```

ここで大事なのは、`iframe`の親に一意のIDを割り当てる必要があるということです。
ここではYouTube動画のIDを使用して一意のIDを実現しています（同じ動画を複数埋め込みたい場合はより工夫する必要があります）。

埋め込みのオプションは用途によって変更してください。

## サンプル

最近個人のブログを作成しており、そこにサンプルを載せているのでよかったら見てください

- https://iwataka.netlify.com/tech/youtube-embed-best-practice/

<div id="youtube-Y2VF8tmLFHw-wrapper">
  <iframe
    class="b-lazy"
    data-src="https://www.youtube.com/embed/Y2VF8tmLFHw?autohide=1&fs=1"
    frameborder="0"
    allowfullscreen>
  </iframe>
</div>

## まとめ

> [fitVids.js](http://fitvidsjs.com/)と[blazy](https://github.com/dinbror/blazy/)を使うとベストなYouTube埋め込みができる

ちなみに、Vimeoなどの他のサイトの動画や、ChromeやiPhone版Safari以外の他のWEBブラウザについてはまだ試していないのですが、おそらく期待通りに動くと思います。
