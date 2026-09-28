---
title: "📰 **Tự Động Hóa Tóm Tắt Tin Tức Hàng Ngày từ RSS sang WhatsApp với OpenAI (N8N)**"
description: "Workflow tự động hóa thu thập tin tức từ các nguồn RSS, tóm tắt nội dung bằng AI (OpenAI), và gửi tóm tắt hàng ngày đến WhatsApp - tiết kiệm thời gian lên đến 5 tiếng/tuần cho các sếp bận rộn."
slug: "tu-dong-hoa-tom-tat-rss-sang-whatsapp-voi-openai"
tags: [n8n, automation, no-code, ai, openai, rss, whatsapp, workflow]
keywords: [n8n workflow rss, tự động hóa tin tức, tóm tắt tin tức bằng ai, gửi tin tức whatsapp, workflow n8n ai]
---

# 🚀 **Tự Động Hóa Tóm Tắt Tin Tức Hàng Ngày từ RSS sang WhatsApp với OpenAI**

### **Giải pháp cho các sếp bị "ngập" tin tức hàng ngày**
Hàng ngày, các sếp phải mất **từ 30 phút đến 1 tiếng** để đọc và tóm tắt tin tức từ các nguồn RSS (như TechCrunch, Reuters, VnExpress) để cập nhật tình hình thị trường, công nghệ hay chính trị. **Workflow này tự động hóa toàn bộ quy trình** bằng cách:
✅ **Thu thập** tin tức từ **nhiều nguồn RSS** (không giới hạn).
✅ **Tóm tắt** nội dung bằng **AI (OpenAI)** với hệ thống prompt chuyên nghiệp.
✅ **Gửi tóm tắt** hàng ngày đến **WhatsApp** (hoặc Email, Google Drive...) **một cách cá nhân hóa**.
✅ **Hoạt động 24/7** mà không cần can thiệp thủ công.

---
### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần đọc từng bài tin, chỉ cần mở tin tóm tắt hàng ngày.
- **Tính chính xác cao**: AI tóm tắt dựa trên **prompt chuyên nghiệp**, tránh bỏ sót tin tức quan trọng.
- **Cá nhân hóa**: Thêm/loại bỏ nguồn RSS theo sở thích cá nhân.
- **Hoạt động liên tục**: Workflow chạy tự động hàng ngày, không phụ thuộc vào giờ làm việc.
- **Dễ dàng mở rộng**: Có thể thay đổi kênh gửi (Email, Telegram, Slack) mà không cần sửa code.
:::

