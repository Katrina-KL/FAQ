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

# Introduction

Autonomys-farmer consists of [**the following components**](https://github.com/oula-network/autonomys/releases):

* **autonomys-controller**: Responsible for proxying node RPC, used to manage cluster components.
* **sharded-cache**: Piece sharded cache.
* **full-piece-sharded-cache**: Full node of piece sharded cache.
* **proof-server**: GPU-based block generation, used for computing proofs.
* **plot-server**: Plotting service, responsible for encoding data.
* **plot-client**: Farming component, used for scanning disks and submitting solutions.

### Architecture

Currently, all cluster management is based on **NATS**, but the actual data transmission for the cache is done through **TCP** for peer-to-peer (P2P) communication.

<figure><img src="../../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>



