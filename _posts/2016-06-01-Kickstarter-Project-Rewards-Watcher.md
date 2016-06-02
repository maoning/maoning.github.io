---
layout: post
title: Kickstarter Project Reward Watcher
excerpt: "Watching Kickstarter Reward Tile's Availability, and Sending Push Notifications to iPhone"
categories: Ruby, Pushover, crontab
comments: true
---

As a regular Kickstarter project backer, it is very frustrating for me to see most of the early bird
reward tiles are all gone by the time I check the project. As a result, I came up with a simple Ruby
script to watch the project I'm interested in for me, and send me a push message to my iPhone once
the reward tile I want is available.

This was the first time for me to write a script in Ruby, I found the language is surprisingly easy to
pick up, and spent little time to complete the tasks I had in mind. Here is how I did it.

#### Use External Kickstarter API

The best undocumented Kickstarter library I found is [Kickscraper](https://github.com/markolson/kickscraper).
It is written in Ruby, and can get info on virtually anything from Kickstarter.

Here is the kickstarter_watcher.rb I wrote, so that I can keep an eye on the €25 early bird tile
of [Common Loon project](https://www.kickstarter.com/projects/573665728/common-loon-a-ruler-set-that-holds-a-world-of-crea)
.

{% highlight ruby %}
require 'kickscraper'
require 'http'

# Part I
Kickscraper.configure do |config|
    # replace with your kickstarter account email
    config.email = '<kickstarter email>'
    # replace with your kickstarter account password
    config.password = '<kickstarter password>'
end

c = Kickscraper.client
# search project name containing "Common Loon",
# and return first hit
vm = c.search_projects('Common Loon').first
# I cheated a bit here, counted my reward tile on the project page
# it is the 8th reward tile
reward = vm.rewards[8];

# USEFUL PROJECT RELATED INFO I USED FOR DEBUGGING PURPOSES
# print "==========================================================================================\n"
# print "Project Name: #{vm.name}\n"
# print "==========================================================================================\n"
# print "Reward Description:\n #{reward.description}\n"
# print "==========================================================================================\n"
# print "Backers Count: #{reward.backers_count}\n"
# print "Reward Limit: #{reward.limit}\n"

# output time stamp to log file, so that I could make sure the script actually runs
time1 = Time.new
puts "Current Time : " + time1.inspect + "\n\n"

# Part II
# Check if number of backers if below reward limit, if it is true,
# a pushover notification will be sent to my iPhone.  
if reward.backers_count < reward.limit
    HTTP.post('https://api.pushover.net/1/messages.json', :body =>
                "token=<pushover app token>&"\
                "user=<user id>&"\
                "message=#{vm.name}\nurls: #{vm.urls.web.project}&"\
                "title=Cheaper Reward Tile Available!!!"
                )
end

{% endhighlight %}

Part I. of the code uses the Kickscraper to get reward tile info for Common Loon project for me. In order to use the API,
I had to enter my Kickstarter credentials to construct the client.

#### Use Pushover to Send Notifications to iPhone
Long time ago, I came across [Pushover](https://pushover.net) as a notification service triggered by simple POST API.
Although I remember I purchased the one-time charge service, I never had real use for it until now.

I think I have the most basic plan, which gives me the ability to send 7500 messages per month for
free via their API calls. In order to send a verified message to my device, I specified following fields
in my POST request's body:

- token: I have to register an application in Pushover, and uses the created applicant's token
- user: this is my user key on my dash board on Pushover
- message: the content of the message I want to send
- title: title of the message (optional)
- priority: 1 for immediate notification. Alternatively, I can set up quiet hours and set the priority to a lower number. (optional)
- device: specify which device I want to send the msg to (optional).

In order to receive the message on my phone, I downloaded the Pushover app on my iPhone, logged in with my
Pushover account and assigned a device name to my phone. When I log onto your Pushover dashboard in my browser afterwards,
I would see my device name got listed there.

To make the POST request in Ruby, I have downloaded Ruby's http library, by doing ``` sudo gem install http ```

#### Write a Crontab Script on Mac to Run the Ruby Script Every 10 min
Now everything is set up, I just need to run the Kickstarter watcher script regularly in the background. A simple crontab script
on mac is sufficient for the job.

```bash
crontab -e # to edit the crontab file in vim

# enter following to the opened up editor, press i first to get into insert mode
*/10 * * * * /bin/bash -l -c 'ruby /Users/ning/Desktop/Ning/kickstarter/kickstarter_watcher.rb >> /Users/ning/Desktop/Ning/kickstarter/run.log'

# then press :wq to save and quit, you should see a message "crontab: installing new crontab"
```

I set a frequency of running the script every 10 min. Interestingly, I have to keep the asterisk (\*) for 10 min on Mac.
The standard linux crontab timing format can be found [here](http://www.unixgeeks.org/security/newbie/unix/cron-1.html).
