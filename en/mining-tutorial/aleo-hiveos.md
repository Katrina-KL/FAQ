---
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
    visible: true
  pagination:
    visible: true
---

# 🤖 Aleo - HiveOS

{% embed url="https://oula.network/en/" %}

&#x20;❕ [Aleo](https://www.aleo.org/) is a blockchain project that integrates Proof of Work (PoW) and Proof of Stake (PoS) consensus mechanisms to offer highly private smart contract capabilities. It utilizes advanced Synthesis Puzzle technology to ensure transaction privacy and security. Aleo focuses on developing decentralized applications and provides efficient and secure privacy protection solutions.



Please read the mining tutorial carefully and follow the steps to connect the mining machine to the mining pool.

{% hint style="info" %}
Please stay updated with [<mark style="color:blue;">**OULA's official website**</mark>](https://oula.network/en) announcements and use the latest version of the software client for optimal technical service and higher Token output.
{% endhint %}

### **Environment Setup**

*   Download and install the latest version of [HiveOS](https://hiveon.com/install/).&#x20;

    * GPU Image Version: <mark style="color:red;">**HiveOS-0.6-227-stable**</mark>&#x20;
    * Distro Base: <mark style="color:red;">**Ubuntu 20.04.6 LTS**</mark>

    <figure><img src="../.gitbook/assets/image (1) (1).png" alt=""><figcaption></figcaption></figure>

{% hint style="danger" %}
**Note:** Do not use the firmware online upgrade feature. Please reinstall the new firmware and ensure that the system version is Ubuntu 20.04.
{% endhint %}

* Upgrade the GCC and G++ compilers with the command:

<pre class="language-sh"><code class="lang-sh">apt install software-properties-common
<strong>add-apt-repository ppa:ubuntu-toolchain-r/test
</strong>apt update
apt install gcc-11 g++-11
</code></pre>

* Set the priority for GCC and G++ with the command:

```sh
update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-11 10
update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-11 10
```

* upgrade the NVIDIA driver with the command:

```
nvidia-driver-update
```

{% hint style="info" %}
If you encounter any issues during the setup or use of HiveOS, or if you have other configuration-related questions, we recommend checking out the [HiveOS Official Guide](https://hiveon.com/knowledge-base/guides/) for detailed instructions and support. The guide covers solutions for both beginners and advanced users, helping you manage your mining environment more effectively. 📘
{% endhint %}

### **Account Setup**

* Register for an [**Oula Account**](https://oula.network/en/register) and setup the [**Sub-Account**](https://oula.network/en/pool/manager?tab=subAccount).
* Use the default Aleo Sub-Account name or create a new one as the wallet address.&#x20;

{% hint style="warning" %}
**Sub-account and miner names can be customized but must be globally unique!**&#x20;

**It is recommended to use 2-15 lowercase letters, numbers, or a combination, and the name cannot start with a number.**
{% endhint %}

### &#x20;Wallet Creation

* Go to the "<mark style="color:blue;">**Wallet**</mark>" tab and click the "<mark style="color:blue;">**Add Wallet**</mark>" button.

<figure><img src="../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

* Set the corresponding parameters.
  * Coin `ALEO`
  * Address [`Created Oula Sub-Account Name`](https://oula.network/en/pool/manager?tab=subAccount)
  * Name `Oula`

<figure><img src="../.gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure>

* Click the "Create" button.

### Flight Sheet Creation

* Go to the "<mark style="color:blue;">**Flight Sheet**</mark>" tab and click the "<mark style="color:blue;">**Add Flight Sheet**</mark>" button.

<figure><img src="../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

* Set the corresponding parameters.
  * Coin `ALEO`
  * Wallet `Oula`
  * Pool `Configure in miner`
  * Miner `Custom`
  * Name `oulapool`

<figure><img src="../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

* Click the "<mark style="color:blue;">**Setup Miner Config**</mark>" button, enter the following parameters and Click the "<mark style="color:blue;">**Apply Changes**</mark>" button to save the configurations.
  * Miner Name: `oulapool`
  * Installation URL: `https://oula-hiveos.oss-ap-southeast-1.aliyuncs.com/oulapool-vX.X.tar.gz`\
    (Update the link address according to [the latest version number](https://app.gitbook.com/s/yseWjqJcypCcEst0oC22/), e.g., v1.15.)
  * Hash algorithm: `aleo`
  * Wallet and worker template: `%WAL%.%WORKER_NAME%`
  * Pool URL: `wss://aleo.oula.network:6666`

<figure><img src="../.gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>

* Click the "Create Flight Sheet" button to complete the flight sheet setup.
* Apply the added miners to the created flight sheet.

### **Monitoring and Yield Viewing**

Once your mining machine is running stably and submitting solutions, you can check the worker's operational status, output details and payment details under [**Worker**](https://oula.network/en/pool/manager?tab=miner) and [**Output / Payout**](https://oula.network/en/pool/manager?tab=output) by switching to the corresponding sub-account.





[**Back to Oula**](https://oula.network/en/login)
