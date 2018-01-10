# Dsupervisord
Supervisor Configuration for BJM Elastic Beanstalk

Tested on Laravel 5.2

1. Add Elastic Beanstalk Extension to your deploy Source

        git clone https://github.com/dedenbangkit/denebsupervisord.git
        cp denebsupervisord/supervisor.config {$path_to_source}/source/.ebextension/
        cp denebsupervisord/supervisor.sh {$path_to_source}/source/.ebextension/

2. Add new value to Elastic Beanstalk software configuration
   - All Application > ```${YOUR_ENV}``` > Configuration > Software Configuration.
   - Look at your Environment Properties, add this value:
     ```
     Property Name = SUPERVISE
     Property Value = enable
     ```
   - Apply and wait until the configuring procces done.

3. Deploy your app with the webhook or by executing this command in *EB OPS*

        cd {$path_to_source}
        sh deploy.sh

### Important Notes

* All log files related to supervisor will be written in ```/var/www/app/support/logs``` in your EB container.
* Run ```ps -aux | grep artisan``` to make sure that supervisor is running on your system.

### See Also

* [Supervisor/initscripts](https://github.com/Supervisor/initscripts)
* [Supervisord](http://supervisord.org/)

### Acknowledgments

Check the [Original Source](https://lifeofguenter.de/2015/04/27/laravel-queues-with-supervisor-on-elasticbeanstalk) for more details about the config
