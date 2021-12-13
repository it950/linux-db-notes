# How to migrate sqlserver to postgres
1. Install java and config JAVA_HOME, use the following command to test if you have installed java: 
    ``` sh
    java -version
    ```
2. Install edb(enterprise database) mtk(migrate took kit),
    > You can use **Aplication stack builder** to download this tool kit
    >
    > This tools has been installed if you tick it in Postgresql installation progress
3. Config tookit properties file in: C:\Program Files\edb\mtk\etc\toolkit.properties.properties
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
    ``` sh
    runMTK.bak -sourcedbtype sqlserver -targetdbtype postgres -targetschema public dbo
    ```

  

