

# 樹莓派 影像串流 
# (RTSP / WebRTC / HLS) with mediaMTX
---

以 **Raspberry Pi 5** 與 **Raspberry Pi Zero** 的相機為來源，提供 **RTSP**、**WebRTC**、**HLS** 串流，供後端 **AI Server** 進行分析與應用。
快速測試可用 VLC / Chrome / Safari 等工具。

> **網段說明**：以下示範使用裝置 IP `10.18.61.229`，請依你的實際 IP 替換。

---

## 🔎 立即測試連結（建議先驗證）

**WebRTC（預設 8889，Chrome 建議）**

* http://10.18.61.229:8889/mystream
* http://10.18.61.229:8889/rotate

**HLS（預設 8888，Chrome & Safari）**

* http://10.18.61.229:8888/mystream
* http://10.18.61.229:8888/rotate   ← *說明：此處為 HLS，故使用 8888 連接埠。*

**RTSP（預設 8554，VLC/CCTV NVR 建議）**

* `rtsp://10.18.61.229:8554/mystream`
* `rtsp://10.18.61.229:8554/rotate`

> 連接埠對照：RTSP `8554`、HLS `8888`、WebRTC `8889`（皆為 mediaMTX 預設，可於 `mediamtx.yml` 調整）

---

## 目錄

