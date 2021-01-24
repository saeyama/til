# Chapter1

- インターネットとWebもともとは別の目的で開発

- Web ••• World Wide Web（世界に広がるクモの巣）<br> 
﹂Webページ ••• ハイパーテキスト(コンテンツ)と呼ばれる言語で構成<br> 
﹂ハイパーリンクを埋め込むことができる

- ハイパーテキストはハイパーリンクで繋がっている＝だからクモの巣

- ユーザーインターフェース(UI)•••コンピューターの機能とユーザーのやりとりを橋渡し

- API ••• ソフトウェア同士のやりとりを橋渡しする機能

- HTTP(Hyper Text Transfer Protocol)•••ハイパーテキスト(コンテンツ)のやりとりの手順

- WebブラウザとWebサーバーのやりとりはHTTPに従って行われる<br>
﹂HTTPというプロトコル(規約・手順) <br>
﹂環境が異なってもプロトコルは世界共通

- HTML•••ハイパーテキストを記述する為の言語<br>
﹂HTMLで記述された文書をコンテンツと呼ぶ

- Webブラウザ ••• ハイパーテキストを読みやすいものに解釈するもの<br>
（Chrome IE Firefox等）<br>

- Webページ ••• URLでアクセス<br>
http://www.●●.jp/index.html <br>
﹂HTTP/HTTPS (セキュリティ高め)でやり取り<br>
﹂www.●●.jp サーバーアクセス<br>
﹂index.html コンテンツ


## 動的ページの仕組み

- **<font color="HotPink">CGI</font>**(Common Gateway Interface) •••  WebサーバーがWebブラウザの要求に応じてプログラムを起動させる仕組み。

- **<font color="HotPink">サーバーサイドスクリプト</font>** ••• CGIから呼び出されるスクリプト。<br> 
﹂一般的に文字列の扱いに長けた<font color="Pink">スクリプト言語で記述(Perl,Ruby,Python,JavaScript,PHP)</font>

- **<font color="HotPink">クライアントサイドスクリプト</font>** ••• HTMLに埋め込まれ、Webブラウザによって読み込まれる際に実行される <br> 
﹂クライアントサイドスクリプトは主に<font color="Pink">JavaScript</font>が用いられる。


## Webの標準化

- **<font color="HotPink">W3C</font>**(World Web Consortium) •••  Webの標準化を進める団体。<br>
﹂W3Cが標準化したものは「勧告」であり強制ではないがほぼW3C標準に準拠。

## Webの設計思想

- **<font color="HotPink">RESTful</font>** ••• 4つの原則からなるシンプルな設計 <br> 
https://blog.api.rakuten.net/ja/jp-restful-api/#:~:text=REpresentational%20State%20Transfer%E3%81%AE%E7%95%A5,%E3%81%AE%E3%81%93%E3%81%A8%E3%82%92%E6%8C%87%E3%81%97%E3%81%BE%E3%81%99%E3%80%82

- **<font color="HotPink">セマンティックWeb</font>** •••  Webページの情報に意味を持たせる。プログラムにメタデータを埋め込む。W3Cの標準化を進めてる。普及はまだまだ先<br>

## Web●●
- Webページ ••• Web上にある文書
- Webサイト ••• Webページの集まり
- Webアプリケーション ••• Webを介して人が利用するサービス
- Webサービス ••• プログラムが利用するサービスを提供
- Webシステム ••• Webサービスを提供するための仕組み


# Chapter2

- サーバー ••• ネットワーク上で情報やサービスを提供する役割を持つコンピューター(Webサイトを提供)
- クライアント ••• サーバーから提供された情報やサービスを利用する役割を持つコンピューター(Webブラウザ)
- インターネット ••• Webサイトを閲覧する際にインターネットサービスプロバイダーが提供するサービスを利用しインターネットへ接続する必要がある。
- IX ••• プロバイダー同士を接続する拠点

- **<font color="HotPink">TCP/IP</font>** •••  インターネットにおけるさまざまなサービスを実現するためのプロトコルの集まり(インターネットにおける標準)<br>
﹂プロトコル種類 ••• <font color="Pink">HTTP・FTP ・SMTP(送信)・POP(受信)</font>

