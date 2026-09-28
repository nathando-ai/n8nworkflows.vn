---
title: "🚀 Tự Động Hóa & Xếp Loại Yêu Cầu IT với Jotform, Gemini AI & Google Workspace - Giảm Thời Gian Phản Hồi IT Lên Gấp 5 Lần"
description: "Workflow tự động hóa nhận, phân loại và xử lý yêu cầu IT từ Jotform sang Google Sheets, gửi thông báo Telegram và phản hồi tự động qua email - giảm thiểu công việc thủ công và tăng cường hiệu quả đội ngũ IT. Sử dụng AI Gemini để tóm tắt và phân loại ưu tiên (P0, P1, P2) tự động."
slug: "tu-dong-hoa-xep-loai-yeu-cau-it-voi-jotform-gemini-google-workspace"
tags: [n8n, automation, ticket-management, ai-summarization, google-workspace, jotform, gemini-ai]
keywords: [tự động hóa yêu cầu IT, phân loại ticket IT, gemini AI n8n, google sheets tự động hóa, jotform n8n, giảm thời gian phản hồi IT]
---

# 🚀 **Tự Động Hóa & Xếp Loại Yêu Cầu IT với Jotform, Gemini AI & Google Workspace**

## **🔥 Nỗi Đau Của Các Sếp IT Hiện Nay**
Hàng ngày, đội ngũ IT phải chịu gánh nặng **nhận, phân loại và xử lý hàng chục yêu cầu IT thủ công** từ các form, email hoặc hệ thống hỗn hợp. Kết quả?
- **Thời gian phản hồi chậm**: Yêu cầu phải chờ xếp loại và chuyển tiếp giữa các bộ phận.
- **Rủi ro sai sót**: Phân loại ưu tiên không chính xác dẫn đến việc bỏ qua yêu cầu cấp bách (P0).
- **Dữ liệu phân tán**: Thông tin yêu cầu rải rác trên email, Google Sheets hoặc Slack, khó theo dõi.
- **Tốn thời gian**: Cần tóm tắt lại nội dung dài để báo cáo hoặc gửi cho các kỹ sư.

