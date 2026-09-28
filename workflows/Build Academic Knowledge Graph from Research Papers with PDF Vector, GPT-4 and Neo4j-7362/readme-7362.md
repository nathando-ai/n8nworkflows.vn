---
title: "🧠 **Tự Động Xây Dựng Bảng Mạng Tri Thức (Knowledge Graph) Từ Bài Nghiên Cứu PDF Với GPT-4 & Neo4j - AI RAG 100% Không Code**"
description: "Workflow tự động hóa lấy dữ liệu từ PDF, phân tích bằng GPT-4, xây dựng và cập nhật liên tục bảng mạng tri thức (knowledge graph) trong Neo4j. Giúp các sếp phân tích nhanh, kết nối thông tin và tìm kiếm thông minh trong lĩnh vực nghiên cứu khoa học."
slug: "tieu-dong-xay-dung-knowledge-graph-neo4j-gpt4"
tags: [n8n, automation, ai-rag, multimodal-ai, neo4j, gpt-4, pdf-vector, knowledge-graph]
keywords: [tự động hóa n8n, xây dựng knowledge graph, ai rag pdf, neo4j với gpt-4, phân tích bài báo khoa học tự động, tự động hóa nghiên cứu khoa học]
---

# 🚀 **Tự Động Xây Dựng Bảng Mạng Tri Thức (Knowledge Graph) Từ Bài Nghiên Cứu PDF**

Hiện nay, việc phân tích hàng ngàn bài báo khoa học để tổng hợp kiến thức là một thách thức lớn đối với các nhà nghiên cứu, doanh nghiệp và tổ chức. Các sếp thường phải mất nhiều thời gian để đọc, tóm tắt và kết nối thông tin từ nhiều nguồn khác nhau. **Workflow này giải quyết vấn đề này bằng cách tự động hóa toàn bộ quy trình:**
- **Lấy dữ liệu** từ PDF của các bài báo khoa học.
- **Phân tích nội dung** bằng GPT-4 để trích xuất khái niệm, tác giả, phương pháp, và mối quan hệ.
- **Xây dựng và cập nhật** liên tục một **bảng mạng tri thức (Knowledge Graph)** trong Neo4j.
- **Lưu lịch sử cập nhật** trong cơ sở dữ liệu PostgreSQL để theo dõi tiến trình.

