---
title: "📚 **Tự Động Hóa Tìm Kiếm & Tóm Tắt Bài Nghiên Cứu Hàng Ngày từ arXiv, Gemini AI & Lưu Trữ Trên Notion**"
description: "Workflow tự động hóa lấy dữ liệu bài báo mới nhất từ arXiv, phân tích bằng Gemini AI, tóm tắt và lưu trữ trên Notion hàng ngày - Giúp các sếp tiết kiệm 10+ giờ/tháng tìm kiếm và tổng hợp thông tin khoa học."
slug: "tieu-dong-hoa-tim-kiem-bai-nghien-cuu-arxiv-gemini-notion"
tags: [n8n, automation, content-creation, ai-multimodal, research-paper, gemini-ai, notion-integration, arxiv-api]
keywords: [n8n workflow tự động hóa, lấy bài báo arXiv hàng ngày, Gemini AI tóm tắt bài báo, lưu trữ trên Notion, tự động hóa nghiên cứu khoa học, API arXiv tự động]
---

# 🚀 **Tự Động Hóa Hub Bài Nghiên Cứu Hàng Ngày với arXiv, Gemini AI & Notion**

### **Giải pháp cho các sếp:**
Bạn có phải mất **10+ giờ/tuần** để tìm kiếm, đọc và tổng hợp bài báo mới nhất từ arXiv? Hay thường xuyên bị **quên bỏ** những bài báo quan trọng vì không có hệ thống lưu trữ? **Workflow này sẽ tự động hóa toàn bộ quy trình** cho bạn:**
✅ **Lấy dữ liệu** bài báo mới nhất từ arXiv hàng ngày (không cần code)
✅ **Phân tích & tóm tắt** bằng Gemini AI (Google’s LLM mạnh nhất hiện nay)
✅ **Lưu trữ** kết quả vào Notion với định dạng chuyên nghiệp
✅ **Gửi báo cáo** tự động qua Email và Feishu (Lark) mỗi sáng

---
## 🎯 **Kết quả các sếp nhận được**
:::tip[**Lợi ích cốt lõi**]
- **Tiết kiệm 10+ giờ/tháng** tìm kiếm và đọc bài báo thủ công.
- **Đảm bảo không bỏ lỡ** bất kỳ bài báo mới nào từ arXiv.
- **Tóm tắt thông minh** bằng Gemini AI, giúp hiểu nhanh nội dung chính.
- **Lưu trữ sạch sẽ** trên Notion với định dạng chuẩn (không cần chỉnh sửa thủ công).
- **Báo cáo tự động** qua Email và Feishu, không cần nhắc nhở.
- **Cập nhật liên tục** 24/7, không phụ thuộc vào thời gian làm việc của bạn.
:::

