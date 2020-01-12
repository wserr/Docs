---
title: "Publish ASP .NET Core App on a Raspberry Pi"
metaTitle: "Publish ASP .NET Core App on a Raspberry Pi"
metaDescription: "How to publish an ASP .NET Core App on a Raspberry Pi"
---

```csharp
var i = 0;
```


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

[Hosting an ASP NET core app on RPi](https://thomaslevesque.com/2018/04/17/hosting-an-asp-net-core-2-application-on-a-raspberry-pi/)