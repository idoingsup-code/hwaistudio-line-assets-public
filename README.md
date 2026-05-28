# HW AI Studio LINE 素材助手 / 素材管理器

版本：v0.9.10 測試修正版  
更新日期：2026-05-28  
專案：LINE 外掛貼圖 / HW AI Studio LINE 素材助手  
狀態：功能測試中；PNG/JPG 與 GIF 流程保持既有可用狀態，MP4 改為真實檔案拖放模擬，仍需 Windows + LINE 實機確認。

---

## 1. 專案用途

本工作區用於管理、發布與使用 HW AI Studio 的 LINE 素材：

- 使用者端：提供素材選擇、貼圖貼入、GIF 動態素材使用、MP4 影片素材檔案傳送輔助。
- 管理端：管理素材包、匯入素材、編輯資料、產生發布包、檢查公開包、發布官方公開素材。
- 官方公開素材：透過指定公開 repo 發布，供使用者端讀取最新素材。

---

## 0. v0.9.10 重要更新

- GIF：回復並鎖定既有可用流程，不再套用 MP4 實驗流程。
- MP4 / MOV / M4V：改用 Windows 真實檔案拖放模擬，目標是讓 LINE 自行跳出「傳送檔案」確認視窗。
- 03_PUBLISH_OFFICIAL_ASSETS.bat：產生官方公開包時，會把主目錄 README.md 複製到公開 repo 根目錄並一起 commit / push。
- 發布目標仍強制鎖定 `idoingsup-code/hwaistudio-line-assets-public`。

## 2. 日常使用入口

根目錄只保留三個主要入口：

```text
01_START_LINE_ASSISTANT.bat
02_START_ASSET_MANAGER.bat
03_PUBLISH_OFFICIAL_ASSETS.bat
```

### 01_START_LINE_ASSISTANT.bat

開啟使用者端：

```text
HW AI Studio LINE 素材助手
```

用途：選擇素材並送到 LINE。

### 02_START_ASSET_MANAGER.bat

開啟管理端：

```text
HW AI Studio 素材管理器
```

用途：匯入、編輯、刪除、檢查、發布素材。

### 03_PUBLISH_OFFICIAL_ASSETS.bat

一鍵發布官方公開素材。流程包含：

```text
1. 檢查素材資料
2. 產生本機發布包
3. 產生官方公開素材包
4. 公開包完整性檢查
5. 同步到使用者端 bundled_assets
6. commit 本機公開 repo
7. push 到官方公開素材 repo
```

---

## 3. 正確發布目標

官方 LINE 素材公開 repo 必須是：

```text
idoingsup-code/hwaistudio-line-assets-public
```

對應遠端 URL：

```text
https://github.com/idoingsup-code/hwaistudio-line-assets-public.git
```

發布前可用下列指令確認：

```bat
cd C:\Users\USER\Desktop\HWAssetManagerWorkspace\github_public_repo_local_repo
git remote -v
```

應顯示：

```text
origin  https://github.com/idoingsup-code/hwaistudio-line-assets-public.git (fetch)
origin  https://github.com/idoingsup-code/hwaistudio-line-assets-public.git (push)
```

不可發布到：

```text
idoingsup-code/hwaistudio-public-assets
```

該 repo 曾被誤推 LINE 素材，已清理回原本狀態。後續發布流程必須阻止誤推。

---

## 4. 目前素材流程狀態

### PNG / JPG

狀態：可用，維持貼圖流程。

重點：

- 預設使用純圖片剪貼簿模式。
- 不再同時放入文字或檔案路徑，避免 LINE 跳出「圖片 / 文字」選擇。
- 透明 PNG 需持續實測是否完整保留 alpha。

### GIF

狀態：v0.9.10 已回復原本可用流程。

重點：

- v0.9.8 曾錯誤改成開啟檔案總管，此方向已撤回。
- 後續修改 MP4 時，不得共用並破壞 GIF 流程。

### MP4 / MOV / M4V

狀態：v0.9.10 改為自動檔案拖放嘗試，仍需實機確認。

重點：

- MP4 不適合走純圖片剪貼簿。
- MP4 不應要求使用者手動開檔案總管再拖曳。
- 目前程式會嘗試直接送 Windows 檔案拖放訊息到指定 LINE 視窗。
- 若 LINE Desktop 不接受此方式，下一步需改成更底層的滑鼠拖曳模擬或 Windows UI Automation。

---

## 5. 使用者端畫面規則

使用者端不得暴露技術來源：

```text
正確顯示：官方公開素材
避免顯示：GitHub、raw.githubusercontent.com、OSError、FileNotFoundError 等技術字樣
```

貼圖格子規則：

- 不顯示 01 / 02 / 03 編號。
- 素材包應顯示為可選分類，例如「柴犬」。
- 「最近使用」沒有紀錄時，不代表素材沒有載入。

---

## 6. 管理端狀態

管理端目前支援：

- 素材包列表
- 素材項目列表
- 右側素材預覽與詳細資料
- 匯入素材
- 修改素材資料
- 停用 / 啟用素材
- 刪除紀錄
- 刪除紀錄 + 實體檔案
- 執行檢查
- 產生發布包
- 查看發布紀錄
- 公開包檢查
- 同步到使用者端 bundled_assets

