今後見直す為に、備忘として残す。

`bundle exec rspec spec/system/tasks_spec.rb`
↓
```
WARN Selenium [DEPRECATION] Selenium::WebDriver::Chrome#driver_path= is deprecated. Use Selenium::WebDriver::Chrome::Service#driver_path= instead.

（訳:  WARN Selenium [DEPRECATION] Selenium::WebDriver::Chrome#driver_path= は非推奨です。代わりに Selenium::WebDriver::Chrome::Service#driver_path= を使用してください。）
```
テストは通っているが警告が出る。  
そして、describeとcontextで定義した日本語が出てこなかったので上記が原因かと思い調べる。  

https://techtechmedia.com/chrome-web-driver/  
https://qiita.com/jnchito/items/f9c3be449fd164176efa    
https://qiita.com/MasaoSasaki/items/8ead24ba685acbb3d6c0

```
Gemfile

  # gem 'chromedriver-helper'
  gem 'webdrivers', '~> 3.0'

```
`bundle install`  
↓
```
Bundler could not find compatible versions for gem "rubyzip":
  In snapshot (Gemfile.lock):
    rubyzip (= 2.3.0)
  In Gemfile:
    selenium-webdriver was resolved to 3.142.7, which depends on
      rubyzip (>= 1.2.2)
    webdrivers (~> 3.0) was resolved to 3.9.4, which depends on
      rubyzip (~> 1.0)
Running `bundle update` will rebuild your snapshot from scratch, using only
the gems in your Gemfile, which may resolve the conflict.
```

↓  
とりあえず`Gemfile.lock`退避して、`bundle install`  
↓  
今度は`mimemagic`がエラーと出る。
↓  
`bundle update`,`bundle update mimemagic`等、色々試して、`Gemfile.lock`退避後、`bundle install`  
↓  
```
Bundler could not find compatible versions for gem "rubyzip":
  In snapshot (Gemfile.lock):
    rubyzip (= 2.3.0)
  In Gemfile:
    selenium-webdriver was resolved to 3.142.7, which depends on
      rubyzip (>= 1.2.2)
    webdrivers (~> 3.0) was resolved to 3.9.4, which depends on
      rubyzip (~> 1.0)
Running `bundle update` will rebuild your snapshot from scratch, using only
the gems in your Gemfile, which may resolve the conflict.
```
同じ  
↓  
rubyzipコンフリクトとのことなので、`gems`フォルダを確認。  
`rubyzip`２つファイルあり。2.3.0の方を一旦退避。`minemagic`もアップデートしたことで２つ出来てしまったので、古い0.3.5を一旦退避。  
`bundle install`  
↓  
成功！  

`bundle exec rspec spec/system/tasks_spec.rb`  
↓
```
WARN Webdrivers Driver caching is turned off in this version, but will be enabled by default in 4.x. Set the value with `Webdrivers#cache_time=` in seconds

（訳: WARN Webdrivers ドライバのキャッシングは、このバージョンではオフになっていますが、4.xではデフォルトで有効になる予定です。）

```

https://github.com/titusfortner/webdrivers/issues/118  

もぉ一度伊藤さんの記事を見て、下記確認  
https://github.com/titusfortner/webdrivers

```
gem 'webdrivers', '~> 4.0'
```
素直に、記事のまま`~> 3.0`にしていたので、`~> 4.0`に変更。  
もしかしたら`~> 3.0`だったから`rubyzip`エラーになったのか？  
(解決した意味が大分変わってくる)

一点、`Gemfile.lock`の`rubyzip (~> 1.0)Chromedriver.set_version`が気になる。  
`Chromedriver.set_version`がついているので`gems`にあった`chromedriver-helper-2.1.1`を退避。  

`bundle install`  
↓  
成功！

`Gemfile.lock`
`rubyzip (~> 1.0)Chromedriver.set_version`→`rubyzip (2.3.0)`になった。 

`bundle exec rspec spec/system/tasks_spec.rb`  
↓

```
An error occurred while loading ./spec/system/tasks_spec.rb. - Did you mean?
                    rspec ./spec/factories/tasks.rb

Failure/Error: require File.expand_path('../config/environment', __dir__)

LoadError:
  cannot load such file -- /Users/saekoyamada/Documents/taskleaf/vendor/bundler/ruby/2.5.0/gems/rubyzip-2.3.0/lib/zip.rb
```

https://ja.stackoverflow.com/questions/61284/rails5%E3%81%A7rspec%E5%AE%9F%E8%A1%8C%E6%99%82%E3%81%ABfailure-error%E3%82%A8%E3%83%A9%E3%83%BC%E3%81%8C%E5%87%BA%E3%81%BE%E3%81%99

他の記事にもあったが、多分見るべきところは
`Failure/Error: require File.expand_path('../config/environment', __dir__)`  
ではなくて  
`cannot load such file -- /Users/saekoyamada/Documents/taskleaf/vendor/bundler/ruby/2.5.0/gems/rubyzip-2.3.0/lib/zip.rb`

色々試して上記結論に至ったがこれ以上追うのはきついので試しに一回立ち上げ直し。  

`bundle exec rspec spec/system/tasks_spec.rb`  
↓  
警告は出なくなった。  
```
Capybara starting Puma...
* Version 3.12.6 , codename: Llamas in Pajamas
* Min threads: 0, max threads: 4
* Listening on tcp://127.0.0.1:50821
.

Finished in 1.92 seconds (files took 2.25 seconds to load)
1 example, 0 failures
```
https://qiita.com/jnchito/items/f9c3be449fd164176efa  
再インストールされているか確認。

`Webdrivers.logger.level = ::Logger::Severity::DEBUG`  
↓  
`DEBUG Webdrivers A working webdriver version is already on the system`  
（訳: 動作するウェブドライバーのバージョンがすでにシステム上にある）

記事と異なるがエラーぽくない。`rubyzip`が関係？  
コンフリクトのエラーにはなっていない。

RSpecの知識があまりない中では断定的なことは言えないしタイポの可能性もあるので一旦ここまでとする。  
知識をつけて今後比較検討予定。細かくブランチ切って管理しておく。


バージョン指定  
https://qiita.com/homhom_star/items/0a401a1075060fe2de4b  


Rails6  
https://qiita.com/Atelier-Mirai/items/89b8b38e897d64847c9a


別アプリを作成した時に警告でたのを確認。

![ERD](https://gyazo.com/a2eca9b4e8ab861b794738c6511a6739.png)
