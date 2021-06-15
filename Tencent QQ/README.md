# Using QQ on Linux through wine and docker.


### 准备工作

允许所有用户访问X11服务,运行命令:

```bash
    xhost +
```

### 运行QQ

```bash
  docker run -d --name qq \
    --device /dev/snd --ipc="host"\
    -v $HOME/Tencent/QQFiles:/TencentFiles \
	-v /tmp/.X11-unix:/tmp/.X11-unix \
    -e XMODIFIERS=@im=fcitx \
    -e QT_IM_MODULE=fcitx \
    -e GTK_IM_MODULE=fcitx \
    -e DISPLAY=unix$DISPLAY \
    -e AUDIO_GID=`getent group audio | cut -d: -f3` \
    -e VIDEO_GID=`getent group video | cut -d: -f3` \
    -e GID=`id -g` \
    -e UID=`id -u` \
    bestwu/qq:im
```


#### 维护
启动容器

```bash
docker start qq
```

停止容器

```bash
docker stop qq
```

### 更新

进入docker容器：docker exec -it qq bash
运行以下命令更新深度软件包：

```bash
apt-get update


# 更新企业版
# apt-get install -y deepin.com.qq.b.eim 
# 更新QQ
apt-get install -y deepin.com.qq.im
# 更新轻聊版
# apt-get install -y deepin.com.qq.im.light 
# 更新TIM
# apt-get install -y deepin.com.qq.office

```

删除容器

```bash
docker rm qq
```

