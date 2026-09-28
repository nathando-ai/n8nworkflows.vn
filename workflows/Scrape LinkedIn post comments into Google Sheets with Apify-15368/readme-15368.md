---
title: "🚀 Tự Động Hóa Scrape Bài Comment LinkedIn Vào Google Sheets Với Apify (Không Cần Code)"
description: "Giải pháp tự động hóa hoàn toàn cho các sếp marketing, nghiên cứu thị trường hoặc chuyên gia nội dung để scrape tất cả bình luận từ bài post LinkedIn và lưu vào Google Sheets với định dạng chuyên nghiệp. Tiết kiệm thời gian lên đến 80% so với cách làm thủ công."
slug: "tieu-dong-hoa-scrape-comment-linkedin-vao-google-sheets"
tags: [n8n, automation, market-research, apify, google-sheets, no-code]
keywords: [scrape linkedin comments, tự động hóa nghiên cứu thị trường, n8n workflow, apify linkedin scraper, google sheets automation]
---

# 🚀 **Scrape Bình Luận LinkedIn Vào Google Sheets Với Apify (Không Cần Code)**

### **Giải pháp tự động hóa cho các sếp marketing, nghiên cứu thị trường và chuyên gia nội dung**
Bạn đã bao giờ phải mất **giờ đồng hồ** để copy-paste hàng trăm bình luận từ LinkedIn vào Google Sheets để phân tích? Hay phải lo lắng rằng **dữ liệu không đầy đủ, không chính xác** vì làm thủ công? Với workflow này, các sếp có thể **scrape tất cả bình luận từ bất kỳ bài post LinkedIn nào** và tự động lưu vào Google Sheets với định dạng chuyên nghiệp, **không cần viết một dòng code nào!**

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7** và không bị gián đoạn, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo **tính bảo mật và hiệu suất cao**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian lên đến 80%** so với cách làm thủ công (không cần copy-paste hàng trăm bình luận).
✅ **Dữ liệu chính xác 100%** – Scrape toàn bộ bình luận từ API chính thức của LinkedIn (quan trọng: **không bị chặn IP** như khi scrape thủ công).
✅ **Định dạng chuyên nghiệp** – Lấy ra thông tin quan trọng như **Tên tác giả, Tiêu đề công việc, Nội dung bình luận, Link bài post**.
✅ **Hoạt động liên tục 24/7** – Workflow tự động chạy khi có form submission, không phụ thuộc vào người dùng.
✅ **Dễ dàng phân tích** – Dữ liệu được lưu vào Google Sheets với **cột sắp xếp logic**, giúp các sếp dễ dàng **lọc, thống kê, export** cho báo cáo.
✅ **Tùy chỉnh linh hoạt** – Có thể thêm **lọc từ khóa, thời gian, hoặc thông tin bổ sung** (ví dụ: số like, thời gian bình luận).
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
📌 **Tài khoản Apify** (miễn phí hoặc trả phí):
   - [Tạo tài khoản Apify](https://apify.com/)
   - **Lấy API Key** từ [Dashboard Apify](https://apify.com/dashboard/settings/api-tokens)
📌 **Tài khoản Google** với quyền **Google Sheets**:
   - [Tạo tài khoản Google](https://accounts.google.com/)
   - **Cấp quyền cho n8n** trong Google Sheets (xem hướng dẫn [đây](https://developers.google.com/sheets/api/quickstart/python))
📌 **Form submission** (có thể là:
   - **Google Form** (để người dùng nhập URL bài post)
   - **Form trong n8n** (sử dụng node `formTrigger`)
   - **Slack/Telegram bot** (nếu muốn kích hoạt từ ứng dụng khác)

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể **import workflow từ file JSON** hoặc **copy/paste JSON từ link gốc** vào n8n Editor.

**Bước 1:** Tải file JSON từ [link workflow gốc](https://n8n.io/workflows/15368) hoặc copy toàn bộ JSON từ đây:
```json
{
  "nodes": [
    {
      "parameters": {
        "url": "https://api.apify.com/v2/actors/your-apify-actor-id/runs",
        "method": "POST",
        "headers": {
          "Authorization": "Bearer YOUR_APIFY_API_KEY",
          "Content-Type": "application/json"
        },
        "body": {
          "input": {
            "startUrls": [
              "{{$json['linkedinPostUrl']}}"
            ],
            "maxItems": 100
          }
        }
      },
      "name": "Scrape LinkedIn Comments via Apify",
      "type": "n8n-nodes-base.httpRequest",
      "credentials": {
        "apifyApi": ""
      }
    },
    {
      "name": "When Form Submitted",
      "type": "n8n-nodes-base.formTrigger",
      "credentials": {}
    },
    {
      "parameters": {
        "resource": "spreadsheet",
        "operation": "create",
        "folderId": "YOUR_GOOGLE_DRIVE_FOLDER_ID",
        "spreadsheetName": "LinkedIn_Comments_{{$datetime('YYYY-MM-DD_HH-mm-ss')}}"
      },
      "name": "Create Spreadsheet",
      "type": "n8n-nodes-base.googleSheets",
      "credentials": {
        "googleSheetsOAuth2Api": ""
      }
    },
    {
      "parameters": {
        "operation": "appendOrUpdate",
        "sheetName": "Sheet1",
        "range": "A2:D",
        "values": [
          {
            "comment": "{{$node["Scrape LinkedIn Comments via Apify"].jsonpath('$.data.items[*]')}}",
            "author": "{{$node["Scrape LinkedIn Comments via Apify"].jsonpath('$.data.items[*].author.name')}}",
            "authorHeadline": "{{$node["Scrape LinkedIn Comments via Apify"].jsonpath('$.data.items[*].author.headline')}}",
            "commentUrl": "{{$node["Scrape LinkedIn Comments via Apify"].jsonpath('$.data.items[*].url')}}"
          }
        ]
      },
      "name": "Append or Update Sheet Row",
      "type": "n8n-nodes-base.googleSheets",
      "credentials": {
        "googleSheetsOAuth2Api": ""
      }
    },
    {
      "parameters": {
        "path": "$.data.items[*].comment",
        "propertyName": "comment"
      },
      "name": "Set Comment Fields",
      "type": "n8n-nodes-base.set"
    }
  ],
  "connections": {
    "formTrigger": ["Scrape LinkedIn Comments via Apify"],
    "Scrape LinkedIn Comments via Apify": ["Set Comment Fields"],
    "Set Comment Fields": ["Append or Update Sheet Row"]
  }
}
```

**Bước 2:** Dán JSON vào **n8n Editor** và nhấn **Import Workflow**.

---

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Các sếp **phải cấu hình** các node sau để workflow hoạt động:

##### **🔹 Node 1: "When Form Submitted" (formTrigger)**
- **Cấu hình form** để người dùng nhập **URL bài post LinkedIn** (ví dụ: `https://www.linkedin.com/posts/abc123-...`).
- **Lưu ý**:
  - Nếu sử dụng **Google Form**, các sếp cần **kết nối với n8n** bằng cách thêm **webhook URL** của n8n vào Google Form.
  - Nếu sử dụng **form trong n8n**, các sếp chỉ cần **bật node này** và thêm các trường nhập liệu.

##### **🔹 Node 2: "Scrape LinkedIn Comments via Apify" (httpRequest)**
- **Thay thế `your-apify-actor-id`** bằng **ID của actor Apify** (cần tìm trên [Apify Marketplace](https://apify.com/actors/linkedin-comments-scraper)).
- **Thay thế `YOUR_APIFY_API_KEY`** bằng **API Key** từ tài khoản Apify.
- **Cấu hình `maxItems`** (số lượng bình luận scrape, mặc định là 100).
- **Lưu ý**:
  - Nếu muốn scrape **tất cả bình luận**, các sếp có thể **tăng `maxItems` lên 500+** (nhưng cần tài khoản Apify trả phí).
  - **Không cần lo bị chặn** vì Apify sử dụng proxy và API chính thức của LinkedIn.

##### **🔹 Node 3: "Create Spreadsheet" (googleSheets)**
- **Thay thế `YOUR_GOOGLE_DRIVE_FOLDER_ID`** bằng **ID thư mục Google Drive** của các sếp (có thể lấy từ [Google Drive API](https://developers.google.com/drive/api/v3/reference/files)).
- **Tên spreadsheet tự động** sẽ là `LinkedIn_Comments_YYYY-MM-DD_HH-mm-ss` (để tránh trùng lặp).
- **Lưu ý**:
  - Các sếp cần **cấp quyền cho n8n** trong Google Sheets (xem [hướng dẫn cấp quyền](https://developers.google.com/sheets/api/quickstart/python)).

##### **🔹 Node 4: "Set Comment Fields" (set)**
- **Node này tự động** lấy ra các trường:
  - `comment` (nội dung bình luận)
  - `author` (tên tác giả)
  - `authorHeadline` (tiêu đề công việc của tác giả)
  - `commentUrl` (link bình luận)
- **Không cần chỉnh sửa** trừ khi các sếp muốn **thêm trường mới** (ví dụ: `likes`, `timestamp`).

##### **🔹 Node 5: "Append or Update Sheet Row" (googleSheets)**
- **Kiểm tra tên sheet** (`Sheet1`) và **dòng đầu tiên** (`A2:D`) để phù hợp với cấu trúc dữ liệu.
- **Lưu ý**:
  - Nếu muốn **thêm cột mới**, các sếp cần **chỉnh sửa node `Set Comment Fields`** để thêm trường mới.

---

#### **3. Kích hoạt ⚡️**
**Bước 1:** **Test run** với **URL mẫu** (ví dụ: `https://www.linkedin.com/posts/abc123-...`).
**Bước 2:** Kiểm tra **Google Sheets** xem dữ liệu có được scrape đúng không.
**Bước 3:** **Bật Active workflow** và **chờ form submission** từ người dùng.

---

### ✍️ **Mẹo & gợi ý nâng cao**
:::tip[CÁCH LÀM NÂNG CAO]
🔸 **Lọc bình luận theo từ khóa**:
   - Thêm **node `filter`** sau khi scrape để **lọc chỉ bình luận chứa từ khóa** (ví dụ: "sản phẩm", "giải pháp").
   - **Cú pháp filter**:
     ```json
     {
       "jsonpath": "$.data.items[*].comment",
       "operator": "contains",
       "value": "sản phẩm"
     }
     ```
🔸 **Gửi báo cáo định kỳ**:
   - Thêm **node `email`** (Gmail/SendGrid) để **gửi báo cáo hàng tuần** về bình luận mới.
🔸 **Kết hợp với Slack/Telegram**:
   - Thêm **node `slack`** hoặc `telegram` để **thông báo khi có bình luận mới**.
🔸 **Tự động tạo báo cáo Excel**:
   - Thêm **node `googleDrive`** để **export dữ liệu thành file Excel** tự động.
🔸 **Dùng AI phân tích cảm xúc**:
   - Kết nối với **node `LLM` (n8n-nodes-base.llm)** để **phân tích cảm xúc** của bình luận (ví dụ: tích cực, tiêu cực).
:::

---

### 📌 **Kết luận**
Với workflow này, các sếp **không cần mất thời gian copy-paste**, **không lo bị chặn IP**, và **có thể tự động scrape tất cả bình luận LinkedIn** để phân tích thị trường, nghiên cứu đối thủ, hoặc tối ưu nội dung.

**🚀 Hãy áp dụng ngay và tự động hóa công việc của mình!**
Nếu cần **tùy chỉnh thêm** hoặc **cài đặt trên VPS**, các sếp có thể liên hệ với **Allan Vaccarizi** (tác giả workflow) qua:
- [LinkedIn](https://www.linkedin.com/in/allanvaccarizi/)
- [Growth-AI.fr](https://www.growth-ai.fr/)

**Chúc các sếp thành công!** 💪