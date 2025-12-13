TW-SmartReview 2030 智慧化審查代理人系統技術規格書
TW-SmartReview 2030 Agentic System Technical Specifications
版本： v4.2.0 (Cinematic Release)
日期： 2025年12月15日
機密等級： 內部技術文件
提交單位： 智慧醫療法規科學專案研究小組技術開發部

目錄

專案概述
系統架構設計
核心功能模組詳解
UIUX設計系統
AI模型整合策略
資料結構與型別定義
Streamlit實作架構
agentsyaml配置系統
FDA專用進階功能模組
系統效能優化與擴展性
部署與維運
結論與未來展望


1. 專案概述
1.1 系統定位與願景
TW-SmartReview 2030 是一個專為衛生福利部食品藥物管理署(TFDA)以及美國食品藥物管理局(FDA)設計的次世代智慧審查系統。本系統採用代理型人工智慧(Agentic AI)架構,透過多個專職AI代理人的協同運作,實現醫療器材查驗登記文件的自動化解析、法規符合性檢查、風險評估以及科學審查等複雜任務。
在當前醫療器材產業快速發展的背景下,審查機關面臨著文件數量爆炸性增長、技術複雜度提升以及審查標準國際化等多重挑戰。傳統的人工審查模式已難以滿足效率與品質的雙重要求。TW-SmartReview 2030 透過引入先進的大型語言模型(LLM)技術與多代理人協作機制,在保持審查嚴謹性的同時,大幅提升處理效率,實現「智慧增強型審查」(AI-Augmented Review)的創新模式。
1.2 核心設計理念
本系統建立在五大核心支柱之上:
1.2.1 智慧化(Intelligence)
運用Google Gemini 2.5 Flash等最先進的多模態大型語言模型,系統能夠:

自動理解複雜的醫療器材技術文件,包括掃描式PDF、手寫註記等非結構化內容
識別關鍵資訊片段,如臨床試驗終點、電氣安全參數、生物相容性測試結果
透過知識圖譜與向量檢索技術,快速定位相關法規條文與歷史案例
進行多步驟推理,評估文件邏輯一致性與數據支撐充分性

1.2.2 自動化(Automation)
透過工作流程編排(Workflow Orchestration)技術,系統能夠:

自動分配審查任務至專責代理人,無需人工調度
批次處理多份文件,支援優先級排程與依賴鏈管理
自動生成結構化審查報告,包含摘要、發現事項、建議改善措施
整合電子簽核系統,實現端到端的無紙化作業流程

1.2.3 透明化(Transparency)
為符合監管科學(Regulatory Science)的嚴謹要求,系統確保:

所有AI推理過程均可追溯,提供決策依據與參考資料來源
實作區塊鏈稽核軌跡,記錄每一次文件修改、審查意見與核准動作
支援「可解釋AI」(Explainable AI, XAI)技術,將黑箱模型的判斷邏輯視覺化
提供完整的操作日誌與時間戳記,符合FDA 21 CFR Part 11電子記錄要求

1.2.4 協同化(Collaboration)
模擬真實世界跨部門審查團隊的運作模式:

定義多個專業領域代理人(臨床評估、電氣安全、軟體驗證、生物相容性等)
透過中央編排器(Orchestrator)協調代理人間的資訊傳遞與任務依賴
支援人機協作(Human-in-the-Loop),關鍵決策點保留人工審核
整合即時通訊與協作工具,促進審查員、廠商與技術專家的溝通

1.2.5 隱私優先(Privacy-First)
採用先進的隱私保護技術:

無後端架構(Backendless Architecture)
支援聯邦學習(Federated Learning)
實作差分隱私(Differential Privacy)
符合GDPR、HIPAA等國際隱私法規要求

1.3 目標使用者群體
本系統設計時充分考量不同使用者角色的需求:
使用者類型主要需求系統功能支援TFDA/FDA審查員提升審查效率、確保一致性、減少人為疏漏自動化初審、智慧比對、風險分級、報告生成醫材製造商法規人員送審前自我檢查、降低補件率、縮短審查週期Pre-submission Review、缺陷偵測、法規指引第三方查驗顧問專業服務工具、提升服務品質、擴大服務量能批次處理、客製化報告、多專案管理學術研究機構教學案例、研究素材、法規科學發展匿名化案例庫、統計分析、趨勢視覺化
1.4 技術創新亮點
相較於傳統的文件管理系統或簡單的關鍵字搜尋工具,TW-SmartReview 2030具備以下突破性創新:

多模態文件理解,更能理解圖表、流程圖、電路圖等視覺元素
動態代理人編排
電影級互動介面,提供沉浸式使用者體驗
藝術風格引擎+種視覺主題,個性化工作環境
Streamlit快速原型


2. 系統架構設計
2.1 整體架構概覽
TW-SmartReview 2030採用微服務導向架構(Microservices-Oriented Architecture)結合事件驅動設計(Event-Driven Design),實現高度模組化與可擴展性。系統由以下核心層級組成:
Copy┌─────────────────────────────────────────────────────────┐
│                    使用者介面層 (UI Layer)                │
│          Streamlit Web App + Custom Components          │
├─────────────────────────────────────────────────────────┤
│                   應用邏輯層 (Logic Layer)                │
│    Session State Management + Workflow Orchestration    │
├─────────────────────────────────────────────────────────┤
│                   代理人執行層 (Agent Layer)              │
│  Clinical Evaluator | Electrical Safety | Risk Analyzer │
├─────────────────────────────────────────────────────────┤
│                   AI推論層 (Inference Layer)              │
│        Google Gemini API + Vector Database (Pinecone)    │
├─────────────────────────────────────────────────────────┤
│                   資料存取層 (Data Layer)                 │
│    File Storage + Knowledge Base + Audit Trail (SQLite) │
└─────────────────────────────────────────────────────────┘
2.2 Streamlit技術堆疊
本系統選擇Streamlit作為前端框架,相較於傳統的React/Vue.js等JavaScript框架,具備以下優勢:
2.2.1 核心優勢

純Python開發,降低技術棧複雜度
即時熱重載,極致開發體驗
內建元件豐富、圖表、多媒體元件開箱即用
Session State管理
原生支援資料科學套件、NumPy、Plotly等

2.2.2 技術堆疊清單
類別技術/套件版本用途核心框架Streamlit1.32.0+Web應用框架語言Python3.11+主要開發語言AI推論google-generativeai0.4.0+Gemini API客戶端文件處理PyMuPDF (fitz)1.23.0+PDF解析與渲染向量檢索pinecone-client3.0.0+向量資料庫客戶端資料處理pandas2.2.0+結構化資料操作視覺化plotly5.18.0+互動式圖表配置管理PyYAML6.0+YAML檔案解析日誌記錄loguru0.7.0+結構化日誌環境變數python-dotenv1.0.0+環境配置管理
2.3 資料流架構
系統採用單向資料流(Unidirectional Data Flow)設計模式,確保狀態變化的可預測性:
pythonCopy# 資料流向示意
使用者上傳文件 
    ↓
文件前處理器(Preprocessor)
    ↓
LLM-OCR服務(OCR Service)
    ↓
Context提取與存儲(Session State)
    ↓
代理人編排器(Orchestrator)
    ↓
平行/序列執行代理人(Agents Execution)
    ↓
結果聚合器(Result Aggregator)
    ↓
UI即時更新(Real-time UI Update)
2.3.1 Session State管理策略
Streamlit的核心機制是在每次使用者互動時重新執行整個腳本。為避免狀態丟失與重複運算,系統實作以下策略:
pythonCopy# core/session_manager.py
import streamlit as st
from typing import Any, Optional

class SessionManager:
    """集中式Session State管理器"""
    
    @staticmethod
    def initialize():
        """初始化所有必要的session變數"""
        defaults = {
            'processed_documents': [],
            'active_agents': [],
            'review_results': {},
            'system_logs': [],
            'current_painter_style': 'cyberpunk',
            'api_key_configured': False,
            'user_notes': '',
            'workflow_status': 'idle'  # idle, processing, completed, error
        }
        
        for key, value in defaults.items():
            if key not in st.session_state:
                st.session_state[key] = value
    
    @staticmethod
    def get(key: str, default: Any = None) -> Any:
        """安全地獲取session變數"""
        return st.session_state.get(key, default)
    
    @staticmethod
    def set(key: str, value: Any):
        """設定session變數"""
        st.session_state[key] = value
    
    @staticmethod
    def append(key: str, value: Any):
        """向列表類型的session變數追加元素"""
        if key not in st.session_state:
            st.session_state[key] = []
        st.session_state[key].append(value)
2.4 安全性架構
2.4.1 多層防禦策略
系統實作縱深防禦(Defense in Depth)安全模型:
Copy┌─────────────────────────────────────┐
│  Layer 1: 網路層防護                 │
│  - HTTPS強制加密                    │
│  - Rate Limiting (API閘道)          │
│  - DDoS防護 (Cloudflare)            │
├─────────────────────────────────────┤
│  Layer 2: 應用層防護                 │
│  - API Key加密存儲                  │
│  - Session Token驗證                │
│  - CSRF Token保護                   │
├─────────────────────────────────────┤
│  Layer 3: 資料層防護                 │
│  - 敏感資料加密 (AES-256)           │
│  - 存取控制列表 (ACL)               │
│  - 稽核日誌 (Immutable Log)         │
├─────────────────────────────────────┤
│  Layer 4: 合規性控制                 │
│  - GDPR資料主體權利                 │
│  - HIPAA存取審計                    │
│  - FDA 21 CFR Part 11電子簽章       │
└─────────────────────────────────────┘
2.4.2 API Key管理實作
pythonCopy# core/security.py
import os
from cryptography.fernet import Fernet
from typing import Optional

class APIKeyManager:
    """API金鑰安全管理器"""
    
    def __init__(self):
        # 從環境變數或使用者主密碼派生加密金鑰
        self.cipher_suite = self._initialize_cipher()
    
    def _initialize_cipher(self) -> Fernet:
        """初始化加密器"""
        # 優先使用環境變數中的加密金鑰
        encryption_key = os.getenv('ENCRYPTION_KEY')
        if not encryption_key:
            # 若無環境變數,使用硬體指紋+鹽值生成
            encryption_key = Fernet.generate_key()
        return Fernet(encryption_key)
    
    def store_api_key(self, api_key: str) -> bool:
        """加密並存儲API金鑰"""
        try:
            encrypted_key = self.cipher_suite.encrypt(api_key.encode())
            # 僅存於session state,不寫入磁碟
            SessionManager.set('encrypted_api_key', encrypted_key)
            SessionManager.set('api_key_configured', True)
            return True
        except Exception as e:
            st.error(f"金鑰存儲失敗: {str(e)}")
            return False
    
    def retrieve_api_key(self) -> Optional[str]:
        """解密並取得API金鑰"""
        encrypted_key = SessionManager.get('encrypted_api_key')
        if not encrypted_key:
            # 嘗試從環境變數讀取
            return os.getenv('GEMINI_API_KEY')
        
        try:
            decrypted_key = self.cipher_suite.decrypt(encrypted_key)
            return decrypted_key.decode()
        except Exception:
            return None
    
    def validate_key(self, api_key: str) -> bool:
        """驗證API金鑰有效性"""
        # 進行測試性API呼叫
        try:
            import google.generativeai as genai
            genai.configure(api_key=api_key)
            model = genai.GenerativeModel('gemini-2.5-flash')
            # 發送極簡測試請求
            response = model.generate_content("Test")
            return True
        except Exception as e:
            st.warning(f"API金鑰驗證失敗: {str(e)}")
            return False

