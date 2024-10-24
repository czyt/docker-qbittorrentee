# qBittorrent Enhanced Edition in Docker

## 简介

这是一个 [qBittorrent Enhanced Edition](https://github.com/c0re100/qBittorrent-Enhanced-Edition) 的 Docker 镜像。
Fork自 [linuxserver/docker-qbittorrent](https://github.com/linuxserver/docker-qbittorrent)，并使用了 [SuperNG6/Docker-qBittorrent-Enhanced-Edition](https://github.com/SuperNG6/Docker-qBittorrent-Enhanced-Edition) 的部分代码。在此感谢上述开源工作者的无私付出。

aarch64 架构的代码未经测试。

### 特性

- 修复了 [SuperNG6/Docker-qBittorrent-Enhanced-Edition](https://github.com/SuperNG6/Docker-qBittorrent-Enhanced-Edition) 最新版本中PUID/PGID未生效的问题。
- 以 [linuxserver/docker-qbittorrent](https://github.com/linuxserver/docker-qbittorrent) 构建镜像为基础，将原版 [qBittorrent](https://github.com/qbittorrent/qBittorrent) 替换为了 [qBittorrent Enhanced Edition](https://github.com/c0re100/qBittorrent-Enhanced-Edition) ，更适合大陆人使用。

## 使用方法

### Docker Compose (推荐)

```yaml
version: '3'

services:
  qbittorrent:
    image: rogunt/qbittorrentee:latest
    container_name: qbittorrent
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Asia/Shanghai
      - WEBUI_PORT=8080
      - TORRENTING_PORT=6881
    volumes:
      - ./qb/appdata:/config      # 配置文件路径，请自行映射
      - ./qb/downloads:/downloads # 下载路径，请自行映射
    ports:
      - 8080:8080
      - 6881:6881
      - 6881:6881/udp
    restart: unless-stopped
```

### Docker CLI
```bash
docker run -d \
  --name qbittorrentee \
  -e PUID=1000 \
  -e PGID=1000 \
  -e TZ==Asia/Shanghai \
  -e WEBUI_PORT=8080 \
  -e TORRENTING_PORT=6881 \
  -p 8080:8080 \
  -p 6881:6881 \
  -p 6881:6881/udp \
  -v ./qb/appdata:/config \
  -v ./qb/downloads:/downloads \
  rogunt/qbittorrentee:latest
```


### 从源码构建

```bash
git clone https://github.com/Rougnt/docker-qbittorrentee.git
cd docker-qbittorrentee

docker compose up -d
```

# 其他文档
- [LinuxServer Docker qBittorrent](README-linuxserver.md)
- [SuperNG6/Docker-qBittorrent-Enhanced-Edition Readme](https://github.com/SuperNG6/Docker-qBittorrent-Enhanced-Edition/blob/master/README.md)

# 鸣谢

https://github.com/qbittorrent/qBittorrent
https://github.com/c0re100/qBittorrent-Enhanced-Edition
https://github.com/ngosang/trackerslist
https://github.com/linuxserver/docker-qbittorrent
https://github.com/SuperNG6/Docker-qBittorrent-Enhanced-Edition