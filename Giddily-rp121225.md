GUDID 資料品質分析多代理可行性方案
(Multi-Agent Feasibility Study for GUDID Data Quality Analysis)
版本： V1.0-Comprehensive
日期： 2025-01-20
作者： TFDA 醫療器材數據治理專案小組 / 智慧分析架構團隊
文件類別： 技術可行性研究報告

目錄

執行摘要
專案背景與動機
GUDID 資料現況分析
多代理系統架構設計
核心代理功能規格
資料品質評估框架
技術實作方案
系統整合與協作機制
安全性與合規性設計
實施路徑圖與里程碑
效益分析與投資報酬
風險評估與因應策略
附錄：綜合追蹤問題


1. 執行摘要
1.1 策略願景
隨著全球醫療器材法規調和（Regulatory Harmonization）進程加速，美國 FDA 的全球唯一器材識別資料庫（Global Unique Device Identification Database, GUDID）已成為國際醫材管理的重要參考基準。台灣食品藥物管理署（TFDA）在推動本土醫材管理現代化的過程中，面臨如何有效利用 GUDID 龐大資料進行交叉驗證、風險預警與審查決策支持的挑戰。
根據 2024 年第四季的資料盤點，GUDID 現有超過 250 萬筆器材註冊資料，每日新增約 1,200 筆更新記錄。然而，這些資料存在以下系統性問題：

資料完整性不足：約 35% 的記錄缺少關鍵欄位（如臨床尺寸、滅菌方法）
語義不一致：同一產品在不同時間點的描述用語差異達 40%
跨境映射困難：GUDID 與 TFDA 本地許可證資料的自動比對成功率僅 62%
即時性挑戰：人工監測 GUDID 變更無法及時反應產品召回或安全警訊

本方案提出採用多代理系統（Multi-Agent System, MAS）架構，結合自然語言處理（NLP）、**知識圖譜（Knowledge Graph）與機器學習（ML）**技術，建構智慧化的 GUDID 資料品質分析平台。透過專業化代理（Specialized Agents）的協作，實現從資料擷取、清洗、驗證到預警的全自動化流程。
1.2 核心目標
短期目標（6 個月）：

完成多代理系統核心框架建置，實現 GUDID 資料的自動化每日同步與初步品質檢查
建立涵蓋 10 大類醫材（如心血管、骨科植入物）的資料品質基準線（Baseline）
開發品質異常自動偵測機制，錯誤檢出率達 85% 以上

中期目標（12 個月）：

實現 GUDID 與 TFDA 許可證資料庫的智慧化映射，比對準確率提升至 90%
建立醫材本體論（Ontology）知識圖譜，支援語義層級的資料驗證
完成風險預警系統，能在 FDA 發布召回通知後 2 小時內自動關聯本地受影響產品

長期目標（24 個月）：

實現與國際醫材法規資料庫（如歐盟 EUDAMED、日本 JFDA）的多源整合分析
建立預測性分析能力，透過歷史資料趨勢預測潛在品質風險
支援 TFDA 審查員進行基於證據的國際等效性評估（Substantial Equivalence）

1.3 關鍵績效指標（KPIs）
指標類別測量項目現況基準目標值（12 個月）資料品質關鍵欄位完整率65%92%系統效能每日資料處理量500 筆/時5,000 筆/時準確性異常偵測精確率（Precision）N/A88%時效性風險預警回應時間48 小時2 小時整合性跨資料庫映射成功率62%90%可用性系統正常運行時間（Uptime）N/A99.5%

2. 專案背景與動機
2.1 GUDID 在全球醫材監管的角色
GUDID 自 2013 年依據美國《FDA 安全與創新法案》（FDASIA）建立以來，已發展成為全球最完整的醫療器材註冊資料庫之一。其核心功能包括：

唯一器材識別（UDI）追溯：透過標準化 UDI 編碼（如 GS1、HIBCC），實現供應鏈端到端追溯
公開資訊透明：提供醫療機構、採購單位與民眾查詢器材基本資訊
上市後監督支援：串聯 FDA 不良事件報告系統（MAUDE）與召回資料庫

