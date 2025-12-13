TW-SmartReview 2030 智慧化審查代理人系統技術規格書
TW-SmartReview 2030 Agentic System Technical Specifications
版本： v4.2.0 (Cinematic Release)
日期： 2025年12月15日
機密等級： 內部技術文件
提交單位： 智慧醫療法規科學專案研究小組技術開發部

目錄 (Table of Contents)

專案概述 (Executive Summary)
系統架構設計 (System Architecture)

2.1 技術堆疊 (Tech Stack)
2.2 資料流架構 (Data Flow Architecture)
2.3 安全性與隱私設計 (Security & Privacy)


核心功能模組詳解 (Core Modules)

3.1 智慧儀表板 (Cinematic Dashboard)
3.2 文件攝取與多模態 OCR (Ingestion & Multimodal OCR)
3.3 代理人編排器 (Agent Orchestrator)
3.4 智慧筆記中樞 (Intelligence Hub)
3.5 全域設定與側邊欄 (Global Configuration)


UI/UX 設計系統 (Design System)

4.1 藝術風格引擎 (Painter Style Engine)
4.2 視覺化互動設計 (Visualization & Interactions)


AI 模型整合策略 (AI Integration Strategy)

5.1 Google Gemini API 實作
5.2 Prompt Engineering 架構


資料結構與型別定義 (Data Models)
部署與維運 (Deployment & DevOps)
FDA專用進階功能模組 (FDA-Specific Advanced Features)

8.1 法規智慧比對引擎 (Regulatory Intelligence Matching Engine)
8.2 臨床試驗數據分析模組 (Clinical Trial Data Analysis Module)
8.3 風險管理自動化系統 (Automated Risk Management System)
8.4 上市後監測整合平台 (Post-Market Surveillance Integration)
8.5 多國法規協調模組 (Multi-Regional Regulatory Harmonization)
8.6 品質管理系統追蹤器 (QMS Compliance Tracker)
8.7 醫療器材分類智慧引擎 (Medical Device Classification AI)
8.8 生物相容性評估自動化 (Biocompatibility Assessment Automation)
8.9 標籤與說明書審查助手 (Labeling & IFU Review Assistant)
8.10 區塊鏈審查軌跡系統 (Blockchain Audit Trail System)


系統效能優化與擴展性 (Performance Optimization & Scalability)
結論 (Conclusion)
綜合性後續問題 (Comprehensive Follow-up Questions)


1. 專案概述 (Executive Summary)
TW-SmartReview 2030 是一個專為衛生福利部食品藥物管理署 (TFDA) 以及美國食品藥物管理局 (FDA) 設計的未來概念驗證系統，旨在解決醫療器材查驗登記過程中面臨的數據洪流與審查效率瓶頸。本系統採用代理型人工智慧 (Agentic AI) 架構，透過多個專職的 AI 代理人協同工作,自動化處理文件解析、法規比對、風險評估與科學審查。
本技術規格書涵蓋了 v4.2.0 版本的完整實作細節。此版本引入了全新的 "WOW UI" (Cinematic Interface)，強調高互動性的視覺體驗、動態的神經網絡視覺化、以及基於藝術風格的主題切換引擎。系統完全基於瀏覽器端執行 (Client-Side Execution)，利用 Google Gemini 2.5 Flash 模型的高速推論能力，實現近乎即時的文件理解與多步驟推理。
1.1 系統設計理念
本系統的核心設計理念包含以下五大支柱：
智慧化 (Intelligence)：運用最先進的大型語言模型 (LLM) 與機器學習技術，自動識別醫療器材文件中的關鍵資訊、潛在風險點以及法規符合性缺口。
自動化 (Automation)：減少人工重複性作業，將審查員從繁瑣的資料收集與初步篩選中解放，使其能專注於高價值的科學判斷與決策制定。
透明化 (Transparency)：所有 AI 代理人的推理過程、參考資料來源與決策依據均以結構化方式呈現，確保審查流程的可追溯性與可解釋性，符合監管科學 (Regulatory Science) 的嚴謹要求。
協同化 (Collaboration)：系統設計為多代理人協作模式，每個代理人負責特定領域 (如臨床評估、電氣安全、軟體驗證等)，透過中央編排器 (Orchestrator) 進行任務分配與結果整合，模擬真實世界中的跨部門審查團隊運作模式。
隱私優先 (Privacy-First)：採用無後端架構 (Backendless Architecture)，所有敏感文件與審查數據僅存在於使用者的本地瀏覽器 Session 中，不經過任何第三方伺服器儲存，從根本上消除資料外洩風險。
1.2 目標使用者群體

TFDA/FDA 醫療器材審查員：作為日常審查工作的輔助工具，提升審查效率與一致性。
醫療器材製造商法規事務人員：用於送審前的自我檢查 (Pre-submission Review)，降低補件率與審查週期。
第三方查驗登記顧問：作為專業服務工具，協助客戶快速識別文件缺陷與法規風險。
學術研究機構：用於醫療器材法規科學的教學與研究。


2. 系統架構設計 (System Architecture)
本系統採用單頁應用程式 (Single Page Application, SPA) 架構，強調輕量化、高回應性與隱私優先的設計原則。整體架構遵循無伺服器 (Serverless) 與邊緣運算 (Edge Computing) 的現代化設計模式。
2.1 技術堆疊 (Tech Stack)
2.1.1 核心框架 (Core Framework)
React 19.2.3

利用最新的 React Hooks (useState, useEffect, useRef, useMemo, useCallback) 進行狀態管理與效能優化。
採用 Function Components 確保程式碼的可維護性與模組化。
實作 Error Boundaries 進行優雅的錯誤處理與使用者體驗保護。
使用 React.lazy 與 Suspense 實現程式碼分割 (Code Splitting)，優化首次載入速度。

2.1.2 建置工具 (Build Tool)
Vite 7.2.7

提供閃電般的熱模組替換 (Hot Module Replacement, HMR) 開發體驗，變更即時反映。
優化 Production Build，自動進行 Tree Shaking、Minification 與 Asset Optimization。
原生支援 ES Modules (ESM)，無需複雜的 Webpack 配置。
整合 Rollup 進行高效的 Bundle 產出，支援 Legacy Browser Polyfills。

2.1.3 語言標準 (Language)
TypeScript 5.7

全面採用強型別定義，確保大型專案開發的穩定性與團隊協作效率。
利用 Interface、Type Alias、Generics 與 Union Types 建立嚴謹的型別系統。
整合 ESLint 與 Prettier 進行程式碼品質管控與自動格式化。
啟用 Strict Mode 與 No Implicit Any，杜絕型別漏洞。

2.1.4 樣式系統 (Styling)
Tailwind CSS 3.4

Utility-first CSS 框架，實現快速原型開發與一致的設計語言。
自定義配置 (tailwind.config.js) 支援動態主題、玻璃擬態 (Glassmorphism) 與漸層色系。
使用 JIT (Just-In-Time) 編譯模式，僅產出實際使用的 CSS，減少最終 Bundle 體積。
整合 PostCSS 進行 Autoprefixer 與 CSS Minification。

