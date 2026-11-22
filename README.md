# migrate

Applies numbered SQL migration files to a database in order and records each one with its checksum. It works with `io.sqlite` and with any database that offers `exec`, `query`, and `transaction`.

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

The package requires Lus 2.0. It needs `fs:read` to read the migration files. `io.sqlite` needs `fs:read` and `fs:write` for a database file. It calls no `pledge` of its own, so the program that loads it keeps control of its permissions.

The reference is in the doc comments of `migrate.lus`. Run `lus doc migrate.lus` to print it.