- **<font color="HotPink">TCP/IPは4階層(レイヤー)</font>**<br>
﹂<font color="Pink">アプリケーション層(レイヤー4)</font>:アプリケーション毎のやりとりを規定(クライアントとサーバーシステムで構成
)<br>
﹂<font color="Pink">トランスポート層(レイヤー3)</font>:アプリケーション層のやりとりに応じデータの転送処理している。**<font color="HotPink">TCP(メール等の重要なデータで利用)/UDP(通信手続簡略/動画等で利用)</font>**<br>
﹂<font color="Pink">インターネット層(レイヤー2)</font>:ネットワーク間の通信を規定。**<font color="HotPink">IP/ICMP</font>**<br>
﹂<font color="Pink">ネットワークインターフェース層(レイヤー1)</font>:ハードウェアに関する規定。**<font color="HotPink">イーサネット/Wi-Fi</font>**<br>

## IPアドレスとポート番号位置付け
- コンピューター：マンション
- IPアドレス：住所(数字で表示)
- ポート番号：部屋番号

- **ポート番号** ••• 0~65535(Webサーバー80番)

- **<font color="HotPink">DNS</font>** •••  ドメインとIPアドレスに変換するための仕組み。DNSサーバーがツリー状の階層構造をとり、分散処理。

- **<font color="HotPink">名前解決</font>** •••  ドメインとIPアドレスを紐付けること<br>
﹂<font color="Pink">正引き</font>:ドメインからIPアドレスを取得<br>
﹂<font color="Pink">逆引き</font>:IPアドレスからドメインを取得

- **<font color="HotPink">HTTP</font>** •••  クライアント(Webブラウザ)とサーバー(Webサーバー)間において Webコンテンツを送受信する為のプロトコル。

- **データの流れは、4階層にの順で各プロトコルが利用される**<br>
﹂Webブラウザから下層に渡される際にヘッダーが追加 **(カプセル化)**<br>
﹂Webサーバーに上層から渡される際にヘッダーが取り除かれる **(非カプセル化)**<br>

## IPv4とIPv6の違い
- **IPはIPv4とIPv6の2種類ある(IPv4が枯渇すると予想されたためIPv6ができた)**<br>
﹂IPアドレスの節約化でIPv6への移行は進んでいないが、IoTの登場で枯渇は待ったなしの状態
### IPv4<br>
- アドレス：32 ビット(約43億)
### IPv6<br>
- アドレス：128 ビット(約340澗)

# Chapter3
- **<font color="HotPink">HTTPメッセージ</font>** ••• WebブラウザとWebサーバーでやりとりする際に利用されるデータ形式<br>
﹂<font color="Pink">HTTPリクエスト</font>:Webブラウザからの要求<br>
﹂<font color="Pink">HTTPレスポンス</font>:Webサーバーからの応答<br>
1リクエストに対し１レスポンスを返す。
<br>

| 【HTTPメッセージのデータ構成】|
|:--|
|HTTPリクエスト(リクエスト行)　HTTPレスポンス(ステータス行)|
|メッセージヘッダー(HTTPヘッダー)|
|空白行|
|メッセージボディ|
<br>

- **<font color="HotPink">HTTPメソッド</font>** ••• 目的別に複数定義<br>
﹂<font color="Pink">GET</font>:Webブラウザに履歴が残る<br>
﹂<font color="Pink">POST</font>:Webブラウザに履歴が残らない(個人情報をサーバーに送る場合はPOSTを使用)<br>

- **<font color="HotPink">ステータスコード</font>** ••• Webサーバー内での処理結果(ステータス行に表示)<br>
﹂<font color="Pink">100番台</font>:HTTPリクエスト処理中(100)<br>
﹂<font color="Pink">200番台</font>:HTTPリクエスト正常処理(200)<br>
﹂<font color="Pink">300番台</font>:転送処理等、Webブラウザ側で追加処理が必要な時(URLが変更された場合等)(301/302/304)<br>
﹂<font color="Pink">400番台</font>:クライアント(Webブラウザ)のエラー(400/404)<br>
﹂<font color="Pink">500番台</font>:Webサーバーエラー(高負荷状態になった場合等)(500/503)

- **<font color="HotPink">メッセージヘッダー</font>** ••• HTTPメッセージに関する詳細な情報。リクエスト・レスポンスどちらにも使用<br>
﹂**<font color="Pink">ヘッダーフィールド</font>**:メッセージヘッダーは複数のヘッダーフィールドから成り立っている。<br>

- **<font color="HotPink">ヘッダーフィールド種類（独自で定義も可能）</font>**<br>
﹂<font color="Pink">一般ヘッダーフィールド</font>:リクエスト・レスポンス両方(接続状態・日付等)<br>
﹂<font color="Pink">リクエストヘッダーフィールド</font>:リクエストのみ(リクエスト先のサーバー名・Webブラウザの情報・直前のリンク先URL等)<br>
﹂<font color="Pink">レスポンスヘッダーフィールド</font>:レスポンスのみ(サーバー情報・リダイレクト先等)<br>
﹂<font color="Pink">エンティティヘッダーフィールド</font>:リクエスト・レスポンス両方（HTTPメソッドの一覧・コンテンツの周りの内容/使用言語など等）

