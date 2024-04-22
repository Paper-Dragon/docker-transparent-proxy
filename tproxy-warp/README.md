
# Tproxy Warp

这个代码实现通过warp网络给一个容器分配一个公网ip，并且连接到国际网络。

透明代理项目源码地址 [Warp Tproxy For Docker](https://github.com/Paper-Dragon/warp-tproxy-for-docker) 。

Docker Hub地址 [jockerdragon/warp-tproxy](https://hub.docker.com/r/jockerdragon/warp-tproxy)。

免费密钥获取： [geekery.cn](https://www.geekery.cn/free-service/cloudflare-warp.html)。


适用于 `free` 或 `warp+` 和 `Zero Trust` 网络，因为不可明说的原因，大陆用户建议使用 `Zero Trust` 。

- [tproxy warp](#tproxy-warp)
    - [功能](#功能)
    - [如何使用？](#如何使用)
    - [启动模式](#启动模式)
        - [Zero Turst模式](#zero-turst模式)
            - [Zero-Turst模式启动日志](#zero-turst模式启动日志)
        - [Warp Plus模式](#zarp-plus模式)
            - [Warp-Plus模式启动日志](#warp-plus模式启动日志)
        - [Free 模式](#free-模式)
    - [声明](#声明)
    - [致谢](#致谢)
    - [协议](#致谢)

## 功能
它可以让单个Docker容器内部具有透明代理，且拥有一个与本机公网ip不同的公网ip。

## 如何使用？
根据启动模式在 `docker-compose.yaml` 文件里设置变量。

启动命令
```bash
docker compose up -d
```

测试
```bash
docker exec -it warp-transparent-proxy-warp-tproxy-1 bash
apt update && apt install curl -y
curl ifconfig.icu
curl cip.cc
```


## 启动模式
详细介绍看 [Warp Tproxy For Docker](https://github.com/Paper-Dragon/warp-tproxy-for-docker/blob/container-tproxy/README.zh_CN.md)
### Zero Turst模式
设置环境变量

```bash
# 使用zero trust方式
- WARP_ORG_ID=paperdragxx
- WARP_AUTH_CLIENT_ID=c4d31ea084c2940e17b714de890xxxxx.access
- WARP_AUTH_CLIENT_SECRET=7120f34bd52ce19a90534ca804cdaeaa72bb03e9c5da10ee0279fdc7bcdxxxxx
- WARP_UNIQUE_CLIENT_ID=aa7b5738-ff99-11ee-b4c1-72e2181b199b  # 可选
```
#### Zero-Turst模式启动日志

```text
[+] Starting dbus...
[+] warp's TOS already accepted!
[+] Starting warp-svc...
[!] warp-svc in debug mode
/entrypoint.sh: line 85: docker: command not found
[!]  show warp svc log
nohup: appending output to 'nohup.out'
[!] wait for warp-svc to start in debug mode
[+] wait warp-svc show status   ...
Status update: Connecting
[+] Set warp license to Y9U8f53G-0C8Z9d1j-C37hg8c9 ... Success
[+] New registration generated ... Error: Old registration is still around. Try running: "warp-cli registration delete"
[+] Set warp mode to warp ... Success
[+] Turn ON warp ... Success
[+] Waiting for warp to connect...
[+] warp connected!
[+] All services started!
---
warp-svc config: /var/lib/cloudflare-warp/conf.json
---
[+] warp status: Status update: Connected

[+] You can check it with warp local tproxy in container:
    E.g.:
      curl https://cloudflare.com/cdn-cgi/trace (inside container)
```

### Warp Plus模式
必须在宿主机内安装wireguard  `apt update && apt install wireguard -y`
```bash
# 使用key方式
- WARP_LICENSE=Y9U8f53G-0C8Z9d1j-C37hg8c9
```


#### Warp-Plus模式启动日志
```text
 *  正在执行任务: docker compose --file '/root/docker-transparent-proxy/tproxy-warp/docker-compose.yaml' --project-name 'warp-transparent-proxy' logs --follow --tail '1000' 

WARN[0000] /root/docker-transparent-proxy/tproxy-warp/docker-compose.yaml: `version` is obsolete 
warp-tproxy-1  | [+] Starting dbus...
warp-tproxy-1  | [+] Bypassing warp's TOS ...
warp-tproxy-1  | [+] Starting warp-svc...
warp-tproxy-1  | [+] Waiting for warp to connect...
warp-tproxy-1  | Status update: Unable to connect. Reason: Registration Missing
warp-tproxy-1  | [+] New registration generated ... Success
warp-tproxy-1  | [+] Set warp mode to warp ... Success
warp-tproxy-1  | [+] Turn ON warp ... Success
warp-tproxy-1  | [+] Waiting for warp to connect...
[+] warp connected!
warp-tproxy-1  | [+] All services started!
warp-tproxy-1  | ---
warp-tproxy-1  | warp-svc config: /var/lib/cloudflare-warp/conf.json
warp-tproxy-1  | ---
warp-tproxy-1  | [+] warp status: Status update: Connected
warp-tproxy-1  | 
warp-tproxy-1  | [+] You can check it with warp local tproxy in container:
warp-tproxy-1  |     E.g.:
warp-tproxy-1  |       curl https://cloudflare.com/cdn-cgi/trace (inside container)

```
### Free 模式
在大陆地区极低概率连接成功，不建议使用。

## 声明
本项目仅供学习，非法使用必追究法律责任，下载后请于24小时内删除。

自行下载所造成任何后果与作者无关!!

## 致谢
- [Warp Tproxy For Docker](https://github.com/Paper-Dragon/warp-tproxy-for-docker/blob/container-tproxy/README.zh_CN.md)
- [Cloudflare](cloudflare.com)

## 协议
MIT