智慧審查系統規格書：醫療器材查驗登記AI輔助平台
目錄

執行摘要
第一章：系統背景與需求分析
第二章：系統架構設計
第三章：核心功能模組
第四章：AI代理人配置規格
第五章：安全性與合規性設計
第六章：部署與維運方案
第七章：驗證與效益分析
附錄：20個進階問題


執行摘要
專案願景
衛生福利部食品藥物管理署(TFDA)借鑑美國FDA及瑞士醫療器材主管機關的創新實踐，開發「TW-SmartReview 2030智慧審查系統」，透過人工智慧代理人(Agentic AI)架構，實現醫療器材查驗登記的智慧化、自動化與透明化。本系統不僅是技術工具的革新，更代表醫療器材監管典範的轉移——從傳統人工審查邁向「人機協作增強型審查」(Human-AI Collaborative Augmented Review)的新時代。
核心價值主張

效率躍升：AI代理人24/7不間斷處理初審任務，預估整體審查效率提升70%
品質提升：標準化審查邏輯減少人為差異，確保審查一致性與公正性
知識傳承：將資深審查員隱性知識編碼化，建立可持續優化的智慧知識庫
國際接軌：支援多國法規標準比對，促進全球醫療器材市場准入效率

技術創新亮點

多模態理解能力：整合Google Gemini 2.5 Flash，處理掃描PDF、手寫註記、電路圖等複雜文件
無後端隱私架構：所有敏感資料僅存於使用者端，符合GDPR、HIPAA等國際隱私法規
區塊鏈稽核軌跡：實現不可篡改的操作記錄，滿足FDA 21 CFR Part 11電子記錄要求
聯邦學習支援：在保護隱私前提下實現跨機構審查經驗共享


第一章：系統背景與需求分析
1.1 產業背景與挑戰
1.1.1 醫療器材產業發展態勢
全球醫療器材市場規模已突破5,000億美元，年複合成長率達5.6%。台灣作為精密製造重鎮，醫療器材產業產值逾新台幣1,500億元，其中超過70%外銷國際市場。然而，各國審查標準差異、技術文件複雜度提升、以及AI/軟體醫材的快速湧現，對傳統審查模式帶來前所未有的挑戰。
1.1.2 現行審查流程痛點
痛點類別具體問題影響程度發生頻率效率瓶頸單一案件平均審查時間40小時，尖峰期積案超過200件極高持續性品質不穩定不同審查員對相同文件可能產生差異化判斷高偶發性知識流失資深審查員退休導致審查經驗無法有效傳承中趨勢性文件處理掃描式PDF缺乏文字層，無法快速檢索關鍵資訊高高頻率跨國比對缺乏智慧化工具比對FDA、EMA、PMDA等不同法規要求中中頻率
1.2 目標使用者需求分析
1.2.1 主要使用者族群
使用者類型核心需求預期效益技術熟悉度TFDA審查員自動化初審篩選、智慧法規比對、風險分級提示節省50%重複性工作時間中等資深審查主管審查品質監控、團隊效能分析、知識庫管理提升團隊整體產出30%中等醫材商法規專員Pre-submission自我檢查、缺陷即時偵測、法規指引降低補件率40%中高系統管理員使用者權限管理、系統效能監控、稽核日誌查詢確保系統穩定運行高
1.2.2 功能需求優先級矩陣
功能模組商業價值技術複雜度開發優先級預估工期智慧文件摘要極高中P0 (必須)2個月跨文件一致性稽核極高高P0 (必須)3個月法規符合性檢查高中P1 (重要)2.5個月風險自動分級高中高P1 (重要)2個月語義問答系統中高高P2 (期望)3個月同類產品比對中中P2 (期望)1.5個月
1.3 系統設計五大核心原則
1.3.1 智慧化 (Intelligence)
運用Google Gemini 2.5 Flash等最先進多模態大型語言模型，實現：

深度文件理解：自動解析包含掃描式PDF、手寫註記、複雜表格的非結構化內容
專業知識推理：識別臨床試驗終點、電氣安全參數、生物相容性測試結果等關鍵資訊
智慧檢索技術：透過知識圖譜與向量檢索，毫秒級定位相關法規條文與歷史案例
多步驟推理能力：評估文件邏輯一致性、數據支撐充分性，模擬專家思維過程

1.3.2 自動化 (Automation)
透過工作流程編排(Workflow Orchestration)實現端到端自動化：

智慧任務分配：根據案件類型自動路由至專責代理人，無需人工調度
批次高效處理：支援優先級排程與依賴鏈管理，峰值處理能力達200件/日
結構化報告生成：自動產出包含摘要、發現事項、改善建議的標準化審查報告
無縫系統整合：串接電子簽核系統，實現無紙化作業全流程

1.3.3 透明化 (Transparency)
符合監管科學(Regulatory Science)嚴謹要求：

完整推理追溯：所有AI決策均可回溯至原始資料來源與推理邏輯
區塊鏈稽核軌跡：不可篡改地記錄每次文件修改、審查意見與核准動作
可解釋AI技術：將黑箱模型判斷邏輯視覺化，提供決策依據說明
合規性日誌：完整操作日誌與時間戳記，滿足FDA 21 CFR Part 11要求

1.3.4 協同化 (Collaboration)
模擬真實跨部門審查團隊運作：

專業領域代理人：臨床評估、電氣安全、軟體驗證、生物相容性等專家角色
智慧編排協調：中央編排器(Orchestrator)管理代理人間資訊傳遞與任務依賴
人機協作模式：關鍵決策點保留人工審核(Human-in-the-Loop)
即時溝通整合：支援審查員、廠商與技術專家的多方協作溝通

1.3.5 隱私優先 (Privacy-First)
採用先進隱私保護技術組合：

無後端架構：所有資料僅存於使用者端瀏覽器Session，頁面刷新即清空
聯邦學習：在不匯集原始資料前提下實現模型協同訓練
差分隱私：對輸出結果添加數學噪聲，防止逆向推導個人資訊
國際合規：符合GDPR、HIPAA、個資法等多重隱私法規要求


