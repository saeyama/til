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

```
【備忘】  
`rbenv install 2.5.8`  
↓
WARNING: ruby-2.5.8 is nearing its end of life.
It only receives critical security updates, no bug fixes.
(警告: ruby-2.5.8 は寿命が近づいています．
重要なセキュリティアップデートのみで、バグフィックスはありません。)
```

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

### 想定エラー

```
【Ruby versionsエラー】
rbenv: bundle: command not found

The `bundle' command exists in these Ruby versions:
  2.5.1
  2.6.6
  2.7.1

gem install bundler
↓
Fetching: bundler-2.2.15.gem (100%)
Successfully installed bundler-2.2.15
1 gem installed  
```
https://qiita.com/opiyo_taku/items/f4459ce4f42e18d08e28

```
【sqlite】バージョン相違エラーが出たらバージョン変更
Gem::LoadError: Error loading the 'sqlite3' Active Record adapter. Missing a gem it depends on? can't activate sqlite3 (~> 1.3.6), already activated sqlite3-1.4.2. Make sure all dependencies are added to Gemfile.

`Gemfile` sqlite3に追記 '~> 1.3.6'   
```
https://qiita.com/flowerhill/items/bb1e99bd87b151c0129b

↓  

`bundle install --path vendor/bundler`  

[DEPRECATED] The `--path` flag is deprecated because it relies on being remembered across bundler invocations, which bundler will no longer do in future versions. Instead please use `bundle config set --local path 'vendor/bundler'`, and stop using this flag
（なぜなら、このフラグはbundlerの起動を超えて記憶されることに依存しているからですが、bundlerは将来のバージョンではこれを行いません。代わりに、`bundle config set --local path 'vendor/bundler'` を使用し、このフラグの使用をやめてください。）

と出たが、成功したっぽい（今後注意）。

↓   

`bin/rails db:create`  

↓   
`bundle exec rails s`   
`bundle exec rails c`   

出来たら成功！

### 【備忘】
**bundle絡みのエラー**    
ターミナルでバージョン確認。  
Gemfile.lockと相違している可能性大。Gemfile.lockを削除せずにGemfile.lockに合わせてアンインストールしてインストールしても手順を踏み間違えるとエラーになる可能性高い。

参考サイト(とりあえず備忘で残す)    
https://qiita.com/MotohiroSiobara/items/c0d343a160cffc2902ef    
https://qiita.com/Miyayan/items/6f1a629bf8642f0a3f44  


**バージョン指定**  
https://qiita.com/homhom_star/items/0a401a1075060fe2de4b
