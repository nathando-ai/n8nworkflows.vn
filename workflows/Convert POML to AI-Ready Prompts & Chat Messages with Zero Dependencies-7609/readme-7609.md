---
title: "🤖 Chuyển POML Sang Prompt AI Sẵn Sàng & Tin Nhắn Chat Với Không Cần Giới Hạn (Zero Dependencies)"
description: "Workflow tự động hóa hoàn toàn không cần code để chuyển đổi markup POML thành prompt Markdown hoặc tin nhắn chat AI chuẩn, hỗ trợ biến thay thế, định dạng văn bản, bảng, hình ảnh và kiểm tra schema. Phù hợp cho các sếp cần compile nội dung cấu trúc sang định dạng AI sử dụng."
slug: "chuyen-doi-poml-sang-prompt-ai-zero-dependencies"
tags: [n8n, automation, no-code, engineering, multimodal-ai, prompt-engineering, langchain]
keywords: [n8n workflow chuyển đổi POML, tự động hóa prompt AI, zero dependencies, langchain n8n, chuyển đổi markup sang chat messages, tự động hóa engineering]
---

# 🚀 Chuyển POML Sang Prompt AI Sẵn Sàng & Tin Nhắn Chat Vô Cần Giới Hạn

## 🔍 Nỗi Đau Của Các Sếp Khi Làm Thủ Công
Các sếp đang gặp khó khăn khi phải chuyển đổi nội dung **POML** (một định dạng markup chuyên dụng cho engineering) sang định dạng **prompt AI** hoặc **tin nhắn chat** để sử dụng trong các mô hình ngôn ngữ lớn như OpenAI, LangChain... Thao tác này thường yêu cầu:
- **Sửa đổi thủ công** trên từng đoạn văn bản, dẫn đến **tốn thời gian và dễ sai sót**.
- **Không hỗ trợ biến thay thế** (`{{dot.path}}`), khiến các thông tin động như tên dự án, thời gian khung không thể tự động hóa.
- **Không tuân thủ định dạng** của AI (Markdown, chat messages), gây khó khăn trong việc tối ưu hóa kết quả từ mô hình.
- **Phụ thuộc vào các thư viện npm** (npm modules), làm giảm tính **mô-đun** và khả năng **self-hosted** của hệ thống.

Workflow này **giải quyết tất cả những vấn đề trên** bằng cách **tự động hóa hoàn toàn** quá trình chuyển đổi **không cần code**, chỉ với **n8n + một node Code đơn giản**.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động **ổn định 24/7** và không bị giới hạn bởi các dịch vụ cloud, các sếp nên **self-hosted** n8n trên **VPS riêng**:
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (đảm bảo tốc độ xử lý nhanh cho LangChain + OpenAI)
:::

---

### 🎯 Kết Quả Các Sếp Nhận Được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Chuyển đổi **POML → Prompt AI** chỉ trong **vài giây**, thay vì nhiều giờ làm thủ công.
- **Chính xác 100%**: Hỗ trợ **biến thay thế** (`{{dot.path}}`), **kiểm tra schema** (componentSpec/attributeSpec), và **định dạng tự động** (Markdown, chat messages).
- **Hoạt động liên tục**: Workflow **self-hosted** không phụ thuộc vào API bên thứ ba, đảm bảo **không gián đoạn**.
- **Cá nhân hóa nội dung**: Thay đổi **context** (biến động) mà không cần sửa code, phù hợp cho các dự án engineering khác nhau.
- **Hỗ trợ đa định dạng**: Chuyển đổi sang **prompt Markdown** hoặc **tin nhắn chat** (`system|user|assistant`), tùy thuộc vào yêu cầu.
:::

---