- **<font color="HotPink">TCP</font>** ••• HTTPのデータのやりとりを行っている。
クライアントとサーバーが互いに通信できる状態か確認し  **<font color="Pink">コネクション</font>** と呼ばれる通信経路を確認しデータのやりとりを行う

- **<font color="HotPink">コネクション確立後の3回のやりとり流れ</font>**<br>
﹂<font color="Pink">クライアントからの接続要求(SYN)</font><br>
﹂<font color="Pink">クライアント確認応答＋サーバー接続要求(SYN＋ACK)</font><br>
﹂<font color="Pink">サーバーに対して確認応答(ACK)</font>

- **<font color="HotPink">SYN•••接続要求　ACK•••確認応答</font>**

## HTTP/1.1

- **<font color="HotPink">HTTPキープアライブ</font>** ••• TCPでコネクションを確立後、コネクションを継続して利用する方式（HTTPリクエストごとにコネクションを確立する必要がない）効率的

- **<font color="HotPink">HTTPパイプライン</font>** ••• HTTPリクエストに対してHTTPレスポンスを待つことなく複数のHTTPリクエストを送る機能。時間短縮できる。

## HTTP/2

- HTTP/2はGoogleが提案した **<font color="HotPink">SPDY</font>** と呼ばれる通信の高速化を目的としたプロトコルがベースになっている。2015年5月に標準化された。

- **<font color="HotPink">ストリームによる多重化</font>** ••• HTTPパイプラインはHTTPリクエストの順番通りにHTTPレスポンスを返さなければいけない制約があるため、Webページの表示速度が遅くなる問題点があった。HTTP/2は1つのTCPコネクション上に **<font color="Pink">ストリーム</font>** と呼ばれる仮想的な通信経路を複数生成しそれぞれのストリームでHTTPリクエストとHTTPレスポンスのやりとりができるのでレスポンスを順番通りに待つ必要がないため処理の待ち時間を短縮できるメリットがある。










- **<font color="HotPink">バイナリ形式</font>** <br> 
﹂**<font color="Pink">HTTP/1.1以前</font>**:テキスト形式でHTTPリクエストとHTTPレスポンスのやりとりをしていた。HTTP/1.1以前では、バイナリ形式でやりとりをする場合は一旦テキスト形式に変換する必要があった。**全てのデータが一度に送信されていた。**<br>
﹂**<font color="Pink">HTTP/2</font>**:HTTP/2ではより効率的にデータをやりとりするため、バイナリ形式そのままでやりとりができるようになった。変換処理＋Webブラウザ＋Webサーバーヘの負担を軽減。**フレームと呼ばれる単位に分割されバイナリ形式で送信**

- **<font color="HotPink">ヘッダー圧縮</font>** <br>
﹂**<font color="Pink">HTTP/1.1以前</font>**:ファイル等のテキスト形式ファイルのデータを圧縮転送することが可能。<br>
﹂**<font color="Pink">HTTP/2</font>**:上記＋ヘッダー情報も圧縮可能。HTTP/1.1以前はリクエストとレスポンスをする度に重複したデータ転送していたがHTTP/2ではヘッダー情報の中から差分だけを送信できる**HPACK**と呼ばれる圧縮方式を利用。データ転送量を削減。

- **<font color="HotPink">サーバープッシュ</font>** <br>
﹂WebブラウザからHTTPリクエストの内容を元にWebサーバー側で必要なファイルを判断し事前にWebブラウザに送信することが可能。(HTMLに画像を埋め込まれたいたら画像に対するHTTPリクエストを送信しなくても事前に画像データを転送してくれる)

## HTTPS

- **<font color="HotPink">SSL／TLSハンドシェイク</font>** ••• HTTPSの通信を開始するにはTCPコネクションが確立されたあと、以下手順で行われる(SSL／TLSハンドシェイク)<br> 
﹂**<font color="Pink">暗号化方式の決定</font>**<br>
﹂**<font color="Pink">通信相手の証明 </font>** ••• SSLサーバー証明書により確認<br>
﹂**<font color="Pink">鍵の交換</font>**<br>
﹂**<font color="Pink">暗号化方式の確認</font>**

