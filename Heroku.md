## Heroku

#### New Django project
[link](https://devcenter.heroku.com/articles/django-app-configuration)

* clone the [template](https://github.com/heroku/heroku-django-template)
or `$ django-admin(.py) startproject --template=https://github.com/heroku/heroku-django-template/archive/master.zip --name=Procfile <project_name>`

* deploy to Heroku (1st commit)

    1. `$ git init`
    2. `$ git add -A`
    3. `$ git commit -m "<message>"`
    4. `$ heroku login`
    4. `$ heroku create <heroku_app_name>`
    5. `$ git push heroku master`
    6. `$ heroku run(:detached) python manage.py migrate`
    7. `$ heroku open` or open `<heroku_app_name>`.herokuapp.com in browser

#### New Django app
[link](https://devcenter.heroku.com/articles/deploying-python)
1. go inside the project directory, `$ virtualenv <env>`
2. `$ source <env>/bin/activate`
3. edit .gitignore file
4. `$ pip install -r requirements.txt`: run the app locally
5. `$ python manage.py collectstatic`
5. `$ heroku local web` or open local:5000 in the browser

#### Deply to Heroku
1. `$ git add .`
2. `$ git commit -m "<message>"`

    * *if error with static files:* `heroku config:set DISABLE_COLLECTSTATIC=0`

3. `$ git push heroku master`
4. `$ heroku run(:detached) python manage.py migrate`

    * *error with static files:* `heroku config:unset DISABLE_COLLECTSTATIC`

5. `$ heroku run(:detached) python manage.py collectstatic`

#### Installation
[link](https://devcenter.heroku.com/articles/getting-started-with-python#introduction)

* install Postgres
* Postgres configuration:

    1. `$ export PATH="/Applications/Postgres.app/Contents/Versions/latest/bin:$PATH"`: the directory of psql file
    2. install the command line tool for psql - [link](http://postgresapp.com/documentation/install.html)
    3. may need: command line tool for Xcode - [link](https://developer.apple.com/download/more/)

* install Heroku command line tool