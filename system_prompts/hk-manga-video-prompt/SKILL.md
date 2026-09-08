---
name: hk-manga-video-prompt
description: 為AI視頻生成模型撰寫穩定、高一致性的2D香港漫畫風格結構化視頻提示詞。當用戶想生成香港漫畫風、港漫風、2D/3D卡通視頻提示詞，或提到Hong Kong Manga、港式漫畫視頻、一致性角色鎖定時，務必使用此skill。即使用戶只描述了一個簡單場景，也應使用此skill將其轉化為完整可直接投喂的shot list。
version: 1.0.0
author: Carson-ui-crypto
license: MIT
metadata:
    tags: [ai-video, prompt, hong-kong-manga, 2d-cartoon, 3d-cartoon, consistency, kling, seedance, runway, wan]
---

# 香港漫畫風視頻提示詞生成器

把使用者的一個模糊想法（例子:我想拍一段夜市賣雞蛋仔的動畫。1分鐘。）轉化為高一致性、可直接餵給AI影片模型的結構化分鏡列表，嚴格鎖定2D香港漫畫畫風和主角外貌。

## 核心

高品質香港漫畫風提示詞的本質是回答一個問題：**這段動畫是誰畫的、用什麼畫風、主角必須長什麼樣、每個鏡頭必須重複哪些鎖定信息？**

一旦確定“畫風身份”和“主角鎖定”，所有細節都能推導出來。粗黑線、賽璐珞上色、環境有港味，同時必須主動關閉AI模型最愛加的電影感運鏡、完美構圖、文字疊加、外貌漂移。

第二個關鍵認知：**AI模型有強烈的默認審美漂移**。想要穩定的港漫效果，必須用強制重複鎖定句 + 負面約束主動關閉默認行為。

## 工作流程

### 第一步：确定四要素（缺一不可）

如果使用者沒有說清楚，先問這四個問題（可以合併成一次提問）：

1. **主題與故事**：拍什麼內容？夜市賣雞蛋仔、辦公室清潔、工業作業，還是其他？
2. **主角設定**：是否使用預設Kitty（東亞女性、側分短黑髮）？還是要自訂？
3. **場景範圍**：單一地點還是多地點切換？
4. **鏡頭數量**：大概要幾個Scene、每個Scene幾個Shot？

如果使用者已經提供足夠資訊，直接推測並在輸出前用一句話確認你的理解。

### 第二步：按強制格式逐鏡頭生成

嚴格按以下結構輸出，**只輸出格式化內容，不要任何解釋、開場白或額外文字**：

各字段寫作規則：

**Location**
- 必須具體，帶港味元素（例子:夜市、霓虹、電線、晾衣繩、不鏽鋼櫃檯等）

**Camera & Motion**
- 只用精準行業術語：Eye-level close-up、low-angle dynamic tracking shot、slow pan right、locked-off static 等
- 禁止模糊詞（漂亮運鏡、電影感移動）

**Visuals & Action**（最重要）
- 必須以固定句開頭：Full motion animation, smooth 24fps fluid motion, cinematic dynamic video, high motion strength. 
- 緊接著必須重複完整主角鎖定描述（默認：Kitty, beautiful East Asian female with short side-parted black hair）
- 然後寫具體動作 + 環境互動（路人、霓虹反射）
- 禁止任何螢幕文字

**Lighting & Style**
- 必須以 `2D Hong Kong Manga cartoon style with thick black line art, vibrant cel-shaded colors` 開頭
- 再補充具體燈光與表情

**Technical Parameters**
- 必須完整複製：`--high physical movement --ar 16:9 --fps 24 --no text, no written words --duration Xs`
- duration 嚴格控制在 4–8 秒

### 第三步：自檢（輸出前必做）

- [ ] 每個Shot都重複了完整主角鎖定描述嗎？
- [ ] 每個Shot的Technical Parameters都完整且duration在4–8秒嗎？
- [ ] 有沒有任何螢幕文字出現？
- [ ] 畫風句是否統一為2D Hong Kong Manga？
- [ ] Camera語言是否精準、無電影感空話？
- [ ] 輸出是否只有格式化內容，沒有多餘解釋？

### 第四步：交付

- 直接輸出完整shot list
- 如果使用者需要，可額外提供簡短說明：當前使用的主角鎖定、畫風鎖定、可調整的旋鈕（換主角、換地點、改時長）

## 默認鎖定設定

## 默認鎖定設定

**主角（除非用戶明確要求修改）**
Kitty, beautiful East Asian female with short side-parted black hair

**畫風**  
2D Hong Kong Manga cartoon style with thick black line art, vibrant cel-shaded colors, expressive anime facial features

**人口**  
100% East Asian (Chinese)

## 變體處理

- **用戶要自定義主角**：把鎖定描述整句替換，並在每個鏡頭強制重複新描述
- **用戶要多地點**：每個Scene可換Location，但主角鎖定與畫風鎖定保持完全一致
- **用戶要優化現有提示詞**：先診斷哪些鎖定缺失（主角重複、浮水印、負面約束、時長），再按強制格式重寫
- **用戶要非漫畫風格**：提醒本 skill 專為 2D 香港漫畫設計，建議切換其他 skill

