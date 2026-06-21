# 元智大學紅磚道交通號誌即時辨識系統

基於 YOLOv8 之元智大學校園紅磚道交通號誌即時偵測與辨識系統

---

## 📌 專題目標

本專題以元智大學校園紅磚道為應用場景，透過自主收集與標註的影像資料，訓練一個物件偵測模型，用以即時辨識紅磚道周邊常見的交通號誌（包含「禁止進入」、「禁止行駛」、「靠右行駛」三種標誌）。期望此系統未來能應用於校園導覽或行人安全提示，協助使用者快速辨識周遭的交通管制資訊。

---

## 📌 系統設計

### 1. 資料集收集與標註

- 於元智大學校園紅磚道實地拍攝三段約 30 秒的影片，分別對應三種交通號誌
- 使用 Python（OpenCV）將影片每隔固定幀數自動截圖，共取得約 250 張影像
- 使用線上標註工具 [makesense.ai](https://www.makesense.ai/) 進行物件框選與類別標註，並匯出為 YOLO 格式

| 類別代號 | 標誌名稱 |
|---------|---------|
| 0 | cant_drive（禁止行駛）|
| 1 | cant_in（禁止進入）|
| 2 | right（靠右行駛）|

### 2. 物件偵測方法

- 採用 **YOLOv8（You Only Look Once v8）** 作為物件偵測模型
- 使用 Ultralytics 提供之 `yolov8n.pt` 預訓練權重進行遷移學習（Transfer Learning）

### 3. 訓練方式

- **訓練環境**：Google Colab（T4 GPU）
- **訓練參數**：epochs=50、imgsz=640、batch=16
- **訓練結果**：
  - mAP50：0.995
  - mAP50-95：0.830
  - Precision：0.993
  - Recall：1.000

訓練程式碼請見 `train_colab.ipynb`

---

## 📂 專案結構

```
yzu-traffic-sign-detection/
├── README.md
├── best.pt              # 訓練完成的模型權重
├── detect.py             # 即時偵測程式
├── data.yaml              # 類別設定檔
├── train_colab.ipynb       # Colab 訓練程式碼
└── yolo_dataset/
    ├── images/
    │   ├── train/
    │   └── val/
    └── labels/
        ├── train/
        └── val/
```

---

## 🛠️ 安裝與執行方式

### 1. 安裝套件

```bash
pip install ultralytics opencv-python
```

### 2. 執行即時偵測

確認 `best.pt` 與 `detect.py` 在同一個資料夾內，執行：

```bash
python detect.py
```

開啟攝影機後，將交通號誌置於鏡頭前，畫面會即時顯示偵測框與類別名稱。

按下鍵盤 **q** 鍵結束程式。

### 3. （選用）重新訓練模型

1. 開啟 `train_colab.ipynb` 於 Google Colab
2. 將 `yolo_dataset/` 與 `data.yaml` 上傳至 Google Drive
3. 依照 Notebook 步驟執行訓練

---

## 📊 模型效能

| 指標 | 數值 |
|------|------|
| mAP50 | 0.995 |
| mAP50-95 | 0.830 |
| Precision | 0.993 |
| Recall | 1.000 |

---

## 🎬 展示影片

（補充中）

---

## 📜 使用之開源資源

- [Ultralytics YOLOv8](https://github.com/ultralytics/ultralytics) — 物件偵測模型框架，採用 AGPL-3.0 授權
- [makesense.ai](https://www.makesense.ai/) — 線上影像標註工具

本專題之資料集為自行拍攝、標註，模型訓練流程與校園場景應用為團隊獨立完成。