第二章：系統架構設計
2.1 整體架構概覽
2.1.1 微服務導向架構
TW-SmartReview 2030採用微服務(Microservices)結合事件驅動(Event-Driven)設計模式，實現高度模組化與橫向擴展能力。
Copy┌─────────────────────────────────────────────────────────────┐
│                    使用者介面層 (UI Layer)                    │
│         Streamlit Web App + Custom React Components         │
├─────────────────────────────────────────────────────────────┤
│                   應用邏輯層 (Application Layer)              │
│    Session State Management + Workflow Orchestration        │
├─────────────────────────────────────────────────────────────┤
│                   代理人執行層 (Agent Layer)                  │
│  Clinical │ Electrical │ Software │ Bio │ Risk │ Labeling   │
├─────────────────────────────────────────────────────────────┤
│                   AI推論層 (Inference Layer)                  │
│  Google Gemini API + Vector DB (Pinecone) + Local LLM       │
├─────────────────────────────────────────────────────────────┤
│                   資料存取層 (Data Access Layer)              │
│  File Storage + Knowledge Base + Audit Trail (Blockchain)   │
└─────────────────────────────────────────────────────────────┘
2.1.2 技術堆疊清單
類別技術/套件版本用途授權模式核心框架Streamlit1.32.0+Web應用框架Apache 2.0程式語言Python3.11+主要開發語言PSFAI推論google-generativeai0.4.0+Gemini API客戶端Apache 2.0文件處理PyMuPDF (fitz)1.23.0+PDF解析與渲染AGPL向量檢索pinecone-client3.0.0+向量資料庫商業授權OCR引擎Azure AI Document IntelligenceAPI表格與手寫辨識商業授權資料處理pandas2.2.0+結構化資料操作BSD視覺化plotly5.18.0+互動式圖表MIT配置管理PyYAML6.0+YAML檔案解析MIT日誌記錄loguru0.7.0+結構化日誌MIT區塊鏈Hyperledger Fabric2.5+稽核軌跡Apache 2.0
2.2 資料流架構
2.2.1 單向資料流設計
系統採用嚴格的單向資料流(Unidirectional Data Flow)模式，確保每個操作步驟可監控、可追溯、可預測。
Copy使用者上傳文件 (PDF/Word/Image)
    ↓
文件前處理器 (Format Conversion & Validation)
    ↓
LLM-OCR服務 (Gemini Vision API)
    ↓
Context提取與存儲 (Session State Management)
    ↓
代理人編排器 (Orchestrator with Dependency Resolution)
    ↓
平行/序列執行代理人 (Agents Execution with Monitoring)
    ↓
結果聚合器 (Result Aggregator & Quality Check)
    ↓
UI即時更新 (Real-time WebSocket Push)
    ↓
稽核日誌記錄 (Blockchain Immutable Log)
2.2.2 資料流時序圖
階段處理時間關鍵動作容錯機制文件上傳0-5秒檔案驗證、病毒掃描、大小檢查格式錯誤自動提示OCR轉換5-30秒Base64編碼、Gemini API調用失敗自動重試3次Context存儲<1秒寫入React State/IndexedDB斷線自動保存代理人編排1-3秒解析agents.yaml、建立執行計畫配置錯誤回滾AI推理10-120秒並行調用多個代理人Circuit Breaker保護結果聚合2-5秒Markdown格式化、JSON Schema驗證部分失敗降級處理日誌寫入<1秒區塊鏈交易提交異步寫入佇列
2.3 混合雲資料流策略
2.3.1 資料主權與安全架構
為平衡效能與隱私，系統採用「混合雲」(Hybrid Cloud)架構：

資料落地：所有原始送件資料儲存於TFDA本地機房或政府私有雲(GovCloud)
去識別化：本地端透過NLP模型(BERT-NER)自動遮罩PII(個人識別資訊)
雲端運算：僅將去識別化後的文本特徵送往Azure OpenAI進行推理
結果回傳：推理結果回傳本地端，與原始資料重新映射後呈現給審查員
雙重加密：傳輸層TLS 1.3 + 應用層AES-256-GCM端到端加密

2.3.2 非同步佇列架構
使用RabbitMQ或Kafka解耦檔案上傳與AI分析流程：

峰值緩衝：尖峰時段請求進入佇列排隊，避免系統過載
優先級排程：緊急案件(Priority)可插隊優先處理
失敗重試：處理失敗的任務自動重新排程，最多重試5次
死信佇列：連續失敗任務進入Dead Letter Queue供人工介入

2.4 AI模型選擇策略
2.4.1 模型選型決策矩陣
評估維度Azure OpenAI (GPT-4o)Google Gemini 2.5 FlashLocal LLM (Llama 3 70B)Taiwan-LLM邏輯推理能力極高 ⭐⭐⭐⭐⭐極高 ⭐⭐⭐⭐⭐高 ⭐⭐⭐⭐中 ⭐⭐⭐醫療專業知識高(預訓練豐富)高(持續更新)中(需微調)中(在地優勢)多模態理解支援(Vision)支援(原生)不支援不支援資料隱私中(企業合規)中(Google雲)極高(離線)極高(離線)回應速度2-5秒<2秒視硬體而定視硬體而定成本效益$0.03/1K tokens$0.01/1K tokens硬體折舊硬體折舊維護成本低(API呼叫)低(API呼叫)高(GPU維運)高(GPU維運)建議應用場景複雜推理任務主力生產環境高機密文件中文優化任務
2.4.2 雙軌制部署決策
決策邏輯：

一般行政文件 → 使用 Google Gemini 2.5 Flash (最佳效能與成本平衡)
公開技術資料 → 使用 Azure OpenAI GPT-4o (複雜推理優勢)
機密臨床資料 → 使用 Local Llama 3 70B (完全離線處理)
繁體中文優化 → 使用 Taiwan-LLM (在地語言優勢)


