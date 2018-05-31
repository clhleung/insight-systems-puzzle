# insight-systems-puzzle
System-puzzle for insight

## Background regarding the tools involved in this challenge

I previously had some experience working with Docker and Python Flask as part of my coursework in University of California, Santa Cruz.
The only new things I had to learn about were the Docker-compose function, a bit of the PostGres SQL stuff, and the Nginx, for its
web server and reverse address proxying abilities. 

## Minor Notes

Because I am coding on a Windows 7 laptop, I have to run Docker using Docker Toolbox, which involves running a Linux VM inside Oracle 
VirtualBox, where nothing will be ```localhost``` and will always be ```192.168.99.100``` by default for me and for others who may run 
Docker ToolBox to complete this challenge. 

## A sense of how I did this challenge

First step for me was to get familiar with the files and how they interacted with each other. And, from the description, the main idea for me was that the challenge was primarily split into three, distinct parts.

Nginx <-----> Python Flask <-----> PostGres SQL

Nginx would be the web server the process client requests, and do the reverse addressing from 8080 to the exposed port 80 in the Docker
Python app. Python Flask, would host the actual contents of the web app the user would see and interact with. PostGres would be 
responsible for the database backend. 

### Nginx

Related files: flaskapp.conf (within conf.d folder), docker-compose.yml

Initially, when I tried running it, as expected, it did not run after executing the 3 Docker commands. Instead, I got nothing back,
which meant that the application could not even connect to the web server in the first place, which needed to be fixed.

### Python Flask

Related files: flaskapp.conf, Dockerfile, app.py

After fixing why the app could not reach the Nginx web server, another error I had to fix was the 502 bad gateway error. Although
it was still terrible, at least I could connect to Nginx now. This one was pretty simple, since I just had to specify the port to 
5001, since by Python Flask standards, leaving the port blank defaults to 5000, which was bad considering most of files specified 
5001 as the desginated port for the Python app. 

### PostGres SQL

Related files: app.py, models.py

As I worked my way down, the errors became more easier to recognize. Fixes here involved making the app initialize the 
database before its first request, as well as add a __repr__ function to format the results that get returned when the 
database is queried. 
