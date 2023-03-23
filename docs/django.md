# Django Basic Notes
- static collection command   
    ```
    python manage.py collectstatic
    ```
- make database migration  
    ```
    python manage.py makemigrations
    python manage.py migrate
    ```

- re-create all tables
1. Manully drop tables in database
2. fake migrate to zero point
    ```
    python manage.py migrate --fake <app_name> zero
    ```  
3. migrate
    ```
    python manage.py migrate <app_name>
    ```  
  
- create admin account 
    ```
    python manage.py createsuperuser
    ```
  


