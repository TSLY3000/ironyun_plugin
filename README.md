
#  NX Witness + IronYun Plugin 使用手冊

## 安裝說明（Install Instructions）

1. **停止伺服器 (Stop the server)**  
2. 將 `ironyun.dll` 檔案複製至以下路徑：  
   ```
   C:/Program Files/Network Optix/Nx Witness/MediaServer/plugins
   ```
3. **重新啟動伺服器 (Restart the server)**


## 插件安裝確認

1. 於 NX Witness 右鍵點擊任一相機，選擇 **Camera Settings**。
2. 確認左側出現 **IronYun Plugin**，表示已安裝成功。
3. Plugin 分為三個模組：
   - **物件偵測 (Object Detection)**
   - **入侵偵測 (Intrusion Detection)**
   - **人臉辨識 (Facial Recognition)**

## 注意事項

- 使用 Plugin 時，請務必開啟 **Object Search**，才能查看分析結果。
- 啟用功能後，請前往 **System Administration > Plugins > IronYun** 設定 HTTP 接口等基本資料。
- IronYun 系統端需設定正確的資料格式與位置，並確保 ID、OD 和版本設定與 NX 一致。

---

## 1. 物件偵測（Object Detection）

### 功能說明

- IronYun 正確設定後，會自動發送偵測結果 (`results`) 至 NX Plugin。
- 開啟 **Object Search**，可於側邊欄查看偵測結果。
- 偵測內容包括：
  - 類型（objectType）
  - 信心值（confidence）
  - 座標框（x, y, w, h）
  - 顏色資訊（colors）

---

## 2. 入侵偵測（Intrusion Detection）

### 功能說明

- 功能與 Object Detection 類似，主要差異是支援 **ROI（Region of Interest）** 設定。
- Plugin 可視覺化顯示 ROI 區域。

### 設定流程

1. 使用 **Postman**，POST 請求至 IronYun API（如 `http://xxx.xxx.xxx.xxx/...`）取得 Token。
2. 在 Plugin 中輸入：
   - **IP Address**
   - **Token**
   - **ROI 名稱**
3. 點擊 **Apply** 載入 ROI 設定。
4. 亦可於 NX GUI 中選擇是否顯示 ROI 可視範圍。

---

## 3. 人臉辨識（Facial Recognition）

### 功能說明

- 若 NX 系統已建立名單，將會比對人臉並顯示對應姓名。
- 若無對應名單，則標示為 **Not on List**。
- 顯示結果包含：
  - 臉部框位置（face.rect）
  - 名單名稱（targetName，若存在）

---

## 顏色屬性支援

| 模組             | 顏色顯示 | 額外說明                         |
|------------------|----------|----------------------------------|
| Object Detection | ✅ 支援   | 顯示主要顏色 (`colors`)          |
| Intrusion Detection | ✅ 支援   | 同上，並搭配 ROI 顯示            |
| Facial Recognition | ❌ 不支援 | 顯示名單與姓名，無顏色屬性顯示     |

---
## 總覽表格

| 模組名稱           | 功能說明                                                | 額外備註                          |
|--------------------|---------------------------------------------------------|-----------------------------------|
| Object Detection   | 顯示物件類型、位置與主要顏色屬性                         | 需開啟 Object Search              |
| Intrusion Detection| 類似 Object Detection，但加入 ROI 設定與顯示             | 需提供 Token 並選擇 ROI 名稱     |
| Facial Recognition | 與 NX 名單比對人臉，顯示姓名；若無名單則標示 Not on List | 不支援顏色顯示，僅顯示姓名與臉框 |

---

