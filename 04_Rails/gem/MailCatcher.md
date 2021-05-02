https://mailcatcher.me/  
https://github.com/sj26/mailcatcher

`gem install mailcatcher`  

↓  

```
Building native extensions. This could take a while...
ERROR:  Error installing mailcatcher:
        ERROR: Failed to build gem native extension.

    current directory: /Users/saekoyamada/.rbenv/versions/2.5.1/lib/ruby/gems/2.5.0/gems/thin-1.5.1/ext/thin_parser
/Users/saekoyamada/.rbenv/versions/2.5.1/bin/ruby -I /Users/saekoyamada/.rbenv/versions/2.5.1/lib/ruby/site_ruby/2.5.0 -r ./siteconf20210502-4896-uj5olr.rb extconf.rb
checking for main() in -lc... yes
creating Makefile

current directory: /Users/saekoyamada/.rbenv/versions/2.5.1/lib/ruby/gems/2.5.0/gems/thin-1.5.1/ext/thin_parser
make DESTDIR\= clean

current directory: /Users/saekoyamada/.rbenv/versions/2.5.1/lib/ruby/gems/2.5.0/gems/thin-1.5.1/ext/thin_parser
make DESTDIR\=
compiling parser.c
parser.rl:112:17: warning: comparison of integers of different signs: 'long' and 'unsigned long' [-Wsign-compare]
  assert(pe - p == len - off && "pointers aren't same distance");
         ~~~~~~ ^  ~~~~~~~~~
/Library/Developer/CommandLineTools/SDKs/MacOSX.sdk/usr/include/assert.h:93:25: note: expanded from macro 'assert'
    (__builtin_expect(!(e), 0) ? __assert_rtn(__func__, __FILE__, __LINE__, #e) : (void)0)
                        ^
parser.rl:142:7: error: implicit declaration of function 'thin_http_parser_has_error' is invalid in C99 [-Werror,-Wimplicit-function-declaration]
  if (thin_http_parser_has_error(parser) ) {
      ^
parser.rl:142:7: note: did you mean 'http_parser_has_error'?
./parser.h:44:5: note: 'http_parser_has_error' declared here
int http_parser_has_error(http_parser *parser);
    ^
parser.rl:144:14: error: implicit declaration of function 'thin_http_parser_is_finished' is invalid in C99 [-Werror,-Wimplicit-function-declaration]
  } else if (thin_http_parser_is_finished(parser) ) {
             ^
1 warning and 2 errors generated.
make: *** [parser.o] Error 1

make failed, exit code 2

Gem files will remain installed in /Users/saekoyamada/.rbenv/versions/2.5.1/lib/ruby/gems/2.5.0/gems/thin-1.5.1 for inspection.
Results logged to /Users/saekoyamada/.rbenv/versions/2.5.1/lib/ruby/gems/2.5.0/extensions/x86_64-darwin-20/2.5.0/thin-1.5.1/gem_make.out
```

Gemfileから試す。  
http://zakihaya.hatenablog.com/entry/2014/12/08/111217  

```
group :development do
  gem 'mailcatcher'
end
```  

`bundle install`  

↓ 

