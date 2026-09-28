---
title: "🦷 Hệ Thống Lịch Hẹn & Quản Trị Nhanh Chóng Cho Nha Kho - Tự Động Hóa 100% Với Supabase, AI & SMS"
description: "Giải pháp tự động hóa lịch hẹn khám nha khoa, quản lý hành chính, tích hợp SMS tự động và AI hỗ trợ tư vấn 24/7 - giảm thời gian hành chính 80% và cải thiện trải nghiệm khách hàng."
slug: "he-thong-lich-hen-nha-kho-suabase-ai-sms"
tags: [n8n, automation, no-code, supabase, ai-chatbot, sms-integration, nha-kho]
keywords: [tự động hóa lịch hẹn nha khoa, supabase n8n, chatbot AI hỗ trợ khám nha, SMS tự động nhắc lịch, quản lý hành chính nha khoa]
---

# 🦷 **Hệ Thống Lịch Hẹn & Quản Trị Nhanh Chóng Cho Nha Kho - Tự Động Hóa 100% Với Supabase, AI & SMS**

---

### **😩 Nỗi Đau Của Các Sếp Nha Kho Hiện Nay**
Hành chính nha khoa thường phải chịu gánh nặng:
- **Lịch hẹn thủ công**: Khách hàng gọi điện, ghi nhớ ngày giờ, dễ bị nhầm lẫn hoặc quên.
- **Quản lý hồ sơ phức tạp**: Dữ liệu phân tán giữa giấy tờ, Excel và hệ thống cũ.
- **Hỗ trợ khách hàng chậm**: Y tá phải trả lời hàng chục tin nhắn/SMS mỗi ngày, làm giảm chất lượng dịch vụ.
- **Tăng trưởng chậm**: Không có hệ thống tự động hóa để mở rộng dịch vụ mà không tăng nhân sự.

