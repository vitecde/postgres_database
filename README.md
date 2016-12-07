# postgres_database
Usage:

First, the docker can be downladed with the following command in the Docker terminal as:

$ docker pull vitecde/postgres-database

In order to star the docker, the following command is used:

$ docker run -v /c/Users/myDir:/home -p 8000:5432 -e "POSTGRES_PASSWORD=toor1" -it --rm vitecde/postgres_database

where:

/c/Users/myDir -> example of a directory where the file with the data to populate the data base can be copied.

POSTGRES_PASSWORD=toor1 -> environment variable to define the password of the database. Note that the standard name of the
database and the standard user is "postgres". To set a custom name and user please refer to https://hub.docker.com/_/postgres/


As example to test the database, two files are provided in the /example directory: "tables2.sql" and "example_M.csv".

"tables2.sql" -> defines the structure of a table which is used to create the database as it is initialized. As shown in the Dockerfile,
this file is added when the docker is created:
ADD ./example/tables2.sql /docker-entrypoint-initdb.d

"example_M.csv" -> is an example of data which can be written to the database. As mentioned above, a directory is mounted to the
/home directory for this example. 

Then, a sql command can be sent by a client application to the database to populate the database with this file :

 COPY customer_reviews FROM '/home/example_M.csv' WITH CSV;

