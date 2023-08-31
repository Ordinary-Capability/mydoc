# Django Basic Notes
- Start new django project and app
  ```
  django-admin startproject <site_name>
  python manage.py startapp <app_name>
  ```
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
2. fake migrate to some point
    ```
    python manage.py migrate --fake <app_name> zero  # Fake reverse all applied migrations
    
    python manage.py migrate --fake <app_name> 0007  # Fake reverse applied migrations after 0007
    
    # Django will detect that you have an initial migration and that the tables it wants to create already exist,
    # and will mark the migration as already applied
    python manage.py migrate --fake-initial 
    ```  
3. migrate
    ```
    python manage.py migrate <app_name>
    ```  
  
- create admin account 
    ```
    python manage.py createsuperuser
    ```
  