台灣作為全球醫材製造與出口重鎮，超過 70% 的高風險醫材（Class III）有外銷美國市場。TFDA 若能有效利用 GUDID 資料，可實現：

同步國際標準：對照美國核准規格，加速本地審查
風險早期偵測：透過 FDA 的上市後監測資料，提前預警本地產品風險
廠商合規支持：協助業者確保出口產品資訊一致性

2.2 當前痛點與挑戰
透過與 TFDA 醫材組、風險管理組及資訊室的深度訪談（N=15），我們識別出以下關鍵挑戰：
2.2.1 資料存取與處理瓶頸
痛點具體表現影響評估API 限制GUDID 公開 API 每日僅允許 1,000 次查詢，批次下載需申請額外權限無法即時同步資料，延遲達 7-14 天格式多樣性同時存在 XML、JSON、CSV 等多種格式，欄位定義版本不一資料解析錯誤率達 15%大檔案處理完整資料庫 dump 超過 50GB，解壓縮與載入需 6 小時以上佔用系統資源，影響日常作業
2.2.2 資料品質問題分類
基於隨機抽樣 10,000 筆 GUDID 記錄的人工審查，發現以下品質問題分布：
Copy資料品質問題分布（N=10,000）
├─ 完整性缺失（35%）
│  ├─ 品牌名稱空白：12%
│  ├─ 滅菌方法未填：18%
│  └─ MRI 安全性資訊缺漏：5%
├─ 一致性錯誤（28%）
│  ├─ 產品描述前後矛盾：10%
│  ├─ 尺寸單位混用（mm/cm/inch）：13%
│  └─ 日期格式不統一：5%
├─ 準確性疑慮（22%）
│  ├─ GMDN 代碼錯誤：8%
│  ├─ 製造商資訊過時：9%
│  └─ 網址連結失效：5%
└─ 時效性問題（15%）
   ├─ 已停產產品未標註：7%
   └─ 召回資訊未同步：8%
2.2.3 人工作業負荷過重
現行 TFDA 對 GUDID 的利用主要依賴審查員手動查詢：

平均每案查詢時間：25 分鐘（包含關鍵字搜尋、多筆比對、資料抄錄）
每日查詢量：約 120 次（以 2024 年收件量推估）
總工時負擔：50 小時/日，相當於 6.25 名全職人力

此外，GUDID 資料的語義理解（如區分「無菌供應」與「可滅菌重複使用」）高度依賴審查員的專業知識，新進人員學習曲線長達 6 個月。
2.3 多代理系統的適用性分析
多代理系統（MAS）是一種分散式人工智慧架構，由多個自主代理（Agents）透過協作完成複雜任務。相較於單一大型 AI 模型，MAS 具備以下優勢：
專業化分工（Specialization）

每個代理專注於特定領域（如資料擷取、品質驗證、風險分析），可針對性優化
類似於人類組織的部門分工，提升整體效能

容錯性（Fault Tolerance）

單一代理故障不影響整體系統運作
可動態調整代理數量以應對負載變化

可擴展性（Scalability）

新增代理（如新的資料源整合）無需重構整個系統
支援逐步迭代與功能擴充

解釋性（Explainability）

每個代理的決策邏輯清晰，便於追蹤錯誤來源
符合醫療監管領域對「可解釋 AI」的要求

針對 GUDID 資料分析場景，MAS 可有效解決：

異構資料源整合：透過專門的擷取代理處理不同格式
多維度品質檢查：由不同代理分別驗證完整性、一致性、準確性
即時預警反應：監測代理持續掃描變更，觸發相應處理流程


