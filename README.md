# Azure AI Search + Azure OpenAI Demo

這個專案是一組 Python 範例，用來示範如何在 Azure AI Search 中建立索引、上傳資料、進行關鍵字搜尋、向量搜尋、混合搜尋與語意搜尋，並搭配 Azure OpenAI Embeddings 產生向量。

本專案適合拿來學習：

- Azure AI Search 基本 CRUD
- Azure OpenAI text embeddings
- 向量搜尋（Vector Search）
- 混合搜尋（Hybrid Search）
- 語意搜尋（Semantic Search）
- 酒店資料索引與查詢實作

---

## 專案目標

此程式碼庫的重點是展示 Azure AI Search 在實務上的常見工作流：

1. 建立 Search Index
2. 上傳文件資料
3. 使用 Azure OpenAI 產生 embeddings
4. 建立向量欄位（如 `titleVector`、`contentVector`）
5. 執行搜尋（簡單查詢、向量查詢、混合查詢與語意查詢）
6. 針對旅館資料呈現更完整的搜尋能力

---

## 專案結構

```text
.
├── .env
├── app.log
├── hotels-small.json
├── text-sample.json
├── text-sample-embeddings.json
├── azure_ai_search_create_vector_index.py
├── azure_ai_search_hotel_index.py
├── azure_ai_search_hybrid_search.py
├── azure_ai_search_index_crud.py
├── azure_ai_search_index_maintenance.py
├── azure_ai_search_semantic_hybrid_search.py
├── azure_ai_search_simple_query.py
├── azure_ai_search_upload_json_data.py
├── azure_ai_search_upload_vector_documents.py
├── azure_ai_search_vector_search.py
├── azure_openai_generate_embeddings.py
└── README.md
```

### 主要腳本簡介

- `azure_openai_generate_embeddings.py`
  - 使用 Azure OpenAI 產生文本 embedding
  - 將結果寫入 `text-sample-embeddings.json`

- `azure_ai_search_create_vector_index.py`
  - 建立含向量欄位的 Azure AI Search index

- `azure_ai_search_upload_json_data.py`
  - 將 JSON 文件上傳到 Search Index

- `azure_ai_search_upload_vector_documents.py`
  - 上傳已帶向量欄位的文件資料

- `azure_ai_search_vector_search.py`
  - 執行向量搜尋 Demo

- `azure_ai_search_hybrid_search.py`
  - 執行 hybrid search（關鍵字 + 向量）

- `azure_ai_search_semantic_hybrid_search.py`
  - 結合語意搜尋與 hybrid search 的進階查詢

- `azure_ai_search_simple_query.py`
  - 基本查詢範例

- `azure_ai_search_index_crud.py`
  - 建立、顯示、刪除索引的 CRUD 範例

- `azure_ai_search_hotel_index.py`
  - 為酒店資料建立索引與上傳範例

- `azure_ai_search_index_maintenance.py`
  - 維護索引、更新與管理相關操作

---

## 環境需求

- Python 3.10+
- Azure Subscription
- Azure AI Search Service
- Azure OpenAI Resource
- 有效的 Azure AI Search API Key

---

## 安裝依賴

在專案根目錄執行：

```bash
pip install python-dotenv azure-search-documents openai rich
```

如果你使用的是虛擬環境，也可先啟用後再安裝。

---

## 設定環境變數

請確認專案根目錄已有 `.env` 檔案，並包含以下變數：

```env
AZURE_AI_SEARCH_API_ENDPOINT=https://<your-search-service>.search.windows.net
AZURE_AI_SEARCH_API_KEY=<your-search-admin-key>
AZURE_AI_SEARCH_INDEX_NAME=azure-ai-search-demo-index
AZURE_AI_SEARCH_HOTEL_INDEX_NAME=hotels-index

AZURE_OPENAI_API_KEY=<your-openai-key>
AZURE_OPENAI_API_VERSION=2024-12-01-preview
AZURE_OPENAI_API_EMBEDDING_ENDPOINT=https://<your-openai-resource>.openai.azure.com/
AZURE_OPENAI_API_EMBEDDING_DEPLOYMENT=text-embedding-3-small
```

> 注意：請不要將 `.env` 內容提交到 Git，並確保敏感資訊不被公開。

---

## 執行方式

### 1. 產生 embeddings

```bash
python azure_openai_generate_embeddings.py
```

這會讀取 `text-sample.json`，並產生向量欄位後輸出 `text-sample-embeddings.json`。

### 2. 建立一般索引

```bash
python azure_ai_search_index_crud.py
```

這個腳本會建立索引，並可依需求切換 `create_index()`、`delete_index()`、`show_all_index()` 等功能。

### 3. 上傳文件

```bash
python azure_ai_search_upload_json_data.py
```

### 4. 執行向量搜尋

```bash
python azure_ai_search_vector_search.py
```

### 5. 執行 hybrid / semantic 查詢

```bash
python azure_ai_search_hybrid_search.py
python azure_ai_search_semantic_hybrid_search.py
python azure_ai_search_simple_query.py
```

### 6. 酒店資料範例

```bash
python azure_ai_search_hotel_index.py
```

這會建立酒店索引並上傳 `hotels-small.json` 內的資料。

---

## 資料範例

### `text-sample.json`
這是一組簡單文本資料，包含 `title` 和 `content` 欄位，適合用於 embedding 與向量搜尋 demo。

### `hotels-small.json`
這是一份酒店資料集，包含：

- hotelId
- hotelName
- description
- category
- tags
- rating
- address
- rooms
- location

適合展示 Azure AI Search 的結構化資料查詢與語意搜尋能力。

---

## 常見用途

這個專案可作為以下場景的參考：

- 知識庫搜尋
- 文件檢索
- 客服問題搜尋
- 商品/旅館/文章向量相似度搜尋
- AI 驅動的語意搜尋應用

---

## 開發筆記

- `text-sample-embeddings.json` 會在執行 embedding 產生器後產生
- `app.log` 會記錄執行過程中的日志
- 若執行過程出現權限或設定錯誤，最常見原因為：
  - `.env` 未正確設定
  - Azure AI Search endpoint/key 無效
  - Azure OpenAI deployment 名稱不正確
  - 目標 index 不存在

---

## 進階建議

如果你想把這個專案延伸為完整應用，可以進一步加入：

- FastAPI / Flask Web API
- 前端搜尋 UI
- 權限與角色管理
- RAG（Retrieval-Augmented Generation）流程
- 更大規模資料集與自動化索引更新

---

## License

此專案僅供學習與實驗用途，請依照你的 Azure / OpenAI 帳號與環境條款使用。
