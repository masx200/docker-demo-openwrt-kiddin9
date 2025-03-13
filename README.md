# docker-demo-openwrt-kiddin9

#### 介绍

docker-demo-openwrt-kiddin9

#### 软件架构

软件架构说明

#### 安装教程

下载镜像,运行命令

```bash
sh import.sh
```

启动容器,运行命令

```bash
sh start.sh
```

关闭容器,运行命令

```bash
sh stop.sh
```

#### 使用说明

### 修改 ip 地址和网关

修改配置文件`/etc/config/network` 中的网络范围和网络地址

```text
config interface 'lan'
	option device 'br-lan'
	option proto 'static'
    list ipaddr '172.20.254.2/24'
    option gateway '172.20.254.1'
	list ip6addr 'fc00:1111:1111:1111::2/64'
	option ip6gw 'fc00:1111:1111:1111::1'
```

修改配置文件`kiddin9_openwrt.yml` 中的网络范围和网络地址

```yml
networks:
  app_net:
    ipv6_address: fc00:1111:1111:1111::2
    ipv4_address: 172.20.254.2
```

```yml
ipam:
  config:
    # IPv4子网配置（可自定义）
    - subnet: 172.20.254.0/24
    # IPv6子网配置（使用私有地址段）[[6]]
    - subnet: fc00:1111:1111:1111::/64
```

### 修改默认用户的密码

修改默认用户的密码的哈希值,然后写入到`/etc/shadow` 文件中

```bash
openssl passwd -6 "你的密码"
```

输出示例：`$6$随机盐值$加密后的哈希值`，其中 `$6$` 表示 SHA-512 算法 。

```text
root:$6$随机盐值$加密后的哈希值:1970:0:99999:7:::
```
