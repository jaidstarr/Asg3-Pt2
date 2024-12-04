# Asg3-Pt2

## creating new droplets for load balancer
when creating a load balancer, first thing you need to do is make sure that you have two servers set up and running. these servers will hold all your kernel information. This will also act as a file server, that you can hold and download files from.

Start by creating your 2 droplets in digital ocean. They should have the tag `web`. This allows you to connect the servers to a load balancer. When the droplets are created, you then have to install nginx and enable and start it. 

## starting nginx on your servers
*these actions will need to be done on each of your servers*<br/>

start by installing nginx with this command<br/>
```sudo pacman -Syu nginx```<br/>
As you just created your server, it will need to be updated. That is why we are using `-Syu` instead of just `-S`<br/>

Once nginx is installed, it will need to enabled and then started. Do this with these commands.<br/>
```sudo systemctl enable nginx```<br/>
followed by<br/>
```sudo systemctl start nginx```<br/>

You can check if nginx is active with `sudo nginx -t` <br/>
If all is good you can now start setting up your load balancer.

## Setting up a load balancer in digital ocean
This step is pretty simple with digital ocean. <br/>
Click Create and then click load balancer. From here you set your region to SF3 and connect your droplets through the tag section. The two droplets that were created earlier had the `web` tag, so put the same `web` in the tag section, and you droplets will be connected.<br/>
Now that the load balancer is created, you can start configuring each server to act as a file server.

## configuring nginx file servers
Start by creating a new super user. Do this with `sudo --system -m -d /var/lib/webgen` -m is creating a home directory if one is not already made, and -d is the path to the home directory.<br/>
To get permission to enter the webgen directory you will have to change the ownership with `chown`<br/>
```sudo chown arch:arch webgen```<br/>
This allows you to enter the webgen directory. Here you need to make three more directorys: `bin`, `documents` and `HTML`. Do this using `touch`. Inside the `bin` dir, you will have to move the `generate_index` file found in the cloned git repo given.<br/>

Next the nginx.conf file will need to be configued. <br/>
Create two directories in `/etc/nginx` and name them `sites-enabled` and `sites-available`. Inside of `sites-available` create a new file `webgen.conf`. This file will hold the nginx server block config.<br/>
The server block inside of the `nginx.conf` will be removed as there is now one in `webgen.conf`
