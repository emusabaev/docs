---
title: Getting Started with IronMQ v3
layout: default
section: mq
---
<p>Connect your applications and processes with an elastic message queue. Decouple your processes and create a highly scalable system by passing messages. This example is in Ruby, but can be done in your language of choice. You can find all of our client libraries <a href='http://dev.iron.io/mq/3/libraries'>here</a>/</p>

This is a VERY high level overview of a complex tool.



<h2>Create a Project and Setup Credentials</h2>

Before starting, you'll need to setup a couple of things. You only need to do this once.

First, create a project to put this example into.<br>
<img src='https://raw.githubusercontent.com/iron-io/docs/gh-pages/images/newProject.png' style='width: 400px; margin-left: -250px;'>

Click the MQ 3 button next to the title to go to the project's dashboard.
<img src='https://raw.githubusercontent.com/iron-io/docs/gh-pages/images/dashButton.png' style='width: 400px; margin-left: 66px;'>

Now lets create a directory on our local computer to hold this project. I'm calling mine mqExample, but yours can be anything you'd like. After it's made, CD into it:
{% highlight bash %}
$ mkdir mqExample
$ cd mqExample
{% endhighlight %}


Great, the last thing we need to is download the iron.json file and move it into that directory. For alternative ways, [please see the configuration page](/worker/reference/configuration/)<br>
<img src='https://raw.githubusercontent.com/iron-io/docs/gh-pages/images/ironDown.png' style='width: 400px; margin-left: -142px;'>
{% highlight bash %}
$ mv ~/Downloads/iron.json .
{% endhighlight %}


Now, we're all done with the setup process and can get to work.

<h2>Create a Queue and Add a Message</h2>

In your working directory, create a file called example.rb containing:
{% highlight ruby %}
# Get package here: https://github.com/iron-io/iron_mq_ruby
require 'iron_mq'

#Create an IronMQ client object
#The api_version can also be placed in your iron.json file if you prefer
ironmq = IronMQ::Client.new(
    api_version: 3
    )

#create a queue
queue = ironmq.queue('My_Very_First_Queue')

#add a message to the queue
queue.post('IronMQ v3 is great!')
{% endhighlight %}


This simple script creates a queue called My_Very_First_Queue with one message in it. Let's go ahead and run it
{% highlight bash %}
$ ruby example.rb
{% endhighlight %}


Now, if you refresh your dashboard, you should see that queue waiting for you:
<img src='https://raw.githubusercontent.com/iron-io/docs/gh-pages/images/newQueue.png' style='width: 400px; margin-left: 63px;'>

You can click on the queue name to see more information about that queue:
<img src='https://raw.githubusercontent.com/iron-io/docs/gh-pages/images/queueInfo.png' style='width: 400px; margin-left: 75px;'>

<h2>Process/Consume the Messages</h2>
From here, you can work with the queue via the Hud UI, programatically, or the Iron CLI, whichever you prefer. Because I don't need this message for anything, I'll get rid of it.

If you don't already have the CLI installed, [please click here](/worker/cli/) for installation instructions

We'll be using the pop tool. For information on this speific tool as well as all of the other features in the CLI, please refer to their man pages(--help). 
{% highlight bash %}
$ iron mq pop My_Very_First_Queue
{% endhighlight %}


If you watch the dashboard as you send that command, you'll see the message being removed in the realtime data graph.
<img src='https://raw.githubusercontent.com/iron-io/docs/gh-pages/images/postPop.png' style='width: 400px;'>
