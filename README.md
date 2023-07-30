# [juicity](https://github.com/juicity/juicity) 安装指南

## 服务端

### 安装

1. 下载程序（**linux-amd64**）

```
curl -Lo /root/juicity.zip https://github.com/juicity/juicity/releases/latest/download/juicity-linux-x86_64.zip && unzip -q /root/juicity.zip -d /root/juicity && chmod +x /root/juicity/juicity-server && mv -f /root/juicity/juicity-server /usr/local/bin/juicity && rm -rf /root/juicity.zip /root/juicity
```

2. 下载配置

```
curl -Lo /root/juicity_config.json https://raw.githubusercontent.com/chika0801/juicity-install/main/config_server.json
```

3. 下载systemctl配置

```
curl -Lo /etc/systemd/system/juicity.service https://raw.githubusercontent.com/chika0801/juicity-install/main/juicity.service && systemctl daemon-reload
```

4. 上传证书和私钥

- 将证书文件改名为 **fullchain.cer**，将私钥文件改名为 **private.key**，将它们上传到 **/root** 目录

5. 启动程序

```
systemctl enable --now juicity
```

| 项目 | |
| :--- | :--- |
| 程序 | **/usr/local/bin/juicity** |
| 配置 | **/root/juicity_config.json** |
| 重启 | `systemctl restart juicity` |
| 状态 | `systemctl status juicity` |
| 查看日志 | `journalctl -u juicity --output cat -e` |
| 实时日志 | `journalctl -u juicity --output cat -f` |

### 卸载

```
systemctl disable --now juicity
```

```
rm -f /usr/local/bin/juicity /root/juicity_config.json /etc/systemd/system/juicity.service
```

## 客户端

### Windows 客户端使用方法：

1. 新建一个批处理文件，内容为 `start /min juicity.exe run -c config.json`。
2. 参考[客户端配置](https://github.com/chika0801/juicity-install/blob/main/config_client.json)示例，修改chika.example.com为证书中包含的域名，修改10.0.0.1为VPS的IP，将文件名改为 **config.json**，与 **juicity.exe**，批处理文件放在同一文件夹里。
3. 运行批处理文件。

### 由 sing-box 提供 Tun 模式（透明代理）

1. sing-box：参考 [sing-box Windows 客户端使用方法](https://github.com/chika0801/sing-box-examples/blob/main/Tun/README.md)，将 [sing-box Windows 客户端配置](https://github.com/chika0801/sing-box-examples/blob/main/Tun/config_client_windows.json) 进行如下修改。

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
