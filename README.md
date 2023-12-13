## Here I downgrade python version and switch the multiple version of python
#### To check python version `python3 -V`

I'm using python3.11.6 now i want switch 3.10.11
#### Make a directory python file which you want downgrade 
`mkdir ~/python-source-files`

#### Download python3.10.11 
`wget -P ~/python-source-files https://www.python.org/ftp/python/3.10.11/Python-3.10.11.tgz`


#### Extract 3.10.11.tgz 
```
cd python-source-files/
tar xvzf Python-3.10.11.tgz

```
#### change directory in Python3.10.11 
`cd Python-3.10.11/` and configure optimization `./configure --enable-optimizations`
and run this command for alternative install `sudo make altinstall`

 After alternative install now check how many python version available in your system to see that 
 run this `ls /usr/local/lib | grep python`
 
 where is python3.10 to see that `type -a python3.10`
 
 Now update pyhton3.10 for alternative 
 ```
 sudo update-alternatives --install /usr/bin/python3 python3 /usr/local/bin/python3.10 1
 
 sudo update-alternatives --install /usr/bin/python3 python3 /usr/bin/python3.11 2

 ```
#### Switch version of python 
```
sudo update-alternatives --config python3

```

#### click 0/1/2 to switch the version

# To create Virtual Environment to install Django 

##### If you dont have venv then install it  `sudo apt install python3-venv`

##### To create environment                  ` python3 -m venv my_env`

##### Activate the environment               `source my_env/bin/activate`

##### Deactivate the environment             `deactivate `
 
##### Install django                         `python3 -m pip install Django`

##### If you want to install django specifiq version  `python3 -m pip install Django==3.2`

##### Create A project                       `django-admin startproject mysite`
 

#### To install pipreqs run this command `pip install pipreqs`

`pipreqs` command for requirement.txt

##### Or You can run this command ` pip freeze > requirements.txt`

# To deploy Your Django app in Vercel

##### create `vercel.json` file in root directory of your project paste this line of code

```
{
  "version": 2,
  "builds": [
    {
      "src": "projectname/wsgi.py",
      "use": "@vercel/python",
      "config": { "maxLambdaSize": "15mb", "runtime": "python3.11" }
    },
    {
      "src": "build_files.sh",
      "use": "@vercel/static-build",
      "config": {
        "distDir": "staticfiles_build"
      }
    }
  ],
  "routes": [
    {
      "src": "/static/(.*)",
      "dest": "/static/$1"
    },
    {
      "src": "/(.*)",
      "dest": "projectname/wsgi.py"
    }
  ]
}
# change projectname your actual projectname

```


##### create a  file name `build_files.sh`  in root directory of your project paste this line of code
```
# build_files.sh
pip install -r requirements.txt
python3.9 manage.py collectstatic
#here you must be give python3.9
```
#### In setting.py file of project below STATIC_URL paste this lines of code

##### `import os` in import section and ALLOWED_HOSTS = ['127.0.0.1', '.vercel.app', '.now.sh']

```
STATICFILES_DIRS = (os.path.join(BASE_DIR, 'static'),)
STATIC_ROOT = os.path.join(BASE_DIR,'staticfiles_build','static')

```
#### Comment Database setion of setting.py 

```
DATABASES = {
    # 'default': {
    #     'ENGINE': 'django.db.backends.sqlite3',
    #     'NAME': BASE_DIR / 'db.sqlite3',
    # }
}
```


#### In urls.py add this line code
```
from django.conf import settings
from django.conf.urls.static import static
```
add this line of code below 
```
urlpatterns = [
###
]

urlpatterns += static(settings.MEDIA_URL, document_root = settings.MEDIA_ROOT)
urlpatterns += static(settings.STATIC_URL, document_root=settings.STATIC_ROOT)
```


# Installed Postgresql Database in ubuntu
### Just go to the postges website and copy and pase the command to install postgres shell and pgadmin4 .

#### To Show psql version `psql --version`.

#### Navigate back to the Postgres shell and run the following commands consecutively` sudo -i -u postgres`.

#### To interact with the database server run ` psql`.

#### To create Database user & password run this ` CREATE USER username WITH PASSWORD 'password';`.

#### To create a database run this `CREATE DATABASE db_name; ` or `createdb db_name `.

#### To delete a database run this `DROP DATABASE db_name;`.

#### To see list of db here `\l`.

#### To connect db run `\c db_name`.

# Install postgresql in Django

#### To install postgresql in virstual environment run `pip install psycopg2-binary`.

#### To change requirement.txt file run `pip freeze > requirements.txt`.

#### Now Change in setting.py DATABASE section

```
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': 'database_name',
        'USER': 'user_name_of_psql',
        'PASSWORD': 'password_pf_psql',
        'HOST': 'localhost',
        'PORT': 5432
    }
}

```

#### To migrate database run `python3 manage.py migrate`.

#### If You face Error :
```
django.db.migrations.exceptions.MigrationSchemaMissing: Unable to create the django_migrations table (permission denied for schema public
LINE 1: CREATE TABLE "django_migrations"
```
#### Go your psql shell and GRANT the the databse to user`GRANT ALL ON DATABASE mydb TO myuser;` and `ALTER DATABASE my_db OWNER TO myuser;`.


