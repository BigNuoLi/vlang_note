## 泛型

看作者的计划,目前计划支持泛型函数和泛型结构体,还未开发完成

```
struct Repo<T> {
	db DB
}

fn new_repo<T>(db DB) Repo<T> {
	return Repo<T>{db: db}
}

// This is a generic function. V will generate it for every type it's used with.
fn (r Repo<T>) find_by_id(id int) ?T {
	table_name := T.name // in this example getting the name of the type gives us the table name
	return r.db.query_one<T>('select * from $table_name where id = ?', id)
}

db := new_db()
users_repo := new_repo<User>(db)
posts_repo := new_repo<Post>(db)
user := users_repo.find_by_id(1)?
post := posts_repo.find_by_id(1)?
```
