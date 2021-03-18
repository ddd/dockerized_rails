# Dockerized Rails

This project lets you dockerize a Ruby on Rails 6.1 application backed by PostgreSQL.

## Features

This includes the following:

	Dockerfile to create the web app
	database.yml for accessing the PostgreSQL database backend
	docker-compose.yml to create the full environment
	entrypoint.sh for the web app container
	Gemfile/Gemfile.lock to bootstrap the initial application
	README.md is obviously this file

## Installation

To create this you would run the following

	* Ensure you have Docker/Docker Desktop installed (with docker-compose)
	* Create your directory where you want the app on your local system
	* Copy all file except the README.md into that created directory
	* CD into that directory
	* Run 
		```bash
		docker-compose run --no-deps web rails new . --force --database=postgresql
		```
	* If you are on Linux, you need to run 
		```bash
		sudo chown -R $USER:$USER .
		```
	  to own the files.
	* Any additional gems you want available need to be added to the Gemfile now, like RSpec.
	* Run 
		```bash
		docker-compose build
		```
	  This command is rerun every time you change either the Gemfile in your app, or the Dockerfile.
	* When the entire process is complete, you need to copy _database.yml_ into the
	  _config/_ directory of your new app.
	* Run 
		```bash
		docker-compose up
		```
	* When its all running, issue the following to the web container
		```bash
		docker exec $(nameOfYourWebContainer) rails generate rspec:install
		``` 
		This is only if you added RSpec.

		```bash
		docker exec $(nameOfYourWebContainer) rake db:create
		```
		```bash
		docker exec $(name of yourWebContainer) rake db:migrate
		```
	* Open your web browser and go to *http://localhost:3000* and you should see the app running.
	* To stop everything, run 
		```bash
		docker-compose down
		```
	* To restart the application in the future, run 
		```bash
		docker-compose up
		```

## More Information

For additional information, or to see where this all originated and get more ideas of what to do, please
visit [Docker] (https://docs.docker.com/compose/rails/)


