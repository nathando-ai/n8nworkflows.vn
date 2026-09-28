---
title: "🤖 **Tự Động Học Lấy Thông Tin Mô Tả Vị Trí & Lương Thực Tế bằng Bright Data + OpenAI GPT-4o Mini (N8n HR)**"
description: "Workflow tự động hóa lấy thông tin mô tả công việc và mức lương từ trang web tuyển dụng, kết hợp Bright Data MCP Client và OpenAI GPT-4o Mini để tiết kiệm thời gian cho bộ phận HR lên tới 90%. Kết quả được lưu vào Google Sheets và gửi thông báo webhook thời gian thực."
slug: "tieu-dong-hoa-lay-thong-tin-mo-ta-vi-tri-luong"
tags: [n8n, automation, hr, ai, bright-data, openai, gpt-4o-mini, google-sheets]
keywords: [n8n workflow hr, tự động hóa tuyển dụng, lấy thông tin lương mô tả công việc, bright data mcp client, openai gpt-4o mini, tự động hóa no-code]
---

# 🚀 **Tự Động Học Lấy Thông Tin Mô Tả Vị Trí & Lương Thực Tế (Bright Data + OpenAI GPT-4o Mini)**

### **Nỗi Đau Của Các Sếp HR**
Bộ phận tuyển dụng thường phải **quét thủ công** hàng trăm trang tuyển dụng để lấy thông tin chi tiết về **mô tả công việc** và **mức lương**, tiêu tốn thời gian và dễ mắc sai sót. Với workflow này, các sếp sẽ **tự động hóa toàn bộ quy trình** bằng cách:
✅ **Lấy dữ liệu mô tả công việc** từ trang web tuyển dụng (thông qua Bright Data MCP Client).
✅ **Trích xuất mức lương** bằng AI (OpenAI GPT-4o Mini) với độ chính xác cao.
✅ **Lưu kết quả vào Google Sheets** để theo dõi và phân tích.
✅ **Gửi thông báo webhook** khi có dữ liệu mới (để tích hợp với Slack/Telegram).

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7**, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động hóa lấy dữ liệu thay vì làm thủ công (giảm 90% công việc).
- **Độ chính xác cao**: AI OpenAI GPT-4o Mini trích xuất thông tin mô tả và lương chính xác hơn con người.
- **Lưu trữ tự động**: Dữ liệu được ghi vào **Google Sheets** để theo dõi và phân tích.
- **Thông báo thời gian thực**: Webhook gửi kết quả ngay khi có dữ liệu mới.
- **Không cần code**: Sử dụng **n8n + Bright Data + OpenAI** để tự động hóa toàn bộ quy trình.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi chạy workflow, các sếp cần chuẩn bị:
✔ **Tài khoản Bright Data MCP Client** (để lấy dữ liệu từ trang web tuyển dụng).
✔ **API Key OpenAI** (để sử dụng GPT-4o Mini trích xuất thông tin).
✔ **Google Sheets OAuth 2.0 API** (để lưu kết quả).
✔ **Webhook URL** (để nhận thông báo khi có dữ liệu mới).

---
:::note[Lưu ý quan trọng]
Workflow **chỉ hoạt động trên n8n self-hosted** vì sử dụng **Bright Data MCP Client (community node)**.
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/4829](https://n8n.io/workflows/4829) hoặc copy/paste JSON vào **n8n Editor**.
- **Cách import**:
  1. Mở **n8n Editor** → Nhấn **"Import"** → Chọn file JSON.
  2. Hoặc **copy toàn bộ JSON** và dán vào **"Import from JSON"** trong menu.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow gồm **15 node**, các sếp cần **cấu hình chính xác** các node sau:

##### **A. Cấu Hình Bright Data MCP Client**
- **Node 1**: `Bright Data MCP Client List Tools` → Điền **API Key** vào `mcpClientApi`.
- **Node 3**: `MCP Client for Job Data Extract with Markdown` → Chọn **tool phù hợp** (ví dụ: `web_scraper`).
- **Node 4**: `MCP Client for Salary Data Extraction` → Chọn **tool khác** (ví dụ: `web_extractor`).

##### **B. Cấu Hình OpenAI GPT-4o Mini**
- **Node 11**: `OpenAI Chat Model for Salary Info Extract` → Điền **API Key OpenAI** vào `openAiApi`.
- **Node 12**: `OpenAI Chat Model for Job Desc Extract` → Cùng cấu hình như node 11.
- **Prompt mẫu** (có thể tùy chỉnh):
  ```json
  "prompt": "Extract the salary range from this job description: {jobDescription}"
  ```

##### **C. Cấu Hình Google Sheets**
- **Node 14**: `Update Google Sheets` → Chọn **Google Sheets OAuth 2.0 API** (`googleSheetsOAuth2Api`).
- **Sheet Name**: Đặt tên sheet (ví dụ: `Job_Data_Extraction`).
- **Columns**: Cần định nghĩa cột (ví dụ: `Job Title`, `Salary`, `Description`).

##### **D. Cấu Hình Webhook**
- **Node 10**: `Webhook Notification for Job Info` → Điền **URL webhook** của Slack/Telegram.

##### **E. Cấu Hình Input Fields (Quá Trình)**
- **Node 2**: `Set input fields` → Điền **URL trang tuyển dụng** và **thông tin cần trích xuất** (ví dụ: `job_title`, `salary`).

#### **3. Kích Hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu (ví dụ: URL của một trang tuyển dụng).
2. **Bật Active workflow** sau khi kiểm tra kết quả.

---
### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tích hợp với Slack/Telegram**:
   - Sử dụng **node `httpRequest`** để gửi thông báo khi có dữ liệu mới.
   - Ví dụ: Gửi tin nhắn Slack khi có **mô tả công việc mới** hoặc **lương được cập nhật**.

2. **Lưu Log Dữ Liệu**:
   - Sử dụng **node `readWriteFile`** để lưu dữ liệu vào **file JSON** hoặc **CSV** trên VPS.

3. **Tự Động Lấy Dữ liệu Định Kỳ**:
   - Sử dụng **node `set`** kết hợp với **cron job** để chạy workflow hàng ngày.

4. **Tùy Chỉnh Prompt AI**:
   - Nếu AI không trích xuất chính xác, **cập nhật prompt** trong node `lmChatOpenAi` để rõ ràng hơn.

---
### 📌 **Kết Luận**
Workflow này **giúp các sếp HR tự động hóa lấy thông tin mô tả công việc và lương** một cách **chính xác, nhanh chóng và không cần code**. Bằng cách kết hợp **Bright Data MCP Client** (lấy dữ liệu từ web) và **OpenAI GPT-4o Mini** (trích xuất thông tin), các sếp sẽ **tiết kiệm thời gian** và **giảm sai sót** trong quy trình tuyển dụng.

**🚀 Hãy áp dụng ngay và tự động hóa bộ phận HR của mình!** 🚀

---
**📩 Liên hệ tác giả (Ranjan Dailata)**:
- Email: [ranjancse@gmail.com](mailto:ranjancse@gmail.com)
- GitHub: [@ranjancse](https://github.com/ranjancse) (nếu có)