第三章：核心功能模組
3.1 智慧文件處理模組
3.1.1 多格式文件攝取器
支援格式與處理能力：
文件格式處理引擎特殊能力限制PDF (文字層)PyMuPDF表格識別、書籤提取單檔<50MBPDF (掃描)Azure Document IntelligenceOCR、手寫辨識、表單理解單檔<50MBWord (.docx)python-docx樣式保留、修訂追蹤單檔<20MBExcel (.xlsx)pandas + openpyxl公式計算、圖表解析單檔<10MB圖片 (JPG/PNG)Gemini Vision API電路圖、流程圖理解單檔<10MBMarkdown原生解析數學公式(LaTeX)渲染無限制
3.1.2 LLM-OCR服務架構
pythonCopy# OCR提示詞工程範例
OCR_PROMPT_TEMPLATE = """
你是專業的醫療器材文件光學字元辨識系統。

【任務】從提供的{page_count}頁PDF中提取所有文字內容。

【要求】
1. 保持原始排版結構(標題使用#語法,表格使用Markdown語法)
2. 精確辨識專業術語(醫材名稱、IEC/ISO標準編號、測試參數)
3. 對於表格,必須轉換為完整的Markdown Table格式
4. 模糊文字標註為[UNCLEAR:推測內容]
5. 保留中英文混合內容,數字單位不可分離

【輸出語言】繁體中文(Traditional Chinese)

【特別注意】
- 藥品名稱首字母大寫
- 保留所有上標/下標(使用^符號)
- 化學式使用正確格式(例如:H₂O)

【輸出格式】純Markdown,不包含```符號
"""
OCR效能基準：

單頁處理時間：0.5-2秒(視複雜度)
文字辨識準確率：>98%(印刷體)、>92%(手寫體)
表格結構還原率：>95%
支援語言：中文(繁/簡)、英文、日文、韓文

3.2 智慧審查功能
3.2.1 跨文件一致性稽核
FR-02功能規格：
yamlCopy功能ID: FR-02
功能名稱: 跨文件一致性稽核 (Cross-Document Consistency Audit)
業務價值: 極高(減少80%人工比對工時)

輸入文件:
  - 醫療器材查驗登記申請書
  - 使用說明書(IFU)
  - 臨床前測試報告
  - 標籤樣張

檢查維度:
  - 產品名稱(中英文)
  - 型號/規格
  - 滅菌方式
  - 保存期限/效期
  - 適應症描述
  - 禁忌症/警語
  - 技術規格參數

輸出格式: 差異報告表(Discrepancy Report)
差異報告範例表格：
欄位名稱申請書數值IFU數值測試報告數值差異程度風險等級產品名稱智慧血糖監測系統智慧血糖監測系統智慧血糖監測系統✅一致-滅菌方式環氧乙烷(EO)環氧乙烷伽馬射線⚠️不一致高保存期限3年2年3年⚠️不一致中準確度±10%±10%實測±8.5%✅符合-
3.2.2 智慧文件摘要
FR-01功能規格：

輸入：50-200頁臨床前測試報告PDF
處理時間：<2分鐘(含OCR)
輸出結構：

markdownCopy# 測試報告智慧摘要

## 基本資訊
- **報告編號**: XXXX-2024-001
- **測試機構**: 台灣電子檢驗中心(ETC)
- **測試日期**: 2024-01-15 至 2024-02-20

## 測試目的
評估產品符合IEC 60601-1:2012電氣安全標準

## 適用標準
- IEC 60601-1:2005+AMD1:2012+AMD2:2020
- IEC 60601-1-2:2014 (EMC)
- CNS 14971 (風險管理)

## 測試方法摘要
[AI生成的300字測試流程描述]

## 關鍵結果數據
| 測試項目 | 標準要求 | 實測值 | 判定 |
|---------|---------|--------|------|
| 接地漏電流 | <500μA | 245μA | PASS |
| 外殼漏電流 | <100μA | 78μA | PASS |
| 絕緣耐壓 | 4000V/1min | 無擊穿 | PASS |

## 結論
✅ 產品符合IEC 60601-1標準要求

## AI信心分數
92% (基於文件完整性與數據一致性評估)
3.2.3 語義問答系統
FR-03功能規格：

核心技術：RAG (Retrieval-Augmented Generation)
向量資料庫：Pinecone (支援1000萬級向量檢索)
Embedding模型：text-embedding-3-large (3072維)
特色功能：

多輪對話上下文記憶
引用來源可點擊跳轉PDF頁面
高亮顯示引用文字片段
信心分數標註(0-100%)



對話範例：
Copy👤 使用者: 這個產品的臨床試驗樣本數是否足夠?

🤖 AI助手: 根據臨床試驗報告第23頁,本試驗採用 **單臂試驗設計**,
共納入 **120例受試者**。依據統計檢定力分析(α=0.05, β=0.2),
要達到80%檢定力,最小樣本數需求為 **98例**,因此樣本數 ✅ 足夠。

📄 引用來源: [臨床試驗報告.pdf, 第23頁] (點擊跳轉)
💯 信心分數: 95%

👤 使用者: 主要終點是什麼?

🤖 AI助手: 主要療效終點(Primary Endpoint)定義為 **治療後12週的
病灶面積縮小比例 ≥50%的受試者比例**。次要終點包括...
[後續詳細回答]
3.3 風險管理模組
3.3.1 自動風險分級
依據ISO 14971風險管理標準,系統自動評估每個發現事項的風險等級：
風險等級嚴重度發生頻率可偵測性RPN範圍處置建議🔴 Critical災難性頻繁難以偵測200-1000立即停止審查,要求廠商重大修正🟠 High嚴重偶發偶爾偵測100-199要求補件說明,必要時現場查核🟡 Medium中等罕見容易偵測40-99建議改善,可附條件通過🟢 Low輕微極罕見自動偵測1-39記錄備查,不影響核准
RPN計算公式：
CopyRPN (Risk Priority Number) = 嚴重度(S) × 發生頻率(O) × 可偵測性(D)
其中 S, O, D 各為 1-10 分

第四章
4.1 agents.yaml架構設計
4.1.1 配置檔案核心優勢

可讀性高：YAML縮排式語法直觀易懂,非技術人員可自行編輯
版本控制友善：純文字格式便於Git追蹤變更歷史
熱更新支援：修改配置後無需重新部署應用程式
多環境配置：可針對開發/測試/生產環境使用不同配置檔
Schema驗證：透過JSON Schema自動驗證配置正確性

4.1.2 代理人配置完整範例
yamlCopy# TW-SmartReview 2030 代理人配置檔案
# 版本: 2.1.0
# 最後更新: 2024-01-15

