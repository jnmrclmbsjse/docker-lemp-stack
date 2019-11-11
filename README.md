# Docker LEMP Stack

Linux, Nginx, MySQL, PHP (LEMP) Stack for local development environment built using Docker. This stack was based from an undisclosable project made by some genius developers.

## Features

* **NGINX** (pronounced "engine-x") that supports hosting of multiple web applications locally
* **MariaDB** with persistent data on a mounted volume
* **PHP 7.3** with **FPM** to provide high performance PHP web applications together with NGINX
* Say no to different bugs on development due to different environments

## Installation

1. Using your favorite terminal, navigate to your Projects folder (*this could be anywhere e.g /foo/Documents/Projects*) then clone this repository.
```
git clone https://gitlab.com/jnmrclmbsjse/docker-lemp-stack.git
```
2. Inside the cloned repository folder, have your environment variables available by duplicating the **.env.example** file.
```
cp .env.example .env
```
3. Optionally, you can change **PROJECT_DIRECTORY** and **PROTOCOL** variable inside your **.env** file to your desired value.
```
# Application/Project Directory path (absolute or relative)
PROJECT_DIRECTORY=/home/administrator/Projects

# First 3 segments for network IP Address
PROTOCOL=10.5.0
```
4. See **Usage** notes below to build and have this cool environment running on your machine.

## Usage
This awesome stack gives you ready-made bash scripts which contains commands to run, reload, rebuild or stop the environment.

*First, make sure to be on the root directory of this repository and run one of the commands below on your favorite terminal*

```
# Initialize or start the environment
./bin/start

# Stops the environment
./bin/stop

# Reloads the environment, but does not reinitialize
./bin/restart

# Reinitialize specific service
./bin/rebuild <service_name>

``` 
## Author
* **Junmar Jose** - *Initial work* - [Gitlab](https://gitlab.com/jnmrclmbsjse)

## FAQs
### How does NGINX access our projects?
> This stack was designed to mount a project directory into the container. The **PROJECT_DIRECTORY** variable in .env file gets mounted inside the nginx container's **/var/www/** directory.
### How to add new web applications and virtual hosts?
> Simply put your web application folder inside your project directory and map it in your virtual host by adding a vhost file inside **./services/nginx/virtualhosts/sites** folder. This folder is being mounted on the nginx container's conf.d folder.

> There are example vhost files for symfony, drupal, laravel and slim inside **./services/nginx/virtualhosts/examples**. Upon addition of new virtual host, simply run **./bin/restart** on the root directory to apply changes.
### What path should I put on the vhost file?
> Assuming that your **PROJECT_DIRECTORY** variable has a value of **/home/administrator/AwesomeProjects** and your web application path is **/home/administrator/AwesomeProjects/symfony-application**, then your vhost entry should be **/var/www/symfony-application/**.
### How to configure and map my web application to the databases?
> On your configuration file (*e.g. settings.php, parameters.yaml*), you can simply put **mysql** as the hostname of your database. Default username is **root** and password is **secret**.
### How to access databases using GUI tools
> If you are on **Windows** or **Linux**, use the static IP (*localhost, 127.0.0.1*) and use port 3306. If within a **VM**, use the static IP (10.5.0.4) defined on the **docker-compose** file.
### Troubleshooting
> 1. Destroy then re-initialize the stack
> 2. If the step above does not solve your problem, restart your workstation a couple of times.
> 3. If problems still persist, try to fix it or consult me (Junmar).