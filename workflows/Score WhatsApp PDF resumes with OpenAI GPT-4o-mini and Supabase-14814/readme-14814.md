---
title: "📊 Tự Động Đánh Giá CV PDF trên WhatsApp bằng GPT-4o-mini & Supabase - Giúp HR Tiết Kiệm 100h/Năm"
description: "Workflow tự động hóa đánh giá CV PDF từ ứng viên qua WhatsApp bằng trí tuệ nhân tạo GPT-4o-mini, kết hợp cơ sở dữ liệu Supabase để lưu trữ và phân loại ứng viên. Giúp HR tiết kiệm thời gian, giảm thiểu sai sót và tăng cường hiệu quả tuyển dụng."
slug: "tieu-dong-danh-gia-cv-pdf-whatsapp-gpt-4o-mini-supabase"
tags: [n8n, automation, hr, ai-chatbot, openai, supabase, whatsapp-business-api]
keywords: [tự động hóa tuyển dụng, đánh giá cv bằng ai, n8n workflow, chatbot hr, supabase database, gpt-4o-mini, whatsapp automation]
---

# 🚀 **Tự Động Đánh Giá CV PDF qua WhatsApp với GPT-4o-mini & Supabase**

### **Giải pháp AI cho HR: Đánh giá CV chỉ trong vài giây, không cần code!**
Hiện nay, việc tuyển dụng thường là một quá trình tốn thời gian và mệt mỏi: HR phải đọc hàng trăm CV, đánh giá kỹ năng, kinh nghiệm và phù hợp với vị trí. Với **workflow này**, các sếp sẽ tự động hóa toàn bộ quy trình:
- **Nhận CV PDF** từ ứng viên qua WhatsApp Business API.
- **Đánh giá nội dung** bằng GPT-4o-mini (OpenAI) để trích xuất thông tin quan trọng như kinh nghiệm, kỹ năng, trình độ học vấn.
- **Lưu trữ và phân loại** ứng viên vào cơ sở dữ liệu Supabase, giúp dễ dàng theo dõi và lọc ứng viên phù hợp.
- **Gửi phản hồi tự động** cho ứng viên, tiết kiệm thời gian và cải thiện trải nghiệm ứng tuyển.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow hoạt động 24/7 với hiệu suất tối ưu, các sếp nên **self-host n8n** trên VPS chuyên dụng:
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 **[VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (đảm bảo tốc độ xử lý nhanh cho AI)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 100+ giờ/năm** cho bộ phận HR: Không cần đọc CV thủ công.
- **Đánh giá khách quan** bằng AI: Tránh chủ quan và giảm thiểu sai sót.
- **Lưu trữ và quản lý** ứng viên hiệu quả: Supabase giúp theo dõi và phân loại ứng viên một cách dễ dàng.
- **Trải nghiệm ứng viên tốt hơn**: Phản hồi tự động và nhanh chóng.
- **Cải thiện chất lượng tuyển dụng**: Lọc ứng viên phù hợp với vị trí nhanh chóng.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản WhatsApp Business API**:
   - Đăng ký trên [Facebook Developer](https://developers.facebook.com/) và lấy **API Key** và **Phone Number ID**.
   - Cài đặt **Webhook URL** của n8n để nhận tin nhắn từ ứng viên.

2. **Tài khoản OpenAI**:
   - Đăng ký trên [OpenAI](https://platform.openai.com/) và lấy **API Key** để sử dụng GPT-4o-mini.

3. **Tài khoản Supabase**:
   - Đăng ký trên [Supabase](https://supabase.com/) và tạo một **Database Project**.
   - Lấy **URL Database** và **Anonymized Public Key** để kết nối với n8n.

4. **File `.env` (nếu cần)**:
   - Các sếp có thể lưu trữ API Key và thông tin kết nối trong file `.env` để bảo mật.

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/14814](https://n8n.io/workflows/14814) (nếu có) hoặc sao chép JSON từ trang này.
- Mở **n8n Editor** và chọn **Import Workflow** → Dán JSON hoặc tải file `.json`.
- **Kích hoạt mode "Active"** để workflow bắt đầu hoạt động.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflows này sử dụng các node chính sau. Các sếp cần cấu hình kỹ lưỡng:

##### **🔹 Node `WhatsApp Trigger` (n8n-nodes-base.whatsAppTrigger)**
- **Cấu hình**:
  - **Phone Number ID**: Điền từ WhatsApp Business API.
  - **Webhook URL**: Điền URL của n8n (ví dụ: `https://tên-domain.n8n.workers.dev`).
  - **Message Type**: Chọn `text` hoặc `document` (để nhận CV PDF).

##### **🔹 Node `Extract From File` (n8n-nodes-base.extractFromFile)**
- **Cấu hình**:
  - **File Type**: Chọn `PDF`.
  - **Extract Text**: Bật để trích xuất toàn bộ nội dung từ CV.

##### **🔹 Node `Code` (n8n-nodes-base.code)**
- **Cấu hình**:
  - **Script**: Sử dụng mã JavaScript để chuẩn bị dữ liệu cho GPT-4o-mini.
  - **Ví dụ**:
    ```javascript
    // Chuyển đổi dữ liệu từ WhatsApp thành format phù hợp cho OpenAI
    return {
      content: $input.all().map(item => ({
        role: "user",
        content: `Analyze this resume PDF: ${item.json.text}`
      })).flat(),
    };
    ```

##### **🔹 Node `HTTP Request` (n8n-nodes-base.httpRequest)**
- **Cấu hình**:
  - **Method**: `POST`.
  - **URL**: `https://api.openai.com/v1/chat/completions`.
  - **Headers**:
    - `Authorization: Bearer {API_KEY_OPENAI}`.
    - `Content-Type: application/json`.
  - **Body**:
    ```json
    {
      "model": "gpt-4o-mini",
      "messages": $input.all(),
      "temperature": 0.7
    }
    ```

##### **🔹 Node `Set` (n8n-nodes-base.set)**
- **Cấu hình**:
  - **Key**: `resume_score` (hoặc tên khác tùy ý).
  - **Value**: Trích xuất kết quả từ OpenAI (ví dụ: `skills`, `experience`, `score`).

##### **🔹 Node `Supabase` (n8n-nodes-base.httpRequest)**
- **Cấu hình**:
  - **Method**: `POST`.
  - **URL**: `https://{PROJECT_REF}.supabase.co/rest/v1/{TABLE_NAME}`.
  - **Headers**:
    - `apikey: {ANON_PUBLIC_KEY}`.
    - `Authorization: Bearer {API_KEY}`.
  - **Body**:
    ```json
    {
      "name": $input.all()[0].json.name,
      "skills": $input.all()[0].json.skills,
      "experience": $input.all()[0].json.experience,
      "score": $input.all()[0].json.resume_score
    }
    ```

##### **🔹 Node `WhatsApp` (n8n-nodes-base.whatsApp)**
- **Cấu hình**:
  - **Phone Number ID**: Điền từ WhatsApp Business API.
  - **Message**: Gửi phản hồi tự động cho ứng viên (ví dụ: `Xin chào {name}, CV của bạn đã được nhận và đang được đánh giá. Chúng tôi sẽ liên hệ lại trong 24h.`).

---

#### **3. Kích hoạt ⚡️**
- **Test Run**:
  - Gửi một tin nhắn PDF từ WhatsApp Business API đến số điện thoại đã đăng ký.
  - Kiểm tra **n8n Editor** để xem workflow có chạy đúng không.
- **Bật Active**:
  - Sau khi test thành công, chuyển workflow sang **mode "Active"**.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Tích hợp Slack/Telegram**:
   - Sử dụng node `Slack` hoặc `Telegram` để thông báo kết quả đánh giá cho team HR.

2. **Lưu log hoạt động**:
   - Sử dụng node `Sticky Note` (n8n-nodes-base.stickyNote) để ghi lại lịch sử đánh giá.

3. **Gửi báo cáo định kỳ**:
   - Sử dụng node `HTTP Request` kết hợp với `Set` để tạo báo cáo Excel/PDF và gửi qua email.

4. **Cải thiện prompt cho GPT-4o-mini**:
   - Tùy chỉnh prompt để AI đánh giá theo tiêu chí cụ thể của công ty (ví dụ: yêu cầu kỹ năng cụ thể).

5. **Tích hợp với CRM**:
   - Kết nối với **HubSpot** hoặc **Zoho CRM** để tự động chuyển ứng viên phù hợp vào pipeline tuyển dụng.

---

### 📌 **Kết luận**
Workflow này **giải phóng HR khỏi công việc mòn mỏi đọc CV**, giúp tự động hóa quy trình tuyển dụng với độ chính xác cao nhờ trí tuệ nhân tạo. **Bắt đầu tự động hóa ngay hôm nay** và tiết kiệm thời gian cho đội ngũ của mình!

👉 **[Tải workflow này](https://n8n.io/workflows/14814)** và **cài đặt trên VPS** để bắt đầu!
👉 **[Hướng dẫn self-host n8n](https://docs.n8n.io/hosting/self-hosting-on-a-vps/)** nếu chưa có.