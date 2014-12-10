---
title: Setting up Netflix OSS With Docker
layout: post
---

Wanted to evaluate Netflix's OSS. So, I decided to look at their RSS sample app. I also wanted to evaluate Docker, so I decided to use some of the Docker containers released by Netflix to get the RSS sample up and running. These are some of my notes.

Loosely followed the instructions here:

https://github.com/Netflix/recipes-rss/wiki

Also used some info from:

https://github.com/Netflix-Skunkworks/zerotodocker


# Setting up Eureka

First, I got the Eureka docker container. I did this just by running the eureka docker container with the command:

docker run -d --name eureka -p 8080:8080 netflixoss/eureka:1.1.142

Note the -p part, I found that I had to specify the external container port to get this to work. I suspect this is because I'm running this within a boot2docker vm on a Mac. 

Once I got this going, I had to figure out the boot2docker ip address. The IP for the boot2docker VM can be determined using the command: boot2docker ip

My boot2docker ip was 192.168.59.103, so now when I go to http://192.168.59.103:8080/eureka I see the Eureka web app running.

# Building the Middle Tier and Edge Tier of the Recipes RSS app

Since Eureka is sitting on a different host I changed the middletier.properties and edge.properties files to point to the proper Eureka instance:

e.g.

eureka.serviceUrl.default=http://192.168.59.103:8080/eureka/v2/

Once these changes are made then I built those tiers following the instructions at:

https://github.com/Netflix/recipes-rss/wiki/Building-RSS-Middle-Tier-and-Edge

# Running the App:

I then ran the app following the instructions here:

https://github.com/Netflix/recipes-rss/wiki/Running-the-RSS-Reader-Recipes-application

Note that you don't have to follow the Eureka instructions since that's already running in it's own Docker container.


# Bringing Source into Eclipse

# Add the Gradle plugin to eclipse: http://dist.springsource.com/release/TOOLS/gradle/





