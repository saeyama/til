## Rails6 

### `Webpacker+Yarn+Sprockets`  

以下サイトを参考に、他参考サイトと合わせて概要をまとめ。  
https://techracho.bpsinc.jp/hachi8833/2020_01_16/85940  
https://techracho.bpsinc.jp/hachi8833/2020_01_17/85943

---

【用語/備忘】  
`パッケージマネージャ`  
コンピュータ(自分のPC)に何のソフトウェアがインストールされたかを記録し、新しいソフトウェアのインストール・新しいバージョンへのソフトウェアの更新・以前インストールしたソフトウェアの削除を容易に行えるようにするプログラム。  

`モジュール`  
設計上の概念で、システムを構成する要素となるもの。  

`ビルド`  
ソフトウェアのビルドは、プログラミング言語で書かれたソースコードファイルや各種リソースファイルを独立したソフトウェア生成物に変換するコンピュータ上で実行されるプロセス、またはその結果を指す。  

`非同期処理(Ajax)`  
ページが更新された際などに、更新前と更新後を比較して足りない部分だけをデータ通信する処理のこと。
この非同期処理の事をフロントエンド側の処理ではAjaxと呼ぶ事もある。  

`アセットパイプライン`  
アセットファイル（JavaScriptやCSSや画像など）を入力に取り、それらを処理して欲しいフォーマットを出力として生成するもの。

---

## Node.js  
https://eng-entrance.com/what-is-nodejs  
Node.js = サーバサイドのJavaScript

- Node.jsが開発されたことで、JavaScriptでサーバーサイドの処理ができるようになった。
- それに伴い、JavaScriptのフレームワークが開発された。（React、Express）  

## npm  
Node Package Manager  
Node.jsモジュールのパッケージ（Package ）を管理する（Manager）ツール。  
Node.jsのパッケージ（Package）とは、予め用意された便利な機能をまとめたもの。  
npmはパッケージのインストールとバージョン管理に使う。  

npmとは  
https://www.webprofessional.jp/beginners-guide-node-package-manager/ 

**Node.jsをインストールするとnpmもインストールされる。**

```
npmでパッケージをインストールする方法  
npm install <パッケージ>
```
ダウンロードしたパッケージを`./node_modules`に保存。  
パッケージのリストを`./package.json`に保存。   

※パッケージはvueやjQueryといった有名なフレームワーク、gulpなどのビルドシステム、非同期promise/asyncとかも

## yarn
https://qiita.com/ta2roo/items/5b3784dc3616aeb7e61b  
npmより新しいパッケージマネージャ(npmをパワーアップしたもの)

**Node.jsをインストールしてもyarnはインストールされない。npm、homebrew、MacPortsからインストールできる。**

```
yarnでパッケージをインストールする方法
`yarn add パッケージ`
```
ダウンロードしたパッケージを`./node_modules`に保存。  
パッケージのリストを`./package.json`に保存。    

↓ `./node_modules` 
``` 
5系
.yarn-integrityファイルのみ
"modulesFolders": [  ]  
```
  
```　
6系 たくさん
.yarn-integrity
  "modulesFolders": [
    "node_modules"
  ],
```  
yarnでインストールしたnpm情報が記録されておりこれによってキャッシュからnpmをコピーしてくる仕組み  
(yarnのキャッシュ)    
https://sakanasoft.net/yarn-cache/

- yarnもnpmのリポジトリからパッケージを取得する点は同じ  
- npmより高速。  
- npmと互換性があり、npmで使用していたプロジェクト設定ファイル（package.json）がそのまま使える。  
- バージョン管理に優れている。  
  `yarn.lock`というファイルをプログラムインストール後に自動生成し、必要なバージョンのnpmパッケージをそのファイルでロック。  
  （RubyのGemfile.lockと同じようなもの）  
  `yarn.lock`はインストールしたプログラムが使用している別のプログラム（依存プログラム/パッケージ）のバージョンが明確に書き込まれている。  
   依存プログラム/パッケージをその後再度インストールしてもバージョンの整合性が保たれるので、バージョン不一致でプロジェクトが動かなくなる危険性が無くなる。     
   (npｍにもpackage-lock.jsonでロックする機能が追加された。)    

yarn.lockエラー  
https://qiita.com/nakki/items/4fa58cb6ff4d6c24c2d2

npm yarn 違い  
https://qiita.com/Hai-dozo/items/90b852ac29b79a7ea02b  

---

## Rails6でJavaScriptのライブラリが必要になった場合の操作。

- 従来: JavaScriptのライブラリを提供する`gem`を追加し、app/assets/application.jsでライブラリをrequire（`Sprockets`がコンパイル）
- 現在: 同じ作業を`yarn`（https://yarnpkg.com）で行う。  
yarn add <パッケージ名>を実行してからrequire

＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝

## ES6
JavaScriptの新しい標準
ES6にはクラス定義やデストラクタ、アロー関数といった極めて便利な機能が搭載

## Babel  
https://qiita.com/mzmz__02/items/e6fbe5e30cc3fd13788f

すべてのブラウザがES6を理解できるとは限らないため、ES6のJavaScriptがどんなブラウザでも動くようにするには、ES6のJavaScriptコードを読み取って旧来のES5 JavaScriptに変換するツールが必要となる。
Babelはそのための変換を行うコンパイラ。

## Webpack

Webアプリケーションを構成するリソース（jsファイル、cssファイル、画像ファイル等々）を一つにまとめてくれるツール。 
https://webpack.js.org/   
https://ja.wikipedia.org/wiki/Webpack

