# To reproduce

```
git clone https://github.com/rosa/phantom-db-sqlite-repro.git
cd phantom-db-sqlite-repro
bundle install

bin/rails db:drop db:create db:schema:load --trace
bin/rails runner "puts Dog.count"
```

This results in:
```
$ bin/rails db:drop db:create db:schema:load --trace
** Invoke db:drop (first_time)
** Invoke db:load_config (first_time)
** Invoke environment (first_time)
** Execute environment
** Execute db:load_config
** Invoke db:check_protected_environments (first_time)
** Invoke db:load_config
** Execute db:check_protected_environments
** Execute db:drop
** Invoke db:drop:_unsafe (first_time)
** Invoke db:load_config
** Execute db:drop:_unsafe
Dropped database 'storage/development.sqlite3'
** Invoke db:create (first_time)
** Invoke db:load_config
** Execute db:create
Created database 'storage/development.sqlite3'
** Invoke db:schema:load (first_time)
** Invoke db:load_config
** Invoke db:check_protected_environments
** Execute db:schema:load

$ bin/rails runner "puts Dog.count"
SQLite3::SQLException: no such table: dogs: (ActiveRecord::StatementInvalid)
SELECT COUNT(*) FROM "dogs" /*application='PhantomDbSqliteRepro'*/
...
``