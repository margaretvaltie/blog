---
title: Moving Wordpress Content
author: mvaltie
date: 2020-03-31

---

## Migrating a Wordpress Blog to Static Website
### Part 2: Moving the Content

Lightsail was a great parking spot for the old Wordpress blog. [See part 1 of for that](/posts/migrating-to-static-blogs/).  I ended up keeping it there for almost a year and just redirected the Lightsail WP instance to blog.margaretmvaltierra.com so it looked good on the website. I never did get around to creating a cert and setting it up with https.

The non-https site and monthly cost finally motivated me to get back to updating the site. The other sticking part was what to migrate *to* and how. After some research, I decided Hugo and Netlify are best. 

I was initially worried because all the WordPress to static site guides and articles are at least 2 years old. The best one I found was on [Hackernoon by Phong Huynh](https://hackernoon.com/wordpress-to-static-site-generator-hugo-migration-and-deployment-788a69b93e66#6953) in 2018. It is straightforward  with steps to: create a GitHub repo, install and customize Hugo and viewing a sample site. The sticking point was "Exporting the Content" :

Hackernoon suggested the WordPress plugin [WordPress to Jekyll](https://github.com/benbalter/wordpress-to-jekyll-exporter/blob/master/docs/command-line-usage.md) but the plugin page notes it has not be tested with the 3 latest WP releases, and all the [comments note](https://wordpress.org/plugins/jekyll-exporter/) it does not work for them. Somewhat luckily for me I didn't read that until I'd tried it... 

### Notable differences
The plugin should just magically create a .zip file that downloads from the UI. Mine just timed out. I rebooted the Lightsail instance. No luck. I launched a larger Lightsail instance and started over with a new copy of the  website, this time with a whole 1GB of RAM and 40GB SSD. No luck. 

<img src="/wp-content/uploads/2020/03/wptojekylltimeout.jpg" alt="wp to jekyll timeout" width="400"/>

I ssh-ed into both instances and poked around. After way too much  aimless digging I found that the plugin was creating files in `/apps/wordpress/tmp` but I could not for the life of me get them to download. I spent too long trying to figure out the possible key permissions before I realized I should try to use SMTP. 

With Cyberduck and [this Bitnami guide](https://docs.bitnami.com/aws/faq/administration/upload-files/) I remembered what to do. There they were, the .zip files WP-to-Jekyll and WP-to-Hugo tools created. For whatever reason they just sat there but killed the WordPress UI. Thank goodness because I was doing crazy things like thinking about manually rewriting posts in markdown. Whew. 

Once I got the posts extracted and in Markdown, I did notice I was missing a fair amount of images, or contents of the wp-uploads folder. All my post images from 2019 are just missing.  

Another issue is that all the posts have `type = post` in the heading, which lost them to the Hugo blog's built in Archives and post listing. I had to make sure each post had the lable removed, which was annoying. I was going through each post anyway searching for lost media. 

Now back to the Hackernoon guide. I'll write more on the Netlify set up and deployment and customizing the domain in a part 3 post. 
