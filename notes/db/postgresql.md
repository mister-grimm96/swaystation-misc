## setting up psql

```sh
# psotgres automatically creates a user `postgres`
sudo -iu postgres
initdb -D /var/lib/postgres/data
```

now exit and `systemctl start postgresql`

```sh
# setting up pass
sudo -u postgres psql
alter user postgres with password '<your password>'
# or
\password <user_name>
```

- go pg_admin right click on servers -> register -> server
- give it a name like `LocalHost` in general tab
- go to connection set the hostname like : `localhost`
- provide the password and save.

## accessing psql from the terminal

```sh
psql -U <user_name>
eg : psql -U postgres
```