---
## 🔧 **Yêu cầu cần thiết**
:::info[**Chuẩn bị trước khi chạy**]
Trước khi import workflow, các sếp cần chuẩn bị:
### **1. Tài khoản & API Keys**
| Dịch vụ          | Yêu cầu cụ thể                                                                 |
|-------------------|---------------------------------------------------------------------------------|
| **arXiv API**     | Không cần API key (miễn phí), chỉ cần truy cập internet.                       |
| **Google Gemini** | [Tạo API key](https://makersuite.google.com/app/apikey) và [cấu hình OAuth](https://developers.google.com/workspace/guides/create-credentials) cho Gmail. |
| **Gmail**         | [Bật Gmail API](https://developers.google.com/gmail/api/quickstart) và [cấu hình OAuth 2.0](https://developers.google.com/identity/protocols/oauth2). |
| **Notion**        | [Tạo API key](https://www.notion.so/my-integrations) và [cấu hình database](https://developers.notion.com/docs/create-a-database) với các field sau:
   - `id` (Text)
   - `title` (Title)
   - `summary` (Rich Text)
   - `author` (Multi-select)
   - `primary_category` (Single-select)
   - `category` (Multi-select)
   - `updated` (Date)
   - `published` (Date)
   - `html_url` (URL)
   - `pdf_url` (URL)
   - `github` (Text, để trống)
   - `huggingface` (Text, để trống)
   |
| **Feishu (Lark)** | [Tạo Bot](https://developers.larksuite.com/en-US/docs/im-bot/create-bot) và [cấu hình Webhook](https://developers.larksuite.com/en-US/docs/im-bot/webhook). |

### **2. Hệ thống chạy workflow**
:::info[**Gợi ý hạ tầng cho n8n**]
Để workflow chạy **ổn định 24/7**, các sếp nên cài n8n trên **VPS riêng** (Self-hosted) thay vì dùng phiên bản cloud.
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 Mã giảm giá: **VPSN8N** - giảm tới **39%**)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (Đảm bảo tốc độ nhanh, không lag).
:::

---
## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. **Tải workflow** từ [n8n.io/workflows/8847](https://n8n.io/workflows/8847) (chọn **Export as JSON**).
2. **Mở n8n Editor** và nhấn **Import** → Chọn file JSON vừa tải.
3. **Chọn "Import"** để thêm workflow vào canvas.

#### **Phương pháp 2: Copy/Paste JSON**
1. **Copy toàn bộ JSON** từ [n8n.io/workflows/8847](https://n8n.io/workflows/8847) (chọn **Export as JSON**).
2. Trong n8n Editor, nhấn **Import** → **Paste JSON** và chọn **Import**.

---
### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow có **17 node**, nhưng chỉ có **5 node quan trọng cần cấu hình** sau khi import:

#### **🔹 Node 1: Schedule Trigger (Đặt lịch chạy hàng ngày)**
- **Thời gian chạy:** **6:00 AM** (EST) để lấy dữ liệu bài báo mới nhất của ngày hôm trước.
- **Lưu ý:**
  - Node này **không cần cấu hình thêm**, chỉ cần **bật Active**.
  - Nếu muốn chạy ở giờ khác, chỉnh **cron expression** trong node này (ví dụ: `0 0 6 * * ?` cho 6:00 AM hàng ngày).

#### **🔹 Node 2: arXiv API (Lấy dữ liệu bài báo)**
- **Không cần API key**, chỉ cần **chỉnh URL** trong node `arXiv API` (type: `httpRequest`):
  ```json
  {
    "url": "http://export.arxiv.org/api/query?search_query=all_fields:&start=0&max_results=2000&sortBy=submittedDate&sortOrder=descending"
  }
  ```
  - **Lưu ý:**
    - `start=0` và `max_results=2000` để lấy **2000 bài báo mới nhất** (arXiv cho phép tối đa 2000 kết quả/lần gọi).
    - `sortBy=submittedDate&sortOrder=descending` để sắp xếp theo ngày submit mới nhất.

#### **🔹 Node 3: Data Extraction (Chuyển đổi XML thành JSON)**
- **Node này sử dụng code JavaScript** để xử lý dữ liệu từ arXiv (format XML).
- **Không cần chỉnh sửa**, nhưng các sếp nên **hiểu logic** để debug nếu có lỗi:
  ```javascript
  // Node "Data Extraction" (type: code)
  return $input.all();
  ```
  - Node này **truyền dữ liệu thô** từ arXiv sang node tiếp theo.

#### **🔹 Node 4: Google Gemini (Tóm tắt bài báo)**
- **Cấu hình credentials:**
  - Trong node `Message a model` (type: `googleGemini`), chọn **credentials** là `googlePalmApi`.
  - **Prompt mẫu** (được định sẵn trong node `Message Construction`):
    ```plaintext
    Tóm tắt bài báo này trong 3 đoạn ngắn (mỗi đoạn <100 từ), nhấn mạnh:
    1. Mục tiêu nghiên cứu
    2. Phương pháp mới
    3. Kết quả chính
    Đảm bảo không có thông tin sai lệch.
    ```
  - **Lưu ý:**
    - Nếu Gemini trả về kết quả không tốt, **cập nhật prompt** trong node `Message Construction` (type: code).

#### **🔹 Node 5: Notion Database (Lưu trữ dữ liệu)**
- **Cấu hình credentials:**
  - Trong node `RAG Daily Paper Summary` và `RAG Daily papers` (type: `notion`), chọn **credentials** là `notionApi`.
- **Field mapping (định dạng dữ liệu):**
  - **Không cần chỉnh sửa**, nhưng các sếp phải đảm bảo **Notion database** có các field như sau:
    | Field          | Loại dữ liệu       | Ghi chú                                  |
    |----------------|--------------------|------------------------------------------|
    | `id`           | Text               | URL bài báo (vd: `http://arxiv.org/abs/2409.06062v1`) |
    | `title`        | Title              | Tiêu đề bài báo                         |
    | `summary`      | Rich Text          | Tóm tắt từ Gemini                        |
    | `author`       | Multi-select       | Danh sách tác giả (phải là mảng array)  |
    | `primary_category` | Single-select | Danh mục chính (vd: `cs.CL`)           |
    | `category`     | Multi-select       | Danh sách danh mục (mảng array)          |
    | `updated`      | Date               | Thời gian cập nhật (UTC)                |
    | `published`    | Date               | Thời gian đăng (UTC)                    |
    | `html_url`     | URL                | Link trực tiếp bài báo                  |
    | `pdf_url`      | URL                | Link PDF bài báo                        |
    | `github`       | Text               | Để trống (không bắt buộc)               |
    | `huggingface`  | Text               | Để trống (không bắt buộc)               |

- **Lưu ý quan trọng:**
  - **Notion không chấp nhận `null`** → Đảm bảo tất cả field đều có giá trị (không để trống).
  - **Multi-select field** phải là **mảng array**, không phải chuỗi (vd: `[ "cs.CL", "cs.SD" ]` chứ không phải `"cs.CL, cs.SD"`).

#### **🔹 Node 6: Email & Feishu (Gửi báo cáo)**
- **Gmail:**
  - Node `Send a message` (type: `gmail`) cần **credentials** là `gmailOAuth2`.
  - **Chỉnh nội dung email** trong node `Message Construction` (type: code) nếu muốn thay đổi template.
- **Feishu (Lark):**
  - Node `FEISHU POST` (type: `httpRequest`) cần **URL Webhook** từ bot Feishu.
  - **Cấu hình payload** (định dạng JSON):
    ```json
    {
      "msg_type": "interactive",
      "card": {
        "config": {
          "wide_screen_mode": true
        },
        "elements": [
          {
            "tag": "div",
            "text": {
              "content": "📚 Bài báo mới từ arXiv",
              "tag": "lark_md"
            }
          },
          {
            "tag": "div",
            "text": {
              "content": "{{ $json.title }}",
              "tag": "lark_md"
            }
          }
        ]
      }
    }
    ```
  - **Lưu ý:**
    - Thay đổi `{{ $json.title }}` thành các field khác (vd: `{{ $json.summary }}`) nếu muốn hiển thị nội dung khác.

---
### **3. Kích hoạt ⚡️**
1. **Test Run (kiểm tra trước khi chạy thực tế):**
   - Chọn node **Schedule Trigger** → Nhấn **Run Workflow**.
   - Kiểm tra **log** để đảm bảo:
     - Dữ liệu từ arXiv được lấy đúng.
     - Gemini tóm tắt bài báo thành công.
     - Dữ liệu được lưu vào Notion và gửi Email/Feishu.
2. **Bật Active:**
   - Sau khi test thành công, **bật Active** cho node **Schedule Trigger**.

---
## ✍️ **Mẹo & gợi ý nâng cao**
### **1. Tăng số lượng bài báo lấy từ arXiv**
- Mặc định workflow lấy **2000 bài báo mới nhất**. Nếu muốn lấy nhiều hơn:
  - Chỉnh `max_results` trong node `arXiv API` lên **3000** (giá trị tối đa của arXiv).
  - **Lưu ý:** arXiv chỉ cho phép **2000 kết quả/lần gọi**, nên không thể lấy nhiều hơn.

### **2. Thêm báo cáo định kỳ vào Slack/Telegram**
- **Cách thực hiện:**
  1. Thêm node **Slack** hoặc **Telegram Bot** vào workflow.
  2. Sử dụng node `httpRequest` để gửi tin nhắn định kỳ (ví dụ: **10:00 AM**).
  3. **Payload mẫu:**
     ```json
     {
       "text": "📊 Báo cáo bài báo mới từ arXiv (ngày {{ $json.date }}):\n{{ $json.summary }}"
     }
     ```

### **3. Lưu log hoạt động vào Google Sheets**
- **Cách thực hiện:**
  1. Thêm node **Google Sheets** (n8n-nodes-base.googleSheets).
  2. Cấu hình để ghi **log** của workflow (vd: thời gian chạy, số bài báo lấy được).
  3. **Payload mẫu:**
     ```json
     {
       "values": [
         [
           "{{ $json.timestamp }}",
           "{{ $json.paperCount }}",
           "{{ $json.status }}"
         ]
       ]
     }
     ```

### **4. Cập nhật prompt cho Gemini**
- Nếu muốn **Gemini tóm tắt bài báo theo cách riêng**, chỉnh sửa node `Message Construction` (type: code):
  ```javascript
  // Ví dụ: Tóm tắt bài báo về AI với trọng tâm khác
  return {
    content: `Tóm tắt bài báo này trong 3 đoạn ngắn, nhấn mạnh:
    1. Ứng dụng thực tế của nghiên cứu
    2. So sánh với các phương pháp trước đó
    3. Điểm mạnh/điểm yếu của phương pháp mới.
    Đảm bảo không