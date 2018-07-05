[TOC]


## pymysql -python3的mysql库

### 事务回滚
```python
import pymysql.cursors
connection = pymysql.connect(host='localhost', user='root', password='root', db='test', charset='utf8mb4', cursorclass=pymysql.cursors.DictCursor)
try:
    with connection.cursor() as cursor:
        sql = "INSERT INTO `urllist` (`urlname`, `urlhref`) VALUES (%s, %s)"
        cursor.execute(sql, ('webmaster@python.org', 'very-secret'))
        print(cursor.rowcount) #受影响条数
        sql = "UPDATE `urllist` set  urlname=%s,urlhref=%s where id=%s"
        cursor.execute(sql, ('cpjupdate', 'hrefupadte', '13'))
        print(cursor.rowcount)

    connection.commit()
except Exception as  e:
    connection.rollback()
    print("mysq:", e)
finally:
    connection.close()

```