---
### 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản OpenAI**:
   - API Key từ [OpenAI](https://platform.openai.com/account/api-keys) (đăng ký miễn phí).
   - **Gói tài khoản**: Đảm bảo có đủ credit để chạy AI (tóm tắt 10 bài tin/tuần ≈ **$0.5 - $1.0 USD**).

2. **API WhatsApp Business**:
   - **Tài khoản WhatsApp Business API** (cần đăng ký với nhà cung cấp như [Twilio](https://www.twilio.com/), [MessageBird](https://www.messagebird.com/), hoặc [360dialog](https://360dialog.vn/)).
   - **Credentials**:
     - `httpHeaderAuth`: Tham số `Authorization` (dạng `Bearer <API_KEY>`).
     - `Phone Number`: Số điện thoại WhatsApp Business (dạng quốc tế, ví dụ: `+841234567890`).

3. **Nguồn RSS**:
   - Các liên kết RSS của bài tin muốn theo dõi (ví dụ: [RSS TechCrunch](https://techcrunch.com/feed/), [RSS VnExpress](https://vnexpress.net/rss)).

4. **n8n Self-hosted** (khuyến nghị):
   - Workflow này **không chạy được** trên n8n Cloud do giới hạn tài nguyên của OpenAI.
   - 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%).
   - 👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172).
:::

---
## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. **Tải workflow** từ [n8n.io/workflows/4709](https://n8n.io/workflows/4709) (chọn "Download JSON").
2. **Mở n8n Editor** (trên VPS hoặc n8n Cloud).
3. **Nhấp vào "Import"** → Chọn file JSON vừa tải → **Nhấn "Import"**.

#### **Phương pháp 2: Copy/Paste JSON**
1. **Mở n8n Editor** → Nhấp vào **"Create"** → Chọn **"Import Workflow"** → **"Paste JSON"**.
2. **Dán JSON** từ [n8n.io/workflows/4709](https://n8n.io/workflows/4709) (chọn "Copy JSON").
3. **Nhấn "Import"**.

---
### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**

#### **A. Cấu hình OpenAI (Node "OpenAI")**
1. **Tạo credentials OpenAI**:
   - Trong n8n Editor → **"Credentials"** → **"Add"** → Chọn **"OpenAI API"** → Điền:
     - **API Key**: Copy từ OpenAI Dashboard.
     - **Model**: Giữ mặc định (`gpt-3.5-turbo`).
     - **System Message**: (Không cần thay đổi, nhưng có thể tùy chỉnh prompt):
       ```
       I've received 10 news articles via RSS. Please analyze them and provide a concise summary of the top 3 to 5 main highlights. My goal is to get a quick overview of what's most relevant in these articles.
       ```

2. **Kết nối credentials**:
   - Trong node **"OpenAI"**, chọn **"openAiApi"** trong trường **"Credentials"**.

#### **B. Cấu hình RSS Feeds (Nodes "My RSS 01", "My RSS 02", ...)**
1. **Thêm/loại bỏ nguồn RSS**:
   - Mỗi node **"rssFeedRead"** tương ứng với một nguồn RSS.
   - **Nhấp chuột phải** vào node → **"Duplicate"** để thêm nguồn mới.
   - **Cấu hình**:
     - **URL**: Nhập liên kết RSS (ví dụ: `https://techcrunch.com/feed/`).
     - **Max Items**: Giữ mặc định (`10`) để lấy 10 bài tin mới nhất.

#### **C. Cấu hình WhatsApp (Node "Send resum to Whatsapp")**
1. **Thiết lập HTTP Request**:
   - **Method**: `POST`.
   - **URL**: Tham khảo từ nhà cung cấp WhatsApp API (ví dụ:
     - **Twilio**: `https://api.twilio.com/2010-04-01/Accounts/{ACCOUNT_SID}/Messages.json`
     - **MessageBird**: `https://rest.messagebird.com/v2/messages`
   - **Headers**:
     - `Authorization`: `Bearer <YOUR_API_KEY>`.
     - `Content-Type`: `application/json`.
   - **Body (JSON)**:
     ```json
     {
       "to": "+841234567890",
       "from": "+1234567890", // Số WhatsApp Business của bạn
       "body": "{{ $json.summary }}"
     }
     ```
     - Thay `+841234567890` bằng số điện thoại người nhận (dạng quốc tế).
     - Thay `+1234567890` bằng số WhatsApp Business của bạn.

2. **Credentials**:
   - Chọn **"httpHeaderAuth"** trong trường **"Credentials"**.
   - Điền `Authorization` như hướng dẫn trên.

#### **D. Cấu hình Schedule Trigger (Node "Schedule Trigger")**
1. **Thiết lập lịch chạy**:
   - **Cron Expression**: Giữ mặc định (`0 0 * * *`) để chạy **lúc 00:00 hàng ngày** (giờ UTC).
   - **Nếu muốn chạy theo giờ Việt Nam**:
     - Sử dụng công cụ [crontab.guru](https://crontab.guru/) để chuyển đổi giờ (ví dụ: `0 17 * * *` để chạy lúc 17:00 GMT+7).

---
### **3. Kích hoạt ⚡️**
1. **Test Run (kiểm tra trước khi chạy thực tế)**:
   - Nhấp chuột phải vào node **"Schedule Trigger"** → **"Run Workflow"**.
   - Kiểm tra:
     - Có tin tức được thu thập từ RSS không?
     - AI có tóm tắt đúng không?
     - Tin tóm tắt có được gửi đến WhatsApp không?

2. **Bật Active Workflow**:
   - Nhấp vào nút **"Active"** ở góc trên bên phải → **"Active"**.

---
## ✍️ **Mẹo & gợi ý nâng cao**

### **1. Thêm/Loại bỏ nguồn RSS**
- **Thêm nguồn mới**:
  - Nhấp chuột phải vào node **"My RSS 01"** → **"Duplicate"** → Cập nhật URL RSS mới.
- **Loại bỏ nguồn**:
  - Nhấp chuột phải vào node → **"Delete"**.

### **2. Tùy chỉnh Prompt cho AI**
- Mở node **"OpenAI"** → Thay đổi **System Message** để AI tóm tắt theo phong cách riêng:
  ```plaintext
  You are a professional news summarizer. Summarize these articles into 3 key points:
  1. Main headline
  2. Key statistics or data
  3. Implications for [industry/sector, e.g., tech, finance, politics]
  ```

### **3. Gửi tóm tắt đến nhiều kênh**
- **Thay đổi node "Send resum to Whatsapp"** thành:
  - **Email**: Sử dụng node **`n8n-nodes-base.email`**.
  - **Google Drive**: Sử dụng node **`n8n-nodes-base.googleDrive`**.
  - **Telegram**: Sử dụng node **`n8n-nodes-base.telegram`**.

### **4. Lưu log hoạt động**
- Thêm node **"Sticky Note"** (nếu có) để ghi lại kết quả:
  ```json
  {
    "json": {
      "timestamp": "{{ $node["Schedule Trigger"].json.timestamp }}",
      "articles_analyzed": "{{ $node["Aggregate"].json.data.length }}",
      "summary": "{{ $json.summary }}"
    }
  }
  ```

### **5. Báo cáo định kỳ**
- Sử dụng node **"Schedule Trigger"** để chạy **hàng tuần** và gửi báo cáo tổng hợp:
  ```plaintext
  Cron: "0 0 * * 0" (chạy thứ Bảy 00:00)
  ```

---
## 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp để tập trung vào công việc chiến lược hơn. **Chỉ cần 5 phút để cấu hình**, sau đó nó tự động hoạt động hàng ngày. **Thử ngay** và cảm nhận sự khác biệt!

### **Bước tiếp theo**
1. **Import workflow** và cấu hình theo hướng dẫn.
2. **Test Run** trước khi bật Active.
3. **Tùy chỉnh** nguồn RSS và kênh gửi theo nhu cầu.

👉 **Nếu gặp vấn đề**, hãy để lại comment dưới đây hoặc liên hệ với [n8n Community](https://community.n8n.io/).

---
**#TựĐộngHóa #N8N #AI #WhatsAppAutomation #TinTứcHàngNgày**