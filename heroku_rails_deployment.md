# Heroku Rails Deployment Notes

https://devcenter.heroku.com/articles/getting-started-with-rails6#create-a-new-rails-app-or-upgrade-an-existing-one



## Process for Deploying an App:

rails s

heroku create

git config --list | grep heroku

git push heroku master

heroku run rake db:migrate

heroku ps:scale web=1

heroku ps

heroku open



## General Commands:

https://devcenter.heroku.com/articles/heroku-cli

heroku restart --app [app_name]

heroku logs

heroku update 

sudo apt-get update && sudo apt-get upgrade heroku

heroku apps:destroy --app [app-name]



