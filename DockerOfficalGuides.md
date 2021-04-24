# 1. Getting started

## Orientation and setup

* Overview
  * Build and run an image as a container
  * Share images using Docker Hub
  * Deploy Docker applications using multiple containers with a database
  * Running applications using Docker Compose

## Download and install Docker

* Skip

## Start the tutorial
``` Docker
docker run -d -p 80:80 docker/getting-started
```
* ` -d ` - 以分离模式运行Container（在后台）
* ` -p 80:80 ` - 映射宿主的端口到容器的端口
* ` docker/getting-started ` - 要用的镜像

> Tip
``` Docker
docker run -dp 80:80 docker/getting-started
```

## The Docker Dashboard

* The Docker Dashboard is available for Mac and Windows.

## What is container?

* 容器只是您计算机上的另一个进程，已与主机上的所有其他进程隔离。

## What is a container image?
* 当我们运行一个容器，它使用一个独立的文件系统。这个自定义的文件系统是由镜像提供的。因为镜像包含容器的文件系统，它必须包含运行应用程序的所有需要——所有的依赖，配置，脚本，目录等。镜像也包含容器的其它配置，例如环境变量，要运行的默认命令和其它元数据。

# 2. Sample application

## Get the app

* [Download the App contents](https://github.com/docker/getting-started/tree/master/app).
* Use your favorite editor to open the project.

## Build the app's container image

* Create a file named ` Dockerfile ` in the same folder as the file ` package.json ` with the following contents.

  ``` Docker
  # syntax=docker/dockerfile:1
  FROM node:12-alpine
  RUN apk add --no-cache python g++ make
  WORKDIR /app
  COPY . .
  RUN yarn install --production
  CMD ["node", "src/index.js"]
  ```
> Warning
> * No extension like `.txt`.

* Now build the container image using the `docker build` command.
  ``` Docker
  docker build -t getting-started .
  ```
> Explain
> * 这行命令用Dockerfile去创建一个新容器的镜像。用From指定我们想要从` node:12-alpine `镜像开始，但是我们机器上没有，所以需要下载。
> * 镜像下载之后，我们让我们的应用用` yarn `命令去按照我们应用的依赖。` CMD `是容器运行之后需要运行的命令。
> * 最后，` -t ` 你可以看成是给镜像的名字。因为我们把镜像命名为 ` getting-started ` ，当运行容器时我们好识别。
> * 在` docker build ` 后的 `.` 是告诉Docker在当前目录寻找 ` Dockerfile ` 文件。 

## Start an app container

* Using ` docker run ` command and specify the name of the image to start container.
  ``` Docker
  docker run -dp 3000:3000 getting-started
  ```
* open your web browser to http://localhost:3000


# 3. Upadate the application