2.1.5 AI 推論層 (AI Inference Layer)
Google GenAI SDK (@google/genai)

直接介接 Gemini 2.5 Flash 與 Gemini 2.5 Flash-Lite 模型。
支援 Streaming Response，實現打字機效果的即時輸出。
內建 Token Counting 與 Safety Settings 管理。
實作 Retry Logic 與 Exponential Backoff 處理 API 限流 (Rate Limiting)。

2.1.6 視覺化圖表 (Visualization)
Recharts

用於儀表板的統計圖表 (AreaChart, BarChart, LineChart, PieChart)。
支援響應式設計與主題自定義。
內建動畫效果與互動式 Tooltip。

HTML5 Canvas

用於 Agent Network 的粒子特效與即時運算渲染。
實作 RequestAnimationFrame 迴圈，達成 60FPS 流暢動畫。
支援動態節點連接、脈衝波紋與顏色漸變效果。

Lucide React

統一的向量圖標庫，提供超過 1000+ 高品質 SVG 圖標。
支援動態尺寸、顏色與 Stroke Width 調整。
輕量化設計，按需引入 (Tree-shakable)。

2.1.7 資料處理 (Data Processing)
js-yaml

用於解析 YAML 格式的代理人定義檔 (agents.yaml)。
支援複雜的巢狀結構與多行字串 (Multiline Strings)。
實作 Schema Validation 確保配置檔格式正確性。

pdf.js (未來整合)

用於更進階的 PDF 解析需求，如提取嵌入式表格、圖片與元數據。

2.2 資料流架構 (Data Flow Architecture)
系統採用單向資料流 (Unidirectional Data Flow) 與狀態提升 (State Lifting) 相結合的模式,確保資料流的可預測性與除錯便利性。
2.2.1 五層架構模型
第一層：輸入層 (Input Layer)

使用者透過 FileProcessor 元件上傳 PDF、TXT、Markdown 或 JSON 檔案。
支援拖放 (Drag & Drop) 與點擊上傳兩種互動方式。
檔案大小限制：單檔最大 50MB，總計最大 200MB。
即時顯示上傳進度條與檔案預覽縮圖。

第二層：預處理層 (Preprocessing Layer)

檔案透過 Gemini Vision API 進行 LLM-based OCR，轉換為結構化純文字 Context。
針對 PDF 檔案，使用 FileReader.readAsDataURL() 轉換為 Base64 編碼。
實作頁面範圍選擇 (Page Range Selection)，如 "1-5, 10, 15-20"，以節省 Token 用量與處理時間。
支援多語言文件 (中文、英文、日文)，自動偵測與轉換編碼 (UTF-8, Big5, Shift-JIS)。

第三層：狀態層 (State Layer)

轉換後的 processedContext 被提升至 App.tsx，作為全域狀態供下游模組使用。
使用 React Context API 或 Zustand 進行跨元件狀態管理 (視專案規模而定)。
實作 useReducer 處理複雜的狀態轉換邏輯 (如代理人執行狀態機)。

第四層：編排層 (Orchestration Layer)

AgentOrchestrator 讀取 agents.yaml 定義檔與 Context，並根據使用者選取的模型發送異步請求。
實作工作佇列 (Job Queue) 機制，支援批次執行與優先級排程。
支援平行執行 (Parallel Execution) 與依賴鏈執行 (Sequential Execution)，根據代理人定義的 dependencies 欄位自動排程。
整合 Circuit Breaker 模式，當連續失敗次數超過閾值時自動熔斷保護。

第五層：呈現層 (Presentation Layer)

執行結果即時回傳並儲存於 Component State，透過 TerminalLog 與 AgentNetwork 進行視覺化反饋。
支援多種輸出格式：Markdown、JSON、HTML、PDF (匯出功能)。
實作 WebSocket 或 Server-Sent Events (SSE) 模擬即時串流輸出 (在完全本地執行的限制下,透過 Chunked Streaming 實現)。

2.2.2 資料流時序圖 (Sequence Diagram)
Copy使用者 → FileProcessor → OCR Service → App State
                                          ↓
                                    AgentOrchestrator
                                    ↓     ↓     ↓
                                Agent1 Agent2 Agent3
                                    ↓     ↓     ↓
                                  Result Aggregator
                                          ↓
                                  UI Components
                                (Dashboard, Logs, Network)
2.3 安全性與隱私設計 (Security & Privacy)
本系統採用零信任架構 (Zero Trust Architecture) 與隱私設計 (Privacy by Design) 原則。
2.3.1 API Key 管理
環境變數優先策略

系統優先讀取 import.meta.env.VITE_API_KEY 環境變數。
適用於開發環境與內部演示場景。
部署時透過 CI/CD Pipeline 自動注入，不納入版本控制。

本地存儲機制

若無環境變數，使用者需透過 Sidebar 輸入 API Key。
該 Key 僅存於 React State (記憶體) 中，絕不傳送至任何第三方後端伺服器 (除了直接發送給 Google API)。
支援 LocalStorage 加密儲存 (可選)，使用 AES-256-GCM 演算法，密鑰由使用者主密碼 (Master Password) 派生。

安全性最佳實踐

API Key 顯示時自動遮罩 (Masking)，僅顯示前 4 位與後 4 位。
實作 Key Rotation 提醒機制，每 90 天提示使用者更新。
支援多組 Key 輪替使用，避免單一 Key 配額耗盡。

2.3.2 無後端儲存 (Backendless Storage)
資料不落地原則

本系統不設後端資料庫，所有文件與審查結果僅存在於使用者的瀏覽器 Session 中。
頁面刷新即清空所有資料，確保機敏資料不落地。
適用於高度敏感的醫療器材審查文件,符合 HIPAA、GDPR 等隱私法規。

可選持久化方案

支援匯出為加密 JSON 檔案 (使用者自行保管)。
整合 IndexedDB 進行本地暫存 (需使用者明確授權)。
未來可擴展支援 去中心化儲存 (IPFS) 或 私有區塊鏈。

2.3.3 文件處理安全性
Base64 編碼傳輸

文件內容轉換為 Base64 後直接透過 HTTPS 傳送至 Gemini API，不經過中繼伺服器。
傳輸過程啟用 TLS 1.3 加密，確保端到端安全。

內容安全政策 (Content Security Policy, CSP)

實作嚴格的 CSP Headers，防止 XSS 攻擊。
禁止內聯腳本 (Inline Scripts) 與不安全的 eval()。

子資源完整性 (Subresource Integrity, SRI)

所有外部 CDN 資源 (如 Google Fonts) 均啟用 SRI 校驗，防止供應鏈攻擊。

2.3.4 存取控制與稽核
角色基礎存取控制 (RBAC)

定義四種角色：Admin (系統管理員)、Senior Reviewer (資深審查員)、Reviewer (審查員)、Guest (訪客)。
不同角色擁有不同的功能權限 (如 Guest 僅能查看 Demo 模式)。

操作日誌 (Audit Log)

