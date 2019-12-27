# NGINX + SSL

#### A simple docker configuration to use NGINX with HTTPS for development

This is a simple Dockerfile that uses the latest NGINX image and creates a self  
signed certificate to enable the default SSL. This is suitable for development  
and testing, not for production.

## Requiriments
Have a local folder named htdocs

`$ mkdir htdocs`

For a test, make a file named index.php and save in htdocs folder created before.
#### content of index.html
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Hello NGINX</title>
</head>
<body>
    <p>Hello!</p>
</body>
</html>
```

Now you are ready for the next step.

## Usage

### MAC or Linux
`$ docker container run -d -p 80:80 -p 443:443 -v $(pwd)/htdocs:/var/www periscuelo/nginx-ssl`
#### with default.conf
`$ docker container run -d -p 80:80 -p 443:443 -v $(pwd)/htdocs:/var/www -v $(pwd)/default.conf:/etc/nginx/conf.d/default.conf periscuelo/nginx-ssl`

### Windows PowerShell
`$ docker container run -d -p 80:80 -p 443:443 -v ${pwd}/htdocs:/var/www periscuelo/nginx-ssl`
#### with default.conf
`$ docker container run -d -p 80:80 -p 443:443 -v ${pwd}/htdocs:/var/www -v ${pwd}/default.conf:/etc/nginx/conf.d/default.conf periscuelo/nginx-ssl`


### docker-compose

#### The `default.conf` volume is necessary only if you want change something there.

```
# docker-compose.yml
version: '3'

services:
  webserver:
    image: periscuelo/nginx-ssl
    ports:
      - 80:80
      - 443:443
    volumes:
      - ./htdocs:/var/www
      - ./default.conf:/etc/nginx/conf.d/default.conf
```
`$ docker-compose up -d`

### Terminal Access
You can access `nginx` too. For this, use the following command:

`$ docker exec -it ID_OR_NAME_OF_YOUR_CONTAINER bash`

You have to replace `ID_OR_NAME_OF_YOUR_CONTAINER` for  the respective Container ID or Container NAME.  
Ex: If my container id is f3c99c3239ex then, the command must be:

`$ docker exec -it f3c99c3239ex bash`

Inside the terminal you can use the `nano` as you want.  
For example:

`$ nano test.txt

For exit of terminal after, the command must be:

`$ exit`

And you come out of container.

# Enjoy

You can access the server by https://localhost or http://localhost now!  
Put your files in htdocs to access by URL. Have fun =)