Webpack 詳細のところを参照↓  
https://qiita.com/tatsurou313/items/645cbf0a3af4c673b5df


`Babel`と`Yarn`、それらの設定ファイルのアセットを自動コンパイルして環境を管理  
バンドル

流れ
- ES6 JavaScriptコードを取り出す
- babel-loaderプラグインでBabelにES6をコンパイルさせ、ES5 JavaScriptコードに変換する
- できあがったpackをHTML DOMにインクルードできる形の1つのファイルにまとめる。  
```  
<script type="text/javascript" src="path-to-es5-javascript-pack.js"></script>
```

## webpacker  
webpackerはRailsのgemの1つ  
webpackは色々な設定ができる分、学習コストがやや高い。webpackerはwebpackの中身を良く知らなくても、良い感じにwebpackを動かしてくれる優れもの

Webpackとwebpacker  
https://www.fundely.co.jp/blog/tech/2020/01/22/180037/#:~:text=webpack%E3%81%A8webpacker%E3%81%AE%E9%81%95%E3%81%84&text=%E5%90%8D%E5%89%8D%E3%81%8C%E4%BC%BC%E3%81%A6%E3%81%84%E3%81%A6,%E3%81%A6%E3%81%8F%E3%82%8C%E3%82%8B%E5%84%AA%E3%82%8C%E3%82%82%E3%81%AE%E3%81%A7%E3%81%99%E3%80%82  


### `注意１ stylesheet_pack_tag を有効にする場合`　 

```
config/webpacker.yml

extract_css: true

デフォルトはextract_css: false
```

### `注意２ rails assets:precompileを実行した時の挙動。`    
app/assets/の下にあるものだけがプリコンパイルされるだけではない。
実際には、Railsはapp/javascript/の下にある`Webpackのアセット`と、app/assets/の下にある`Sprocketsのアセット`が両方コンパイルされる。


↓参考  
stylesheet_pack_tag と Webpackerの設定 extract_css  
https://qiita.com/kazutosato/items/23d2aa126084d054398b

基本的な設定と概要  
https://numb86-tech.hatenablog.com/entry/2019/01/09/215714

Railsでwebpackを用いて画像を表示させる  
https://qiita.com/hida-yoshi/items/55dc48477201dc195bb8


## Sprockets 4
Webpackと同様に、Sprokectsもアセットパイプライン。  
アセットパイプラインとは、アセットファイル（JavaScriptやCSSや画像など）を入力に取り、それらを処理して欲しいフォーマットを出力として生成するもの。

Rails 6から、Sprocketsに代わってWebpack（er）がRailsアプリでJavaScriptを書くための新しい標準となったが`Sprocketsは今もアプリケーションにCSSを追加するデフォルトの方法でもある。`

Sprocketsのパイプラインを用いてアセットをインクルードしたい場合。
- CSSを書く（ここではapp/assets/stylesheets/my_makeup.cssとする）
- app/assets/config/manifest.jsでlink_treeかlink_directoryかlinkを用いて、stylesheet_link_tagでそのCSSを利用できるようにする（例: link my_makeup.css）
- ビューにstylesheet_link_tagを書いてCSSをインクルード（例: <%= stylesheet_link_tag 'my_makeup' %>）


#### Webpackがコンパイルするのは`モジュール`であるという点が、Sprocketsと異なる。  
- モジュール化されていないものはバンドルすることができない。
- Webpackのローダー(リソースをモジュール化するためのツール)を通じてモジュール化させてあげることで、はじめてバンドルができるようになる。

sprocketsとWebpacker   
https://qiita.com/tatsurou313/items/645cbf0a3af4c673b5df   
https://www.school.ctc-g.co.jp/ruby/columns/trans/trans57.html  

Webpacker導入してCoffeeScriptからES2015（ES6）に移行  
https://blog.rista.jp/entry/2017/09/27/103715

---
## Rails6でもsprocketsは使える

```
rails new アプリ名
``` 
できたファイル↓

**Yarnのファイル:**
- package.json  

**Webpackerのファイル:**
- config/webpacker.yml
- app/javascript/packs/application.js
- app/views/layouts/application.html.erb  

**Sprocketsのファイル:**
- app/assets/config/manifest.json  

### bootstrapをyarnでインストールした場合

```
app/javascript/packs/application.js

require("bootstrap");
```
※jQueryをrequireしなくても動く。  
理由：jQueryをyarnでインストールしているので、bootstrap自身がjQueryを自動でrequireできる。jQueryはapplication.jsの中で利用可能な状態になる。jQueryをapplication.jsの中で直接使う必要がない限り、実際にはjQueryをapplication.jsでrequireする必要がない。

```
fortawesomeは以下のように設定
require("@fortawesome/fontawesome-free");
```

SprocketsはWebpackと異なり、インクルードするファイルを決定するためにnpmモジュールのpackage.jsonファイルを読み込まない。  
名前だけを指定してモジュールをインポートすることはできない。実際にインポートしたいファイル名とそのパスを指定する必要がある（拡張子はなくても大丈夫）。　　　

---
【備忘】

インストール済みのパッケージを確認する方法  
`npm list -g`   
(-gとつけることで、使用しているコンピューター内の全てのパッケージを表示)  

promise  
非同期処理を分かりやすく実装。(promiseもパッケージ)  
npmを使ってinstall  
`npm install promise`  

async  
promise同様非同期処理を実装 。(asyncもパッケージ)    
promiseよりもasyncの方が簡潔に非同期処理実装が可能。  
asynicはIE等、非対応のブラウザも存在するため、採用には実務上でもよく考える必要がある。  
`npm install async`  

