P.47

累乗：puts 数字 ** 数字    


### to_s  string(整数を文字列へ変換)
### to_i  integer(文字列を整数へ変換)
数値以外の文字列オブジェクトにto_iを使用すると結果は０


p.52

オブジェクトの種類のことをクラスをいう。
(IntegerオブジェクトのIntegerがクラスの名前)

変数はオブジェクトにつける名札


### 式展開　#{計算式}
ダブルだと変数の内容が表示
シングルだとそのまま表示


getsメソッド    
https://pikawaka.com/ruby/gets
文字列オブジェクトになる（数値オブジェクトにはならない）
- getsで数値オブジェクトを取得したい時はto_iメソッドを使用する

- ターミナルから入力された値をとってくるようあらかじめ設定されている

- 標準入力
キーボードから入力した値をコマンドへ渡すことを標準入力という

$stdin 変数 　STDIN 定数

stdin = Standard Input

- 標準出力

$stdout 変数 　STDOUT 定数

stdout = Standard Out

puts = put string
putsも標準出力メソッド

---

## 定数
先頭に大文字の名前をつけると定数になる。(キャメル)
定数なので同じ名前の定数を複数作成するのはNG

---

## 2-6

## デバッグ
バグを見つけて直して行くこと

pメソッドは原則、デバッグ用に使用(pメソッドを使って変数の中身を表示していく)

## 3-1

返す = 実行結果で置き換えられる
<=  >=   <>が先。=が後。時々迷う。
=> だと別の意味になるJSのアロー関数

---

== != は数値オブジェクトだけではなく、文字列オブジェクトを比較することも可能

---

===  はRubyにはない認識でいたけどあるっぽい
https://qiita.com/Siva0410/items/c0b6ed52017ffada8bf4

!== はあるのか？

---

末尾に「?」がつくメソッドはtrueかfalseのどちらかを返すことが多い。

---

後置if(if修飾子)
- end不要　一行でかける

例   
puts "●●" if 変数 条件

---
## 3-2

unless：ifと反対の動きをする。

! : trueとfalseを反転させる。!は変数やオブジェクトの前に書く


if 条件がfalseまたはnilでなけらば条件分岐していなくても成立する。
elsif   elseifじゃないので注意

---

## 繰り返し

## case

変数の値に応じて、複数の道から１つを選んで分岐する
最初に合致したwhen節のみ処理を実行

ruby

```
order = "aaa"

case order
when "aaa"
  puts "300"
when "bbb"
  puts "400"
else
  puts "なし"  
end
```

JS
https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Statements/switch

```
const expr = 'Papayas';
switch (expr) {
  case 'Oranges':
    console.log('Oranges are $0.59 a pound.');
    break;
  case 'Mangoes':
  case 'Papayas':
    console.log('Mangoes and papayas are $2.79 a pound.');
    // expected output: "Mangoes and papayas are $2.79 a pound."
    break;
  default:
```

>2択の時はif   
3択以上の時はcase


ruby繰り返し

https://www.javadrive.jp/ruby/for/


JS繰り返し
https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide/Loops_and_iteration


### doとendのセット ： ブロック(処理のかたまりを書ける部品)
﹂doとendの代わりに{}でも書ける

複数業書くときはdoとend

3.times do
  puts "aaa"
  puts "bbb"
end

一行書く時は{}

3.times { puts "aaa" }  

---
### DRY : 重複を避けてプログラムを書く習慣
---

## while
﹂条件を満たしてる間ずっと繰り返したい場合
doは使わない

```
a = 0
while a < 2
  a += 1
  puts "aaa#{a}"
end

while 条件
  条件を満たしている間、繰り返しを実行する処理
end 

```

## 4 配列
- 配列は複数のオブジェクトをまとめて扱う道具
- 種類の違うオブジェクトを1つの配列に入れることもできる
- 配列を代入する変数名は複数形にする

配列の要素　
test = ["a","b"]

最初の要素
puts test[0] #=> "a" 
puts test.first #=> "a" 

後ろから数える
puts test[-1] #=> "b"
※-0からではない。-1のあとは-2,-3と続く
puts test.last #=> "b"
 
## 4-3

要素を追加
末尾へ追加 push <<
先頭へ追加 unshift

要素を削除
末尾を削除 pop
先頭を削除 shift

