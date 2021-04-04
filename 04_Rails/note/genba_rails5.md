# Chapter2

### database.ymlz:データベースと接続する為の設定ファイル。YAMLという形式で記述。

#### コネクションプール:データベースへ接続するときに接続状態を保持しておきそのコネクションを再利用することでデータベースへの接続を短縮する機能のこと。

### YAML 
キー：値の形でハッシュ表現。インデントを使って入れ子構造も可能。
```

&エイリアス名　：親のキーとなるエイリアスを設定

default: &default
  adapter: sqlite3
  pool: <%= ENV.fetch("RAILS_MAX_THREADS") { 5 } %>
  timeout: 5000


<<: *エイリアス名　：エイリアスを参照したい箇所

development:
  <<: *default
  database: db/development.sqlite3  
```
---

`exec` gemfileのバージョンを指定する時に付ける  
https://qiita.com/d0ne1s/items/fa2dafcee02e963fe997   


# Chapter3

**Q**

#### config.i18n.default_locale = :jaの記述箇所

config/initializers/locale.rb   
or  
config/application.rb   

**A**  
結論、どっちでもいいけど、application.rbの記述量が他で増えると重くなるので、config/initializers/locale.rbに記述するようにする。

# Chapter4

- 1つのマイグレーションファイルが１つのバージョンとして扱われる
- Mysqlはエラーになっても一部のデータベースではロールバックされず中途半端な状態になるので注意。


###  カラム名
:data (~「on」付けることが多い)  
:datetime (~at ex:updated_at)  
（過去動画参照）


add_column    
﹂単純にカラムを追加

change_column   
﹂もともとあるカラムを変更   

change_columnの注意点   
limitをつけるようなマイグレーションを追加する場合は
up downメソッドで作成する必要がある。  
downメソッドを記述する意味  
﹂change_columnではバージョンを戻す処理が出来ない。    

結論、設計をちゃんとしておくことが大事。    

データベースではnull同士は常に異なる値だと見なされる（ユニークインデックスを作成しているカラムの値がNULLのレコードは複数存在することができる）    

modelの登録・更新の為のメソッドがsave   

検証 valid?

save! 検証エラー時にfalseを返すのではなく例外を発生させるメソッド   
基本的に登録・更新が成功するはずと信じている場面ではsave!を使った方が予期せぬ失敗を防ぐことができる。   

意図的に検証をスキップすることもできる。あまり使わない。意図的にデータベースに登録・更新をしたいとき    
```
task.save(validate: false)
```

エラー検証    
rails c   
```
task.errors
=> #<ActiveModel::Errors:0x00007fa036130f50 @base=#<Task id: nil, name: nil, description: nil, created_at: nil, updated_at: nil>, @messages={:name=>["を入力してください"]}, @details={:name=>[{:error=>:blank}]}>

メッセージの内容をとる
task.errors.full_messages
=> ["名称を入力してください"]

データベースに保存済かどうかを確認
task.persisted?
=> false
```

```
- if task.errors.present?
  ul#error_explanation
    - task.errors.full_messages.each do |message|
      li= message
      
present? → 全てのデータを取得する
any? → 1件のみデータを取得する
```
https://www.sejuku.net/blog/73197

```
validates 標準 複数形

validate カスタム 単数形
```

### コールバック  
後で呼んでほしい処理をあらかじめ指定しておく仕組みを指すプログラミング用語。モデルオブジェクトの重要なイベントの前後に、任意の処理をいくつでも呼び出せる仕組みになっている。    

 ### ActiveRecordモデルのコールバック　検証・登録・更新・削除   
 - before
 - after
 - around


### セッションの保管場所
デフォルトはCookie。その他、railsのキャッシュ・データベース・memcahed

### Cookieとキャッシュの違い
https://www.geekly.co.jp/column/cat-webgame/1910_001/
- Cookie ユーザーのユニークデータを保存
- キャッシュ　一度アクセスしたWebページを保存

### マイグレーションファイル
nilじゃなくてnull データベースに登録するから。    