## Cookie

- Webブラウザに保存(Cookieを送信することでWebサーバーは接続相手を認識できる)

- Cookie送信には**メッセージヘッダー**を利用<br>
(Webブラウザ:Cookieヘッダー　Webサーバー:Set-Cookieヘッダー *有効期限を設定できる)<br>

- セッションCookie ••• 有効期限が設定されていないCookie/Webブラウザ閉じるたびに削除<br>
(セキュリティの観点からショッピングサイトではセッションCookieを使用。)

## セッション

-　WebブラウザとWebサーバーのやりとりにおいて、一連の関連性のある処理の流れ

- WebサーバーでセッションIDを生成。Cookieに含めてWebブラウザに送信。次回以降、CookieにセッションIDを含めて処理を行うことでWebサーバーとのセッションを維持できる


## URI

- **<font color="HotPink">URI</font>** ••• リソースを識別するための記述方法<br>
(記述方式：スキームと呼ばれる識別子(http・ftpなど)＋：)<br>
﹂**<font color="Pink">URL</font>**:URIの内、リソースが存在する場所を示すもの<br>
﹂**<font color="Pink">URN</font>**:URIの内、リソースの名前を示すもの<br>

- **<font color="HotPink">リクエストURI</font>** ••• HTTPにおいてリソース特定の為にURIが利用。HTTPリクエストのリクエスト行のメソッドに続いて記述される。記述方法は以下。<br>
﹂**<font color="Pink">絶対URI形式</font>**:URIを全て含める<br>
﹂**<font color="Pink">相対URI形式</font>**:URIを一部を含める(通常は相対URI形式で記述)<br>

- **<font color="HotPink">パーセントエンコーディング</font>** ••• URIで使用できる文字は**予約文字と非予約文字**のみ。左記以外でURIを使用する場合は**パーセントエンコーディング**に変換する必要がある。<br>
(%の後に16進数で記述/使用する文字コードによりパーセントエンコーディングの変換結果が異なる)

# Chapter4

## HTML

- タグで表示< 要素名 >要素A 要素B 要素C（入れ子OK）</ 要素名>
- 要素は必要に応じ属性追加可　<要素名　属性名=属性 >　テキスト　</ 要素名>

## 画像

- **<font color="HotPink">jpeg</font>** <br>
﹂1677万色/データ圧縮:非可逆圧縮(人の目が感じにくいデータを削り圧縮/データを削るほど画質が荒くなる)

- **<font color="HotPink">png</font>** <br>
﹂1677万色/GIF特許問題によりW3Cにより開発/データ圧縮:可逆圧縮/データの整理を行い圧縮する＝データを削らないので劣化しない＋透過が扱える<br>

## XML

- HTMLもXMLも **<font color="HotPink">SGML</font>** というマークアップ言語を改良して生まれた<br>

- **<font color="HotPink">XML</font>** <br>
﹂目的に応じタグを自由に定義できる。柔軟に構造化された文書を作成できる。データをやりとりする際にデータを構造化することで扱い安くするために用いられている。<br>
﹂W3Cに標準化され勧告されている<br>
﹂**<font color="Pink">MathML(XMLで記述された数式)・SVG(XMLで記述された画像)</font>**<br>

- **<font color="HotPink">XHTML</font>** ••• HTMLをXMLの文法で再定義したもの<br>
﹂HTMLよりも書式が厳密<br>
﹂MathML・SVG 埋め込み可能<br>
﹂W3Cに標準化され勧告されている

## スクリプト言語

- 動的処理に使用

- **<font color="HotPink">ECMAScript</font>** •••　Mosilla Foundationと Microsoftが別々で実装を進めていたので、ECMAインターナショナルがJavaScriptを標準化したもの

- **<font color="HotPink">サーバーサイドスクリプトの開発言語</font>** <br> 
﹂**<font color="Pink">Perl</font>**:文法の自由度が高い <br>
﹂**<font color="Pink">PHP</font>**:Webで使用することが想定された言語。HTMLに埋め込み可能 <br>
﹂**<font color="Pink">Python</font>**:読みやすく簡潔。スクリプトの可読性高い。文法の自由度は低い <br>
﹂**<font color="Pink">Ruby</font>**:オブジェクト指向<br>

## DOM