## each
|●●●|　変数

## 5

# size : 配列の要素数を得る

### to_f : 小数へ変換

```
a = [1, 1, 3]
puts a.sum.to_f / a.size

a.sumで合計値5
to_fで5.0に変換

```

破壊的変更：元々のオブジェクトを変更する

sample : 配列からランダムに要素を取得
shuffle : 配列をランダムに並びかえる
sort : 並び替え　数字は小さい順 文字はa~ 大文字は入ると大文字が先になる
sort.reverse : sortと逆


object_id : 識別番号を返すメソッド

join : 配列の全要素をつなげる
split : 文字を分割
map : 配列の各要素へ処理を行い、新しい配列を作るメソッド

## 6 hash

### to_sym symbol(文字列をシンボルへ変換) 

## hash書き方
- {:a => 1, :b => 2}
- {a: 1, b: 2}

シンボル以外のオブジェクトは=>で書く。
{"a" => 1, "b" => 2}

```
menu = {coffee: 300, caffe_latte: 400}
p menu[:coffee] シンボルをつける

文字列だったら"coffee"
p menu["coffee"]文字列で指定

追加
menu[:mocha] = 400　変数の後にkey = valueで追記

```
- ハッシュは同じキーを持てない 同じキーを追加すると値が上書きされる。
- 存在しないキーを指定したときの値はdefault=メソッドで設定も可能
- deleteでキーと値を削除できる

each_key(キーだけ取り出す)    
each_value(値だけ取り出す)

has_key?(keyが存在するかどうか調べる)

## 7
引数はメソッドをオブジェクトを渡す機能。

### return : 設置したところで処理を止める
### キーワード引数 :　引数名の後ろに「：」をつける
﹂引数の順番を変えても呼び出せる。

```
def order(item:, size:)
  "#{item}を#{size}サイズで！"
end
```

## スコープ : 変数の見える範囲と寿命
 
## 8 class

クラスはオブジェクトの種族を表すもの
命名規則：キャメルケース

インスタンス : あるクラスのオブジェクト

レシーバ：メソッドを呼び出されるオブジェクト

methodsメソッド
レシーバであるオブジェクトで呼び出せるメソッド一覧表示できる。
自分で作成したクラスのメソッドも確認できる
p 1.methods
p 1.methods.sort

- p self でレシーバが調べられる
- インスタンス変数を取得するメソッドは慣習的にインスタンス変数名から＠を取り除いたものにすることが多い。

```
def name
  puts @name
end
```

インスタンス変数へ代入するメソッド
```
def name=(text)
  @name = text
end
```

- instance_variables ：インスタンス変数の変数名一覧を取得するメソッド

- initialize : オブジェクトが新しく作られる時に自動で呼びだしされる   
﹂呼び出しているのはnewメソッドだが、自動で呼び出されるのはinitializeメソッド


```
クラスメソッド

def self.メソッド名
  "hello"
end

呼び出し
クラス名.メソッド名
```
![ｍethod](https://gyazo.com/fd7b21be07dbb3507868bf99d008e5bb.png)

- インスタンスメソッドからクラスメソッドを呼べる
- クラスメソッドからインスタンスメソッドは呼べない

- ### ancestors : クラスの継承関係を確認できる

- super 親クラスも同名メソッドを呼び出す

クラスメソッドのprivate
```
class Foo
  private_class_metnod def self.a
    "method a"
  end
end
```


## 9 module

include : 含める

- クラスにインクルードできる
- クラスメソッドを定義できる

```
module WhippedCream
  def self.info
    "aaa"
  end
end

puts WhippedCream.info
```

- モジュールと定数/モジュールとクラスつなげる時 ::

- 別ファイル読み込む時    
require_relative "ファイル名"
require "./ファイル名"

階層違えば/追記

## 10 

- ライブラリ
﹂組み込みライブラリ（クラス）
﹂標準添付ライブラリ（JSON）
﹂Gem

``bundle init`` するとGemfileができる
``bundle install`` するとGemfile.lockができる

``bundle exec`` Gemfile.lockに書かれたGemバージョンでrubyのプログラムが実行できる

###プログラムでWebにアクセス。
```
require "net/http"
require "uri"
uri = URI.parse("https://example.com/")
puts Net::HTTP.get(uri)
```