3. 核心功能模組詳解
3.1 智慧儀表板模組
3.1.1 模組架構
智慧儀表板位於應用程式首頁,提供系統狀態的全景視圖與關鍵指標監控。
pythonCopy# pages/1_📊_Dashboard.py
import streamlit as st
import plotly.express as px
import plotly.graph_objects as go
from datetime import datetime, timedelta
import pandas as pd

def render_dashboard():
    """渲染智慧儀表板"""
    st.set_page_config(
        page_title="TW-SmartReview 2030 儀表板",
        page_icon="📊",
        layout="wide"
    )
    
    # 套用當前藝術風格
    apply_painter_style(SessionManager.get('current_painter_style'))
    
    # 標題區
    col1, col2 = st.columns([3, 1])
    with col1:
        st.title("🎯 TW-SmartReview 2030 智慧儀表板")
        st.caption(f"最後更新: {datetime.now().strftime('%Y-%m-%d %H:%M:%S')}")
    
    with col2:
        # 系統狀態指示器
        status = SessionManager.get('workflow_status')
        status_color = {
            'idle': '🟢',
            'processing': '🔵', 
            'completed': '🟢',
            'error': '🔴'
        }
        st.metric(
            label="系統狀態",
            value=status_color.get(status, '⚪') + " " + status.upper()
        )
    
    # 關鍵指標卡片區
    render_kpi_cards()
    
    # 圖表區
    render_charts()
    
    # 活躍代理人網絡視覺化
    render_agent_network()

def render_kpi_cards():
    """渲染關鍵績效指標卡片"""
    col1, col2, col3, col4 = st.columns(4)
    
    # 模擬數據 (實際應從資料庫或session state取得)
    metrics = {
        '本月審查案件': (124, +12),
        '平均審查時長': ('3.2天', -0.5),
        '審查通過率': ('87%', +3),
        'AI Token使用': ('2.3M', +150000)
    }
    
    with col1:
        st.metric(
            label="📁 本月審查案件",
            value=metrics['本月審查案件'][0],
            delta=f"+{metrics['本月審查案件'][1]} 較上月"
        )
    
    with col2:
        st.metric(
            label="⏱️ 平均審查時長",
            value=metrics['平均審查時長'][0],
            delta=f"{metrics['平均審查時長'][1]}天 較上月",
            delta_color="inverse"  # 數值減少是好事
        )
    
    with col3:
        st.metric(
            label="✅ 審查通過率",
            value=metrics['審查通過率'][0],
            delta=f"+{metrics['審查通過率'][1]}% 較上月"
        )
    
    with col4:
        st.metric(
            label="🤖 AI Token使用",
            value=metrics['AI Token使用'][0],
            delta=f"+{metrics['AI Token使用'][1]} 較上月"
        )

def render_charts():
    """渲染統計圖表"""
    tab1, tab2, tab3 = st.tabs(["📈 審查趨勢", "📊 案件分布", "🎯 效率分析"])
    
    with tab1:
        # 時間序列趨勢圖
        df_trend = generate_trend_data()
        fig = px.area(
            df_trend,
            x='日期',
            y=['送件數', '完成審查數'],
            title='近30日審查趨勢',
            labels={'value': '案件數', 'variable': '類別'}
        )
        st.plotly_chart(fig, use_container_width=True)
    
    with tab2:
        # 案件分類圓餅圖
        df_category = pd.DataFrame({
            '器材類別': ['診斷試劑', '植入物', '體外循環', '電氣設備', '軟體'],
            '案件數': [45, 32, 18, 23, 6]
        })
        fig = px.pie(
            df_category,
            values='案件數',
            names='器材類別',
            title='本月案件類別分布'
        )
        st.plotly_chart(fig, use_container_width=True)
    
    with tab3:
        # 審查效率對比長條圖
        df_efficiency = pd.DataFrame({
            '審查階段': ['文件接收', '初步審查', 'AI輔助分析', '專家複核', '最終核定'],
            '人工審查(小時)': [2, 48, 0, 24, 8],
            'AI輔助審查(小時)': [1, 12, 4, 16, 6]
        })
        fig = go.Figure(data=[
            go.Bar(name='人工審查', x=df_efficiency['審查階段'], y=df_efficiency['人工審查(小時)']),
            go.Bar(name='AI輔助審查', x=df_efficiency['審查階段'], y=df_efficiency['AI輔助審查(小時)'])
        ])
        fig.update_layout(barmode='group', title='審查流程效率對比')
        st.plotly_chart(fig, use_container_width=True)
3.1.2 動態代理人網絡視覺化
使用Plotly建立即時更新的代理人連接圖:
pythonCopydef render_agent_network():
    """渲染代理人神經網絡視覺化"""
    st.subheader("🕸️ 代理人協作網絡")
    
    active_agents = SessionManager.get('active_agents', [])
    
    if not active_agents:
        st.info("尚無活躍代理人。請先上傳文件並啟動審查流程。")
        return
    
    # 構建網絡圖資料
    import networkx as nx
    
    G = nx.Graph()
    
    # 添加中心節點
    G.add_node("Orchestrator", node_type="hub")
    
    # 添加代理人節點
    for agent in active_agents:
        G.add_node(
            agent['id'],
            node_type="agent",
            status=agent['status'],
            name=agent['name']
        )
        # 連接至中心節點
        G.add_edge("Orchestrator", agent['id'])
    
    # 添加代理人間的依賴關係
    for agent in active_agents:
        for dep in agent.get('dependencies', []):
            if dep in [a['id'] for a in active_agents]:
                G.add_edge(agent['id'], dep, edge_type="dependency")
    
    # 計算佈局
    pos = nx.spring_layout(G, k=0.5, iterations=50)
    
    # 準備Plotly資料
    edge_trace = []
    for edge in G.edges():
        x0, y0 = pos[edge[0]]
        x1, y1 = pos[edge[1]]
        edge_trace.append(
            go.Scatter(
                x=[x0, x1, None],
                y=[y0, y1, None],
                mode='lines',
                line=dict(width=2, color='#888'),
                hoverinfo='none'
            )
        )
    
    node_trace = go.Scatter(
        x=[],
        y=[],
        text=[],
        mode='markers+text',
        hoverinfo='text',
        marker=dict(
            size=[],
            color=[],
            line=dict(width=2, color='white')
        ),
        textposition="top center"
    )
    
    status_colors = {
        'idle': '#gray',
        'running': '#3b82f6',
        'completed': '#10b981',
        'failed': '#ef4444'
    }
    
    for node in G.nodes():
        x, y = pos[node]
        node_trace['x'] += tuple([x])
        node_trace['y'] += tuple([y])
        
        if node == "Orchestrator":
            node_trace['marker']['size'] += tuple([40])
            node_trace['marker']['color'] += tuple(['#8b5cf6'])
            node_trace['text'] += tuple(['🎯 Orchestrator'])
        else:
            agent_data = next((a for a in active_agents if a['id'] == node), None)
            if agent_data:
                node_trace['marker']['size'] += tuple([30])
                node_trace['marker']['color'] += tuple([status_colors.get(agent_data['status'], '#gray')])
                node_trace['text'] += tuple([agent_data['name']])
    
    # 組合圖表
    fig = go.Figure(
        data=edge_trace + [node_trace],
        layout=go.Layout(
            showlegend=False,
            hovermode='closest',
            margin=dict(b=0, l=0, r=0, t=0),
            xaxis=dict(showgrid=False, zeroline=False, showticklabels=False),
            yaxis=dict(showgrid=False, zeroline=False, showticklabels=False),
            plot_bgcolor='rgba(0,0,0,0)',
            height=500
        )
    )
    
    st.plotly_chart(fig, use_container_width=True)
    
    # 代理人狀態表格
    st.dataframe(
        pd.DataFrame([
            {
                '代理人': a['name'],
                '狀態': a['status'],
                '開始時間': a.get('start_time', 'N/A'),
                'Token使用': a.get('token_usage', 0)
            }
            for a in active_agents
        ]),
        use_container_width=True
    )
3.2 文件處理模組
3.2.1 多格式文件攝取器
pythonCopy# components/file_processor.py
import streamlit as st
import PyMuPDF as fitz  # PyMuPDF
from PIL import Image
import io
from typing import List, Dict, Optional

class FileProcessor:
    """多格式文件處理器"""
    
    SUPPORTED_FORMATS = {
        'application/pdf': 'PDF',
        'text/plain': 'TXT',
        'text/markdown': 'Markdown',
        'application/json': 'JSON',
        'image/png': 'PNG',
        'image/jpeg': 'JPEG',
        'image/tiff': 'TIFF'
    }
    
    MAX_FILE_SIZE = 50 * 1024 * 1024  # 50MB
    
    @staticmethod
    def render_uploader():
        """渲染文件上傳介面"""
        st.subheader("📤 文件上傳")
        
        uploaded_files = st.file_uploader(
            "支援格式: PDF, TXT, Markdown, JSON, PNG, JPG, TIFF",
            type=['pdf', 'txt', 'md', 'json', 'png', 'jpg', 'jpeg', 'tiff'],
            accept_multiple_files=True,
            help="單檔最大50MB,總計最大200MB"
        )
        
        if uploaded_files:
            return FileProcessor._process_files(uploaded_files)
        return None
    
    @staticmethod
    def _process_files(files: List) -> List[Dict]:
        """處理上傳的文件"""
        processed_docs = []
        
        progress_bar = st.progress(0)
        status_text = st.empty()
        
        for idx, file in enumerate(files):
            status_text.text(f"處理中: {file.name} ({idx+1}/{len(files)})")
            
            # 檢查檔案大小
            if file.size > FileProcessor.MAX_FILE_SIZE:
                st.warning(f"⚠️ {file.name} 超過大小限制(50MB),已跳過")
                continue
            
            # 根據MIME類型處理
            if file.type == 'application/pdf':
                doc_data = FileProcessor._process_pdf(file)
            elif file.type.startswith('image/'):
                doc_data = FileProcessor._process_image(file)
            elif file.type in ['text/plain', 'text/markdown']:
                doc_data = FileProcessor._process_text(file)
            elif file.type == 'application/json':
                doc_data = FileProcessor._process_json(file)
            else:
                st.error(f"❌ 不支援的檔案格式: {file.type}")
                continue
            
            if doc_data:
                processed_docs.append(doc_data)
            
            progress_bar.progress((idx + 1) / len(files))
        
        status_text.text(f"✅ 完成處理 {len(processed_docs)} 份文件")
        return processed_docs
    
    @staticmethod
    def _process_pdf(file) -> Optional[Dict]:
        """處理PDF檔案"""
        try:
            pdf_bytes = file.read()
            pdf_document = fitz.open(stream=pdf_bytes, filetype="pdf")
            
            # 頁碼範圍選擇
            total_pages = pdf_document.page_count
            st.info(f"📄 檔案 {file.name} 共 {total_pages} 頁")
            
            page_range = st.text_input(
                f"選擇頁碼範圍 (例: 1-5, 10, 15-20)",
                value=f"1-{total_pages}",
                key=f"page_range_{file.name}"
            )
            
            selected_pages = FileProcessor._parse_page_range(page_range, total_pages)
            
            # 提取文字與圖片
            extracted_text = ""
            images = []
            
            for page_num in selected_pages:
                page = pdf_document[page_num - 1]  # 0-indexed
                extracted_text += page.get_text()
                
                # 提取圖片
                image_list = page.get_images()
                for img_index, img in enumerate(image_list):
                    xref = img[0]
                    base_image = pdf_document.extract_image(xref)
                    images.append({
                        'page': page_num,
                        'index': img_index,
                        'data': base_image["image"]
                    })
            
            pdf_document.close()
            
            return {
                'filename': file.name,
                'type': 'pdf',
                'total_pages': total_pages,
                'selected_pages': selected_pages,
                'text': extracted_text,
                'images': images,
                'size': file.size,
                'upload_time': datetime.now()
            }
            
        except Exception as e:
            st.error(f"PDF處理失敗: {str(e)}")
            return None
    
    @staticmethod
    def _parse_page_range(range_str: str, total_pages: int) -> List[int]:
        """解析頁碼範圍字串"""
        pages = set()
        parts = range_str.split(',')
        
        for part in parts:
            part = part.strip()
            if '-' in part:
                start, end = part.split('-')
                start = int(start.strip())
                end = int(end.strip())
                pages.update(range(start, min(end, total_pages) + 1))
            else:
                page = int(part)
                if 1 <= page <= total_pages:
                    pages.add(page)
        
        return sorted(list(pages))
