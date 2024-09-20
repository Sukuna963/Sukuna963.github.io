---
layout: post
title: "Spring Boot With Kong Api"
author: "Leonardo Marques"
categories: software
tags: [java, api, docker, python]
image: kong/kong-spring.png
---

# Simple Api with route in Kong Gateway

|
[Code](https://github.com/Sukuna963/API_with_Kong_Gateway)
|


### technologies used
- jdk 22
- spring boot
- docker
- docker-compose
- python


## ApiController
```java
@RestController
public class KongController {

    @GetMapping
    public String hello() {
        return "Hello Kong Gateway";
    }
}
```

## DockerFile

```
FROM eclipse-temurin:22-jdk-alpine

RUN adduser -D username

USER username

COPY target/KongKeyAuthentication-0.0.1-SNAPSHOT.jar KongKeyAuthentication-0.0.1-SNAPSHOT.jar

CMD ["java","-jar","/KongKeyAuthentication-0.0.1-SNAPSHOT.jar"]
```

## docker-compose.yml

```
version: "3.9"
services:
  postgres:
    image: postgres:13
    restart: always
    hostname: kong-database
    container_name: kong-database
    environment:
      POSTGRES_USER: "kong"
      POSTGRES_DB: "kong"
      POSTGRES_PASSWORD: "kong"
    ports:
      - "5432:5432"
  kong-bootstrap:
    image: kong/kong-gateway:3.7.1.2
    hostname: kong-bootstrap
    container_name: kong-bootstrap
    depends_on:
      - postgres
    environment:
      KONG_DATABASE: "postgres"
      KONG_PG_HOST: "kong-database"
      KONG_PG_DATABASE: "kong"
      KONG_PG_USER: "kong"
      KONG_PG_PASSWORD: "kong"
    command: "kong migrations bootstrap"
    restart: 'on-failure'
  kong:
    image: kong/kong-gateway:3.7.1.2
    restart: always
    hostname: kong
    container_name: kong
    depends_on:
      - kong-bootstrap
    environment:
      KONG_DATABASE: "postgres"
      KONG_PG_HOST: "kong-database"
      KONG_PG_DATABASE: "kong"
      KONG_PG_USER: "kong"
      KONG_PG_PASSWORD: "kong"
      KONG_PROXY_ACCESS_LOG: '/dev/stdout'
      KONG_ADMIN_ACCESS_LOG: '/dev/stdout'
      KONG_PROXY_ERROR_LOG: '/dev/stderr'
      KONG_ADMIN_ERROR_LOG: '/dev/stderr'
      KONG_ADMIN_LISTEN: "0.0.0.0:8001"
      KONG_ADMIN_GUI_URL: "http://localhost:8002"
    command: "kong start"
    ports:
      - "8000:8000"
      - "8443:8443"
      - "8001:8001"
      - "8444:8444"
      - "8002:8002"
      - "8445:8445"
      - "8003:8003"
      - "8004:8004"
  api:
    container_name: api
    image: api
    restart: on-failure
    build: .
    ports:
      - "8080:8080"
networks:
  default:
    name: kong-net
```

## config_kong.py

Run the config_kong.py file to perform the necessary kong gateway configurations

```python
import requests
import json


URL = "http://localhost:8001"


def create_service():
    """
    To add a service, we send a POST request to the Kong Admin API. 
    We provide a name for our service, along with the URL where the service is found:
    """

    data = {
        "name": "api-server",
        "url": "http://api:8080"
    }

    response = requests.post(URL + "/services", json=data)
    print(response.text)
    

def creat_route():
    """
    A route is a path that Kong Gateway will listen to, 
    which it will then forward to the upstream service
    """
    data = {
        "name": "route-to-api",
        "service": {
            "name": "api-server"
        },
        "paths": ["/api"]
    }
    
    response = requests.post(URL + "/routes", json=data)
    print(response.text)


def add_key_authentication_plugin():
    """
    The Key Authentication plugin has several configuration options.
    For our simple use case, we will tell the plugin that the location of the API key
    will be in the request header called x-api-key
    """
    
    data = {
        "name": "key-auth",
        "config": {
            "key_names": ["x-api-key"],
            "key_in_header": True,
            "key_in_query": False,
            "key_in_body": False
        },
        "route": {
            "name": "route-to-api"
        }
    }
    
    response = requests.post(URL + "/plugins", json=data)
    print(response.text)


def create_consumer():
    """
    To create a consumer, we send a request to Kong’s Admin API. 
    The consumer is a separate resource not specifically tied to any service or route
    """
    
    data = {
        "username": "bob"
    }
    
    response = requests.post(URL + "/consumers", json=data)
    print(response.text)


def create_credential():
    """
    create a credential for our user
    """
    
    response = requests.post(URL + "/consumers/bob/key-auth")
    print(response.text)
    
    
print("------------------------------------------------------")
print("---------------- config kong services-----------------")
print("------------------------------------------------------")
create_service()
print("------------------------------------------------------")
creat_route()
print("------------------------------------------------------")
add_key_authentication_plugin()
print("------------------------------------------------------")
create_consumer()
print("------------------------------------------------------")
create_credential()
print("------------------------------------------------------")
```

## Execution

Copy the key generated in create_credential() and paste it in the header of the next request

![response](/assets/img/kong/reponse.png)