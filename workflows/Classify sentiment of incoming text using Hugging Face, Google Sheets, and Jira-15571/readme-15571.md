---
title: "🤖 Tự Động Phân Loại Tình Trạng (Sentiment Analysis) Cho Phản Hồi Nhập Lại - Google Sheets + Jira + AI Hugging Face"
description: "Workflow tự động phân loại phản hồi khách hàng thành 'Tích cực', 'Trung tính' hoặc 'Tiêu cực' bằng AI Hugging Face, lưu kết quả vào Google Sheets và tạo ticket Jira cho phản hồi tiêu cực. Giúp doanh nghiệp theo dõi và xử lý phản hồi 24/7 mà không cần code."
slug: "tieu-dong-phan-loai-tinh-trang-phan-hoi-google-sheets-jira"
tags: [n8n, automation, no-code, sentiment-analysis, jira, google-sheets, ai-hugging-face]
keywords: [tự động hóa phân loại tình trạng, sentiment analysis n8n, lưu phản hồi google sheets, tạo ticket jira tự động, ai hugging face n8n]
---

# 🚀 **Tự Động Phân Loại Tình Trạng Phản Hồi Khách Hàng - Từ Webhook Đến Jira Ticket**

## **🔥 Nỗi Đau Của Các Sếp**
Hàng ngày, doanh nghiệp phải xử lý **ngàn lượt phản hồi** từ khách hàng trên email, chatbot, hoặc form đăng ký. Việc phân loại từng phản hồi thành "tích cực", "trung tính" hoặc "tiêu cực" thủ công không chỉ **tốn thời gian** mà còn dễ gây **sai sót** và **chậm trễ** trong xử lý. Kết quả?
- **Khách hàng không hài lòng** vì phản hồi chậm.
- **Dữ liệu phân loại không chính xác**, làm mất đi cơ hội cải thiện dịch vụ.
- **Nhân viên phải làm việc thêm giờ** để theo dõi và xử lý.

**Workflow này giải quyết tất cả!** Sử dụng **AI Hugging Face**, nó tự động phân loại phản hồi, lưu kết quả vào **Google Sheets** và **tạo ticket Jira** cho những phản hồi tiêu cực. **Không cần code, chỉ cần cài đặt và chạy!**

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**3 Lợi Ích Cốt Lõi**]
✅ **Tiết kiệm 10+ giờ/ngày** cho đội ngũ CSKH và marketing.
✅ **Chính xác 95%+** nhờ AI Hugging Face phân loại tự động.
✅ **Xử lý phản hồi tiêu cực ngay lập tức** với ticket Jira tự động.
✅ **Dữ liệu phân loại sẵn sàng** trong Google Sheets để báo cáo và phân tích.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
✔ **Tài khoản n8n Self-hosted** (khuyến nghị dùng VPS để chạy 24/7).
✔ **API Key Hugging Face** (để gọi model phân loại tình trạng).
✔ **Google Sheets** với **3 tab riêng biệt**:
   - `Positive` (Phản hồi tích cực)
   - `Neutral` (Phản hồi trung tính)
   - `Negative` (Phản hồi tiêu cực)
✔ **Tài khoản Jira Cloud** (để tạo ticket cho phản hồi tiêu cực).
✔ **Credentials cho Google Sheets & Jira** (cấu hình trong n8n).