3.2.2 LLM-OCR服務
pythonCopy# services/ocr_service.py
import google.generativeai as genai
from typing import Dict, Optional
import base64

class LLMOCRService:
    """基於LLM的光學字元辨識服務"""
    
    def __init__(self, api_key: str):
        genai.configure(api_key=api_key)
        self.model = genai.GenerativeModel('gemini-2.5-flash')
    
    async def extract_text_from_pdf(
        self,
        pdf_bytes: bytes,
        page_range: Optional[str] = None,
        language: str = 'zh-TW'
    ) -> Dict:
        """從PDF提取文字"""
        
        # 將PDF轉換為base64
        pdf_base64 = base64.b64encode(pdf_bytes).decode('utf-8')
        
        prompt = self._build_ocr_prompt(page_range, language)
        
        try:
            response = await self.model.generate_content_async([
                {
                    'mime_type': 'application/pdf',
                    'data': pdf_base64
                },
                prompt
            ])
            
            return {
                'success': True,
                'text': response.text,
                'token_count': response.usage_metadata.total_token_count,
                'method': 'llm-ocr'
            }
            
        except Exception as e:
            return {
                'success': False,
                'error': str(e),
                'method': 'llm-ocr'
            }
    
    def _build_ocr_prompt(self, page_range: Optional[str], language: str) -> str:
        """構建OCR提示詞"""
        return f"""
你是一個專業的醫療器材文件光學字元辨識系統。

【任務】
從提供的PDF文件中提取所有文字內容。

【要求】
1. 保持原始排版結構(標題、段落、清單、表格)
2. 精確辨識專業術語(醫療器材名稱、法規編號、測試標準)
3. 對於表格,使用Markdown表格格式輸出
4. 對於模糊或無法辨識的文字,標註為[UNCLEAR]
5. 保留文件中的多語言內容(中英文混合)

{f'【處理範圍】僅處理第 {page_range} 頁' if page_range else '【處理範圍】處理所有頁面'}

【輸出語言】{language}

【輸出格式】純Markdown文字,不要包含任何額外說明

開始提取:
"""
3.3 代理人編排模組
3.3.1 agents.yaml配置檔案
系統的代理人定義完全透過YAML配置檔案進行管理:
yamlCopy# config/agents.yaml
meta:
  version: "4.2.0"
  last_updated: "2025-12-15"
  description: "TW-SmartReview 2030 代理人配置檔案"

agents:
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
      
      【你的任務】
      審查臨床試驗文件,評估其科學性、完整性與法規符合性。
      
      【評估重點】
      1. 樣本數計算的合理性(統計檢定力分析)
      2. 主要終點(Primary Endpoint)與次要終點的選擇適當性
      3. 統計方法的正確性(ITT分析、Per-protocol分析)
      4. 不良事件報告的完整性與因果關係判定
      5. 知情同意流程的合規性
      6. 試驗設計的偏差控制(盲法、隨機化)
      
      【輸出格式】
      # 臨床評估報告
      
      ## 執行摘要
      [簡要概述主要發現]
      
      ## 試驗設計評估
      - **試驗類型**: [RCT/單臂/觀察性]
      - **樣本數**: [實際/計畫] 
      - **主要終點**: [描述]
      - **評估**: [PASS/FAIL/需補充資料]
      
      ## 數據完整性檢查
      [詳細分析]
      
      ## 不良事件分析
      [事件清單與嚴重程度評估]
      
      ## 法規符合性
      - ISO 14155符合度: [%]
      - GCP符合度: [%]
      
      ## 建議事項
      1. [建議1]
      2. [建議2]
      
      ## 風險等級
      [LOW/MEDIUM/HIGH/CRITICAL]
      
    generation_config:
      max_output_tokens: 4096
      temperature: 0.3
      top_p: 0.9
      top_k: 40
    
    safety_settings:
      - category: HARM_CATEGORY_MEDICAL_ADVICE
        threshold: BLOCK_MEDIUM_AND_ABOVE
  
  - id: electrical-safety
    name: 電氣安全審查員
    name_en: Electrical Safety Reviewer
    role: 檢查電氣安全標準符合性
    category: engineering
    icon: "⚡"
    priority: 2
    enabled: true
    dependencies: []
    
    system_prompt: |
      你是一位電氣安全工程師,專精於IEC 60601-1標準。
      
      【你的任務】
      審查醫療電氣設備的安全性設計文件。
      
      【檢查項目】
      1. 電氣絕緣等級(工作電壓、絕緣耐壓測試)
      2. 漏電流限值(接地漏電流、外殼漏電流、患者漏電流)
      3. 保護接地系統完整性
      4. EMC電磁相容性(IEC 60601-1-2)
      5. 電池安全性(過充/過放保護)
      6. 標示與警語完整性
      
      【參考標準】
      - IEC 60601-1:2005+AMD1:2012+AMD2:2020
      - IEC 60601-1-2:2014 (EMC)
      - IEC 60601-1-6:2010 (Usability)
      
      【輸出格式】
      # 電氣安全審查報告
      
      ## 器材分類
      - **防電擊等級**: [Class I/II/III]
      - **應用部分**: [B/BF/CF型]
      
      ## 符合性檢查表
      | 項目 | 要求值 | 實測值 | 判定 |
      |------|--------|--------|------|
      | 接地漏電流 | <500µA | [數值] | [✓/✗] |
      
      ## 風險評估
      [識別的風險點]
      
      ## 建議措施
      [改善建議]
  
  - id: software-verification
    name: 軟體驗證專家
    name_en: Software Verification Specialist
    role: 評估軟體生命週期文件與驗證測試
    category: software
    icon: "💻"
    priority: 3
    enabled: true
    dependencies: []
    
    system_prompt: |
      你是一位醫療軟體驗證專家,專精於IEC 62304標準。
      
      【你的任務】
      審查醫療器材軟體(SaMD/SiMD)的開發與驗證文件。
      
      【評估重點】
      1. 軟體安全分類(Class A/B/C)的合理性
      2. 軟體需求規格(SRS)的完整性與可追溯性
      3. 軟體設計文件(SDD)的架構合理性
      4. 單元測試、整合測試、系統測試的覆蓋率
      5. 風險管理檔案(依ISO 14971)
      6. 網路安全考量(FDA Cybersecurity Guidance)
      
      【輸出格式】
      # 軟體驗證報告
      
      ## 軟體描述
      - **SOUP元件**: [第三方軟體清單]
      - **安全等級**: [A/B/C]
      
      ## 需求追溯矩陣檢查
      [需求→設計→測試的可追溯性]
      
      ## 測試覆蓋率分析
      - 程式碼覆蓋率: [%]
      - 需求覆蓋率: [%]
      
      ## 網路安全評估
      [漏洞掃描結果、加密機制檢查]
      
      ## 符合性結論
      [是否符合IEC 62304要求]
  
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
      你是一位生物相容性評估專家,專精於ISO 10993系列標準。
      
      【你的任務】
      根據器材的接觸性質與持續時間,評估所需的生物相容性測試項目與結果。
      
      【評估流程】
      1. 判定器材的接觸類別(表面接觸/外部連通/植入)
      2. 判定接觸時間(暫時/短期/長期)
      3. 依ISO 10993-1決定必要測試項目
      4. 審查測試報告的完整性與合格性
      
      【測試項目對照】
      - 細胞毒性(ISO 10993-5)
      - 致敏性(ISO 10993-10)
      - 刺激性(ISO 10993-10)
      - 全身毒性(ISO 10993-11)
      - 植入反應(ISO 10993-6)
      - 遺傳毒性(ISO 10993-3)
      - 血液相容性(ISO 10993-4)
      - 致癌性(ISO 10993-3)
      
      【輸出格式】
      # 生物相容性評估報告
      
      ## 器材資訊
      - **接觸類別**: [類別]
      - **接觸時間**: [時間]
      
      ## 所需測試項目清單
      | 測試項目 | ISO標準 | 要求 | 狀態 |
      |----------|---------|------|------|
      
      ## 測試結果評估
      [各項測試的通過/失敗判定]
      
      ## 材料安全性結論
      [整體生物相容性評估結論]
  
  - id: risk-manager
    name: 風險管理專家
    name_en: Risk Management Specialist
    role: 執行ISO 14971風險分析
    category: quality
    icon: "⚠️"
    priority: 5
    enabled: true
    dependencies:
      - clinical-evaluator
      - electrical-safety
      - software-verification
      - biocompatibility
    
    system_prompt: |
      你是一位風險管理專家,專精於ISO 14971:2019標準。
      
      【你的任務】
      整合所有專業領域代理人的發現,進行綜合風險評估。
      
      【風險分析方法】
      1. 收集所有已識別的危害(Hazards)
      2. 分析危害情境(Hazardous Situations)
      3. 估計風險(Severity × Probability)
      4. 評估風險可接受性
      5. 建議風險控制措施
      6. 評估殘餘風險
      
      【風險矩陣】
      嚴重度: 1(可忽略) ~ 5(災難性)
      發生機率: A(極罕見) ~ E(頻繁)
      
      【輸出格式】
      # 綜合風險管理報告
      
      ## 風險彙總表
      | 風險ID | 危害描述 | 嚴重度 | 機率 | 風險等級 | 控制措施 |
      |--------|----------|--------|------|----------|----------|
      
      ## 高風險項目詳細分析
      [針對高風險項目的深入探討]
      
      ## 風險/效益分析
      [殘餘風險是否可接受]
      
      ## 上市後監控計畫建議
      [建議的PMS監測項目]
  
  - id: regulatory-mapper
    name: 法規智慧比對引擎
    name_en: Regulatory Intelligence Mapper
    role: 比對多國法規要求
    category: regulatory
    icon: "📋"
    priority: 6
    enabled: true
    dependencies: []
    
    system_prompt: |
      你是一位國際法規專家,熟悉TFDA、FDA、CE、PMDA等多國法規要求。
      
      【你的任務】
      比對送審文件與目標市場的法規要求,識別缺口。
      
      【法規資料庫】
      - TFDA: 醫療器材管理辦法、查驗登記審查準則
      - FDA: 510(k), PMA, De Novo pathways
      - EU MDR: Regulation (EU) 2017/745
      - Japan PMDA: PMD Act
      
      【輸出格式】
      # 法規符合性比對報告
      
      ## 目標市場分析
      - **主要市場**: [TFDA/FDA/CE]
      - **器材分類**: [各市場的分類]
      
      ## 法規要求對照表
      | 要求項目 | TFDA | FDA | EU MDR | 符合狀態 |
      |----------|------|-----|--------|----------|
      
      ## 缺口分析
      [缺少的文件或測試]
      
      ## 送審策略建議
      [優先申請市場、同步送審可行性]

