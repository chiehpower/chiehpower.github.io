---
title: DVC
description: <center> </center>
photos:
  - 'https://lh3.googleusercontent.com/pw/AM-JKLVcZMv8Y84R_6NNJRIcWCzF7z2YUEpvOoCQFj0DoTFvjX9IuybBYmxUdOO1GBIASjsTEAOCLOJQtPS10_-pTo-Pj29cawiP4yXgPawhWgENfavuwe9WajbOJdk82xkMox-8h-8u8J3WN4byuzb9pq3lQw=w2038-h1530-no?authuser=3'
date: 2021-09-01 16:31:21
tags:
categories:
password:
---

# DVC

Step:
*Do it in the .git directory.*
```
dvc init

## Add file
dvc add test
git add test.dvc
git commit -m "Add raw data"

### Add the remote source 
# For now, we only use local folder.
dvc remote add -d myremote /tmp/dvcstore
### If you use webhdfs 
dvc remote add -d myremote webhdfs://10.1.2.84:9870/tmp/webhdfs


# check the information
cat .dvc/config 
# Push the test folder to dvc 
dvc push 

### Add "test" folder into .gitignore
git add .dvc/configsolomon
git commit -m "Configure remote storage"
git push
```

If you wanna pull
```
dvc pull
```

# Setup WebHDFS Part [Failure]

Reference:
1. [hub.docker-hadoop-docker](https://hub.docker.com/r/sequenceiq/hadoop-docker/)
2. [Hadoop REST API – WebHDFS使用详解](https://blog.csdn.net/qq_45083975/article/details/106137674)
3. [DOCKER的HADOOP一鍵啟動之旅](http://paulfun.net/wordpress/?p=307)
    Use Docker to start HDFS: 
    ```
    sudo docker run -d --name=hadoop-dev-server \
        -p 8020:8020 \
        -p 8030:8030 \
        -p 8040:8040 \
        -p 8042:8042 \
        -p 8088:8088 \
        -p 19888:19888 \
        -p 49707:49707 \
        -p 50010:50010 \
        -p 50020:50020 \
        -p 50070:50070 \
        -p 50075:50075 \
        -p 50090:50090 \
        -p 9000:9000 \
        762e8eefc162 /etc/bootstrap.sh -d
    ```
4. [big-data-europe / docker-hadoop](https://github.com/big-data-europe/docker-hadoop)
    ```
    docker-compose up
    ```

## Commands

- Check the status:
    ```
    curl -i http://localhost:50070/webhdfs/v1/tmp\?user.name\=istvan\&op\=GETFILESTATUS
    ```

- Create a folder at the `/tmp/webhdfs`

    ```
    curl -i -X PUT http://localhost:50070/webhdfs/v1/tmp/webhdfs\?user.name\=istvan\&op\=MKDIRS
    ```

# Via SSH Part [Success]

Reference: 
1. [How do I use DVC with SSH remote](https://discuss.dvc.org/t/how-do-i-use-dvc-with-ssh-remote/279/2)

SUPPOSE : 
>hostname/ip: 10.1.2.30
user: Chieh
password: 123456789
port: 22

Let's add SSH remote.

I wanna put it in my remote server at `/home/user/tmp/` 
```
dvc remote add --default ssh-storage ssh://10.1.2.30/home/user/tmp/
dvc remote modify ssh-storage user Chieh
dvc remote modify ssh-storage port 22
dvc remote modify --local ssh-storage password 123456789
```

If you dont wanna record any information into `.dvc/config`, then you can use `--local` option.
Otherwise, it will be added into the git control.

## How to add new files?

When we change something new files in the tracked dvc folder, how can we add this new files into dvc?

For example, suppose I have a tmp folder, there is one `index` file inside. 

**Before**:
└── tmp
    └── index

After we `dvc add tmp`, it will generate a file as `tmp.dvc`.
And I add one document, `confusion.json`, into the tmp folder like below:

**After**:
└── tmp
    ├── index
    └── confusion.json

We can use `dvc add tmp` again, then it will update the tmp.dvc again. 
Dont forget to `git commit` this `tmp.dvc` file and `dvc push`.

We use `tmp.dvc` to control the files; hence, if you wanna get one files from specific commit, you can `git checkout (specific commit)` back to that one commit, and remove the original tmp folder and dvc pull the files from server.

Step:
```
dvc unprotect tmp
dvc add tmp

# Let's push to server
dvc push

# It will also update the .dvc file, so we need to git add it to do git control again.
git add tmp.dvc

# Regularly git commit and push it to git server.
git commit -m "Update tmp.dvc file"
git push
```

# Docker

Dockerfile:

```
FROM ubuntu:latest
RUN sed -i -e 's/archive.ubuntu.com/free.nchc.org.tw/' /etc/apt/sources.list
RUN apt-get update && apt-get install -y ssh openssh-server vim ca-certificates wget sudo

# RUN mkdir /var/run/sshd
RUN echo 'root:Root' | chpasswd
RUN sed -i 's/#PermitRootLogin/PermitRootLogin/' /etc/ssh/sshd_config
RUN sed -i 's/#PasswordAuthentication/PasswordAuthentication/' /etc/ssh/sshd_config
  
EXPOSE 22
ARG USER_ID=1000
RUN useradd -m --no-log-init --system  --uid ${USER_ID} user -g sudo
RUN echo 'user:user' | sudo /usr/sbin/chpasswd
RUN echo '%sudo ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers
# ENTRYPOINT sudo service ssh restart 
WORKDIR /home/user
USER $USER_NAME
RUN chmod 700 /home/user
CMD [ "bash" ]
```
Build image:
```
docker build -t dvc:0.1 .
docker run --rm -ti -p 8787:22 dvc:0.1 bash
```

# Requirements
```
pip3 install dvc 
```
If you use WebHDFS, you need to install this requirement.
```
pip3 install 'dvc[webhdfs]'
```
Or you can use `dvc[all]`




# Reference: 
- [DVC 介紹](https://www.dazhuanlan.com/wdgann/topics/1008692)