## gulp-ejs-sass



**via 上カルビ**

https://onedarling.site/programming/htmlcss/gulp-ejs-sass/

以下すべて引用



#### やること

- ejsファイルのコンパイル・整形・コメントの削除
- scssファイルのコンパイル（ベンダープレフィックス付与、メディアクエリをまとめる）・圧縮
- jsの変換（Babel）・圧縮
- 画像（jpg,png,gif,svg）の圧縮
- Webp形式への変換
- ローカルサーバーで確認＆自動反映
- コンパイル・圧縮しないファイルのコピー（外部ライブラリのスタイルシートやスクリプト、ローカルフォントなど）
- 出力先のフォルダの削除

#### やらないこと

- scss,cssのプロパティのソート（記述順序の変更）
- jsファイルのバンドル
- 出力先のフォルダ、ファイルを自動で削除
- FTPを使用した自動アップロード
- WordPress関連の処理



### version

Node.js：14.18.0
npm：6.14.15

### install

```shell
npm i
```

### run

```shell
npx gulp
```



#### 出力先のファイル削除について

gulpはsrcからファイルを削除しても、public（出力先）からは消えません。

**アップするときや納品する際は余計なファイルを削除したいので、直前にcleanAllですべて削除してまたgulpを走らせる、みたいな処理を行います。**



#### EJSのディレクトリ構造について

今回のgulpではEJS初心者が分かりやすいように、共通パーツをすべて「includes」フォルダに入れております。

こちらはお好みで「components」や「laylouts」など、CSS設計やフレームワークチックにカスタマイズしてもよいと思います。



#### Sassのコンパイルについて

今回はコンパイルのオプションでcompressedを使っています。ただ納品後に他の誰かがCSSファイルを編集する場合は、expandedなど他のオプションを指定することをおすすめします。

またメディアクエリをまとめる際に、**多くの方が[css-mqpacker](https://www.npmjs.com/package/css-mqpacker)を使っていますが、こちらは非推奨とされています。**

ですので代わりに**[gulp-group-css-media-queries](https://www.npmjs.com/package/gulp-group-css-media-queries)**を使ってます。

ただ残念ながらこちらのパッケージを使用すると、**なぜか自動で整形されてしまいます。**

私の場合、基本的に納品後に先方が修正することはない案件ばかりなので、**最後にCSSを圧縮するcssNano()という処理を走らせています。**

もしコンパイルオプションをexpandedなどにしている場合は、こちらのcssNano()の処理は削除またはコメントアウトすれば圧縮されません。