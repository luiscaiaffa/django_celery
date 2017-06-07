# django_celery


## Installation

Clone the source:

    $ git clone https://github.com/luiscaiaffa/django_celery.git
    
Execute:

1. [http://www.rabbitmq.com/download.html](Install RabbitMQ)

2. Create a user, a virtual host, and give permissions to that user on virtualhost:
	
	```
	sudo rabbitmqctl add_user youruser yourpassword
	sudo rabbitmqctl add_vhost yourvhost`
	sudo rabbitmqctl set_permissions -p yourvhost youruser ".*" ".*" ".*"
	```

3. pip install -r requirements.txt

4. Your settings
	
	```
	BROKER_URL = 'amqp://guest:guest@localhost:5672//'
	CELERY_ACCEPT_CONTENT = ['json']
	CELERY_TASK_SERIALIZER = 'json'
	CELERY_RESULT_SERIALIZER = 'json'
	```

5. In the project folder
	
	create file celery.py

	```
	from __future__ import absolute_import, unicode_literals
	import os
	from celery import Celery

	os.environ.setdefault('DJANGO_SETTINGS_MODULE', 'django_celery.settings')
	app = Celery('django_celery')
	app.config_from_object('django.conf:settings', namespace='CELERY')
	app.autodiscover_tasks()
	```

6. In the project folder __init__.py

	```
	from __future__ import absolute_import, unicode_literals
	from .celery import app as celery_app

	__all__ = ['celery_app']
	```

7. In the folder of your app create a file named tasks.py
	
	```
	from __future__ import absolute_import, unicode_literals
	from celery import shared_task

	@shared_task
	def task_example(email):
		print (email)
		return "success"
	```

## Running

1. Running celery
	
	```
	celery -A django_celery worker -l info
	```
2 Running python manage.py shell
	```
	from app_example.tasks import task_example
	task_example.delay(email)
	```

## Celery in Production

1. Install sudo apt-get install supervisor

2. create file in /etc/supervisor/conf.d/
	
	```
	[program:celery]
	command=/home/deploy/.virtualenvs/yourvirtual/bin/celery --app=yourproject worker --loglevel=INFO
	directory=/home/deploy/webapps/yourproject
	user=nobody
	autostart=true
	autorestart=true
	redirect_stderr=true

	```

3 execute 
	```
	sudo supervisorctl reread
	sudo supervisorctl update
	sudo supervisorctl start celery
	```

## Documentation

Visit [http://docs.celeryproject.org/en/latest/django/first-steps-with-django.html](http://docs.celeryproject.org/en/latest/django/first-steps-with-django.html) for api reference 


