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

# 🤖 Quai - HiveOS

請詳細閱讀挖礦教程，並按照步驟完成礦機接入礦池的操作。

{% hint style="info" %}
請隨時關注[**OULA官方網站**](https://oula.network/zh)公告，並更新使用最新版本的軟體客戶端，以獲得更優質的技術服務和更高的 Token 產出。
{% endhint %}



### 環境準備

*   下載並安裝最新版本的[**HiveOS鏡像**](https://hiveon.com/zh/install/)

    * [ ] Hive OS镜像版本: <mark style="color:yellow;">HiveOS-0.6-227-stable</mark>
    * [ ] 基礎系統: <mark style="color:yellow;">Ubuntu 20.04.6 LTS</mark>
    * [ ] 英偉達驅動: <mark style="color:yellow;">v535.171.04</mark>



    <figure><img src="../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

{% hint style="danger" %}
**注意：**&#x8ACB;勿使用固件在線升級功能，需重新安裝新固件並確保系統版本為 Ubuntu 20.04。
{% endhint %}

{% hint style="info" %}
如果您在設置或使用HiveOS的過程中遇到任何問題，或者有其他配置相關的疑問，我們建議您參考HiveOS的[官方指南](https://hiveon.com/knowledge-base/guides/)來獲取詳細的說明和幫助。官方指南涵蓋了從初學者到高階用戶的多種解決方案，幫助您更好地管理您的挖礦環境。📘
{% endhint %}

### 帳號設立

* 須通過完成 [**OULA帳號註冊**](https://oula.network/zh/register)，在用戶面板→礦池市場→[**子賬戶管理**](https://oula.network/zh/pool/manager?tab=subAccount)模組下，使用 Aleo 對應的預設或創建新的子賬戶名作為錢包地址。

{% hint style="warning" %}
子賬戶和礦工名稱可自訂義，需滿足全域唯一性！&#x20;

建議使用2-15個小寫字母、數字或其組合，且不能以數字開頭。
{% endhint %}

### &#x20;錢包創建

* 在「<mark style="color:blue;">**錢包**</mark>」標簽頁下點擊「<mark style="color:blue;">**添加錢包**</mark>」按鈕

<figure><img src="../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

*   設置對應參數

    * 數字貨幣 `QUAI`
    * 地址 [`Oula 默認或新建的子帳戶名`](https://oula.network/zh/pool/manager?tab=subAccount)&#x20;
    * 名稱 `oula-quai-miner`&#x20;



    <figure><img src="../.gitbook/assets/image (17).png" alt=""><figcaption></figcaption></figure>
* 點擊「<mark style="color:blue;">**創建**</mark>」按鈕

### 飛行表創建

* 在「<mark style="color:blue;">**飛行表**</mark>」標簽頁下點擊「<mark style="color:blue;">**添加飛行表**</mark>」按鈕

<figure><img src="../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

*   設置對應參數

    * 數字貨幣 `QUAI`
    * 錢包 `oula-quai-miner`
    * 礦池 `挖礦軟件配置`
    * 挖礦軟件 `Custom`
    * 名稱 `Oula`

    <figure><img src="../.gitbook/assets/image (18).png" alt=""><figcaption></figcaption></figure>
*   點擊「<mark style="color:blue;">**設定挖礦軟件配置**</mark>」，輸入以下對應參數，點擊「應用更改」保存配置信息

    **挖礦軟體名稱**: `oula-quai-miner`

    **安裝鏈接**: [`https://oula-pool.oss-ap-southeast-1.aliyuncs.com/quai/Hiveos/oula-quai-miner-vx.y.z.tar.gz`](https://oula-pool.oss-ap-southeast-1.aliyuncs.com/quai/Hiveos/oula-quai-miner-vx.y.z.tar.gz)`（根據`[`最新版本號`](https://github.com/oula-network/quai/releases)`更新鏈接地址，例如v1.0.0）`

    **加密算法**: `progpow-quai`

    **錢包與礦機模板**: `%WAL%.%WORKER_NAME%`

    **礦池地址**: `stratum://quai.oula.network:3333`

    <figure><img src="../.gitbook/assets/image (19).png" alt=""><figcaption></figcaption></figure>

點擊「<mark style="color:blue;">**創建飛行表**</mark>」按鈕，飛行表添加完成

* 將添加的礦機應用于已創建的飛行表

{% hint style="success" %}
若在<mark style="color:red;">`miner.log`</mark>中見到以下相關訊息，則表示程序已成功啟動。
{% endhint %}

<figure><img src="../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

### 礦機監控及產出查看

設備穩定運行並提交數據後，在用戶面板→礦池市場→[**礦工管理**](http://192.168.1.51/zh/pool/manager?tab=miner)和[**產出/支付**](http://192.168.1.51/zh/pool/manager?tab=output)模組下，切換對應的子賬戶即可檢視礦工運行狀態、產出詳情及支付詳情。





[**返回Oula**](https://oula.network/zh/login)
