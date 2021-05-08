## node.js バージョン管理 
※zsh前提  

### 事前確認  

```
% node -v #これをプロジェクト毎に変更出来るようにする。
v15.12.0

% npm -v
7.6.3

% yarn -v
1.22.10  

% which npm  
/usr/local/bin/npm  

% which node
/usr/local/bin/node  

% which yarn
/usr/local/bin/yarn

```

```
% brew list # node yarn あり         
==> Formulae
autoconf		libidn2			rbenv
docbook			libunistring		readline
docbook-xsl		m4			redis
gdbm			mpdecimal		ruby-build
gettext			mysql@5.7		shared-mime-info
glib			※node			sqlite
gnu-getopt		openssl@1.1		tree
heroku			pcre			wget
heroku-node		pkg-config		xmlto
icu4c			postgresql		xz
krb5			protobuf		※yarn
libffi			python@3.9
```
```
% npm ls -g #yarnはグローバル設定されていなかった。
/usr/local/lib
└── npm@7.6.3
```

### npm,yarn,node アンインストール  
https://qiita.com/wagi0716/items/94193a80502f9d81a9e0  
https://qiita.com/ucan-lab/items/a662532f1ce46f152c4e

```
% npm uninstall -g npm
removed 253 packages, and audited 1 package in 618ms
```

※注意  
yarnが残っている状態でnodeをアンインストールするとエラーになる。  

```
% brew uninstall node
Error: Refusing to uninstall /usr/local/Cellar/node/15.12.0
because it is required by yarn, which is currently installed.
You can override this and force removal with:
  brew uninstall --ignore-dependencies node
```

nodeをアンインストールするに当たって、オプション(`--ignore-dependencies node`)をつければ出来そうだが、yarnだけ残すメリットは？と思いyarnをuninstall。

```
% brew uninstall yarn
Uninstalling /usr/local/Cellar/yarn/1.22.10... (15 files, 5MB)
% which yarn
yarn not found

% brew uninstall node
Uninstalling /usr/local/Cellar/node/15.12.0... (3,283 files, 56MB)
saekoyamada@sy ~ % which node
node not found

とりあえず
% sudo rm -rf /usr/local/bin/npm
% sudo rm -rf /usr/local/bin/node
% sudo rm -rf /usr/local/bin/yarn

```
↓  

```
% brew list # node yarn 無くなった。
==> Formulae
autoconf		libffi			python@3.9
docbook			libidn2			rbenv
docbook-xsl		libunistring		readline
gdbm			m4			redis
gettext			mpdecimal		ruby-build
glib			mysql@5.7		shared-mime-info
gnu-getopt		openssl@1.1		sqlite
heroku			pcre			tree
heroku-node		pkg-config		wget
icu4c			postgresql		xmlto
krb5			protobuf		xz
```
↓  

```
% brew doctor
Please note that these warnings are just used to help the Homebrew maintainers
with debugging if you file an issue. If everything you use Homebrew for is
working fine: please don't worry or file an issue; just ignore this. Thanks!

Warning: Broken symlinks were found. Remove them with `brew cleanup`:

npm絡みのファイルがたくさん。指示に従い下記実行。

% brew cleanup
↓
% brew doctor 
Your system is ready to brew.

okey!
```

### バージョン管理設定手順(参考サイトまとめ)  

### `nodebrew`  

手順  
https://liginc.co.jp/513122  
（わかりやすい）  
+  
https://qiita.com/nqyutq/items/5bd8ecfc3598a43a4cd1

※注意  
homebrewでnodebrewをインストールしない方が無難。
（複数の記事にて確認）

http://webdev.jp.net/homebrew%e3%81%a7%e3%82%a4%e3%83%b3%e3%82%b9%e3%83%88%e3%83%bc%e3%83%ab%e3%81%97%e3%81%9fnodebrew%e3%81%a7%e3%81%afnode-js%e3%82%84np%ef%bd%8d%e3%81%8c%e4%bd%bf%e3%81%88%e3%81%aa%e3%81%84/

https://hisa-tech.site/yarn-install-stumble/  

https://qiita.com/muuuuminn/items/6477c8d839164e779996

※デメリット  
`nodebrew`は、`.node-version`でプロジェクト毎に管理出来ない。  

### `nodenv`  

今回は`nodenv`を入れる。
 
`anyenv`経由で入れることも出来るが、現時点で`rbenv`も入れてるし、他のenvを使う予定も今のところないので`nodenv`のみ入れることにする。(参考：https://qiita.com/kyosuke5_20/items/eece817eb283fc9d214f)  

手順  
https://qiita.com/282Haniwa/items/a764cf7ef03939e4cbb1  
（わかりやすい）  

新しいバージョンを入れたら`nodenv rehash`忘れず。(`●●denv`絡みは`rehash`する)

ついでに`nodenv`経由でインストールした`node`に`yarn`をインストール出来るように設定。
https://qiita.com/ttokdev/items/3547587b0494dd624901  

```
.zshrc

eval "$(rbenv init -)"
export PATH="~/.rbenv/shims:/usr/local/bin:$PATH"
export PATH="/usr/local/opt/mysql@5.7/bin:$PATH"
export PATH="$HOME/.nodenv/bin:$PATH"  #追加
eval "$(nodenv init -)"  #追加
```
```　
% nodenv versions       
  12.22.1
* 15.14.0 (set by /Users/saekoyamada/.nodenv/version) #グローバル設定
```
```
% which npm
/Users/saekoyamada/.nodenv/shims/npm

% which node
/Users/saekoyamada/.nodenv/shims/node

% which yarn
/Users/saekoyamada/.nodenv/shims/yarn
```
```
% npm ls -g
/Users/saekoyamada/.nodenv/versions/15.14.0/lib
├── npm@7.7.6
└── yarn@1.22.10
```  

### アプリに指定のバージョンを設定。  

```
taskleaf % nodenv local 12.22.1  
```  
↓  

`.node-version`が出来る。  

↓

```
taskleaf % node -v                               
v12.22.1
```
