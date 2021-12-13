# How to migrate sqlserver to postgres
1. Install java and config JAVA_HOME, use the following command to test if you have installed java: 
    ``` sh
    java -version
    ```
2. Install edb(enterprise database) [mtk](https://www.enterprisedb.com/docs/migration_toolkit/latest),
    > You can use **Aplication stack builder** to install this tool kit
    >
    > This tool has been installed if you tick it in Postgresql installation progress
3. Config [tookit](https://www.enterprisedb.com/docs/migration_toolkit/latest/) properties file in: C:\Program Files\edb\mtk\etc\toolkit.properties.properties
    ## Properties for sqlserver
    ``` sh
    SRC_DB_URL=jdbc:jtds:sqlserver://192.168.1.155:1433/your_source_db_name
    SRC_DB_USER=your_source_db_user_id
    SRC_DB_PASSWORD=your_source_db_password
    TARGET_DB_URL=jdbc:postgresql://127.0.0.1:5432/your_target_db_name
    TARGET_DB_USER=your_target_db_user_id
    TARGET_DB_PASSWORD=your_target_db_password
    ```

    ## Properties for sqlserver express    
    ``` sh
    SRC_DB_URL=jdbc:jtds:sqlserver://192.168.1.155:1433/your_source_db_name;instance=SQLEXPRESS
    SRC_DB_USER=your_source_db_user_id
    SRC_DB_PASSWORD=your_source_db_password
    TARGET_DB_URL=jdbc:postgresql://127.0.0.1:5432/your_target_db_name
    TARGET_DB_USER=your_target_db_user_id
    TARGET_DB_PASSWORD=your_target_db_password
    ```
    > if you use sqlexpress, you must enable **Sql Server Browser** in service
    > 
    > if you use sqlexpress, you must enable **TCP/IP** client protocol by Sql Configuration Manager
4. Copy db drivers to C:\Program Files\edb\mtk\lib, this driver can be download from [this repos](https://github.com/it950/migrate-sqlserver-to-postgresql/tree/main/drivers),
    * postgresql-42.3.1.jar    
    * jtds-1.3.1.jar

5. Open the command as an **administrator**, and go to the folder: C:\Program Files\edb\mtk\bin, run the command: 
    ## Migrate all tables
    ``` sh
    runMTK.bak -sourcedbtype sqlserver -targetdbtype postgres -targetschema public dbo
    ```
    
    ## Migrate specified tables by option **-tables**, table list is a comma-separated list
    ``` sh
    runMTK.bak -sourcedbtype sqlserver -targetdbtype postgres -targetschema public dbo -tables table1,table2
    ```
6. View the logs in **C:\Users\your_windows_user_name\.enterprisedb\migration-toolkit\logs** to check if there are some errors.  
7. Other reference:
    * [migrate-MSSQL-to-PostgreSQL-MTK](https://rainmakerho.github.io/2021/02/09/migrate-MSSQL-to-PostgreSQL-MTK/)
    * [migrating-database-from-sql-server-mssql-to-postgresql](https://dev.to/abhinavgupta1997/migrating-database-from-sql-server-mssql-to-postgresql-1mje)

