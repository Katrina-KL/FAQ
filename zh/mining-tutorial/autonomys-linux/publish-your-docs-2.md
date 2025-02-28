---
cover: ../../.gitbook/assets/aa.png
coverY: 0
layout:
  cover:
    visible: true
    size: full
  title:
    visible: true
  description:
    visible: false
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# 😉 最佳實踐

{% hint style="info" %}
_注：以下名稱、 IP 等都是示例_
{% endhint %}

## 環境介紹

<table><thead><tr><th width="109">服务器</th><th width="116">ip 地址</th><th width="183">配置</th><th>部署組件</th></tr></thead><tbody><tr><td>節點機1</td><td>192.168.1.1</td><td>GPU * 1</td><td><p><code>controller</code> <code>autonomys-node</code> </p><p><code>proof-server</code> <code>nats-server</code></p></td></tr><tr><td>節點機2</td><td>192.168.1.2</td><td>GPU * 1</td><td><p><code>controller</code> <code>autonomys-node</code> </p><p><code>proof-server</code> <code>nats-server</code></p></td></tr><tr><td>節點機3</td><td>192.168.1.3</td><td>GPU * 1</td><td><p><code>controller</code> <code>autonomys-node</code> </p><p><code>proof-server</code> <code>nats-server</code></p></td></tr><tr><td>P 盤機1</td><td>192.168.1.4</td><td>GPU * 4</td><td><p><code>autonomys-plot-server-0</code> </p><p><code>autonomys-plot-server-1</code> </p><p><code>autonomys-plot-server-2</code> </p><p><code>autonomys-plot-server-3</code> </p><p><code>sharded-cache</code> <code>full-piece-cache</code></p></td></tr><tr><td>P 盤機2</td><td>192.168.1.5</td><td>GPU * 4</td><td><p><code>autonomys-plot-server-0</code> </p><p><code>autonomys-plot-server-1</code> </p><p><code>autonomys-plot-server-2</code> </p><p><code>autonomys-plot-server-3</code> </p><p><code>sharded-cache</code> <code>full-piece-cache</code></p></td></tr><tr><td>存儲機1</td><td>192.168.1.6</td><td><p>8T NVMe SSD * 4 </p><p><code>/mnt/nvme0n1</code> </p><p><code>/mnt/nvme0n2</code> </p><p><code>/mnt/nvme1n2</code> </p><p><code>/mnt/nvme1n1</code></p></td><td><code>autonomys-plot-client</code></td></tr><tr><td>存儲機2</td><td>192.168.1.7</td><td><p>8T NVMe SSD * 4 </p><p><code>/mnt/nvme0n1</code> </p><p><code>/mnt/nvme0n2</code> </p><p><code>/mnt/nvme1n1</code> </p><p><code>/mnt/nvme1n2</code></p></td><td><code>autonomys-plot-client</code></td></tr></tbody></table>

## 集群啟動命令

首先啟動 NATS，然後按照以下教學配置 Supervisor 的參數。配置完成後，只需執行以下指令即可啟動所有程序：

```sh
supervisorctl start all
```

## Supervisor 配置

### **節點機配置**

{% hint style="info" %}
單台節點機需要部署4個組件：`controller` `autonomys-node` `proof-server` `nats-server`&#x20;

部署順序： `nats-server` -> `autonomys-node` -> `controller` -> `proof-server`&#x20;
{% endhint %}

<mark style="color:yellow;">**nats-server**</mark>

{% hint style="warning" %}
本軟件需要開啟 nats-server jetstream 功能，啟動 nats-server ，添加 `--jetstream` flag即可啟用