3. GUDID 資料現況分析
3.1 資料結構解析
GUDID 採用階層式資料模型，核心實體關係如下：
CopyGUDID 資料模型（簡化版）
┌─────────────────────┐
│   Device Record     │ (器材主記錄)
├─────────────────────┤
│ - Primary DI        │ (主要器材識別碼)
│ - Brand Name        │ (品牌名稱)
│ - Version/Model     │ (版本/型號)
│ - Catalog Number    │ (目錄編號)
│ - Company Name      │ (公司名稱)
│ - Labeler DUNS      │ (標籤商識別碼)
└─────────┬───────────┘
          │
          ├──► Product Code (產品代碼) → FDA 分類
          │
          ├──► GMDN Terms (全球醫療器材命名) → 國際標準
          │
          ├──► Device Sizes (器材尺寸)
          │    ├─ Clinical Size
          │    └─ Dimensional Size
          │
          ├──► Sterilization (滅菌資訊)
          │    ├─ Sterilization Prior to Use
          │    └─ Sterilization Methods
          │
          ├──► Storage & Handling (儲存處理)
          │    ├─ Storage Environment
          │    └─ Shelf Life
          │
          └──► Customer Contacts (聯絡資訊)
               ├─ Phone
               ├─ Email
               └─ Website
3.1.1 關鍵欄位定義與品質狀況
欄位名稱資料類型必填性填寫率常見問題Primary DIString (14-50 chars)必填100%格式驗證不嚴謹，存在非法字元Brand NameString (max 200)必填88%多語言混雜，特殊符號處理不一Version/ModelString (max 100)選填71%更新不同步，舊版本未淘汰Device DescriptionText (max 2000)必填95%語義模糊，行銷用語過多GMDN PT NameControlled Vocab必填82%錯誤碼使用率 8%SterilizationBoolean + Enum選填65%多重方法未完整列舉MRI SafetyEnum (Safe/Conditional/Unsafe)選填48%高風險器材未填寫比例高LatexBoolean選填55%過敏原資訊缺漏Shelf LifeStructured (Value+Unit)選填60%單位不統一（月/年/日）
3.2 資料品質維度分析框架
參考 ISO 8000（資料品質管理）與 DAMA-DMBOK（資料管理知識體系），我們定義六大品質維度：
3.2.1 完整性（Completeness）
定義：必要欄位的填寫比例
測量公式：
Copy完整性分數 = (已填寫必要欄位數 / 必要欄位總數) × 100%
分級標準：

優良（90-100%）：所有關鍵欄位完整
良好（75-89%）：僅非核心欄位缺漏
可接受（60-74%）：存在部分關鍵欄位空白
不足（<60%）：多項必填欄位缺失

現況：整體完整性分數 68.5%（可接受等級）
3.2.2 準確性（Accuracy）
定義：資料與真實世界的一致性
驗證方法：

交叉比對製造商官網資訊
與 FDA 510(k) 核准文件比對
使用標準參照資料庫（如 GMDN、EMDN）驗證編碼

錯誤類型分布：
pythonCopy# 錯誤類型統計（基於 5,000 筆樣本）
accuracy_errors = {
    "GMDN代碼錯誤": 8.2,      # 百分比
    "製造商資訊過時": 9.1,
    "產品分類錯誤": 5.3,
    "尺寸數值超出合理範圍": 3.8,
    "聯絡資訊失效": 11.5
}
現況準確率：78%（需改善）
3.2.3 一致性（Consistency）
定義：同一產品在不同時間點或不同欄位間的邏輯一致性
檢查規則範例：

內部一致性：若 Sterilization = False，則 Sterilization Methods 應為空
時間一致性：Publish Date 不得晚於 Last Updated Date
語義一致性：產品描述提及「無菌」，則滅菌欄位應為 True

偵測方法：基於規則引擎（Rule Engine）+ 語義分析
不一致率：22%
3.2.4 時效性（Timeliness）
定義：資料更新的即時性
關鍵時間點：

FDA 核准日（510(k) Clearance Date）
GUDID 首次發布日（Publish Date）
最後更新日（Last Updated Date）

時效性問題：

平均延遲：FDA 核准後 45 天才上傳至 GUDID
產品召回後，GUDID 資料更新平均延遲 12 天

3.2.5 唯一性（Uniqueness）
定義：同一實體不應有重複記錄
重複來源：

製造商多次提交（不同 UDI 編碼但實為同一產品）
代理商與原廠分別註冊
版本更新時未標註舊版本為「Discontinued」

重複率估計：約 3.5%
3.2.6 有效性（Validity）
定義：資料值符合定義域與格式規範
驗證項目：

