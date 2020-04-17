---
title: gitlab-update
date: 2020-04-17 17:47:33
tags: gitlab
---
- 今天对**gitlab**进行升级，发现还是比较方便对。我这边是使用 docker 来部署**gitlab**。查看了官网文档进行升级

>
 - [更新日志](https://gitlab.com/gitlab-org/omnibus-gitlab/blob/master/CHANGELOG.md) 
 - [官网docker部署](https://docs.gitlab.com/omnibus/docker/)
 
- 直接拉取最新的**docker**镜像，按照官方进行部署

1. 停止现有容器
```bash
docker stop gitlab
```
2. 删除现有容器
```bash
docker rm gitlab
```
3. 部署
```bash
sudo docker run --detach \
  --hostname gitlab.example.com \
  --publish 443:443 --publish 80:80 --publish 22:22 \
  --name gitlab \
  --restart always \
  --volume $GITLAB_HOME/gitlab/config:/etc/gitlab \
  --volume $GITLAB_HOME/gitlab/logs:/var/log/gitlab \
  --volume $GITLAB_HOME/gitlab/data:/var/opt/gitlab \
  gitlab/gitlab-ce:latest
```
> - 其中 **$GITLAB_HOME** 就是服务器中外挂文件的地址。
  - `gitlab.example.com` 指访问的地址，使用ip访问不设域名可以直接设置ip地址
  - 这里使用`--publish 80:80`会占用到`ssh`的端口，需要更改服务器的设置，把`ssh`的端口变更到其他端口
  - `--restart always` 会睡着**docker**启动
  - `gitlab-ce:latest` 最新的镜像，也可指定想要升级的版本
- 这边需要注意的点是`gitlab`会自动升级，不需要再进行设置