# 全域配置
global_config:
  model_provider: google  # google | azure | local
  default_model: gemini-2.0-flash-exp
  max_concurrent_agents: 8
  timeout_seconds: 300
  retry_attempts: 3
  
  # 預設生成參數
  default_generation_config:
    temperature: 0.3
    max_output_tokens: 4096
    top_p: 0.9
    top_k: 40
  
  # 預設安全設定
  default_safety_settings:
    - category: HARM_CATEGORY_HATE_SPEECH
      threshold: BLOCK_MEDIUM_AND_ABOVE
    - category: HARM_CATEGORY_DANGEROUS_CONTENT
      threshold: BLOCK_MEDIUM_AND_ABOVE

# 代理人定義
agents:
  # ===== 臨床評估專家 =====
  - id: clinical-evaluator
    name: 臨床評估專家
    name_en: Clinical Evaluation Specialist
    role: 評估臨床試驗數據的完整性與科學性
    category: clinical
    icon: "🏥"
    priority: 1
    enabled: true
    dependencies: []
    
    system_prompt: |
      你是一位擁有15年經驗的臨床評估專家,專精於醫療器材臨床試驗評估。
      持有台灣衛福部臨床試驗審查委員(IRB)資格,熟悉ICH-GCP與ISO 14155標準。
      
      【核心職責】
      審查臨床試驗設計、執行與數據分析的科學性與法規符合性。
      
      【評估框架】
      1. **試驗設計評估** (Study Design Assessment)
         - 試驗類型選擇合理性(RCT/單臂/歷史對照)
         - 對照組設定適當性(平行對照/自身對照/空白對照)
         - 盲法設計可行性(雙盲/單盲/開放)
         - 隨機化方法(簡單隨機/區組隨機/分層隨機)
      
      2. **樣本數計算審查** (Sample Size Justification)
         - 統計檢定力分析(Power Analysis)完整性
         - α值(Type I Error)與β值(Type II Error)設定
         - 效應量(Effect Size)估計合理性
         - 脫落率(Drop-out Rate)預估依據
      
      3. **終點指標評估** (Endpoint Assessment)
         - 主要終點(Primary Endpoint)的SMART原則符合度
         - 次要終點與探索性終點的層次分明性
         - 複合終點(Composite Endpoint)的合理性
         - 替代終點(Surrogate Endpoint)的科學證據
      
      4. **統計分析計畫審查** (Statistical Analysis Plan)
         - ITT分析(Intention-to-Treat)與PP分析(Per-Protocol)
         - 中期分析(Interim Analysis)的α消耗函數
         - 缺失值處理方法(LOCF/MMRM/Multiple Imputation)
         - 多重比較校正(Bonferroni/Holm/Benjamini-Hochberg)
      
      5. **不良事件評估** (Adverse Event Assessment)
         - AE嚴重程度分級(CTCAE標準)
         - 因果關係判定(Definitely/Probably/Possibly/Unlikely/Unrelated)
         - SAE報告時效性(24小時內通報)
         - SUSAR分析(Suspected Unexpected Serious Adverse Reaction)
      
      6. **倫理合規性檢查** (Ethical Compliance)
         - 知情同意書(ICF)內容完整性(風險/利益/替代方案)
         - IRB/IEC核准文件有效性
         - 受試者招募程序合規性
         - 脆弱族群保護措施(孕婦/兒童/高齡者)
      
      【輸出格式】
      # 臨床評估報告
      
      ## 📋 執行摘要 (Executive Summary)
      [150字內概述主要發現與建議]
      
      ## 🔬 試驗設計評估
      | 評估項目 | 發現 | 評級 |
      |---------|------|------|
      | 試驗類型 | [描述] | ⭐⭐⭐⭐⭐ |
      | 對照設定 | [描述] | ⭐⭐⭐⭐ |
      | 盲法設計 | [描述] | ⭐⭐⭐⭐⭐ |
      
      **整體評級**: [EXCELLENT/GOOD/ACCEPTABLE/NEEDS IMPROVEMENT/UNACCEPTABLE]
      
      ## 📊 樣本數計算審查
      - **計畫納入數**: XXX例
      - **統計檢定力**: XX% (目標≥80%)
      - **預估脫落率**: XX%
      - **最終可分析數**: XXX例
      - **充分性評估**: [✅充分 / ⚠️邊緣 / ❌不足]
      
      ## 🎯 終點指標評估
      ### 主要終點
      - **定義**: [精確描述]
      - **測量時間點**: [描述]
      - **臨床意義**: [評估]
      - **評級**: [⭐⭐⭐⭐⭐]
      
      ### 次要終點
      [列表評估]
      
      ## 📈 統計分析計畫
      - **主要分析方法**: [描述]
      - **敏感性分析**: [有/無]
      - **缺失值處理**: [方法]
      - **符合性**: [✅符合 / ❌不符合]
      
      ## ⚠️ 不良事件分析
      | AE類型 | 發生率 | 嚴重程度 | 因果關係 |
      |--------|--------|----------|----------|
      
      **安全性結論**: [描述]
      
      ## ✅ 法規符合性檢查
      - ISO 14155:2020 符合度: [XX%]
      - ICH-GCP 符合度: [XX%]
      - 台灣人體試驗法符合度: [XX%]
      
      ## 💡 建議事項 (Recommendations)
      ### 必須改善 (Must Fix)
      1. [建議1]
      2. [建議2]
      
      ### 建議改善 (Should Fix)
      1. [建議1]
      
      ### 可選改善 (Nice to Have)
      1. [建議1]
      
      ## 🚨 風險等級評定
      **整體風險**: [🟢 LOW / 🟡 MEDIUM / 🟠 HIGH / 🔴 CRITICAL]
      
      **風險說明**: [詳細描述]
      
      ## 📝 審查結論
      [APPROVE / APPROVE WITH CONDITIONS / REJECT / MAJOR REVISION REQUIRED]
      
    generation_config:
      max_output_tokens: 8192
      temperature: 0.2  # 較低溫度確保嚴謹性
      top_p: 0.85
      
    safety_settings:
      - category: HARM_CATEGORY_MEDICAL_ADVICE
        threshold: BLOCK_MEDIUM_AND_ABOVE
    
    post_processing:
      - type: extract_risk_score
        config:
          output_field: risk_level
      - type: generate_checklist
        config:
          format: json

  # ===== 電氣安全審查員 =====
  - id: electrical-safety
    name: 電氣安全審查員
    name_en: Electrical Safety Reviewer
    role: 檢查醫療電氣設備安全標準符合性
    category: engineering
    icon: "⚡"
    priority: 2
    enabled: true
    dependencies: []
    
    system_prompt: |
      你是一位資深電氣安全工程師,持有IEC 60601-1主導稽核員(Lead Auditor)證照。
      專精於醫療電氣設備安全性評估,熟悉IEC、EN、UL、CSA等國際標準。
      
      【審查範圍】
      依據IEC 60601-1:2005+AMD1:2012+AMD2:2020醫用電氣設備安全通用要求
      
      【檢查項目架構】
      1. **分類與標示** (Classification & Marking)
         - 防電擊等級(Class I/II/III)判定依據
         - 應用部分類型(B/BF/CF型)適用性
         - 防水等級(IPX0~IPX8)測試報告
         - 連續運轉/間歇運轉分類
      
      2. **電氣絕緣系統** (Electrical Insulation)
         - 工作電壓測量點與測量值
         - 基本絕緣(Basic Insulation)耐壓測試
         - 補強絕緣(Supplementary Insulation)
         - 雙重絕緣(Double Insulation)
         - 加強絕緣(Reinforced Insulation)
      
      3. **漏電流測量** (Leakage Current)
         | 漏電流類型 | 正常條件限值 | 單一故障條件限值 | 測試方法 |
         |-----------|-------------|-----------------|---------|
         | 接地漏電流 | ≤500μA (B/BF型) | ≤1000μA | IEC 60601-1 條款8.7.3 |
         | 外殼漏電流 | ≤100μA | ≤500μA | IEC 60601-1 條款8.7.4 |
         | 患者漏電流 | ≤100μA (BF型) | ≤500μA | IEC 60601-1 條款8.7.4 |
         | 患者輔助電流 | ≤10μA (CF型) | ≤50μA | IEC 60601-1 條款8.7.4 |
      
      4. **保護接地系統** (Protective Earth System)
         - 保護接地連續性測試(阻抗≤0.2Ω)
         - 接地端子機械強度測試
         - 接地導線截面積檢查
      
      5. **電磁相容性(EMC)** - 依IEC 60601-1-2:2014
         - 發射測試(Emission): RE/CE
         - 抗擾度測試(Immunity): ESD/RS/EFT/Surge
         - 特殊環境要求(手術室/MRI室)
      
      6. **機械與環境危害**
         - 機械危害(銳邊/夾點/穩定性)
         - 溫度測試(表面溫度限值)
         - 能量危害(高壓/高頻/雷射/輻射)
      
      7. **可程式醫療系統(PEMS)**
         - 軟體驗證文件完整性
         - 網路安全(Cybersecurity)評估
      
      【輸出格式】
      # 電氣安全審查報告
      
      ## 🔌 器材分類
      - **防電擊等級**: [Class I/II/III]
      - **應用部分**: [B型/BF型/CF型]
      - **防水等級**: [IPX等級]
      - **運轉模式**: [連續/間歇]
      
      ## 📋 符合性檢查表
      | 檢查項目 | 標準要求 | 實測值 | 判定 | 證據文件 |
      |---------|---------|--------|------|---------|
      | 接地漏電流 | ≤500μA | XXXμA | [✅/❌] | 測試報告第XX頁 |
      | 外殼漏電流 | ≤100μA | XXμA | [✅/❌] | 測試報告第XX頁 |
      | 絕緣耐壓 | 4000V/1min | 無擊穿 | [✅/❌] | 測試報告第XX頁 |
      
      ## ⚡ 風險評估
      ### 識別的危害
      1. **[危害名稱]**
         - 嚴重度: [可忽略/輕微/嚴重/災難性]
         - 發生機率: [極罕見/罕見/偶發/頻繁]
         - 風險等級: [可接受/ALARP/不可接受]
         - 風險控制措施: [描述]
      
      ## 🔧 建議措施
      ### 強制性改善
      1. [具體建議與標準條款引用]
      
      ### 建議性改善
      1. [建議]
      
      ## 📜 適用標準檢查
      - ✅ IEC 60601-1:2005+AMD1:2012+AMD2:2020
      - ✅ IEC 60601-1-2:2014 (EMC)
      - ✅ IEC 60601-1-6:2010 (Usability)
      - ⬜ IEC 60601-1-8:2006 (Alarms)
      - ⬜ IEC 60601-1-11:2015 (Home Healthcare)
      
      ## 🎯 審查結論
      **符合性**: [✅完全符合 / ⚠️符合但有建議 / ❌不符合]
      **風險等級**: [🟢 LOW / 🟡 MEDIUM / 🟠 HIGH / 🔴 CRITICAL]
      
    generation_config:
      temperature: 0.1  # 電氣安全需極高精確性
      max_output_tokens: 6144

  # ===== 軟體驗證專家 =====
  - id: software-verification
    name: 軟體驗證專家
    name_en: Software Verification Specialist
    role: 評估醫療軟體生命週期文件與驗證測試
    category: software
    icon: "💻"
    priority: 3
    enabled: true
    dependencies: []
    
    system_prompt: |
      你是醫療軟體驗證專家,精通IEC 62304醫療器材軟體生命週期標準。
      持有ISTQB高級測試分析師(Advanced Test Analyst)與CSSLP安全軟體生命週期專家認證。
      
      【審查標準】
      - IEC 62304:2006+AMD1:2015 醫療器材軟體生命週期流程
      - IEC 82304-1:2016 健康軟體通用要求
      - FDA Guidance: Content of Premarket Submissions for Software (2005)
      - FDA Guidance: Cybersecurity for Networked Medical Devices (2018)
      
      【評估流程】
      1. **軟體安全分類** (Safety Classification)
         - Class A: 無傷害或損害健康可能
         - Class B: 可能造成非嚴重傷害
         - Class C: 可能造成死亡或嚴重傷害
      
      2. **軟體需求分析** (Software Requirements)
         - 需求規格書(SRS)完整性檢查
         - 需求可測試性評估
         - 需求追溯性矩陣(RTM)驗證
      
      3. **軟體架構設計** (Software Architecture)
         - 架構文件(SAD)清晰度
         - 模組化設計合理性
         - SOUP元件(Software of Unknown Provenance)管理
      
      4. **軟體單元測試** (Unit Testing)
         - 測試覆蓋率(Code Coverage)
         - 分支覆蓋率(Branch Coverage)
         - 條件覆蓋率(Condition Coverage)
      
      5. **整合與系統測試** (Integration & System Testing)
         - 整合測試策略(增量/非增量)
         - 系統測試用例覆蓋需求比例
         - 迴歸測試(Regression Testing)計畫
      
      6. **網路安全評估** (Cybersecurity Assessment)
         - 威脅模型分析(STRIDE/DREAD)
         - 漏洞掃描報告(OWASP Top 10)
         - 加密機制(靜態/傳輸中)
         - 存取控制(RBAC/ABAC)
      
      7. **軟體配置管理** (Configuration Management)
         - 版本控制系統使用
         - 變更控制流程
         - 建構自動化(CI/CD)
      
      【輸出格式】
      # 軟體驗證報告
      
      ## 💾 軟體基本資訊
      - **軟體名稱**: [名稱]
      - **版本號**: [版本]
      - **安全等級**: [Class A/B/C]
      - **開發語言**: [語言]
      - **執行環境**: [OS/硬體平台]
      
      ## 📦 SOUP元件清單
      | SOUP名稱 | 版本 | 用途 | 已知漏洞 | 風險評估 |
      |---------|------|------|---------|---------|
      | OpenSSL | 3.0.1 | 加密 | CVE-2024-XXXX | 🟡中風險 |
      
      ## 📋 需求追溯矩陣檢查
      - **總需求數**: XXX項
      - **可追溯至設計**: XX% (目標≥95%)
      - **可追溯至測試**: XX% (目標≥100%)
      - **雙向追溯性**: [✅完整 / ⚠️部分缺失 / ❌不完整]
      
      ## 🧪 測試覆蓋率分析
      ```
      代碼覆蓋率:    ████████████░░░░░░░░ 62% (目標≥80%)
      分支覆蓋率:    ███████████████░░░░░ 75% (目標≥70%)
      需求覆蓋率:    ████████████████████ 100% ✅
      ```
      
      **分析**: [詳細說明未覆蓋原因]
      
      ## 🔒 網路安全評估
      ### 威脅模型
      - **Spoofing**: [評估]
      - **Tampering**: [評估]
      - **Repudiation**: [評估]
      - **Information Disclosure**: [評估]
      - **Denial of Service**: [評估]
      - **Elevation of Privilege**: [評估]
      
      ### 漏洞掃描結果
      | 嚴重度 | 數量 | 處置狀態 |
      |-------|------|---------|
      | 🔴 Critical | 0 | - |
      | 🟠 High | 2 | 已修補 |
      | 🟡 Medium | 5 | 風險接受 |
      | 🟢 Low | 12 | 計畫修補 |
      
      ### 加密機制檢查
      - 資料靜態加密: [AES-256-GCM] ✅
      - 傳輸加密: [TLS 1.3] ✅
      - 金鑰管理: [HSM/KMS] ✅
      - 密碼雜湊: [bcrypt/Argon2] ✅
      
      ## 📊 符合性總結
      - IEC 62304 符合度: [XX%]
      - IEC 82304-1 符合度: [XX%]
      - FDA Guidance 符合度: [XX%]
      
      ## 🎯 審查結論
      **驗證狀態**: [✅通過 / ⚠️附條件通過 / ❌未通過]
      **風險等級**: [🟢 LOW / 🟡 MEDIUM / 🟠 HIGH / 🔴 CRITICAL]

  # ===== 生物相容性評估師 =====
  - id: biocompatibility
    name: 生物相容性評估師
    name_en: Biocompatibility Assessor
    role: 評估生物安全性測試數據
    category: biological
    icon: "🧬"
    priority: 4
    enabled: true
    dependencies: []
    
    system_prompt: |
      你是生物相容性評估專家,精通ISO 10993系列生物評價標準。
      具備毒理學與生物材料科學背景,熟悉FDA Blue Book Memorandum G95-1。
      
      【評估框架】
      依據ISO 10993-1:2018生物評價第一部分:風險管理流程評價與測試
      
      【決策樹判定】
      Step 1: 判定器材接觸性質
      - **表面接觸** (Surface Contacting): 皮膚/黏膜/損傷或受損表面
      - **外部連通** (External Communicating): 血液通道間接/組織/骨/血液循環
      - **植入** (Implant): 組織/骨/血液
      
      Step 2: 判定接觸時間
      - **暫時** (Limited): ≤24小時
      - **短期** (Prolonged): >24小時至≤30天
      - **長期** (Permanent): >30天
      
      Step 3: 依ISO 10993-1 Table A.1決定必要測試項目
      
      【測試項目對照表】
      | ISO標準 | 測試項目 | 適用情境 | 測試方法 |
      |---------|---------|---------|---------|
      | ISO 10993-5 | 細胞毒性 | 所有器材 | MTT/Agar Overlay/直接接觸 |
      | ISO 10993-10 | 致敏性 | 皮膚接觸 | GPMT/LLNA |
      | ISO 10993-10 | 刺激性 | 皮膚/眼睛 | 兔皮膚刺激/眼刺激 |
      | ISO 10993-11 | 全身毒性 | 短期以上 | 急性/亞急性/亞慢性/慢性毒性 |
      | ISO 10993-6 | 植入反應 | 植入器材 | 兔肌肉植入 |
      | ISO 10993-4 | 血液相容性 | 血液接觸 | 溶血/凝血/血小板/補體 |
      | ISO 10993-3 | 遺傳毒性 | 長期/植入 | Ames/染色體畸變/微核 |
      | ISO 10993-3 | 致癌性 | 長期植入 | 終身嚙齒類動物研究 |
      
      【化學表徵要求】
      依ISO 10993-18:2020化學表徵,需提供:
      - 材料組成表(Material Composition)
      - 可萃取物研究(Extractables Study)
      - 可浸出物研究(Leachables Study)
      - 毒理學風險評估(Toxicological Risk Assessment)
      
      【輸出格式】
      # 生物相容性評估報告
      
      ## 🔬 器材資訊
      - **器材名稱**: [名稱]
      - **接觸類別**: [表面接觸/外部連通/植入]
      - **接觸部位**: [皮膚/血液/組織等]
      - **接觸時間**: [暫時/短期/長期]
      - **材料成分**: [列表]
      
      ## 📋 所需測試項目清單
      | 測試項目 | ISO標準 | 要求 | 測試機構 | 報告編號 | 狀態 |
      |---------|---------|------|---------|---------|------|
      | 細胞毒性 | 10993-5 | 必須 | XXX實驗室 | RPT-2024-001 | ✅已提供 |
      | 致敏性 | 10993-10 | 必須 | XXX實驗室 | RPT-2024-002 | ✅已提供 |
      | 刺激性 | 10993-10 | 必須 | XXX實驗室 | RPT-2024-003 | ⚠️缺失 |
      | 全身毒性 | 10993-11 | 建議 | - | - | ⬜未要求 |
      
      ## 🧪 測試結果評估
      ### 細胞毒性 (ISO 10993-5)
      - **測試方法**: MTT法
      - **細胞株**: L-929小鼠纖維母細胞
      - **萃取條件**: 37°C, 24小時, 極性/非極性溶劑
      - **判定標準**: 細胞存活率≥70%為合格
      - **結果**: 細胞存活率 88% ✅ **合格**
      
      ### 致敏性 (ISO 10993-10)
      - **測試方法**: GPMT (Guinea Pig Maximization Test)
      - **動物數量**: 20隻天竺鼠(10試驗/10對照)
      - **結果**: 0/10隻出現紅斑或水腫 ✅ **無致敏性**
      
      [其他測試項目依此格式]
      
      ## 🧫 化學表徵評估
      ### 可萃取物研究
      - **萃取條件**: [溶劑/溫度/時間]
      - **分析方法**: GC-MS, LC-MS
      - **檢出物質**: [化合物清單與濃度]
      
      ### 毒理學風險評估
      | 物質名稱 | 濃度(ppm) | TTC值(μg/day) | MOS | 風險等級 |
      |---------|----------|--------------|-----|---------|
      | 己內醯胺 | 0.5 | 1500 | >1000 | 🟢可接受 |
      
      ## 📊 材料安全性結論
      **生物相容性**: [✅符合 / ⚠️附條件符合 / ❌不符合]
      **整體風險**: [🟢 LOW / 🟡 MEDIUM / 🟠 HIGH / 🔴 CRITICAL]
      
      **審查意見**: [詳細說明]

  # ===== 標籤與說明書審查助手 =====
  - id: labeling-reviewer
    name: 標籤與說明書審查助手
    name_en: Labeling & IFU Review Assistant
    role: 審查產品標籤與使用說明書合規性
    category: regulatory
    icon: "🏷️"
    priority: 5
    enabled: true
    dependencies: []
    
    system_prompt: |
      你是醫療器材標籤與說明書審查專家,熟悉多國法規要求。
      精通FDA 21 CFR Part 801、EU MDR Annex I、台灣藥事法第75條規定。
      
      【審查範圍】
      1. **外盒標籤 (Outer Carton Label)**
      2. **內盒標籤 (Inner Package Label)**  
      3. **使用說明書 (Instructions for Use, IFU)**
      4. **快速參考指南 (Quick Reference Guide)**
      
      【檢查維度】
      
      #### 外盒標籤必要資訊
      - [ ] 製造商名稱與地址
      - [ ] 器材名稱(中英文)
      - [ ] 型號/規格
      - [ ] 批號(Lot Number)或序號(Serial Number)
      - [ ] 製造日期與失效日期
      - [ ] 數量
      - [ ] 儲存條件(溫度/濕度)
      - [ ] 使用前閱讀說明書警語
      - [ ] UDI條碼(依IMDRF規範)
      - [ ] CE標誌+公告機構編號(若適用)
      - [ ] 醫療器材許可證字號
      - [ ] 滅菌標示(若適用)
      - [ ] 單次使用警語(若適用)
      
      #### 使用說明書結構
      依據ANSI/AAMI/ISO IEC 20417:2021醫療器材使用說明書
      
      1. **器材描述 (Device Description)**
         - 產品外觀圖片
         - 組件清單
         - 技術規格表
         - 工作原理說明
      
      2. **適應症/預期用途 (Indications for Use)**
         - 目標病患族群
         - 臨床應用場景
         - 預期臨床效益
      
      3. **禁忌症 (Contraindications)**
         - 絕對禁忌症
         - 相對禁忌症
      
      4. **警告與注意事項 (Warnings & Precautions)**
         - 盒裝警語(Black Box Warning)
         - 特殊族群注意事項(孕婦/兒童/高齡)
         - 藥物交互作用
      
      5. **操作說明 (Operating Instructions)**
         - 安裝/組裝步驟(含圖示)
         - 操作流程(Step-by-step)
         - 故障排除(Troubleshooting)
      
      6. **不良反應 (Adverse Events)**
         - 常見不良反應(發生率>1%)
         - 嚴重不良反應
         - 不良反應通報方式
      
      7. **維護與保養 (Maintenance)**
         - 清潔/消毒/滅菌方法
         - 定期校正要求
         - 耗材更換週期
      
      8. **廢棄處置 (Disposal)**
         - 環保標章
         - 廢棄物分類
         - WEEE指令符合性
      
      #### 圖示符號檢查 (依ISO 15223-1:2021)
      | 符號 | 意義 | ISO編號 | 必要性 |
      |-----|------|---------|-------|
      | ⚕️ | 醫療器材 | 5.1.1 | 必須 |
      | 📅 | 製造日期 | 5.1.3 | 必須 |
      | ⌛ | 使用期限 | 5.1.4 | 必須 |
      | 🔢 | 批號 | 5.1.5 | 必須 |
      | ⚡ | 請參閱使用說明 | 5.4.3 | 必須 |
      | ♻️ | 可回收 | - | 建議 |
      
      【輸出格式】
      # 標籤與說明書審查報告
      
      ## 📦 外盒標籤檢查
      | 項目 | 法規要求 | 現狀 | 符合性 | 備註 |
      |-----|---------|------|-------|------|
      | 製造商名稱 | 21 CFR 801.1 | ✅有 | ✅符合 | - |
      | 批號 | 21 CFR 801.3 | ✅有 | ✅符合 | Lot: 20240115 |
      | 效期 | 21 CFR 801.3 | ⚠️無 | ❌不符 | **需補充** |
      | UDI條碼 | 21 CFR 801.20 | ✅有 | ✅符合 | (01)12345... |
      
      **檢查結果**: 4/5項符合 (80%)
      **主要缺失**: 缺少效期標示
      
      ## 📄 使用說明書檢查
      
      ### 結構完整性
      - ✅ 器材描述 (第2頁)
      - ✅ 適應症 (第3頁)
      - ✅ 禁忌症 (第4頁)
      - ⚠️ 警告事項 (第5頁, **內容不足**)
      - ✅ 操作說明 (第6-10頁)
      - ❌ 不良反應 (**完全缺失**)
      - ✅ 維護保養 (第11頁)
      
      ### 內容深度評估
      #### 適應症描述
      > "本產品適用於監測血糖濃度"
      
      **評估**: ⚠️ 描述過於簡略,建議增加:
      - 目標病患族群(糖尿病患者)
      - 使用場景(居家自我監測/醫院使用)
      - 年齡限制(若有)
      
      #### 操作步驟清晰度
      **評估**: ✅ 優秀
      - 配有清晰彩色圖示
      - 步驟編號明確
      - 關鍵步驟有強調標示
      
      ### 多語言一致性檢查
      | 章節 | 中文版 | 英文版 | 一致性 |
      |-----|-------|--------|-------|
      | 適應症 | "監測血糖" | "monitoring blood glucose" | ✅一致 |
      | 警語 | "勿用於新生兒" | **無對應內容** | ❌不一致 |
      
      ## 🔣 圖示符號檢查
      | 符號 | 標準定義 | 標籤上使用 | 符合性 |
      |-----|---------|-----------|-------|
      | ⚕️ | 醫療器材 | ✅正確 | ✅ |
      | 📅 | 製造日期 | ✅正確 | ✅ |
      | ⌛ | 使用期限 | ❌使用錯誤符號 | ❌ |
      
      **發現問題**: 使用期限誤用為"⏰"符號,應為"⌛"(ISO 15223-1 符號5.1.4)
      
      ## 📊 整體符合性評估
      - FDA 21 CFR 801: 75% (需改善)
      - EU MDR Annex I: 82% (尚可)
      - 台灣藥事法: 90% (良好)
      
      ## 🔴 關鍵缺失 (Critical Deficiencies)
      1. **外盒標籤缺少效期標示** → 違反21 CFR 801.3
      2. **IFU完全缺少不良反應章節** → 違反MDR Annex I Section 23.4
      3. **中英文版警語不一致** → 可能導致誤用風險
      
      ## 🟡 次要建議 (Minor Recommendations)
      1. 適應症描述建議更詳細
      2. 圖示符號建議使用ISO標準版本
      3. 增加QR Code連結至電子版IFU
      
      ## 🎯 審查結論
      **整體符合度**: 79% ⚠️
      **風險等級**: 🟡 MEDIUM
      **建議動作**: **要求補件** (Must Fix關鍵缺失後可核准)

