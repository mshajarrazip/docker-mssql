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

### Tips & Tricks

1. Restoring a database from [.bak]() file:
    - Copy the [.bak]() file to the base directory. The `/mnt` directory in the container is mounted to `${BASE_DIR}/docker-mssql/mnt`, so you can put the file there.
    - Perform restore:
        - Option 1: Run the following command:
    
            ```bash
            docker exec -it <container_name> /bin/bash -c "/opt/mssql-tools/bin/sqlcmd -S localhost -U sa -P Password123 -Q \"RESTORE DATABASE <database_name> FROM DISK='/var/opt/mssql/backup/<backup_file>.bak' WITH MOVE '<logical_name>' TO '/var/opt/mssql/data/<database_name>.mdf', MOVE '<logical_name>_log' TO '/var/opt/mssql/data/<database_name>_log.ldf'\""
            ```
            > Replace `<container_name>`, `<database_name>`, `<backup_file>`, and `<logical_name>` with the appropriate values.

        - Option 2: If you are using ssms as your sql client, you can restore the database from the backup file using the GUI:

            - Right-click on the `Databases` node in the Object Explorer.
            - Select `Restore Database...`.
            - In the `General` page, select `Device` and click on the `...` button.
            - Click on the `Add` button and select the backup file.
            - Click on the `OK` button.
            - Click on the `OK` button to restore the database.