記錄所有關鍵操作：檔案上傳、代理人執行、結果匯出。
日誌包含時間戳記、使用者 ID、操作類型、IP 位址 (可選)。
支援匯出為 CSV 或 JSON 格式供合規性稽核使用。


3. 核心功能模組詳解 (Core Modules)
3.1 智慧儀表板 (Cinematic Dashboard)
智慧儀表板位於系統首頁，提供宏觀的審查狀態概覽與系統健康監控。
3.1.1 功能描述
系統狀態監控

運作狀態指示器：顯示系統當前狀態 (Operational / Processing / Maintenance / Error)。
心跳動畫：模擬伺服器心跳，使用 animate-pulse CSS 類別實現呼吸燈效果。
活躍代理人計數：即時顯示正在執行的代理人數量 (Active Agent Nodes)。

資安等級展示

加密狀態指示：顯示資料傳輸加密等級 (TLS 1.3, AES-256)。
合規性標章：展示符合的法規標準 (ISO 13485, FDA 21 CFR Part 11, GDPR)。

向量資料庫連線狀態模擬

雖然本系統為無後端架構，但儀表板模擬了未來可能整合的向量資料庫 (如 Pinecone, Weaviate) 連線狀態。
顯示向量索引數量、查詢延遲與快取命中率 (模擬數據)。

3.1.2 技術實作
圖表繪製

使用 Recharts 繪製 AreaChart (效率分析) 與 BarChart (案件量分析)。
資料來源：從 mockData.ts 引入模擬數據，展示過去 30 天的審查趨勢。
響應式設計：圖表自動適應容器寬度，支援移動端查看。

動畫效果

實作自定義 CSS 動畫：

animate-pulse：用於狀態指示燈的脈衝效果。
animate-ping：用於新通知的波紋擴散效果。
animate-spin：用於載入中的旋轉圖標。


所有動畫支援 prefers-reduced-motion 媒體查詢，尊重使用者的無障礙設定。

互動性

圖表支援 Tooltip 懸停顯示詳細數據 (日期、案件數、審查時長)。
點擊圖表區域可深入查看該時間段的詳細日誌。
根據亮/暗色主題自動切換配色方案 (使用 Tailwind 的 dark: 修飾符)。

效能監控卡片

顯示關鍵指標：

平均審查時長 (Average Review Time)
Token 使用量 (Token Consumption)
審查通過率 (Approval Rate)
系統可用性 (System Uptime)



3.1.3 程式碼範例
typescriptCopy// Dashboard.tsx
import { AreaChart, Area, XAxis, YAxis, Tooltip, ResponsiveContainer } from 'recharts';

const Dashboard: React.FC = () => {
  const [systemStatus, setSystemStatus] = useState<'operational' | 'processing'>('operational');
  
  return (
    <div className="glass-panel p-6 rounded-xl">
      <div className="flex items-center gap-3 mb-6">
        <div className={`w-3 h-3 rounded-full ${systemStatus === 'operational' ? 'bg-green-500 animate-pulse' : 'bg-yellow-500 animate-ping'}`} />
        <h2 className="text-2xl font-bold">系統狀態監控</h2>
      </div>
      
      <ResponsiveContainer width="100%" height={300}>
        <AreaChart data={efficiencyData}>
          <defs>
            <linearGradient id="colorUv" x1="0" y1="0" x2="0" y2="1">
              <stop offset="5%" stopColor="#8b5cf6" stopOpacity={0.8}/>
              <stop offset="95%" stopColor="#8b5cf6" stopOpacity={0}/>
            </linearGradient>
          </defs>
          <XAxis dataKey="date" />
          <YAxis />
          <Tooltip />
          <Area type="monotone" dataKey="efficiency" stroke="#8b5cf6" fillOpacity={1} fill="url(#colorUv)" />
        </AreaChart>
      </ResponsiveContainer>
    </div>
  );
};
3.2 文件攝取與多模態 OCR (Ingestion & Multimodal OCR)
此模組負責將非結構化的醫療器材文件轉換為機器可讀的 Context，是整個系統的資料入口。
3.2.1 功能描述
多格式支援

PDF：支援標準 PDF、掃描式 PDF (Image-based PDF) 與混合式 PDF。
文字檔案：TXT, Markdown (.md), CSV。
結構化資料：JSON, XML, YAML。
圖片格式：PNG, JPG, TIFF (用於單頁文件或圖表)。
Office 文件 (未來支援)：DOCX, XLSX, PPTX。

LLM-OCR 技術

利用 Gemini Vision API 的多模態能力，直接對 PDF 頁面或圖片進行視覺理解與文字轉錄。
優勢：

保留版面結構：能識別表格、清單、標題階層。
專業術語準確性：對醫療領域的專有名詞 (如藥品成分、手術術式) 有更高的識別率。
多語言混合：同一頁面中的中英文混合內容能正確分離與翻譯。


與傳統 Tesseract OCR 的比較：

特性LLM-OCR (Gemini)Tesseract OCR準確率95-98%85-90%表格識別優秀需額外處理手寫文字支援不支援處理速度慢 (API 呼叫)快 (本地運算)成本按 Token 計費免費
頁面範圍指定

支援靈活的頁碼表達式：

單頁："5"
連續範圍："1-10"
不連續頁面："1, 5, 10-15, 20"
從末頁倒數："-5" (最後 5 頁)


即時預覽選取的頁面，避免誤選。

批次處理

支援一次上傳多個檔案，自動排隊處理。
顯示整體處理進度與預估剩餘時間。

