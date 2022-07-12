# There are some questions should be resolved
- [ ] Change original of apt source
- [ ] List local of linux
- [ ] Which local should be selected when install postgresql
- [ ] Change table schemal remotely
- [ ] Backup database
- [ ] Transfer backup files from remote server to local server
- [ ] Restore backup files
- [ ] Change data forder to another location of server

# Install
``` shell
sudo sh -c 'echo "deb http://apt.postgresql.org/pub/repos/apt $(lsb_release -cs)-pgdg main" > /etc/apt/sources.list.d/pgdg.list'
wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo apt-key add -
sudo apt update
sudo apt install postgresql postgresql-contrib
```

# View the status of postgresql
``` 
service postgresql status
```

# List all options
```
service postgresql
```

# You must login first if you want use postgresql, the default user is postgres which own all privilege
## Switch user to postgres
```
sodo su postgers
```

# Type psql in the command
```
psql
```

# Command
```
// for quite
\q

// for help
\? 

// List all database
\l

// Display all user
\du
```

# Change user password, do not forget add a comma in the end of each command
```
alter user postgres with password 'my-pass';
```

# You should create a new user instead of postgres user
```
CREATE USER my_user WITH PASSWORD 'my_password';
```

# add privilege to new added user
```
ALTER USER my_user WITH SUPERUSER;
```
# Drop a user
```
DROP USER my_user;
```

# Login with a new user name
```
\q
psql -U my_user
```

# Or login to db directly
```
psql -U my_user -d my_db
```

# Login error:
```
psql: FATAL:  Peer authentication failed for user "my_user"

// replace peer with md5 and then restart
sudo vim /etc/postgresql/14/main/pg_hba.conf
service postgresql restart
```