- **<font color="HotPink">DOM(Document Object Model)</font>** ••• HTMLやXML文書を扱うための手法(API)。プログラムからHTMLやXMLの内容にアクセスするときはDOMを利用。各要素を容易に参照・制御できる<br> 
﹂**<font color="Pink">DOMツリー</font>**:対象となる文書の各要素を抽出し階層構造として扱う。文書の最上位の要素(HTML)を根として下位の要素が木の枝のように分かれていく木構造。木構造の枝葉の部分を **<font color="Pink">ノード</font>** といい、ノードをたどっていくことで目的のデータにアクセスし参照や編集を行う。<br>

- W3Cによって標準化され勧告されている(Level1~3)<br>
﹂Level1:XML1.0とHTML4.0xへの対応<br>
﹂Level2:XML1.0の拡張とXHTML1.0、スタイルシートのサポートなどの追加<br>
﹂Level3:XML1.0の拡張とDOMツリーの読み書き機能などの追加<br>

https://developer.mozilla.org/ja/docs/Web/API/Document_Object_Model


## JSON

- 構造化したデータを表す為のデータ記述言語/データを木構造で表現
- web上でのデータのやりとりによく使用<br>
﹂JavaScriptの書式にしたがっているのでJavaScriptで書かれたプログラムに読み込むことができる。XMLはDOMを利用する必要がある。JavaScriptをよく利用される Webの世界では選択されやすいデータ形式。

- **<font color="HotPink">XMLとJSONの違い</font>** <br>
﹂**<font color="Pink">XML</font>** (文字列しか表せない・データサイズ大きくなりがち・テキストの任意の場所にタグ付けできる)<br>
﹂**<font color="Pink">JSON</font>** (文字以外に数値や空データが扱える・データファイル小さめ・タグによるマーク付けがないため、人間に読みにくいデータ)

## フィード

- **<font color="HotPink">フィード</font>** ••• Webサイトなどの更新履歴を配信するためのファイル<br>
﹂**<font color="Pink">RSSとAtomが利用</font>**<br>
(RDFという記述言語がベースのRSS1.0とXMLをベースとしたRSS2.0が分裂して開発が進められていたがRSSの代わりになるものを開発しようとXMLベースのAtomも構築された)

- **<font color="HotPink">フィードリーダー(フィードアグリゲーター　もしくは　RSSリーダー　とも呼ぶ)</font>** ••• Web上のフィードを取得し管理するためのソフトウェア。更新情報をユーザーが閲覧できるように整形して表示する機能。

- **<font color="HotPink">ポッドキャスト</font>** ••• Webサーバー上に音楽や動画を配置しRSSを通してWeb上に公開することで音楽をインターネットで配信する手法。

## マイクロフォーマット

- **<font color="HotPink">マイクロフォーマット</font>** ••• HTMLやXHTMLで記述されたWebページに意味を埋め込む。<br>
﹂class属性/rel属性等に埋め込むことでセマンティックWeb(Webページの情報に意味を持たせる)を実現
﹂色々な団体で開発されており統一化されていない

## 音声・動画配信

- **<font color="HotPink">コーデック</font>** ••• 音声・動画データ圧縮をするソフトウェア<br>
﹂**<font color="Pink">エンコード</font>**:圧縮すること<br>
﹂**<font color="Pink">デコード</font>**:再生するために伸張すること

- **<font color="HotPink">配信方法</font>**<br>
﹂**<font color="Pink">ダウンロード配信</font>**:ファイルをダウンロード<br>
﹂**<font color="Pink">プログレッシブダウンロード配信</font>**:ファイルをダウンロードしながら再生(擬似ストリーミングとも呼ばれる)<br>
(ダウンロード/プログレッシブダウンロードはユーザー側に残るので著作権のあるデータ配信には向いていない)<br>
﹂**<font color="Pink">ストリーミング配信</font>**:ファイルを細かく分割し細切れにしたデータをユーザーに配信して再生。再生したデータは都度削除されるので著作権の問題は解決するが、ストリーミングサーバーを用意する必要がある。データが残らないので再生するたびにデータをダウンロードする必要がある。

## 検索エンジン

- **<font color="HotPink">ロボット型検索エンジン</font>** <br>
﹂クローラやロボットと呼ばれるプログラムが自動的にWebの情報を収集。クローラはリンクをたどってwebページを収集しデータベース化する。またデータベース化したページの更新・削除を行いデータベースを最新化する。クローラの動作を **<font color="Pink">クローリング</font>** という。情報の解析・抽出・分析可能なデータに変換する作業を **<font color="Pink">スクレイピング</font>** という。HTMLから要素を抽出するには **<font color="Pink">HTMLサーバー</font>** というプログラムが用いられる。検索エンジンのデータと、ユーザーの検索文字をマッチさせることでWeb検索を行う。

