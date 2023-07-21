# Database Usage notes
## Mariadb
- Drop tables with prefix name match 
    ```
    SELECT CONCAT( 'DROP TABLE ', GROUP_CONCAT(table_name) , ';' )  AS statement FROM information_schema.tables  WHERE table_name LIKE 'ipc_%';
    ```

- Drop all tables in one database
    ```
    SELECT CONCAT('DROP TABLE IF EXISTS ', GROUP_CONCAT(table_name), ';')  FROM information_schema.tables  WHERE table_schema = 'database_name';
    ```
    The SQL command above generates a one line command. Execute that command to drop all tables in 'database_name'.
    You may need to disable foreign key check before execute that command.

- drop table when foreign key deadlock  
    ```
    SET foreign_key_checks=0;
    SET foreign_key_checks=1;
    ```

- difference between manytoone and foreign key  
    To define a many-to-one relationship, use ForeignKey
    
- Database SET/COLLATION operations
    ```
    SHOW CHARACTER SET;
    SHOW COLLATION LIKE 'utf8bm4%';
    CREATE DATABASE database_name CHARACTER SET character_set_name COLLATE collation_name;
    ALTER  DATABASE databasename CHARACTER SET utf8mb4 COLLATE utf8mb4_general_ci;
    ALTER TABLE ToolDownload_tag CONVERT TO CHARACTER SET utf8mb4 COLLATE utf8mb4_general_ci;
    ```
    
 - Simple data backup and restore operation
    ```
    mysqldump -u springuser -p spring_rhino_test test_case > case.sql //dump table test_case to case.sql 
    mysql -u springuser -p spring_rhino_test < case.sql //restore case.sql to table test_case
    ```
