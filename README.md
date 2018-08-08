# Nginx Reverse Proxy for Web Applications

This is a generic Docker image that provides an Nginx reverse proxy for any application running
in a Docker container with port 8080 exposed and accessible to the container running this image.

## Build and Deploy

```
$ docker build -t jvandusen/nginx-proxy-webapp .
```

## Use

To provide a reverse proxy to a container running an image called "example/some-webapp", first
create the container for the "example/some-webapp" image, giving it the name "webapp". Then
create the proxy container.

```
$ docker run -d --name webapp jvandusen/example
$ docker run -d -p 80:80 --name proxy jvandusen/nginx-proxy-webapp
```

If you're using Docker Compose, your docker-compose.yml file should look something like this:

```
version: "3"

services:
  webapp:
    image: example/some-webapp:latest
  proxy:
    image: jvandusen/nginx-proxy-webapp
  ports:
  - "80:80"
```

## Troubleshooting

In the image, Nginx is configured to proxy to an application that is accessible using the DNS
name "webapp", therefore you need to ensure that the container your web application is running
in has the name "webapp", otherwise Nginx will not be able to access it.