# Changelog

## 1.0.0

**Release date:** TBD

Version 1.0.0 is the first release of `migrate`, which runs on Lus 2.0.

- Added the `migrate` package.
  - `migrate.load`: Reads the migrations of a directory and returns them in order.
  - `migrate.up`: Applies the pending migrations of a source in order, each in its own transaction.
  - `migrate.down`: Reverts applied migrations, the latest first.
  - `migrate.status`: Lists every migration with its state.
  - `migrate.iserror`: Returns true for an error object that `migrate` raised.
