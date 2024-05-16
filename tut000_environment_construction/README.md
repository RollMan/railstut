Run

```bash
docker-compose run web rails new . --force --database=postgresql
```

first to make a template of rails directory structures, then the command modifies `Dockerfile` or `Gemfile`.
Subsequently, run a docker build command

```bash
docker-compose build
```

to apply the changes of `Dockerfile` or `Gemfile`.

After that, modify `config/database.yaml` into following which `docker-compose build` generates.

```
default: &default
  adapter: postgresql
  encoding: unicode
  host: db
  username: postgres
  password:
  pool: 5

development:
  <<: *default
  database: myapp_development


test:
  <<: *default
  database: myapp_test
```

Finally, launch the app by `up` command and, simultaneously, run database generation.

```
docker-compose up
```

On another terminal,

```
docker-compose run web rake db:create
```

## Reference
- https://docs.docker.jp/compose/rails.html