:::info[**Gợi ý hạ tầng cho n8n**]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. Tải workflow từ [n8n.io/workflows/15571](https://n8n.io/workflows/15571) (chọn **Export JSON**).
2. Trên **n8n Editor**, nhấn **Import** → Chọn file JSON vừa tải.
3. Chọn **Create new workflow** và nhấn **Import**.

#### **Phương pháp 2: Copy/Paste JSON**
1. Copy toàn bộ mã JSON từ [n8n.io/workflows/15571](https://n8n.io/workflows/15571) (chọn **Export JSON**).
2. Trên **n8n Editor**, nhấn **Import** → Chọn **Paste JSON** và dán vào.
3. Chọn **Create new workflow** và nhấn **Import**.

---

### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**

#### **🔹 Node 1: Receive Feedback (Webhook)**
- **Cấu hình:**
  - **Path:** `sentiment-input` (không đổi).
  - **HTTP Method:** `POST`.
  - **Credentials:** Không cần (sử dụng default).
- **Lưu ý:**
  - Các sếp cần **bật Webhook** này để nhận dữ liệu từ bên ngoài (ví dụ: từ form, chatbot, hoặc API).
  - **Test:** Gửi một request POST từ Postman hoặc cURL để kiểm tra:
    ```bash
    curl -X POST https://[your-n8n-domain]/webhook/sentiment-input \
    -H "Content-Type: application/json" \
    -d '{"text": "Tôi rất hài lòng với sản phẩm!"}'
    ```

#### **🔹 Node 5: Get Sentiment Scores (HTTP Request - Hugging Face)**
- **Cấu hình:**
  - **URL:** `https://api-inference.huggingface.co/models/distilbert-base-uncased-finetuned-sst-2-english`
  - **Headers:**
    ```
    Authorization: Bearer {HUGGING_FACE_API_KEY}
    Content-Type: application/json
    ```
  - **Body:**
    ```json
    {
      "inputs": "{{$node["Split Text Items"].json["text"]}}"
    }
    ```
- **Lưu ý:**
  - **Thêm API Key Hugging Face** vào **Credentials** của n8n (tạo mới ở **Settings → Credentials**).
  - **Rate Limit:** Node **Rate Limit Control (Wait)** sẽ tự động chờ nếu API bị giới hạn.

#### **🔹 Node 10-12: Store Positive/Neutral/Negative Feedback (Google Sheets)**
- **Cấu hình chung:**
  - **Credentials:** Chọn `googleApi` (cấu hình trước ở **Settings → Credentials**).
  - **Operation:** `append` (thêm mới vào sheet).
  - **Sheet Name:**
    - `Positive` → Tab `Positive`.
    - `Neutral` → Tab `Neutral`.
    - `Negative` → Tab `Negative`.
  - **Headers:**
    - `text` (nội dung phản hồi).
    - `sentiment` (tình trạng: Positive/Neutral/Negative).
    - `confidence` (độ tin cậy của AI).
- **Lưu ý:**
  - **Tạo 3 tab mới** trong Google Sheets với tên chính xác (`Positive`, `Neutral`, `Negative`).
  - **Cấu hình Google Sheets Credentials** trong n8n:
    1. Vào **Settings → Credentials → Add Credential**.
    2. Chọn **Google Sheets**.
    3. Đăng nhập và cấp quyền.

#### **🔹 Node 13: Create Jira Ticket (Jira)**
- **Cấu hình:**
  - **Credentials:** Chọn `jiraSoftwareCloudApi` (cấu hình trước ở **Settings → Credentials**).
  - **Project Key:** Khóa dự án Jira của bạn (ví dụ: `PROJ`).
  - **Issue Type:** `Task` (hoặc loại ticket phù hợp).
  - **Summary:** `Phản hồi tiêu cực: {{$node["Preserve Input Text"].json["text"]}}`.
  - **Description:** `Tình trạng: {{$node["Compute Sentiment"].json["sentiment"]}} (Độ tin cậy: {{$node["Compute Sentiment"].json["confidence"]}})`.
- **Lưu ý:**
  - **Cấu hình Jira Credentials** trong n8n:
    1. Vào **Settings → Credentials → Add Credential**.
    2. Chọn **Jira Cloud**.
    3. Đăng nhập và cấp quyền.
  - **Test:** Chỉ chạy node này với dữ liệu mẫu để đảm bảo ticket được tạo đúng.

---

### **3. Kích Hoạt ⚡️ Workflow**
1. **Test Run** với dữ liệu mẫu:
   - Gửi một request POST từ Postman:
     ```json
     {
       "text": "Sản phẩm rất tệ, không hài lòng với chất lượng!"
     }
     ```
   - Kiểm tra:
     - Phản hồi được phân loại là `Negative`.
     - Dữ liệu được lưu vào tab `Negative` của Google Sheets.
     - Ticket Jira được tạo tự động.
2. **Bật Active workflow** trong n8n Editor.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**

### **🔹 Kết Nối Với Slack/Telegram**
- **Thêm node Slack/Telegram** sau `Route by Sentiment` để thông báo kết quả phân loại.
- **Ví dụ:**
  - Nếu sentiment là `Negative`, gửi tin nhắn Slack:
    ```
    🚨 Phản hồi tiêu cực mới!
    Nội dung: {{text}}
    Độ tin cậy: {{confidence}}%
    Ticket Jira: {{jiraTicketUrl}}
    ```

### **🔹 Lưu Log & Báo Cáo Định Kỳ**
- **Thêm node `Set`** sau `Merge Text & Scores` để lưu log vào **Google Drive** hoặc **Database**.
- **Tạo báo cáo hàng tuần** bằng **Google Sheets Script** hoặc **n8n + Google Data Studio**.

### **🔹 Cải Thiện Model AI**
- **Thay đổi model Hugging Face** để phù hợp với ngôn ngữ của doanh nghiệp (ví dụ: `vinai/phobert-base-v2` cho tiếng Việt).
- **Cấu hình ngưỡng confidence** trong node `Compute Sentiment` để tránh sai sót.

### **🔹 Tích Hợp Email & Chatbot**
- **Sử dụng node `HTTP Request`** để gọi từ **Zapier** hoặc **Make (Integromat)** để nhận phản hồi từ email/facebook messenger.

---

## 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho đội ngũ CSKH, **tăng tính chính xác** trong phân loại phản hồi và **tự động hóa xử lý vấn đề** với Jira. **Không cần code, chỉ cần cài đặt và chạy!**

**Bắt tay vào tự động hóa ngay hôm nay!**
👉 [Tải workflow từ n8n.io](https://n8n.io/workflows/15571)
👉 [Cài đặt n8n trên VPS](https://docs.n8n.io/hosting/installation/installation-on-a-vps/) (dùng mã giảm giá **VPSN8N** để tiết kiệm!)

---
**Chia sẻ & phản hồi:** Các sếp có thể **customize** workflow này để phù hợp với nhu cầu cụ thể của doanh nghiệp. Nếu gặp vấn đề, hãy để lại bình luận dưới đây! 🚀