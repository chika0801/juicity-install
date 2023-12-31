# [Juicity](https://github.com/juicity/juicity) 安装指南

## 服务端

### 安装

1. 下载程序（**linux-amd64**）或 [编译程序](compile_juicity.md)

```
apt install -y unzip
curl -Lo juicity.zip https://github.com/juicity/juicity/releases/latest/download/juicity-linux-x86_64.zip && unzip -q juicity.zip -d tmp && chmod +x tmp/juicity-server && cp -f tmp/juicity-server /usr/local/bin/ && rm -r juicity.zip tmp
```

2. 下载配置

```
curl -Lo /root/juicity-server_config.json https://raw.githubusercontent.com/chika0801/juicity-install/main/config_server.json
```

3. 下载systemctl配置

```
curl -Lo /etc/systemd/system/juicity-server.service https://raw.githubusercontent.com/chika0801/juicity-install/main/juicity-server.service && systemctl daemon-reload
```

4. 上传证书和私钥

- 将证书文件改名为 **fullchain.cer**，将私钥文件改名为 **private.key**，将它们上传到 **/root** 目录

5. 启动程序

```
systemctl enable --now juicity-server
```

| 项目 | |
| :--- | :--- |
| 程序 | **/usr/local/bin/juicity-server** |
| 配置 | **/root/juicity-server_config.json** |
| 重启 | `systemctl restart juicity-server` |
| 状态 | `systemctl status juicity-server` |
| 查看日志 | `journalctl -u juicity-server -o cat -e` |
| 实时日志 | `journalctl -u juicity-server -o cat -f` |

### 卸载

```
apt remove -y unzip && systemctl disable --now juicity-server && rm -f /usr/local/bin/juicity-server /root/juicity-server_config.json /etc/systemd/system/juicity-server.service
```

## 客户端

### 由 v2rayN 提供 HTTP SOCKS5 代理，由 v2rayN 提供路由规则

1. 下载Windows端程序[juicity-windows-x86_64.zip](https://github.com/juicity/juicity/releases/latest/download/juicity-windows-x86_64.zip)，将juicity-client.exe，复制到v2rayN\bin\juicity文件夹。

2. 下载客户端配置[config_client.json](config_client.json)，修改chika.example.com为证书中包含的域名，修改10.0.0.1为VPS的IP。

3. v2rayN：服务器 ——> 添加自定义配置服务器 ——> 浏览 ——> 选择客户端配置 ——> Core类型 juicity ——> Socks端口 50000

### 由 sing-box 提供 Tun 模式（透明代理），由 sing-box 提供路由规则

1. sing-box：参考[Windows 使用方法](https://github.com/chika0801/sing-box-examples/blob/main/README.md)，将[客户端配置](https://github.com/chika0801/sing-box-examples/blob/main/Tun/config_client_windows.json)进行如下修改。

原内容

```jsonc
        {
            "tag": "proxy",
            // 粘贴你的客户端配置，需要保留 "tag": "proxy",
        },
```

替换为

```jsonc
        {
            "type": "socks",
            "tag": "proxy",
            "server": "127.0.0.1",
            "server_port": 50000
        },
```

检查此处有 **juicity.exe** 或 **juicity-client.exe**

```jsonc
            {
                "process_name": [ // 直连的 Windows 可执行程序
                    "xray.exe",
                    "hysteria.exe",
                    "tuic.exe",
                    "tuic-client.exe",
                    "juicity.exe",
                    "juicity-client.exe"
                ],
                "outbound": "direct"
            },
```

2. v2rayN：服务器 ——> 添加自定义配置服务器 ——> 浏览 ——> 选择客户端配置 ——> Core类型 juicity ——> Socks端口 0。