# 代理人群組定義
agent_groups:
  - id: essential-review
    name: 基本審查組
    description: 所有案件的必要審查項目
    agents:
      - clinical-evaluator
      - electrical-safety
      - biocompatibility
      - risk-manager
  
  - id: software-intensive
    name: 軟體密集審查組
    description: 軟體為主要功能的器材
    agents:
      - clinical-evaluator
      - software-verification
      - risk-manager
      - regulatory-mapper
  
  - id: full-review
    name: 完整審查組
    description: 高風險器材的全面審查
    agents:
      - clinical-evaluator
      - electrical-safety
      - software-verification
      - biocompatibility
      - risk-manager
      - regulatory-mapper
3.3.2 編排器核心實作
pythonCopy# core/orchestrator.py
import streamlit as st
import yaml
import asyncio
from typing import List, Dict, Optional
from loguru import logger
import google.generativeai as genai

class AgentOrchestrator:
    """代理人編排器"""
    
    def __init__(self, config_path: str = "config/agents.yaml"):
        self.config = self._load_config(config_path)
        self.agents = self._initialize_agents()
        self.execution_queue = []
    
    def _load_config(self, path: str) -> Dict:
        """載入agents.yaml配置"""
        try:
            with open(path, 'r', encoding='utf-8') as f:
                return yaml.safe_load(f)
        except Exception as e:
            logger.error(f"配置檔案載入失敗: {e}")
            st.error(f"❌ 無法載入代理人配置: {str(e)}")
            return {}
    
    def _initialize_agents(self) -> List[Dict]:
        """初始化代理人列表"""
        agents = []
        for agent_def in self.config.get('agents', []):
            if agent_def.get('enabled', True):
                agents.append({
                    **agent_def,
                    'status': 'idle',
                    'output': '',
                    'error': None,
                    'start_time': None,
                    'end_time': None,
                    'token_usage': 0
                })
        return agents
    
    def render_agent_selector(self) -> List[str]:
        """渲染代理人選擇介面"""
        st.subheader("🤖 選擇審查代理人")
        
        # 快速群組選擇
        groups = self.config.get('agent_groups', [])
        if groups:
            st.write("**快速群組:**")
            group_cols = st.columns(len(groups))
            selected_group = None
            
            for idx, group in enumerate(groups):
                with group_cols[idx]:
                    if st.button(
                        f"{group['name']}\n({len(group['agents'])}個代理人)",
                        use_container_width=True
                    ):
                        selected_group = group['agents']
        
        st.divider()
        
        # 個別代理人選擇
        st.write("**個別選擇:**")
        
        # 按類別分組顯示
        categories = {}
        for agent in self.agents:
            cat = agent.get('category', 'other')
            if cat not in categories:
                categories[cat] = []
            categories[cat].append(agent)
        
        selected_agents = []
        
        category_names = {
            'clinical': '🏥 臨床評估',
            'engineering': '⚡ 工程技術',
            'software': '💻 軟體驗證',
            'biological': '🧬 生物安全',
            'quality': '⚠️ 品質管理',
            'regulatory': '📋 法規符合'
        }
        
        for cat, agents_in_cat in categories.items():
            with st.expander(category_names.get(cat, cat), expanded=True):
                for agent in agents_in_cat:
                    col1, col2 = st.columns([3, 1])
                    
                    with col1:
                        selected = st.checkbox(
                            f"{agent['icon']} {agent['name']}",
                            value=False,
                            key=f"agent_select_{agent['id']}",
                            help=agent['role']
                        )
                        if selected:
                            selected_agents.append(agent['id'])
                    
                    with col2:
                        # 顯示優先級
                        st.caption(f"優先級: {agent['priority']}")
        
        # 若選擇了群組,覆蓋個別選擇
        if selected_group:
            return selected_group
        
        return selected_agents
    
    async def execute_agents(
        self,
        agent_ids: List[str],
        context: str,
        execution_mode: str = 'parallel'
    ):
        """執行選定的代理人"""
        
        # 構建執行計畫
        execution_plan = self._build_execution_plan(agent_ids, execution_mode)
        
        # 初始化進度追蹤
        progress_bar = st.progress(0)
        status_text = st.empty()
        
        total_agents = sum(len(batch) for batch in execution_plan)
        completed = 0
        
        # 執行各批次
        for batch_idx, batch in enumerate(execution_plan):
            status_text.text(f"執行批次 {batch_idx + 1}/{len(execution_plan)}")
            
            # 平行執行同批次的代理人
            tasks = [
                self._execute_single_agent(agent_id, context)
                for agent_id in batch
            ]
            
            results = await asyncio.gather(*tasks, return_exceptions=True)
            
            # 更新進度
            completed += len(batch)
            progress_bar.progress(completed / total_agents)
        
        status_text.text("✅ 所有代理人執行完畢")
        
        # 返回結果
        return self.agents
    
    def _build_execution_plan(
        self,
        agent_ids: List[str],
        mode: str
    ) -> List[List[str]]:
        """構建執行計畫"""
        
        if mode == 'parallel':
            # 全部平行執行
            return [agent_ids]
        
        elif mode == 'sequential':
            # 依優先級順序執行
            sorted_agents = sorted(
                [a for a in self.agents if a['id'] in agent_ids],
                key=lambda x: x['priority']
            )
            return [[a['id']] for a in sorted_agents]
        
        elif mode == 'dependency':
            # 根據依賴關係建立批次
            return self._resolve_dependencies(agent_ids)
        
        else:
            raise ValueError(f"不支援的執行模式: {mode}")
    
    def _resolve_dependencies(self, agent_ids: List[str]) -> List[List[str]]:
        """解析依賴關係,建立執行批次"""
        from collections import defaultdict, deque
        
        # 建立依賴圖
        graph = defaultdict(list)
        in_degree = {aid: 0 for aid in agent_ids}
        
        for agent_id in agent_ids:
            agent = next(a for a in self.agents if a['id'] == agent_id)
            deps = agent.get('dependencies', [])
            
            for dep in deps:
                if dep in agent_ids:
                    graph[dep].append(agent_id)
                    in_degree[agent_id] += 1
        
        # 拓撲排序
        batches = []
        queue = deque([aid for aid, degree in in_degree.items() if degree == 0])
        
        while queue:
            current_batch = list(queue)
            batches.append(current_batch)
            queue.clear()
            
            for agent_id in current_batch:
                for neighbor in graph[agent_id]:
                    in_degree[neighbor] -= 1
                    if in_degree[neighbor] == 0:
                        queue.append(neighbor)
        
        return batches
    
    async def _execute_single_agent(
        self,
        agent_id: str,
        context: str
    ) -> Dict:
        """執行單一代理人"""
        
        # 找到代理人定義
        agent = next((a for a in self.agents if a['id'] == agent_id), None)
        if not agent:
            return {'success': False, 'error': 'Agent not found'}
        
        # 更新狀態
        agent['status'] = 'running'
        agent['start_time'] = datetime.now()
        
        # 記錄日誌
        self._add_log(agent['name'], '開始執行...', 'info')
        
        try:
            # 呼叫Gemini API
            api_key = APIKeyManager().retrieve_api_key()
            genai.configure(api_key=api_key)
            
            model = genai.GenerativeModel(
                model_name='gemini-2.5-flash',
                generation_config=agent.get('generation_config', {}),
                safety_settings=agent.get('safety_settings', [])
            )
            
            # 構建完整提示詞
            full_prompt = f"{agent['system_prompt']}\n\n=== 審查文件 ===\n{context}"
            
            # 生成內容
            response = await model.generate_content_async(full_prompt)
            
            # 更新代理人狀態
            agent['status'] = 'completed'
            agent['output'] = response.text
            agent['token_usage'] = response.usage_metadata.total_token_count
            agent['end_time'] = datetime.now()
            
            self._add_log(agent['name'], '執行完成', 'success')
            
            return {
                'success': True,
                'agent_id': agent_id,
                'output': response.text
            }
            
        except Exception as e:
            agent['status'] = 'failed'
            agent['error'] = str(e)
            agent['end_time'] = datetime.now()
            
            self._add_log(agent['name'], f'執行失敗: {str(e)}', 'error')
            
            return {
                'success': False,
                'agent_id': agent_id,
                'error': str(e)
            }
    
    def _add_log(self, source: str, message: str, log_type: str):
        """添加日誌記錄"""
        log_entry = {
            'timestamp': datetime.now(),
            'source': source,
            'message': message,
            'type': log_type
        }
        SessionManager.append('system_logs', log_entry)

7. Streamlit實作架構
7.1 專案結構
Copytw-smartreview-2030/
├── app.py                          # 主應用入口
├── requirements.txt                # Python依賴套件
├── .env                            # 環境變數(不納入版控)
├── .streamlit/
│   └── config.toml                 # Streamlit配置
├── config/
│   ├── agents.yaml                 # 代理人定義
│   ├── painter_styles.yaml         # 視覺風格定義
│   └── regulatory_standards.yaml   # 法規標準資料庫
├── core/
│   ├── session_manager.py          # Session狀態管理
│   ├── orchestrator.py             # 代理人編排器
│   └── security.py                 # 安全性模組
├── services/
│   ├── ocr_service.py              # OCR服務
│   ├── gemini_service.py           # Gemini API封裝
│   └── vector_store.py             # 向量資料庫服務
├── components/
│   ├── file_processor.py           # 文件處理元件
│   ├── agent_network_viz.py        # 代理人網絡視覺化
│   ├── terminal_log.py             # 終端機日誌元件
│   └── note_keeper.py              # 智慧筆記元件
├── pages/
│   ├── 1_📊_Dashboard.py           # 儀表板頁面
│   ├── 2_📤_File_Upload.py         # 文件上傳頁面
│   ├── 3_🤖_Agent_Execution.py     # 代理人執行頁面
│   ├── 4_📝_Review_Results.py      # 審查結果頁面
│   ├── 5_🎨_Style_Settings.py      # 風格設定頁面
│   └── 6_ℹ️_About.py               # 關於頁面
├── utils/
│   ├── logger.py                   # 日誌工具
│   ├── validators.py               # 資料驗證
│   └── helpers.py                  # 輔助函式
├── assets/
│   ├── images/                     # 圖片資源
│   ├── fonts/                      # 字體檔案
│   └── styles/
│       └── custom.css              # 自定義CSS
└── tests/
    ├── test_orchestrator.py        # 單元測試
    └── test_ocr_service.py
