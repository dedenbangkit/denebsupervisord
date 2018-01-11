# Dsupervisord
Supervisor Configuration for BJM Elastic Beanstalk

## About Supervisor
Supervisor is a client/server system that allows its users to monitor and control a number of processes on UNIX-like operating systems.
use supervisord tools to start/stop, conditionally wait for child processes to shutdown, and startup later.
* processname   : ```supervisord```
* config        : ```/etc/supervisord.conf```
* config        : ```/etc/sysconfig/supervisord```
* pidfile       : ```/var/run/supervisord.pid```
* chkconfig     : ```345 83 04```

### Installation

Tested on Laravel 5.2

1. Add Elastic Beanstalk Extension to your deploy Source

        git clone https://github.com/dedenbangkit/denebsupervisord.git
        cp denebsupervisord/supervisor.config {$path_to_source}/source/.ebextension/
        cp denebsupervisord/supervisor.sh {$path_to_source}/source/.ebextension/

2. Add new value to Elastic Beanstalk software configuration in your dashboard.
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

* All log files related to supervisor will be written in ```/var/www/app/support/logs``` in your EB container. You can also request for log files in log dashboard also, All Application > ```${YOUR_ENV}``` > Logs.
* Run ```ps -aux | grep artisan``` to make sure that supervisor is running on your system.
* The demo

### More Details

* [Supervisor/initscripts](https://github.com/Supervisor/initscripts)
* [Supervisord](http://supervisord.org/)

### Acknowledgments

Check the [Original Source](https://lifeofguenter.de/2015/04/27/laravel-queues-with-supervisor-on-elasticbeanstalk) for more details about the config