3.2.2 技術實作
檔案讀取
typescriptCopy// fileUtils.ts
export const readFileAsBase64 = (file: File): Promise<string> => {
  return new Promise((resolve, reject) => {
    const reader = new FileReader();
    reader.onload = () => {
      const base64String = reader.result as string;
      // 移除 Data URL 前綴 (data:application/pdf;base64,)
      const base64Data = base64String.split(',')[1];
      resolve(base64Data);
    };
    reader.onerror = reject;
    reader.readAsDataURL(file);
  });
};
LLM-OCR 服務
typescriptCopy// geminiService.ts
export const performLLMOCR = async (
  base64Data: string,
  mimeType: string,
  pageRange?: string
): Promise<string> => {
  const model = genAI.getGenerativeModel({ model: "gemini-2.5-flash" });
  
  const prompt = `You are an expert OCR system specialized in medical device documentation.

TASK: Extract all text content from the provided document image(s).

REQUIREMENTS:
1. Maintain the original formatting layout (headings, paragraphs, lists, tables).
2. Preserve technical terminology exactly as shown.
3. For tables, output in Markdown table format.
4. Indicate any unclear or illegible text with [UNCLEAR].
5. If multiple languages are present, preserve them as-is.

${pageRange ? `PROCESS ONLY PAGES: ${pageRange}` : 'PROCESS ALL PAGES'}

OUTPUT FORMAT: Pure Markdown text.`;

  const result = await model.generateContent([
    {
      inlineData: {
        mimeType: mimeType,
        data: base64Data
      }
    },
    prompt
  ]);
  
  return result.response.text();
};
元件實作
typescriptCopy// FileProcessor.tsx
const FileProcessor: React.FC<FileProcessorProps> = ({ onProcessComplete }) => {
  const [selectedFile, setSelectedFile] = useState<File | null>(null);
  const [pageRange, setPageRange] = useState<string>('');
  const [isProcessing, setIsProcessing] = useState(false);
  const [progress, setProgress] = useState(0);

  const handleFileUpload = async () => {
    if (!selectedFile) return;
    
    setIsProcessing(true);
    try {
      const base64Data = await readFileAsBase64(selectedFile);
      const mimeType = selectedFile.type;
      
      // 模擬進度更新
      const progressInterval = setInterval(() => {
        setProgress(prev => Math.min(prev + 10, 90));
      }, 500);
      
      const extractedText = await performLLMOCR(base64Data, mimeType, pageRange);
      
      clearInterval(progressInterval);
      setProgress(100);
      
      onProcessComplete(extractedText);
    } catch (error) {
      console.error('OCR failed:', error);
      // 錯誤處理
    } finally {
      setIsProcessing(false);
    }
  };

  return (
    <div className="glass-panel p-6">
      <input 
        type="file" 
        accept=".pdf,.txt,.md,.json"
        onChange={(e) => setSelectedFile(e.target.files?.[0] || null)}
      />
      <input
        type="text"
        placeholder="頁碼範圍 (例: 1-5, 10)"
        value={pageRange}
        onChange={(e) => setPageRange(e.target.value)}
      />
      <button onClick={handleFileUpload} disabled={isProcessing}>
        {isProcessing ? `處理中... ${progress}%` : '開始處理'}
      </button>
    </div>
  );
};
3.3 代理人編排器 (Agent Orchestrator)
這是系統的核心大腦，負責管理與執行 AI 代理人。
3.3.1 功能描述
YAML 定義驅動

代理人的角色、任務與系統提示詞 (System Prompt) 定義於 agents.yaml 檔案中。
支援動態匯入/匯出，方便審查員自定義專屬代理人。
YAML 結構範例：

yamlCopyagents:
  - id: clinical-evaluator
    name: 臨床評估專家
    role: Clinical Evaluation Specialist
    description: 評估臨床試驗數據的完整性與科學性
    systemPrompt: |
      You are a clinical evaluation expert with 15 years of experience in medical device assessment.
      Your task is to review clinical trial data and identify any gaps or inconsistencies.
      Focus on: sample size adequacy, endpoint selection, statistical methodology, adverse events reporting.
    dependencies: []
    priority: 1
    
  - id: electrical-safety
    name: 電氣安全審查員
    role: Electrical Safety Reviewer
    description: 檢查電氣安全標準符合性 (IEC 60601-1)
    systemPrompt: |
      You are an electrical safety engineer specializing in IEC 60601-1 standard compliance.
      Review the provided technical documentation for electrical safety requirements.
    dependencies: []
    priority: 2
批次/平行執行

支援同時選取多個代理人進行審查。
執行模式:

平行模式 (Parallel)：所有代理人同時執行，適用於獨立任務。
序列模式 (Sequential)：按優先級依次執行，適用於有依賴關係的任務。
混合模式 (Hybrid)：根據 dependencies 欄位自動判斷。



即時日誌 (Live Terminal)

模擬 Linux 終端機介面 (Terminal Emulator)，顯示詳細的執行 Log。
日誌類型：

[INFO]：一般資訊
[SUCCESS]：成功訊息 (綠色)
[WARNING]：警告訊息 (黃色)
[ERROR]：錯誤訊息 (紅色)
[SYSTEM]：系統訊息 (藍色)


支援日誌過濾、搜尋與匯出。

神經網絡視覺化 (Neural Network View)

一個基於 HTML5 Canvas 的即時動畫，顯示中心節點 (Hub) 與代理人節點 (Nodes) 的連接狀態。
視覺元素：

中心節點：代表 Orchestrator。
代理人節點：環繞中心節點排列，顏色代表狀態 (灰色=閒置, 藍色=執行中, 綠色=完成, 紅色=失敗)。
連接線：動態脈衝線條,表示資料傳輸。
粒子效果：沿連接線移動的光點,模擬資訊流動。



3.3.2 技術實作
狀態機設計
typescriptCopy// types.ts
type AgentStatus = 'idle' | 'running' | 'completed' | 'failed';

interface Agent {
  id: string;
  name: string;
  status: AgentStatus;
  output: string;
  error?: string;
  startTime?: Date;
  endTime?: Date;
  tokenUsage?: number;
}
編排器核心邏輯
typescriptCopy// AgentOrchestrator.tsx
const AgentOrchestrator: React.FC = () => {
  const [agents, setAgents] = useState<Agent[]>([]);
  const [selectedAgentIds, setSelectedAgentIds] = useState<string[]>([]);
  const [isBusy, setIsBusy] = useState(false);
  const [logs, setLogs] = useState<LogEntry[]>([]);

  const executeAgents = async () => {
    setIsBusy(true);
    addLog('SYSTEM', '開始執行代理人任務', 'system');

    try {
      // 根據 dependencies 建立執行順序
      const executionPlan = buildExecutionPlan(selectedAgentIds);
      
      for (const batch of executionPlan) {
        // 平行執行同一批次的代理人
        await Promise.all(
          batch.map(agentId => executeAgent(agentId))
        );
      }
      
      addLog('SYSTEM', '所有任務執行完成', 'success');
    } catch (error) {
      addLog('SYSTEM', `執行失敗: ${error}`, 'error');
    } finally {
      setIsBusy(false);
    }
  };

  const executeAgent = async (agentId: string) => {
    const agent = agents.find(a => a.id === agentId);
    if (!agent) return;

    updateAgentStatus(agentId, 'running');
    addLog(agent.name, '開始執行...', 'info');

    try {
      const result = await callGeminiAPI(agent.systemPrompt, processedContext);
      
      updateAgent(agentId, {
        status: 'completed',
        output: result.text,
        tokenUsage: result.tokenCount
      });
      
      addLog(agent.name, '執行完成', 'success');
    } catch (error) {
      updateAgent(agentId, {
        status: 'failed',
        error: error.message
      });
      
      addLog(agent.name, `執行失敗: ${error.message}`, 'error');
    }
  };

  return (
    <div className="grid grid-cols-2 gap-6">
      <div className="glass-panel p-6">
        <h2>代理人選擇</h2>
        {/* Agent selection UI */}
        <button onClick={executeAgents} disabled={isBusy}>
          執行選取的代理人
        </button>
      </div>
      
      <div className="glass-panel p-6">
        <AgentNetwork agents={agents} isBusy={isBusy} />
      </div>
      
      <div className="col-span-2">
        <TerminalLog logs={logs} />
      </div>
    </div>
  );
};
Canvas 神經網絡渲染
typescriptCopy// AgentNetwork.tsx
const AgentNetwork: React.FC<{ agents: Agent[], isBusy: boolean }> = ({ agents, isBusy }) => {
  const canvasRef = useRef<HTMLCanvasElement>(null);
  const particlesRef = useRef<Particle[]>([]);

  useEffect(() => {
    const canvas = canvasRef.current;
    if (!canvas) return;

    const ctx = canvas.getContext('2d');
    if (!ctx) return;

    const centerX = canvas.width / 2;
    const centerY = canvas.height / 2;
    const radius = 150;

    const animate = () => {
      // 清空畫布
      ctx.clearRect(0, 0, canvas.width, canvas.height);

      // 繪製中心節點
      ctx.beginPath();
      ctx.arc(centerX, centerY, 20, 0, Math.PI * 2);
      ctx.fillStyle = isBusy ? '#ef4444' : '#3b82f6';
      ctx.fill();

      // 繪製代理人節點
      agents.forEach((agent, index) => {
        const angle = (index / agents.length) * Math.PI * 2;
        const x = centerX + radius * Math.cos(angle);
        const y = centerY + radius * Math.sin(angle);

        // 繪製連接線
        ctx.beginPath();
        ctx.moveTo(centerX, centerY);
        ctx.lineTo(x, y);
        ctx.strokeStyle = getStatusColor(agent.status);
        ctx.stroke();

        // 繪製節點
        ctx.beginPath();
        ctx.arc(x, y, 12, 0, Math.PI * 2);
        ctx.fillStyle = getStatusColor(agent.status);
        ctx.fill();

        // 節點標籤
        ctx.fillStyle = '#ffffff';
        ctx.font = '10px sans-serif';
        ctx.fillText(agent.name, x - 20, y + 25);
      });

      // 繪製粒子
      updateParticles();
      drawParticles(ctx);

      requestAnimationFrame(animate);
    };

    animate();
  }, [agents, isBusy]);

  return <canvas ref={canvasRef} width={600} height={600} className="w-full h-full" />;
};

