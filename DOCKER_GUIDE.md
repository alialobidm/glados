## Docker Guide

The `docker-compose.yml` file defines a glados deployment containing a trin node,
a postgres instance, and the components of glados pre-configured to use the node and postgres
instance.

### Deploying Glados

First, set the environment variables:

- `GLADOS_POSTGRES_DATA_DIR` to the directory
where Postgres should store its data on the host machine.

- `GLADOS_POSTGRES_PASSWORD` to the password for accessing the DB.

- `GLADOS_PROVIDER_URL` to the execution API provider URL.

- `GLADOS_PORTAL_CLIENT` to the Portal client to be used for Portal network
access. Currently supported values are `trin` and `fluffy`.

Then, from the root of this repo, run:

`docker compose up -d`

Finally, seed the `block` table with pre-merge blocks

`docker compose run --rm glados_monitor --database-url postgres://postgres:$GLADOS_POSTGRES_PASSWORD@glados_postgres:5432/glados seed --table-name block`

If successful, you should be able to navigate to `127.0.0.1:3001/` and see
the Glados web dashboard populating with data.

### Updating

`docker compose pull && docker compose up -d`

### Tearing Down

`docker compose down` will remove the deployment.

