---
layout: post
title: Medium - Docker Introduction
description: >
  <a href="https://medium.com/@kelvin_sp/docker-introduction-what-you-need-to-know-to-start-creating-containers-8ffaf064930a">원문 - Kelvin Salton do Prado</a>
author: author

---

Trend 파악을 Medium 기고문 요약 포스팅 - 컨테이너를 생성하기 위해 당신이 알아야 할 것

![500x400](https://miro.medium.com/max/1400/1*y6CvfE6WUgoIdT8Mp0Ev_g.png)

이것은 따라하는 튜토리얼 입니다. 그러니까 커피를 가지고 느긋하게 앉아서 컨테이너를 만들어 봅시다. 오늘은 도커의 기본적인 사항을 배울 것이며 어떻게 빌드하고 실행하고 컨테이너를 삭제하는지 알아볼 겁니다.


당신은 이러한 유명한 문장에 대해 들어봤나요? "제 컴퓨터에서 동작할까요?"

![500x400](https://miro.medium.com/max/800/1*qY9Mmc2k_agwALr2UGY-8g.png)
도커와 함께라면 더 이상 아무 문제되지 않습니다. 도커는 제품이 논리적으로 동일한 환경에서 실행되도록 해줍니다.
자 그러면 도커에 대해서 이해해 봅시다. 도커는 무엇이고 어떤게 도커가 아닌지.

### Docker is...

저는 도커가 21세기의 가장 위대한 발명 중 하나라고 생각합니다. 그러나 여기서는 제 의견을 토론하는 자리가 아니죠 기술적인 측면만 알아봅시다.

도커는 컨테이너 제이션이라는 OS 수준의 가상화를 수행하는 컴퓨터 프로그램입니다

그것을 넘어서 도커는 컨테이너를 통해서 프로그램들을 쉽게 빌드하고 배포할 수 있게 해주는 유명한 도구입니다. 컨테이너는 응용 프로그램이 필요한 외부 라이브러리나 다른 종속성들을 패키지에 담을 수 있게 해줍니다. 이런 식으로 우리의 응용프로그램은 어떤 머신에서도 똑같은 동작을 하게 되는 것입니다.

도커는 2013년에 처음 릴리즈 되었으며 5년만에 스포티파이나 페이팔 같은 많은 회사에서 사용하고 있습니다. 그리고 도커는 <b>오픈 소스</b>입니다.

### Docker is not...

도커는 VM은 아닙니다. 컨테이너로서 VM이 아니며 분리된 OS를 요구하거나 포함하지 않습니다. 대신에 도커는 커널의 기능과 독립된 cpu와 메모리에 의존합니다. 그리고 응용프로그램의 관점에서 독립된 네임스페이스를 필요로 합니다.

![500x400](https://miro.medium.com/max/1400/1*gVNbunchCV5wXgnwlT-iGg.jpeg)

위의 이미지와 같이 도커는 VM보다 훨씬 간단하고 VM을 유지하고 실행하는 오버해드를 피할 수 있습니다.

이것은 손 쉬운 튜토리얼 이므로 어떻게 도커가 동작하는지 까지는 다루지 않습니다. 그런 것을 알고싶다면 도커 문서를 참조하세요!

### Hands-on
도커를 설치해 봅시다!

<a href ="https://docs.docker.com/docker-for-mac/install/"> install Docker for Mac
</a>

<a href ="https://docs.docker.com/docker-for-windows/install/">
install Docker for Window
</a>

<a href = "https://docs.docker.com/install/linux/docker-ce/ubuntu/">
Get Docker CE for Ununtu
</a>

### Hello World

```
$ docker run hello-world
Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
9db2ca6ccae0: Pull complete
Digest: sha256:4b8ff392a12ed9ea17784bd3c9a8b1fa3299cac44aca35a85c90c5e3c7afacdc
Status: Downloaded newer image for hello-world:latest
Hello from Docker!
This message shows that your installation appears to be working correctly.
...
```
### Creating and Running containers

```
from flask import Flask
app = Flask(__name__)
@app.route("/")
def hello():
    return "Hello World!"
if __name__ == "__main__":
    app.run(debug=True, host="0.0.0.0")
```

```
# Inherit from the Python Docker image
FROM python:3.7-slim
# Install the Flask package via pip
RUN pip install flask==1.0.2
# Copy the source code to app folder
COPY ./app.py /app/
# Change the working directory
WORKDIR /app/
# Set "python" as the entry point
ENTRYPOINT ["python"]
# Set the command as the script name
CMD ["app.py"]
```

```
$ docker run -d -p 5000:5000 flask_app:0.1
$ docker ps
CONTAINER ID   IMAGE           COMMAND             CREATED
03c650a4eb58   flask_app:0.1   "python app.py"   16 seconds ago
STATUS              PORTS                    NAMES
Up 3 seconds        0.0.0.0:5000->5000/tcp   gifted_kar

```

### Stopping and Removing containers

```
$ docker stop gifted_kar
# or
$ docker stop 03c650a4eb58
```

```
$ docker rm gifted_kar
# or
$ docker rm 03c650a4eb58
```
### Basic Commands

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

위의 예제를 통해 도커의 기본을 이해했으면 좋겠네요 고맙습니다!
