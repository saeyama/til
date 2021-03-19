モデルを消して痛い目を見たことがあるので、ちょっとしたことも備忘に残す。    
まとめかたはまた考える。


```
taskleaf % bin/rails db:migrate
rails aborted!
SyntaxError: 
... t.string :password_digest null:false
```
↓

「,」もれ

↓

状態確認
```
taskleaf % bundle exec rails db:migrate:status

 Status   Migration ID    Migration Name
--------------------------------------------------
   up     20210313002841  Create tasks
   up     20210315161618  Change tasks name not null
  down    20210319061009  Create users
```

↓

ロールバックするべき…？    
とりあえずしない
```
% bin/rails db:migrate                                                  
== 20210319061009 CreateUsers: migrating ======================================
-- create_table(:users)
   -> 0.0017s
== 20210319061009 CreateUsers: migrated (0.0017s) =============================
```

成功    
↓

```
% bundle exec rails db:migrate:status

 Status   Migration ID    Migration Name
--------------------------------------------------
   up     20210313002841  Create tasks
   up     20210315161618  Change tasks name not null
   up     20210319061009  Create users
```

downがupに変わった。