### has_secure_password
﹂gem 'bcrypt', '~> 3.1.7' 入れる必要あり  
﹂modelに設置

追記するとデータベースのカラムに対応しない以下の属性が追加  
﹂password  
﹂password_confimation

管理系コントローラ他にもある（Admin::BaseController）


### pathとurl違い  
https://qiita.com/bSRATulen2N90kL/items/a183c501f56c4068584c


### ログインする　= セッションというリソースを作る

新規登録はUser    
ログインはsession

コントローラが扱う概念的なデータを「リソース」と表現することがある    
リソースとしてのセッションはあるユーザーとしてのアプリケーションとのやりとり    
ログアウトはdestroy   


session routes 
```
  get    '/login',   to: 'sessions#new'
  post   '/login',   to: 'sessions#create'
  delete '/logout',  to: 'sessions#destroy'
```

### form_withのscopeについて
https://qiita.com/akilax/items/f36b13f377f7e442bc73

session_controller

&. →　&&  
https://qiita.com/yoshi_4/items/e987b698c1978d248cfc

### authenticate Userクラスにhas_secure_passwordと記述した時に自動で追加された認証のためのメソッド。
引数で受け取ったパスワードをハッシュ化して、その結果がUserオブジェクト内部に保存されているdigestと一致するか調べる。    
- 認証成功 Userオブジェクト true返す
- 認証失敗 false 



### ユニーク制限

`t.index :email, unique: true`

https://teratail.com/questions/121938

※メールの衝突のたびにデータベースエラーになるのでmodel側にもバリデーション設定必要    

` validates :email, presence: true, uniqueness: true`

#### find nilを渡した時はエラーが発生する 例外を発生させないようにするにはfind_byを利用する。

### User Tasl 紐付け

add_reference  
https://railsdoc.com/page/add_reference


現在ログインしているユーザーの管理権限を確認。
current_user.admin?

一番最初の管理者はrails consoleから作成　or seedから作成。

create create!の違い
https://qiita.com/keisukesaito/items/20adc17112d6d0bcf9d5

User.where(admin: true).`to_sql`   
﹂生成予定のSQLを見ることができる。

### scope クエリー用のカスタムメソッド 

https://www.sejuku.net/blog/26994
https://www.sejuku.net/blog/21300

`->`  は　ラムダ　（理解度…2％）  
ラムダはdefをインスタンスにしたもの

## Chapter5

- テストは、環境のバージョンアップやリファクタリングの必須条件

### テスト駆動開発（TDD）
https://www.qbook.jp/column/20181009_713.html

### RSpec
テスティングフレームワーク

### Capybara  
﹂E2E(End-toEnd)テスト用フレームワーク   
　テスティングライブラリを合わせて使用  
﹂JSの動作もテスト可能

### Factry Bot
﹂テスト用データをサポートするgem    
https://qiita.com/piggydev/items/32717b6c382272e2134e
https://qiita.com/morrr/items/f1d3ac46b029ccddd017

`DSL`を使って似たデータを効率よく定義することができる  
https://gihyo.jp/admin/feature/01/dsl/0001   
https://www.fenet.jp/infla/column/technology/dsl%E3%81%A8%E3%81%AF%EF%BC%9F%E5%9F%BA%E7%A4%8E%E7%9F%A5%E8%AD%984%E3%81%A4%E3%82%92%E3%82%8F%E3%81%8B%E3%82%8A%E3%82%84%E3%81%99%E3%81%8F%E8%A7%A3%E8%AA%AC%EF%BD%9C%E5%9B%9E%E7%B7%9A%E3%81%AB/

systemspec  
https://qiita.com/jnchito/items/c7e6e7abf83598a6516d


Headless Chrome  
https://developers.google.cn/web/updates/2017/04/headless-chrome?hl=ja

- テストケースを整理・分類する　describe, context
- テストコードを実行する　before, it  

### describe  何について仕様を記述しようとしているのか（テスト対象）を記述

### context　テストの内容を「状況・状態」のバリエーションごとに分類するために利用。

