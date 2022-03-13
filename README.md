<p align="center"><a href="https://laravel.com" target="_blank"><img src="https://raw.githubusercontent.com/laravel/art/master/logo-lockup/5%20SVG/2%20CMYK/1%20Full%20Color/laravel-logolockup-cmyk-red.svg" width="400"></a></p>

## Jobs in Laravel 9

Jobs permits to do some task in a controlled way. For example send emails 5 minutes later some action has been done.

### To start the project run in the root of project

```
./vendor/bin/sail up
```

This will start the containers of the project and a mysql database.

Access to the project in your web browser in http://localhost


### Steps

- Open the file /config/queue.php. You will see the availables drivers for queue: Drivers: "sync", "database", "beanstalkd", "sqs", "redis", "null"
- If you need to change the configuration of an specific driver do it.
- If the default one it's not that one you need, then change its value in the .env file (not in queue.php)
- QUEUE_CONNECTION=database (changed to database in the .env file).
- In this example we will be using [Mailtrap] (https://mailtrap.io) test the emil send. Create an account in this site and copy the configuration of environment variables corresponding to Laravel, the site will bring you this values.
- Once you had set the configuration in .env file creates the CustomerJob.php and SendMailable.php
- sail php artisan make:job CustomerJob
- sail php artisan make:mail SendMailable
- In CustomerJob modify the handle() method 
- Also modify the build method in SendMailable.php
- Now we need to create the queue table: sail php artisan queue:table. This table will store the jobs.
- And: sail php artisan migrate
- Now create a Controller: sail php artisan make:controller EmailController.php. And create the method sendMail()
- Creates the route to /sendmail
- Test the route. The email will not beed sended. It is because you need to start the service enabling the queue to listeng for new jobs
- php artisan queue:work
- This will start the process of jobs. Each new jobs is stored in queue database, when it is processed the next job is processed

