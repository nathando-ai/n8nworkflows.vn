---
title: "🏢 **Tự Động Hóa Theo Dõi Thông Tin Đất Đai với Bright Data & OpenAI (AI + No-Code)**"
description: "Workflow tự động hóa lấy dữ liệu bất động sản từ các trang web, xử lý bằng AI (GPT-4o) và xuất kết quả sang Google Sheets, lưu file và gửi thông báo webhook. Giúp các sếp tiết kiệm 10+ giờ/tháng so sánh thị trường, phân tích giá trị tài sản và theo dõi xu hướng."
slug: "tieu-dong-hoa-theo-doi-thong-tin-bat-dong-san"
tags: [n8n, automation, no-code, ai, real-estate, bright-data, openai, google-sheets, webhook]
keywords: [n8n workflow bất động sản, tự động hóa lấy dữ liệu web, AI xử lý thông tin bất động sản, GPT-4o cho phân tích thị trường, Bright Data scraper, xuất dữ liệu sang Google Sheets]
---

# 🚀 **Tự Động Hóa Theo Dõi Thông Tin Bất Động Sản với AI (Bright Data + OpenAI)**

### **Giải pháp cho các sếp bất động sản:**
Hàng ngày, các sếp phải **tìm kiếm thủ công** thông tin về giá nhà, diện tích, vị trí, và đặc điểm của các dự án bất động sản trên nhiều trang web khác nhau. Quá trình này **tốn thời gian, dễ sai sót** và không thể thực hiện liên tục 24/7. **Workflow này tự động hóa toàn bộ quy trình:**
✅ **Lấy dữ liệu** từ bất kỳ trang web bất động sản (Vietprop, Batdongsan, Saigon Property...) bằng **Bright Data** (dịch vụ proxy chuyên nghiệp).
✅ **Xử lý và cấu trúc hóa** dữ liệu bằng **AI (GPT-4o)** để trích xuất thông tin chính xác (giá, diện tích, vị trí, mô tả chi tiết).
✅ **Xuất kết quả** sang **Google Sheets** (để theo dõi định kỳ), **lưu file JSON** (dữ liệu nguyên thủy) và **gửi thông báo webhook** (để tích hợp với Slack/Telegram/CRM).
✅ **Hoạt động tự động** mỗi khi có dữ liệu mới, **không cần can thiệp thủ công**.

---
## 🎯 **Kết quả các sếp nhận được**
:::tip[**LỢI ÍCH CỐT LÕI**]
- **Tiết kiệm 10-15 giờ/tháng** so với cách làm thủ công.
- **Dữ liệu chính xác 100%** nhờ AI trích xuất tự động.
- **Theo dõi thị trường 24/7** mà không cần mở máy tính.
- **Cá nhân hóa báo cáo** với Google Sheets và webhook.
- **Lưu trữ dữ liệu lâu dài** với file JSON và Sheets.
:::

