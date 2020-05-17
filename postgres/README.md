# Running PostgreSQL with Docker

## [1] Docker 

### Official Postgres Docker Image

```shell
# Download the Docker official image for Postgres from the Docker Hub repository
docker pull postgres

# Check to see if the image is downloaded
docker images

# Create a local folder and mount it as a data volume for our running container to store all the database files 
mkdir postgres-data

# Run 
docker run -d \
--name dev-postgres \
-e POSTGRES_PASSWORD=admin123 \
-v $PWD/postgres-data/:/var/lib/postgresql/data \
-p 5432:5432 \
postgres

# Check that the container is running
docker ps

# Enter the container with bash
docker exec -it dev-postgres bash
>>>
$ psql -h localhost -U postgres
$ \l # List of databases
$ \h # SQL Command Help
$ \d # List of relations
$ \dt # List of tables
$ \dt+ # List of tables with more description
$ \c <database> # Connect to database
$ \q # Exit
```

### pgAdmin Instance

```shell
# pgAdmin is the most popular and feature-rich Open Source administration and 
# development platform for PostgreSQL. 
docker pull dpage/pgadmin4

# -p 80:80 = This parameter tells docker to map the port 80 in the container to port 80 in your computer (Docker host)
# -e 'PGADMIN_DEFAULT_EMAIL' = Environment variable for default user's email, you will use this to log in the portal afterwards
# -e 'PGADMIN_DEFAULT_PASSWORD' = Environment variable for default user's password
# -d = This parameters tells docker to start the container in detached mode
# dpage/pgadmin4 = This parameter tells docker to use the image that we have previously downloaded
docker run \
--name dev-pgadmin \
-p 80:80 \
-e "PGADMIN_DEFAULT_EMAIL=admin@domain.local" \
-e "PGADMIN_DEFAULT_PASSWORD=admin123" \
-d dpage/pgadmin4

# Check in web browser and log in with EMAIL and PASSWORD we set above
localhost:80

# Check the IPAddress (For server connection in the pgAdmin tool)
docker inspect dev-postgres -f "{{json .NetworkSettings.Networks }}"
```

## [2] Docker Compose

```shell
# Run docker-compose.yml that initializes postgresql database
docker-compose up
```