# Chapter5

- **<font color="HotPink">Webアプリケーション</font>** ••• ネットワークを介してWebブラウザ上で動作するアプリケーション。**<font color="Pink">3層構造(3層アーキテクチャ)</font>** になっている。

- **<font color="HotPink">3層構造(3層アーキテクチャ)</font>**<br>
﹂**<font color="Pink">プレゼンテーション層</font>**:ユーザーインターフェース(WebブラウザとWebサーバー)クライアントスクリプトはここで動作<br>
﹂**<font color="Pink">アプリケーション層</font>**:業務処理(アプリケーションサーバー/APサーバー)サーバーサイドスクリプトはここで動作<br>
﹂**<font color="Pink">データ層</font>**:データ処理や保管(データベースサーバー)

- 有効期限を設定する(コンテンツやデータは更新してもユーザーに新しい内容はレスポンスされないのを防ぐため)  **<font color="Pink"> 負荷分散・改修範囲</font>**  を限定することができる。(階層構造なのでプレゼンテーション層とデータ層がやりとりすることはない)

- **<font color="HotPink">MVCモデル</font>**<br>
﹂**<font color="Pink">Model</font>**:データと業務処理<br>
﹂**<font color="Pink">View</font>**:結果をユーザーに出力<br>
﹂**<font color="Pink">Controller</font>**:必要な処理をModel/Viewに伝える<br>
(各要素が相互にやりとり)


- **<font color="HotPink">3層アーキテクチャとMVC</font>** ••• MVCを表す部分は3層のアプリケーション層とデータ層。プレゼンテーション層はMVCモデルとユーザーの仲介を行う部分になる。

## Webサーバー

- **<font color="HotPink">冗長化</font>** ••• 複数のWebサーバーを用意し1台あたりの負担を軽減するとともに1台が故障しても他のWebサーバーでサービスを継続させること。 <br>

- **<font color="HotPink">サーバー機器の性能</font>** ••• リクエストが多く求められた時に必要なスペック <br>
﹂**<font color="Pink">Webサーバー(静的ページ)</font>**:ハードディスクの読み取り速度が速く、読み取りをサポートするメモリの容量が大きいことが求められる。<br>
﹂**<font color="Pink">APサーバー(動的ページ)</font>**:データ連携処理を早くするのにCPUの性能の高さが求められる。

## Webクライアント

- **<font color="HotPink">Webクライアント</font>** ••• Webサーバーとやりとりを行いWebシステムを利用するためのプログラム。<br>
﹂**<font color="Pink">Webブラウザ</font>**:Webクライアントとして最も利用されているもの<br>
﹂**<font color="Pink">クライアントプログラム</font>**:Webブラウザで利用できないものや十分に機能を活かせないものは専用のクライアントプログラムが用意される。 **<font color="Pink">専用クライアント、専用ブラウザ</font>** と呼ばれる。(デスクトップアプリ/スマホアプリ)

## アプリケーションサーバー(APサーバー)

- **<font color="HotPink">アプリケーションサーバー(APサーバー)</font>**<br> 
 ﹂Webサーバーから転送されてきたデータを受け取りサーバーサイドプログラムを実行。データ処理をしたらWebサーバーへ返す。<br>
﹂3層アーキテクチャのアプリケーション層に位置。プレゼンテーション層とデータ層の両方のやりとりを行う多機能サーバー。多機能で業務容量により負荷がかかるのでメモリ容量・CPU性能が重視される。<br>
﹂**<font color="Pink">セッション管理機能</font>**:APサーバーはクライアントごとにセッションIDを発行し通信データに含め同クライアントからの通信を1つのセッションと呼ばれる単位で判別し各クライアントごとのログイン状態を把握。クライアントがログアウトしたらセッションIDは破棄される。**ログインからログアウトまでの一連の通信が1セッション **<br>
﹂**<font color="Pink">トランザクション管理機能</font>**:セッション中で行われる一連の最小単位(予約手続きのようなやりとりが成功するまで完了しない処理は1リクエスト・レスポンス単位ではなくトランザクション単位で管理)

## データベース管理システム

- **<font color="HotPink">DBMS(データベース管理システム)</font>**<br> 
 ﹂APサーバーから検索や更新命令を受けデータ管理をする

- **<font color="HotPink">データベースサーバー(DBサーバー)</font>** ••• DBMSを搭載したサーバー

- データが複雑化したりデータ量が増えると負荷がかかるのでメモリ・CPU・ハードディスク読み込み速度が重要になる。