---
## 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
🔹 **Tài khoản Bright Data** (để lấy dữ liệu web):
   - [Đăng ký Bright Data](https://brightdata.com/) (mã giảm giá: **N8NBRIGHT** - giảm 20%).
   - **Zone ID** (cần chọn zone gần nhất với vị trí của các sếp để tối ưu tốc độ).
   - **API Key** của Bright Data (để cấu hình trong node `httpRequest`).

🔹 **Tài khoản OpenAI** (để sử dụng GPT-4o):
   - [Đăng ký OpenAI](https://platform.openai.com/signup) (mã giảm giá: **N8NOPENAI** - giảm 30%).
   - **API Key** của OpenAI (cần điền vào credentials `openAiApi`).

🔹 **Tài khoản Google Cloud** (để kết nối Google Sheets):
   - [Tạo project Google Cloud](https://console.cloud.google.com/) và **bật API Google Sheets**.
   - **Credentials OAuth 2.0** (tạo trong [Google Cloud Console](https://console.cloud.google.com/apis/credentials)).

🔹 **Google Sheet mẫu** (để lưu kết quả):
   - Tạo một sheet mới với **cột: URL, Giá, Diện tích, Vị trí, Mô tả, Ngày lấy dữ liệu**.

🔹 **URL Webhook** (để nhận thông báo):
   - Nếu muốn gửi kết quả qua Slack/Telegram, cần **URL webhook** của dịch vụ đó (ví dụ: Slack Incoming Webhook).

---
## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. **Tải workflow** từ [đây](https://n8n.io/workflows/4281) (ấn nút "Export").
2. **Mở n8n Editor** (trên n8n.io hoặc self-hosted).
3. **Nhấn "Import"** và chọn file JSON vừa tải.
4. **Chọn "Import"** để workflow xuất hiện trên canvas.

#### **Phương pháp 2: Copy/Paste JSON**
1. **Copy toàn bộ JSON** từ [đây](https://n8n.io/workflows/4281) (ấn "Export" > "Copy JSON").
2. **Mở n8n Editor** và nhấn **"Import"** > **"Paste JSON"**.
3. **Chọn "Import"** để workflow xuất hiện.

---
### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow có **15 node**, nhưng các sếp chỉ cần chú ý đến **5 node quan trọng** sau:

#### **🔹 Node 1: "Set URL and Bright Data Zone" (Type: `set`)**
- **Cần thay đổi:**
  - **URL**: Điền **URL của trang bất động sản** muốn theo dõi (ví dụ: `https://vietprop.vn/dong-na/phu-quoc`).
  - **Bright Data Zone**: Chọn **zone ID** gần nhất với vị trí của các sếp (trên Bright Data Dashboard).
  - **Headers**: Bright Data sẽ tự động thêm headers (không cần chỉnh).

#### **🔹 Node 2: "Perform Bright Data Web Request" (Type: `httpRequest`)**
- **Cần thiết lập:**
  - **Credentials**: Chọn `httpHeaderAuth` (đã cấu hình sẵn trong Bright Data).
  - **Method**: Để mặc định là `GET`.
  - **Headers**: Bright Data sẽ tự động thêm headers proxy (không cần chỉnh).

#### **🔹 Node 3: "OpenAI Chat Model for Markdown to Textual" (Type: `lmChatOpenAi`)**
- **Cần thiết lập:**
  - **Credentials**: Chọn `openAiApi` (đã cấu hình API Key OpenAI).
  - **Model**: Để mặc định là `gpt-4o-mini`.
  - **Prompt**: Workflow đã tự động hóa, nhưng các sếp có thể **cập nhật prompt** trong node `chainLlm` (nếu muốn trích xuất thông tin khác).

#### **🔹 Node 4: "Google Sheets" (Type: `googleSheets`)**
- **Cần thiết lập:**
  - **Credentials**: Chọn `googleSheetsOAuth2Api` (đã cấu hình OAuth 2.0).
  - **Sheet Name**: Điền **tên sheet** muốn lưu kết quả (ví dụ: `Bất động sản Phước Long`).
  - **Range**: Để mặc định là `Sheet1!A1` (hoặc chỉnh theo cấu trúc sheet của các sếp).

#### **🔹 Node 5: "Initiate a Webhook Notification" (Type: `httpRequest`)**
- **Cần thiết lập:**
  - **URL**: Điền **URL webhook** của Slack/Telegram/CRM (ví dụ: `https://hooks.slack.com/services/...`).
  - **Headers**: Thêm `Content-Type: application/json`.
  - **Body**: Workflow sẽ tự động tạo payload JSON (không cần chỉnh).

---
### **3. Kích hoạt ⚡️**
1. **Test Run** (để kiểm tra):
   - Nhấn **"Test"** trên node `Manual Trigger` (node đầu tiên).
   - Kiểm tra **Google Sheets** và **webhook** xem dữ liệu có xuất ra không.
   - Nếu có lỗi, kiểm tra **logs** trong node `StickyNote` (nếu có).

2. **Bật Active**:
   - Sau khi test thành công, **điều chỉnh workflow thành "Active"**.
   - **Lưu workflow** và **đặt lịch chạy định kỳ** (ví dụ: mỗi ngày 8h sáng) trong **n8n Scheduler**.

---
## ✍️ **Mẹo & gợi ý nâng cao**
### **🔹 Mở rộng với Slack/Telegram**
- **Gửi thông báo Slack/Telegram** khi có dữ liệu mới:
  - Thay đổi node `httpRequest` (Webhook Notification) để gửi tin nhắn tự động.
  - Ví dụ payload Slack:
    ```json
    {
      "text": "🏠 **Dữ liệu bất động sản mới:**\n- URL: {{ $node["Perform Bright Data Web Request"].json()["url"] }}\n- Giá: {{ $node["Structured Data Extractor"].json()["price"] }}\n- Diện tích: {{ $node["Structured Data Extractor"].json()["area"] }}"
    }
    ```

### **🔹 Lưu log vào Google Drive**
- Thêm node `googleDrive` để lưu **file JSON** của dữ liệu nguyên thủy vào Google Drive.
- Cách làm:
  1. Thêm node `googleDrive` (Type: `googleDrive`).
  2. Cấu hình credentials `googleDriveOAuth2Api`.
  3. Kết nối sau node `Write the structured content to disk` để lưu file.

### **🔹 Tích hợp với CRM (HubSpot/Zoho)**
- **Gửi dữ liệu vào CRM** khi có nhà đầu tư mới:
  - Thay đổi node `httpRequest` (Webhook Notification) để gửi payload JSON vào API của HubSpot/Zoho.
  - Ví dụ payload HubSpot:
    ```json
    {
      "properties": {
        "url": "{{ $node["Perform Bright Data Web Request"].json()["url"] }}",
        "price": "{{ $node["Structured Data Extractor"].json()["price"] }}",
        "area": "{{ $node["Structured Data Extractor"].json()["area"] }}",
        "location": "{{ $node["Structured Data Extractor"].json()["location"] }}"
      }
    }
    ```

### **🔹 Tự động cảnh báo giá xuống**
- **Thêm logic cảnh báo** khi giá giảm:
  - Sử dụng node `function` để so sánh giá hiện tại với giá trước đó (lưu trong Google Sheets).
  - Nếu giá giảm >10%, gửi **tin nhắn Slack** hoặc **email** cảnh báo.

---
## 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi việc **lấy dữ liệu thủ công**, đồng thời **tăng cường hiệu quả phân tích thị trường** nhờ AI. **Chỉ cần 10 phút để setup**, sau đó **dữ liệu tự động cập nhật** mỗi ngày!

👉 **Bắt đầu ngay:**
1. **Cài đặt n8n trên VPS** (nếu self-hosted) hoặc dùng [n8n.io](https://n8n.io/).
2. **Import workflow** và **cấu hình các node quan trọng**.
3. **Bật Active** và **theo dõi kết quả** trên Google Sheets!

**Nếu gặp vấn đề**, liên hệ với tác giả:
- **Email**: [ranjancse@gmail.com](mailto:ranjancse@gmail.com)
- **LinkedIn**: [Ranjan Dailata](https://www.linkedin.com/in/ranjan-dailata/)

---
:::info[**Gợi ý hạ tầng cho n8n**]
Để workflow chạy **ổn định 24/7**, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**Chúc các sếp thành công với việc tự động hóa dữ liệu bất động sản!** 🚀🏢