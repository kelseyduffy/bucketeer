[following this guide](https://blog.logrocket.com/how-to-build-a-restful-api-with-docker-postgresql-and-go-chi/)

docker container deployment failing for some reason with the migrate functionality, so for now that's been rolled back to a local instance of the REST API hitting a containerized postgres, which was manually deployed using 
`docker run --name some-postgres -p 5432:5432 -e POSTGRES_PASSWORD=<postgres pass> -d postgres`

set the environment variables needed for Go to connect to the postgres instance
- `export POSTGRES_USER=<postgres user>`
- `export POSTGRES_PASSWORD=<postgres password>`
- `export POSTGRES_DB=<postgres database>`

then connect to the postgres container either with:
- another container
    - `docker run -it --rm --link some-postgres:postgres postgres psql -h postgres -U postgres`
    - `create database <database name>` -- could just use the default postgres database
    - `\connect <database name>`
- pgadmin

then manually execute the sql command in [up.sql](db/migrations/000001_create_items_table.up.sql) to create the items table