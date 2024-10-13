### 服务器
使用：
step1：上传数据
step2: 镜像下载/定制
step3: 创建交互式开发

#### docker
镜像(images) 容器(containers)
Dockerfile
- layer structure
  
workdir 设置镜像位置

User: docker run -d 这里的-d是什么 
##### execution

下面是 `docker run` 命令中一些常用选项的解释：

- `-d` 或 `--detach`：脱离模式运行容器。容器在后台运行，与运行它的命令行终端无关。
- `--name`：为容器指定一个名称。
- `-p` 或 `--publish`：端口映射，将容器内部的端口映射到宿主机的端口。
- `-e` 或 `--env`：设置环境变量。
- `-v` 或 `--volume`：挂载卷，将宿主机的文件系统挂载到容器内部。
- `--network`：指定容器的网络连接。
- `--restart`：设置容器的重启策略。
- `--cpus`：限制容器可以使用的CPU资源。
- `--memory` 或 `-m`：限制容器可以使用的内存大小。

例如，如果你想要运行一个名为 `my_container` 的容器，并且希望它在后台运行，可以使用以下命令：

```sh
docker run -d --name my_container my_image
```

这里 `my_image` 是你想要运行的镜像的名称。容器将使用 `my_image` 镜像创建，并在后台运行，同时被命名为 `my_container`。 
##### Example Dockerfile:
```Dockerfile
# Use an official Python runtime as a parent image
FROM python:3.8-slim

# Set the working directory in the container
WORKDIR /usr/src/app

# Copy the current directory contents into the container at /usr/src/app
COPY . .

# Install any needed packages specified in requirements.txt
RUN pip install --no-cache-dir -r requirements.txt

# Make port 80 available to the world outside this container
EXPOSE 80

# Define environment variable
ENV NAME World

# Run app.py when the container launches
CMD ["python", "app.py"]
```

#### 数据传输与环境配置
- 上传
使用filezilla
共享数据

- 环境配置
选取镜像  
  - 制作镜像-> 使用requirement文件（使用conda/pipd）
  - or (console)
  SSH `apt-get update` or `pip install`


## bug
服务器无conda环境
solution: wget download
made containers from current images

---