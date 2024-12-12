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
    visible: false
  pagination:
    visible: true
---

# ⚡ Power Q\&A

{% embed url="https://oula.network/en/" %}

**Q: How is the Unit of Power defined in Aleo Mining?**

A: In Aleo mining, the units of power include the following:

* **p** stands for Proof
* **c** stands for Commitment
* **h** stands for Hashrate
* **s** stands for Solution

These units are equivalent in measurements per second, i.e., p/s, s/s, c/s, h/s all represent computational power per second.

***

**Q: How long does it usually take to show Aleo mining power?**

A: The mining power typically appears within ten minutes.

***

**Q: Why did my Aleo worker's power decrease suddenly?**

A: Each Epoch has its own difficulty coefficient, hence, it is normal the fluctuation of the worker's power.

***

**Q: Why is the computational power of my newly added Aleo miner very low?**

A: After connecting to the Oula mining pool, you need to wait for about fifteen minutes for the mining machine to stabilize before observing. Due to the fluctuation of Epoch difficulty, the worker power may vary, so it is recommended to extend the observation time.

***

**Q: Why is one of the operating graphics card's power significantly lower than others when starting the miner?**

A: Please check if the graphics card models are consistent, ensure the miner voltage is stable, and check if there are other processes occupying that graphics card.

***

**Q: How to check if the graphics card driver is installed correctly?**

A: Use the <mark style="color:red;">`nvidia-smi`</mark> command. If the operation is successful, it will display the following information. It is able to check the GPU version and running status from the returned results.

<figure><img src="../.gitbook/assets/image (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

***

**Q: What should I do if the system crashes while running mining software?**

A: Crashes can be caused by various reasons such as voltage or hardware issues. If you cannot find the problem after self-inspection, it is recommended to upload or screenshot the system log and contact the administrator in the Oula community for assistance.

***

**Q: Why does the worker show offline while mining Aleo?**

A: If the platform shows the worker as offline but the log is normal and the earnings per Epoch are normal, it could be a network issue causing a temporary inability to push miner data, but it does not affect earnings. To view the logs, please run <mark style="color:red;">`tail -f prover.log`</mark>."\
\




[**Back to Oula**](https://oula.network/en/login)