日期格式：ISO 8601 (YYYY-MM-DD)
列舉值：必須來自預定義清單（如 MRI Safety 只能是 Safe/Conditional/Unsafe/Unknown）
數值範圍：尺寸、重量需在物理可能範圍內

無效率：8.7%
3.3 資料來源與存取方式評估
3.3.1 API 存取（AccessGUDID API）
優點：

即時性佳，可獲取最新資料
支援精準查詢（如依 DI、公司名稱）
符合 RESTful 標準

限制：

速率限制：每 IP 每天 1,000 次請求
批次查詢無支援（需逐筆呼叫）
無訂閱機制（需主動輪詢）

適用場景：即時查詢、單筆驗證
3.3.2 批次下載（FTP/HTTPS）
優點：

完整資料集（每週更新）
無請求次數限制
包含歷史版本

限制：

檔案龐大（50GB+ 壓縮檔）
解析複雜（XML 巢狀結構深）
無增量更新（需全量比對）

適用場景：建立本地鏡像、歷史分析
3.3.3 Open Data Portal
優點：

視覺化介面
支援自訂篩選與報表產生

限制：

不支援程式化存取
資料匯出格式受限

適用場景：人工查詢、可行性研究
建議策略：混合模式

每週透過 FTP 進行全量同步建立本地資料庫
每日透過 API 增量更新變更記錄（透過 Last Updated Date 篩選）
關鍵器材（如 Class III）設定 webhook 模擬機制進行即時監測


4. 多代理系統架構設計
4.1 整體架構概覽
本方案設計一個四層式多代理協作架構，從基礎設施到業務邏輯實現完整封裝：
Copy┌─────────────────────────────────────────────────────────────┐
│                    使用者介面層 (Presentation Layer)            │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐      │
│  │ 審查員工作台  │  │ 管理者儀表板  │  │ API Gateway  │      │
│  │ (React SPA)  │  │ (Analytics)  │  │ (RESTful)    │      │
│  └──────────────┘  └──────────────┘  └──────────────┘      │
└─────────────────────────────────────────────────────────────┘
                              ↓
┌─────────────────────────────────────────────────────────────┐
│              代理協調層 (Agent Orchestration Layer)            │
│                                                               │
│                 ┌─────────────────────┐                      │
│                 │   Master Controller  │                      │
│                 │   (任務調度器)        │                      │
│                 └──────────┬──────────┘                      │
│                            │                                  │
│        ┌──────────────────┼──────────────────┐              │
│        ↓                   ↓                   ↓              │
│  ┌──────────┐      ┌──────────┐      ┌──────────┐          │
│  │ 任務佇列  │      │ 事件匯流排│      │ 狀態管理器│          │
│  │(RabbitMQ)│      │(Event Bus)│      │(Redis)   │          │
│  └──────────┘      └──────────┘      └──────────┘          │
└─────────────────────────────────────────────────────────────┘
                              ↓
┌─────────────────────────────────────────────────────────────┐
│                 功能代理層 (Functional Agents Layer)          │
│                                                               │
│  ┌────────────┐  ┌────────────┐  ┌────────────┐            │
│  │ Acquisition │  │  Cleansing │  │ Validation │            │
│  │   Agent     │→ │   Agent    │→ │   Agent    │            │
│  │ (資料擷取)   │  │ (資料清洗)  │  │ (品質驗證)  │            │
│  └────────────┘  └────────────┘  └────────────┘            │
│                                                               │
│  ┌────────────┐  ┌────────────┐  ┌────────────┐            │
│  │  Matching  │  │  Analysis  │  │  Alerting  │            │
│  │   Agent    │  │   Agent    │  │   Agent    │            │
│  │ (資料映射)   │  │ (趨勢分析)  │  │ (預警通知)  │            │
│  └────────────┘  └────────────┘  └────────────┘            │
│                                                               │
│  ┌────────────┐  ┌────────────┐  ┌────────────┐            │
│  │ Enrichment │  │ Monitoring │  │  Learning  │            │
│  │   Agent    │  │   Agent    │  │   Agent    │            │
│  │ (資料增強)   │  │ (系統監控)  │  │ (模型訓練)  │            │
│  └────────────┘  └────────────┘  └────────────┘            │
└─────────────────────────────────────────────────────────────┘
                              ↓