1. [快速以 VLC 測 RTSP](#1-快速以-vlc-測-rtsp)
2. [安裝與設定 mediaMTX](#2-安裝與設定-mediamtx)

   * [2.1 下載執行檔](#21-下載執行檔)
   * [2.2 基本設定：相機作為來源](#22-基本設定相機作為來源)
   * [2.3 轉 90° 產生第二路串流](#23-轉-90-產生第二路串流)
   * [2.4 設定為 systemd 服務](#24-設定為-systemd-服務)
   * [2.5 啟停與查看日誌](#25-啟停與查看日誌)
3. [常見問題與排錯](#3-常見問題與排錯)
4. [備註與建議](#4-備註與建議)

---

## 1. 快速以 VLC 測 RTSP

建立一個最簡單的 RTSP 轉推腳本（以 `rpicam-vid` → `cvlc` 推 RTSP）：

```bash
#!/bin/bash
# 檔名建議：rtsp.sh
# 功能：從樹莓派相機抓取影像，透過 VLC 轉推成 RTSP（/stream2）
# 需求：已安裝 rpicam-vid 與 VLC（cvlc）

rpicam-vid -t 0 --codec libav --libav-format mpegts -o - \
| cvlc stream:///dev/stdin --sout '#rtp{sdp=rtsp://:8554/stream2}'
```

```bash
chmod +x rtsp.sh
./rtsp.sh
# VLC 打開：rtsp://<PI_IP>:8554/stream2
```

---

## 2. 安裝與設定 mediaMTX

### 2.1 下載執行檔

> 請依 CPU 架構下載對應檔案（例：**arm64** for Pi 5，**armv7** for部分 32-bit 裝置）。以下以 arm64 為例：

```sh
# 下載 CPU 的 Bin 執行檔案（ARM64 / x86_64 / armv7 擇一）
curl -LO https://github.com/bluenviron/mediamtx/releases/download/v1.15.0/mediamtx_v1.15.0_linux_arm64.tar.gz

# 解壓
tar -xzf mediamtx_v1.15.0_linux_arm64.tar.gz
cd mediamtx_v1.15.0_linux_arm64

# 編輯設定檔（範例）
vi mediamtx.yml   # 改設定檔 stream 名稱、路徑
```

### 2.2 基本設定：相機作為來源

在 `mediamtx.yml` 調整 `paths`，使 `mystream` 直接從 Raspberry Pi 相機取得串流：

```yml
paths:
  mystream:             # 第一個來源路徑,可自己改
    source: rpiCamera   # 來源是 rpi 鏡頭
```

啟動：

```sh
./mediamtx   # 啟動 mediaMTX
```

測試連結
WebRTC（8889）
http://10.18.61.229:8889/mystream

HLS（8888）
http://10.18.61.229:8888/mystream

RTSP（8554）
rtsp://10.18.61.229:8554/mystream



> 若你將 `mediamtx.yml` 放在其他目錄，啟動時可帶 `-config /path/to/mediamtx.yml`。

### 2.3 轉 90° 產生第二路串流

若需要旋轉影像（如相機直立安裝），可用 FFmpeg 將 `mystream` 轉 90° 後，推回同機的 `rotate` 路徑。

在 `mediamtx.yml` 的 `paths` 區塊加入：

```yml
paths:
  rotate:                 # 第二路輸出的 RTSP/HLS/WebRTC 路徑（作為 FFmpeg 推流目標）
  mystream:               # 第一個來源路徑
    source: rpiCamera
    runOnReady: >         # 注意縮排；啟動後自動執行，將 mystream 轉 90° 推到 /rotate
      ffmpeg -i rtsp://localhost:8554/mystream
        -vf "transpose=2"
        -pix_fmt yuv420p -c:v libx264 -preset ultrafast -b:v 600k
        -max_muxing_queue_size 1024 -f rtsp rtsp://localhost:8554/rotate
    runOnReadyRestart: yes
```

> `transpose=2` 表示 90° 旋轉（方向依鏡頭安裝而異，可改 `0/1/2/3` 試驗）。此流程會同時保留未旋轉的 `mystream` 與旋轉後的 `rotate` 兩路。

### 2.4 設定為 systemd 服務

建立 service 檔案（以 `pi` 使用者、安裝於 `/home/pi/mtx_arm64` 為例，請依實況調整）：

```sh
sudo vi /etc/systemd/system/mediamtx.service
```

內容：

```ini
[Unit]
Description=MediaMTX Server
After=multi-user.target
Requires=network.target

[Service]
EnvironmentFile=-/home/pi/mtx_arm64
ExecStart=/home/pi/mtx_arm64/mediamtx /home/pi/mtx_arm64/mediamtx.yml
Environment=DISPLAY=:0
Type=simple
Restart=on-failure
StandardOutput=file:/home/pi/mtx_arm64/mtx.log
StandardError=inherit
User=pi
Group=pi

[Install]
WantedBy=multi-user.target
```

複製設定並啟用服務：

```sh
sudo systemctl daemon-reload
sudo systemctl enable mediamtx
sudo systemctl start mediamtx
```

### 2.5 啟停與查看日誌

```sh
sudo systemctl status mediamtx
sudo systemctl restart mediamtx
sudo systemctl stop mediamtx

# 依本 service 設定，stdout 會寫到：
tail -f /home/pi/mtx_arm64/mtx.log
```

---

## 3. 常見問題與排錯

* **沒有影像或黑畫面**

  * 確認相機模組連接與 `libcamera`/`rpicam-*` 可正常取流。
  * 嘗試直接執行快速 RTSP 腳本（`rtsp.sh`）先驗證硬體與驅動。
* **無法開啟 HLS 或 WebRTC**

  * 確認 `mediamtx.yml` 的對應協定已啟用（預設為開）。
  * 防火牆與路由器是否允許 `8888`（HLS）與 `8889`（WebRTC）。
* **轉 90° 的串流沒有出現**

  * 檢查 `runOnReady` 的縮排與 `ffmpeg` 參數是否正確。
  * 以 `journalctl -u mediamtx -f` 或 `tail -f mtx.log` 查看錯誤訊息。
  * 確認 `paths` 中存在 `rotate:` 路徑（做為推流目標）。
* **VLC 或 NVR 播 RTSP 卡頓**

  * 嘗試調降 `-b:v`（例如 `600k` → `400k`），或改 `-preset`。
  * 在 Wi‑Fi 環境下可適度提高 `keyint`/GOP 以增穩（需依 FFmpeg 參數調整）。

---

## 4. 備註與建議

* **IP**：將 `10.18.61.229` 替換為你的樹莓派實際 IP。
* **架構**：請下載符合 CPU 架構的 mediaMTX 壓縮檔（arm64 / armv7 / x86\_64）。
* **連接埠**：預設 RTSP `8554`、HLS `8888`、WebRTC `8889`。如有更動，請同步更新測試連結。
* **安全性**：預設多為區網測試設定，若對外網開放，建議加上存取控制、TLS 與反向代理等防護。
* **設定檔路徑**：若將 `mediamtx.yml` 放在 `/usr/local/etc/`，建議在 `ExecStart` 明確帶上 `-config /usr/local/etc/mediamtx.yml`，避免找不到設定檔。
* **文件中的小修正**

  * HLS 的 `rotate` 測試網址已調整為 `:8888/rotate`（對齊 HLS 連接埠）。
  * `cp mediamtx.tml` 改為 `cp mediamtx.yml`。

---

### 附：測試連結彙整

* **WebRTC（8889）**
  `http://10.18.61.229:8889/mystream`
  `http://10.18.61.229:8889/rotate`

* **HLS（8888）**
  `http://10.18.61.229:8888/mystream`
  `http://10.18.61.229:8888/rotate`

* **RTSP（8554）**
  `rtsp://10.18.61.229:8554/mystream`
  `rtsp://10.18.61.229:8554/rotate`

---

