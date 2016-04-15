---
title:  "Setup Browser Quest on a Server"
date:   2015-02-29 23:22:59
categories: BrowserQuest 
---
## Initial Server Environment Setup

### Create a new droplet from digitalocean with Ubuntu 14.04 x64 OS.

  + copy over .bashrc file to import all the preferences

### Setup Apache and PHP
  + `apt-get update`
  + `apt-get install apache`
  + `apt-get install php5 libapache2-mod-php5 php5-mcrypt`
  + `sudo service apache2 restart`
  + vi /etc/hostname

    add following inside the file
  {% highlight bash %}
127.0.0.1 localhost
127.0.1.1 <name>
  {% endhighlight %}
  + vi /etc/apache2/apache2.conf

     Add 'ServerName localhost' 
  + `sudo service apache2 restart`

### Install BrowserQuest
  + `apt-get install git`
  + `git clone https://github.com/mozilla/BrowserQuest`
  + `apt-get npm`
  + `npm install underscore log bison websocket`
  + Had trouble to find source to install websocket-server, 
    download the folder from a web link instead
    
    `wget -r --no-parent http://reisyukaku.org/games/browserquest/node_modules/websocket-server/`

  + `npm install reisyukaku.org/games/browserquest/node_modules/websocket-server/`
  + `npm config set registry http://registry.npmjs.org/`
  + `npm install sanitizer memcache`
  +  Add to package.json  
{% highlight json %}
  , "repository": {
      "type": "git",
      "url": "https://github.com/maoning/BrowserQuest"
  }
{% endhighlight %}

  and changed all >0 to >0.0.0

  + installed nodejs

{% highlight bash %}
export NODE_VERSION='0.6.8'
wget http://nodejs.org/dist/node-v$NODE_VERSION.tar.gz
tar xvfz node-v$NODE_VERSION.tar.gz
cd node-v$NODE_VERSION
./configure --prefix=~/local
make install
cd ~
{% endhighlight %}

  + add node to path
   (see http://increaseyourgeek.wordpress.com/2010/08/18/install-node-js-without-using-sudo/)
{% highlight bash %}
   export PATH=~/local/bin:${PATH}
   echo 'export PATH=~/local/bin:${PATH}' >> ~/.bashrc
{% endhighlight %}

### Server Start
missing server config file editing info

`node server/js/main.js`

### Client Start
  + `npm install -g http-server`
  + for client config file, replace everything with
{% highlight json %}
{
"host": "<ip addr of server>",
"port": <server listening port, default is 8000>,
"dispatcher": false
}
{% endhighlight %}

  + build client in bin
{% highlight bash %}
chmod +x build.sh
./build.sh
{% endhighlight %}

  + start client
{% highlight bash %}
http-server -a <ip address of server> -p <client port num that is diff from server>
{% endhighlight %}

### Trouble Shooting
Sometimes the BrowserQuest page freezes at "connecting to server" page, it is due to 
the port you choose to use are already in used by some earlier straying processes.
If you check the output of starting the server, you would see:
{% highlight bash %}
[Fri Feb 27 2015 22:16:17 GMT-0500 (EST)] INFO Starting BrowserQuest game server...
[Fri Feb 27 2015 22:16:17 GMT-0500 (EST)] INFO world1 created (capacity: 10 players).
[Fri Feb 27 2015 22:16:17 GMT-0500 (EST)] INFO world2 created (capacity: 10 players).
[Fri Feb 27 2015 22:16:17 GMT-0500 (EST)] INFO world3 created (capacity: 10 players).
[Fri Feb 27 2015 22:16:17 GMT-0500 (EST)] INFO world4 created (capacity: 10 players).
[Fri Feb 27 2015 22:16:17 GMT-0500 (EST)] INFO world5 created (capacity: 10 players).
[Fri Feb 27 2015 22:16:17 GMT-0500 (EST)] ERROR uncaughtException: Error: listen EADDRINUSE
{% endhighlight %}
One thing you can do is to clear the port and restart server and client again.
{% highlight bash %}
fuser -k <port num>/tcp
eg. fuser -k 7000/tcp
{% endhighlight %}

