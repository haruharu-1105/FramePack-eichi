# FramePack-eichi

FramePack-eichi 是基於 lllyasviel 的 [lllyasviel/FramePack](https://github.com/lllyasviel/FramePack) 分支，由 nirvash 的 [nirvash/FramePack](https://github.com/nirvash/FramePack) 開發的功能增強版本。在 nirvash 的開創性改進基礎上，增加了許多細緻的功能。

[https://github.com/hinablue](https://github.com/hinablue) **Hina Chen氏**より多言語対応の協力をいただき非常に感謝しております。

感謝您 [https://github.com/hinablue](https://github.com/hinablue) **Hina Chen** 對多語言支援的協助。

Special thanks to [https://github.com/hinablue](https://github.com/hinablue) **Hina Chen** for the multilingual support contribution.

[繁体字中文版说明文档请点击此处](README_zh.md)

> 注意：目前部分文檔已提供繁體中文版本。英文版 README 和其他語言版本將在日後添加。目前的翻譯涵蓋 v1.7.1 的功能，最新 v1.8 功能的翻譯正在進行中。

![FramePack-eichi畫面1](images/framepack_eichi_screenshot1.png)

## 📘 名稱的由來

**Endframe Image CHain Interface (EICHI)**
- **E**ndframe: 強化和最佳化終端幀功能
- **I**mage: 改善關鍵幀圖像處理和視覺回饋
- **CH**ain: 複數的關鍵幀間的連接和關係的強化
- **I**nterface: 直感性的使用者體驗和 UI/UX 的提升

「eichi」是日本語的「睿智」（深刻的智慧、英知）的表達，代表著 AI 技術的進化和人間創造性的的融合，象征著本專案的哲學。
即叡智的差分幀從動畫製作中專案的現地改修仕別。

## 🌟 主要功能

- **多語言支援（i18n）**：支援日語、英語、繁體中文的 UI ※v1.8.1 新增

- **高品質影片生成**：從單一圖像生成自然流暢的影片 ※現有功能
- **靈活的影片長度設定**：支援 1-20 秒的各個區段模式 ※獨特功能
- **區段幀大小設定**：可切換 0.5 秒模式和 1 秒模式 ※v1.5 新增
- **全填充功能**：所有區段使用相同的填充值 ※v1.4 新增
- **多區段支援**：可在多個區段指定關鍵幀圖像，實現複雜動畫 ※nirvash 新增功能
- **區段專用提示詞設定**：可為每個區段指定獨立的提示詞 ※v1.2 新增
- **紅框/藍框關鍵幀圖像高效複製**：僅需兩個關鍵幀即可覆蓋所有區段 ※v1.7 新增
- **張量數據保存與合併**：可保存影片的潛在表示，並合併多個影片 ※v1.8 新增
- **提示詞管理功能**：輕鬆保存、編輯和重用提示詞 ※v1.3 新增
- **MP4 壓縮設定**：可調整影片檔案大小與品質的平衡 ※v1.6.2 從主版本合併
- **【測試中】Hunyuan LoRA 支援**：通過模型自定義添加獨特表現 ※v1.3 新增
- **輸出資料夾管理功能**：支援指定輸出資料夾和與作業系統無關的開啟方式 ※v1.2 新增
- **日誌功能**：提供詳細的進度資訊，結束時顯示處理時間，Windows 版本還會發出提示音 ※獨特功能
- **跨平台支援**：在 Windows 以外的環境中也能使用基本功能 ※可能

![FramePack-eichi畫面2](images/framepack_eichi_screenshot2.png)

## 📝 最新更新資訊 (v1.8.1)

### 主要變更

#### 1. 多語言支援（i18n）的實現
- **支援語言**：支援日語、英語、繁體中文三種語言
- **語言切換**：可通過以下執行檔切換語言
  - `run_endframe_ichi.bat` - 日語版（預設）
  - `run_endframe_ichi_en.bat` - 英語版
  - `run_endframe_ichi_zh-tw.bat` - 繁體中文版
- **UI 國際化**：按鈕、標籤、訊息等幾乎所有 UI 元素都已多語言化
- **顯示語言保存**：可通過命令行參數選擇語言（例如：`--lang en`）

※ 目前支援 v1.7.1 的功能，v1.8 的功能將在日後添加翻譯。

## 📝 更新資訊 (v1.8)

### 主要變更

#### 1. 張量數據合併功能的添加
- **張量數據保存功能**：將生成的影片的潛在表示（張量數據）以 .safetensors 格式保存
- **張量數據合併**：將保存的張量數據合併到新生成影片的「後方（末尾）」

#### 2. VAE 解碼處理的優化
- **分塊處理方式的引入**：將大型張量分割成小塊進行高效處理
- **記憶體效率的提升**：通過 GPU 和 CPU 之間的明確數據移動，減少記憶體使用量
- **相容性的強化**：通過設備和類型的明確調整提高穩定性

#### 3. 中間檔案管理的改進
- **中間檔案的自動刪除**：自動檢測和刪除合併處理過程中生成的中間檔案
- **刪除檔案的 feedback**：明確顯示已刪除檔案的資訊

### MP4 合併處理的詳細說明

1. **自動合併流程**：當張量數據被合併時，對應的 MP4 影片也會自動合併
2. **中間處理檔案**：合併處理過程中會暫時生成「{檔案名稱}_combined_interim_{編號}.mp4」的中間檔案，處理完成後會自動刪除
3. **原始檔案的保存**：同時保存生成的原始影片檔案「{檔案名稱}.mp4」和合併影片「{檔案名稱}_combined.mp4」
4. **分塊處理的優化**：即使是大型 MP4 檔案也能高效處理，在控制記憶體使用量的同時實現高品質合併
5. **進度顯示**：合併處理過程中會在 UI 上顯示進度，可以確認處理進行到哪個階段

## 張量數據的使用方法

### 張量數據保存功能

1. 進行一般的影片生成設定（上傳圖像、輸入提示詞等）
2. 勾選 **「保存張量數據」** 核取方塊（在 UI 右側新增）
3. 點擊 **「開始生成」** 按鈕生成影片
4. 生成完成時，除了影片（.mp4）外，還會保存張量數據（.safetensors）
5. 保存的張量數據會以與原始影片相同的檔案名稱（副檔名不同）保存在輸出資料夾中

### 張量數據合併功能

1. 從 **「張量數據上傳」** 欄位上傳已保存的 .safetensors 檔案
2. 照常設定圖像和提示詞，點擊 **「開始生成」** 按鈕
3. 新影片生成後，會自動生成將上傳的張量數據合併到「後方（末尾）」的影片
4. 合併後的影片會以「原始檔案名稱_combined.mp4」的形式保存
5. 如果開啟了張量數據保存，合併後的張量數據也會被保存

### MP4 合併處理的詳細說明

1. **自動合併流程**：當張量數據被合併時，對應的 MP4 影片也會自動合併
2. **中間處理檔案**：合併處理過程中會暫時生成「{檔案名稱}_combined_interim_{編號}.mp4」的中間檔案，處理完成後會自動刪除
3. **原始檔案的保存**：同時保存生成的原始影片檔案「{檔案名稱}.mp4」和合併影片「{檔案名稱}_combined.mp4」
4. **分塊處理的優化**：即使是大型 MP4 檔案也能高效處理，在控制記憶體使用量的同時實現高品質合併
5. **進度顯示**：合併處理過程中會在 UI 上顯示進度，可以確認處理進行到哪個階段

### 應用場景

- **長時間影片的分割生成**：將超出 GPU 記憶體限制的長影片分成多個會話生成
- **影片的連續性**：跨越多個會話創建具有一致性的長影片
- **現有影片的擴展**：在之前生成的影片中添加新場景
- **實驗性生成**：保存幀，作為新生成的起點重複使用

### 終點和關鍵幀圖像的持續性問題（正在處理中）

部分用戶報告了以下問題，目前正在考慮對策：

- 生成中斷後重新開始生成時，終點和關鍵幀圖像可能不會被使用
- 刪除圖像後重新上傳可以解決問題，但在開始生成前很難發現問題
- 如果確認存在此問題，請關閉圖像後重新上傳
- 在 v1.5.1 中，已修改為在按下 Start 按鈕時明確重新獲取圖像

### Hunyuan LoRA對應情況

暫定對應狀態：

- 在 v1.6 中，LoRA 應用邏輯已統一，高 VRAM 模式和低 VRAM 模式使用相同的直接應用方式
- VRAM 管理的基準值已更改（60GB→100GB），使更多用戶可以在低 VRAM 模式下運行
- 使用時 VRAM 16GB 可能稍顯緊張，但處理本身比開始前的磁碟讀取時間更短。建議使用較多記憶體
- 也收到了一些關於在高 VRAM 電腦上無法正常運行的詢問，正在考慮進行根本性檢討

## 💻 安裝方法

### 必要條件

- Windows 10/11（Linux/Mac也可能支援基本功能）
- NVIDIA GPU（建議RTX 30/40系列，最低8GB VRAM）
- CUDA Toolkit 12.6
- Python 3.10.x
- 最新版NVIDIA GPU驅動程式

※ Linux支援在v1.2得到加強，並添加了開啟功能，但部分功能可能有限制。

### 步驟

#### 安裝官方套件

首先需要安裝原始的FramePack。

1. 從[官方FramePack](https://github.com/lllyasviel/FramePack?tab=readme-ov-file#installation)下載Windows一鍵安裝包。
   點擊「Click Here to Download One-Click Package (CUDA 12.6 + Pytorch 2.6)」。

2. 解壓下載的套件，執行`update.bat`後再執行`run.bat`啟動。
   執行`update.bat`很重要。如果不執行，可能會使用包含潛在錯誤的舊版本。

3. 首次啟動時會自動下載所需模型（約30GB）。
   如果已有下載好的模型，請放置在`framepack\webui\hf_download`資料夾中。

4. 此時可以運行，但如果未安裝加速庫（Xformers、Flash Attn、Sage Attn），處理速度會較慢。
   ```
   Currently enabled native sdp backends: ['flash', 'math', 'mem_efficient', 'cudnn']
   Xformers is not installed!
   Flash Attn is not installed!
   Sage Attn is not installed!
   ```

   處理時間差異：※RAM:32GB、RXT4060Ti(16GB)的情況
   - 未安裝加速庫時：約4分46秒/25步驟
   - 安裝加速庫時：約3分17秒〜3分25秒/25步驟

5. 要安裝加速庫，請從[Issue #138](https://github.com/lllyasviel/FramePack/issues/138)下載`package_installer.zip`，解壓後在根目錄執行`package_installer.bat`（在命令提示字元中按Enter）。

6. 重新啟動確認加速庫是否安裝成功：
   ```
   Currently enabled native sdp backends: ['flash', 'math', 'mem_efficient', 'cudnn']
   Xformers is installed!
   Flash Attn is not installed!
   Sage Attn is installed!
   ```
   作者執行時，Flash Attn未安裝。
   注意：即使未安裝Flash Attn，對處理速度影響很小。測試結果顯示，Flash Attn的有無造成的速度差異很小，「Flash Attn is not installed!」狀態下約3分17秒/25步驟，與全部安裝時（約3分25秒/25步驟）幾乎相同。
   Xformers是否安裝影響最大。

#### 安裝FramePack-eichi

1. 將執行檔放置在 FramePack 的根目錄中：
   - `run_endframe_ichi.bat` - 日語版用（預設）
   - `run_endframe_ichi_en.bat` - 英語版用（v1.8.1 新增）
   - `run_endframe_ichi_zh-tw.bat` - 繁體中文版用（v1.8.1 新增）

2. 將以下檔案和資料夾放在`webui`資料夾中：
   - `endframe_ichi.py` - 主應用程式檔案
   - `eichi_utils` 資料夾 - 工具模組（v1.3.1改進，v1.6.2新增UI相關模組）
     - `__init__.py`
     - `frame_calculator.py` - 幀大小計算模組
     - `keyframe_handler.py` - 關鍵幀處理模組
     - `keyframe_handler_extended.py` - 關鍵幀處理模組
     - `preset_manager.py` - 預設管理模組
     - `settings_manager.py` - 設定管理模組
     - `ui_styles.py` - UI樣式定義模組（v1.6.2新增）
     - `video_mode_settings.py` - 影片模式設定模組
   - `lora_utils` 資料夾 - LoRA相關模組（v1.3新增，v1.3.2改進）
     - `__init__.py`
     - `dynamic_swap_lora.py` - LoRA管理模組（已廢棄掛鉤方式，僅支援直接應用方式）
     - `lora_loader.py` - LoRA載入模組
     - `lora_check_helper.py` - LoRA應用狀態確認模組（v1.3.2新增）
   - `locales` 資料夾 - 多語言支援模組（v1.8.1 新增）
     - `i18n.py` - 國際化（i18n）功能的核心實現
     - `ja.json` - 日語翻譯檔案（預設語言）
     - `en.json` - 英語翻譯檔案
     - `zh-tw.json` - 繁體中文翻譯檔案

3. 執行所需語言的執行檔，FramePack-eichi 的 WebUI 將以對應語言啟動：
   - 日語版：`run_endframe_ichi.bat`
   - 英語版：`run_endframe_ichi_en.bat`
   - 繁體中文版：`run_endframe_ichi_zh-tw.bat`

   或者，也可以從命令行直接指定語言啟動：
   ```bash
   python endframe_ichi.py --lang en  # 以英語啟動
   python endframe_ichi.py --lang zh-tw  # 以繁體中文啟動
   python endframe_ichi.py  # 以日語啟動（預設）
   ```

#### Docker 安裝
FramePack-eichi 可以通過 Docker 輕鬆設置，在不同系統之間提供一致的環境。

##### Docker 安裝前提條件
- 系統已安裝 Docker
- 系統已安裝 Docker Compose
- NVIDIA GPU（至少 8GB VRAM，推薦 RTX 30/40 系列）

##### Docker 設置步驟
1. **語言選擇**:
   Docker 容器默認以英文啟動。您可以通過修改 `docker-compose.yml` 中的 `command` 參數來更改：
   ```yaml
   # 日文：
   command: ["--lang", "ja"]
   
   # 繁體中文：
   command: ["--lang", "zh-tw"]
   
   # 英文（默認）：
   command: ["--lang", "en"]
   ```

2. **構建並啟動容器**:
   ```bash
   # 構建容器（首次或 Dockerfile 更改後）
   docker-compose build
   
   # 啟動容器
   docker-compose up
   ```
   
   要在後台運行（分離模式）：
   ```bash
   docker-compose up -d
   ```

3. **訪問 Web 界面**:
   容器運行後，通過以下地址訪問 Web 界面：
   ```
   http://localhost:7861
   ```

4. **首次運行注意事項**:
   - 首次運行時，容器將下載必要的模型（約 30GB）
   - 初始啟動期間可能會看到「h11 錯誤」（請參閱故障排除部分）
   - 如果您已經下載了模型，請將它們放在 `./models` 目錄中

#### Linux安裝方法

在Linux上，可以按照以下步驟執行：

1. 下載並放置上述必要檔案和資料夾。
2. 在終端機中執行以下命令：
   ```bash
   python endframe_ichi.py
   ```

#### Google Colab 安裝方法

- 請參考 [在 Google Colab 上試用 FramePack](https://note.com/npaka/n/n33d1a0f1bbc1)

#### Mac(mini M4 Pro) 安裝方法

- 請參考 [在 Mac mini M4 Pro 上運行熱門的 FramePack](https://note.com/akira_kano24/n/n49651dbef319)

## 🚀 使用方法

### 基本動畫生成　※既存功能

1. **上傳圖片**: 「Image」 框中上傳圖片
2. **輸入提示詞**: 輸入角色動作提示詞
3. **設定調整**: 調整動畫長度和種子值
4. **開始生成**: 「開始生成」 按鈕點擊

### 高級設定

- **生成模式選擇**:　※獨自功能
  - **通常模式**: 一般動畫生成
  - **循環模式**: 最終幀返回最初幀的循環動畫

- **所有邊距選擇**:　※v1.4 添加、此值越小1次會動畫越激烈
  - **所有邊距**: 所有區段使用同一邊距值
  - **邊距值**: 0~3 的整數值

- **影片長度設定**：※獨有功能的擴展
  - **1～20秒**

  [繼續閱讀](README_column_zh.md#-%E9%80%B2%E9%9A%8E%E8%A8%AD%E5%AE%9A)

## 🛠️ 配置資訊

### 語言設定

1. **通過執行檔選擇語言**:
   - `run_endframe_ichi.bat` - 日語版（預設）
   - `run_endframe_ichi_en.bat` - 英語版
   - `run_endframe_ichi_zh-tw.bat` - 繁體中文版

2. **通過命令行指定語言**:
   ```bash
   python endframe_ichi.py --lang en  # 以英語啟動
   python endframe_ichi.py --lang zh-tw  # 以繁體中文啟動
   python endframe_ichi.py  # 以日語啟動（預設）
   ```

※ README 的多語言版本將陸續推出。繁體中文版本請參閱 [README_zh.md](README_zh.md)。

有關設定的詳細資訊請參閱[這裡](README_column_zh.md#%E6%80%A7%E8%83%BD%E8%A8%AD%E5%AE%9A)。

## 🔧 故障排除

### 關於 h11 錯誤

當您首次啟動該工具並匯入圖像時，您可能會遇到許多類似以下的錯誤：
*控制台中將顯示錯誤，且 GUI 中不會顯示任何影像。

**大多數情況下，圖片其實已經上傳了，只是縮圖顯示不正常，所以還是可以產生影片的。 **

![FramePack-eichi錯誤畫面1](images/framepack_eichi_error_screenshot1.png)
```
ERROR:    Exception in ASGI application
Traceback (most recent call last):
  File "C:\xxx\xxx\framepack\system\python\lib\site-packages\uvicorn\protocols\http\h11_impl.py", line 404, in run_asgi
```
當處理 HTTP 回應時出現問題時，會顯示此錯誤。
如上所述，這通常發生在啟動過程的早期，即 Gradio 尚未完成啟動時。

解決方案：
  1. 刪除有「X」按鈕的圖片，然後重新嘗試上傳。
  2. 如果上傳同一文件重複失敗：
    - 完全停止 Python 進程，然後重新啟動應用程式
    - 重新啟動電腦，然後重新啟動應用程式

如果錯誤仍然存在，請嘗試其他圖片檔案或減小圖片大小。

### 記憶體不足錯誤

在 Windows 系統中，如果顯示「CUDA out of memory」或「RuntimeError: CUDA error」，請按照以下步驟操作：

1. `gpu_memory_preservation` 的值設定為 12-16GB
2. 關閉其他使用 GPU 的應用程式
3. 重新啟動應用程式
4. 降低圖片解析度（640x640 附近）

### 影片顯示問題

產生的影片在某些瀏覽器（尤其是 Firefox）和 macOS 上無法顯示：

- 症狀：影片無法在 Gradio UI 中顯示，縮圖無法在 Windows 上顯示，無法在某些播放器上播放
- 原因：`\framepack\webui\diffusers_helper\utils.py` 中的視訊編解碼器設定有問題

**此問題已透過合併原始 MP4 壓縮功能解決**

## 🤝 謝辞

本項目基於以下項目的貢獻：

- [lllyasviel/FramePack](https://github.com/lllyasviel/FramePack) - 感謝原作者 lllyasviel 的精湛技術與創新
- [nirvash/FramePack](https://github.com/nirvash/FramePack) - 感謝 nirvash 的開創性改進和擴展

## 📄 許可證

本項目遵循 [Apache 許可證 2.0](LICENSE) 發布。這與原 FramePack 專案的授權一致。



## 📝 更新日誌

### 2025-04-29：版本 1.8.1
  -**多語言支援（i18n）實作**：
    - 支援日語、英文、繁體中文三種語言
    - 新增了特定語言的可執行檔（`run_endframe_ichi_en.bat`、`run_endframe_ichi_zh-tw.bat`）
    - 所有元素支援多語言，包括 UI 文字、日誌訊息和錯誤訊息
    - 使用基於 JSON 檔案的翻譯系統提高了可擴展性
    - * 翻譯支援主要集中於 1.7.1 版的功能。 1.8 功能將在未來添加

### 2025-04-28：版本 1.8
-**新增了張量資料連線**：
  - 新增了以 .safetensors 格式儲存影片潛在表示的功能
  - 增加了將儲存的張量資料與新產生的影片合併的功能。
  - 利用區塊處理方法實現了對大規模張量資料的高效處理
  - 透過提高記憶體效率和增強設備/類型相容性來提高穩定性
  - 增加中間文件自動刪除及回饋顯示

### 2025-04-28：版本 1.7.1
  - **內部計算最佳化**：
    - 0.5秒模式片段數計算更加準確，提升影片產生的穩定性。
    - 幀計算參數（latent_window_size）從 5 改為 4.5
  - **使用者介面改進**：
    - 簡化影片模式名稱：刪除括號（例如「10（5x2）秒」→「10秒」）
    - 佈局清理：整個 UI 已經清理，以使其更易於使用。

### 2025-04-28：版本 1.7.0
- **關鍵影格影像複製功能重大改進**：
  - 引入紅/藍幀視覺區分
  - **紅幀（第 0 幀）** ⇒ 自動複製到所有偶數幀（0、2、4、6…）
  - **藍幀（第 1 幀）** ⇒ 自動複製到所有奇數幀（1、3、5、7…）
  - 提升動態影格數計算精準度，可依所選影片時間精準調整複製範圍
  - 使用者可以根據需要開啟/關閉複製功能
- **提升複製過程安全性**：
  - 強化幀邊界檢查，防止複製到無效位置
  - 詳細的日誌輸出使複製操作更易於追蹤

### 2025-04-27：版本 1.6.2
- **新增 MP4 壓縮設定**：*與原版合併
  - 可調式影片檔案大小與畫質之間的平衡
  - 可在範圍為 0 到 100（0 = 無壓縮，16 = 默認，更高值 = 高壓縮率，低質量）
  - 提供最佳設定以解決黑屏問題
- **提升程式碼品質**：
  - 將 UI 樣式定義分離為 `ui_styles.py`，以提高可維護性和可讀性
  - 透過專注於管理 CSS 樣式，提高 UI 一致性
- **微調幀大小計算**：
  - 提升 0.5 秒模式下的運算精度（使用 `latent_window_size=4.5`）
  - 提升分段數和視訊時長的計算精度，使視訊生成更穩定

### 2025-04-26：版本 1.6.1
- **擴展短視訊模式**：
  - 2 秒模式：60 幀（2 秒 x 30 FPS），2 個分段，無需複製
  - 3 秒模式：90 幀（3 秒 x 30 FPS）， 3 個部分，將關鍵影格 0 複製到 1
  - 4 秒模式：120 幀（4 秒 x 30 FPS），4 個部分，將關鍵影格 0 複製到 1、2
- **回歸 v1.5.1 的基本結構**：
  - 保留原有模式名稱符號（附括號）
  - 恢復關鍵影格指南 HTML
  - 保留原有函數結構和處理方式

### 2025-04-26：版本 1.6.0 *已否決版本
- **UI/UX 改進**：
  - 將部分設定拆分為折疊面板，以便僅在必要時展開
  - 簡化視訊模式名稱（例如「10（5x2）秒」→「10秒」）
  - 移除關鍵影格高亮
  - 將不必要的功能（結束影格影響調整、關鍵影格自動複製功能）變更為內部設置
- **技術改進**：
  - 更改了 VRAM 管理的標準值（60GB → 100GB）
  - 改進了分段計算邏輯（增加了直接從秒數計算的功能）
  - 提高了幀數和分段數的一致性（確保與顯示秒數一致）
  - 優化了調試輸出

### 2025-04-25：版本 1.5.1
- **新增「1 秒」短影片產生模式**：
- 支援 1 秒（約 30 幀，30fps）
- **更改預設影片時長**：
- 將預設值從“6 秒”更改為“1 秒”
- **優化輸入影像複製操作**：
- 在普通模式下停止從輸入影像複製
- 循環模式下啟用僅複製到最後一個影像
- **更改關鍵影格自動複製功能的預設值**：
- 預設關閉，以便更精細地控制
- 必要時可開啟自動複製功能
- **提升影像處理穩定性**：
- 改進了按下「開始」按鈕時重新獲取影像的正確方法
- 新增了預覽影像的明確清除流程

### 2025-04-24：版本 1.5.0
- **新增幀大小設定**：
- 可在 0.5 秒模式和 1 秒模式之間切換
- 根據幀大小動態調整 latent_window_size

### 2025-04-24：版本 1.4.0
- **新增所有填滿功能**：
- 所有部分使用相同的填充值
- 此值越小，單次會話中的運動越劇烈。

### 2025-04-24：版本 1.3.3
- **重新審視 LoRA 應用功能**：
- 直接 LoRA 載入模式已被否決，因為它需要金鑰匹配才能設定參數。統一為 DynamicSwap，並等待後續情況。
- 實現了獲取參數數量的日誌顯示。

### 2025-04-24：版本 1.3.2
- **統一 LoRA 應用功能**：
- 統一在低 VRAM 模式下直接套用 LoRA（DynamicSwap）的方式，與在高 VRAM 模式下相同。
- 廢除了 hook 方法，僅支援更穩定的直接應用方式。
- 改進了內部實現，同時保持了介面的兼容性。
- **增強了調試和驗證功能**：
- 新增了用於檢查 LoRA 應用程式狀態的專用實用程式 (lora_check_helper.py)
- 提供詳細的日誌輸出和偵錯資訊。

### 2025-04-24：版本 1.3.1
- **程式碼庫重構**：將程式碼組織成多個模組，以提高可維護性和可擴展性
- `eichi_utils`：管理關鍵影格處理、設定管理、預設管理和視訊模式設定
- `lora_utils`：聚合 LoRA 相關函數

### 2025-04-23：版本 1.3
- **[研究中] 新增混元 LoRA 支援**：自訂模型並新增自訂表情
- **[測試實作] 新增 EndFrame 影響度設定**：最終影格的影響度可在 0.01 至 1.00 之間調整（nirvash 已知）

### 2025-04-23：版本 1.2
- **新增「20 (4x5) 秒」模式**：支援產生包含 5 個部分的長視頻
- **新增每個部分的提示功能**：允許為每個部分設定單獨的提示 [測試實作]
- **增強輸出資料夾管理功能**：支援指定輸出資料夾和獨立於作業系統的開啟方式
- **改進設定檔管理**：使用基於 JSON 的設定檔持久化設定
- **增強跨平台支援**：改進了在 Windows 以外環境下的操作

### 2025-04-22：版本 1.1
- **新增「16（4x4）秒」模式**：支援由 4 個部分組成的長視頻
- **改進了生成過程中的進度顯示**：現在會顯示部分資訊（例如「部分：3/15」），讓您更容易了解進度，尤其是在生成長影片時
- **設定檔結構**：視訊模式設定現在被拆分到單獨的檔案中，提高了可擴展性

### 2025-04-21：首次發布
- 優化提示管理功能
- 新增關鍵影格引導功能

---

**FramePack-eichi** - 端幀圖片連結口
旨在實現更直覺、更靈活的影片生成