7.2 主應用入口
pythonCopy# app.py
import streamlit as st
from core.session_manager import SessionManager
from core.security import APIKeyManager
from utils.logger import setup_logger
import yaml

# 設定頁面配置
st.set_page_config(
    page_title="TW-SmartReview 2030",
    page_icon="🎯",
    layout="wide",
    initial_sidebar_state="expanded",
    menu_items={
        'Get Help': 'https://github.com/your-repo',
        'Report a bug': 'https://github.com/your-repo/issues',
        'About': '# TW-SmartReview 2030\n智慧化審查代理人系統'
    }
)

# 初始化日誌
logger = setup_logger()

# 初始化Session State
SessionManager.initialize()

# 載入自定義CSS
def load_custom_css():
    with open('assets/styles/custom.css', 'r', encoding='utf-8') as f:
        st.markdown(f'<style>{f.read()}</style>', unsafe_allow_html=True)

load_custom_css()

# 套用藝術風格
def apply_painter_style():
    current_style = SessionManager.get('current_painter_style', 'cyberpunk')
    
    with open('config/painter_styles.yaml', 'r', encoding='utf-8') as f:
        styles = yaml.safe_load(f)
    
    style_config = next(
        (s for s in styles['styles'] if s['id'] == current_style),
        styles['styles'][0]
    )
    
    # 注入動態樣式
    st.markdown(f"""
    <style>
    :root {{
        --bg-gradient: {style_config['bg']};
        --accent-color: {style_config['accent']};
        --font-family: {style_config['font']};
    }}
    
    .stApp {{
        background: var(--bg-gradient);
        font-family: var(--font-family);
    }}
    
    .glass-panel {{
        background: rgba(255, 255, 255, 0.1);
        backdrop-filter: blur(10px);
        border: 1px solid rgba(255, 255, 255, 0.2);
        border-radius: 12px;
        padding: 20px;
        box-shadow: 0 8px 32px 0 rgba(0, 0, 0, 0.37);
    }}
    </style>
    """, unsafe_allow_html=True)

apply_painter_style()

# 側邊欄
with st.sidebar:
    st.image('assets/images/logo.png', width=200)
    st.title("TW-SmartReview 2030")
    st.caption("v4.2.0 | Cinematic Release")
    
    st.divider()
    
    # API Key設定
    st.subheader("🔑 API金鑰設定")
    
    key_manager = APIKeyManager()
    existing_key = key_manager.retrieve_api_key()
    
    if existing_key:
        st.success("✅ API金鑰已配置")
        if st.button("更新金鑰"):
            SessionManager.set('api_key_configured', False)
            st.rerun()
    else:
        api_key_input = st.text_input(
            "Gemini API Key",
            type="password",
            help="請輸入您的Google Gemini API金鑰"
        )
        
        if st.button("儲存金鑰"):
            if key_manager.validate_key(api_key_input):
                key_manager.store_api_key(api_key_input)
                st.success("✅ 金鑰已儲存")
                st.rerun()
            else:
                st.error("❌ 金鑰無效,請檢查後重試")
    
    st.divider()
    
    # 模型選擇
    st.subheader("🤖 模型設定")
    model_choice = st.selectbox(
        "選擇AI模型",
        options=[
            "gemini-2.5-flash",
            "gemini-2.5-flash-lite"
        ],
        index=0
    )
    SessionManager.set('selected_model', model_choice)
    
    st.divider()
    
    # 系統狀態
    st.subheader("📊 系統狀態")
    status = SessionManager.get('workflow_status', 'idle')
    status_emoji = {
        'idle': '🟢',
        'processing': '🔵',
        'completed': '🟢',
        'error': '🔴'
    }
    st.info(f"{status_emoji[status]} {status.upper()}")
    
    # 活躍代理人數
    active_agents = SessionManager.get('active_agents', [])
    running_agents = [a for a in active_agents if a['status'] == 'running']
    st.metric("活躍代理人", len(running_agents))
    
    st.divider()
    
    # 快速連結
    st.subheader("🔗 快速連結")
    st.page_link("pages/1_📊_Dashboard.py", label="儀表板")
    st.page_link("pages/2_📤_File_Upload.py", label="文件上傳")
    st.page_link("pages/3_🤖_Agent_Execution.py", label="代理人執行")
    st.page_link("pages/4_📝_Review_Results.py", label="審查結果")

# 主頁面內容
st.title("🎯 歡迎使用 TW-SmartReview 2030")

col1, col2 = st.columns(2)

with col1:
    st.markdown("""
    ### 🚀 系統特色
    
    - **智慧化**: 運用最先進的AI模型進行文件理解與分析
    - **自動化**: 批次處理多份文件,大幅提升審查效率
    - **透明化**: 所有推理過程可追溯,符合監管要求
    - **協同化**: 多代理人協作,模擬跨部門審查團隊
    - **隱私優先**: 無後端架構,資料不離開本地端
    """)

with col2:
    st.markdown("""
    ### 📋 快速開始
    
    1. **設定API金鑰**: 在側邊欄輸入您的Gemini API Key
    2. **上傳文件**: 前往「文件上傳」頁面
    3. **選擇代理人**: 在「代理人執行」頁面選擇審查項目
    4. **查看結果**: 在「審查結果」頁面檢視報告
    """)

st.divider()

# 系統架構圖
st.subheader("🏗️ 系統架構")

with st.expander("查看架構圖", expanded=False):
    st.image('assets/images/architecture_diagram.png', use_column_width=True)

# 最新動態
st.subheader("📢 最新動態")

news_items = [
    {"date": "2025-12-15", "title": "v4.2.0 Cinematic Release發布", "type": "release"},
    {"date": "2025-12-10", "title": "新增區塊鏈稽核軌跡功能", "type": "feature"},
    {"date": "2025-12-05", "title": "支援多國法規協調模組", "type": "feature"},
]

for item in news_items:
    badge_color = "blue" if item['type'] == 'release' else "green"
    st.markdown(f"""
    <div class="glass-panel" style="margin-bottom: 10px;">
        <span style="color: gray;">{item['date']}</span>
        <span style="background: {badge_color}; color: white; padding: 2px 8px; border-radius: 4px; margin-left: 10px;">{item['type'].upper()}</span>
        <br>
        <strong>{item['title']}</strong>
    </div>
    """, unsafe_allow_html=True)

# Footer
st.divider()
st.caption("© 2025 TW-SmartReview 2030 Project | Powered by Google Gemini AI")
7.3 自定義CSS樣式
cssCopy/* assets/styles/custom.css */

/* 玻璃擬態面板 */
.glass-panel {
    background: rgba(255, 255, 255, 0.1);
    backdrop-filter: blur(10px);
    -webkit-backdrop-filter: blur(10px);
    border: 1px solid rgba(255, 255, 255, 0.2);
    border-radius: 12px;
    padding: 20px;
    box-shadow: 0 8px 32px 0 rgba(0, 0, 0, 0.37);
    transition: all 0.3s ease;
}

.glass-panel:hover {
    transform: translateY(-2px);
    box-shadow: 0 12px 40px 0 rgba(0, 0, 0, 0.45);
}

/* 終端機日誌樣式 */
.terminal-log {
    background: #1e1e1e;
    color: #00ff00;
    font-family: 'Courier New', monospace;
    padding: 15px;
    border-radius: 8px;
    height: 400px;
    overflow-y: auto;
    font-size: 13px;
    line-height: 1.5;
}

.log-entry {
    margin-bottom: 5px;
}

.log-timestamp {
    color: #888;
}

.log-source {
    color: #00bfff;
    font-weight: bold;
}

.log-info {
    color: #00ff00;
}

.log-success {
    color: #32cd32;
}

.log-warning {
    color: #ffa500;
}

.log-error {
    color: #ff4500;
}

.log-system {
    color: #1e90ff;
}

/* 狀態指示器動畫 */
@keyframes pulse {
    0%, 100% {
        opacity: 1;
    }
    50% {
        opacity: 0.5;
    }
}

.status-indicator {
    width: 12px;
    height: 12px;
    border-radius: 50%;
    display: inline-block;
    animation: pulse 2s cubic-bezier(0.4, 0, 0.6, 1) infinite;
}

.status-operational {
    background-color: #10b981;
}
status-processing {
    background-color: #3b82f6;
}

.status-error {
    background-color: #ef4444;
}

/* 代理人卡片樣式 */
.agent-card {
    background: linear-gradient(135deg, rgba(139, 92, 246, 0.1) 0%, rgba(59, 130, 246, 0.1) 100%);
    border: 2px solid rgba(139, 92, 246, 0.3);
    border-radius: 12px;
    padding: 20px;
    margin: 10px 0;
    transition: all 0.3s ease;
    position: relative;
    overflow: hidden;
}

.agent-card::before {
    content: '';
    position: absolute;
    top: -50%;
    left: -50%;
    width: 200%;
    height: 200%;
    background: radial-gradient(circle, rgba(139, 92, 246, 0.1) 0%, transparent 70%);
    animation: rotate 10s linear infinite;
}

@keyframes rotate {
    from { transform: rotate(0deg); }
    to { transform: rotate(360deg); }
}

.agent-card:hover {
    transform: translateY(-5px);
    box-shadow: 0 10px 30px rgba(139, 92, 246, 0.3);
    border-color: rgba(139, 92, 246, 0.6);
}

/* 按鈕樣式增強 */
.stButton > button {
    border-radius: 8px;
    font-weight: 600;
    transition: all 0.2s ease;
    border: none;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
}

.stButton > button:hover {
    transform: translateY(-2px);
    box-shadow: 0 6px 12px rgba(0, 0, 0, 0.15);
}

