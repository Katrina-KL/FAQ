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

請詳細閱讀挖礦教程，並按照步驟完成礦機接入礦池的操作。

### 環境準備

* 操作系統：<mark style="color:yellow;">Ubuntu 22.04 (GCC 11.4)</mark>
* NVIDIA驱动版本：<mark style="color:yellow;">535以上</mark>
* 軟體客戶端：[oula-gpu-miner](https://github.com/oula-network/quai/releases)

{% hint style="info" %}
請隨時關注[**Oula官方網站**](https://oula.network/zh)公告，並更新使用最新版本的軟體客戶端，以獲得更優質的技術服務和更高的 Token 產出。
{% endhint %}

### 帳號設立

* 須通過完成 [**Oula帳號註冊**](https://oula.network/zh/register)，在用戶面板→礦池市場→[**子賬戶管理**](https://oula.network/zh/pool/manager?tab=subAccount)模組下，使用預設或新建立的子賬戶名啟動軟體。
* 運行軟體客戶端後，每日的產出將自動累計至對應的子賬戶中。餘額達到最低起付金額後，平台將每日自動支付至綁定的提現地址。

### 程序運行

#### **Oula GPU Miner**

* 在Ubuntu系統中，下載並解壓縮[<mark style="color:red;">**`oula-gpu-miner`**</mark>](https://github.com/oula-network/quai/releases)
* 設置執行程序的權限命令

```sh
chmod +x oula-gpu-miner
```

* 設置參數對應的文本資訊，執行程序啟動命令

{% code overflow="wrap" %}
```bash
nohup ./oula-gpu-miner -U -P stratums://quai.oula.network:3333 --account=SubAccount --worker-name=Worker_Name > miner.log 2>&1 &
```
{% endcode %}

* [ ] 替換礦池地址`-P`：以[**概覽**](https://oula.network/zh/pool/manager)頁提供的「**礦池地址**」為準
* [ ] 替換帳戶`--account`：[**子賬戶管理**](https://oula.network/zh/pool/manager?tab=subAccount)頁已創建的「**賬戶名**」
* [ ] 替換設備名`--worker-name`：礦工名稱

{% hint style="warning" %}
子賬戶和礦工名稱可自定義，需滿足全域唯一性！&#x20;

建議使用2-15個小寫字母、數字或其組合，且不能以數字開頭。
{% endhint %}

* 執行查看日誌命令

```bash
tail -f miner.log
```

{% hint style="success" %}
若在<mark style="color:red;">`miner.log`</mark>中見到`ProgPow kernel`相關日誌，則表示程序已成功啟動。
{% endhint %}

{% hint style="warning" %}
如果您不需要輸出日誌內容，可以將啟動命令中的“&> miner.log &”替換為“> /dev/null 2>&1 &”。
{% endhint %}

* 執行程式停止命令

```bash
killall oula-gpu-miner
# 強制執行
```

### 礦機監控及產出查看

設備穩定運行並提交數據後，在用戶面板→礦池市場→[礦工管理](https://oula.network/zh/pool/manager?tab=miner)和[產出/支付](https://oula.network/zh/pool/manager?tab=output)模組下，切換對應的子賬戶即可檢視礦工運行狀態、產出詳情及支付詳情。





[**返回Oula**](https://oula.network/zh/login)
