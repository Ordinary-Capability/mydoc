# Database Usage notes
## Mariadb
- drop table with prefix  
    ```
    SELECT CONCAT( 'DROP TABLE ', GROUP_CONCAT(table_name) , ';' )  AS statement FROM information_schema.tables  WHERE table_name LIKE 'ipc_%';
    ```

- drop table when foreign key deadlock  
    ```
    SET foreign_key_checks=0; 
    SET foreign_key_checks=1;
    ```

- difference between manytoone and foreign key  
    To define a many-to-one relationship, use ForeignKey
    
- Modify a existing table char set
    ```
    ALTER TABLE ToolDownload_tag CONVERT TO CHARACTER SET utf8mb4 COLLATE utf8mb4_general_ci;
    ```