**Workflow này giải quyết tất cả!** Sử dụng **Jotform để nhận yêu cầu**, **Gemini AI để tóm tắt và phân loại ưu tiên tự động**, và **Google Workspace để lưu trữ, gửi thông báo và phản hồi tự động** – tất cả **không cần viết một dòng code nào!**

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động **24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS riêng.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới **39%**)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (Đảm bảo tốc độ cao, phù hợp cho AI)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Giảm thời gian phản hồi IT từ 24h → dưới 1h**: Yêu cầu được phân loại và chuyển tiếp tự động.
✅ **Phân loại ưu tiên chính xác (P0, P1, P2)**: Gemini AI phân tích nội dung và xếp loại dựa trên mức độ cấp thiết.
✅ **Dữ liệu tập trung**: Tất cả yêu cầu được lưu vào **Google Sheets** theo tab ưu tiên, dễ theo dõi và báo cáo.
✅ **Phản hồi tự động**: Người gửi nhận email xác nhận ngay lập tức, giảm thiểu việc nhắc nhở thủ công.
✅ **Gửi thông báo Telegram**: Các yêu cầu cấp bách (P0) được gửi ngay đến nhóm Telegram của IT Team.
✅ **Tóm tắt AI tự động**: Gemini AI rút gọn nội dung yêu cầu dài thành **tóm tắt ngắn gọn**, giúp kỹ sư hiểu nhanh vấn đề.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
| **Tài Khoản/Dịch Vụ**       | **Thông Tin Cần Thiết**                                                                 | **Lưu Ý**                          |
|-----------------------------|---------------------------------------------------------------------------------------|-------------------------------------|
| **Jotform**                 | API Key (tạo từ [Jotform Developer Console](https://developer.jotform.com/))           | Chọn form IT Service Request.      |
| **Google Workspace**         | - OAuth 2.0 API Key (Google Sheets) <br> - Gmail OAuth 2.0 (để gửi email phản hồi)     | Cần quyền **Editor** trên Sheets.  |
| **Google Gemini API**        | API Key từ [Google AI Studio](https://aistudio.google.com/)                          | Chọn model `gemini-pro`.           |
| **Telegram Bot**            | Token Bot từ [@BotFather](https://t.me/BotFather) + Chat ID của nhóm IT Team          | Cần quyền gửi tin nhắn.          |
| **Google Sheets**            | 3 Tab riêng biệt: **P0 (High)**, **P1 (Medium)**, **P2 (Low)** (tạo trước khi import) | Cấu trúc cột: `Full Name`, `Email`, `Problem`, `Summary`, `Priority`. |

---
:::note[CHÚ Ý QUAN TRỌNG]
- **Không cần cài đặt thêm plugin**: Workflow sử dụng **n8n-nodes-langchain** (sẵn có trong n8n Community).
- **Google Sheets phải có cấu trúc cố định**: Các tab `P0`, `P1`, `P2` phải được tạo trước để workflow append dữ liệu.
- **Jotform phải có các trường bắt buộc**: `Full Name`, `Department`, `Email`, `Problem Category`, `Comments`.
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
**Cách 1: Từ File JSON**
1. Tải workflow từ [n8n.io/workflows/10127](https://n8n.io/workflows/10127) (chọn **Export as JSON**).
2. Trên n8n Editor, nhấn **Import** → Chọn file JSON vừa tải.
3. Chọn **Create new workflow** và nhấn **Import**.

**Cách 2: Copy/Paste JSON**
1. Mở n8n Editor → **Create new workflow**.
2. Nhấn **Import** → Chọn **Paste JSON**.
3. Dán toàn bộ mã JSON từ [n8n.io/workflows/10127](https://n8n.io/workflows/10127) (chọn **Export as JSON**).
4. Nhấn **Import**.

---
#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Sau khi import, các sếp cần **cấu hình chi tiết** các node quan trọng:

##### **A. JotForm Trigger**
- **Credentials**: Chọn `jotFormApi` (đã tạo trước).
- **Form ID**: Nhập ID của form IT Service Request (thường là chuỗi số trong URL Jotform).
- **Fields to Capture**:
  - `fullName` → `Full Name`
  - `email` → `Email`
  - `department` → `Department`
  - `problemCategory` → `Problem Category`
  - `comments` → `Comments`

##### **B. Google Gemini Chat Model**
- **Credentials**: Chọn `googlePalmApi` (API Key từ Google AI Studio).
- **Model**: Chọn `gemini-pro`.
- **Prompt Tóm Tắt** (cần chỉnh sửa để phù hợp):
  ```plaintext
  Tóm tắt vấn đề IT của người dùng dưới dạng ngắn gọn (dưới 100 từ). Nếu có từ khóa cấp bách như "không hoạt động", "hỏng", "không kết nối", hãy nhấn mạnh mức độ ưu tiên.
  ```
- **Prompt Phân Loại** (cần chỉnh sửa):
  ```plaintext
  Phân loại yêu cầu IT vào một trong 3 mức ưu tiên:
  - P0 (High): Vấn đề ảnh hưởng đến toàn bộ hệ thống hoặc yêu cầu xử lý ngay lập tức.
  - P1 (Medium): Vấn đề ảnh hưởng đến một người dùng hoặc bộ phận cụ thể.
  - P2 (Low): Yêu cầu bảo trì hoặc cập nhật không cấp bách.
  ```

##### **C. Priority Classifier (TextClassifier)**
- **Model**: Chọn `gemini-pro`.
- **Training Data**: Sử dụng **các ví dụ phân loại** để AI học:
  ```json
  [
    { "text": "Máy tính không kết nối mạng", "label": "P0" },
    { "text": "Chuột không hoạt động", "label": "P1" },
    { "text": "Yêu cầu đổi mật khẩu", "label": "P2" }
  ]
  ```
- **Output**: Node này sẽ trả về `priority` (P0, P1, P2) để chuyển tiếp đến Sheets đúng tab.

##### **D. Store to Sheets (P0, P1, P2)**
- **Credentials**: Chọn `googleSheetsOAuth2Api`.
- **Spreadsheet ID**: Nhập ID của Google Sheets (thường là chuỗi số trong URL).
- **Sheet Name**: Chọn tab tương ứng (`P0`, `P1`, `P2`).
- **Headers**: Đảm bảo các cột trong Sheets trùng khớp với `Full Name`, `Email`, `Problem`, `Summary`, `Priority`.

##### **E. Reply User (Gmail)**
- **Credentials**: Chọn `gmailOAuth2`.
- **Template Email**:
  ```plaintext
  Chào {{ $node["Set Fields"].json["fullName"] }},

  Cảm ơn bạn đã gửi yêu cầu IT. Chúng tôi đã nhận và đang xử lý với ưu tiên {{ $node["Priority Classifier"].json["priority"] }}.

  Tóm tắt vấn đề:
  {{ $node["Summarization Chain"].json["summary"] }}

  Trân trọng,
  Đội ngũ IT
  ```
- **CC/BCC**: Có thể thêm email của quản lý IT.

##### **F. Send to Group (Telegram)**
- **Credentials**: Chọn `telegramApi`.
- **Chat ID**: Nhập Chat ID của nhóm Telegram (có thể lấy từ [@userinfobot](https://t.me/userinfobot)).
- **Message Template**:
  ```plaintext
  🚨 **Yêu cầu IT cấp bách (P0)** 🚨
  Người gửi: {{ $node["Set Fields"].json["fullName"] }}
  Email: {{ $node["Set Fields"].json["email"] }}
  Vấn đề: {{ $node["Set Fields"].json["comments"] }}
  Tóm tắt: {{ $node["Summarization Chain"].json["summary"] }}
  ```

---
#### **3. Kích Hoạt ⚡️**
1. **Test Run** với một yêu cầu mẫu:
   - Điền thông tin vào form Jotform.
   - Kiểm tra:
     - Email phản hồi có được gửi không?
     - Dữ liệu có được lưu vào Sheets tab đúng không?
     - Telegram có nhận thông báo không?
2. **Active Workflow**: Sau khi kiểm tra thành công, nhấn **Active** để workflow chạy tự động.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Thêm Logs cho Dễ Theo Dõi**
   - Sử dụng node **StickyNote** để lưu lịch sử yêu cầu:
     ```json
     {
       "nodeName": "Log Request",
       "type": "stickyNote",
       "credentials": ["stickyNoteApi"],
       "content": "Yêu cầu {{ $node["Set Fields"].json["fullName"] }} (ID: {{ $node["JotForm Trigger"].json["id"] }}) đã được xử lý."
     }
     ```

2. **Gửi Báo Cáo Định Kỳ**
   - Tạo một workflow mới để **tổng hợp dữ liệu từ Sheets** và gửi báo cáo hàng tuần qua email:
     ```plaintext
     - Node: Google Sheets → Lấy dữ liệu từ tab P0, P1, P2.
     - Node: Gmail → Gửi báo cáo tổng hợp với biểu đồ (sử dụng Google Charts).
     ```

3. **Kết Nối với Slack**
   - Thay thế Telegram bằng **Slack Webhook** để thông báo trong kênh #it-support:
     ```json
     {
       "name": "Send to Slack",
       "type": "slack",
       "credentials": ["slackWebhook"],
       "webhookUrl": "https://hooks.slack.com/services/...",
       "message": "🚨 *Yêu cầu IT mới* 🚨\n*Người gửi*: {{ $node["Set Fields"].json["fullName"] }}\n*Vấn đề*: {{ $node["Set Fields"].json["comments"] }}\n*Ưu tiên*: {{ $node["Priority Classifier"].json["priority"] }}"
     }
     ```

4. **Tự Động Xóa Yêu Cầu Sau Xử Lý**
   - Sử dụng **node Set** để thêm trường `status` và node **Google Sheets** để cập nhật:
     ```json
     {
       "name": "Update Status",
       "type": "set",
       "operations": [
         {
           "propertyName": "status",
           "value": "Đang xử lý"
         }
       ]
     }
     ```

5. **Tối Ưu Hóa Prompt AI**
   - Nếu Gemini AI phân loại sai, **cập nhật lại training data** trong node `Priority Classifier` với các ví dụ mới.

---

### 📌 **Kết Luận: Hãy Áp Dụng Ngay!**
Workflow này **giải phóng đội ngũ IT khỏi công việc thủ công**, giúp **phân loại yêu cầu chính xác**, và **tăng tốc độ phản hồi** lên gấp 5 lần. Với **AI Gemini tự động tóm tắt và phân loại**, các sếp không cần lo lắng về việc bỏ lỡ yêu cầu cấp bách hay mất thời gian xử lý dữ liệu.

**Bước đầu tiên**: Import workflow và **cấu hình Jotform + Google Sheets** theo hướng dẫn trên. Sau đó, **test với một yêu cầu mẫu** và **bật Active** để workflow hoạt động 24/7.

👉 **Bắt đầu tự động hóa IT của bạn ngay hôm nay!** Nếu có vấn đề, hãy để lại comment bên dưới hoặc liên hệ với cộng đồng n8n tại [n8n.io/community](https://n8n.io/community).

---
**#TựĐộngHóaIT #GeminiAI #GoogleWorkspace #n8nNoCode #PhânLoạiTicket**