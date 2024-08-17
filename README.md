# docker-mssql

Dockerized MSSQL container for development purposes.

_What's so special?_

- Creates multiple databases on startup automatically :D

## Usage

1. Create a base directory:
    ```bash
    mkdir -p ~/docker/mssql
    ```
1. Copy the folder [db/](db/), and the files [.env](.env) and [docker-compose.yml](docker-compose.yml) to the base directory.
1. Set the following environment variables (default values are provided in [.env](.env)):
    - `COMPOSE_PROJECT_NAME`: The project name.
    - `PORT`: The port to expose the database.
    - `DB_NAMES`: The databases to create. You can create multiple databases by separating them with a comma.
    - `BASE_DIR`: For persistence, this path will be mounted to the container. It is where the database files will be stored.
1. Using your favourite sql client, you may now connect to the database using the following credentials:
    - **Server**: `localhost``
        > If you are using WSL, use the IP address of the host machine instead of `localhost` e.g. use `hostname -I` to get the IP address.
    - **Port**: _The port you set in the environment variables._
    - **Username**: `sa`
    - **Password**: `Password123`


