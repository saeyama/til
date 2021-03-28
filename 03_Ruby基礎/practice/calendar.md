https://docs.ruby-lang.org/ja/latest/method/Time/i/strftime.html  
https://docs.ruby-lang.org/ja/latest/method/String/i/center.html  
https://docs.ruby-lang.org/ja/latest/method/Date/i/wday.html  
https://docs.ruby-lang.org/ja/latest/method/String/i/rjust.html  

```
require "date"

# 配列
week = %w(su mo tu we th fr sa)

#今日
today = Date.today

first_day = Date.new(today.year, today.month, 1) 
#=> <Date: 2021-03-01 ((2459275j,0s,0n),+0s,2299161j)>
last_day = Date.new(today.year, today.month, -1)
#=> <Date: 2021-03-31 ((2459305j,0s,0n),+0s,2299161j)> 

#1行目
puts today.strftime("%B %Y").center(20)
#2行目
puts week.join(" ")

space = "   " * first_day.wday
count = first_day.wday
print space
# first_day.wdayの分だけスペースを開ける
# wday 曜日を数値に変換　0 = 日曜〜 6 = 土曜
# first_day.wday #=> 1 (2021/03/01は月曜なので = 1) 

days = first_day.day..last_day.day
# first_day.day #=> 1
# last_day.day #=> 31

days.each do |day|
  print day.to_s.rjust(2)
  print " "
  count += 1
  if(count % 7 == 0)
    print("\n")
  end
end

```
![ERD](https://gyazo.com/025900bab48a2dbbc290149fdacc6986.png)
