## 特点
* 在任何无线信道上创建热点.
* 可以选择以下加密协议: WPA, WPA2, WPA/WPA2, Open (无加密).
* 隐藏你的 SSID.
* 禁止客户端之间的通信 (客户端 隔离).
* 支持IEEE 802.11n & 802.11ac 
* 网络共享方式: NATed 或者 Bridged 或者 无 (无联网共享).
* 选择 AP w网关 IP (仅支持 'NATed' 和 '无网络共享').
* 您可以使用和获得网络连接相同的接口创建AP.
* 你可以通过管道或者参数传递SSID和密码 (##案例).


## 依赖
### g概括
* bash (运行脚本)
* util-linux 
* procps or procps-ng
* hostapd
* iproute2
* iw
* iwconfig (如果'iw'无法识别你的适配器，你只需要这个)
* haveged (k可选的)

### 'NATed' 或者 'None' 网络共享方式
* dnsmasq
* iptables


## 安装
### t通用
    git clone https://github.com/oblique/create_ap
    cd create_ap
    make install

### ArchLinux
    pacman -S create_ap

### Gentoo
    emerge layman
    layman -f -a jorgicio
    emerge net-wireless/create_ap

## 案例
### 无密码 (开放网络):
    create_ap wlan0 eth0 MyAccessPoint

### WPA + WPA2 密码:
    create_ap wlan0 eth0 MyAccessPoint MyPassPhrase

### 无网络共享的AP:
    create_ap -n wlan0 MyAccessPoint MyPassPhrase

### 桥接网络共享:
    create_ap -m bridge wlan0 eth0 MyAccessPoint MyPassPhrase

### 桥接网络共享 (预配置的桥接接口):
    create_ap -m bridge wlan0 br0 MyAccessPoint MyPassPhrase

### 从相同的 WiFi 接口共享网络:
    create_ap wlan0 wlan0 MyAccessPoint MyPassPhrase

### 选择其他WiFi适配器驱动程序
    create_ap --driver rtl871xdrv wlan0 eth0 MyAccessPoint MyPassPhrase

### 使用管道无密码 (开放网络) :
    echo -e "MyAccessPoint" | create_ap wlan0 eth0

### 使用 WPA + WPA2 管道密码 :
    echo -e "MyAccessPoint\nMyPassPhrase" | create_ap wlan0 eth0

### 开启 IEEE 802.11n
    create_ap --ieee80211n --ht_capab '[HT40+]' wlan0 eth0 MyAccessPoint MyPassPhrase

### 客户端 隔离:
    create_ap --isolate-clients wlan0 eth0 MyAccessPoint MyPassPhrase

## 系统服务
使用systemd [systemd](https://wiki.archlinux.org/index.php/systemd#Basic_systemctl_usage) 服务
### 立即启动服务:
    systemctl start create_ap

### 开机启动:
    systemctl enable create_ap


## License
FreeBSD
