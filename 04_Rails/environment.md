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

### Rubyのバージョンをアプリのディレクトリでローカル指定
`rbenv local 2.●.●`

`less .ruby-version`で切り替わったことを確認。
