`rails new curl_example`  
↓

```
dyld: Library not loaded: /usr/local/opt/icu4c/lib/libicui18n.67.dylib
  Referenced from: /usr/local/bin/node
  Reason: image not found
sh: line 1:  5710 Abort trap: 6           node -v
sh: nodejs: command not found
Node.js not installed. Please download and install Node.js https://nodejs.org/en/download/
```
↓
5系で試しに作成。  
local3000は立ち上がるが、scaffoldのindexページでエラー。  
さすがにscaffoldで入力間違いは考えづらい。エラーログにもnodeぽいこと書いてあった。  

`node -v`したら入ってない。
  
https://info.yama-lab.com/mac%E3%81%A7npm%E3%81%A8%E3%81%8Bnode%E3%81%8C%E4%BD%BF%E3%81%88%E3%81%AA%E3%81%8F%E3%81%AA%E3%81%A3%E3%81%9F%E3%80%82%E3%82%A8%E3%83%A9%E3%83%BCdyld-library-not-loaded-usrlocalopticu4cliblib/  

https://qiita.com/SuguruOoki/items/3f4fb307861fcedda7a5  

https://mophie-blog.com/2020/07/26/rails-error-from-chapter8-node-reinstall/

↓

`brew reinstall node`  

↓

```
node -v
v15.12.0
```
入った

↓  

トライ  
`rails new curl_example`  

↓  

エラー
``` 
No receipt for 'com.apple.pkg.CLTools_Executables' found at '/'.

No receipt for 'com.apple.pkg.DeveloperToolsCLILeo' found at '/'.

No receipt for 'com.apple.pkg.DeveloperToolsCLI' found at '/'.

gyp: No Xcode or CLT version detected!
gyp ERR! configure error 
gyp ERR! stack Error: `gyp` failed with exit code: 1
gyp ERR! stack     at ChildProcess.onCpExit (/Users/saekoyamada/Documents/curl_example/node_modules/node-gyp/lib/configure.js:345:16)
gyp ERR! stack     at ChildProcess.emit (node:events:369:20)
gyp ERR! stack     at Process.ChildProcess._handle.onexit (node:internal/child_process:290:12)
gyp ERR! System Darwin 20.3.0
gyp ERR! command "/usr/local/Cellar/node/15.12.0/bin/node" "/Users/saekoyamada/Documents/curl_example/node_modules/node-gyp/bin/node-gyp.js" "rebuild" "--verbose" "--libsass_ext=" "--libsass_cflags=" "--libsass_ldflags=" "--libsass_library="
gyp ERR! cwd /Users/saekoyamada/Documents/curl_example/node_modules/node-sass
gyp ERR! node -v v15.12.0
gyp ERR! node-gyp -v v3.8.0
gyp ERR! not ok 

```

https://qiita.com/Jackson123/items/1468129c8c1e11764ef1  
https://qiita.com/baby-0105/items/18f6fbc073e160bf83ac  

↓

```
% sudo rm -rf $(xcode-select -print-path)
% sudo rm -rf /Library/Developer/CommandLineTools
% xcode-select --install
```  
↓  

トライ  
`rails new curl_example`  

↓

成功！

奇跡的にできた感覚値なので、改めて色々調べておきたいところ。  

--- 

【備忘】

Node.js 16  
https://forest.watch.impress.co.jp/docs/news/1320061.html

iterm2  
https://qiita.com/SuguruOoki/items/3f4fb307861fcedda7a5

とりあえずiterm2は使わない。
