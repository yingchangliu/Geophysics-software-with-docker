# Using Wechat on linux by docker and wine.
reference: https://github.com/top-bettercode/docker-wechat

### 准备工作

允许所有用户访问X11服务,运行命令:

```bash
    xhost +
```

### 运行

```bash
    docker run -d --name wechat --device /dev/snd --ipc="host"\
    -v /tmp/.X11-unix:/tmp/.X11-unix \
    -v $HOME/Tencent/WeChatFiles:/WeChatFiles \
    -e DISPLAY=unix$DISPLAY \
    -e XMODIFIERS=@im=fcitx \
    -e QT_IM_MODULE=fcitx \
    -e GTK_IM_MODULE=fcitx \
    -e AUDIO_GID=`getent group audio | cut -d: -f3` \
    -e GID=`id -g` \
    -e UID=`id -u` \
    bestwu/wechat
```
#### 维护
启动容器

```bash
docker start wechat
```

停止容器

```bash
docker stop wechat
```
### 更新

进入docker容器：docker exec -it wechat bash
运行以下命令更新深度软件包：

```bash
apt-get update

apt-get install -y deepin.com.wechat

```

删除容器

```bash
docker rm wechat
```
