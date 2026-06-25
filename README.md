# 安裝方式

1. 安裝套件：
bash
pip install ultralytics opencv-python
2. 確認 `best.pt`（模型權重）與 `detect12345.ipynb` 在同一個資料夾內

# 執行方式

開啟 `detect12345.ipynb`，使用Jupyter Notebook執行：
- 程式會開啟攝影機進行即時偵測
- 將交通標誌置於鏡頭前，畫面會顯示偵測框與類別名稱

# 使用之開源資源

- [Ultralytics YOLOv8](https://github.com/ultralytics/ultralytics) — 物件偵測模型框架，採用 AGPL-3.0 授權，本專題使用其 `yolov8n.pt` 預訓練權重進行遷移學習
- [makesense.ai](https://www.makesense.ai/) — 線上影像標註工具，用於標註自行拍攝之資料集

