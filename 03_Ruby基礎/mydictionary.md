# to_●●

to_a 配列変換  
to_s 文字変換  
to_i 数値変換  
to_f 整数を少数変換  
to_h 配列をハッシュ変換  
to_sym 文字列をシンボル変換  

# %●

*小文字だと式展開されない。大文字は式展開される。

%q!! シングルクオートで囲ったことと同じになる　＊式展開されない   
%,%Q!! ダブルクオートで囲ったことと同じになる　＊式展開される   

%w 配列を作る  ＊式展開されない    
%W 配列を作る　＊式展開される   

%i シンボルの配列を作る  ＊式展開されない   
%I シンボルの配列を作る  ＊式展開される   

%x コマンド出力を行う   
%s シンボル

# ||= 自己代入

変数がnilかfalseでなければ右辺のデータを代入する。

```
limit = nil
limit ||= 10

p limit #=> 10 


limit = 20
limit ||= 10

p limit #=> 20

↓捉え方

limit = limit || 10
(n += 1 #=> n = n + 1 と同じ考え)

```

# &. ぼっち演算子

```
a = 'foo'

a&.upcase #=> "FOO"
a.upcase #=> "FOO"

a = nil

a.upcase #=> undefined method `upcase' for nil:NilClass (NoMethodError)

a&.upcase #=> nil
ぼっち演算子にすることによって例外にならない。

```
```
def find_currency(country)
  currencies = {japan: 'yen', us: 'dollar', india: 'rupee'}
  currencies[country]
end

def show_currency(country)
  currency = find_currency(country)

  #nilでないことをチェック

  if currency
    currency.upcase
  end

　↓

  currency&.upcase
  
end

p show_currency(:japan) #=> "YEN"
p show_currency(:brazil) #=> "nil"

レシーバがnilだった場合にnilで返す。
```
