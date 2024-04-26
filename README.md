# ridgepole-generated-columns-issue-repro

reproduction repository for https://github.com/ridgepole/ridgepole/issues/482

## step
1. clone this repo
2. bundle install
3. docker compose up -d
4. bundle exec ridgepole --config config/database.yml --apply --file Schemafile
5. bundle exec ridgepole --config config/database.yml --apply --file Schemafile.after

### result
```
❯ bundle exec ridgepole --config config/database.yml --apply --file Schemafile.after
Found existing alias for "bundle exec". You should use: "be"
Apply `Schemafile.after`
-- change_column("users", "full_name", :virtual, {:type=>:string, :as=>"concat(`first_name`,_utf8mb4' ',`last_name`)", :stored=>true, :null=>true, :default=>nil, :unsigned=>false, :comment=>nil})
[ERROR] Mysql2::Error: Incorrect usage of DEFAULT and generated column
* 1: change_column("users", "full_name", :virtual, **{:type=>:string, :as=>"concat(`first_name`,_utf8mb4' ',`last_name`)", :stored=>true, :null=>true, :default=>nil, :unsigned=>false, :comment=>nil})
	/path/to/vendor/bundle/ruby/3.0.0/gems/mysql2-0.5.6/lib/mysql2/client.rb:151:in `_query'
```
