# Postgres

## Run Postgres docker images

1. Run `docker images` to check the image to run
2. Run eg. `docker run --name postgres15.2 -p 5432:5432 -e POSTGRES_USER=root -e POSTGRES_PASSWORD=secret -d postgres:15.2-alpine`
3. Run `docker ps` to check if container starts
4. Connect to the container and use psql concole: `docker exec -it <name_of_container> psql -U <user>`

## Commands

| Command | Description |
| ------- | ----------- |
| `show transaction isolation level` ||