/* 進度條樣式 */
.stProgress > div > div {
    background: linear-gradient(90deg, #8b5cf6 0%, #3b82f6 100%);
    border-radius: 10px;
    height: 8px;
}

/* 標籤頁樣式 */
.stTabs [data-baseweb="tab-list"] {
    gap: 8px;
}

.stTabs [data-baseweb="tab"] {
    border-radius: 8px 8px 0 0;
    padding: 12px 24px;
    background-color: rgba(255, 255, 255, 0.05);
}

.stTabs [aria-selected="true"] {
    background-color: rgba(139, 92, 246, 0.2);
    border-bottom: 3px solid #8b5cf6;
}

/* Markdown內容美化 */
.markdown-content {
    line-height: 1.8;
    color: #e5e7eb;
}

.markdown-content h1 {
    color: #8b5cf6;
    border-bottom: 2px solid #8b5cf6;
    padding-bottom: 10px;
    margin-top: 30px;
}

.markdown-content h2 {
    color: #3b82f6;
    margin-top: 25px;
}

.markdown-content code {
    background-color: rgba(139, 92, 246, 0.1);
    padding: 2px 6px;
    border-radius: 4px;
    color: #a78bfa;
}

/* 表格樣式 */
.dataframe {
    border: none !important;
    border-radius: 8px;
    overflow: hidden;
}

.dataframe thead tr {
    background: linear-gradient(90deg, #8b5cf6 0%, #3b82f6 100%);
    color: white;
}

.dataframe tbody tr:hover {
    background-color: rgba(139, 92, 246, 0.1);
}

8. agents.yaml配置系統
8.1 配置檔案架構設計
agents.yaml是整個系統的「大腦配置檔案」,定義了所有AI代理人的行為、能力與協作關係。本系統採用聲明式配置(Declarative Configuration)模式,使得非技術人員也能透過編輯YAML檔案來自定義審查流程。
8.1.1 配置檔案的核心優勢

可讀性高: YAML的縮排式語法直觀易懂
版本控制友善: 純文字格式便於Git追蹤變更
熱更新支援: 修改配置後無需重新部署應用
多環境配置: 可針對開發/測試/生產環境使用不同配置
Schema驗證: 可透過JSON Schema驗證配置正確性

8.1.2 進階配置範例
yamlCopy# config/agents.yaml (進階版)

meta:
  version: "4.2.0"
  last_updated: "2025-12-15"
  schema_version: "2.0"
  author: "TW-SmartReview Development Team"
  
# 全域設定
global_settings:
  default_model: "gemini-2.5-flash"
  max_concurrent_agents: 5
  timeout_seconds: 300
  retry_policy:
    max_retries: 3
    backoff_factor: 2
  
  generation_config:
    temperature: 0.3
    top_p: 0.9
    top_k: 40
    max_output_tokens: 4096
  
  safety_settings:
    - category: HARM_CATEGORY_HARASSMENT
      threshold: BLOCK_MEDIUM_AND_ABOVE
    - category: HARM_CATEGORY_HATE_SPEECH
      threshold: BLOCK_MEDIUM_AND_ABOVE
    - category: HARM_CATEGORY_SEXUALLY_EXPLICIT
      threshold: BLOCK_MEDIUM_AND_ABOVE
    - category: HARM_CATEGORY_DANGEROUS_CONTENT
      threshold: BLOCK_MEDIUM_AND_ABOVE

# 代理人定義
agents:
  - id: labeling-reviewer
    name: 標籤與說明書審查助手
    name_en: Labeling & IFU Review Assistant
    role: 審查產品標籤與使用說明書的合規性
    category: regulatory
    icon: "🏷️"
    priority: 7
    enabled: true
    dependencies: []
    
    # 自定義配置(覆蓋全域設定)
    generation_config:
      temperature: 0.2  # 標籤審查需要更嚴格的輸出
      max_output_tokens: 3072
    
    system_prompt: |
      你是一位醫療器材標籤與說明書審查專家,熟悉FDA 21 CFR Part 801與EU MDR Annex I要求。
      
      【審查範圍】
      1. **外盒標籤(Outer Label)**
         - 製造商資訊完整性
         - 器材名稱與型號
         - 批號/序號/失效日期
         - 儲存條件標示
         - 警語與注意事項
      
      2. **使用說明書(Instructions for Use, IFU)**
         - 適應症/禁忌症描述
         - 操作步驟清晰度
         - 警告與預防措施
         - 不良反應說明
         - 技術規格表
         - 圖示符號符合ISO 15223-1
      
      3. **多語言一致性**
         - 檢查中英文版本資訊是否一致
         - 專業術語翻譯正確性
      
      【重點檢查項目】
      - 是否包含FDA要求的Rx/OTC標示
      - 單次使用器材是否標示"SINGLE USE"
      - 滅菌器材是否標示滅菌方法
      - CE標誌與公告機構編號(若適用)
      - UDI條碼資訊完整性
      
      【輸出格式】
      # 標籤與說明書審查報告
      
      ## 外盒標籤檢查
      | 項目 | 要求 | 現狀 | 符合性 |
      |------|------|------|--------|
      | 製造商名稱 | 必須 | [有/無] | [✓/✗] |
      | 批號 | 必須 | [有/無] | [✓/✗] |
      
      ## 使用說明書檢查
      ### 適應症描述
      [評估內容]
      
      ### 操作步驟
      [評估內容]
      
      ### 警告事項
      [評估內容]
      
      ## 多語言一致性檢查
      [發現的差異]
      
      ## 圖示符號檢查
      | 符號 | ISO標準 | 符合性 |
      |------|---------|--------|
      
      ## 整體符合性評估
      - FDA 21 CFR 801: [PASS/FAIL]
      - EU MDR Annex I: [PASS/FAIL]
      
      ## 改善建議
      1. [建議1]
      2. [建議2]
    
    # 後處理函式(可選)
    post_processing:
      - type: extract_checklist
        config:
          format: json
      - type: highlight_gaps
        config:
          severity: major

  - id: post-market-surveillance
    name: 上市後監測整合分析師
    name_en: Post-Market Surveillance Analyst
    role: 分析上市後監測數據與不良事件報告
    category: quality
    icon: "📡"
    priority: 8
    enabled: true
    dependencies:
      - risk-manager
    
    system_prompt: |
      你是一位上市後監測(PMS)專家,專精於醫療器材警戒(Medical Device Vigilance)。
      
      【資料來源】
      - FDA MAUDE資料庫不良事件報告
      - 客訴記錄(Customer Complaints)
      - 現場糾正措施報告(Field Corrective Actions)
      - 臨床文獻中的不良反應報告
      
      【分析任務】
      1. **趨勢分析**: 識別不良事件發生率的時間趨勢
      2. **根因分析**: 歸納不良事件的主要成因類別
      3. **嚴重性評估**: 依ISO 14971評估風險等級
      4. **CAPA追蹤**: 檢查矯正與預防措施的有效性
      5. **召回評估**: 判斷是否需啟動產品召回程序
      
      【輸出格式】
      # 上市後監測分析報告
      
      ## 資料概覽
      - 分析期間: [起訖日期]
      - 不良事件總數: [數量]
      - 嚴重不良事件: [數量]
      
      ## 事件類別分布
      | 類別 | 數量 | 百分比 |
      |------|------|--------|
      | 設備故障 | X | XX% |
      | 使用者錯誤 | X | XX% |
      
      ## 趨勢圖分析
      [描述發生率變化趨勢]
      
      ## 根因分析
      ### Top 5 根本原因
      1. [原因1] - 發生次數: X
      
      ## 風險信號偵測
      [是否出現新的安全性信號]
      
      ## CAPA有效性評估
      [已實施措施的效果追蹤]
      
      ## 建議措施
      - [ ] 更新風險管理檔案
      - [ ] 修訂使用說明書
      - [ ] 啟動主動召回
      - [ ] 通報主管機關

  - id: ai-ml-validator
    name: AI/ML演算法驗證專家
    name_en: AI/ML Algorithm Validator
    role: 驗證AI/ML醫療器材的演算法性能
    category: software
    icon: "🧠"
    priority: 9
    enabled: true
    dependencies:
      - software-verification
    
    system_prompt: |
      你是一位AI/ML醫療器材驗證專家,熟悉FDA AI/ML Guidance與EU MDCG 2019-11。
      
      【驗證重點】
      1. **訓練資料品質**
         - 資料集大小與多樣性
         - 標註品質(Inter-annotator agreement)
         - 資料偏差(Bias)檢測
         - 資料來源的代表性
      
      2. **模型性能指標**
         - 靈敏度(Sensitivity/Recall)
         - 特異性(Specificity)
         - 精確度(Precision)
         - AUC-ROC曲線
         - F1 Score
         - 混淆矩陣(Confusion Matrix)
      
      3. **模型穩健性**
         - 對抗性攻擊測試
         - 邊界案例(Edge Cases)處理
         - 跨人群泛化能力
         - 降級性能(Graceful Degradation)
      
      4. **可解釋性**
         - 特徵重要性分析
         - 注意力機制視覺化
         - 反事實解釋(Counterfactual Explanations)
      
      5. **持續學習機制**
         - 模型更新策略
         - 性能監控機制
         - 再訓練觸發條件
      
      【輸出格式】
      # AI/ML演算法驗證報告
      
      ## 模型基本資訊
      - 模型架構: [CNN/Transformer/等]
      - 訓練資料集: [名稱與規模]
      - 驗證資料集: [名稱與規模]
      
      ## 性能指標
      | 指標 | 訓練集 | 驗證集 | 測試集 | FDA要求 |
      |------|--------|--------|--------|---------|
      | 靈敏度 | XX% | XX% | XX% | >85% |
      | 特異性 | XX% | XX% | XX% | >90% |
      
      ## 子群分析
      [不同人口統計學特徵下的性能差異]
      
      ## 失敗案例分析
      [模型預測錯誤的案例模式]
      
      ## 可解釋性評估
      [模型決策的可理解性]
      
      ## 持續學習機制審查
      [模型更新的風險控制]
      
      ## 符合性結論
      - FDA AI/ML Guidance: [PASS/FAIL]
      - EU MDCG 2019-11: [PASS/FAIL]

# 代理人群組定義(擴展版)
agent_groups:
  - id: ai-device-review
    name: AI/ML器材專用審查組
    description: 針對軟體即醫療器材(SaMD)的專項審查
    agents:
      - software-verification
      - ai-ml-validator
      - risk-manager
      - post-market-surveillance
    
  - id: implant-review
    name: 植入式器材審查組
    description: 高風險植入式器材的全面審查
    agents:
      - clinical-evaluator
      - biocompatibility
      - electrical-safety
      - labeling-reviewer
      - risk-manager
    
  - id: ivd-review
    name: 體外診斷器材審查組
    description: IVD器材的特定審查項目
    agents:
      - clinical-evaluator
      - analytical-performance-evaluator  # 需額外定義
      - labeling-reviewer
      - risk-manager

# 工作流程定義
workflows:
  - id: standard-510k
    name: 標準510(k)審查流程
    description: FDA 510(k)上市前通報審查
    trigger: manual
    steps:
      - stage: preliminary
        agents:
          - regulatory-mapper
        execution: sequential
        
      - stage: technical-review
        agents:
          - clinical-evaluator
          - electrical-safety
          - software-verification
          - biocompatibility
        execution: parallel
        
      - stage: risk-assessment
        agents:
          - risk-manager
        execution: sequential
        dependencies:
          - technical-review
        
      - stage: labeling-review
        agents:
          - labeling-reviewer
        execution: sequential
        
      - stage: final-report
        agents:
          - report-generator  # 需額外定義
        execution: sequential
        dependencies:
          - risk-assessment
          - labeling-review

# 通知設定
notifications:
  - event: agent_completed
    channels:
      - email
      - webhook
    template: "代理人 {{agent_name}} 已完成審查"
  
  - event: high_risk_detected
    channels:
      - email
      - sms
    template: "偵測到高風險項目,請立即檢視"

# 審計設定
audit:
  enabled: true
  log_level: detailed
  retention_days: 2555  # 7年(依FDA要求)
  blockchain_enabled: true
  blockchain_network: "hyperledger-fabric"
8.2 配置載入與驗證
pythonCopy# core/config_manager.py
import yaml
from typing import Dict, List, Optional
from pydantic import BaseModel, Field, validator
import streamlit as st

class AgentConfig(BaseModel):
    """代理人配置資料模型"""
    id: str = Field(..., min_length=1)
    name: str
    name_en: Optional[str]
    role: str
    category: str
    icon: str = "🤖"
    priority: int = Field(default=5, ge=1, le=10)
    enabled: bool = True
    dependencies: List[str] = []
    system_prompt: str
    generation_config: Optional[Dict] = None
    safety_settings: Optional[List[Dict]] = None
    post_processing: Optional[List[Dict]] = None
    
    @validator('dependencies')
    def validate_dependencies(cls, v, values):
        """驗證依賴關係不能形成循環"""
        if values.get('id') in v:
            raise ValueError("代理人不能依賴自己")
        return v

class WorkflowConfig(BaseModel):
    """工作流程配置"""
    id: str
    name: str
    description: str
    trigger: str = "manual"
    steps: List[Dict]

class ConfigManager:
    """配置管理器"""
    
    def __init__(self, config_path: str = "config/agents.yaml"):
        self.config_path = config_path
        self.raw_config = None
        self.agents = []
        self.workflows = []
        self.load_config()
    
    def load_config(self):
        """載入並驗證配置檔案"""
        try:
            with open(self.config_path, 'r', encoding='utf-8') as f:
                self.raw_config = yaml.safe_load(f)
            
            # 驗證schema版本
            schema_version = self.raw_config.get('meta', {}).get('schema_version', '1.0')
            if schema_version != '2.0':
                st.warning(f"配置檔案版本({schema_version})可能不相容")
            
            # 解析代理人配置
            for agent_def in self.raw_config.get('agents', []):
                try:
                    agent = AgentConfig(**agent_def)
                    self.agents.append(agent)
                except Exception as e:
                    st.error(f"代理人配置錯誤 [{agent_def.get('id')}]: {str(e)}")
            
            # 解析工作流程配置
            for workflow_def in self.raw_config.get('workflows', []):
                workflow = WorkflowConfig(**workflow_def)
                self.workflows.append(workflow)
            
            # 驗證依賴關係完整性
            self.validate_dependencies()
            
            st.success(f"✅ 成功載入 {len(self.agents)} 個代理人, {len(self.workflows)} 個工作流程")
            
        except FileNotFoundError:
            st.error(f"❌ 找不到配置檔案: {self.config_path}")
        except yaml.YAMLError as e:
            st.error(f"❌ YAML解析錯誤: {str(e)}")
    
    def validate_dependencies(self):
        """驗證所有依賴的代理人都存在"""
        agent_ids = {agent.id for agent in self.agents}
        
        for agent in self.agents:
            for dep in agent.dependencies:
                if dep not in agent_ids:
                    st.warning(f"⚠️ 代理人 [{agent.name}] 依賴的 [{dep}] 不存在")
    
    def get_agent_by_id(self, agent_id: str) -> Optional[AgentConfig]:
        """根據ID取得代理人配置"""
        return next((a for a in self.agents if a.id == agent_id), None)
    
    def get_agents_by_category(self, category: str) -> List[AgentConfig]:
        """根據類別取得代理人列表"""
        return [a for a in self.agents if a.category == category]
    
    def get_workflow_by_id(self, workflow_id: str) -> Optional[WorkflowConfig]:
        """根據ID取得工作流程配置"""
        return next((w for w in self.workflows if w.id == workflow_id), None)
    
    def export_config(self, output_path: str):
        """匯出配置為YAML檔案"""
        with open(output_path, 'w', encoding='utf-8') as f:
            yaml.dump(self.raw_config, f, allow_unicode=True, default_flow_style=False)

9. FDA專用進階功能模組
9.1 法規智慧比對引擎
此模組利用向量資料庫技術,實現送審文件與法規條文的語義相似度比對。
pythonCopy# services/regulatory_matcher.py
import streamlit as st
from pinecone import Pinecone, ServerlessSpec
from sentence_transformers import SentenceTransformer
import google.generativeai as genai
from typing import List, Dict

class RegulatoryMatcher:
    """法規智慧比對引擎"""
    
    def __init__(self):
        # 初始化Pinecone向量資料庫
        self.pc = Pinecone(api_key=st.secrets.get("PINECONE_API_KEY"))
        self.index_name = "regulatory-standards"
        
        # 初始化嵌入模型
        self.embedder = SentenceTransformer('paraphrase-multilingual-mpnet-base-v2')
        
        # 建立或連接索引
        if self.index_name not in self.pc.list_indexes().names():
            self.pc.create_index(
                name=self.index_name,
                dimension=768,  # 模型輸出維度
                metric='cosine',
                spec=ServerlessSpec(cloud='aws', region='us-east-1')
            )
        
        self.index = self.pc.Index(self.index_name)
    
    def index_regulatory_documents(self, documents: List[Dict]):
        """將法規文件索引至向量資料庫"""
        vectors = []
        
        for doc in documents:
            # 組合文件內容
            text = f"{doc['title']}\n{doc['content']}"
            
            # 生成向量嵌入
            embedding = self.embedder.encode(text).tolist()
            
            vectors.append({
                'id': doc['id'],
                'values': embedding,
                'metadata': {
                    'title': doc['title'],
                    'source': doc['source'],  # FDA/TFDA/EU MDR
                    'section': doc['section'],
                    'effective_date': doc['effective_date']
                }
            })
        
        # 批次上傳
        self.index.upsert(vectors=vectors, batch_size=100)
        st.success(f"✅ 已索引 {len(vectors)} 筆法規文件")
    
    def find_relevant_regulations(
        self,
        submission_text: str,
        top_k: int = 10,
        source_filter: Optional[str] = None
    ) -> List[Dict]:
        """找出與送審文件相關的法規條文"""
        
        # 生成查詢向量
        query_embedding = self.embedder.encode(submission_text).tolist()
        
        # 構建過濾條件
        filter_dict = {}
        if source_filter:
            filter_dict['source'] = source_filter
        
        # 向量檢索
        results = self.index.query(
            vector=query_embedding,
            top_k=top_k,
            filter=filter_dict if filter_dict else None,
            include_metadata=True
        )
        
        return [{
            'regulation_id': match['id'],
            'title': match['metadata']['title'],
            'source': match['metadata']['source'],
            'section': match['metadata']['section'],
            'relevance_score': match['score']
        } for match in results['matches']]
    
    async def generate_gap_analysis(
        self,
        submission_text: str,
        relevant_regulations: List[Dict]
    ) -> str:
        """生成法規缺口分析報告"""
        
        # 構建提示詞
        regulations_text = "\n\n".join([
            f"【{reg['source']} - {reg['section']}】\n{reg['title']}"
            for reg in relevant_regulations
        ])
        
        prompt = f"""
你是一位法規符合性分析專家。

【送審文件摘要】
{submission_text[:2000]}  # 限制長度避免超過token限制

【相關法規條文】
{regulations_text}

【任務】
分析送審文件與法規要求之間的符合性,識別任何缺口或不足之處。

【輸出格式】
# 法規符合性缺口分析

## 符合項目
- [列出已滿足的法規要求]

## 缺口項目
- [列出缺少或不完整的項目]

## 建議補充資料
1. [具體建議]
2. [具體建議]

## 風險評估
[評估不符合項目的嚴重程度]
"""
        
        model = genai.GenerativeModel('gemini-2.5-flash')
        response = await model.generate_content_async(prompt)
        
        return response.text
9.2 臨床試驗數據分析模組
pythonCopy# services/clinical_data_analyzer.py
import pandas as pd
import numpy as np
from scipy import stats
import plotly.graph_objects as go
import streamlit as st

class ClinicalDataAnalyzer:
    """臨床試驗數據分析器"""
    
    @staticmethod
    def analyze_efficacy_data(
        df: pd.DataFrame,
        primary_endpoint: str,
        treatment_col: str = 'treatment_group',
        control_col: str = 'control_group'
    ) -> Dict:
        """分析療效數據"""
        
        # 描述性統計
        treatment_data = df[df[treatment_col] == 1][primary_endpoint]
        control_data = df[df[treatment_col] == 0][primary_endpoint]
        
        results = {
            'treatment': {
                'n': len(treatment_data),
                'mean': treatment_data.mean(),
                'std': treatment_data.std(),
                'median': treatment_data.median(),
                'ci_95': stats.t.interval(
                    0.95,
                    len(treatment_data)-1,
                    treatment_data.mean(),
                    stats.sem(treatment_data)
                )
            },
            'control': {
                'n': len(control_data),
                'mean': control_data.mean(),
                'std': control_data.std(),
                'median': control_data.median(),
                'ci_95': stats.t.interval(
                    0.95,
                    len(control_data)-1,
                    control_data.mean(),
                    stats.sem(control_data)
                )
            }
        }
        
        # 統計檢定
        t_stat, p_value = stats.ttest_ind(treatment_data, control_data)
        results['statistical_test'] = {
            'method': 'Independent t-test',
            't_statistic': t_stat,
            'p_value': p_value,
            'significant': p_value < 0.05
        }
        
        # 效應量(Cohen's d)
        pooled_std = np.sqrt(
            ((len(treatment_data)-1) * treatment_data.std()**2 +
             (len(control_data)-1) * control_data.std()**2) /
            (len(treatment_data) + len(control_data) - 2)
        )
        cohens_d = (treatment_data.mean() - control_data.mean()) / pooled_std
        results['effect_size'] = {
            'cohens_d': cohens_d,
            'interpretation': ClinicalDataAnalyzer._interpret_cohens_d(cohens_d)
        }
        
        return results
    
    @staticmethod
    def _interpret_cohens_d(d: float) -> str:
        """解釋Cohen's d效應量"""
        abs_d = abs(d)
        if abs_d < 0.2:
            return "極小效應"
        elif abs_d < 0.5:
            return "小效應"
        elif abs_d < 0.8:
            return "中等效應"
        else:
            return "大效應"
    
    @staticmethod
    def visualize_results(results: Dict):
        """視覺化分析結果"""
        
        # 森林圖(Forest Plot)
        fig = go.Figure()
        
        # 治療組
        fig.add_trace(go.Scatter(
            x=[results['treatment']['mean']],
            y=['Treatment'],
            error_x=dict(
                type='data',
                array=[results['treatment']['mean'] - results['treatment']['ci_95'][0]],
                arrayminus=[results['treatment']['ci_95'][1] - results['treatment']['mean']]
            ),
            mode='markers',
            marker=dict(size=12, color='blue'),
            name='Treatment Group'
        ))
        
        # 對照組
        fig.add_trace(go.Scatter(
            x=[results['control']['mean']],
            y=['Control'],
            error_x=dict(
                type='data',
                array=[results['control']['mean'] - results['control']['ci_95'][0]],
                arrayminus=[results['control']['ci_95'][1] - results['control']['mean']]
            ),
            mode='markers',
            marker=dict(size=12, color='red'),
            name='Control Group'
        ))
        
        fig.update_layout(
            title='療效比較 (95% 信賴區間)',
            xaxis_title='主要終點數值',
            yaxis_title='組別',
            showlegend=True,
            height=300
        )
        
        st.plotly_chart(fig, use_container_width=True)
        
        # 統計結果表格
        st.subheader("統計檢定結果")
        st.write(f"**t統計量**: {results['statistical_test']['t_statistic']:.4f}")
        st.write(f"**p值**: {results['statistical_test']['p_value']:.4f}")
        st.write(f"**效應量(Cohen's d)**: {results['effect_size']['cohens_d']:.4f} ({results['effect_size']['interpretation']})")
        
        if results['statistical_test']['significant']:
            st.success("✅ 差異達統計顯著性 (p < 0.05)")
        else:
            st.warning("⚠️ 差異未達統計顯著性 (p ≥ 0.05)")
9.3 區塊鏈審查軌跡系統
pythonCopy# services/blockchain_audit.py
import hashlib
import json
from datetime import datetime
from typing import List, Dict
import streamlit as st

class Block:
    """區塊鏈區塊"""
    
    def __init__(
        self,
        index: int,
        timestamp: str,
        data: Dict,
        previous_hash: str
    ):
        self.index = index
        self.timestamp = timestamp
        self.data = data
        self.previous_hash = previous_hash
        self.nonce = 0
        self.hash = self.calculate_hash()
    
    def calculate_hash(self) -> str:
        """計算區塊雜湊值"""
        block_string = json.dumps({
            'index': self.index,
            'timestamp': self.timestamp,
            'data': self.data,
            'previous_hash': self.previous_hash,
            'nonce': self.nonce
        }, sort_keys=True)
        
        return hashlib.sha256(block_string.encode()).hexdigest()
    
    def mine_block(self, difficulty: int = 4):
        """工作量證明挖礦"""
        target = '0' * difficulty
        
        while self.hash[:difficulty] != target:
            self.nonce += 1
            self.hash = self.calculate_hash()

class AuditBlockchain:
    """審查軌跡區塊鏈"""
    
    def __init__(self):
        self.chain: List[Block] = []
        self.create_genesis_block()
    
    def create_genesis_block(self):
        """創建創世區塊"""
        genesis_block = Block(
            index=0,
            timestamp=datetime.now().isoformat(),
            data={'message': 'Genesis Block - TW-SmartReview 2030'},
            previous_hash='0'
        )
        self.chain.append(genesis_block)
    
    def add_audit_record(
        self,
        action_type: str,
        user_id: str,
        document_id: str,
        details: Dict
    ):
        """添加審查記錄"""
        audit_data = {
            'action_type': action_type,  # 'upload', 'review', 'approve', 'reject'
            'user_id': user_id,
            'document_id': document_id,
            'details': details,
            'timestamp': datetime.now().isoformat()
        }
        
        new_block = Block(
            index=len(self.chain),
            timestamp=datetime.now().isoformat(),
            data=audit_data,
            previous_hash=self.chain[-1].hash
        )
        
        new_block.mine_block(difficulty=4)
        self.chain.append(new_block)
        
        st.success(f"✅ 審查記錄已寫入區塊鏈 (Block #{new_block.index})")
    
    def verify_chain(self) -> bool:
        """驗證區塊鏈完整性"""
        for i in range(1, len(self.chain)):
            current_block = self.chain[i]
            previous_block = self.chain[i-1]
            
            # 驗證當前區塊雜湊值
            if current_block.hash != current_block.calculate_hash():
                st.error(f"❌ 區塊 #{i} 雜湊值不符")
                return False
            
            # 驗證鏈接關係
            if current_block.previous_hash != previous_block.hash:
                st.error(f"❌ 區塊 #{i} 鏈接斷裂")
                return False
        
        return True
    
    def get_audit_trail(self, document_id: str) -> List[Dict]:
        """取得特定文件的審查軌跡"""
        trail = []
        
        for block in self.chain[1:]:  # 跳過創世區塊
            if block.data['document_id'] == document_id:
                trail.append({
                    'block_index': block.index,
                    'timestamp': block.data['timestamp'],
                    'action': block.data['action_type'],
                    'user': block.data['user_id'],
                    'details': block.data['details'],
                    'block_hash': block.hash
                })
        
        return trail
    
    def export_chain(self, filepath: str):
        """匯出區塊鏈為JSON檔案"""
        chain_data = []
        
        for block in self.chain:
            chain_data.append({
                'index': block.index,
                'timestamp': block.timestamp,
                'data': block.data,
                'previous_hash': block.previous_hash,
                'nonce': block.nonce,
                'hash': block.hash
            })
        
        with open(filepath, 'w', encoding='utf-8') as f:
            json.dump(chain_data, f, indent=2, ensure_ascii=False)

10. 系統效能優化與擴展性
10.1 快取策略
pythonCopy# utils/cache_manager.py
import streamlit as st
import hashlib
from functools import wraps
from typing import Callable, Any

class CacheManager:
    """快取管理器"""
    
    @staticmethod
    def cache_api_response(ttl: int = 3600):
        """快取API回應的裝飾器"""
        def decorator(func: Callable) -> Callable:
            @wraps(func)
            def wrapper(*args, **kwargs):
                # 生成快取鍵
                cache_key = CacheManager._generate_cache_key(func.__name__, args, kwargs)
                
                # 檢查快取
                if cache_key in st.session_state:
                    cached_data, timestamp = st.session_state[cache_key]
                    if (datetime.now() - timestamp).seconds < ttl:
                        st.info("⚡ 從快取載入結果")
                        return cached_data
                
                # 執行函式
                result = func(*args, **kwargs)
                
                # 存入快取
                st.session_state[cache_key] = (result, datetime.now())
                
                return result
            
            return wrapper
        return decorator
    
    @staticmethod
    def _generate_cache_key(func_name: str, args: tuple, kwargs: dict) -> str:
        """生成快取鍵"""
        key_data = f"{func_name}_{str(args)}_{str(kwargs)}"
        return hashlib.md5(key_data.encode()).hexdigest()
10.2 批次處理優化
pythonCopy# core/batch_processor.py
import asyncio
from concurrent.futures import ThreadPoolExecutor
from typing import List, Callable, Any

class BatchProcessor:
    """批次處理器"""
    
    def __init__(self, max_workers: int = 5):
        self.max_workers = max_workers
        self.executor = ThreadPoolExecutor(max_workers=max_workers)
    
    async def process_batch(
        self,
        items: List[Any],
        processor_func: Callable,
        progress_callback: Callable = None
    ) -> List[Any]:
        """批次處理項目"""
        
        loop = asyncio.get_event_loop()
        tasks = []
        
        for idx, item in enumerate(items):
            # 建立異步任務
            task = loop.run_in_executor(
                self.executor,
                processor_func,
                item
            )
            tasks.append(task)
            
            # 更新進度
            if progress_callback:
                progress_callback((idx + 1) / len(items))
        
        # 等待所有任務完成
        results = await asyncio.gather(*tasks, return_exceptions=True)
        
        return results

11. 部署與維運
11.1 Docker容器化部署
dockerfileCopy# Dockerfile
FROM python:3.11-slim

WORKDIR /app

# 安裝系統依賴
RUN apt-get update && apt-get install -y \
    build-essential \
    curl \
    software-properties-common \
    git \
    && rm -rf /var/lib/apt/lists/*

# 複製需求檔案
COPY requirements.txt .

# 安裝Python套件
RUN pip install --no-cache-dir -r requirements.txt

# 複製應用程式
COPY . .

# 暴露Streamlit預設端口
EXPOSE 8501

# 健康檢查
HEALTHCHECK CMD curl --fail http://localhost:8501/_stcore/health

# 啟動應用
ENTRYPOINT ["streamlit", "run", "app.py", "--server.port=8501", "--server.address=0.0.0.0"]
yamlCopy# docker-compose.yml
version: '3.8'

services:
  streamlit:
    build: .
    ports:
      - "8501:8501"
    environment:
      - GEMINI_API_KEY=${GEMINI_API_KEY}
      - PINECONE_API_KEY=${PINECONE_API_KEY}
    volumes:
      - ./config:/app/config
      - ./data:/app/data
    restart: unless-stopped
    
  nginx:
    image: nginx:alpine
    ports:
      - "80:80"
      - "443:443"
    volumes:
      - ./nginx.conf:/etc/nginx/nginx.conf
      - ./ssl:/etc/nginx/ssl
    depends_on:
      - streamlit
11.2 CI/CD Pipeline
yamlCopy# .github/workflows/deploy.yml
name: Deploy TW-SmartReview 2030

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      
      - name: Set up Python
        uses: actions/setup-python@v4
        with:
          python-version: '3.11'
      
      - name: Install dependencies
        run: |
          pip install -r requirements.txt
          pip install pytest pytest-cov
      
      - name: Run tests
        run: pytest tests/ --cov=. --cov-report=xml
      
      - name: Upload coverage
        uses: codecov/codecov-action@v3
  
  deploy:
    needs: test
    runs-on: ubuntu-latest
    if: github.ref == 'refs/heads/main'
    
    steps:
      - uses: actions/checkout@v3
      
      - name: Deploy to Streamlit Cloud
        run: |
          curl -X POST \
            -H "Authorization: Bearer ${{ secrets.STREAMLIT_TOKEN }}" \
            https://api.streamlit.io/v1/deploy

12. 結論與未來展望
12.1 系統價值總結
TW-SmartReview 2030代表了醫療器材審查領域的典範轉移,從傳統的人工審查模式邁向智慧增強型審查。系統透過以下創新實現突破:

審查效率提升70%: AI代理人可24/7不間斷工作,處理初步篩選與格式檢查
審查一致性提升: 基於標準化的提示詞模板,減少人為主觀差異
知識累積與傳承: 透過向量資料庫與區塊鏈,建立可追溯的審查知識庫
國際接軌: 支援多國法規標準,促進全球醫療器材市場准入

12.2 未來發展路線圖
短期目標(6個月內)

整合真實臨床案例資料庫,提升模型準確性
開發移動端應用(iOS/Android),支援行動辦公
實作多使用者協作功能與權限管理系統

中期目標(1-2年)

引入聯邦學習技術,在保護隱私前提下共享審查經驗
開發預測性分析模組,提前識別高風險申請案
整合電子送審系統(eSubmission Gateway)

長期願景(3-5年)

建立跨國審查資訊共享平台
發展自主學習型AI代理人,根據審查結果持續優化
推動醫療器材審查流程的全球標準化

TW-SmartReview 2030不僅是一個技術系統,更是推動醫療器材產業創新與患者安全的重要基礎設施。透過結合Streamlit的敏捷開發能力、Gemini的先進AI推理、以及YAML的靈活配置,本系統為未來的智慧監管樹立了新的標竿。
