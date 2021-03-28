# 新規登録・ログイン・ログアウト

## 新規登録

### has_secure_password

Userモデル作成時、name等と共にパスワード設定をする場合は、属性名はpassword_digestで設定(passwordではない)   

password_digest   
﹂has_secure_passwordを使った時の命名ルール

digest：元に戻すことができない一方的な変換(ハッシュ化)を行った文字列のこと。パスワードのdigestは同じパスワードから生成すると常に同じになる。


利用する意味    
・pwの漏洩を防ぐ（pwそのものをdbに登録するのは危険）  

### 登録したpwをdigestへ保存する

- gem 'bcrypt' 入れる

-  Use model　`has_secure_password`　かく  
﹂dbのカラムに対応しない属性が追記される
「password」「password_confimation」

password,password_confimationが登録されると、password_digestにハッシュ化されてdbに保存される。    
﹂復元は不可   
﹂pwの確認には使える

### ユニーク制限

userモデル作成時に、emailにユニーク制限する場合。

`t.index :email, unique: true`

https://teratail.com/questions/121938

※メールの衝突のたびにデータベースエラーになるのでmodel側にもバリデーション設定必要    

` validates :email, presence: true, uniqueness: true`

## ログイン

- ログイン = セッションというリソースを作る
- sessionメソッド Railsにもともと定義されているメソッド。暗号化して保存するためのメソッド。

`routes`

```
  get    '/login',   to: 'sessions#new'
  post   '/login',   to: 'sessions#create'
  delete '/logout',  to: 'sessions#destroy'
```

`session_controller`

```
  def create
    user = User.find_by(email: session_params[:email])

    if user&.authenticate(session_params[:password])
    ** もしくはif user && user.authenticate(params[:session][:password])　**
    # https://teratail.com/questions/143927?sort=3
    
      session[:user_id] = user.id
      redirect_to root_path, notice: 'ログインしました。'
    else
      render :new  
    end
  end

  private
  def session_params
    params.require(:session).permit(:email, :password)
  end  
```
params.require(:session).permit(:email, :password)  
↓  

<input class="form-control" id="session_email" type="text" `name="session[email]`">

<input class="form-control" id="session_password" type="text" `name="session[password]`">

### authenticate 
Userクラスにhas_secure_passwordと記述した時に自動で追加された認証のためのメソッド。
引数で受け取ったパスワードをハッシュ化して、その結果がUserオブジェクト内部に保存されているdigestと一致するか調べる。    

流れ。  
emailでユーザー検索  
↓  
見つかった場合はパスワード認証をauthenticateメソッドを使って実行。  
↓  
認証に成功したらセッションにuser_idを格納。  

eamilでユーザーデータが見つからない場合はuserはnilになるので、`&.`を使用。  

session[:user_id]   
﹂誰もログインしていない:nil
﹂誰かログインしてる:ログイン中のユーザーのIdが格納

### helper_method

ログイン後のユーザーの取得
User.find_by(id: session[:user_id])   

※findでも可能だがnilを渡した時はエラーになる。セッションが消えているときは例外が走る。

↓

current_user設定

```
  helper_method :current_user
  全てのビューから利用可能

  def current_user
    @current_user ||= User.find_by(id: session[:user_id]) if session[:user_id]

    #=> @current_user = @current_user || User.find_by(id: session[:user_id])
   
  end
　全てのコントローラーから利用可能
```

## ログアウト

ユーザーidだけ消す    
session.delete(:user_id)

セッション内の情報を削除  
reset_session


```
skip_before_action :login_required

↑これつけないとサーバー立ち上がらない302

```
