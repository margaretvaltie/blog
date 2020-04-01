---
title: "Migrating to Static Blogs"
author: mvaltie
date: 2020-03-23T17:04:57-05:00
---
 
# Migrating to Static Blog Posts

## Part 1 - self host Wordpress on Lightsail

My first goal was to move off of Wordpress hosts as soon as possible. I’d left my blog alone for a while, which is normal, but the last time I looked at it there were ads smack in the middle of a post. I forgot how annoying it can be to have a scammy “cops in IL *hate* this one weird trick” type of thing as you’re reading. 

My goal was to self-host ASAP. Eventually I could migrate away from WP and lead about some other website tools eventually. 

The guides from AWS and a few blogs were consistent: download the xml off site data, create a new instance in aws, then repopulate the site. 

I didn’t want to build a LAMP stack and mess with it all just to redo it for a simple blog. I wanted to try something new in AWS too so I chose a template - hosting Wordpress on [LightSail](https://www.awsgeek.com/Amazon-Lightsail/?ck_subscriber_id=512841042).   
 <img src="https://www.awsgeek.com/Amazon-Lightsail/Amazon-Lightsail.jpg" width="400" alt="LightSail visual from AWS Geek">
  
[LightSail visual from AWS Geek](https://www.awsgeek.com/Amazon-Lightsail/?ck_subscriber_id=512841042)

Lightsail is the beginner’s intro to AWS. The main benefit is to quickly use AWS resources for the uninitiated. Lightsail abstracts things that can bog down a beginner: myriads of choices of instances in EC2, networking, usage billing, etc. For one price - $3.50 per month - you can get an instance spun up with a pre-made stack like Wordpress from Bitmani. 

It was good enough for me and a spot to park my personal blog for a while. I could pay a bit more for a Load Balancer, extra compute or storage, and snapshots. Luckily for me I never got around to phase 2 which recommends setting up an ELB, cert and updating DNS settings to make it an https site which would cost $18. 

Of course my plan to move it to Lightsail for a short while has grown to over a year.  As side projects do. Luckily the price is steady, even if it is more than on demand for a minimum instance. 

Up next, [part 2: Moving Wordpress Content](/posts/2020-03-31-moving-wordpress-content/)