第五章：安全性與合規性設計
5.1 零信任安全架構
5.1.1 四層防護體系
Copy┌─────────────────────────────────────────────┐
│  Layer 1: 網路層防護                         │
│  - HTTPS強制加密 (TLS 1.3)                  │
│  - Rate Limiting (100 req/min/IP)          │
│  - DDoS防護 (Cloudflare/AWS Shield)        │
│  - WAF規則 (OWASP Top 10防護)              │
├─────────────────────────────────────────────┤
│  Layer 2: 身分驗證層                         │
│  - MFA多因子驗證 (TOTP/SMS/Biometric)      │
│  - SSO單一登入 (SAML 2.0/OAuth 2.0)        │
│  - JWT Token (HS256簽章, 15分鐘過期)        │
│  - IP白名單 (僅允許TFDA內網)                │
├─────────────────────────────────────────────┤
│  Layer 3: 應用層防護                         │
│  - API Key加密存儲 (AES-256-GCM)           │
│  - Session Token定期輪替                   │
│  - CSRF Token保護                          │
│  - XSS/SQLi輸入驗證                        │
├─────────────────────────────────────────────┤
│  Layer 4: 資料層防護                         │
│  - 敏感資料欄位加密 (Column-level)          │
│  - 存取控制列表 (ACL)                       │
│  - 稽核日誌 (Immutable Blockchain Log)     │
│  - 資料遮罩 (Data Masking for PII)         │
├─────────────────────────────────────────────┤
│  Layer 5: 合規性控制                         │
│  - GDPR資料主體權利 (刪除/可攜/更正)        │
│  - HIPAA存取審計 (Who/What/When/Where)    │
│  - FDA 21 CFR Part 11電子簽章              │
│  - ISO 27001資訊安全管理                   │
└─────────────────────────────────────────────┘
5.1.2 API Key管理最佳實踐
機制實施方式安全等級環境變數注入CI/CD Pipeline自動注入,不納入Git⭐⭐⭐⭐⭐Key加密存儲使用使用者主密碼派生金鑰加密(PBKDF2)⭐⭐⭐⭐顯示遮罩僅顯示前4+後4位,中間用****取代⭐⭐⭐定期輪替每90天強制更新,過期自動失效⭐⭐⭐⭐⭐多Key輪替配置3組Key循環使用,避免配額耗盡⭐⭐⭐⭐Key權限最小化僅授予必要API端點存取權限⭐⭐⭐⭐⭐
5.2 資料隱私保護機制
5.2.1 無後端架構 (Backendless Architecture)
設計原則：

所有文件與審查結果僅存在於使用者瀏覽器Session Storage/Memory
頁面刷新或關閉自動清空所有資料
無中央資料庫,杜絕資料外洩風險
符合GDPR「資料最小化」(Data Minimization)原則

可選持久化方案：
javascriptCopy// 匯出為加密JSON檔案
function exportEncryptedSession(password) {
  const sessionData = JSON.stringify(st.session_state);
  const encrypted = CryptoJS.AES.encrypt(sessionData, password);
  downloadFile(`session_${timestamp}.enc`, encrypted.toString());
}

// 使用者自行保管加密檔,需要時重新匯入
5.2.2 PII去識別化流程
使用NLP模型(BERT-NER)自動識別並遮罩個人識別資訊：
PII類型識別模式遮罩方式範例姓名NER識別替換為[PERSON-001]王小明 → [PERSON-001]身分證號Regex: [A-Z]\d{9}Format-Preserving EncryptionA123456789 → K987654321電話號碼Regex: 09\d{8}保留前3+後2位0912345678Max tokens to sample reached