管理端 UI 已在 v0.8.3 修正：

- 中間表格縮寬
- 右側預覽固定寬度
- 詳細資料可捲動
- 目前素材包資訊同步
- 危險操作分區

---

## 7. 版本重點摘要

### v0.8.x 管理端建立與 UI 修正

- 建立管理端基礎功能。
- 保留使用者端 v0.7.2 穩定版。
- 新增素材匯入、編輯、刪除、發布、檢查、同步流程。
- 修正刪除後 manifest integrity 未更新造成 warning。
- 修正管理端表格與素材預覽區配置。

### v0.9 發布與版本管理

- 新增發布紀錄、版本差異、公開包安全檢查。
- 使用者端顯示素材版本與來源。
- 日常 BAT 整理成三個主要入口。

### v0.9.1 使用者端顯示與發布流程整理

- 隱藏 GitHub 字樣。
- 移除貼圖下方編號。
- PNG 改為純圖片剪貼簿模式。

### v0.9.2 發布完整性與快取修正

- 發布目標鎖定 `hwaistudio-line-assets-public`。
- 修正錯抓 `sample_workspace` 的問題，改抓根目錄 `public_dist`。
- 增加公開包缺檔檢查。
- 使用者端重新載入時強制檢查最新 manifest。

### v0.9.3 BAT 路徑修正

- 修正 Windows BAT 路徑尾端引號造成 `WinError 123`。

### v0.9.4 遠端快取與 base URL 修正

- 修正使用者端讀不到已上線柴犬素材包的問題。
- 遠端 base URL 改由 manifest URL 自動推導。
- 遠端資料採 staging cache 驗證後覆蓋。

### v0.9.5 純圖片剪貼簿修正

- PNG/JPG 不再同時放入文字與檔案路徑。
- 避免 LINE 詢問「圖片 / 文字」。

### v0.9.6 動態素材與選單修正

- 修正剪貼簿模式選單勾選狀態。
- `clipboard_mode` 可寫入 `settings.json`。

### v0.9.7 MP4 檔案傳送嘗試

- 嘗試讓 MP4 走 LINE 檔案傳送模式。
- 後續實測確認單純剪貼簿 FileDrop 不足以穩定觸發 LINE 傳檔。

### v0.9.8 動態素材開檔流程

- 曾把 GIF/MP4 改成開啟檔案位置。
- 後續確認此方向不符合需求，已由 v0.9.10 修正取代。

### v0.9.10 GIF 回復 + MP4 自動拖放嘗試

- GIF 回復原流程。
- MP4 不再開啟檔案總管。
- MP4 改為嘗試直接送 Windows 檔案拖放訊息到指定 LINE 視窗。
- 使用者端版本：`2026.05.28.025`。

---

## 8. 測試清單

每次更新後至少測：

```text
1. 01_START_LINE_ASSISTANT.bat 可開啟
2. 02_START_ASSET_MANAGER.bat 可開啟
3. 使用者端可看到「柴犬」素材包
4. PNG/JPG 點擊後能送到 LINE
5. PNG 不再跳「圖片 / 文字」選擇
6. GIF 保持可用
7. MP4 點擊後是否能觸發 LINE 原生「傳送檔案」確認
8. 03_PUBLISH_OFFICIAL_ASSETS.bat 發布目標正確
9. GitHub 正確 repo 出現 assets/stickers/dog 等素材目錄
10. 使用者端來源只顯示「官方公開素材」
```

---

## 9. 目前已知風險

### MP4 自動送入 LINE

v0.9.10 採自動檔案拖放訊息，但 LINE Desktop 是否接受取決於：

- LINE 視窗類型
- Windows 權限
- 螢幕縮放
- LINE 版本
- 是否已正確指定 LINE 視窗

若仍無法跳出 LINE「傳送檔案」確認視窗，下一步需改用：

```text
低階滑鼠拖曳模擬 / Windows UI Automation
```

### GIF 不可再被 MP4 修正牽連

GIF 已回復，後續不得把 GIF 與 MP4 共用同一條不穩定流程。

### 報告與 README 需跟版

每次 patch-only / full zip 應包含：

```text
README.md
reports/program_update_<version>_<date>.md
reports/release_history_<range>.md
reports/known_issues_<version>_<date>.md
```

---

## 10. 建議下一步

1. 實機測 v0.9.10：PNG、GIF、MP4 三種素材。
2. 若 MP4 自動拖放仍失敗，改做低階滑鼠拖曳模擬，不再改 GIF。
3. 補自動報告產生流程，確保每次輸出都同步更新 README 與 reports。
4. 若 v0.9.10 測試通過，封存為穩定候選版。


## v0.9.10 補充測試標準

1. PNG / JPG：點擊後貼入 LINE，不應跳出「圖片 / 文字」選擇。
2. GIF：維持目前可用流程；若 LINE 顯示「圖片 / 文字」，選「圖片」後 GIF 應進入訊息框。
3. MP4：點擊後應嘗試拖放到指定 LINE 視窗，理想結果是 LINE 出現「傳送檔案」確認視窗。
4. 發布：執行 `03_PUBLISH_OFFICIAL_ASSETS.bat` 後，公開 repo 根目錄應同步出現此 README.md。
