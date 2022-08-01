# Instll mssql on docker

## Reference
[mssql docker image](https://hub.docker.com/_/microsoft-mssql-server)

[tutorial-restore-backup-in-sql-server-container](https://docs.microsoft.com/en-us/sql/linux/tutorial-restore-backup-in-sql-server-container?view=sql-server-ver16)

[how-to-use-a-docker-host-folder-for-a-sql-server-database](https://theserogroup.com/how-to-use-a-docker-host-folder-for-a-sql-server-database/)

> [!IMPORTANT]
> Do not change the port that mssql run on docker

## Install Express
```bash
docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=Your@Password" -e "MSSQL_PID=Express" \
   -v "D:\database\sqlserver\docker-express-data":/mnt/sqlexpress-2019 \
   -p 1401:1433 --name sqlexpress-2019 --hostname sqlexpress-2019 \
   -d \
   mcr.microsoft.com/mssql/server:2019-latest
```

## Install Standard
```bash
docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=Your@Password" -e "MSSQL_PID=Standard" \
   -v "D:\database\sqlserver\docker-standard-data":/mnt/sqlstandard-2019 \
   -p 1401:1433 --name sqlstandard-2019 --hostname sqlstandard-2019 \
   -d \
   mcr.microsoft.com/mssql/server:2019-latest
```

---

## How to change mssql `default server collation`

> The default value is: `SQL_Latin1_General_CP1_CI_AS`


## Performance optimization for mssql

>
>


## How to restore a `backup` for mssql which run on docker

1. Fist stop the container
```bash
docker stop sqlstandard-2019
```

2. Run container
```bash
docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=Your@Password" -e "MSSQL_PID=Standard" \
   -v "D:\database\sqlserver\docker-standard-data":/mnt/sqlstandard-2019 \
   -p 1401:1433 --name sqlstandard-2019 --hostname sqlstandard-2019 \
   -d \
   mcr.microsoft.com/mssql/server:2019-latest
```

3. Create a empty database on the mounted folder, and then restore the backup to it
```SQL
CREATE DATABASE Learn 
ON
( NAME = Learn,
    FILENAME = '/mnt/sqlserver-2019/data/Learn.mdf',
    SIZE = 10,
    MAXSIZE = 100,
    FILEGROWTH = 5 )
LOG ON
( NAME = Learn_log,
    FILENAME = '/mnt/sqlserver-2019/data/Learn_log.ldf',
    SIZE = 5MB,
    MAXSIZE = 100MB,
    FILEGROWTH = 5MB ) ;
GO

RESTORE DATABASE Learn 
    FROM DISK='/mnt/sqlserver-2019/backup/Learn.bak' 
    WITH REPLACE,
    MOVE 'Learn' TO '/mnt/sqlserver-2019/data/Learn.mdf', 
    MOVE 'Learn_log' TO '/mnt/sqlserver-2019/data/Learn_log.ldf';
```

4. Or use `SQL Server Management Studio` to restore a database to a `mounted folder`
> [!IMPORTANT]
> Must create a empty database firstly, otherwise an error will throw if directly restore.
> Msg 3634, Level 16, State 1, Line 2
The operating system returned the error ‘2(The system cannot find the file specified.)’ while attempting ‘RestoreContainer::ValidateTargetForCreation’ on `/mnt/sqlserver-2019/data/Learn.mdf`.

```SQL
USE [master]
RESTORE DATABASE [Learn] FROM  DISK = N'/mnt/sqlserver-2019/backup/Learn.bak' WITH  FILE = 1,  
   MOVE N'Learn' TO N'/mnt/sqlserver-2019/data/Learn.mdf',  
   MOVE N'Learn_log' TO N'/mnt/sqlserver-2019/data/Learn_log.ldf',  
NOUNLOAD,  STATS = 5
```




