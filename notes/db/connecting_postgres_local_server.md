1. Check that PostgreSQL is running
   `pg_isready -h localhost -p 5432`

You should see something like:

`localhost:5432 - accepting connections`

2. Connect directly with psql
   `psql -h localhost -p 5432 -U postgres`

It will ask for the PostgreSQL password.

Or specify a database:

`psql -h localhost -p 5432 -U postgres -d postgres`

3. If you want to create a database

Inside psql:

`CREATE DATABASE myapp;`

Or directly from your shell:

`createdb -h localhost -p 5432 -U postgres myapp`

4. If you want to create a user
   `psql -h localhost -U postgres`

Then:

`CREATE USER myuser WITH PASSWORD 'mypassword';`

Grant access:

`GRANT ALL PRIVILEGES ON DATABASE myapp TO myuser;`

5. Use the connection from your application

The equivalent connection information to what you'd enter in pgAdmin is:

```sh
Host: localhost
Port: 5432
Database: myapp
Username: myuser
Password: mypassword
```

For example, a PostgreSQL connection URL is:

`postgresql://myuser:mypassword@localhost:5432/myapp`
