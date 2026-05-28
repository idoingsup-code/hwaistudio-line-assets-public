# HW AI Studio LINE 素材更新報告

版本：2026.05.28.001  
發布時間：2026-05-28 09:30（UTC+8）  
發布人員：HANK  
狀態：已發布  

## 更新摘要

建立第一版素材資料骨架，作為後續 GitHub 公開素材庫與管理端發布流程的基準。

## 新增內容

### 素材包

- HW 系列 / 好事多（內部 ID：`hw_haoshiduo`）

### 靜態貼圖

- `hw_haoshiduo_001.png`
- `hw_haoshiduo_002.png`

### 動態素材

- `hw_haoshiduo_motion_001.gif`

### 官方資訊

- LINE：@935ycsty
- Email：idoingsup@gmail.com
- 官網：https://hwaistudio.pythonanywhere.com/

## 修改內容

- 無。此版本為初始化版本。

## 停用內容

- 無。

## 檢查項目

- JSON 可解析
- 素材包 ID 不重複
- 素材 ID 不重複
- `pack_id` 指向有效素材包
- `icon_item_id` 指向有效素材
- 原始素材檔存在
- 縮圖檔存在
- SHA256 雜湊正確
- 公開資料夾未包含 draft / archive / disabled / source / secret 類目錄

## 下一步

1. 讓主程式先讀取本機 `public_dist/manifest.json`。
2. 確認貼圖 / 動態素材 / 我的圖片三個頁籤的資料流程。
3. 再開發管理端 UI 與 GitHub 發布流程。

## Git 資訊

Branch：main  
Commit：LOCAL_V0_1_NOT_PUSHED  
