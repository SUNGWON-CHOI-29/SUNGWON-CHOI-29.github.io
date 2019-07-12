---
layout: post
title: Medium - Docker Introduction
description: >
  <a href="https://medium.com/@kelvin_sp/docker-introduction-what-you-need-to-know-to-start-creating-containers-8ffaf064930a">원문 - Kelvin Salton do Prado</a>
author: author

---

Trend 파악을 Medium 기고문 요약 포스팅 - 컨테이너를 생성하기 위해 당신이 알아야 할 것

![500x400](https://miro.medium.com/max/1400/1*y6CvfE6WUgoIdT8Mp0Ev_g.png)

## Docker is...

![500x400](https://miro.medium.com/max/800/1*qY9Mmc2k_agwALr2UGY-8g.png)

## Docker is not...

![500x400](https://miro.medium.com/max/1400/1*gVNbunchCV5wXgnwlT-iGg.jpeg)

## Hands-on

## Basic Commands

```
# Build a Docker image
$ docker build -t [image_name]:[tag] .
# Run a Docker container specifying a name
$ docker run --name [container_name] [image_name]:[tag]
# Fetch the logs of a container
$ docker logs -f [container_id_or_name]
# Run a command in a running container
$ docker exec -it [container_id_or_name] bash
# Show running containers
$ docker ps
# Show all containers
$ docker ps -a
# Show Docker images
$ docker images
# Stop a Docker container
$ docker stop [container_id_or_name]
# Remove a Docker container
$ docker rm [container_id_or_name]
# Remove a Docker image
$ docker rmi [image_id_or_name]
```

## Useful Commands

```
# Stop all running containers
$ docker stop $(docker ps -q)
# Remove all containers
$ docker rm $(docker ps -aq)
# Remove all images
$ docker rmi $(docker images -aq)
```
## Integration

![500x400](https://miro.medium.com/max/1000/1*nWBoq5XMyxogKNGBz_rJ-A.png)