### before　前提条件 describe context内にbeforeを記述すると、describe contextの領域内のテストコードを実行する前にbeforeのブロック内に書かれたコードを実行。itが実行されるたびに新たに実行。次のitが実行されるまでにデータベースの状態は元に戻されるため、あるテストケースのせいで別のテストケースが影響を受けるということは基本的には起きないようになっている。

### it　テストケース 期待する動作を文章とブロック内のコードに記述。

```
describe
  describe
    before

    context
      before
      it
      it

    context

describe
```

test環境のデータベースをテスト専用で用いることになっている。  
`Factory(ファクトリ)`　データを作成することを簡単にする仕組み  

テストデータ  
FactoryBotでデータを作成するための「テンプレート」を用意しておく。
beforeなどで FactoryBotのテンプレートを利用してテスト用データベースにテストデータを投入。

次のテストケースに進む前にデータ状態を戻す処理はSystem specが適切に処理。

ファクトリをモデル毎に作成。

```
FactoryBot.define do
  factory :user do
    name {'テストユーザー'}
    email {'text1@example.com'}
    password{'password'}
  end
end
```
`:user` 左記からUserクラスを自動で類推。  
ファクトリ名とクラスが異なる場合には`:class`オプションでクラスを指定することができる 

FactoryBot:属性の名前を記述。パスワード password{ ‘password’ }

```
  factory :admin_user, class: User do
  ...
```

```
FactoryBot.define do
  factory :task do
    name {'テストを書く'}
    description {'準備'}
    user
  end
end
```
`user` 左記から自動類推。  
関連名とファクトリ名が異なる場合は下記で記述可能  
```
  association :user, factory: :admin_user
```  

```
user_a = FactoryBot.create(:user, name: 'ユーザーA', email: 'a@example.com')
FactoryBot.create(:task, name: '最初のタスク', user: user_a)
```

タスクをローカル変数に代入しないのは後で使う用途がないから。
userオプションの指定がなければTaskオブジェクトを作る際に、新しいUserオブジェクトを合わせて作成・登録する。

:taskというファクトリを利用してTaskオブジェクトを生成する際に、同時に:userというファクトリを利用して作られたUserオブジェクトがuser関連に入った状態を作成してくれる。  

spec/  
|_factories(仮のデータをセット)  
|_sytem(テスト)


createの代わりにbuildを使用すればデータベースに登録する前で止めて未保存のオブジェクトを得ることができる。  

Capybaraはブラウザ上で操作を行うためのメソッド群を用意してくれている。  
https://qiita.com/morrr/items/0e24251c049180218db4  
https://qiita.com/sogu/items/4370e8e54751899d5cad  

```
it 'ユーザーAが作成したタスクが表示される' do
        expect(page).to have_content '最初のタスク'
      end
```
・have_contentの部分は「マッチャ（Matcher）」  

`let`  
オブジェクト定義: `let(定義名){定義の内容}`  

定義した位置に応じて確実に実行してほしい場合は`let!`を使用。

letのブロックが実行されるタイミングはletが初めて呼ばれた時。  
﹂定義が初めて呼び出されたときに評価されることを`遅延評価`とよぶ。

`login_user` というletを describe/contextの中で定義した場合は、外側でも内側でも`login_user`を変数のように呼び出して使うことができる。

itを共通化する場合は`shared_examples`という仕組みを利用。

ex／5 examples → it 5件実行

### 失敗したSpecの場所  
####  #./spec/system/tasks_spec.rb:69:in `block (4 levels) in <top (required)>'   

### どのような理由で失敗したか
```
Failure/Error:
       within '#error_explanation' do
         expect(page).to have_content '名称を入力してください'
       end
     
     Capybara::ElementNotFound:
       Unable to find css "#error_explanation"
```
（↑error_explanationというidを持つ要素が画面内に見つからなかった)


### `rails c -s(rails console --sandbox)` ロールバックされる。

```
irb(main):004:0> exit
   (0.1ms)  rollback transaction
```   

https://qiita.com/takuyanin/items/d39e2a049409258f90f5
