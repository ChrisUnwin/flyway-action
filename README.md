# Flyway Pipeline Action

This action runs [Flyway latest][flyway] to migrate database. It aims to migrate database for testing in workflows.

## Usage

```yaml
name: Main
on:
  - push
jobs:
  test:
    runs-on: ubuntu-latest
    
    steps:
      - uses: actions/checkout@v2
      - uses: ChrisUnwin/flyway-action@v4
        with:
          url: jdbc:postgresql://postgres:5432/postgres
          user: postgres
          password: postgres
          command: migrate
          disableclean: false
          baselineonmigrate: false
          baselineversion: 001
      - run: echo 'testing'
```

Currently, it supports `url`, `user`, `password`, `locations`, `baselineonmigrate`, `baselineversion`, `disableclean` and `command`. 

Defaults: `locations` is set to `filesystem:./sql`, `command` is set to `migrate`, `disableclean` is set to `false`, `baselineonmigrate` is set to `false` and `baselineversion` is set to `0.0`

For details, please check out Flyway [documentation].

[flyway]: https://flywaydb.org/
[documentation]: https://flywaydb.org/documentation/configuration/parameters/

Thanks to joshuaavalon for the initial version, which I forked for the purposes of a blog post.