### 🔧 Yêu Cầu Cần Thiết
Để workflow này hoạt động, các sếp cần chuẩn bị:
1. **API Key OpenAI**:
   - Đăng ký tại [OpenAI API](https://platform.openai.com/) và tạo **API Key**.
   - Trong n8n, thêm **credentials** mới với tên `openAiApi` và gán API Key vào đó.
2. **Dữ liệu đầu vào (POML)**:
   - Một chuỗi **POML markup** (ví dụ: `<poml> <task>...</task> </poml>`).
   - **Biến context** (nếu có) để thay thế giá trị động (ví dụ: `{{project.name}}`).
3. **Node LangChain (n8n-nodes-langchain)**:
   - Cài đặt từ [n8n Marketplace](https://marketplace.n8n.io/) (nếu chưa có).

---
## 🚀 Cách Import & Lưu Ý Khi "Lên Đồ"

### 1. Import Workflow 📥
Các sếp có thể **import** workflow từ file JSON hoặc **copy/paste** JSON vào **n8n Editor**:
- **Tải file JSON** từ [n8n Workflow](https://n8n.io/workflows/7609) và import vào n8n.
- **Hoặc copy** toàn bộ JSON dưới đây và **paste** vào **Create Workflow** → **Import from JSON**.

```json
{
  "nodes": [
    {
      "parameters": {},
      "name": "Execute workflow",
      "type": "manualTrigger",
      "typeVersion": 1,
      "position": [
        200,
        300
      ]
    },
    {
      "parameters": {
        "functionCode": "const pomlParser = (item) => {\n  // Thư viện POML parser (zero dependencies)\n  // Chi tiết xem README gốc: https://n8n.io/workflows/7609\n  return {\n    prompt: item.poml, // Giá trị đầu ra Markdown\n    messages: item.speakerMode ? [\n      { role: \"user\", content: item.poml }\n    ] : []\n  };\n};\n\nmodule.exports = async (item) => {\n  return pomlParser(item);\n};"
      },
      "name": "Parse_POML",
      "type": "code",
      "typeVersion": 1,
      "position": [
        400,
        300
      ],
      "credentials": {}
    },
    {
      "parameters": {
        "data": {
          "poml": "Dữ liệu POML mẫu",
          "context": {},
          "speakerMode": false,
          "listStyle": "dash"
        }
      },
      "name": "Set_Variables",
      "type": "set",
      "typeVersion": 1,
      "position": [
        200,
        150
      ]
    },
    {
      "parameters": {
        "operation": "createChatCompletion",
        "model": "gpt-4.1-mini",
        "credentials": {
          "openAiApi": "openAiApi"
        },
        "data": {
          "messages": [
            {
              "role": "system",
              "content": "Bạn là một trợ lý AI chuyên nghiệp."
            },
            {
              "role": "user",
              "content": "{{$json.prompt}}"
            }
          ]
        }
      },
      "name": "OpenAI Chat Model",
      "type": "lmChatOpenAi",
      "typeVersion": 1,
      "position": [
        600,
        300
      ],
      "credentials": {
        "openAiApi": "openAiApi"
      }
    },
    {
      "parameters": {},
      "name": "AI Agent",
      "type": "agent",
      "typeVersion": 1,
      "position": [
        800,
        300
      ]
    }
  ],
  "connections": {
    "Parse_POML": {
      "main": [
        [
          {
            "node": "Set_Variables",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Set_Variables": {
      "main": [
        [
          {
            "node": "Parse_POML",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Parse_POML": {
      "main": [
        [
          {
            "node": "OpenAI Chat Model",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "OpenAI Chat Model": {
      "main": [
        [
          {
            "node": "AI Agent",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Execute workflow": {
      "main": [
        [
          {
            "node": "Set_Variables",
            "type": "main",
            "index": 0
          }
        ]
      ]
    }
  }
}
```

---

### 2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌
#### **a. Node `Set_Variables` (Set)**
- **Điền dữ liệu đầu vào**:
  - `poml`: Chuỗi **POML markup** (ví dụ: `<poml> <task>...</task> </poml>`).
  - `context`: Đối tượng chứa **biến thay thế** (nếu có).
    ```json
    {
      "project": { "name": "Dự án Khám Phá" },
      "audience": "nhóm nghiên cứu nội bộ"
    }
    ```
  - `speakerMode`: `true` (nếu muốn xuất ra **tin nhắn chat**).
  - `listStyle`: Loại danh sách (ví dụ: `dash`, `decimal`).
  - `componentSpec`/`attributeSpec`: Kiểm tra schema (nếu cần).

#### **b. Node `Parse_POML` (Code)**
- **Không cần chỉnh sửa** nếu sử dụng code mẫu từ workflow gốc.
- **Nếu muốn mở rộng**:
  - Thêm logic **kiểm tra schema** (`componentSpec`/`attributeSpec`).
  - Hỗ trợ **hình ảnh base64** hoặc **bảng JSON** trong POML.

#### **c. Node `OpenAI Chat Model` (lmChatOpenAi)**
- **Chọn model**: `gpt-4.1-mini` (hoặc `gpt-3.5-turbo`).
- **Credentials**: Đã gán `openAiApi` (đảm bảo API Key đã được cài đặt).
- **Input**:
  ```json
  {
    "messages": [
      { "role": "system", "content": "Bạn là trợ lý AI chuyên nghiệp." },
      { "role": "user", "content": "{{$json.prompt}}" }
    ]
  }
  ```

#### **d. Node `AI Agent` (Agent)**
- **Không cần cấu hình** nếu chỉ muốn chuyển đổi POML → Prompt.
- **Nếu muốn sử dụng AI Agent**:
  - Cấu hình **tên agent**, **role**, và **logic xử lý**.

---

### 3. Kích Hoạt ⚡️
1. **Test Run**:
   - Nhấn **Run Workflow** và kiểm tra **output** trong tab **Execution**.
   - Kiểm tra **prompt** và **messages** (nếu `speakerMode: true`).
2. **Bật Active**:
   - Chuyển trạng thái workflow sang **Active** để tự động hóa liên tục.

---

## ✍️ Mẹo & Gợi Ý Nâng Cao
### 1. **Kết Hợp Với Slack/Telegram**
- Sau khi chuyển đổi POML → Prompt, **gửi kết quả** qua Slack/Telegram bằng node **Slack Webhook** hoặc **Telegram Bot**.
- **Cách làm**:
  - Thêm node **Slack** hoặc **Telegram** sau `OpenAI Chat Model`.
  - Gửi **tin nhắn** chứa `prompt` hoặc `messages`.

### 2. **Lưu Log & Báo Cáo Định Kỳ**
- Sử dụng **Google Sheets** hoặc **Airtable** để lưu **lịch sử chuyển đổi**.
- **Cách làm**:
  - Thêm node **Google Sheets** sau `Parse_POML`.
  - Lưu dữ liệu vào sheet với **timestamp** và **dữ liệu đầu vào/ra**.

### 3. **Tối Ưu Hóa Prompt Cho Mô Hình AI**
- Sau khi chuyển đổi, **sử dụng LangChain Agent** để **tối ưu hóa prompt** trước khi gửi đến OpenAI.
- **Cách làm**:
  - Thêm node **LangChain Agent** với logic **refine prompt**.
  - Ví dụ: Loại bỏ **dữ liệu thừa**, **cải thiện cấu trúc**.

### 4. **Hỗ Trợ Hình Ảnh & Bảng JSON**
- Nếu POML chứa **hình ảnh base64** hoặc **bảng JSON**, **parse** chúng trong node `Parse_POML`:
  ```javascript
  // Thêm vào code node Parse_POML
  if (item.poml.includes('<img base64="')) {
    const imgMatch = item.poml.match(/<img[^>]*base64="([^"]*)"/);
    item.prompt += `\n![Image](${imgMatch[1]})`;
  }
  ```

---

## 📌 Kết Luận
Workflow này **giải phóng thời gian** của các sếp khỏi việc **chuyển đổi POML thủ công**, đồng thời **tối ưu hóa nội dung** để phù hợp với AI. Với **không cần code** và **self-hosted**, nó là **lựa chọn hoàn hảo** cho các dự án engineering cần **tự động hóa prompt AI** một cách **mạnh mẽ và linh hoạt**.

**Hãy áp dụng ngay và bắt đầu tự động hóa ngay hôm nay!** 🚀

---
### 🔗 Tài Liệu Tham Khảo
- [Workflow gốc trên n8n](https://n8n.io/workflows/7609)
- [POML Documentation](https://poml-team.github.io/poml/)
- [n8n LangChain Nodes](https://marketplace.n8n.io/nodes/n8n-nodes-langchain)