const getStatusColor = (status: AgentStatus): string => {
  switch (status) {
    case 'idle': return '#6b7280';
    case 'running': return '#3b82f6';
    case 'completed': return '#10b981';
    case 'failed': return '#ef4444';
  }
};
3.4 智慧筆記中樞 (Intelligence Hub)
位於右側的常駐面板，輔助審查員進行知識管理與決策記錄。
3.4.1 功能描述
Markdown 編輯/預覽

雙模式切換：編輯模式與預覽模式。
支援完整的 Markdown 語法：標題、清單、表格、程式碼區塊、引用。
即時預覽：編輯時右側即時顯示渲染結果。
語法高亮：程式碼區塊自動識別語言並套用語法高亮。

AI Magic Buttons
提供四種 AI 輔助功能，透過單鍵操作即可智慧化處理筆記內容：

Format (格式化)

自動排版雜亂的筆記。
統一標題層級、清單格式。
移除多餘的空白行與不一致的縮排。


Summarize (摘要)

生成行政摘要 (Executive Summary)。
提取關鍵發現 (Key Findings)。
適用於將長篇審查報告濃縮為簡報用的重點。


Action Items (待辦事項)

自動識別筆記中的待辦事項。
提取為結構化的 Checklist。
標註優先級與負責人 (如有提及)。


Translate (翻譯)

中英互譯。
保留專業術語的一致性 (透過預定義的術語庫)。
適用於撰寫雙語報告。



範本庫

內建常用的審查報告範本：

FDA 510(k) 審查報告範本
CE Mark 技術文件範本
TFDA 醫療器材查驗登記範本


支援使用者自定義範本。

3.4.2 技術實作
元件架構
typescriptCopy// NoteKeeper.tsx
const NoteKeeper: React.FC = () => {
  const [noteContent, setNoteContent] = useState<string>('');
  const [mode, setMode] = useState<'edit' | 'preview'>('edit');
  const [isTransforming, setIsTransforming] = useState(false);

  const handleMagicButton = async (action: 'format' | 'summarize' | 'actionItems' | 'translate') => {
    setIsTransforming(true);
    
    try {
      const transformedText = await transformNote(noteContent, action);
      setNoteContent(transformedText);
    } catch (error) {
      console.error('Note transformation failed:', error);
    } finally {
      setIsTransforming(false);
    }
  };

  return (
    <div className="glass-panel p-6 h-full flex flex-col">
      <div className="flex items-center justify-between mb-4">
        <h2 className="text-xl font-bold">智慧筆記</h2>
        <div className="flex gap-2">
          <button onClick={() => setMode('edit')}>編輯</button>
          <button onClick={() => setMode('preview')}>預覽</button>
        </div>
      </div>

      <div className="flex-1 overflow-auto">
        {mode === 'edit' ? (
          <textarea
            value={noteContent}
            onChange={(e) => setNoteContent(e.target.value)}
            className="w-full h-full p-4 font-mono"
            placeholder="在此輸入您的審查筆記..."
          />
        ) : (
          <div 
            className="prose dark:prose-invert max-w-none p-4"
            dangerouslySetInnerHTML={{ __html: markdownToHtml(noteContent) }}
          />
        )}
      </div>

      <div className="flex gap-2 mt-4">
        <button onClick={() => handleMagicButton('format')} disabled={isTransforming}>
          <Wand2 className="w-4 h-4 mr-2" />
          格式化
        </button>
        <button onClick={() => handleMagicButton('summarize')} disabled={isTransforming}>
          <FileText className="w-4 h-4 mr-2" />
          摘要
        </button>
        <button onClick={() => handleMagicButton('actionItems')} disabled={isTransforming}>
          <CheckSquare className="w-4 h-4 mr-2" />
          待辦事項
        </button>
        <button onClick={() => handleMagicButton('translate')} disabled={isTransforming}>
          <Languages className="w-4 h-4 mr-2" />
          翻譯
        </button>
      </div>

      {isTransforming && (
        <div className="absolute inset-0 bg-black/50 flex items-center justify-center">
          <div className="text-white">AI 處理中...</div>
        </div>
      )}
    </div>
  );
};
AI 轉換服務
typescriptCopy// geminiService.ts
export const transformNote = async (
  noteContent: string,
  action: 'format' | 'summarize' | 'actionItems' | 'translate'
): Promise<string> => {
  const model = genAI.getGenerativeModel({ model: "gemini-2.5-flash" });

  const prompts = {
    format: `Format the following note with consistent heading levels, proper list formatting, and remove extra whitespace:\n\n${noteContent}`,
    
    summarize: `Generate a concise executive summary of the following review note:\n\n${noteContent}`,
    
    actionItems: `Extract all action items from the following note and format them as a prioritized checklist:\n\n${noteContent}`,
    
    translate: `Translate the following text between English and Traditional Chinese. If it's in English, translate to Chinese; if in Chinese, translate to English. Preserve technical terminology:\n\n${noteContent}`
  };

  const result = await model.generateContent(prompts[action]);
  return result.response.text();
};
3.5 全域設定與側邊欄 (Global Configuration)
3.5.1 功能描述
隱藏式側邊欄 (Sidebar)

透過漢堡選單 (Hamburger Menu) 圖標觸發。
從左側滑入，覆蓋式設計 (Overlay)。
包含以下設定項目：

