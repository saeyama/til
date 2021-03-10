![environment](https://gyazo.com/4d497969a3fded8b69e17ddb30532a39.png)

## Ruby インストール    

### 事前check

インストールされているRubyのバージョンを確認    
`rbenv versions`

インストール可能なRubyの最新一覧    
`rbenv install -l`

インストール可能なRubyの全一覧   
`rbenv install --list-all`    

### インストール
`rbenv install 2.●.●`

使えるように`rbenv rehash`

確認    
![environment](https://gyazo.com/288a26688a0950260b51e208f0113872.png)

## Rails インストール

### 事前check
`gem info -e rails`

### インストール
`rbenv install rails -v 5.●.●`

確認    
![environment](https://gyazo.com/3861e346ffd68595dc0065e31eef2a38.png)


### バージョン指定してアプリ新規作成
`rails _5.●.●_ new アプリ名`    

※バージョン指定してもGemfileに`~>`があるとGemfile.lock上では指定したバージョンの最新のものになる。   
※異なるバージョンで指定するとアプリの中身が変わるので、とりあえず5だったら５で新規作成。

### Rubyのバージョンをアプリのディレクトリでローカル指定
`rbenv local 2.●.●`

`less .ruby-version`で切り替わったことを確認。

---

`Gemfile`のruby・rails(~>があれば消す)のバージョンを指定のバージョンに書き換え。    

↓   
`Gemfile.lock`削除。   

↓   
`bundle install --path vendor/bundler`   

↓   
sqliteバージョン相違エラーが出たらバージョン変更
```
Gem::LoadError: Error loading the 'sqlite3' Active Record adapter. Missing a gem it depends on? can't activate sqlite3 (~> 1.3.6), already activated sqlite3-1.4.2. Make sure all dependencies are added to Gemfile.
```
`Gemfile` sqlite3に追記 '~> 1.3.6' 

参考サイト   
https://qiita.com/flowerhill/items/bb1e99bd87b151c0129b

↓   
`bundle install --path vendor/bundler`  

↓   
`bin/rails db:create`  

↓   
`bundle exec rails s`   
`bundle exec rails c`   
出来たら成功！


### 【備忘】
もし、bundle絡みのエラーが出たら、ターミナルでバージョン確認。
Gemfile.lockと相違している可能性大。Gemfile.lockを削除せずにGemfile.lockに合わせてアンインストールしてインストールしても手順を踏み間違えるとエラーになる可能性高い。

参考サイト(とりあえず備忘で残す)    
https://qiita.com/MotohiroSiobara/items/c0d343a160cffc2902ef    
https://qiita.com/Miyayan/items/6f1a629bf8642f0a3f44
