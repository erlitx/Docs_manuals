# How to run Heroku

#### 1. Install 
	$ curl https://cli-assets.heroku.com/install-ubuntu.sh | sh
#### 2. Check version
	$ heroku -v
#### 3. Install Gunicorn
	$ pip install gunicorn 
#### 4. Write down requirements
    $ pip freeze > requirements.txt
#### 5. Create a Procfile which tells Heroku which app (here is app.py) we are running
    $ echo web: gunicorn app:app > Procfile
#### 6. Login into Heroku
    $ heroku login
 Should open webpage and get back to bash already logged in

#### 7. Create an app in Heroku
    $ heroku create flask-blog-test
#### 8. Create PostgreSQL
    $ heroku addons:create heroku-postgresql:mini
or

    $ heroku addons:create heroku-postgresql:mini --app flask-blog-test
*Terminal response: Created postgresql-rigid-38612 as HEROKU_POSTGRESQL_CHARCOAL_URL*

#### 9. Get URL for PostgreSQL database
    $ heroku config --app flask-blog-test
Insert this URL into `app.config['SQLALCHEMY_DATABASE_URI'] =`

**WARNING:**
The path should start from `postgresql://` not `postgres://`


#### 10. Push changes to Heroku
  
    $ git push heroku master
* `requirements.txt` should exist before running and `git commit -m "..."` executed

#### 11. Make DB Initialisation and Migration
    $ heroku run python 
Run python on Heroku server

    >>> from app import db, app
    >>> app.app_context().push()
    >>> db.create_all()





###### ** Official Heroku manual for running Flask app
    https://devcenter.heroku.com/articles/flask-memcache#add-task-list-functionality