**Giải pháp?** Một **hệ thống tự động hóa toàn diện** kết hợp:
✅ **Supabase** (Database) – Quản lý lịch hẹn, hồ sơ khách hàng và dữ liệu an toàn.
✅ **SMS tự động** – Nhắc nhở lịch hẹn, xác nhận đặt lịch, giảm tỷ lệ bỏ lịch.
✅ **AI Chatbot** – Trả lời thắc mắc y khoa, tư vấn khám nhanh, giảm tải cho nhân viên.
✅ **Tích hợp Webhook** – Nhận và xử lý yêu cầu đặt lịch từ nhiều kênh (website, SMS, chatbot).

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động **ổn định 24/7**, các sếp nên **self-host n8n** trên VPS chuyên dụng:
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 Mã giảm giá: **VPSN8N** - giảm tới **39%**)
👉 **[VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (Đảm bảo tốc độ xử lý nhanh cho AI & SMS)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80% thời gian hành chính**: Không cần ghi chép thủ công, tự động hóa từ đặt lịch đến nhắc nhở.
- **Giảm tỷ lệ bỏ lịch**: SMS tự động nhắc nhở với **tỷ lệ hoàn thành lên đến 70%**.
- **Hỗ trợ khách hàng 24/7**: AI Chatbot trả lời thắc mắc y khoa ngay lập tức, giảm tải cho nhân viên.
- **Dữ liệu thống kê chi tiết**: Theo dõi lịch hẹn, doanh thu, và hành vi khách hàng trên **Supabase Dashboard**.
- **Mở rộng dịch vụ dễ dàng**: Thêm dịch vụ mới (khám răng, nha khoa thẩm mỹ) mà không cần tăng nhân sự.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi chạy workflow, các sếp cần chuẩn bị:
1. **Tài khoản Supabase**:
   - **Database** để lưu trữ lịch hẹn, hồ sơ khách hàng và dữ liệu nha khoa.
   - **API Key** và **URL Supabase** (có thể tạo miễn phí tại [supabase.com](https://supabase.com/)).
   - **Table** cần thiết:
     - `appointments` (lịch hẹn)
     - `patients` (thông tin khách hàng)
     - `services` (dịch vụ khám nha).

2. **Dịch vụ SMS**:
   - **API Key** từ một nhà cung cấp SMS như:
     - [Twilio](https://www.twilio.com/)
     - [Nexmo](https://www.nexmo.com/)
     - [VietnamTel](https://vietnamtel.vn/) (đối với số Việt Nam).
   - **Số điện thoại** để gửi nhắc nhở (có thể là số của nha khoa).

3. **API Key OpenAI (LLM)**:
   - Để AI Chatbot trả lời thắc mắc y khoa. Các sếp có thể:
     - Sử dụng **miễn phí** với mô hình `gpt-3.5-turbo` (có giới hạn).
     - **Upgrade** với mô hình `gpt-4` nếu cần độ chính xác cao hơn.

4. **Webhook URL**:
   - Một **URL công khai** để nhận yêu cầu đặt lịch từ website hoặc chatbot (có thể sử dụng **ngrok** để tạo URL test).

5. **Credentials cho n8n**:
   - **Supabase**: Đăng ký **credentials** trong n8n với `URL`, `Key`, và `Database Name`.
   - **SMS Provider**: Đăng ký **credentials** với `Account SID`, `Auth Token`, và `Phone Number`.
   - **OpenAI**: Đăng ký **credentials** với `API Key`.

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/11463) hoặc copy **JSON** từ editor n8n.
- **Cách import**:
  1. Mở **n8n Editor** trên VPS.
  2. Nhấn **Import** → **Paste JSON** và dán nội dung.
  3. Chọn **Create Workflow**.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này gồm **7 node chính** cần cấu hình cẩn thận:

##### **A. Node `Webhook` (n8n-nodes-base.webhook)**
- **Mục đích**: Nhận yêu cầu đặt lịch từ website, SMS, hoặc chatbot.
- **Cấu hình**:
  - **HTTP Method**: `POST`.
  - **Path**: `/appointment` (hoặc tùy chỉnh).
  - **Credentials**: Không cần (hoặc sử dụng **Basic Auth** nếu cần bảo mật).
  - **Response**: Chọn `JSON`.

##### **B. Node `Supabase` (n8n-nodes-base.supabase)**
- **Mục đích**: Tạo/đọc/xóa dữ liệu lịch hẹn và khách hàng trên Supabase.
- **Cấu hình**:
  1. **Credentials**:
     - `URL`: `https://<your-project-ref>.supabase.co`
     - `Key`: `your-supabase-key`
     - `Database Name`: `postgres` (mặc định).
  2. **Query**:
     - **Tạo lịch hẹn**:
       ```sql
       INSERT INTO appointments (patient_id, service_id, date, time, status)
       VALUES ($.patient_id, $.service_id, $.date, $.time, 'pending')
       ```
     - **Cập nhật trạng thái**:
       ```sql
       UPDATE appointments SET status = 'completed' WHERE id = $node["appointments"]["data"][0].id
       ```

##### **C. Node `SMS` (n8n-nodes-base.http + Twilio/Nexmo)**
- **Mục đích**: Gửi SMS nhắc nhở lịch hẹn.
- **Cấu hình**:
  1. **Credentials**:
     - **Twilio**:
       - `Account SID`: `your_account_sid`
       - `Auth Token`: `your_auth_token`
       - `From Number`: `+1234567890` (số gửi SMS).
     - **Nexmo**:
       - `API Key` và `API Secret`.
  2. **Request Body**:
     ```json
     {
       "to": "+84123456789",
       "from": "+1234567890",
       "body": "Xin chào! Lịch hẹn khám răng của bạn vào ngày {{date}} tại {{time}} đã được xác nhận."
     }
     ```

##### **D. Node `LLM Chatbot` (n8n-nodes-langchain.lmChatOpenAi)**
- **Mục đích**: AI trả lời thắc mắc y khoa từ khách hàng.
- **Cấu hình**:
  1. **Credentials**:
     - `OpenAI API Key`: `your_openai_key`.
  2. **Prompt**:
     ```plaintext
     Bạn là một chuyên gia nha khoa. Trả lời thắc mắc của khách hàng về:
     - Các loại khám răng (khám tổng quát, nha khoa thẩm mỹ, răng hàm mặt).
     - Cách chăm sóc răng miệng sau khi khám.
     - Giá dịch vụ và bảo hiểm y tế.
     Nếu không biết, hãy trả lời: "Tôi sẽ liên hệ với bác sĩ để tư vấn chi tiết."
     ```
  3. **Input**:
     - Dữ liệu từ **Webhook** hoặc **Chatbot** (ví dụ: `"Tôi muốn khám răng hàm mặt, giá bao nhiêu?"`).

##### **E. Node `Aggregate` (n8n-nodes-base.aggregate)**
- **Mục đích**: Gộp dữ liệu từ nhiều nguồn (SMS, AI, Supabase) trước khi xử lý.
- **Cấu hình**:
  - **Trigger**: Chọn `Webhook` hoặc `SMS`.
  - **Fields to aggregate**: `patient_id`, `appointment_id`, `message`.

##### **F. Node `Switch` (n8n-nodes-base.switch)**
- **Mục đích**: Xác định hành động dựa trên trạng thái lịch hẹn (đã hoàn thành, hủy, chờ xử lý).
- **Cấu hình**:
  - **Condition**:
    - `status === 'completed'` → Gửi SMS cảm ơn.
    - `status === 'cancelled'` → Gửi SMS thông báo hủy lịch.
    - `status === 'pending'` → Gửi SMS nhắc nhở.

##### **G. Node `StickyNote` (n8n-nodes-base.stickyNote)**
- **Mục đích**: Ghi chú nội bộ cho nhân viên (ví dụ: "Khách hàng cần khám khẩn cấp").
- **Cấu hình**:
  - **Text**: `Khách hàng {{patient_name}} cần khám khẩn cấp về {{issue}}`.

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Gửi một **yêu cầu đặt lịch mẫu** qua Webhook (sử dụng **Postman** hoặc **ngrok**).
   - Kiểm tra:
     - Lịch hẹn có được tạo trên **Supabase** không?
     - SMS nhắc nhở có được gửi không?
     - AI Chatbot có trả lời chính xác không?

2. **Bật Active**:
   - Nhấn **Active** trên workflow trong n8n Editor.
   - **Monitor** trên **Supabase Dashboard** và **n8n Dashboard** để theo dõi hoạt động.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tích Hợp Slack/Telegram**:
   - Sử dụng **node `slack`** hoặc **`telegram`** để thông báo lịch hẹn cho nhân viên.
   - **Cách làm**:
     - Thêm **node `slack`** sau `Supabase` với message:
       ```json
       {
         "text": "📅 Lịch hẹn mới: {{patient_name}} - {{service}} vào {{date}} {{time}}",
         "blocks": [...]
       }
       ```

2. **Lưu Log & Báo Cáo**:
   - Sử dụng **node `log`** để ghi lại tất cả hoạt động (đặt lịch, hủy lịch, AI trả lời).
   - **Tích hợp với Google Sheets** để tạo **báo cáo hàng tháng**:
     - Thêm **node `google-sheets`** sau `Aggregate` để ghi dữ liệu vào sheet.

3. **Cá Nhân Hóa SMS**:
   - Thay vì SMS chung, **tùy chỉnh nội dung** dựa trên dịch vụ khám:
     - **Khám răng tổng quát**:
       ```plaintext
       Xin chào {{patient_name}}! Lịch khám răng tổng quát vào {{date}} {{time}} đã được xác nhận. Chúng tôi sẽ chuẩn bị dụng cụ khám.
       ```
     - **Nha khoa thẩm mỹ**:
       ```plaintext
       Xin chào {{patient_name}}! Lịch khám nha khoa thẩm mỹ vào {{date}} {{time}} đã được xác nhận. Vui lòng mang theo ảnh răng trước khi khám.
       ```

4. **Hỗ Trợ Ngôn Ngữ Múlti**:
   - Sử dụng **node `translate`** (ví dụ: **DeepL API**) để chuyển đổi SMS/AI Chatbot sang tiếng Việt hoặc tiếng Anh tùy chọn.

5. **Tự Động Xóa Lịch Hủy**:
   - Thêm **node `supabase`** sau `Switch` để xóa lịch khi khách hàng hủy:
     ```sql
     DELETE FROM appointments WHERE id = $node["appointments"]["data"][0].id
     ```

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian hành chính**, **tăng trải nghiệm khách hàng**, và **mở rộng dịch vụ** cho nha khoa một cách **tự động hóa hoàn toàn**. Các sếp chỉ cần:
1. **Chuẩn bị Supabase, SMS API, và OpenAI Key**.
2. **Import workflow** và cấu hình các node.
3. **Bật Active** và theo dõi kết quả!

**🚀 Hành động ngay**: Đăng ký **VPS TinoHost** với mã giảm giá **VPSN8N** để chạy workflow ổn định 24/7. Nếu có thắc mắc, để lại bình luận bên dưới hoặc liên hệ **Isight** (tác giả) qua [n8n Community](https://community.n8n.io/).

---
**#TựĐộngHóaNhaKho #SupabaseN8N #AIChoNhaKho #SMSAutomation**