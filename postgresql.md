# PostgreSQL

---

### Connect to db

#### Log in to postgress

`sudo -i -u postgres`

#### Connect to `mydb` database

`psql -U postgres -d mydb`

or

`psql`

#### Commands


| Command   | Description                |
|-----------|----------------------------|
| `\l`      | Database list              |
| `\c mydb` | Connect to `mydb` database |
| `\dt`     | Show tables on current db  |
| `\q`      | Logout                     |

#### Drop column from table

```shell
alter table address
drop column data;
```

#### Drop table

`drop table table_name;`