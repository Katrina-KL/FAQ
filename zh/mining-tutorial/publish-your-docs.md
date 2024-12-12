---
hidden: true
cover: ../.gitbook/assets/aleo.png
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
    visible: false
  pagination:
    visible: true
---

# 🤖 Aleo挖礦教程 - Solo

{% embed url="https://oula.network/zh" %}

> &#x20;❕ [ALEO](https://www.aleo.org/)是一個融合PoW和PoS共識機制的區塊鏈項目，旨在提供高度隱私的智能合約功能。其利用先進的Synthesis Puzzle技術來確保交易的隱私和安全性。ALEO專注於構建去中心化應用程序，提供高效且安全的隱私保護方案。



### 環境準備

* **操作系統：**&#x55;buntu 20.04、Ubuntu 22.04 及 HiveOS
* **軟體客戶端：**[Oula-Aleo](https://github.com/oula-network/aleo/releases/tag/v1.6-testnet-beta)/ HiveOS。

{% hint style="info" %}
請隨時關注[OULA官方網站](https://oula.network/zh)公告，並更新使用最新版本的軟體客戶端，以獲得更優質的技術服務和更高的 Token 產出。
{% endhint %}

### 程序運行

#### **Aleo Solo Prover**

* 在Ubuntu系統中，将[**aleo-solo-prover**](https://github.com/oula-network/aleo/releases/download/v1.6-testnet-beta/aleo-solo-prover)和[**license**](https://github.com/oula-network/aleo/releases/download/v1.6-testnet-beta/license)文件下載至同一目錄下
* 替換(--address) 和  (--worker-name) 的參數，並執行程序啟動命令

{% code overflow="wrap" %}
```bash
nohup ./aleo-solo-prover --proxy wss://aleo.oula.network:5555 --address <YOUR_ALEO_ADDRESS> --worker-name <WORKER_NAME> > prover.log 2>&1 &
```
{% endcode %}

* 執行查看日誌命令

```bash
tail -f prover.log
```

{% hint style="success" %}
若在<mark style="color:red;">`prover.log`</mark>中見到相關成功訊息，則表示程序已成功啟動。
{% endhint %}

<figure><img src="../.gitbook/assets/image (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

{% hint style="warning" %}
如果您不需要輸出日誌內容，可以將啟動命令中的“&> prover.log &”替換為“> /dev/null 2>&1 &”。
{% endhint %}

* 執行程式停止命令

```bash
killall aleo-pool-prover
# 強制執行
```

#### **HiveOS**

請參考上述下載鏈接中的HiveOS操作指南。



### 礦機監控及產出查看

設備穩定運行並提交數據後，可以通過以下鏈接檢視礦工運行狀態和產出詳情。



{% embed url="https://oula.network/zh/solo" %}



[**返回Oula**](https://oula.network/zh/login)
