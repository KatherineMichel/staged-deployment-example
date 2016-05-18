# Staged Deployment Example

Created using [Heroku Django Template](https://github.com/heroku/heroku-django-template)

## Example Instructions

### Create Project Locally and Push to GitHub master and development Branches

Python and pip should be installed globally, as well as Heroku Toolbelt. Create a GitHub repo and clone locally, but do not cd into the directory. In parent directory:

    $ django-admin.py startproject --template=https://github.com/heroku/heroku-django-template/archive/master.zip --name=Procfile projectname repo-name

You can replace "projectname" with your desired project name.

    $ cd repo-name
    $ pip install django
    $ pip install -r requirements.txt
    $ python manage.py runserver 
    
Check that it works

    http://127.0.0.1:8000

Add and commit files

    $ git add -A
    $ git commit -m "Message"

Push to GitHub master branch

    $ git push origin master

Create local development branch and push to GitHub development branch

    $ git checkout -b development
    $ git push origin development

Pull changes

    $ git pull origin master
    $ git pull origin development

Merge changes

    $ git checkout master
    $ git merge development (merge local development branch changes into local master branch)
    $ git checkout development
    $ git merge master (merge local master branch changes into local development branch)

## Deployment to Heroku

    $ heroku create
    $ git push heroku master

    $ heroku run python manage.py migrate
