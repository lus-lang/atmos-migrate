# migrate

`migrate` applies numbered SQL migration files to a database in order and records each one with its checksum, so every database runs each schema change once and in the same order. It works with `io.sqlite` and with any database object that has the methods `exec`, `query`, and `transaction`.

The following example applies the migrations of an application database, then reverts the latest.

```lus nocheck
local migrate = require("https://atmosp.here/2.0/migrate.lus")

local db = io.sqlite("app.db")
-- Applies migrations/0001_create_users.sql, migrations/0002_add_email.sql, ...
for _, name in ipairs(migrate.up(db, "migrations")) do
    print("applied", name)
end
print(migrate.status(db, "migrations")[1].name)   --> 0001_create_users.sql
migrate.down(db, "migrations")                    -- runs 0002_add_email.down.sql
```

The package requires Lus 2.0 and declares the permission `fs:read`, which it uses to read the migration files. A database file that `io.sqlite` opens also needs `fs:read` and `fs:write`. It never calls `pledge`, so the program that loads it keeps control of its permissions.

The reference is in the doc comments of `migrate.lus`, which `lus doc migrate.lus` prints.