- **<font color="HotPink">冗長化</font>** ••• データ保全は非常に重要なため冗長化構成にしている。データベースは頻繁に更新されるため機器同士で扱うデータベースを最新の状態に同期にさせることが重要。ミラーリングとレプリケーションは冗長化。<br>
﹂**<font color="Pink">ミラーリング</font>**:データ更新命令を受けたプリンシパルDBMS(正)が複数のミラーDBMS(副)に対して同時に同じ更新を行うこと<br>
﹂**<font color="Pink">レプリケーション</font>**:データ更新命令を受けたマスタDBMS(正)
が更新の内容をスレープDBMS(副)に連携。スレープDBMSは任意のタイミングで更新を行う<br>
﹂**<font color="Pink">シェアードディスク</font>**:データベースを共有の機器(データストレージ)に持ち、複数のDBサーバー(DBMS)から更新。DBサーバーのみ冗長化となるのでデータベースを格納する機器には耐障害性の強い機器を採用する必要がある。正副の概念はない。

## キャッシュサーバー

- **<font color="HotPink">キャッシュサーバー</font>** ••• リクエストが多くなるとサーバーの負荷が増える。リクエストに対するレスポンスを覚えておけば毎回コンテンツを読み込む必要がなくなり負荷が減る。リクエストに対するレスポンスを覚えてく役割をするのが  **<font color="Pink">キャッシュサーバー</font>** 

- **<font color="HotPink">キャッシュ</font>** ••• リクエストに対するレスポンスの記憶<br>
﹂**<font color="Pink">コンテンツキャッシュ</font>**:文書・画像・動画のコンテンツのキャッシュ<br>
﹂**<font color="Pink">クエリキャッシュ</font>**:DBMSのデータ検索要求(クエリ)の結果のキャッシュ

- 有効期限を設定する(コンテンツやデータは更新してもユーザーに新しい内容はレスポンスされないのを防ぐため) 

- **<font color="HotPink">CDN</font>** ••• 世界各地に分散して配置されたキャッシュサーバーの集合体。あらかじめ大容量のコンテンツのキャッシュをWebサーバーから取得しておきCDN全体として1台のキャッシュサーバーのように動作する。リクエストに対しアクセス元からネットワーク的に最も近いサーバーが対応することで速くレスポンスを返せる。

## Ajax

- **<font color="HotPink">同期処理</font>** ••• クライアントとサーバーが交互に処理を行い、同調して通信を行うこと。WebサーバーからHTMLファイルを受け取って表示処理が行われるので時間がかかる＋送信するデータも多くなりサーバーに負荷がかかる。

- **<font color="HotPink">Ajax/非同期通信</font>** <br>
﹂クライアントサイドスクリプトとして動くJavaScriptが直接Webサーバーと通信を行う。取得したデータを用いて表示するHTMLを更新。
データやりとりはXMLが用いられる。HTMLそのものではやりとりしないので更新に必要なデータのみをやりとりできるので送信するデータも少なくサーバーに負荷がかからない。<br>
﹂Webブラウザの代わりにJavaScriptが更新を行うため、JavaScriptの機能を利用した **<font color="HotPink">非同期通信</font>** が可能。Webサーバーからのレスポンスを待つ間もクライアント側であるJavaScriptがレスポンスに左右されない箇所のHTMLを更新したりユーザーからの入力を受け付けることが可能。

## Webプログラミング

- **<font color="HotPink">Webプログラミング</font>** ••• プログラミング言語を利用しWebアプリケーションを開発すること<br>
﹂**<font color="Pink">サーバーサイドのプログラミング</font>**:SQL知識必要<br>
﹂**<font color="Pink">クライアントサイドのプログラミング</font>**:Ajax知識必要。専用クライアントの開発もクライアントサイドのプログラミングにあたる。

## WebAPI

- **<font color="HotPink">WebAPI</font>** ••• プログラムが直接サービスを利用するための窓口

- **<font color="HotPink">プログラム同士のデータやりとり</font>** <br>
﹂**<font color="Pink">XML-RPC</font>**:XMLを送信し処理実行を要求するプロトコル<br>
﹂**<font color="Pink">SOAP</font>**:XML-RPCの機能を拡張したもの。高機能で仕様が複雑なので利用が減っている<br>
﹂**<font color="Pink">REST</font>**:設計思想。シンプルな設計。JSONのような軽量なデータも利用できるので主流になっている

## マッシュアップ

