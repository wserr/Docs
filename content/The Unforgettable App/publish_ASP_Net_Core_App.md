---
title: "Publish to Raspberry Pi"
metaTitle: "Publish ASP .NET Core App on a Raspberry Pi"
metaDescription: "Explains how te app can be published to a Raspberry Pi"
---

On this page, I'll explain how to publish this ASP .NET core app to a Raspberry Pi. The reason I chose a Pi to deploy it to, is because this is a very accessible computer for anyone ranging from beginners to more advanced users. It is very easy to get it up and running. Following this tutorial, you'll be running a Raspberry pi Server in no time!

## Which database technology to use

### SQL

Being a .NET developer in windows, it is almost a no brainer for me to use a SQL database together with .NET core. However, at least as far as I know, it is not possible to run SQL server on a Raspberry Pi.

After typing this bold statement, I searched for evidence that could back me up. I searched on forums of Reddit [^2] and Raspberry Pi [^1], and I found mixed answers. A couple of years ago, this was unheard of. Now however, with the rise of Docker, it seems to be possible to run an ASP .NET Core application inside a container, then deploying it to the Pi. Microsoft even has documentation on how to put SQL server in a Docker container [^3]. I am curious if this will be possible. I will try this out for sure.




# Prerequisites
* Install raspbian
* Execute following code (point to a folder where to create new project):

```shell

dotnet new mvc
dotnet publish -c Release -r linux-arm

```

* install dependencies op RPi

```shell

sudo apt-get update
sudo apt-get install curl libunwind8 gettext apt-transport-https

```

# Deploy

* Copy all files from the bin\Release\netcoreapp2.0\linux-arm\publish directory to the Raspberry Pi, and make the binary executable (replace MyWebApp with the name of your app):

```shell

chmod 755 ./MyWebApp
./MyWebApp

```
## Trouble
```shell
Error:
  An assembly specified in the application dependencies manifest (Test.deps.json) was not found:
    package: 'Microsoft.AspNet.WebApi.Client', version: '5.2.6'
    path: 'lib/netstandard2.0/System.Net.Http.Formatting.dll'
```
Cause: my bad; wrong installation folder; you need to set the executable INSIDE the publish folder

# Expose app to network
When exposing the app to outside world: recommended to use reverse proxy => safety

```shell

sudo apt-get install nginx
sudo service nginx start

```

 Now you need to configure it so that requests arriving to port 80 are passed to your app on port 5000. To do that, open the /etc/nginx/sites-available/default

```shell
sudo nano /etc/nginx/sites-available/default
```

Replace location section with following:

```shell

location / {
        proxy_pass http://localhost:5000/;
        proxy_http_version 1.1;
        proxy_set_header Connection keep-alive;
}

```

reload nginx after editing

```shell
sudo nginx -s reload
```

# References

[^1]: [RaspberryPi.org - Forum about SQL Server](https://www.raspberrypi.org/forums/viewtopic.php?t=108343)
[^2]: [Reddit.com - Forum about SQL Server on Raspberry Pi](https://www.reddit.com/r/RASPBERRY_PI_PROJECTS/comments/4nswx2/run_a_ms_sql_server_on_a_raspberry_pi/)
[^3]: [Docs.Microsoft.com - Installation guidance for SQL Server on Linux](https://docs.microsoft.com/en-us/sql/linux/sql-server-linux-setup?view=sql-server-2017)

[^3]: [Hosting an ASP NET core app on RPi](https://thomaslevesque.com/2018/04/17/hosting-an-asp-net-core-2-application-on-a-raspberry-pi/)