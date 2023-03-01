# Run postgres image with name some-postgres, password 123, in background mode
		$ docker run --name some-postgres -e POSTGRES_PASSWORD=123 -d postgres
				or
		$ docker run --name learn_postgres -e POSTGRES_PASSWORD=123 -p 5433:5432 -d postgres

# Create User via Docker Interactive Shell
# Before going to create new user in docker container, first you need to enter into docker name 'learn_posgres' container via execcommand.
		$ docker exec -it learn_postgres bash

# Swithc to postgres user
		root@bf0951223121:/# su - postgres
# Enter PSQL
		postgres@bf0951223121:~$ psql

# We should create superuser 'docker_user' with creation roles and pass 'docker_user'.
		postgres=# create role docker_user with login SUPERUSER PASSWORD 'docker_user';
# Give create DB permission to docker_user
		postgres=# ALTER USER docker_user WITH CREATEDB CREATEROLE;

# Run new container with hew user
		$ docker run --name learn_postgres -e POSTGRES_PASSWORD=docker_user -e POSTGRES_USER=docker_user -p 5433:5432 -d postgres
# Connect vie pgAdmin localhost: 5433 user:docker_user pass:docker_user

# Run with volume from /var/lib/postgresql/data in container to ./test_source to host
		$ docker run --name learn_postgres2 -e POSTGRES_PASSWORD=docker_user -e POSTGRES_USER=docker_user -p 5433:5432 -v ./test_source:/var/lib/postgresql/data -d postgres
# Run with volume from /var/lib/postgresql/data in container to 'pgdata' docker volume
		$ docker volume create pgdata
		$ docker run --name learn_postgres -e POSTGRES_PASSWORD=docker_user -e POSTGRES_USER=docker_user -p 5433:5432 -v pgdata:/var/lib/postgresql/data -d postgres











#enter in 'some-postgres' terminal
$ docker exec -it some-postgres bash

#How to import *.sql file into new DB
-- https://www.warp.dev/terminus/psql-run-sql-file

#enter in SQL 
psql -U postgres

# How to run Flask server with hello.py
$ flask --app hello --debug run 