- **<font color="HotPink">マッシュアップ</font>** ••• プログラムが複数のWebサービスを利用し利用し、処理結果を組み合わせて別のサービスを生み出すこと<br>
﹂元になるWebAPIの仕様変更があればサービスの修正が必要になってくる場合もある。またサービスが終了した場合は代替サービスに切り替えが必要になってくるので注意する必要がある。


## CGI

- **<font color="HotPink">CGIプログラム</font>** ••• 通常、Webサーバーはクライアントからのリクエスト受けると対応するコンテンツを返信するが **<font color="HotPink">CGIプログラム</font>** として定義されたコンテンツについてはそのままクライアントに返信せず、 **<font color="Pink">Webサーバー上で実行した時の結果を返す。</font>** 。APサーバーを用意しなくてもWebサーバー上でサーバーサイドスクリプトを実行できる。小規模な動的ページの作成に多く用いられている。

- **<font color="HotPink">データ渡し方</font>** <br>
﹂**<font color="Pink">コマンドライン引数渡し</font>**:CGIプログラムに直接渡す方法<br>
(http://●●.com/program.cgi?データ1+データ2  ?の後に+で繋いでいく)<br>
﹂**<font color="Pink">パス渡し</font>**:URLの階層構造に含めて渡す<br>
(http://●●.com/program.cgi/データ1/データ2  PATH_INFOという変数に格納)<br>
﹂**<font color="Pink">GET</font>**<br>
(http://●●.com/program.cgi?データ名1=データ1&データ名2=データ2  ?の後にデータを追加 QUERY＿STRINGという変数に格納)<br>
﹂**<font color="Pink">POST</font>**:URLとは別にデータを送る<br>
(POSTメソッドはURLを見ても送信データがわからないのでPOSTメソッドを利用するのが安全)


## サーバー間の連携

- CGIを利用せずにサーバーサイドスクリプトを動作させる場合の流れ<br>
(Webサーバー→APサーバー→サーバーサイドスクリプト)<br>

- サーバー同士でも、WebブラウザとWebサーバーの関係のようにWebサーバー(クライアント)/APサーバー(サーバー)という関係になる。APサーバーとDBMS間の連携も同様<br>

- **<font color="HotPink">サーバー同士の通信</font>** ••• リクエストを送信する側がクライアント/レスポンスを返す側がサーバー。IPアドレスとポート番号を指定してTCP/IP通信が行われる。サーバーやDBMSにもポート番号が割り当てられている。<br>
﹂別のサーバー機器に通信する場合は、IPアドレスとポート番号を指定して通信<br>
﹂同じ機器の場合は、IPアドレスとポート番号で指定するか、自ら稼働しているサーバー機器を表す特殊なIPアドレス「127.0.0.1」を指定して通信

- **<font color="HotPink">サーバー間の通信のプロトコル</font>** <br>
﹂**<font color="Pink">HTTP以外にだと「AJP」/「WebSocket」</font>**:Webサーバーはいずれかを用いてAPサーバーとやりとり。APサーバーの利用するプロトコルにWebサーバーが対応していないと通信できない<br>
﹂**<font color="Pink">ODBC(Open Database Connectivity)</font>**:APサーバーとDBMSで通信を行うためのAPI(DBMSは独自のプロトコルが採用されており、各APサーバーがすべてに対応するのが難しいため、ODBCを用いている)

## クライアントプログラムとWebサーバー

- **<font color="HotPink">クライアントプログラム</font>** ••• Webサーバーとどのように連携するかによって2つに分類<br>
﹂**<font color="Pink">Webビューアプリ</font>**: **<font color="Pink">Webview</font>** と呼ばれるブラウザ機能を呼び出しWebサーバーのコンテンツを表示する。Webサーバーがほとんど処理を行う。アプリ側はコンテンツだけを表示する。Webブラウザとのやりとりを前提としたWebサーバーのプログラムを活用しやすい。コンテンツ生成処理はWebブラウザ向けのものと共有し表示のみスマホに最適化するだけでアプリとすることができる。<br>
﹂**<font color="Pink">ネイティブアプリ</font>**:画像の生成や表示などの処理をアプリ内で行い、データのみをWebサーバーからAPIを通じてJSONなどで取得する。Webviewの制約にとらわれず自由に表示や操作方法が設定できる。スマホの機能や操作性を活かしたものが作りやすい。そのぶん、開発量が多くなりコストが高くなりがち。

- Webビューアプリ、ネイティブアプリのハイブリットの構成になることがほとんど。現状はネイティブアプリが主流。WebビューアプリもWebviewへの追加機能・JavaScriptの高速化などで遜色ないものが作れるようになりつつある。

