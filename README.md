# im_task_flask
This repo adds [Flask](http://flask.pocoo.org/) support for the [im_task](https://github.com/emlynoregan/im_task) library. If you use flask, and you want to use @task, then install this module.

[![Build Status](https://travis-ci.org/emlynoregan/im_task_flask.svg?branch=master)](https://travis-ci.org/emlynoregan/im_task_flask)
 
## Install

Use the python package for this library. You can find the package online [here](https://pypi.python.org/pypi/im_task_flask).

Change to your Python App Engine project's root folder and do the following:

> pip install im_task_flask --target lib

Or add it to your requirements.txt. You'll also need to set up vendoring, see [app engine vendoring instructions here](https://cloud.google.com/appengine/docs/python/tools/using-libraries-python-27).

### Configuring @task

To use @task with flask, you need to set up routes in app.yaml, and you need to register the flask handlers. 

Let's say you have a standard app.yaml file, and a single flask app "app" set up in main.py.

In app.yaml, set up the following route:

	handlers:
		- url: /_ah/task/.*
		  script: main.app
		  login: admin

Note "login: admin"; this locks down the tasks interface to your own code; you don't want external callers to kick off tasks with unknown code.

In main.py, you need to register the tasks handlers with your flask app:

	from flask import Flask
	from im_task_flask import setuptasksforflask

	app = Flask(__name__)

	setuptasksforflask(app)

Once you've got the routes set up and the task handlers registered, you should be able to use @task. Good luck!	
