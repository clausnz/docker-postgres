# Docker Postgres container

Build docker container with PostgreSQL 9.5 and import SQL files in shared folder.

    docker run \
        -d \
        --restart=always \
        --name my_postgres \
        -e POSTGRES_DB=my_db \
        -e POSTGRES_USER=my_user \
        -e POSTGRES_PASSWORD=my_pass \
        -p 5432:5432 \
        -v "$PWD"/sql_import_folder:/docker-entrypoint-initdb.d/ \
    postgres:9.5

Docker compose file `docker-compose.yml` section:

    version: "3"
    db:
        image: "postgres:9.5"
        restart: "always"
        ports:
        - "5432:5432"
        volumes:
        - "./sql_import_dir:/docker-entrypoint-initdb.d/"
        environment:
        - "POSTGRES_DB=my_db"
        - "POSTGRES_USER=my_user"
        - "POSTGRES_PASSWORD=my_pass"

Start `docker-compose.yml` with following command:

    docker-compose up -d