Kết quả? Các sếp có thể **tìm kiếm thông tin liên quan, phát hiện mối quan hệ mới và tổng hợp kiến thức một cách nhanh chóng và chính xác** mà không cần viết một dòng code nào.

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động ổn định 24/7, các sếp nên cài đặt n8n trên **VPS riêng (Self-hosted)** để đảm bảo tính riêng tư và hiệu suất cao.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần đọc thủ công hàng ngàn trang PDF.
- **Tìm kiếm thông minh**: Query trong Neo4j để khám phá mối quan hệ giữa khái niệm, tác giả, phương pháp và dữ liệu.
- **Cập nhật tự động**: Workflow chạy hàng ngày để cập nhật kiến thức mới nhất.
- **Dữ liệu sạch và cấu trúc**: Trích xuất thông tin chính xác từ PDF và lưu vào Knowledge Graph.
- **Lịch sử rõ ràng**: Ghi lại tất cả các cập nhật trong PostgreSQL để theo dõi tiến trình.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản PDF Vector** (để lấy và phân tích PDF):
   - [Đăng ký tài khoản PDF Vector](https://pdfvector.com/) (miễn phí hoặc trả phí tùy thuộc vào nhu cầu).
   - **API Key** của PDF Vector.
2. **Tài khoản OpenAI** (để sử dụng GPT-4):
   - [Đăng ký OpenAI](https://platform.openai.com/) và lấy **API Key**.
3. **Cơ sở dữ liệu Neo4j** (để lưu trữ Knowledge Graph):
   - [Tạo tài khoản Neo4j AuraDB](https://neo4j.com/cloud/aura/) (miễn phí hoặc trả phí).
   - **URI** và **Tên người dùng/Mật khẩu** của Neo4j.
4. **Cơ sở dữ liệu PostgreSQL** (để lưu log cập nhật):
   - [Tạo cơ sở dữ liệu PostgreSQL](https://supabase.com/) hoặc sử dụng dịch vụ khác.
   - **Host, Port, Tên người dùng, Mật khẩu, Tên cơ sở dữ liệu**.
5. **Thiết lập n8n Self-hosted**:
   - Cài đặt n8n trên VPS (hướng dẫn tại [n8n.io](https://n8n.io/)).
   - Cấu hình **credentials** cho các node (PDF Vector, OpenAI, Neo4j, PostgreSQL).

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### 1. **Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/7362) hoặc sử dụng mã JSON dưới đây:
  ```json
  {
    "nodes": [
      {
        "parameters": {
          "cronTimezone": "Asia/Ho_Chi_Minh",
          "cronExpression": "0 0 * * *"
        },
        "name": "Daily KB Update",
        "type": "n8n-nodes-base.scheduleTrigger",
        "position": [100, 300]
      },
      {
        "parameters": {
          "resource": "academic",
          "operation": "search",
          "query": "computer vision",
          "limit": 10
        },
        "name": "PDF Vector - Fetch Papers",
        "type": "n8n-nodes-pdfvector.pdfVector",
        "position": [100, 500],
        "credentials": {
          "pdfVectorApi": "pdfVectorApi"
        }
      },
      {
        "parameters": {
          "resource": "document",
          "operation": "parse",
          "file": "$node[PDF Vector - Fetch Papers].json[0].file"
        },
        "name": "PDF Vector - Parse Papers",
        "type": "n8n-nodes-pdfvector.pdfVector",
        "position": [300, 500],
        "credentials": {
          "pdfVectorApi": "pdfVectorApi"
        }
      },
      {
        "parameters": {
          "model": "gpt-4",
          "prompt": "Extract entities from the following text: {{ $json['content'] }}",
          "temperature": 0.5
        },
        "name": "Extract Entities",
        "type": "n8n-nodes-base.openAi",
        "position": [500, 500],
        "credentials": {
          "openAiApi": "openAiApi"
        }
      },
      {
        "parameters": {
          "code": "// Build graph structure from extracted entities\nconst entities = $node[\"Extract Entities\"].json;\nconst graphNodes = [];\nconst graphRelationships = [];\n\n// Example: Create nodes for concepts, authors, etc.\nentities.forEach(entity => {\n  graphNodes.push({\n    label: entity.type,\n    properties: {\n      name: entity.name,\n      description: entity.description\n    }\n  });\n\n  // Create relationships (e.g., 'CONTAINS', 'AUTHORED_BY')\n  if (entity.type === 'Concept' && entity.relatedTo) {\n    entity.relatedTo.forEach(related => {\n      graphRelationships.push({\n        from: entity.name,\n        to: related,\n        type: 'RELATED_TO'\n      });\n    });\n  }\n});\n\nreturn {\n  graphNodes,\n  graphRelationships\n};"
        },
        "name": "Build Graph Structure",
        "type": "n8n-nodes-base.code",
        "position": [700, 500]
      },
      {
        "parameters": {
          "operation": "create",
          "uri": "$node[\"Build Graph Structure\"].json[0].graphNodes",
          "labels": "Node",
          "properties": {
            "name": "name",
            "description": "description"
          }
        },
        "name": "Create Graph Nodes",
        "type": "n8n-nodes-base.neo4j",
        "position": [900, 500],
        "credentials": {
          "neo4j": "neo4j"
        }
      },
      {
        "parameters": {
          "operation": "create",
          "statements": "$node[\"Build Graph Structure\"].json[0].graphRelationships.map(rel => `CREATE (a:${rel.from})-[r:RELATED_TO]->(b:${rel.to})`)"
        },
        "name": "Create Relationships",
        "type": "n8n-nodes-base.neo4j",
        "position": [900, 700],
        "credentials": {
          "neo4j": "neo4j"
        }
      },
      {
        "parameters": {
          "code": "// Calculate statistics for the knowledge base\nconst nodes = $node[\"Create Graph Nodes\"].json;\nconst relationships = $node[\"Create Relationships\"].json;\n\nreturn {\n  totalNodes: nodes.length,\n  totalRelationships: relationships.length,\n  lastUpdated: new Date().toISOString()\n};"
        },
        "name": "KB Statistics",
        "type": "n8n-nodes-base.code",
        "position": [1100, 500]
      },
      {
        "parameters": {
          "operation": "insert",
          "table": "kb_updates",
          "columns": {
            "total_nodes": "$node[\"KB Statistics\"].json[0].totalNodes",
            "total_relationships": "$node[\"KB Statistics\"].json[0].totalRelationships",
            "last_updated": "$node[\"KB Statistics\"].json[0].lastUpdated"
          }
        },
        "name": "Log KB Update",
        "type": "n8n-nodes-base.postgres",
        "position": [1100, 700],
        "credentials": {
          "postgresDb": "postgresDb"
        }
      }
    ],
    "connections": {
      "Daily KB Update": {
        "main": ["PDF Vector - Fetch Papers"]
      },
      "PDF Vector - Fetch Papers": {
        "main": ["PDF Vector - Parse Papers"]
      },
      "PDF Vector - Parse Papers": {
        "main": ["Extract Entities"]
      },
      "Extract Entities": {
        "main": ["Build Graph Structure"]
      },
      "Build Graph Structure": {
        "main": ["Create Graph Nodes"],
        "main2": ["Create Relationships"]
      },
      "Create Graph Nodes": {
        "main": ["KB Statistics"]
      },
      "Create Relationships": {
        "main": ["KB Statistics"]
      },
      "KB Statistics": {
        "main": ["Log KB Update"]
      }
    }
  }
  ```
- **Copy/paste JSON** vào **n8n Editor** và nhấn **Import Workflow**.

---

#### 2. **Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
##### **a. Cấu hình Credentials**
Các sếp cần thiết lập **credentials** cho các node quan trọng:
1. **PDF Vector**:
   - Tạo **credentials** mới trong n8n với tên `pdfVectorApi`.
   - Điền **API Key** từ tài khoản PDF Vector.
2. **OpenAI**:
   - Tạo **credentials** mới với tên `openAiApi`.
   - Điền **API Key** từ OpenAI.
3. **Neo4j**:
   - Tạo **credentials** mới với tên `neo4j`.
   - Điền:
     - **URI**: `neo4j+s://<your-uri>.neo4j.io`
     - **Username** và **Password**.
4. **PostgreSQL**:
   - Tạo **credentials** mới với tên `postgresDb`.
   - Điền:
     - **Host**, **Port**, **Database Name**.
     - **Username** và **Password**.

##### **b. Cấu hình Node "PDF Vector - Fetch Papers"**
- **Query**: Thay đổi từ `"computer vision"` thành chủ đề nghiên cứu của các sếp (ví dụ: `"machine learning"`, `"quantum computing"`).
- **Limit**: Điều chỉnh số lượng bài báo lấy về (mặc định là 10).

##### **c. Cấu hình Node "Extract Entities"**
- **Prompt**: Có thể tùy chỉnh prompt để phù hợp với yêu cầu cụ thể:
  ```json
  "prompt": "Extract the following entities from the text: Concepts, Authors, Institutions, Methods, Datasets, and Citations. Return in JSON format with keys: type, name, description, and relatedTo."
  ```

##### **d. Cấu hình Node "Build Graph Structure" (Code)**
- **Logic trong Code**: Các sếp có thể chỉnh sửa logic để phù hợp với yêu cầu cụ thể của Knowledge Graph (ví dụ: thêm loại node mới, thay đổi loại mối quan hệ).

##### **e. Cấu hình Node "Log KB Update" (PostgreSQL)**
- **Table**: Đảm bảo bảng `kb_updates` đã tồn tại trong PostgreSQL với các cột:
  - `total_nodes` (INT)
  - `total_relationships` (INT)
  - `last_updated` (TIMESTAMP)

---

#### 3. **Kích hoạt ⚡️**
1. **Test Run**:
   - Chạy **Manual Execution** để kiểm tra workflow với dữ liệu mẫu.
   - Kiểm tra các node quan trọng:
     - **PDF Vector - Fetch Papers**: Đã lấy được dữ liệu PDF không?
     - **Extract Entities**: GPT-4 đã trích xuất được entities không?
     - **Create Graph Nodes/Relationships**: Neo4j đã tạo được node và mối quan hệ không?
     - **Log KB Update**: PostgreSQL đã ghi log không?
2. **Bật Active**:
   - Sau khi test thành công, chuyển **Daily KB Update** sang **Active** để workflow chạy tự động hàng ngày.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Kết nối với Slack/Telegram**:
   - Thêm node **Slack** hoặc **Telegram** để thông báo khi cập nhật Knowledge Graph mới.
   - Ví dụ: Gửi tin nhắn `"Knowledge Graph đã cập nhật với {{ $node[\"KB Statistics\"].json[0].totalNodes }} node mới!"`.

2. **Lưu log chi tiết**:
   - Thêm node **Sticky Note** để lưu trữ dữ liệu trích xuất từ PDF trước khi gửi đến GPT-4.
   - Có thể sử dụng node **File System** để lưu file PDF và metadata vào máy chủ.

3. **Tối ưu hóa GPT-4**:
   - Sử dụng **temperature** thấp hơn (ví dụ: `0.2`) để kết quả trích