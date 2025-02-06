---
hidden: true
cover: ../.gitbook/assets/aleo.jpg
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

# 🤖 Aleo - Solo

{% embed url="https://oula.network/en" %}

> &#x20;❕ [ALEO](https://www.aleo.org/) is a blockchain project that integrates Proof of Work (PoW) and Proof of Stake (PoS) consensus mechanisms to offer highly private smart contract capabilities. It utilizes advanced Synthesis Puzzle technology to ensure transaction privacy and security. Aleo focuses on developing decentralized applications and provides efficient and secure privacy protection solutions.

### **Environment Setup**

* **Operating Systems**: Ubuntu 20.04, Ubuntu 22.04, and HiveOS
* **Software Clients**: [**Oula-Aleo**](https://github.com/oula-network/aleo/releases/tag/v1.6-testnet-beta) / HiveOS

{% hint style="info" %}
Please stay updated with [<mark style="color:blue;">**OULA's official website**</mark>](https://oula.network/en) announcements and use the latest version of the software client for optimal technical service and higher Token output.
{% endhint %}

### **Program Execution**

#### **Aleo Solo Prover**

* Download [**aleo-solo-prover**](https://github.com/oula-network/aleo/releases/download/v1.6-testnet-beta/aleo-solo-prover) and [**license**](https://github.com/oula-network/aleo/releases/download/v1.6-testnet-beta/license) in the same directory.
* Replace (--address) &  (--worker-name) and set execution permissions with the command:

{% code overflow="wrap" %}
```sh
nohup ./aleo-solo-prover --proxy wss://aleo.oula.network:5555 --address <YOUR_ALEO_ADDRESS> --worker-name <WORKER_NAME> > prover.log 2>&1 &shell
```
{% endcode %}

* Check logs with the command:

```bash
tail -f prover.log
```

{% hint style="success" %}
If you see relevant success messages in <mark style="color:red;">`prover.log`</mark>, the program has started successfully.
{% endhint %}

<figure><img src="../.gitbook/assets/image (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

{% hint style="warning" %}
**If you do not need to output log content, you can replace '&> prover.log &' in the startup command with '> /dev/null 2>&1 &'.**
{% endhint %}

* To stop the program, use:

```bash
killall aleo-solo-prover
# Force stop
```

#### **HiveOS**

Please refer to the HiveOS operation guide in the above download link.



### **Monitoring and Output Viewing**

Once your mining machine is running stably and submitting solutions, you can check the miner's operational status and output details via below link.

{% embed url="https://oula.network/en/solo" %}





[**Back to Oula**](https://oula.network/zh/login)
