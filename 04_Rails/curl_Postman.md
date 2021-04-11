### WebはHTTPリクエストに簡単に送るためのツール、HTTPレスポンスをわかりやすく表示するためのツール  

```
class ApplicationController < ActionController::Base
  protect_from_forgery with: :null_session
  ﹂CSRF対策しているので外部からリクエストしても良いみたいな指示。
  ﹂本来は使用しない。session使用するアプリは絶対NG
  ﹂JSONを返すAPIで使用したりする場合もある。
end

セキュリティを一旦無効化  
https://qiita.com/kurashita/items/d1c8f6d79daec89c368c
```
`protect_from_forgery`  
﹂application_controllerが作られるときに自動で書き込まれる。   
https://qiita.com/KumatoraTiger/items/cc6a1107374cce500e6d  
※railsは自動でCSRF対策をしてくれる  
  
`form_for`は自動でCSRF対策用のトークンを埋め込んでくれる。  
﹂protect_from_forgeryによって、アクション実行前に正しいトークンが付随されているかをチェック 

トークン
https://qiita.com/dawn_628/items/5842bdbf92510637bca2#:~:text=%E3%83%97%E3%83%AD%E3%82%B0%E3%83%A9%E3%83%9F%E3%83%B3%E3%82%B0%E3%81%A7%E3%81%AF%E3%80%81%E3%82%BD%E3%83%BC%E3%82%B9%E3%82%B3%E3%83%BC%E3%83%89%E3%82%92,%E3%81%AE%E3%81%93%E3%81%A8%E3%82%92%E3%83%88%E3%83%BC%E3%82%AF%E3%83%B3%E3%81%A8%E3%81%84%E3%81%86%E3%80%82   

curlコマンドを使用してブラウザで入力するのと同じことが裏側で出来る。

curl オプション  
https://qiita.com/ryuichi1208/items/e4e1b27ff7d54a66dcd9  
https://qiita.com/takuyanin/items/949201e3eb100d4384e1  
http://www.mit.edu/afs.new/sipb/user/ssen/src/curl-7.11.1/docs/curl.html

-F(FormData) パラメータを一つづつ指定  
-d(form urlencoded) パラメータをまとめて指定   

送り方色々ある。  

Postman  
POST  bodyでパラメータ指定(form-dataかx-www-form-urlencoded)  

Request URL:エンドポイントにリクエストを投げている。  

form 送信ボタンを送信  
↓  
actionの指定先に飛ぶ  
inputとかselectとかtextareaのnameにパラメータを指定  

form_withは上記の内容を解釈してHTMLを生成してくれる。

session  
ページにアクセスした人と投稿した人をCSRFとcookieで検証している。

スマホ/vue.js/react.jsは
HTMLのサーバーから返す必要がない。データだけもらえればクライアントサイト側で描画される。  
railsはHTMLを返してレンダリングする。  

HTMLとして表示される理由
response headersの`content_type`で`text/html`が指定されているから  
`Content-Type: text/html; charset=utf-8` 

コントローラーに`response.headers["Content-Type"] = "text/plain"`て指定するとコードのテキストがレンダリングされる。(`Content-Type: text/plain`)  
他に  
﹂`render plain: "OK"` →　指定した"OK"がレンダリング(`Content-Type: text/plain; charset=utf-8`)    
﹂`render json: @モデルの変数` →　json形式でレンダリング(`Content-Type: application/json; charset=utf-8`)

curlやpostmanを使用することでブラウザ以外のところで書き換えができてしまう。なので、current_userの定義が必要。  

railsは「PATCH」「DELETE」のリクエストがない。「GET」「POST」のみ  

![Request](https://gyazo.com/d7d6888b04beda352ca0c08002ba24b9.png)  

Form Data  
_method: patch  ←紐づけられてリクエストが送られる。サーバーは左記を見てどの処理なのかを判断している。  
以前はPATCHやDELETEがなかったので_method: patchのように擬似的に表現している。  
リクエストはform_withが自動で出力してくれる。  
`<input type="hidden" name="_method" value="patch">`

![method](https://gyazo.com/3a401c4a3d0cccd49d272218047da142.png)  

↑編集には出るが新規作成には出ない(_methodも出ない)  

※form_withが`persisted?`メソッドでDBに永続化されているかどうかで判断している。  

model.persisted? 
true = 編集  
false = 新規

編集画面をnewにして試すと、`<input type="hidden" name="_method" value="patch">`がなくなる。  
`action="/articles/●"`→`action="/articles"`に変わる = persisted?がfalseになったから。  
エンドポイントだけで判断しない。  
