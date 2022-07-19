# 青龙面板

------



> 本教程镜像克隆于https://hub.docker.com/r/whyour/qinglong
>
> 也可查看大佬Github:https://github.com/whyour/qinglong 了解更多详情



## 说明

本教程只适用于linux/amd64下部署（推荐使用Centos7.6)

## docker部署

### 1.docker安装（已有docker的跳过）

#### 1)检查数据更新

```shell
sudo yum check-update
```

#### 2)拉取镜像并安装

```shell
curl -sSL https://get.daocloud.io/docker | sh
```

> 如果这一步比较慢直接按 `Ctrl + C` 结束，然后用方法二安装

方法二

#### 1)数据检查更新

```shell
sudo yum update
```

#### 2)安装docker

```shell
yum install docker
```

### 2.docker服务设置（已有docker的跳过）

#### 1)启动docker服务

```shell
sudo systemctl start docker
```

#### 2)查看docker服务状态

```shell
sudo systemctl status docker
```

#### 3)docker服务开机自启

```shell
sudo systemctl enable docker
```

### 3.部署

#### 1)拉取镜像

```shell
docker pull rewzh96w/qinglong:2.10.13
```

#### 2)创建容器

> 冒号前面的5700为端口号，可自行修改

```shell
docker run -dit \
  -v $PWD/ql/config:/ql/config \
  -v $PWD/ql/log:/ql/log \
  -v $PWD/ql/db:/ql/db \
  -v $PWD/ql/repo:/ql/repo \
  -v $PWD/ql/raw:/ql/raw \
  -v $PWD/ql/scripts:/ql/scripts \
  -v $PWD/ql/jbot:/ql/jbot \
  -v $PWD/ql/deps:/ql/deps \
  -p 5700:5700 \
  --name qinglong \
  --hostname qinglong \
  --restart unless-stopped \
  rewzh96w/qinglong:2.10.13
```

#### 3)多容器

```
docker run -dit \
  -v $PWD/ql2/config:/ql/config \
  -v $PWD/ql2/log:/ql/log \
  -v $PWD/ql2/db:/ql/db \
  -v $PWD/ql2/repo:/ql/repo \
  -v $PWD/ql2/raw:/ql/raw \
  -v $PWD/ql2/scripts:/ql/scripts \
  -v $PWD/ql2/jbot:/ql/jbot \
  -v $PWD/ql2/deps:/ql/deps \
  -p 9527:5700 \
  --name qinglong2 \
  --hostname qinglong2 \
  --restart unless-stopped \
  rewzh96w/qinglong:2.10.13
```



## 删除

#### 镜像删除

```shell
docker rmi rewzh96w/qinglong:2.10.13
```

#### 容器删除

先查看容器id

```shell
docker ps -a
```

```shell
docker rm -f id
```


##如有其他问题可以联系rewzh96@gmail.com