API Key 設定
模型選擇 (Gemini 2.5 Flash / Flash-Lite)
主題切換 (藝術家風格)
語言設定 (繁中/英文)
關於頁面 (系統版本、授權資訊)



API Key 狀態顯示

顯示 Key 來源：環境變數或使用者輸入。
Key 健康檢查：自動驗證 Key 的有效性與剩餘配額。
安全指示器：顯示 Key 是否已加密儲存。

系統版本與環境資訊

顯示當前版本號 (v4.2.0)。
Build 時間與 Git Commit Hash。
瀏覽器相容性資訊。

3.5.2 技術實作
typescriptCopy// Sidebar.tsx
const Sidebar: React.FC<{ isOpen: boolean, onClose: () => void }> = ({ isOpen, onClose }) => {
  const [apiKey, setApiKey] = useState<string>('');
  const [keySource, setKeySource] = useState<'env' | 'user'>('env');

  useEffect(() => {
    const envKey = import.meta.env.VITE_API_KEY;
    if (envKey) {
      setApiKey(envKey);
      setKeySource('env');
    }
  }, []);

  return (
    <>
      {/* Backdrop */}
      {isOpen && (
        <div 
          className="fixed inset-0 bg-black/50 backdrop-blur-sm z-40"
          onClick={onClose}
        />
      )}

      {/* Sidebar */}
      <div className={`
        fixed top-0 left-0 h-full w-80 bg-white dark:bg-gray-900 
        shadow-2xl z-50 transition-transform duration-300
        ${isOpen ? 'translate-x-0' : '-translate-x-full'}
      `}>
        <div className="p-6">
          <div className="flex items-center justify-between mb-6">
            <h2 className="text-2xl font-bold">系統設定</h2>
            <button onClick={onClose}>
              <X className="w-6 h-6" />
            </button>
          </div>

          {/* API Key Section */}
          <div className="mb-6">
            <label className="block text-sm font-medium mb-2">
              API Key
              <span className="ml-2 text-xs text-gray-500">
                ({keySource === 'env' ? '環境變數' : '使用者輸入'})
              </span>
            </label>
            <input
              type="password"
              value={apiKey}
              onChange={(e) => setApiKey(e.target.value)}
              placeholder="輸入您的 Gemini API Key"
              className="w-full p-2 border rounded"
              disabled={keySource === 'env'}
            />
          </div>

          {/* Model Selection */}
          <div className="mb-6">
            <label className="block text-sm font-medium mb-2">模型選擇</label>
            <select className="w-full p-2 border rounded">
              <option value="gemini-2.5-flash">Gemini 2.5 Flash</option>
              <option value="gemini-2.5-flash-lite">Gemini 2.5 Flash-Lite</option>
            </select>
          </div>

          {/* Version Info */}
          <div className="mt-auto pt-6 border-t">
            <p className="text-sm text-gray-600">版本: v4.2.0</p>
            <p className="text-sm text-gray-600">Build: 2025-12-15</p>
          </div>
        </div>
      </div>
    </>
  );
};

4. UI/UX 設計系統 (Design System)
本系統採用 "Cinematic Modernism" 設計語言，結合了未來科技感與古典藝術美學，打造沉浸式的使用者體驗。
4.1 藝術風格引擎 (Painter Style Engine)
系統內建強大的主題切換引擎，不僅改變顏色，更改變整體氛圍與情感基調。
4.1.1 風格定義
系統支援超過 20 種藝術家風格，每種風格包含以下元素：
typescriptCopy// types.ts
interface PainterStyle {
  id: string;
  name: string;
  bg: string;          // 背景漸層 CSS
  accent: string;      // 強調色
  font: 'serif' | 'sans' | 'mono';  // 字體系列
  description: string;
}

const painterStyles: PainterStyle[] = [
  {
    id: 'vangogh',
    name: 'Van Gogh',
    bg: 'linear-gradient(135deg, #667eea 0%, #764ba2 100%)',
    accent: '#f59e0b',
    font: 'serif',
    description: '星夜般的渦旋與濃烈的情感'
  },
  {
    id: 'monet',
    name: 'Monet',
    bg: 'linear-gradient(135deg, #a8edea 0%, #fed6e3 100%)',
    accent: '#10b981',
    font: 'serif',
    description: '印象派的柔和光影與水面倒影'
  },
  {
    id: 'cyberpunk',
    name: 'Cyberpunk',
    bg: 'linear-gradient(135deg, #0f0c29 0%, #302b63 50%, #24243e 100%)',
    accent: '#ff006e',
    font: 'mono',
    description: '霓虹燈海與賽博朋克的未來感'
  },
  // ... 更多風格
];
4.1.2 動態注入機制
StyleSelector 元件
實作類似拉霸機 (Slot Machine) 的互動效果，讓風格切換充滿趣味性：
typescriptCopy// StyleSelector.tsx
const StyleSelector: React.FC<{ currentStyle: string, onStyleChange: (style: string) => void }> = ({ currentStyle, onStyleChange }) => {
  const [isSpinning, setIsSpinning] = useState(false);

  const randomizeStyle = () => {
    setIsSpinning(true);
    
    // 拉霸機動畫：快速切換風格
    let count = 0;
    const interval = setInterval(() => {
      const randomStyle = painterStyles[Math.floor(Math.random() * painterStyles.length)];
      onStyleChange(randomStyle.id);
      count++;
      
      if (count > 20) {
        clearInterval(interval);
        setIsSpinning(false);
      }
    }, 100);
  };

  return (
    <div className="flex items-center gap-4">
      <div className="grid grid-cols-4 gap-2">
        {painterStyles.map(style => (
          <button
            key={style.id}
            onClick={() => onStyleChange(style.id)}
            className={`
              w-16 h-16 rounded-lg border-2 transition-all
              ${currentStyle === style.id ? 'border-white scale-110' : 'border-transparent'}
            `}
            style={{ background: style.bg }}
            title={style.name}
          />
        ))}
      </div>
      
      <button
        onClick={randomizeStyle}
        disabled={isSpinning}
        className="px-4 py-2 bg-purple-600 hover:bg-purple-700 rounded-lg"
      >
        <Shuffle className="w-5 h-5" />
        {isSpinning ? '抽選中...' : '隨機風格'}
      </button>
    </div>
  );
};
全域樣式注入
當風格改變時，系統會動態更新 CSS 變數與 Tailwind 類別：
typescriptCopy// App.tsx
const App: React.FC = () => {
  const [painterStyle, setPainterStyle] = useState<string>('cyberpunk');

  useEffect(() => {
    const style = painterStyles.find(s => s.id === painterStyle);
    if (!style) return;

    // 注入 CSS 變數
    document.documentElement.style.setProperty('--bg-gradient', style.bg);
    document.documentElement.style.setProperty('--accent-color', style.accent);
    document.body.style.fontFamily = style.font === 'serif' ? 'Georgia, serif' : 
                                     style.font === 'mono' ? 'monospace' : 'sans-serif';
  }, [painterStyle]);

  return (
    <div 
      className="min-h-screen transition-all duration-700"
      style={{ background: 'var(--bg-gradient)' }}
    >
      {/* App content */}
    </div>
  );
};
4.2 視覺化互動設計 (Visualization & Interactions)
4.2.1 玻璃擬態 (Glassmorphism)
自定義 CSS 類別 .glass-panel，實現半透明玻璃質感：
cssCopy/* styles.css */
.glass-panel {
  @apply bg-white/60 dark:bg-gray-900/60 
         backdrop-blur-md 
         border border-white/20 dark:border-white/10 
         shadow-lg 
         rounded-xl;
}
此設計確保內容在複雜的漸層背景上依然清晰可讀，並營造出未來科技感的層次結構。
4.2.2 微互動 (Micro-interactions)
按鈕懸停效果
cssCopy.btn-primary {
  @apply px-4 py-2 bg-purple-600 text-white rounded-lg
         transition-all duration-200
         hover:scale-105 hover:shadow-xl hover:bg-purple-700;
}
系統忙碌指示
當系統執行任務時，多處 UI 元素會同步反應：