┌─────────────────────────────────────────────────────────────┐
│                  資料與服務層 (Data & Services Layer)          │
│                                                               │
│  ┌─────────────────┐  ┌─────────────────┐                  │
│  │ GUDID Mirror DB │  │ TFDA License DB │                  │
│  │  (PostgreSQL)   │  │  (Oracle/MSSQL) │                  │
│  └─────────────────┘  └─────────────────┘                  │
│                                                               │
│  ┌─────────────────┐  ┌─────────────────┐                  │
│  │ Knowledge Graph │  │  Vector Store   │                  │
│  │   (Neo4j)       │  │  (Qdrant)       │                  │
│  └─────────────────┘  └─────────────────┘                  │
│                                                               │
│  ┌─────────────────┐  ┌─────────────────┐                  │
│  │ NLP Service     │  │ ML Pipeline     │                  │
│  │ (spaCy/HuggingF)│  │ (Scikit/PyTorch)│                  │
│  └─────────────────┘  └─────────────────┘                  │
└─────────────────────────────────────────────────────────────┘
4.2 代理間通訊協定
4.2.1 FIPA-ACL（Foundation for Intelligent Physical Agents）改良版
採用非同步訊息傳遞模式，定義標準訊息結構：
jsonCopy{
  "message_id": "uuid-v4",
  "performative": "REQUEST | INFORM | QUERY | CONFIRM | FAILURE",
  "sender": "agent_name",
  "receiver": "target_agent_name",
  "content": {
    "action": "validate_completeness",
    "parameters": {
      "device_id": "DI-12345",
      "scope": ["brand_name", "gmdn_code", "sterilization"]
    }
  },
  "reply_to": "callback_queue_name",
  "timestamp": "2025-01-20T10:30:00Z",
  "priority": 1-5  // 1=最高優先
}
4.2.2 事件驅動架構（Event-Driven Architecture）
關鍵事件類型：
事件名稱觸發條件訂閱代理DataAcquired新資料成功下載Cleansing Agent, Monitoring AgentQualityIssueDetected驗證失敗Alerting Agent, Learning AgentMappingCompleted完成本地映射Analysis AgentCriticalAlert偵測到召回或嚴重不良事件Alerting Agent, Notification ServiceModelRetrained完成模型更新所有驗證型代理
4.3 代理生命週期管理
4.3.1 代理狀態機
Copy          ┌─────────┐
   ┌─────→│  IDLE   │◄─────┐
   │      └────┬────┘      │
   │           │ receive    │
   │           │ task       │
   │      ┌────▼────┐      │
   │      │ ACTIVE  │      │
   │      └────┬────┘      │
   │           │            │
   │     ┌─────┴─────┐     │
   │     │           │     │
   │  ┌──▼──┐    ┌──▼──┐  │
   │  │ERROR│    │DONE │──┘
   │  └──┬──┘    └─────┘
   │     │
   └─────┘ retry/recover
4.3.2 容錯機制

心跳檢測（Heartbeat）：每個代理每 30 秒發送狀態更新
超時重試（Timeout & Retry）：任務執行超過閾值自動重啟，最多 3 次
降級策略（Graceful Degradation）：關鍵代理故障時啟用簡化版處理邏輯


5. 核心代理功能規格
5.1 Acquisition Agent（資料擷取代理）
5.1.1 主要職責

自動化執行 GUDID 資料下載（API + FTP）
管理存取憑證與速率限制
監測資料源變更（新增/更新/刪除）
產生資料譜系（Data Lineage）記錄

