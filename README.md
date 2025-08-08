# instructions_for_postgresql_server
instructions for installing and configuring PostgreSQL on the server


# CONFIGURING THE SERVER
1. Create server VDS/VPS (>= Ubuntu 24.04)
2. sudo apt update && sudo apt upgrade -y  # updating the system
3. sudo apt install postgresql postgresql-contrib -y # installing postgresql
4. sudo systemctl status postgresql # checking the service status
5. sudo -i -u postgres
6. psql


# SETTING UP AND CREATING A DATABASE
7. CREATE DATABASE you_database_name; # creating a database
8. CREATE USER ypu_user WITH PASSWORD 'you_password'; # creating a user
9. GRANT ALL PRIVILEGES ON DATABASE mydb TO myuser; # assigning rights
10. \q # exiting psql
11. exit # exiting the postgres shell


# SETTING UP A NETWORK CONNECTION
12. sudo nano /etc/postgresql/YOU_VERSION/main/postgresql.conf
13. # listen_addresses = 'localhost'  # find and edit a string на listen_addresses = '*'
    or a separate address to restrict access : listen_addresses = '127.0.0.1'
14. sudo nano /etc/postgresql/YOU_VERSION/main/pg_hba.conf # allow connection in pg_hba.conf
    host    all             all             0.0.0.0/0               md5
    or
    host    you_db          you_user        you_host                you_method
15. sudo systemctl restart postgresql # restart postgresql
