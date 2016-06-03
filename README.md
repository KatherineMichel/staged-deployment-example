# Staged Deployment Example

Created using [Heroku Django Template](https://github.com/heroku/heroku-django-template)

## Example Instructions

### Create Project Locally and Push to GitHub master branch

Python, pip, and Django should be installed globally, as well as Heroku Toolbelt installed and authenticated. Create a GitHub repo and clone locally, but do not cd into the directory. Run this command in the parent directory (You can replace "projectname" with your desired project name; replace repo-name with the name of the GitHub repo you have cloned locally.):

    $ django-admin.py startproject --template=https://github.com/heroku/heroku-django-template/archive/master.zip --name=Procfile projectname repo-name

Change directory

    $ cd repo-name

At this point, it's strongly recommended that you create and activate a virtualenv of some type. Afterward, install requirements, and run server. (migrate?)

    $ pip install -r requirements.txt
    $ python manage.py runserver 
    
Check that the Django welcome page appears

    http://127.0.0.1:8000

Add and commit files, with message

    $ git add -A
    $ git commit -m "Message"

Push to GitHub master branch

    $ git push origin master

## Deploy to Heroku Staging and Production Websites

    $ heroku create app-name
    $ git push heroku master

Migrate and Open Heroku App in Browser

    $ heroku run python manage.py migrate (does this need to be run again for forked app?)
    $ heroku open 

Fork the App

    $ heroku fork --from app-name --to app-name-staging

Add Forked Remote

    $ heroku info -a app-name-staging
    $ git remote add forked git@heroku.com:app-name-staging.git (or otherwise use Git URL from previous info command)

Alternatively 

    $ git remote add forked https://git.heroku.com/app-named-staging.git

Heroku Remotes in Repo

    heroku          (app-name)
    forked          (app-name-staging)

Open Staging or Production Sites in Browser

    $ heroku open --app app-name
    $ heroku open --remote forked

Create local development Branch, Push to Staging Site, Create/Push to GitHub development Branch

    $ git checkout -b development 
    $ heroku keys:add (if needed due to publickeys error)
    $ git push forked master
    $ git push origin development

## Staging and Production Site Examples

[Staging URL](https://deployment-example-staging.herokuapp.com)

    https://deployment-example-staging.herokuapp.com

[Production URL](https://deployment-example.herokuapp.com)

    https://deployment-example.herokuapp.com

Two ways to Change URL

    $ heroku apps:rename new-name --remote forked
    $ heroku apps:rename new-name --app old-name

### Merge Changes Between development and master Branches, Push and Pull Between GitHub and Local Branches

Merge changes from development branch into master branch

    $ git checkout master
    $ git merge development -m "Message" (merge local development branch changes into local master branch)
 
Add and commit files, with message

    $ git add -A
    $ git commit -m "Message" 

Push to GitHub master branch and Heroku master branch

    $ git push origin master
    $ git push heroku master

Merge changes from master branch into development branch

    $ git checkout development
    $ git merge master  -m "Message" (merge local master branch changes into local development branch)

Add and commit files, with message

    $ git add -A
    $ git commit -m "Message" 

Push to GitHub development branch and Heroku forked master (staging site)

    $ git push origin development
    $ git push forked master

To Escape Git Message, if needed

    ESC
    $ :wq

Pull changes (checkout as needed)

    $ git pull origin master
    $ git pull origin development