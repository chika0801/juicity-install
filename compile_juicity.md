准备环境

```
curl -sLo go.tar.gz https://go.dev/dl/$(curl -sL https://golang.org/VERSION?m=text|head -1).linux-amd64.tar.gz
rm -rf /usr/local/go
tar -C /usr/local/ -xzf go.tar.gz
rm go.tar.gz
echo -e "export PATH=$PATH:/usr/local/go/bin" > /etc/profile.d/go.sh
source /etc/profile.d/go.sh
go version
```

```
apt install -y git make
```

下载代码

```
git clone https://github.com/juicity/juicity
```

更新代码

```
cd juicity
git pull
cd ..
```

编译命令

**linux-amd64 服务端**

```
cd juicity
export CGO_ENABLED=0 GOOS=linux GOARCH=amd64 GOAMD64=v2
make juicity-server
cd ..
```

**windows-amd64 客户端**

```
cd juicity
export CGO_ENABLED=0 GOOS=windows GOARCH=amd64 GOAMD64=v3
make juicity-client
cd ..
```

[About GOAMD64](https://github.com/golang/go/wiki/MinimumRequirements#amd64)

复制文件

**linux-amd64**

```
cp -f juicity/juicity-server /usr/local/bin/juicity
chmod +x /usr/local/bin/juicity
```

**windows-amd64**

```
cp -f juicity/juicity-client ./juicity.exe
```
