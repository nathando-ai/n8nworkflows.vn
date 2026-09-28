---
title: "🚀 Tự Động Theo Dõi Danh Tiêu Brand Trên Mạng Với GPT-4o, Google Sheets & Email – Không Cần Code!"
description: "Workflow tự động hóa theo dõi nhắc đến thương hiệu trên mạng xã hội, bài viết và diễn đàn bằng GPT-4o, lưu kết quả vào Google Sheets và gửi báo cáo email hàng ngày – tiết kiệm thời gian SEO/Marketing 100%."
slug: "tieu-doi-brand-voi-gpt-4o-google-sheets-email"
tags: [n8n, automation, seo, marketing, ai, google-sheets, email-automation]
keywords: [tự động hóa theo dõi brand, n8n workflow seo, chatgpt theo dõi nhắc đến thương hiệu, tự động hóa marketing, báo cáo nhắc đến thương hiệu]
---

# 🚀 **Tự Động Theo Dõi Danh Tiêu Brand Trên Mạng Với GPT-4o, Google Sheets & Email**

### **Giải pháp cho các sếp SEO/Marketing: Dừng việc tra cứu thủ công nhắc đến thương hiệu trên mạng!**
Hàng ngày, các sếp phải mất nhiều giờ để tra cứu trên Google, Facebook, Twitter hay diễn đàn để biết thương hiệu mình được nhắc đến như thế nào. **Workflow này tự động hóa toàn bộ quá trình** bằng cách:
- **Dùng GPT-4o** để quét và phân tích nhắc đến thương hiệu trên nhiều nguồn (Google, mạng xã hội, diễn đàn).
- **Lưu dữ liệu** vào Google Sheets với định dạng chuyên nghiệp.
- **Gửi báo cáo email tự động** hàng ngày cho team, không cần can thiệp thủ công.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ/tuần** tra cứu thủ công nhắc đến thương hiệu.
- **Dữ liệu chính xác và toàn diện** từ nhiều nguồn (Google, Twitter, Reddit, diễn đàn).
- **Báo cáo tự động** gửi hàng ngày với định dạng email chuyên nghiệp.
- **Dễ dàng theo dõi xu hướng** và phản hồi kịp thời với khách hàng.
- **Không cần kỹ năng code** – chỉ cần cấu hình API và Google Sheets.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản API OpenAI** (để sử dụng GPT-4o):
   - [Tạo API Key OpenAI](https://platform.openai.com/account/api-keys) (Model: `chatgpt-4o-latest`).
2. **Tài khoản Google Cloud** (để kích hoạt API Google Sheets):
   - [Tạo dự án Google Cloud](https://console.cloud.google.com/) và kích hoạt:
     - **Google Sheets API**
     - **Google Drive API**
   - [Cấu hình OAuth 2.0](https://developers.google.com/sheets/api/quickstart/python) để lấy `googleSheetsOAuth2Api`.
3. **Tài khoản email SMTP** (để gửi báo cáo):
   - Nếu dùng Gmail, không cần cấu hình thêm (sử dụng `smtp.gmail.com`).
   - Nếu dùng nhà cung cấp khác (Yahoo, Outlook), lấy thông tin:
     - **Host** (ví dụ: `smtp.mail.yahoo.com`)
     - **Port** (587 hoặc 465)
     - **Tên đăng nhập & mật khẩu** (hoặc mật khẩu ứng dụng nếu 2FA bật).
4. **Google Sheet** để lưu dữ liệu:
   - Tạo một sheet mới và chia sẻ cho `n8n@n8n-io.iam.gserviceaccount.com` (quyền chỉnh sửa).

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Cách 1: Import từ file JSON**
  1. Tải workflow từ [n8n.io/workflows/4443](https://n8n.io/workflows/4443) (chọn **Export as JSON**).
  2. Trên n8n Editor, nhấn **Import** và dán JSON vào.
- **Cách 2: Copy/Paste JSON**
  1. Mở n8n Editor, nhấn **Create new workflow**.
  2. Chọn **Import from JSON** và dán mã JSON từ [n8n.io/workflows/4443](https://n8n.io/workflows/4443).

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow có **7 node chính**, các sếp cần cấu hình như sau:

##### **🔹 Node 1: Daily Trigger (scheduleTrigger)**
- **Thiết lập thời gian chạy**:
  - Mặc định là **1 lần/ngày** (ví dụ: 8h sáng).
  - Để đổi, nhấn **Edit** và chọn **Custom schedule** (ví dụ: `0 8 * * *` = 8h sáng hàng ngày).

##### **🔹 Node 2: Setup Queries (code)**
- **Cấu hình brand name và queries**:
  - Mở node này và thay thế phần `const brandName = "Tên Thương Hiệu Của Bạn";`.
  - Thêm các **query** muốn theo dõi (ví dụ: `"site:facebook.com " + brandName`, `"site:reddit.com " + brandName`).
  - **Ví dụ**:
    ```javascript
    const brandName = "VietNamTech";
    const queries = [
      `site:facebook.com "${brandName}"`,
      `site:twitter.com "${brandName}"`,
      `site:reddit.com "${brandName}"`,
      `intitle:"${brandName}" site:google.com`
    ];
    ```

##### **🔹 Node 3: Query ChatGPT (HTTP)**
- **Cấu hình API OpenAI**:
  - Trong **Credentials**, chọn `openAiApi` (đã cấu hình trước khi import).
  - **Headers**:
    - `Content-Type: application/json`
    - `Authorization: Bearer {API_KEY_CỦA_BẠN}`
  - **Body**:
    - Thay thế `model: "gpt-4o-latest"` (nếu muốn dùng model khác).
    - **Prompt mẫu**:
      ```json
      {
        "messages": [
          {
            "role": "system",
            "content": "You are a brand monitoring assistant. Analyze the following search results for mentions of the brand '{brandName}'. Return structured data including:\n1. Source (website/domain)\n2. Date found\n3. Sentiment (positive/negative/neutral)\n4. Exact mention text\n5. URL (if available)"
          },
          {
            "role": "user",
            "content": "Search queries: {queries}"
          }
        ],
        "temperature": 0.7,
        "max_tokens": 1000
      }
      ```

##### **🔹 Node 4: Process Response (code)**
- **Không cần chỉnh sửa** (node này tự động phân tích kết quả từ GPT-4o).

##### **🔹 Node 5: Save to Google Sheets (googleSheets)**
- **Chọn sheet và tab**:
  - Trong **Credentials**, chọn `googleSheetsOAuth2Api` (đã cấu hình trước).
  - **Spreadsheet ID**: Copy từ URL của sheet (ví dụ: `https://docs.google.com/spreadsheets/d/{SPREADSHEET_ID}/edit`).
  - **Sheet Name**: Tên tab muốn lưu (ví dụ: `Brand_Mentions`).
  - **Operation**: Đã mặc định là `append` (thêm dữ liệu mới vào cuối).

##### **🔹 Node 6: Generate Email Report (code)**
- **Không cần chỉnh sửa** (node này tự động tạo email từ dữ liệu trong Sheets).

##### **🔹 Node 7: Send Email (emailSend)**
- **Cấu hình SMTP**:
  - Trong **Credentials**, chọn `smtp` (đã cấu hình trước).
  - **Host**: `smtp.gmail.com` (nếu dùng Gmail) hoặc `smtp.mail.yahoo.com` (Yahoo).
  - **Port**: `587` (hoặc `465` nếu SSL).
  - **From Email**: Địa chỉ email gửi (ví dụ: `team@viettnamtech.com`).
  - **To Email**: Địa chỉ email nhận (ví dụ: `seo@viettnamtech.com`).
  - **Subject**: Mặc định là `Daily Brand Mentions Report - {date}`.
  - **Body**: Mặc định là HTML từ node trước.

---

#### **3. Kích hoạt ⚡️**
1. **Test run dữ liệu mẫu**:
   - Nhấn **Run Workflow** và kiểm tra:
     - GPT-4o trả về kết quả phân tích như mong đợi?
     - Dữ liệu được lưu vào Google Sheets đúng không?
     - Email được gửi thành công không?
2. **Bật Active workflow**:
   - Sau khi test thành công, nhấn **Active** để workflow chạy tự động hàng ngày.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Kết hợp với Slack/Telegram**:
   - Thêm node **Slack Webhook** hoặc **Telegram Bot** sau node `Send Email` để thông báo kết quả ngay khi có.
2. **Lưu log hoạt động**:
   - Thêm node **Sticky Note** (node `stickyNote`) để ghi lại lỗi hoặc thông tin debug.
3. **Báo cáo định kỳ**:
   - Sử dụng node **Schedule Trigger** để gửi báo cáo tuần/month thay vì hàng ngày.
4. **Tối ưu query**:
   - Nếu GPT-4o trả về quá nhiều kết quả, hãy **giảm số lượng queries** hoặc **chỉnh `max_tokens`** để tiết kiệm chi phí API.
5. **Dùng Google Alerts kết hợp**:
   - Nếu muốn theo dõi thêm, có thể **kết hợp với Google Alerts** và lấy dữ liệu từ đó.

---

### 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp SEO/Marketing muốn theo dõi nhắc đến thương hiệu **một cách tự động, chính xác và tiết kiệm thời gian**. Bằng cách cấu hình đơn giản trên n8n, các sếp có thể:
✅ **Tiết kiệm 10+ giờ/tuần** tra cứu thủ công.
✅ **Nhận báo cáo hàng ngày** với dữ liệu phân tích từ GPT-4o.
✅ **Cập nhật chiến lược marketing** dựa trên phản hồi thực tế của khách hàng.

**Hành động ngay!**
1. **Cài đặt n8n trên VPS** (để workflow chạy 24/7).
2. **Import workflow** và cấu hình API/Google Sheets.
3. **Bật Active** và bắt đầu theo dõi thương hiệu của mình!

👉 [Tải workflow từ n8n.io](https://n8n.io/workflows/4443) và **cấu hình ngay hôm nay**! 🚀