Logo 旁的狀態燈號從藍色脈衝轉為紅色快閃
Agent Network 的連接線顏色從藍色漸變為紅色
儀表板的「處理中」標籤出現旋轉動畫

typescriptCopy// 狀態燈號元件
const StatusIndicator: React.FC<{ isBusy: boolean }> = ({ isBusy }) => (
  <div className={`
    w-3 h-3 rounded-full
    ${isBusy ? 'bg-red-500 animate-ping' : 'bg-blue-500 animate-pulse'}
  `} />
);
側邊欄滑入動畫
cssCopy.sidebar {
  @apply fixed top-0 left-0 h-full w-80
         transition-transform duration-300 ease-out;
}

.sidebar-open {
  @apply translate-x-0;
}

.sidebar-closed {
  @apply -translate-x-full;
}

5. AI 模型整合策略 (AI Integration Strategy)
5.1 Google Gemini API 實作
系統核心依賴 @google/genai SDK，採用最新的 Gemini 2.5 系列模型。
5.1.1 模型選擇策略
Gemini 2.5 Flash (主要模型)

用途：主要推理任務、OCR、筆記轉換、複雜審查邏輯
優勢：

速度快 (平均響應時間 < 2秒)
成本低 (比 Pro 模型便宜 80%)
Context Window 大 (最高 1M tokens)
支援 Thinking Budget (隱式推理鏈)


限制：

複雜數學推理能力較 Pro 模型弱
長文檔理解極限約 100萬 tokens



Gemini 2.5 Flash-Lite (輔助模型)

用途：極輕量任務 (如格式化、簡單分類)
優勢：速度極快、成本極低
限制：推理能力有限，不適合複雜任務

模型選擇邏輯
typescriptCopy// geminiService.ts
const selectModel = (taskComplexity: 'low' | 'medium' | 'high'): string => {
  switch (taskComplexity) {
    case 'low':
      return 'gemini-2.5-flash-lite';
    case 'medium':
    case 'high':
    default:
      return 'gemini-2.5-flash';
  }
};
5.1.2 Client端封裝
單例模式 (Singleton Pattern)
確保整個應用只有一個 GoogleGenAI 實例，避免重複初始化：
typescriptCopy// geminiService.ts
import { GoogleGenerativeAI } from '@google/genai';

let genAIInstance: GoogleGenerativeAI | null = null;

export const initializeGenAI = (apiKey: string): void => {
  if (!genAIInstance) {
    genAIInstance = new GoogleGenerativeAI(apiKey);
  }
};

export const getGenAI = (): GoogleGenerativeAI => {
  if (!genAIInstance) {
    throw new Error('GenAI not initialized. Call initializeGenAI first.');
  }
  return genAIInstance;
};
錯誤處理機制
typescriptCopyexport const callGeminiAPI = async (
  systemPrompt: string,
  userContext: string,
  modelName: string = 'gemini-2.5-flash'
): Promise<{ text: string, tokenCount: number }> => {
  try {
    const genAI = getGenAI();
    const model = genAI.getGenerativeModel({ 
      model: modelName,
      generationConfig: {
        maxOutputTokens: 8192,
        temperature: 0.7,
        topP: 0.9,
        topK: 40
      },
      safetySettings: [
        {
          category: 'HARM_CATEGORY_HARASSMENT',
          threshold: 'BLOCK_MEDIUM_AND_ABOVE'
        }
        // ... 其他安全設定
      ]
    });

    const prompt = buildPrompt(systemPrompt, userContext);
    const result = await model.generateContent(prompt);
    const response = result.response;

    return {
      text: response.text(),
      tokenCount: response.usageMetadata?.totalTokenCount || 0
    };

  } catch (error) {
    if (error.message.includes('API_KEY_INVALID')) {
      throw new Error('API Key 無效，請檢查設定');
    } else if (error.message.includes('QUOTA_EXCEEDED')) {
      throw new Error('API 配額已用盡，請稍後再試');
    } else if (error.message.includes('SAFETY')) {
      throw new Error('內容觸發安全過濾器，請調整輸入');
    } else {
      throw new Error(`API 呼叫失敗: ${error.message}`);
    }
  }
};
5.2 Prompt Engineering 架構
系統採用結構化的 Prompt 模板技術，確保輸出品質與一致性。
5.2.1 Prompt 結構設計
標準 Prompt 模板
typescriptCopyconst buildPrompt = (systemPrompt: string, userContext: string): string => {
  return `
=== SYSTEM ROLE ===
You are an intelligent agent working within the TW-SmartReview 2030 system, 
a regulatory review assistant for the Taiwan FDA (TFDA).

${systemPrompt}

=== SOURCE DOCUMENT START ===
${userContext}
=== SOURCE DOCUMENT END ===

=== INSTRUCTIONS ===
1. Base your analysis PRIMARILY on the SOURCE DOCUMENT above.
2. If information is insufficient, explicitly state "Information not found in document" rather than hallucinating.
3. Cite specific sections or page numbers when making claims.
4. Use structured output format (Markdown with clear headings).
5. Highlight any regulatory concerns or gaps in BOLD.

=== CONSTRAINTS ===
- DO NOT fabricate data or references not present in the source document.
- DO NOT provide medical advice or make clinical decisions.
- DO maintain professional, objective tone suitable for regulatory review.

=== OUTPUT FORMAT ===
# Review Summary
[Brief overview]

## Key Findings
- [Finding 1]
- [Finding 2]

## Regulatory Compliance Analysis
[Detailed analysis]

## Recommendations
[Action items]

## References
[Citations from source document]
`;
};
5.2.2 思考配置 (Thinking Config)
針對 Gemini 2.5 系列模型，實作 Thinking Budget 以提升複雜推理能力：
typescriptCopy// geminiService.ts
const calculateThinkingBudget = (maxTokens: number): number => {
  // 預留 20% 的 Token 作為模型的隱式推理預算
  return Math.floor(maxTokens * 0.2);
};

