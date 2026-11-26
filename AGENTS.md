# AGENTS.md

`lus-lang/atmos-migrate` is the repository of the `migrate` package of the atmosphere registry. Programs load the package with `require("https://atmosp.here/2.0/migrate.lus")`.

## Scope

`migrate` applies numbered SQL migration files to a database in order and records each one with its checksum, so every database runs each schema change once and in the same order. It works with `io.sqlite` and with any database object that has the methods `exec`, `query`, and `transaction`. The public API is every function that `migrate.lus` returns in its module table. A change to that API needs a new entry in `CHANGELOG.md` and a version change in the header.

## Layout

- `migrate.lus` is the whole package. Its header doc comment contains the package metadata and the declared permissions.
- `tests/*_test.lus` are the tests. They load `migrate.lus` from the parent of `TEST_DIR`, the directory that holds the test file.

## Commands

Run these commands from the root of the repository.

```sh
lus test tests          # run the tests
lus check migrate.lus     # lint, including the package codes
lus doc migrate.lus       # print the reference
```

## Rules

- Every public function has a doc comment that states each result and each error, following `spec/design/style.md` of the Lus repository.
- The package never calls `pledge`. A new permission is declared in the header.
- Prose follows the `lus-writing` skill, which `lus agents init` installs and https://lus.dev/agents/skills/lus-writing/SKILL.md serves. In particular, prose has no dashes or semicolons and never names the Roblox Lua dialect.
- Every bug fix comes with a test that fails without it.
