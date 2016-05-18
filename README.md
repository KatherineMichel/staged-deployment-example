# Staged Deployment Example

Created using [Heroku Django Template](https://github.com/heroku/heroku-django-template)

## Example Instructions

### Create Project Locally and Push to GitHub master branch

Python, pip, and Django should be installed globally, as well as Heroku Toolbelt. Create a GitHub repo and clone locally, but do not cd into the directory. Run this command in the parent directory (You can replace "projectname" with your desired project name; replace repo-name with the name of the GitHub repo you have cloned locally.):

    $ django-admin.py startproject --template=https://github.com/heroku/heroku-django-template/archive/master.zip --name=Procfile projectname repo-name

Change directory, install requirements, and run server

    $ cd repo-name
    $ pip install -r requirements.txt
    $ python manage.py runserver 
    
Check that the Django welcome page appears

    http://127.0.0.1:8000

Add and commit files

    $ git add -A
    $ git commit -m "Message"

Push to GitHub master branch

    $ git push origin master

### Create Local development Branch and Create/Push to GitHub development Branch

    $ git checkout -b development
    $ git push origin development

### Update GitHub Updates to Local Branches and Merge Changes Between development and master Branches

Pull changes

    $ git pull origin master
    $ git pull origin development

Merge changes

    $ git checkout master
    $ git merge development (merge local development branch changes into local master branch)
    $ git checkout development
    $ git merge master (merge local master branch changes into local development branch)

## Deploy to Heroku Staging and Production Websites

    $ heroku create app-name
    $ git push heroku master

    $ heroku run python manage.py migrate
