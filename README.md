# 在VPS上安装SS Server
## 安装
```javascript
> wget –no-check-certificate -O shadowsocks.sh https://raw.githubusercontent.com/ArtechChu/VPS-INSTALL-SS/master/shadowsocks.sh

> chmod +x shadowsocks.sh

> ./shadowsocks.sh 2>&1 | tee shadowsocks.log
```
## 一些说明：
加密建议：aes-256-cfb

完成时间有点长，完成后会有提示，并显示服务地址

卸载方法：
```javascript
> ./shadowsocks.sh uninstall
```

修改配置：
```javascript
> vi /etc/shadowsocks.json
```

# 安装 BBR
前置条件：
- 需要linux内核4.9以上
- 需要KVM架构的VPS（目前vultr没什么问题）


## 安装
```javascript
> wget --no-check-certificate https://raw.githubusercontent.com/ArtechChu/VPS-INSTALL-SS/master/bbr.sh
> chmod +x bbr.sh
> ./bbr.sh
```
安装完成后，脚本会提示需要重启 VPS，输入 y 并回车后重启。若未提示，直接命令：reboot 进行重启

## 验证
```javascript
uname -r
```
显示的版本号>4.9即可

```javascript
sysctl net.ipv4.tcp_available_congestion_control
```
返回值一般为：*net.ipv4.tcp_available_congestion_control = bbr cubic reno*

```javascript
sysctl net.ipv4.tcp_congestion_control
```
返回值一般为：*net.ipv4.tcp_available_congestion_control = bbr cubic reno*

```javascript
sysctl net.ipv4.tcp_congestion_control
```
返回值一般为： *net.ipv4.tcp_congestion_control = bbr*

```javascript
sysctl net.core.default_qdisc
```
返回值一般为： *net.core.default_qdisc = fq*

```javascript
lsmod | grep bbr
```
返回值一般为： *tcp_bbr*
