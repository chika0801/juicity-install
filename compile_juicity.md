```
curl -sLo go.tar.gz https://go.dev/dl/go1.20.6.linux-amd64.tar.gz
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
make CGO_ENABLED=0 juicity-server
make juicity-client
cd ..
```