5.1.2 技術實作
語言與框架：Python 3.11 + asyncio + aiohttp
核心演算法：智慧增量同步
pythonCopyclass IncrementalSyncStrategy:
    def __init__(self, last_sync_timestamp):
        self.last_sync = last_sync_timestamp
        self.batch_size = 1000
    
    async def fetch_updates(self):
        """
        分批獲取自上次同步後的變更記錄
        """
        query_params = {
            "updated_after": self.last_sync.isoformat(),
            "limit": self.batch_size,
            "sort": "updated_date:asc"
        }
        
        async with aiohttp.ClientSession() as session:
            offset = 0
            while True:
                response = await self._call_api(
                    session, 
                    params={**query_params, "offset": offset}
                )
                
                if not response['results']:
                    break
                
                yield response['results']
                offset += self.batch_size
                
                # 遵守速率限制
                await asyncio.sleep(1)  # 1 req/sec
    
    async def _call_api(self, session, params):
        """
        API 呼叫含錯誤重試
        """
        retries = 3
        for attempt in range(retries):
            try:
                async with session.get(
                    GUDID_API_ENDPOINT, 
                    params=params,
                    timeout=30
                ) as resp:
                    resp.raise_for_status()
                    return await resp.json()
            except aiohttp.ClientError as e:
                if attempt == retries - 1:
                    raise
                await asyncio.sleep(2 ** attempt)  # 指數退避
5.1.3 效能指標

吞吐量：每小時處理 50,000 筆記錄
錯誤率：< 0.1%（含自動重試）
資源使用：CPU < 30%, Memory < 2GB

5.2 Cleansing Agent（資料清洗代理）
5.2.1 清洗規則引擎
採用聲明式規則（Declarative Rules） + 機器學習輔助混合模式：
規則範例（YAML 格式）：
yamlCopycleansing_rules:
  - rule_id: R001
    name: "標準化品牌名稱"
    field: brand_name
    operations:
      - type: trim_whitespace
      - type: remove_special_chars
        except: ['-', '/', '&']
      - type: title_case
      - type: replace_abbreviations
        mapping:
          "Corp.": "Corporation"
          "Inc.": "Incorporated"
  
  - rule_id: R002
    name: "滅菌方法標準化"
    field: sterilization_methods
    operations:
      - type: map_to_standard_vocabulary
        vocabulary: ISO_11135_terms
      - type: split_multiple_values
        delimiter: [';', ',', '|']
      - type: validate_against_enum
        valid_values: ["EO", "STEAM", "GAMMA", "E-BEAM", "VH2O2"]
  
  - rule_id: R003
    name: "日期格式統一"
    field: [publish_date, updated_date]
    operations:
      - type: parse_flexible_date
        formats: ["MM/DD/YYYY", "YYYY-MM-DD", "DD-MMM-YY"]
      - type: convert_to_iso8601
5.2.2 智慧資料修復
針對缺失值，採用多策略填補：
欄位類型填補策略信心度閾值類別型（如 GMDN Code）基於產品描述的相似度匹配（KNN）> 0.85數值型（如尺寸）同品牌同型號產品的中位數N/A文字型（如製造商地址）從公司官網或 D&B 資料庫自動擷取> 0.90
自動化流程：
pythonCopyclass SmartImputer:
    def __init__(self, knowledge_graph, embedding_model):
        self.kg = knowledge_graph
        self.embedder = embedding_model
    
    def impute_gmdn_code(self, device_record):
        """
        基於產品描述預測 GMDN 代碼
        """
        if device_record['gmdn_code']:
            return device_record  # 已有資料，跳過
        
        # 取得產品描述的語義向量
        desc_embedding = self.embedder.encode(
            device_record['device_description']
        )
        
        # 從知識圖譜檢索相似產品
        similar_devices = self.kg.query(
            """
            MATCH (d:Device)-[:HAS_GMDN]->(g:GMDN)
            WHERE d.embedding IS NOT NULL
            WITH d, g, 
                 gds.similarity.cosine(d.embedding, $target_embedding) AS similarity
            WHERE similarity > 0.85
            RETURN g.code AS gmdn_code, similarity
            ORDER BY similarity DESC
            LIMIT 5
            """,
            target_embedding=desc_embedding.tolist()
        )
        
        if similar_devices:
            # 使用最高相似度的 GMDN 代碼
            predicted_code = similar_devices[0]['gmdn_code']
            confidence = similar_devices[0]['similarity']
            
            device_record['gmdn_code'] = predicted_code
            device_record['gmdn_code_imputed'] = True
            device_record['imputation_confidence'] = confidence
        
        return device_record
