---
title: "🤖 **Tự Động Xử Lý & Phân Loại Email Hỏi Hàng Chờ Sẵn với Gmail + AI Gemini (N8N)**"
description: "Workflow tự động hóa hoàn toàn xử lý email hỏi hàng, phân loại yêu cầu (kiểm tra sẵn có hoặc đặt chỗ trực tiếp) bằng AI Gemini, gửi phản hồi tự động hoặc chuyển email cho bộ phận hỗ trợ. Giúp tiết kiệm 80% thời gian xử lý email hàng ngày cho các sếp và đội ngũ support."
slug: "tieu-dong-xu-ly-email-ai-gemini-n8n"
tags: [n8n, automation, ai-chatbot, gmail-integration, support-automation]
keywords: [n8n workflow email, tự động hóa hỗ trợ khách hàng, AI Gemini n8n, phân loại email hỏi hàng, gửi phản hồi tự động]
---

# 🚀 **Tự Động Xử Lý Email Hỏi Hàng Chờ Sẵn với Gmail + AI Gemini (N8N)**

### **Nỗi đau thực tế của các sếp và đội ngũ support**
Hàng ngày, các sếp và nhân viên support phải mất **giờ đồng hồ** để:
- Lọc và phân loại hàng trăm email hỏi hàng (kiểm tra sẵn có phòng, đặt chỗ, yêu cầu thông tin).
- Trả lời từng email một cách thủ công, dẫn đến **trễ tràng** và **chất lượng phản hồi không đồng đều**.
- Chuyển email đặt chỗ cho bộ phận khác mà không có hệ thống tự động hóa, gây **lặp lại công việc** và **sai sót**.

