## Dushanbe Work Submission APIs (Backend)

#### Developed by Django REST Framework

###### DigitalOcean

* Frontend: https://dushanbe.lp-report.com/
* Backend: http://www.dushanbe.apis.lp-report.com/

###### Heroku

* Frontend: https://dushanbe-frontend-vuejs.herokuapp.com/
* Backend: https://dushanbe-backend-apis.herokuapp.com/

###### Local

* Frontend: http://localhost:5000/
* Backend: http://localhost:8000/

###### Deployment Commands (Heroku & Git)

```
heroku login
```
```
heroku create dushanbe-backend-apis
```
```
heroku addons:create heroku-postgresql:hobby-dev
```
```
git add .
```
```
git commit -m "first commit"
```
```
git remote -v
```
```
git push origin main
```
```
git push heroku main
```
```
git log
```

###### Collecting Static Assets 

* From Local
```
python manage.py collectstatic
```
* From Heroku (No need if collected from locally)
```
heroku run python manage.py collectstatic
```

###### Django Commands 

```
heroku run python manage.py migrate
```
```
heroku run python manage.py createsuperuser
```

###### Access Heroku Bash

```
heroku run bash
```
```
ls
```
```
cd /
```
```
ls
```
```
exit
```

###### Access Heroku PostgreSQL Database

```
heroku pg:credentials:url --app dushanbe-backend-apis
```

###### Open Heroku Bash

```
heroku run bash --app dushanbe-backend-apis
```
###### Heroku Database Access

```
psql -h hostname -d databasename -U username
```
###### Select Database

```
\c d9q659p5g9ats9
```
