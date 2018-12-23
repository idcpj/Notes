[TOC]

## 初始化

conn.go
```
import (
	"database/sql"

	_ "github.com/go-sql-driver/mysql"
)

var (
	dbConn *sql.DB
	err    error
)

func init() {
	dbConn, err = sql.Open("mysql", "root:12345678@tcp(localhost:3306)/video_server?charset=utf8")
	if err != nil {
		panic(err)
	}
	err = dbConn.Ping()
	if err != nil {
		panic(err)
	}

}
```
## 增
```
stmt, e := dbConn.Prepare(`INSERT INTo sessions (session_id,TTL,login_name) values(?,?,?)`)
defer stmt.Close()
_, e = stmt.Exec(sid, ttlstr, uname)
```
## 查单条
```
stmt, e := dbConn.Prepare(`SELECT TTL,login_name FROM sessions where session_id=?`)
defer stmt.Close()
e = stmt.QueryRow(sid).Scan(&ss.TTL, &ss.UserName)
if e != nil && e != sql.ErrNoRows {
	return nil, e
}
```
## 查多条
```
stmt, e := dbConn.Prepare("select video_id from video_del_rec limit=?")
var ids []string
rows, e := stmt.Query(count)
for rows.Next() {
	var id string
	if e := rows.Scan(&id); e != nil {
		return ids, e
	}
	ids = append(ids, id)
}
```