**Workflow này giải quyết tất cả đó bằng cách:**
✅ **Phân loại tự động** email thành **kiểm tra sẵn có** hoặc **đặt chỗ trực tiếp** bằng AI Gemini.
✅ **Gửi phản hồi tự động** cho khách hàng khi yêu cầu là kiểm tra sẵn có.
✅ **Chuyển email đặt chỗ** sang bộ phận hỗ trợ với **thông tin đã được tổng hợp** (không cần copy-paste).
✅ **Hoạt động 24/7** mà không cần can thiệp của con người.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow này chạy **ổn định 24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS riêng.
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (đảm bảo tốc độ cao, không lag)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80% thời gian** xử lý email hàng ngày (từ 2-3 giờ xuống còn 30 phút).
- **Phản hồi khách hàng nhanh chóng** với nội dung **cá nhân hóa** (do AI Gemini tự động tạo).
- **Giảm sai sót** khi chuyển email đặt chỗ (thông tin được **tự động tổng hợp** và chuyển sang bộ phận hỗ trợ).
- **Hoạt động liên tục** mà không cần can thiệp của con người (24/7).
- **Tăng trải nghiệm khách hàng** với thời gian phản hồi **ngắn hơn 5 phút** cho yêu cầu kiểm tra sẵn có.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Gmail** (đã cấp quyền OAuth 2.0 cho n8n):
   - **Credentials**: `gmailOAuth2` (đăng ký tại [n8n Credentials](https://n8n.io/docs/credentials/)).
   - **Email chính** để nhận và gửi email tự động.
   - **Email bộ phận hỗ trợ** (ví dụ: `support@doanhnghiep.com`) để chuyển email đặt chỗ.

2. **API Key Google Gemini**:
   - **Credentials**: `googlePalmApi` (đăng ký tại [Google AI Studio](https://makersuite.google.com/)).
   - **Tài khoản Google Cloud** với quyền sử dụng **Generative AI API**.

3. **Thông tin bổ sung (nếu cần)**:
   - **Danh sách phòng/giá sẵn có** (nếu muốn AI trả lời chi tiết về sẵn có).
   - **Mẫu email phản hồi** (có thể tùy chỉnh trong node **Code**).

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có **2 cách** để import workflow này:
- **Tải file JSON** từ [n8n.io/workflows/6633](https://n8n.io/workflows/6633) và import vào **n8n Editor**.
- **Copy toàn bộ JSON** từ link trên và **paste** vào **Import Workflow** trong n8n.

**Bước cụ thể:**
1. Mở **n8n Editor** ([n8n.io](https://n8n.io/)).
2. Nhấn **Import Workflow** → Chọn **JSON** hoặc **Paste JSON**.
3. Chọn file JSON đã tải hoặc **copy-paste** toàn bộ mã từ [n8n.io/workflows/6633](https://n8n.io/workflows/6633).

---

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này có **9 node** chính, nhưng **3 node quan trọng nhất** cần cấu hình cẩn thận:

##### **A. Node Gmail Trigger (Bắt đầu workflow)**
- **Credentials**: Chọn `gmailOAuth2` (đã đăng ký trước).
- **Label**: Chọn **inbox** (hoặc folder chứa email hỏi hàng).
- **Test**: Nhấn **Run Once** để kiểm tra nếu email mới được bắt được.

##### **B. Node AI Agent (Google Gemini)**
- **Model**: Chọn `Google Gemini` (nếu có vấn đề, xem phần **Mẹo & gợi ý nâng cao**).
- **Credentials**: Chọn `googlePalmApi` (đã đăng ký API Key).
- **Prompt mặc định** (có thể tùy chỉnh trong node **Code**):
  ```json
  {
    "instruction": "Phân loại email này là yêu cầu gì? Nó là yêu cầu kiểm tra sẵn có phòng (check_availability) hay yêu cầu đặt chỗ trực tiếp (forward_booking)?\n\nNếu là yêu cầu kiểm tra sẵn có, hãy trả lời email với thông tin sẵn có và giá.\nNếu là yêu cầu đặt chỗ, hãy chuyển email này cho bộ phận hỗ trợ với thông tin đã được tổng hợp.\n\nTrả lời dưới dạng JSON:\n{\n  \"action\": \"check_availability\" || \"forward_booking\",\n  \"email_response\": \"Nội dung phản hồi cho khách hàng\",\n  \"internal_notes\": \"Ghi chú nội bộ cho bộ phận hỗ trợ\"\n}",
    "thoughts": true
  }
  ```
- **Lưu ý**: Nếu AI trả lời dưới dạng **markdown** (có ```json```), node **Code** sẽ tự động chuyển đổi thành JSON.

##### **C. Node Code (Chuyển đổi JSON)**
- **Code mặc định** (có thể chỉnh sửa nếu AI trả lời không chuẩn):
  ```javascript
  // Kiểm tra nếu output là string và có dấu ```json``` thì chuyển đổi
  if (typeof $input.all().json === 'string' && $input.all().json.includes('```json')) {
    const jsonString = $input.all().json.replace(/`{3}json\n?/, '').replace(/`{3}/, '');
    try {
      return { json: JSON.parse(jsonString) };
    } catch (e) {
      return { json: { action: 'unknown', email_response: 'Không thể phân loại yêu cầu.', internal_notes: 'Yêu cầu không rõ ràng.' } };
    }
  } else {
    return $input.all();
  }
  ```
- **Test**: Nhấn **Run Once** với email mẫu để kiểm tra output JSON.

##### **D. Node If (Phân loại và chuyển hướng)**
- **Condition**:
  - Nếu `$.json.action === "check_availability"` → Gửi email phản hồi tự động.
  - Nếu `$.json.action === "forward_booking"` → Chuyển email cho bộ phận hỗ trợ.

##### **E. Node Gmail (Gửi phản hồi hoặc chuyển email)**
- **Credentials**: Chọn `gmailOAuth2`.
- **Email gửi**: Điền địa chỉ email khách hàng (trích từ email đầu vào).
- **Nội dung email**: Sử dụng `$json.email_response` (tự động tạo bởi AI).
- **CC/BCC**: Có thể thêm email bộ phận hỗ trợ nếu cần.

---

#### **3. Kích hoạt ⚡️**
1. **Test Run** với email mẫu:
   - Gửi email mẫu vào inbox Gmail đã cấu hình.
   - Kiểm tra workflow có chạy đúng không (kiểm tra log trong n8n).
2. **Bật Active**:
   - Nhấn **Active** trên workflow.
   - **Xem log** trong **Execution History** để đảm bảo không có lỗi.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Tùy chỉnh Prompt cho AI Gemini**
   - Nếu AI trả lời không chính xác, chỉnh sửa **Prompt** trong node **AI Agent** để rõ ràng hơn:
     ```json
     {
       "instruction": "Tôi là AI hỗ trợ đặt chỗ. Hãy phân loại email này theo 2 trường hợp:\n
       1. **Kiểm tra sẵn có phòng** (check_availability): Trả lời email với thông tin sẵn có và giá.\n
       2. **Đặt chỗ trực tiếp** (forward_booking): Chuyển email cho bộ phận hỗ trợ với thông tin khách hàng và yêu cầu.\n\n
       Trả lời dưới dạng JSON chuẩn:\n{\n  \"action\": \"check_availability\" || \"forward_booking\",\n  \"email_response\": \"Nội dung phản hồi cho khách hàng\",\n  \"internal_notes\": \"Ghi chú cho bộ phận hỗ trợ (ví dụ: 'Khách hàng muốn phòng VIP, ngày 15/10')\"\n}",
       "thoughts": false
     }
     ```

2. **Lưu log email vào Google Sheets**
   - Thêm node **Google Sheets** sau node **Gmail** để lưu tất cả email đã xử lý:
     ```json
     {
       "name": "Log Email",
       "type": "googleSheets",
       "credentials": ["googleSheetsOAuth2"],
       "options": {
         "sheetName": "Email_Log",
         "appendRow": true
       }
     }
     ```

3. **Gửi báo cáo định kỳ cho quản lý**
   - Sử dụng node **n8n-nodes-base.email** để gửi báo cáo hàng ngày:
     ```json
     {
       "name": "Send Daily Report",
       "type": "email",
       "credentials": ["gmailOAuth2"],
       "options": {
         "to": "quanly@doanhnghiep.com",
         "subject": "Báo cáo email hỏi hàng ngày hôm nay",
         "html": "<h2>Tổng hợp email đã xử lý:</h2><ul>{{ $json.logs }}</ul>"
       }
     }
     ```

4. **Khắc phục lỗi node Google Gemini**
   - Nếu node **Google Gemini** bị lỗi, thử:
     - **Kiểm tra API Key**: Đảm bảo `googlePalmApi` còn hiệu lực.
     - **Chọn model khác**: Thay `Google Gemini` bằng `text-bison` (nếu có).
     - **Tăng timeout**: Trong node **Wait**, tăng thời gian chờ từ 5s → 30s.

5. **Chuyển email đặt chỗ sang Slack/Telegram**
   - Thay node **Gmail** bằng **Slack Webhook** hoặc **Telegram Bot** để chuyển email cho đội ngũ hỗ trợ:
     ```json
     {
       "name": "Send to Slack",
       "type": "slack",
       "credentials": ["slackWebhook"],
       "options": {
         "text": "📩 **Yêu cầu đặt chỗ mới**: {{ $json.internal_notes }}",
         "attachments": [
           {
             "text": "Email gốc: {{ $input.all().email.body }}"
           }
         ]
       }
     }
     ```

---

### 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp và đội ngũ support bằng cách:
✔ **Tự động phân loại** email hỏi hàng (kiểm tra sẵn có vs đặt chỗ).
✔ **Gửi phản hồi tự động** cho khách hàng với nội dung **cá nhân hóa**.
✔ **Chuyển email đặt chỗ** sang bộ phận hỗ trợ với **thông tin đã được tổng hợp**.
✔ **Hoạt động 24/7** mà không cần can thiệp của con người.

**Hành động ngay hôm nay:**
1. **Import workflow** và cấu hình theo hướng dẫn.
2. **Test với email mẫu** trước khi bật chế độ tự động.
3. **Tùy chỉnh Prompt** để phù hợp với nghiệp vụ của doanh nghiệp.

**🚀 Cài đặt n8n trên VPS ngay để workflow này chạy không ngừng!**
👉 **[Mua VPS TinoHost với mã giảm giá VPSN8N](https://tino.vn/vps-n8n?affid=388)**

---
**Chia sẻ và phản hồi:**
Nếu có câu hỏi hoặc gặp khó khăn, hãy **comment bên dưới** hoặc liên hệ qua [Oneclick AI Squad](https://oneclickai.squad). Chúng tôi sẽ hỗ trợ miễn phí! 💡