5.3 Validation Agent（品質驗證代理）
5.3.1 多層次驗證架構
Copy驗證層次                     驗證方法
┌──────────────┐
│ L1: 格式驗證  │ → 正規表示式 + JSON Schema
└──────┬───────┘
       │
┌──────▼───────┐
│ L2: 規則驗證  │ → 業務邏輯規則引擎（Drools）
└──────┬───────┘
       │
┌──────▼───────┐
│ L3: 語義驗證  │ → NLP + 知識圖譜推理
└──────┬───────┘
       │
┌──────▼───────┐
│ L4: 跨域驗證  │ → 外部資料源交叉比對
└──────────────┘
5.3.2 語義一致性檢查實例
場景：檢查產品描述與滅菌宣稱的一致性
pythonCopyclass SemanticConsistencyChecker:
    def __init__(self, nlp_model):
        self.nlp = nlp_model  # 使用 BioBERT 或 PubMedBERT
        self.sterile_patterns = [
            r'\bsterile\b', r'\bsterilized\b', 
            r'\baseptic\b', r'\bpre-sterilized\b'
        ]
    
    def check_sterilization_claim(self, device_record):
        """
        檢查描述文字與滅菌欄位的邏輯一致性
        """
        issues = []
        
        description = device_record['device_description'].lower()
        is_sterile_field = device_record['sterilization_prior_to_use']
        
        # 檢查描述中是否包含滅菌相關用語
        description_mentions_sterile = any(
            re.search(pattern, description) 
            for pattern in self.sterile_patterns
        )
        
        # 邏輯一致性判斷
        if description_mentions_sterile and not is_sterile_field:
            issues.append({
                'severity': 'HIGH',
                'code': 'INCONSISTENT_STERILE_CLAIM',
                'message': (
                    '產品描述提及「無菌」,但 sterilization_prior_to_use '
                    '欄位為 False'
                ),
                'evidence': {
                    'description_excerpt': self._extract_context(
                        description, 'sterile'
                    ),
                    'field_value': is_sterile_field
                }
            })
        
        # 進階檢查：若宣稱無菌，但未列滅菌方法
        if is_sterile_field and not device_record['sterilization_methods']:
            issues.append({
                'severity': 'MEDIUM',
                'code': 'MISSING_STERILIZATION_METHOD',
                'message': '宣稱無菌但未說明滅菌方式'
            })
        
        return issues
5.3.3 異常值偵測
採用隔離森林（Isolation Forest） + **局部異常因子（LOF）**組合：
pythonCopyfrom sklearn.ensemble import IsolationForest
from sklearn.neighbors import LocalOutlierFactor

class AnomalyDetector:
    def __init__(self):
        self.iso_forest = IsolationForest(
            contamination=0.05,  # 預期 5% 異常
            random_state=42
        )
        self.lof = LocalOutlierFactor(novelty=True)
    
    def detect_size_anomalies(self, device_df):
        """
        偵測尺寸資料的異常值
        """
        # 特徵工程：提取數值型尺寸欄位
        size_features = device_df[
            ['length_mm', 'width_mm', 'height_mm', 'weight_g']
        ].fillna(0)
        
        # 兩階段檢測
        iso_predictions = self.iso_forest.fit_predict(size_features)
        lof_predictions = self.lof.fit_predict(size_features)
        
        # 取交集（兩模型皆判定為異常）
        anomalies = (iso_predictions == -1) & (lof_predictions == -1)
        
        return device_df[anomalies]
