准备环境

```
curl -sLo go.tar.gz https://go.dev/dl/go1.20.7.linux-amd64.tar.gz
rm -rf /usr/local/go
tar -C /usr/local -xzf go.tar.gz
rm go.tar.gz
echo -e "export PATH=$PATH:/usr/local/go/bin" > /etc/profile.d/go.sh
source /etc/profile.d/go.sh
go version
```

```
apt install -y git make
```

首次编译

```
git clone https://github.com/juicity/juicity
cd juicity
```

再次编译

```
cd juicity
git pull
```

编译命令

**linux-amd64 服务端**

```
make CGO_ENABLED=0 GOOS=linux GOARCH=amd64 GOAMD64=v2 juicity-server
```

**windows-amd64 客户端**

```
make CGO_ENABLED=0 GOOS=windows GOARCH=amd64 GOAMD64=v3 juicity-client
```

[About GOAMD64](https://github.com/golang/go/wiki/MinimumRequirements#amd64)

复制文件

**linux-amd64**

```
cp -f /root/juicity/juicity-server /usr/local/bin/juicity && chmod +x /usr/local/bin/juicity
```



**windows-amd64**

```
cp -f /root/juicity/juicity-client /root/juicity.exe
```
