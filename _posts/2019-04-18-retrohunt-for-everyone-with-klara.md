---
title: "Klara: Private retrohunting platform"
date: "2019-04-18"
image: assets/images/Screenshot-2019-04-19-at-02.00.21.png
author: jpalanco
layout: post
tags: [ klara, malware, retrohunt, yara]
categories: [ intelligence, research ]
---

Let's talk about malware hunting. Sometimes you may find an interesting malware sample, and after reversing it you realize that the binary has characteristics that make it unique like the size, some bytes at a certain position or a specific header or resource.

If you are familiar with VirusTotal Hunting and Yara, maybe you played already with retro-hunt. Basically, you can run a Yara scan over the files received by VT during the last 3 months and this is awesome. Actually, VT improved their platform recently and they introduced [THREAT HUNTER PRO](https://www.virustotal.com/gui/threat-hunter-pro-overview), which will allow queries over the files received during the last year, we are talking about 5 petabytes.

What if we have a huge collection of malware and we want to do some retro-hunting? We can do it because of [Kaspersky GReAT](https://great.kaspersky.com/). They built a very cool technology which allows scanning 10TB of files in 30 minutes. Brilliant!
 

If you want to deploy your own instance of Klara, you can follow the instructions at their [GitHub repository](https://github.com/KasperskyLab/klara) or if you prefer you can start playing with my docker compose version before, continue reading.

You will need to install docker, docker-compose and a huge collection of malware. You can download collections of malware samples from:

- [VirusShare](https://virusshare.com/)
- [VirusSign](http://www.virussign.com/)
- [VxVault](http://vxvault.net/ViriList.php)
- [URL Haus Abuse](https://urlhaus-api.abuse.ch/downloads/)

Fetch the code from my [repository](https://github.com/jpalanco/klara-docker-compose):

```
git clone https://github.com/jpalanco/klara-docker-compose.git
```

Modify the variables as you need, you will find them at .env.

Copy your malware to klara-repository/repository/virus\_repository/

Build the containers:
```
docker-compose build
```
Run the containers:
```
docker-compose up
```
You will see information about the services running, after a couple of minutes you will be able to log in via [http://localhost/](http://localhost/) (unless you changed the variable at the .env file)

![]({{ site.baseurl }}/assets/images/Screenshot-2019-04-19-at-00.54.34-1024x556.png)

The admin credentials are:

- user: admin
- password: super\_s3cure\_password

Regular user credentials are:

- user: john
- password: super\_s3cure\_password

After login, you will see the following interface:

![]({{ site.baseurl }}/assets/images/Screenshot-2019-04-19-at-00.55.08-1024x319.png)

At profile, you may need to set up your email address before creating jobs, however, the notifications may not work because my implementation of Klara lacks of notifications at the moment.

Once you configured your email address you can create a job:

![]({{ site.baseurl }}/assets/images/Screenshot-2019-04-19-at-00.58.52-1024x994.png)

If you don't know how to write Yara rules, you can pick some from [https://github.com/Yara-Rules/rules](https://github.com/Yara-Rules/rules)

At the repository section you may check the repositories, at this moment we have only one repository configured: virus\_repository.

Now you can launch the job and enjoy your results:

![]({{ site.baseurl }}/assets/images/screencapture-klara-jpalanco-index-php-jobs-view-1-2019-04-19-01_11_18-795x1024.png)

Happy hunting!