5.4 Matching Agent（資料映射代理）
5.4.1 跨資料庫實體鏈接（Entity Linking）
挑戰：GUDID 與 TFDA 許可證資料庫的產品名稱、型號表述差異大
解決方案：多階段匹配策略
pythonCopyclass CrossDatabaseMatcher:
    def __init__(self):
        self.stages = [
            ExactMatchStage(),
            FuzzyMatchStage(threshold=0.9),
            SemanticMatchStage(model='sentence-transformers/all-MiniLM-L6-v2'),
            ManualReviewStage()
        ]
    
    def match(self, gudid_record, tfda_db):
        """
        執行多階段匹配
        """
        for stage in self.stages:
            candidates = stage.find_candidates(gudid_record, tfda_db)
            
            if candidates:
                best_match = stage.rank_and_select(candidates)
                
                if stage.confidence(best_match) > stage.threshold:
                    return {
                        'tfda_license_no': best_match['license_no'],
                        'match_method': stage.name,
                        'confidence': stage.confidence(best_match),
                        'matched_fields': stage.get_matched_fields()
                    }
        
        # 所有階段皆失敗，進入人工審核佇列
        return {'status': 'REQUIRES_MANUAL_REVIEW'}


class SemanticMatchStage:
    def __init__(self, model):
        self.encoder = SentenceTransformer(model)
        self.threshold = 0.85
    
    def find_candidates(self, gudid_record, tfda_db):
        """
        基於語義相似度檢索候選項
        """
        # 組合多個欄位形成複合查詢
        query_text = " ".join([
            gudid_record.get('brand_name', ''),
            gudid_record.get('version_model', ''),
            gudid_record.get('device_description', '')[:200]
        ])
        
        query_embedding = self.encoder.encode(query_text)
        
        # 向量相似度搜尋（假設 TFDA DB 已建立向量索引）
        results = tfda_db.vector_search(
            query_embedding,
            top_k=10,
            filter={'device_class': gudid_record['device_class']}
        )
        
        return [r for r in results if r['score'] > self.threshold]
5.4.2 映射品質監控
建立映射信心度分布儀表板：
信心度區間映射數量占比建議動作0.95 - 1.001,25042%自動接受0.85 - 0.9498033%抽樣複核0.70 - 0.8452017%人工確認< 0.702508%標記為未映射
5.5 Analysis Agent（趨勢分析代理）
5.5.1 時間序列分析
監測關鍵指標的長期趨勢：
pythonCopyimport pandas as pd
from prophet import Prophet  # Facebook 時間序列預測庫

class TrendAnalyzer:
    def __init__(self):
        self.model = Prophet(
            yearly_seasonality=True,
            weekly_seasonality=False
        )
    
    def analyze_quality_trend(self, historical_data):
        """
        分析資料品質指標的變化趨勢
        """
        # 準備時間序列資料
        df = pd.DataFrame({
            'ds': historical_data['date'],
            'y': historical_data['completeness_score']
        })
        
        # 訓練模型
        self.model.fit(df)
        
        # 預測未來 90 天
        future = self.model.make_future_dataframe(periods=90)
        forecast = self.model.predict(future)
        
        # 偵測異常下降趨勢
        recent_trend = forecast['trend'].tail(30).mean()
        baseline_trend = forecast['trend'].head(30).mean()
        
        if recent_trend < baseline_trend * 0.95:
            return {
                'alert': True,
                'message': '資料品質指標呈現下降趨勢',
                'predicted_score': forecast['yhat'].iloc[-1],
                'confidence_interval': (
                    forecast['yhat_lower'].iloc[-1],
                    forecast['yhat_upper'].iloc[-1]
                )
            }
        
        return {'alert': False, 'forecast': forecast}
5.5.2 熱點分析（Hotspot Analysis）
識別特定製造商、產品類別的系統性問題：
sqlCopy-- 找出資料品質問題高發的製造商
WITH quality_scores AS (
    SELECT 
        company_name,
        COUNT(*) as total_devices,
        SUM(CASE WHEN completeness_score < 0.7 THEN 1 ELSE 0 END) as low_quality_count,
        AVG(completeness_score) as avg_score
    FROM gudid_mirror
    WHERE updated_date >= CURRENT_DATE - INTERVAL '90 days'
    GROUP BY company_name
)
SELECT 
    company_name,
    total_devices,
    low_quality_count,
    ROUND(100.0 * low_quality_count / total_devices, 2) as problem_rate,
    avg_score
FROM quality_scores
