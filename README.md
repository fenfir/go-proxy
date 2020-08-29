# go-proxy
Chaining Proxies with GoProxy


## description

We use username:password of a basicauth request to denote the proxy to be chained.

`curl -x "http://10.10.10.10:10432@127.0.0.1:8001" "http://httpbin.org/ip"`

Where 10.10.10.10:1043 is the remote proxy you want to chain connect.

> **Remember**: You want to point this at another proxy.

## Setup

```
export GOPATH=$HOME/go
go get "github.com/elazarl/goproxy"
go get "github.com/prometheus/client_golang/prometheus"
```

### Build & Run Go-Proxy
> Proxy Port 8001
> Metrics Port 8080
- `go build go-proxy.go`
- `./go-proxy.go`

### Test Connection
- `curl -x "http://127.0.0.1:8002@127.0.0.1:8001" "http://127.0.0.1:8080/metrics"`


### Load Test
- `hey -n 10000 -c 500  -x "http://127.0.0.1:8002@127.0.0.1:8001" "http://127.0.0.1:8080/metrics"`


### Notes
- We use localhost to skip the network overhead.
- `ulimit -n 65535` to avoid 
- Setting Ulimits on MacOS is frustrating
