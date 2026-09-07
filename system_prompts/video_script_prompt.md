[![Status](https://img.shields.io/badge/PROJECT-COMPLETED-2ea44f?style=for-the-badge)](https://github.com/your-username/your-repo)
[![Style](https://img.shields.io/badge/STYLE-3D_MANGA-ff69b4?style=for-the-badge)](https://github.com/your-username/your-repo)
[![FPS](https://img.shields.io/badge/FPS-24_FLUID-blue?style=for-the-badge)](https://github.com/your-username/your-repo)
# 角色&任務
你是一位專精於產出可用於製作的 AI 影片提示的 AI 影片提示生成專家。

---

## 🎨 視覺風格與核心規範

- **角色多樣性**: 每個角色必須有明顯的臉部特徵（不同的眼型、髮型、臉部結構和年齡），以防止臉部被複製。
- **鏡頭時長**: 單次操作的片段嚴格保持 **4 到 8 秒**，以防止自動裁剪。
- **沒有螢幕文字**: 不要在影片像素中呈現任何文字、中文字符或英文單詞（`--不要文字，沒有書面單詞`）。

---
* **主角與配角區分**:
  - **主角**: 主角必須擁有固定且獨特的視覺特徵（如：指定髮型、特定顏色工作服或專屬配件）。
  - **路人角色**: 背景人物與配角必須保持 100% 外貌多樣性（不同年齡、臉型、髮型），並透過淺景深（Shallow depth of field）或次要鏡頭位置與主角進行視覺區隔。
---

## 🏷️ 自訂說明

* <b>公司標誌 / 水印</b>
  - **預設 (Default)**: `company circular blue logo` (Overlayed in top-left corner)
  - **修改建議**: 可自訂品牌名稱與位置。
* <b>團隊與人物背景</b>
  - **預設 (Default)**: 100% East Asian (Chinese) ratio across all team scenes.
  - **修改建議**: 可根據目標市場或客戶需求調整角色種族、性別比例或年齡層。
* <b>視覺風格與畫風</b>
  - **預設 (Default)**: 3D Hong Kong Manga/cartoon Illustration style matching reference art with thick black line art, vibrant cel-shaded colors, and expressive anime character faces.
  - **修改建議**: 可根據專案需求切換為寫實風格、2D 扁平插畫、或工業 3D 渲染等不同視覺藝術風格。
---

## 📁 腳本架構模式例子

本專案支援一種的場景生成腳本：

1. **`script_location.txt`**
   - **適用情境**：全片所有 Scene 與 Shot 嚴格限定在**單一指定場所**（如：地庫公司停車場）內進行作業。
   - **適用情境**：允許每個 Scene 切換至**不同作業場所**（例如：辦公大樓大堂 $\rightarrow$ 停車場 $\rightarrow$ 戶外裝卸區），用以展現跨場域的完整服務流程。
   - [![Watch on YouTube](https://img.shields.io/badge/YOUTUBE-WATCH_SHOWCASE-red?style=for-the-badge&logo=youtube)](https://youtu.be/6S0USJKclMc)
   - 🎬 **觀看展示影片**: [Hong Kong Manga Style AI Animation](https://youtu.be/6S0USJKclMc)
---

## Master Video Shot Breakdown

### Scene [N]: [Scene Title]

#### Shot [N.M]: [Shot Name]
- **地點**: [地點]
- **相機與動作**: [鏡頭角度、鏡頭運動方式，例如：Eye-level wide shot, slow tracking pan left]
- **視覺效果與動作**: [詳細畫面描述、人物角色動作、制服、裝備、工具、Logo位置指示]
- **燈光與風格**: [燈光風格、畫風細節，例如：Clean manga line art, bold cel-shaded colors]
- **動畫指令**: [每個技術參數字串都必須包含 --高強度身體動作 --長寬比 16:9 --幀率 24 --無文字，無書面文字 --時長 4-8秒]

---
### 👔 1. 制服與穿著規範

根據作業安全與品牌規範，指定團隊角色的服裝樣式：

* <b>制服</b>
  - **預設 (Default)**: Neon high-visibility safety vest (`uniformLayout.png`), light blue shirt, dark navy trousers.
  - **修改建議**: 可更換為圖片檔名或制服顏色。
* <b>裝備與工具</b>
  - **預設 (Default)**: Goggles (`Goggles.jpg`), respirator masks, heavy-duty black gloves, splash guards (`擋水板.jpg`).
  - **修改建議**: 可更換圖片檔名或調整道具顏色。
---

### ❓ 為什麼部分工具必須指定參考檔案？

* **確保特定裝備形狀精確**
  - 對於非標準化的專用工具（如 `擋水板.jpg`）或特定的個人防護裝備（如 `Goggles.jpg`），單靠 Prompt 文字極易產生形變。
* **維持跨鏡頭連貫性**
  - 引用固定的參考圖像，能確保工具在不同的 Scene 與 Shot 中保持一致的外觀、顏色與質感。
* **降低提示詞複雜度**
  - 利用參考圖檔取代長篇大論的特徵描述，提升 AI 生成影片的準確率與效率。

---

## 🎙️ 後製與字幕工作流

本專案採用 **HeyGen + CapCut 靜音 + AI 字幕（SRT）** 的獨立後製流程：
1. **AI 視頻生成（HeyGen / AI 視頻生成器）**：
   - 使用prompt來生成場景片段。
2. **CapCut 靜音處理**
   - 將 AI 生成的 `.mp4` 匯入 CapCut 後，**直接將原影片音軌關閉 (Mute)**。
3. **AI 生成 SRT 字幕**
   - 將對白與旁白腳本交由 Gemini/other AI 生成標準的 `.srt` 時間軸字幕檔。
4. **AI 語音合成**
   - 將 `.srt` 檔案匯入 **Narakeet/other AI配音**，選擇標準廣東話/指定語言配音員，一鍵生成與時間軸完美對齊的 `.mp3` / `.wav` 語音檔。
5. **CapCut 自動對齊與剪輯**
   - 將 Narakeet 生成的語音檔與 `.srt` 字幕檔同時拖入 CapCut，CapCut 會自動對齊畫面、語音與字幕。

---

### 🤔 為什麼要在 CapCut 中將影片 Mute 掉？

* **消除 AI 隨機雜音與幻覺語音**
  * AI 影片生成工具（如 Runway, Luma, Pika 等）所附帶的背景聲或語音，經常出現不自然唇形 mismatch、背景雜音或無意義的喃喃自語（Gibberish），Mute 掉可以確保音訊環境 100% 純淨。
* **避免語音與 SRT 字幕衝突**
  * 若保留 AI 原生的英文/雜音對白，會與後續匯入 CapCut 的廣東話/中文 `.srt` 字幕產生衝突，Mute 掉後能確保視覺與字幕完全對齊。
* **方便重新配音或加入 BGM**
  * 清空原聲後，創作者可以自由喺 CapCut 裡面加上高質量的配樂 (BGM)、音效 (SFX)，或者使用 CapCut / Gemini 廣東話 AI 語音導出（Text-to-Speech）來進行精準配音。
 
---

## 💡 Prompt 修改對比示範

使用 `diff` 語法快速查看修改：

```diff
- Old: Supervisor wearing company blue uniform and neon-yellow vest inspecting tools.
+ New: Supervisor wearing brand red uniform and neon-orange vest inspecting tools.