```
saekoyamada@sy taskleaf % bundle install
Fetching gem metadata from https://rubygems.org/............
Resolving dependencies...
Using rake 13.0.3
Using concurrent-ruby 1.1.8
Using minitest 5.14.4
Using websocket-extensions 0.1.5
Using mini_mime 1.1.0
Using arel 9.0.0
Using public_suffix 4.0.6
Using execjs 2.7.0
Using bcrypt 3.1.16
Using coderay 1.1.3
Using bindex 0.8.1
Using debug_inspector 1.1.0
Using msgpack 1.4.2
Using popper_js 1.16.0
Using method_source 1.0.0
Using thor 1.1.0
Using ffi 1.15.0
Using tilt 2.0.10
Using bundler 2.2.11
Using byebug 11.1.3
Using regexp_parser 2.1.1
Using childprocess 3.0.0
Using coffee-script-source 1.12.2
Using rack 2.2.3
Using diff-lcs 1.4.4
Using docile 1.3.5
Using erubi 1.10.0
Using temple 0.8.2
Using hpricot 0.8.6
Using racc 1.5.2
Using rb-fsevent 0.10.4
Using ruby_dep 1.5.0
Using nio4r 2.5.7
Using sqlite3 1.3.13
Using puma 3.12.6
Using rspec-support 3.9.4
Using rubyzip 2.3.0
Using simplecov-html 0.12.3
Using simplecov_json_formatter 0.1.2
Using spring 2.1.1
Using turbolinks-source 5.2.0
Using i18n 1.8.10
Using websocket-driver 0.7.3
Using mail 2.7.1
Using addressable 2.7.0
Using autoprefixer-rails 10.2.4.0
Using binding_of_caller 1.0.0
Using uglifier 4.2.0
Using bootsnap 1.7.4
Using sassc 2.4.0
Using rb-inotify 0.10.1
Using pry 0.13.1
Using coffee-script 2.4.1
Using rack-test 1.1.0
Using sprockets 3.7.2
Fetching daemons 1.3.1
Fetching ruby2_keywords 0.0.4
Using thread_safe 0.3.6
Using better_errors 2.9.1
Using crass 1.0.6
Using html2slim 0.2.0
Using slim 4.1.0
Using nokogiri 1.11.3 (x86_64-darwin)
Fetching json 2.5.1
Fetching rack-protection 2.1.0
Fetching eventmachine 1.2.7
Using builder 3.2.4
Using rspec-core 3.9.3
Using rspec-expectations 3.9.4
Using rspec-mocks 3.9.1
Using selenium-webdriver 3.142.7
Using simplecov 0.21.2
Using turbolinks 5.2.1
Using listen 3.1.5
Using pry-byebug 3.9.0
Using sass-listen 4.0.0
Using tzinfo 1.2.9
Using loofah 2.9.1
Using mimemagic 0.3.10
Using xpath 3.2.0
Using webdrivers 4.6.0
Using spring-watcher-listen 2.0.1
Using sass 3.7.4
Using activesupport 5.2.1
Using rails-html-sanitizer 1.3.0
Using marcel 0.3.3
Using capybara 3.35.3
Using rails-dom-testing 2.0.3
Using globalid 0.4.2
Using activemodel 5.2.1
Using factory_bot 4.11.1
Using jbuilder 2.11.2
Using actionview 5.2.1
Fetching sqlite3-ruby 1.3.3
Fetching haml 5.2.1
Using actionpack 5.2.1
Using activejob 5.2.1
Using activerecord 5.2.1
Using actioncable 5.2.1
Using actionmailer 5.2.1
Using activestorage 5.2.1
Using railties 5.2.1
Using sprockets-rails 3.2.2
Using polyamorous 2.3.2
Using sassc-rails 2.1.2
Using coffee-rails 4.2.2
Using factory_bot_rails 4.11.1
Using rails 5.2.1
Using rspec-rails 3.9.1
Using sass-rails 5.1.0
Using slim-rails 3.2.0
Using web-console 3.7.0
Using ransack 2.3.2
Using bootstrap 4.6.0
Using rails_autolink 1.1.6
Installing daemons 1.3.1
Installing rack-protection 2.1.0
Installing ruby2_keywords 0.0.4
Fetching mustermann 1.1.1
Installing sqlite3-ruby 1.3.3
Installing json 2.5.1 with native extensions
Installing haml 5.2.1
Installing mustermann 1.1.1
Installing eventmachine 1.2.7 with native extensions
Fetching sinatra 2.1.0
Installing sinatra 2.1.0
Fetching thin 1.8.0
Installing thin 1.8.0 with native extensions
Fetching skinny 0.2.2
Installing skinny 0.2.2
Fetching mailcatcher 0.2.4
Installing mailcatcher 0.2.4
Bundle complete! 32 Gemfile dependencies, 120 gems now installed.
Bundled gems are installed into `./vendor/bundler`
Post-install message from sqlite3-ruby:

#######################################################

Hello! The sqlite3-ruby gem has changed it's name to just sqlite3.  Rather than
installing `sqlite3-ruby`, you should install `sqlite3`.  Please update your
dependencies accordingly.

Thanks from the Ruby sqlite3 team!

<3 <3 <3 <3

#######################################################

```

なんかおかしい。  
`bundle install`だと不具合が発生するらしい。

https://kossy-web-engineer.hatenablog.com/entry/2018/11/22/132708  

↓  

最初でたエラーの解決策    
https://github.com/sj26/mailcatcher/issues/430  

一旦下記で試し。  

```
gem install mailcatcher -- --with-cflags="-Wno-error=implicit-function-declaration"
```  

↓  

だめ   

```
gem install thin -v '1.5.1' -- --with-cflags="-Wno-error=implicit-function-declaration"
gem install mailcatcher
```  

↓
```
saekoyamada@sy taskleaf % gem install thin -v '1.5.1' -- --with-cflags="-Wno-error=implicit-function-declaration" 
Building native extensions with: '--with-cflags=-Wno-error=implicit-function-declaration'
This could take a while...
Successfully installed thin-1.5.1
Parsing documentation for thin-1.5.1
Installing ri documentation for thin-1.5.1
Done installing documentation for thin after 0 seconds
1 gem installed
saekoyamada@sy taskleaf % gem install mailcatcher
Building native extensions. This could take a while...
Successfully installed sqlite3-1.4.2
Successfully installed skinny-0.2.4
Successfully installed tilt-2.0.10
Successfully installed rack-protection-1.5.5
Successfully installed sinatra-1.4.8
Successfully installed mini_mime-1.1.0
Successfully installed mail-2.7.1
Successfully installed mailcatcher-0.7.1
Parsing documentation for sqlite3-1.4.2
Installing ri documentation for sqlite3-1.4.2
Parsing documentation for skinny-0.2.4
Installing ri documentation for skinny-0.2.4
Parsing documentation for tilt-2.0.10
Installing ri documentation for tilt-2.0.10
Parsing documentation for rack-protection-1.5.5
Installing ri documentation for rack-protection-1.5.5
Parsing documentation for sinatra-1.4.8
Installing ri documentation for sinatra-1.4.8
Parsing documentation for mini_mime-1.1.0
Installing ri documentation for mini_mime-1.1.0
Parsing documentation for mail-2.7.1
Installing ri documentation for mail-2.7.1
Parsing documentation for mailcatcher-0.7.1
Installing ri documentation for mailcatcher-0.7.1
Done installing documentation for sqlite3, skinny, tilt, rack-protection, sinatra, mini_mime, mail, mailcatcher after 181 seconds
8 gems installed
```

成功!  
```
gem which MailCatcher
/Users/saekoyamada/.rbenv/versions/2.5.1/lib/ruby/gems/2.5.0/gems/mailcatcher-0.7.1/lib/MailCatcher.rb
```

出来た。   
http://127.0.0.1:1080/  

![mailcatcher](https://gyazo.com/96857bcfaf8377af250f88a4bd69b289.png)  
