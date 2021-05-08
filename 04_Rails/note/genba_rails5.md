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

### User Task 紐付け

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

https://qiita.com/ozin/items/24d1b220a002004a6351  

https://www.sejuku.net/blog/26994
https://www.sejuku.net/blog/21300

`->`  は　ラムダ　（理解度…2％）  
ラムダはdefをインスタンスにしたもの

# Chapter5

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

**describe**  何について仕様を記述しようとしているのか（テスト対象）を記述。

**context**　テストの内容を「状況・状態」のバリエーションごとに分類するために利用。

**before**　前提条件 describe context内にbeforeを記述すると、describe contextの領域内のテストコードを実行する前にbeforeのブロック内に書かれたコードを実行。itが実行されるたびに新たに実行。次のitが実行されるまでにデータベースの状態は元に戻されるため、あるテストケースのせいで別のテストケースが影響を受けるということは基本的には起きないようになっている。

**it**　テストケース 期待する動作を文章とブロック内のコードに記述。

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

#### 失敗したSpecの場所  
` ./spec/system/tasks_spec.rb:69:in block (4 levels) in <top (required)> `   

**どのような理由で失敗したか**
```
Failure/Error:
       within '#error_explanation' do
         expect(page).to have_content '名称を入力してください'
       end
     
     Capybara::ElementNotFound:
       Unable to find css "#error_explanation"
```
（↑error_explanationというidを持つ要素が画面内に見つからなかった)


**`rails c -s(rails console --sandbox)` ロールバックされる。**

```
irb(main):004:0> exit
   (0.1ms)  rollback transaction
```   

https://qiita.com/takuyanin/items/d39e2a049409258f90f5

# Chapter6  

### routes  
https://railsguides.jp/routing.html  