nats-server 的配置請參考[nats 官方文檔](https://docs.nats.io/running-a-nats-service/configuration/clustering) 以及 [autonomys nats 配置文檔](https://docs.autonomys.xyz/farming/advanced-cli/cluster#core-messaging-technology-natsio)。
{% endhint %}

以下是 nats-server 配置示例，供參考：

```sh
server_name=n1-cluster
max_payload = 3MB

jetstream {
   store_dir=/var/nats-data
}


cluster {
  name: c1-cluster
  listen: 0.0.0.0:4248
  routes: [
    nats://192.168.0.1:4248
    nats://192.168.0.2:4248
  ]
}
```

<mark style="color:yellow;">**autonomys-controller**</mark>

{% code overflow="wrap" %}
```ini
# autonomys-controller 配置
# /etc/supervisor/conf.d/autonomys-controller.conf

[program:autonomys-controller]
command=/root/autonomys/autonomys-farmer cluster --nats-server nats://192.168.1.1:4222 --nats-server nats://192.168.1.2:4222 --nats-server nats://192.168.1.2:4222 controller --tmp --node-rpc-url ws://10.30.1.2:9944
autorestart=true
user=root
redirect_stderr=true
stdout_logfile_maxbytes=100MB
stdout_logfile_backups=2
stdout_logfile=/var/log/autonomys-controller.log
```
{% endcode %}

<mark style="color:yellow;">**autonomys-node**</mark>

{% code overflow="wrap" %}
```ini
# autonomys-node 配置
# /etc/supervisor/conf.d/autonomys-node.conf

[program:autonomys-node]
command=/root/autonomys/autonomys-node run --base-path /var/autonomys-node --farmer --rpc-listen-on 0.0.0.0:9944 --chain mainnet --sync full --rpc-methods unsafe --rpc-cors all
autorestart=true
user=root
redirect_stderr=true
stdout_logfile_maxbytes=100MB
stdout_logfile_backups=2
stdout_logfile=/var/log/autonomys-node.log
```
{% endcode %}

<mark style="color:yellow;">**autonomys-proof-server**</mark>

{% code overflow="wrap" %}
```ini
# autonomys-proof-server 配置
# /etc/supervisor/conf.d/autonomys-proof-server.conf

[program:autonomys-proof-server]
command=/root/autonomys/autonomys-farmer cluster --nats-server nats://192.168.1.1:4222 --nats-server nats://192.168.1.2:4222 --nats-server nats://192.168.1.2:4222 proof-server
autorestart=true
user=root
environment=CUDA_VISIBLE_DEVICES=0
redirect_stderr=true
stdout_logfile_maxbytes=500MB
stdout_logfile_backups=2
stdout_logfile=/var/log/autonomys-proof-server.log
```
{% endcode %}

啟動命令參數及環境變量解釋：

* `--nats-server` 參數用於指定 nats 服務器地址
* `CUDA_VISIBLE_DEVICES` 環境變量用於指定 GPU，0 表示 GPU0，1 表示GPU1，以此類推

***

### **P 盤機配置 (以 4 GPU為例)**

{% hint style="info" %}
單台P 盤機需要部署3個組件： `autonomys-plot-server`，`autonomys-sharded-cache`，`autonomys-full-piece-cache`

`autonomys-plot-server` 組件從 `autonomys-sharded-cache` 和 `autonomys-full-piece-cache` 組件獲取 piece 用於 p 盤
{% endhint %}

<mark style="color:yellow;">**autonomys-sharded-cache**</mark>

{% code overflow="wrap" %}
```ini
# sharded-cache 配置
# /etc/supervisor/conf.d/autonomys-sharded-cache.conf

[program:autonomys-sharded-cache]
command=/root/autonomys/autonomys-farmer cluster --nats-server nats://192.168.1.1:4222 --nats-server nats://192.168.1.2:4222 --nats-server nats://192.168.1.2:4222 sharded-cache path=/var/autonomys-sharded-cache
autorestart=true
user=root
redirect_stderr=true
stdout_logfile_maxbytes=100MB
stdout_logfile_backups=2
stdout_logfile=/var/log/autonomys-sharded-cache.log
```
{% endcode %}

啟動命令參數解釋：

* `--nats-server`參數用於指定 nats 服務器地址
* `path=/path/to/autonomys-sharded-cache`參數用於指定 piece 緩存存儲路徑

<mark style="color:yellow;">**autonomys-full-piece**</mark>

{% code overflow="wrap" %}
```ini
# autonomys-full-piece 配置
# /etc/supervisor/conf.d/autonomys-full-piece.conf

[program:autonomys-full-piece]
command=/root/autonomys/autonomys-farmer cluster --nats-server nats://192.168.1.1:4222 --nats-server nats://192.168.1.2:4222 --nats-server nats://192.168.1.2:4222 full-piece-sharded-cache --tmp path=/var/autonomys-full-piece
autorestart=true
user=root
redirect_stderr=true
stdout_logfile_maxbytes=100MB
stdout_logfile_backups=2
stdout_logfile=/var/log/autonomys-full-piece.log
```
{% endcode %}

啟動命令參數解釋：

* `--nats-server` 參數用於指定 nats 服務器地址
* `path=/path/to/autonomys-full-piece` 參數用於指定 full-piece 存儲路徑

<mark style="color:yellow;">**autonomys-plot-server**</mark>

{% code overflow="wrap" %}
```ini
# autonomys-plot-server 配置文件
# /etc/supervisor/conf.d/autonomys-plot-server.conf

[group:autonomys-plot-server]
programs=autonomys-plot-server-0,autonomys-plot-server-1,autonomys-plot-server-2,autonomys-plot-server-3
[program:autonomys-plot-server-0]
command=numactl -C 0-31 -l /root/autonomys/autonomys-farmer cluster --nats-server nats://192.168.1.1:4222 --nats-server nats://192.168.1.2:4222 --nats-server nats://192.168.1.2:4222 plot-server --priority-cache --listen-port 9966 /var/plot-server/base-path-0
autorestart=true
user=root
environment=CUDA_VISIBLE_DEVICES=0
redirect_stderr=true
stdout_logfile_maxbytes=100MB
stdout_logfile_backups=2
stdout_logfile=/var/log/autonomys-plotter-0.log

[program:autonomys-plot-server-1]
command=numactl -C 96-127 -l /root/autonomys/autonomys-farmer cluster --nats-server nats://192.168.1.1:4222 --nats-server nats://192.168.1.2:4222 --nats-server nats://192.168.1.2:4222 plot-server --priority-cache --listen-port 9967 /var/plot-server/base-path-1
autorestart=true
user=root
environment=CUDA_VISIBLE_DEVICES=1
redirect_stderr=true
stdout_logfile_maxbytes=100MB
stdout_logfile_backups=2
stdout_logfile=/var/log/autonomys-plotter-1.log

[program:autonomys-plot-server-2]
command=numactl -C 96-127 -l /root/autonomys/autonomys-farmer cluster --nats-server nats://192.168.1.1:4222 --nats-server nats://192.168.1.2:4222 --nats-server nats://192.168.1.2:4222 plot-server --priority-cache --listen-port 9968 /var/plot-server/base-path-2
autorestart=true
user=root
environment=CUDA_VISIBLE_DEVICES=2
redirect_stderr=true
stdout_logfile_maxbytes=100MB
stdout_logfile_backups=2
stdout_logfile=/var/log/autonomys-plotter-2.log

[program:autonomys-plot-server-3]
command=numactl -C 144-175 -l /root/autonomys/autonomys-farmer cluster --nats-server nats://192.168.1.1:4222 --nats-server nats://192.168.1.2:4222 --nats-server nats://192.168.1.2:4222 plot-server --priority-cache --listen-port 9969 /var/plot-server/base-path-3
autorestart=true
user=root
environment=CUDA_VISIBLE_DEVICES=3
redirect_stderr=true
stdout_logfile_maxbytes=100MB
stdout_logfile_backups=2
stdout_logfile=/var/log/autonomys-plotter-3.log
```
{% endcode %}

啟動命令參數及環境變量解釋：

* `--nats-server` 參數用於指定 nats 服務器地址
* `CUDA_VISIBLE_DEVICES` 環境變量用於指定 GPU，0 表示 GPU0，1 表示GPU1，以此類推
* `GPU_CONCURRENCY` 增大此值會提高顯存使用量，在使用不同型號的 GPU 時，可以考慮適當調整該變量

{% hint style="warning" %}
需要注意的是， 使用 numactl 工具綁定 CPU 核心時，需考慮 GPU 的 numa 親和性，以達到最佳性能。
{% endhint %}

使用 `nvidia-smi topo -m` 命令可以查看 GPU numa 親和性

```sh
# nvidia-smi topo -m
        GPU0    GPU1    NIC0    NIC1    CPU Affinity    NUMA Affinity   GPU NUMA ID
GPU0     X      SYS     NODE    NODE    0-47,96-143     0               N/A
GPU1     X      SYS     NODE    NODE    0-47,96-143     0               N/A
GPU2    SYS      X      SYS     SYS     48-95,144-191   1               N/A
GPU3    SYS      X      SYS     SYS     48-95,144-191   1               N/A
NIC0    NODE    SYS      X      PIX
NIC1    NODE    SYS     PIX      X

Legend:

  X    = Self
  SYS  = Connection traversing PCIe as well as the SMP interconnect between NUMA nodes (e.g., QPI/UPI)
  NODE = Connection traversing PCIe as well as the interconnect between PCIe Host Bridges within a NUMA node
  PHB  = Connection traversing PCIe as well as a PCIe Host Bridge (typically the CPU)
  PXB  = Connection traversing multiple PCIe bridges (without traversing the PCIe Host Bridge)
  PIX  = Connection traversing at most a single PCIe bridge
  NV#  = Connection traversing a bonded set of # NVLinks

NIC Legend:

  NIC0: mlx5_0
  NIC1: mlx5_1
```

***

### **存儲機配置(以 4 盤為例)**

<mark style="color:yellow;">**autonomys-plot-client**</mark>

{% code overflow="wrap" %}
```ini
# autonomys-plot-client 配置
# /etc/supervisor/conf.d/autonomys-plot-client.conf

[program:autonomys-plot-client]
command=/root/autonomys/autonomys-farmer cluster --nats-server nats://192.168.1.1:4222 --nats-server nats://192.168.1.2:4222 --nats-server nats://192.168.1.2:4222 plot-client --reward-address stBR..S8V  path=/mnt/nvme0n1/,sectors=8000 path=/mnt/nvme0n2/,sectors=8000 path=/mnt/nvme1n0/,sectors=8000 path=/mnt/nvme1n1/,sectors=8000
autorestart=true
user=root
redirect_stderr=true
stdout_logfile_maxbytes=100MB
stdout_logfile_backups=2
stdout_logfile=/var/log/autonomys-plot-client.log
```
{% endcode %}

啟動命令參數解釋：

* `--nats-server` 參數用於指定 nats 服務器地址
* `path=/path/to/plot-dir,sectors=8000` 參數用於指定 plot 的文件路徑以及 plot 的扇區數量





[**返回Oula**](https://oula.network/zh/login)
