# pagar.me


## Installation

Clone the source:

    $ git clone https://github.com/caiaffa/pagarme-python.git
    
Execute:

1. [http://www.rabbitmq.com/download.html](Install RabbitMQ)

2. Create a user, a virtual host, and give permissions to that user on virtualhost:
	
	`sudo rabbitmqctl add_user youruser yourpassword`
	`sudo rabbitmqctl add_vhost yourvhost`
	`sudo rabbitmqctl set_permissions -p yourvhost youruser ".*" ".*" ".*"`

3. pip install -r requirements.txt

## Documentation

Visit [https://docs.pagar.me/api/](https://docs.pagar.me/api/) for api reference or [https://docs.pagar.me/](https://docs.pagar.me/)