export const callGeminiWithThinking = async (
  systemPrompt: string,
  userContext: string
): Promise<string> => {
  const maxOutputTokens = 8192;
  const thinkingBudget = calculateThinkingBudget(maxOutputTokens);

  const model = genAI.getGenerativeModel({ 
    model: 'gemini-2.5-flash',
    generationConfig: {
      maxOutputTokens: maxOutputTokens - thinkingBudget,
      // 啟用 Thinking Mode (實驗性功能)
      thinkingBudget: thinkingBudget
    }
  });

  // ... 執行推理
};
Thinking Budget 的運作原理：

模型在輸出答案前，會先在「思考空間」中進行內部推理。
這些思考過程不會顯示給使用者，但會提升最終答案的邏輯嚴謹性。
特別適用於多步驟推理任務 (如法規比對、風險評估)。

5.2.3 Prompt 優化技巧
Few-Shot Learning
提供範例輸出，引導模型生成符合期望的格式：
typescriptCopyconst fewShotExamples = `
=== EXAMPLE INPUT ===
Document: "The device operates at 220V AC, protected by a 5A fuse..."

=== EXAMPLE OUTPUT ===
# Electrical Safety Review

## Compliance Status
✅ PASS - Voltage specification documented
⚠️ WARNING - Fuse rating should be verified against IEC 60601-1 Table 5

## Detailed Analysis
The device's electrical specifications are partially documented...
`;
Chain-of-Thought Prompting
要求模型展示推理過程：
typescriptCopyconst cotPrompt = `
Before providing your final analysis, please think through the following steps:

1. IDENTIFY: What type of medical device is this? (Class I/II/III)
2. DETERMINE: Which regulatory standards apply?
3. EXTRACT: What are the key claims made in the document?
4. EVALUATE: Do the provided data support these claims?
5. CONCLUDE: What is your final assessment?

Now, work through these steps:
`;

6. 資料結構與型別定義 (Data Models)
系統使用 TypeScript 介面嚴格定義所有資料結構，確保型別安全。
6.1 核心型別定義
typescriptCopy// types.ts

// ===== Agent 相關 =====
export type AgentStatus = 'idle' | 'running' | 'completed' | 'failed';

export interface Agent {
  id: string;
  name: string;
  role: string;
  status: AgentStatus;
  output: string;
  error?: string;
  startTime?: Date;
  endTime?: Date;
  tokenUsage?: number;
  dependencies: string[];  // 依賴的其他 Agent ID
  priority: number;        // 執行優先級 (1-10)
}

export interface YamlAgentDef {
  id: string;
  name: string;
  role: string;
  description: string;
  systemPrompt?: string;
  dependencies?: string[];
  priority?: number;
  enabled?: boolean;  // 是否啟用
}

// ===== 日誌相關 =====
export type LogType = 'info' | 'success' | 'warning' | 'error' | 'system';

export interface LogEntry {
  id: string;
  timestamp: Date;
  source: string;      // 來源 (Agent 名稱或 SYSTEM)
  message: string;
  type: LogType;
  details?: object;    // 額外的結構化資訊
}

// ===== 文件相關 =====
export interface DocumentMetadata {
  filename: string;
  filesize: number;
  mimeType: string;
  uploadTime: Date;
  pageCount?: number;
  language?: string;
}

export interface ProcessedDocument {
  metadata: DocumentMetadata;
  content: string;
  extractedAt: Date;
  ocrMethod: 'llm-ocr' | 'traditional-ocr';
}

// ===== 審查結果 =====
export interface ReviewResult {
  agentId: string;
  agentName: string;
  timestamp: Date;
  summary: string;
  findings: Finding[];
  recommendations: string[];
  complianceScore?: number;  // 0-100
  riskLevel?: 'low' | 'medium' | 'high' | 'critical';
}

export interface Finding {
  category: string;
  severity: 'info' | 'minor' | 'major' | 'critical';
  description: string;
  location?: string;  // 文件中的位置 (頁碼/章節)
  recommendation?: string;
}

// ===== 風格主題 =====
export interface PainterStyle {
  id: string;
  name: string;
  bg: string;
  accent: string;
  font: 'serif' | 'sans' | 'mono';
  description: string;
}

// ===== 系統配置 =====
export interface SystemConfig {
  apiKey: string;
  modelName: string;
  maxTokens: number;
  temperature: number;
  language: 'zh-TW' | 'en-US';
  theme: 'light' | 'dark' | 'auto';
  painterStyle: string;
}
6.2 資料驗證
使用 Zod 或自定義驗證函式確保資料完整性：
typescriptCopy// validation.ts
import { z } from 'zod';

export const AgentDefSchema = z.object({
  id: z.string().min(1),
  name: z.string().min(1),
  role: z.string(),
  description: z.string(),
  systemPrompt: z.string().optional(),
  dependencies: z.array(z.string()).optional(),
  priority: z.number().min(1).max(10).optional(),
  enabled: z.boolean().optional()
});

export const validateAgentDef = (data: unknown): YamlAgentDef => {
  return AgentDefSchema.parse(data);
};

7. 部署與維運 (Deployment & DevOps)
7.1 環境需求
開發環境

Node.js v18+ (建議使用 v20 LTS)
npm v9+ 或 yarn v1.22+
現代瀏覽器 (Chrome 90+, Firefox 88+, Safari 14+)
VS Code (建議) + 推薦擴充套件：

ESLint
Prettier
TypeScript and JavaScript Language Features
Tailwind CSS IntelliSense



生產環境

靜態檔案伺服器 (Nginx, Apache, Caddy)
HTTPS 憑證 (Let's Encrypt 或商業 SSL)
CDN (可選，如 Cloudflare, AWS CloudFront)

7.2 環境變數
創建 .env 檔案 (不納入版本控制)：
bashCopy# .env
VITE_API_KEY=your_gemini_api_key_here
VITE_ENV=development
VITE_VERSION=4.2.0
7.3 建置流程
安裝依賴
bashCopynpm install
開發模式
bashCopynpm run dev
# 啟動 Vite 開發伺服器，預設於 http://localhost:5173
型別檢查
bashCopynpm run type-check
# 執行 tsc --noEmit 檢查型別錯誤
建置生產版本
bashCopynpm run build
# 步驟:
# 1. 執行 tsc 進行型別檢查
# 2. Vite build 產出優化後的靜態檔案至 /dist
# 3. 自動進行 Tree Shaking, Minification, Code Splitting
預覽建置結果
bashCopynpm run preview
# 在本地啟動靜態伺服器預覽 /dist 內容
7.4 靜態託管部署
方案一：GitHub Pages
bashCopy# 安裝 gh-pages 套件
npm install --save-dev gh-pages

# 在 package.json 加入部署腳本
"scripts": {
  "deploy": "npm run build && gh-pages -d dist"
}

# 執行部署
npm run deploy
方案二：Vercel
bashCopy# 安裝 Vercel CLI
npm i -g vercel

# 登入
vercel login

# 部署
vercel --prod
方案三：Netlify
bashCopy# 透過 Netlify CLI
npm