railsガイドにも記載のあった`DSL`を至るところで見かける。サイトは以前ざっと見たがいまいち理解が出来なかったため、自分なりに改めて深掘り  
DSL
(Domain Specific Language）ドメイン固有言語

https://ysk-pro.hatenablog.com/entry/dsl  
https://techracho.bpsinc.jp/hachi8833/2018_06_06/56268  
https://logmi.jp/tech/articles/306406 

ある特定の問題の解決のみに提供されている言語
(いろんな言語でDSLは利用されている)

DSLは，メタプログラミングで使用  
https://gihyo.jp/admin/feature/01/dsl/0001

・メタプログラミングとは，ロジックを直接コーディングするのではなく，あるパターンをもったロジックを生成する高位ロジックを定義する方法のこと。主に対象言語に埋め込まれたマクロ言語によって行われる。  
・プログラムを生成するプログラムを書く

`ドメイン`：全体の中に定義される部分領域。  

↑いろんな部分領域でマクロ（自動化）として利用されているものと一旦理解。  

### ルーティング設定にもDSLが使用されている。

改めてREST RESTfulについて複数サイトを読み込み。

### REST  
https://qiita.com/190131start/items/49e2e9a42f49f17e45c6  
https://qiita.com/geshi/items/5275cc9d089105625c5f

- WEBのインフラを利用
- 情報の取得、作成、更新、削除といった操作は、すべてHTTPメソッドを利用すること。  
HTTPメソッド:取得「GET」、作成「POST」、更新「PUT」、削除「DELETE」となる。  
`sesson`などの状態管理は行わない。

### RESTful RESTの性質を持つルート設計  

https://www.slideshare.net/tkawa1/learning-rest-from-rails-style  
https://necojackarc.hatenablog.com/entry/2015/05/16/174024

本の注意書き  
コントローラ・アクション構造に忠実に対応したインターフェイスにするならばルーティングは非常にシンプルになる。Rails２.0よりも前のルーティングはそうなっていた。  
  
local3000、会社のサイト・RESTful設定をしていないhtmlのURLを確認し違いを理解。  

`URL URI` 違い(大分古いけどわかりやすい)  
https://webtan.impress.co.jp/e/2010/03/09/7539  


### ルート  
URLパターンにURLパターンの一意の名前をつけることでURLヘルパーメソッドが用意される。  
URLパターン名はルートごとというよりも、URLパターンごとにつけるものと理解しておく。
処理は`Rack`のレイヤーで行われる。  
https://railsguides.jp/rails_on_rack.html  
https://qiita.com/k0kubun/items/248395f68164b52aec4a

### RESTful  
REST(設計原則)に従うシステムのことを指す形容詞  

`resources resource`の違い  
https://qiita.com/wacker8818/items/1ba526fcbc73e065a511  

`resources`: ７つのアクションをリクエストするルーティングが設定
`resource` : indexとidつきのパスを外した残りのアクションをリクエストするルーティングが設定  

オプション  
`:only`: 指定したルートだけ作成  
`:except`: 指定したルート以外を作成  

`member collection new`  
https://railsguides.jp/routing.html  

`memberとcollection`の違い
https://qiita.com/k152744/items/141345e34fc0095217fe

`scope namespace module`の違い    
https://qiita.com/ryosuketter/items/9240d8c2561b5989f049  

### I18n

`ymlファイル`  
https://qiita.com/Yama-to/items/587544993fb62610528a  
https://magazine.rubyist.net/articles/0009/0009-YAML.html

`Active Record`  
https://railsguides.jp/active_record_basics.html

`Active Model`   persisted?  
https://railsguides.jp/active_model_basics.html  

`i18n/modelを1つのファイルで管理`
https://qiita.com/shimadama/items/7e5c3d75c9a9f51abdd5  

### 日時  

ActiveSupport::TimeZone クラスのオブジェクト：`UTC (協定世界時)`,`created_at`　　

リクエスト毎に異なるタイムゾーンの時刻を入出力したい場合はフィルタなどでTime.zoneの値を切り替えるのが良い

`スレッドセーフ`  
https://wa3.i-3-i.info/word12456.html  

`Time.current` `Date.current`は`Time.zone`が設定されている場合のみ利用。  
そうでない場合はTimeクラス・Dateクラスを利用する。  

### エラー処理  
どの例外がどのステータスコードになるかはRailsが決めている。  

### ログ
ログの特定のパラメータ値をマスク  
デフォルトではpasswordが設定  
`Rails.application.config.filter_parameters += [:password]`
`"password"=>"[FILTERED]"}`  

RailsのControllerでlogを出力する  
https://qiita.com/Kashiwara/items/f8a4030da6b17e96fabf

### Strong Parameters

`マスアサインメント機能`　モデルの機能で複数の属性を一括で代入することが出来る。  
```
task = Task.new(name: 'a', description: 'b')  
```

```
ない場合

task = Task.new  
task.name = 'a'
task.description = 'b'

```  

`マスアサインメント機能`のおかげで、コントローラーで受け取ったパラメータの一部を以下のように直接モデルに渡して複数の属性値を一括で割り当てることが出来る。  
`task = Task.new(params[:task])`  

上記では例外が走るので、`Strong Parameters`を設定する。  

```  
  def task_params
    params.require(:task).permit(:name, :description)
  end
```
※permitは入れ子構造にすることもできる。  
https://qiita.com/kymmt90/items/4ce8618ca8f537b2ef7e  

よくあるミス事例  
form画面に更新したい属性のフィールドを追加したが、permit属性を増やすことを忘れることがある。  
注意事項として画面上にはエラーも出ず、正しく動作しているように見えるがDBに一部の属性の値だけが反映されないという状況になりバグが発見しづらいので注意が必要。  
※自動テストをした方がいい。 

### CSRF(シーサーフ)  

CSRFを防ぐには同じアプリから生じたリクエストであることを証明するための`セキュリティトークン`を発行し照合する。
https://railsguides.jp/security.html  

Railsはこの発行と照合の仕組みを標準で用意している。  
トークンの発行はformから送られる情報にセキュリティトークンを含める方法で行わる。  
正しいトークンかどうかの照合はコントローラで行われる。  

標準で組み込まれているので設定等、記述は不要。  
﹂Rails5.1まではコントローラーApplicationControllerに`protect_from_forgery with: :exception`の記述が必要だったがRails5.2からはデフォルト設定になったので記述不要。

CSRF(シーサーフ)を防ぐ仕組みはGETリクエストには適用されない。  
POST(DELETE PATCH PUT)でリクエストを行う。  

`rails_ujs`  
https://www.inodev.jp/entry/2019/12/03/234210  

`fetch API`  
https://developer.mozilla.org/ja/docs/Web/API/Fetch_API  

### インジェクション    
Webアプリケーションに悪意あるスクリプトやパラメータを入力し、それが評価されるときの権限で実行させる攻撃。  

### XSS  
ユーザーに表示するコンテンツに悪意あるスクリプト(主にJavaScript)を仕掛けてコンテンツを表示したユーザーにスクリプトを実行させることで任意の操作を行う攻撃。  
オリジンによりユーザーの安全性が保たれる。  

Railsのビューではユーザーが入力した文字列をエスケープしてくれる。(無害なHTML形式/特殊文字に変換)
HTMLをエスケープされると困る場合は`raw`ヘルパー`String#html_safe`を使うとエスケープをスキップできる。  
Slimは`==`で値を展開するとHTMLはエスケープされない。  

許可するタグを指定したい場合は`sanitalize`ヘルパーを使用。  

### SQLインジェクション　
Railsではクエリメソッドに対してハッシュで条件を指定すると自動的に安全化のための処理を行ってくれる。　
クエリメソッドにSQLを直接書きたい場合はプレースホルダを利用する。  

### Rubyコードインジェクション  
`Object#send` あるオブジェクトのメソッドを任意に呼び出せる  
ユーザーからの入力をそのまま`send`に渡すのはNG  

`Kernel.#eval`にユーザーからの入力を渡すのはかなり危険。  
https://techacademy.jp/magazine/18717  

### CSP  
XSSやパケット盗聴といった特定の攻撃をブラウザ側で軽減する仕組み。  
RailsではHTTPヘッダーにCSPを組み込む為の機能が用意されていて、`content_security_policy.rb`に記述をする。  
通常はコメントアウトされている。 

CSPを既存のアプリに適用する場合は`content_security_policy.rb`の以下を許容する。  
スクリプトがポリシーに違反していても実行はブロックされない。指定したURLに違反内容が報告される。
`Rails.application.config.content_security_policy_report_only = true`  

既存のアプリでテストが通らなくなった。  
https://qiita.com/nisshy82/items/34cc97ba15f10d37c861  

設定方法(5.2)  
https://qiita.com/ryohashimoto/items/75f48fa5a3846c58f735   

### アセットパイプライン  

https://railsguides.jp/asset_pipeline.html  
https://www.transnet.ne.jp/2016/02/28/rails%E5%88%9D%E5%AD%A6%E8%80%85%E3%81%8C%E3%81%A4%E3%81%BE%E3%81%9A%E3%81%8Dcolnr%E3%80%8C%E3%82%A2%E3%82%BB%E3%83%83%E3%83%88%E3%83%91%E3%82%A4%E3%83%97%E3%83%A9%E3%82%A4%E3%83%B3/  

https://qiita.com/ttaka66/items/991a52081a92cb6c2738

JavaScript,CSS,画像などのリソース(アセット)を効率的に扱うための仕組み  
アセットパイプラインは`sprockets-rails`で提供される`Sprockets`の機能でデフォルトで有効になっている。  
開発者が書いたJavaScript,CSSを最終的にアプリで使う上で都合の良い状態にするためのパイプライン処理を行う。  
`ブラウザが読み取れる形式で実行速度が早くブラウザキャッシュに対して最適化される`  

CoffeeScript  
https://programming-world.net/language/coffeescript/  

https://re-engines.com/2019/08/26/rails-6%E3%81%AE%E5%A4%89%E6%9B%B4%E7%82%B9/  
https://qiita.com/taiteam/items/a37c60fc15c1aa5bb606
(分かりやすい)

処理内容の最後  
`ダイジェストの付与`  
コードの内容からハッシュ値を算出しファイル名の末尾に付与。  
コードが変更されればファイル名が変更される。ブラウザのキャッシュの影響で修正が反映されない問題を防ぐ。  


環境による挙動の違い  
development/アセットの連結が行われないのでファイル数分のlink,scriptタグが発生  
![development](https://gyazo.com/2fd7771393e7e92ad9a3866c127bdc73.png)  

production/Javascript・cssのファイルが１つずつ読み込み  
(デプロイしたら確認)  

`application.css`と`application.js`のマニフェストファイルはアセットパイプラインによって連結された結果のファイル。 

`application.css`の読み込み  
sassの場合 @import "bootstrap";
cssの場合 //=　
`※@importと//=は併用不可`

`application.js`の読み込み  
`//=` アセットパイプラインに指示を伝えるための特別な行として扱う。 
Sprockets独自のディレクトリ 

//= require_tree . 指定されたディレクトリ配下の全ファイルの内容を結合し、記述した位置に取り込み。  
`.`を指定すると`application.js`が配置されているディレクトリ配下が対象になる。  

※マニフェストで指定するファイル名はアセットの検索パスの設定を元に引き当てられる。  
デフォルト `app/assets lib/assets vendor/assets` パスの出現順で行われるため、`app/assets`が最も優先される。  

`app/assets lib/assets vendor/assets`  
https://blog.tanebox.com/archives/22/  
https://romantist.jp/blog/rails%E3%81%AEassets%E3%83%95%E3%82%A1%E3%82%A4%E3%83%AB%E3%82%92%E9%85%8D%E7%BD%AE%E3%81%99%E3%82%8B%E5%A0%B4%E6%89%80%E3%81%AB%E3%81%A4%E3%81%84%E3%81%A6/  

`vendor/assets`  
https://qiita.com/shimadama/items/cb50ff7fdd9e21431b7c  

アセットのパス検索対象確認。

```
rails c

irb(main):001:0> puts Rails.application.config.assets.paths
```  
View毎に適用するCSSを切り分ける  
https://qiita.com/Ryunosuke38/items/a8daf1278ef5ddd20785


### アセット関連の設定  

`config/initializers/assets.rb`: 全ての環境で読み込まれる。環境共通の設定を記述する。  
﹂`Rails.application.config.assets.version = '1.0'` 数値はダイジェストの生成に関わる。変更すると全てのアセットを強制的に期限切れにすることができる。  
﹂`Rails.application.config.assets.precompile += %w( admin.js admin.css )`  
(多分古いけど参考 https://qiita.com/prgseek/items/bf77c44189c55a7b41d8)

`node_modules`はyarn   

### 本番環境  
`プリコンパイル` : あらかじめアセットパイプラインを実行して静的ファイルを生成する処理。  
本番環境ではソースコードを更新してサーバを起動する際は、必ずプリコンパイルを実行する必要がある。  
`bin/rails assets:precompile`  
↓  
```
コンパイルされたjs,cssが作成される。
ls public/assets/
application-4fa33ed5d60452571bef883da345559df83411dd2f9f7c556455cb84fd836f1f.css
application-4fa33ed5d60452571bef883da345559df83411dd2f9f7c556455cb84fd836f1f.css.gz
application-da5f08fe9f516a1571725d0a928a1be5cac37ec5587d9394c90162df99520620.js
application-da5f08fe9f516a1571725d0a928a1be5cac37ec5587d9394c90162df99520620.js.gz
```  

railsによる静的ファイル
`public/assets/`に↑のプリコンパイルずみのファイルや404.htmlなどの`静的ファイル`配置されている。  
﹂開発環境・テスト環境では基本的にrailsによる静的ファイルの配信の仕組みを利用。

本番環境はNginxやApacheに静的ファイルの配信を担わせrailsは動的なコンテンツの配信に専念させる。 
(railsアプリのパフォーマンスを高めるため)  
この場合は、railsの静的ファイルを配信する昨日は不要になる。  
﹂railsには静的ファイルの配信機能をon/offにする設定があり、本番環境では基本off  

↑を変更するには(production環境をローカルPCで扱う場合)  
~/.bash_profileに以下を追記  
`export RAILS_SERVE_STATIC_FILES=1`  

production環境用のデータベース作成  
`RAILS_ENV=production bin/rails db:create db:migrate`  

productionモードだと`master.key`が必要  

productionモードでサーバ起動
`bin/rails s --enviroment=production` 
Capistranoなどのツールをデプロイして自動化するのが本筋  

`Credentials` 特定の方式で管理されるproduction環境用の秘密情報  
﹂`config/credentials.yml.enc`に記述(常に暗号化された状態で保存)  

`production`環境で起動された場合は`master.key`からキー情報を取り出して秘密情報を内部的に復号して利用。

キーはリポジトリ外で管理↓
```
.gitignore 
/config/master.key 
```

参考：環境ごとのアセットパイプラインの挙動   
https://numb86-tech.hatenablog.com/entry/2018/11/10/002439  

`Credentials`の中身確認。
```
bin/rails credentials:show
# aws:
#   access_key_id: 123
#   secret_access_key: 345
```

`Credentials`の編集    
```
EDITOR="code --wait" bin/rails credentials:edit
New credentials encrypted and saved.
```
https://qiita.com/zaki_zaki/items/dfc83a1fcd7dbc07af6b  

master.keyを紛失した場合は古いcredentials.yml.encファイルを削除してcredentials:editで新しく作成する。  
master.keyと暗号化したcredentialsは同じリポジトリに管理しない。  

`secret_key_base` 暗号化cookieや署名付cookieの整合性確認などに利用される秘密鍵。  
(productionモードで起動するために必要/development・testは指定不要)
外部に漏れた場合は再生成(`rails secret`)を利用  

`Encrypted` Credentialsの汎用化の機能
staging環境だけで使いたい秘密情報をCredentialsと分けて分かりやすく管理することもできる。  
CredentialsはEncryptedをベースに作られている。  
`bin/rails encrypted:show config/credentials.yml.enc`でも確認可能。  


# Chapter7  

### 確認画面  

form_with simple_format(改行)  
https://qiita.com/saik/items/5754aea53ec79a413cd7  

※hiddenで値を渡している。    

![confirm](https://gyazo.com/316b59cd44402d4d32c6018bbc4e0f39.png)  

### 検索フォーム  
https://pikawaka.com/rails/ransack  

検索ワードが含まれる　`_cont`   
完全一致　`_eq`  
ラジオボタン　`_lteq`  
同じかそれより大きい `_gteq`(SQL `>=`)  

https://pikawaka.com/rails/distinct  

![ransack](https://gyazo.com/dae53b9d604db0392642e62c2c079df8.png)

f.search_field(フォームの右に「x」ボタンが表示される)  
![f.search_field](https://gyazo.com/6f9154d3e9c6ec48f80abc06dccf69e2.png)  

「test」で検索  
![ransack](https://gyazo.com/07138ce797aed5914f05f710e2d7eb35.png)  

**ransackable_attributes指定無し**
```
[1] pry(#<TasksController>)> Task.ransackable_attributes
=> ["id", "name", "description", "created_at", "updated_at", "user_id"]
```

**ransackable_attributes指定**    
```
[1] pry(#<TasksController>)> Task.ransackable_attributes
=> ["name", "created_at"]
```

Strong Parametersを使うことで同じ効果を得ることも出来るが、ransackを利用する場合はparams[:q]には何が入ってもいいようにしておいて、モデル側でransackable_attributesなどで制御するやり方が一般的。(その方が管理しやすい)  
Strong Parametersを完璧に設定したり維持し続けるには労力がかかる。  

### 検索フォーム(ソート)  

▲▼なし  
`hide_indicator: true`  

### メイラー  

`gem install mailcatcher`  
bundlerでインストールすると不具合が発生するらしい  
https://kossy-web-engineer.hatenablog.com/entry/2018/11/22/132708  

mailcatcher  
https://github.com/sj26/mailcatcher/issues/430  


### ActiveStorage  

`bin/rails active_storage:install`
ActiveStorageが利用する２つのテーブルが出来る
- active_storage_blobs  
﹂`ActiveStorage::Blob`というモデルと紐付けされている。`ActiveStorage::Blob`は添付されたあファイルに対応するモデル。  
- active_storage_attachments    
﹂`ActiveStorage::Attachments`というモデルと紐付けされている。`ActiveStorage::Attachments`は`ActiveStorage::Blob`とアプリ内のモデルを関連付ける中間テーブル。`ActiveStorage::Blob`とは直接的にidのみで紐付け。  

https://qiita.com/itkrt2y/items/32ad1512fce1bf90c20b  

### ページネーション  
`kaminari`  
https://github.com/kaminari/kaminari  

ページ番号に対応するデータの範囲を検索する部分についてはkaminariのpageというスコープを使うだけで簡単に行うことが出来る。  
デフォルトだと1ページあたりの表示するレコード件数は25件。  
```
@tasks = @q.result(distinct: true).page(params[:page])
```  
- 現在どのページを表示しているのかの情報  
- 他のページに移動する為のリンク   
﹂`paginate`

- 全データが何件なのかといった情報  
﹂`page_entries_info`  

### Active Job  

`sidekiq`/`resque`/`delayed_job`:非同期実行を実現するgem。  

`sidekiq`  
https://en.wikipedia.org/wiki/Sidekiq

`redis`サーバーインストール
```
brew info redis 
```
`redis`サーバー立ち上げ
```
% redis-server
42785:C 03 May 2021 02:11:59.423 # oO0OoO0OoO0Oo Redis is starting oO0OoO0OoO0Oo
42785:C 03 May 2021 02:11:59.423 # Redis version=6.2.2, bits=64, commit=00000000, modified=0, pid=42785, just started
42785:C 03 May 2021 02:11:59.423 # Warning: no config file specified, using the default config. In order to specify a config file use redis-server /path/to/redis.conf
42785:M 03 May 2021 02:11:59.424 * Increased maximum number of open files to 10032 (it was originally set to 256).
42785:M 03 May 2021 02:11:59.424 * monotonic clock: POSIX clock_gettime
                _._                                                  
           _.-``__ ''-._                                             
      _.-``    `.  `_.  ''-._           Redis 6.2.2 (00000000/0) 64 bit
  .-`` .-```.  ```\/    _.,_ ''-._                                  
 (    '      ,       .-`  | `,    )     Running in standalone mode
 |`-._`-...-` __...-.``-._|'` _.-'|     Port: 6379
 |    `-._   `._    /     _.-'    |     PID: 42785
  `-._    `-._  `-./  _.-'    _.-'                                   
 |`-._`-._    `-.__.-'    _.-'_.-'|                                  
 |    `-._`-._        _.-'_.-'    |           https://redis.io       
  `-._    `-._`-.__.-'_.-'    _.-'                                   
 |`-._`-._    `-.__.-'    _.-'_.-'|                                  
 |    `-._`-._        _.-'_.-'    |                                  
  `-._    `-._`-.__.-'_.-'    _.-'                                   
      `-._    `-.__.-'    _.-'                                       
          `-._        _.-'                                           
              `-.__.-'                                               

42785:M 03 May 2021 02:11:59.425 # Server initialized
42785:M 03 May 2021 02:11:59.425 * Ready to accept connections
42785:M 03 May 2021 02:22:47.130 * 100 changes in 300 seconds. Saving...
42785:M 03 May 2021 02:22:47.130 * Background saving started by pid 43052
43052:C 03 May 2021 02:22:47.132 * DB saved on disk
42785:M 03 May 2021 02:22:47.233 * Background saving terminated with success
```

sidekiqインストール
※5系はgem 'sidekiq'だと最新バージョンになってエラーになる。
https://teratail.com/questions/235628

```
gem 'sidekiq', '~> 5.0'
```

sidekiq立ち上げ

```
saekoyamada@sy taskleaf % bundle exec sidekiq


         m,
         `$b
    .ss,  $$:         .,d$
    `$$P,d$P'    .,md$P"'
     ,$$$$$bmmd$$$P^'
   .d$$$$$$$$$$P'
   $$^' `"^$$$'       ____  _     _      _    _
   $:     ,$$:       / ___|(_) __| | ___| | _(_) __ _
   `b     :$$        \___ \| |/ _` |/ _ \ |/ / |/ _` |
          $$:         ___) | | (_| |  __/   <| | (_| |
          $$         |____/|_|\__,_|\___|_|\_\_|\__, |
        .d$$                                       |_|

2021-05-02T17:48:30.225Z 45926 TID-ovb7zns4y INFO: Running in ruby 2.5.1p57 (2018-03-29 revision 63029) [x86_64-darwin20]
2021-05-02T17:48:30.225Z 45926 TID-ovb7zns4y INFO: See LICENSE and the LGPL-3.0 for licensing details.
2021-05-02T17:48:30.225Z 45926 TID-ovb7zns4y INFO: Upgrade to Sidekiq Pro for more features and support: http://sidekiq.org
2021-05-02T17:48:30.225Z 45926 TID-ovb7zns4y INFO: Booting Sidekiq 5.2.9 with redis options {:id=>"Sidekiq-server-PID-45926", :url=>nil}
2021-05-02T17:48:30.237Z 45926 TID-ovb7zns4y INFO: Starting processing, hit Ctrl-C to stop
2021-05-02T17:48:44.248Z 45926 TID-ovb75m4ly SampleJob JID-9d2240b85b5702ea8862d19b INFO: start
2021-05-02T17:48:44.293Z 45926 TID-ovb75m4ly SampleJob JID-9d2240b85b5702ea8862d19b INFO: サンプルジョブを実行しました
2021-05-02T17:48:44.294Z 45926 TID-ovb75m4ly SampleJob JID-9d2240b85b5702ea8862d19b INFO: done: 0.045 sec
2021-05-02T17:49:13.069Z 45926 TID-ovb7st09m ActiveStorage::AnalyzeJob JID-51be4abe1ea2f84c3e957aba INFO: start
2021-05-02T17:49:13.296Z 45926 TID-ovb7st09m ActiveStorage::AnalyzeJob JID-51be4abe1ea2f84c3e957aba INFO: done: 0.227 sec
2021-05-02T17:49:13.389Z 45926 TID-ovb75m4ly SampleJob JID-7775e4a8e2b1fc3135b35f94 INFO: start
2021-05-02T17:49:13.390Z 45926 TID-ovb75m4ly SampleJob JID-7775e4a8e2b1fc3135b35f94 INFO: サンプルジョブを実行しました
2021-05-02T17:49:13.390Z 45926 TID-ovb75m4ly SampleJob JID-7775e4a8e2b1fc3135b35f94 INFO: done: 0.001 sec
```

#### 実行日指定

```
tasks_controllor.rb

#タスク作成を行った後でジョブを呼び出す
SampleJob .perform_later

#翌日午後に実行  
SampleJob.set(wait_untill: Date.tomorrow.noon) .perform_later  

#一週間後に実行  
SampleJob .perform_later
```

# Chapter8  

DOM : HTMLをJavaScript等のプログラムから利用する為の仕組み。  

e.currenteTargetとe.targetの違い    
https://www.javadrive.jp/javascript/event/index9.html  

### turbolinks  
https://techtechmedia.com/turbolinks-rails/#:~:text=Turbolinks%E3%81%A8%E3%81%AF%E3%80%81Rails4%E3%81%8B%E3%82%89,%E3%81%A7%E7%B5%84%E3%81%BF%E8%BE%BC%E3%81%BE%E3%82%8C%E3%81%A6%E3%81%84%E3%81%BE%E3%81%99%E3%80%82  

### Ajax    

`HTML`  
```  
<a data-confirm="タスク「test」を削除します。よろしいですか？" class="btn btn-danger" rel="nofollow" data-method="delete" href="/tasks/6">削除</a>  
```
↓    
`remote: true`追記  

`HTML`  
```
<a data-confirm="タスク「test」を削除します。よろしいですか？" class="btn btn-danger" data-remote="true" rel="nofollow" data-method="delete" href="/tasks/5">削除</a>
```  
`remote: true` →　HTML `data-remote="true"`

`remote: true`はbutton_toメソッドにも利用可能。  
`form_with`はデフォルトでAjaxを利用しているので、無効にする為、`local: true`オプションを指定している。  

### rails-ujs  
https://railsguides.jp/working_with_javascript_in_rails.html#rails-ujs-event-handlers  
https://www.inodev.jp/entry/2019/12/03/234210    
- ActionView添付のJavaScriptライブラリによって処理　　
- Ajaxリクエストを送信するだけでなく、関連イベントも発行  
﹂`ajax:success`もイベントの一つでAjaxによるレスポンスの成功=タスクの削除が成功(ステータスコード2××)の場合に処理。それ以外は`ajax:error`イベントが処理。taskleafアプリだと削除が成功するステータスコード204が返される。    
- HTMLのformを使ってリクエストを飛ばしていることと原理は同じ  
- 他、`method: :delete`、`data-confirm`(確認ダイアログの表示)、submitボタンの`data-disabled-with`(確認ダイアログの表示)のフォームの二重クリックを阻止する機能等ある。  


※JavaScriptのレスポンスを実行してタスクを削除する場合    

サーバ側はDOM要素としてどの削除ボタンがクリックされてAjax通信が発生したのかを知ることが出来ない。  
削除されたタスクのidの値はわかるのでDOM要素側にタスクのid情報を与えておく。  

```
views/tasks/index

tr id="task-#{task.id}"

views/tasks/destroy.js.erb

document.querySelector("#task-<%= @task.id %>").style.display = 'none';
``` 
![rails-ujs](https://gyazo.com/ea638243a26d70e9d58f67be1c5b4cbe.png)  

rails-ujsでAjax通信を行う場合、レスポンスとしてJavaScriptが返されて来ていれば、自動的に実行をしてくれる。  
(サーバ側で動的にJavaScriptを組み立てることが出来る)


### SJR(Server-generated JavaScript Responses)  
﹂サーバーサイドで生成したJavaScriptからなるレスポンス(画面更新までのプロセス)のこと  

- メリット 手軽。サーバサイドの資産を簡単に使える。フラグメントキャッシュの利用による高速化・環境の差異によらず一定のHTMLを表示出来る。  
(フラグメントキャッシュ https://qiita.com/suketa/items/eeae7e2196520323f694)
- デメリット　共有化がしづらい。ES2015(2016) をWebpackで互換性のあるJSに変換することが不可。  

`Elementのメソッド`
https://syncer.jp/Web/API_Interface/Reference/IDL/Element/insertAdjacentElement/  

### Turbolinks  
﹂ページ遷移を高速化する  
﹂`プレビュー機能` １度訪れたことのあるページを再度訪問した際、前回のキャッシュを一旦表示してからリクエストを送信し取得が完了したら新しいものに置き換える。見かけ上の画面遷移が一瞬で行われUXの向上に繋がる。※キャッシュされた古い画面が一時的に表示される点に注意。  
﹂HTTPリクエストメソッドはGETのみだが、他の`redirect_to`によるリダイレクトの際には動作を最適化する。  
﹂Railsとは独立したライブラリ。アプリを作成した時点でTurbolinksは有効になる。新規に導入作業を行う必要はない。アダプタがあればスマホでも利用可能。  
﹂`script`は、head要素内に記述する。bodyに記載すると、ページ遷移で画面が更新される際の不要な読み込みや評価が発生する可能性が高い。headであれば左記を避けることが出来る。ページ遷移先のhead要素内に新しいscriptがあった場合は、そのタイミングで1回だけ評価をする。  
﹂利用する際は、`application.js`、`application.css`を一つにまとめることが重要。高速化のポイントは共通アセットの読み込み頻度を減らすことにある。ページ毎に読み込むJSやCSSファイルが異なるようだと、ページ遷移のたびに再度読み込みが発生し高速化の効果を十分に得られない。 

`History API`を用いることでブラウザの戻るボタンなどの履歴操作や、その際のキャッシュの復元にも対応している。    
https://developer.mozilla.org/ja/docs/Web/API/History_API  

```
turbolinks:loadイベント：初回のページ表示時やTurbolinksによりページの状態が遷移した際に発火するイベント

document.addEventListener('turbolinks:load', function(){
  console.log('Loaded');
});
```
↓
![Turbolinks](https://gyazo.com/dfeebf41d206e72527db470a31d42696.png)  

他、ページ遷移の各タイミングのイベント、キャッシュの保存・復元に関するイベント、Ajaxリクエストに関するイベントなど  

※いずれも`document`オブジェクトに対して発火している。 

※Turbolinksの無効化

アプリ立ち上げ  
```
rails new app_name --skip-turbolinks
```

立ち上げ後に、無効化  
https://qiita.com/matsubishi5/items/c4c8a5df03ae630ae534  

### Yarn  
Facebookにより開発されたJavaScriptのパッケージマネージャ  

従来のJavaScriptライブラリの導入方法  
- vendorディレクトリ配下にコピーを配置  
﹂管理を自分で行う必要がある。ライブラリがバージョンアップしても気づきにくい。  
- gem利用  
﹂ライブラリがバージョンアップについてはgem側の対応を待つ必要があり最新版を利用できるとは限らない。  

```
bin/yarn add <パッケージ名>
```  

※開発環境のみで利用するパッケージをインストールする場合は --devを付与

addコマンドは以下の処理を行っている。  
- 指定されたパッケージをpackage.jsonに追加  
- 指定されたパッケージをインストール  

`package.json`    
﹂追加されたパッケージのことを`依存パッケージ`と呼ぶ。  
﹂`package.json`に記述された`依存パッケージ`を一括でインストール。`bin/yarn install`  
﹂ライブラリは`npmレジストリ`からインストール。  
﹂パッケージを削除。`bin/yarn remove <パッケージ名>`  

インストールしたパッケージは`node_modules`ディレクトリに配置。  

### Webpacker  
﹂Railsで開発 Rails5.1で追加  
﹂RailsでWebpackを使ってJavaScriptを管理することを簡単にしてくれるgem  
(Weboacker登場以前もWeboackをRailsアプリに導入することは可能だったがかなり手間。Weboackerは面倒な仕事を担ってくれる。)

導入方法  
﹂アプリ立ち上げ時に`--webpack`  
﹂既存アプリ`gem webpacker`で追加し必要なパッケージをインストール（`bin/rails webpacker:install`)  

app/javascript/packs/`application.js`  
﹂ `エントリポイント`(コンパイルを開始するファイル)になる。コンパイルの結果生成されるファイルに対応する存在でもある。 

Webpackerは`app/javascript/packs/`にあるファイルをエントリポイントとしてコンパイルを実行するのでインポートしたいJavaScriptファイルなどは`app/javascript/`配下の他のディレクトリに置く。  

本番環境のコンパイル  
﹂`webpacker:compile`という`Rakeタスク`で実行  
﹂Sproketsを導入している場合は`assets:precompile`で実行すれば良い。  

各環境でどのようにコンパイルするかの設定は`config/webpacker.yml`で設定。  

### React  
Facebookが開発しているJavaScriptのUIライブラリ。  
Reactは仮想DOMと呼ばれるデータ構造をメモリ上に持ち、ページ変化の差分のみをレンダリングすることで効率的にページを表示・更新することができる。  
