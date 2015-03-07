---
title:  "BrowserQuest Dev Environment Setup"
date:   2015-03-01 14:58:00
categories: BrowserQuest 
---
## BrowserQuest Dev Environment Setup

### Make a "Private Fork" of Official Source Code 
If you want to make a private repo off the official copy on git,
you can't directly fork the mozilla git repo. Steps are detailed [here](http://stackoverflow.com/questions/10065526/github-how-to-make-a-fork-of-public-repository-private)

### Make a Local Clone

cd to a directory where you want to put your copy at

run `git clone` on the repo you just created

Example: `git clone https://github.com/maoning/BQ.git`

### Change BrowserQuest Map Config 

  + Download [Tiled Map Editor](http://www.mapeditor.org)
  + Open the Tiled Editor and load the map file from your local repo
    at `<YourRepoName>/tools/maps/tmx`
  + You can modify existing layers or add new layers, the interface is similar to Photoshop
  + After you are satisfied with your change, save it
  + Export map file to the readable format for server and client

      May need to install following things:

      node modules like underscore, log, bison ... see previous post.

      python and nodejs

      pip

      lxml: `pip install lxml`

      Run following cmds to export maps:
 
      {% highlight bash %}
cd toos/maps
./export.py client
./export.py server 
      {% endhighlight %}

  + Push it back to the remote repo
   
    `cd to your repo's top dir`

    `git add --all`

    `git commit -am "message for the changes"`

    `git push`

  + Sync/Update the local repo on server

    Log into the server local repo, and do a `git pull` to get the latest change

    Restart server and client again

    Now you should be able to see your changes right away
