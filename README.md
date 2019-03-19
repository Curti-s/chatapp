## Project title
A real-time chat application using django, vue and rabbitmq.

 

## Tech/framework used
- django
- drf
- djoser
- uwsgi
- django-notifs
- vue

<b>Built with</b>
- [VueJs](https://vuejs.org/)

## Features
Uses vuejs to implement the front-end and django to implement the backend.
Resources from the backend are exposed using the django-rest framework.
It also implements message passing of notifications in relation to user events,
such as joining chat sessions, using RabbitMQ and Celery.


## Installation
The folder `chatire-app/` provides the front-end resources, while `chatire` provides the backend resources.

- To run the app, clone it in your development environment.
`git clone git@github.com:Curti-s/chatapp.git`

- Create a python virtual environment and install necessary requirements
`python -m venv env`
`source env/bin/activate`
`pip install -r requirements.txt`

- Run the backend
`cd chatire/`
`python manage.py runserver`

- Proceed to run the front end
`cd ../chatire-app/`
`npm run serve`

- Copy and paste the url to the front-end app to your browser
`localhost:8080/chat/`

## Credits
Special thanks to [Osaetindaniel](https://github.com/danidee10) for providing such an in-depth tutorial
of creating real-time apps with django and vue.


## License
License (MIT)

MIT © [Matthew Kirimi](https://github.com/Curti-s)
