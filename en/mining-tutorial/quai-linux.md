---
cover: ../.gitbook/assets/Quai.png
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

# 🤖 Quai - Linux

{% embed url="https://oula.network/en/" %}

{% hint style="info" %}
Please stay updated with [<mark style="color:blue;">**OULA's official website**</mark>](https://oula.network/en) announcements and use the latest version of the software client for optimal technical service and higher Token output.
{% endhint %}



### **Environment Setup**

* Operating Systems: <mark style="color:yellow;">Ubuntu 22.04</mark>
* NVIDIA Driver Version: <mark style="color:yellow;">535 or higher</mark>
* Software Clients: [oula-gpu-miner](https://github.com/oula-network/quai/releases)

### **Account Setup**

* Register for an [**Oula Account**](https://oula.network/en/register) and setup the [**Sub-Account**](https://oula.network/en/pool/manager?tab=subAccount).
* Use the default Sub-Account name or the created one to start the mining software.&#x20;

{% hint style="info" %}
After running the software client, daily output will be automatically accumulated to the corresponding sub-account. Once the balance reaches the minimum payout threshold, the platform will automatically pay out to the bound withdrawal address daily.
{% endhint %}

### **Program Execution**

#### **Oula Pool Prover**

* Download the [<mark style="color:red;">**`oula-gpu-miner`**</mark>](https://github.com/oula-network/quai/releases) on Ubuntu systems.
* Grant permission with the command:

```sh
chmod +x oula-gpu-miner
```

* Set execution permission with the command:

{% code overflow="wrap" %}
```bash
nohup ./oula-gpu-miner -U -P stratums://quai.oula.network:3333 --account=SubAccount --worker-name=Worker_Name > miner.log 2>&1 &
```
{% endcode %}

* [ ] Replace the pool address (`-P`) with the "Mining Address" provided on the [**Overview**](https://oula.network/en/pool/manager) page.
* [ ] Replace the account (`--account`) with the "Account Name" created on the [**Sub-Account**](https://oula.network/en/pool/manager?tab=subAccount) page.
* [ ] Replace the worker name (`--worker-name`) .

{% hint style="warning" %}
**Sub-account and miner names can be customized but must be globally unique!**&#x20;

**It is recommended to use 2-15 lowercase letters, numbers, or a combination, and the name cannot start with a number.**
{% endhint %}

* Check logs with the command:

```bash
tail -f miner.log
```

{% hint style="success" %}
If you see `ProgPow kernel` relevant messages in <mark style="color:red;">`miner.log`</mark>, the program has started successfully.
{% endhint %}

{% hint style="warning" %}
**If you do not need to output log content, you can replace '&> miner.log &' in the startup command with '> /dev/null 2>&1 &'.**
{% endhint %}

* To stop the program, use:

```bash
killall oula-gpu-miner
# Force stop
```

### **Monitoring and Yield Viewing**

Once your mining machine is running stably and submitting solutions, you can check the worker's operational status, output details and payment details under [**Worker**](https://oula.network/en/pool/manager?tab=miner) and [**Output / Payout**](https://oula.network/en/pool/manager?tab=output) by switching to the corresponding sub-account.





[**Back to Oula**](https://oula.network/en/login)
