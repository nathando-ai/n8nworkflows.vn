---
title: "🤖 Tạo Chatbot AI Thông Minh cho Facebook Messenger với GPT-4o-mini & Nhớ Lịch Sử Chat"
description: "Tự động hóa hỗ trợ khách hàng trên Facebook Messenger bằng AI GPT-4o-mini, lưu trữ lịch sử hội thoại và phản hồi thông minh - giải pháp không cần code cho doanh nghiệp."
slug: "tao-chatbot-ai-facebook-messenger-gpt-4o-mini"
tags: [n8n, automation, ai-chatbot, facebook-messenger, no-code, openai]
keywords: [chatbot facebook messenger tự động hóa, gpt-4o-mini n8n, lưu trữ lịch sử chat ai, tự động trả lời tin nhắn facebook]
---

# 🚀 **Chatbot AI Thông Minh cho Facebook Messenger với GPT-4o-mini**

## **Giải pháp tự động hóa hỗ trợ khách hàng 24/7 mà không cần code**

Hiện nay, doanh nghiệp phải tốn thời gian và nhân lực để trả lời hàng trăm tin nhắn trên Facebook Messenger mỗi ngày. Các tin nhắn lặp đi lặp lại như "Giá bao nhiêu?", "Địa chỉ cửa hàng?", hoặc "Lịch trình giao hàng?" khiến đội ngũ hỗ trợ cảm thấy mệt mỏi. **Workflow này giúp tự động hóa hoàn toàn quá trình này bằng AI GPT-4o-mini**, đồng thời **lưu trữ lịch sử hội thoại** để trả lời chính xác và cá nhân hóa cho từng khách hàng.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Giảm 90% công việc trả lời tin nhắn lặp lại.
- **Trải nghiệm cá nhân hóa**: AI nhớ lịch sử chat và trả lời phù hợp với từng khách hàng.
- **Hỗ trợ 24/7**: Chatbot hoạt động liên tục, không cần nhân viên trực ca.
- **Tối ưu chi phí API**: Batching tin nhắn giảm số lượng API calls với OpenAI.
- **Trả lời thông minh**: Sử dụng GPT-4o-mini để phân tích và trả lời chính xác, ngắn gọn.
:::

---

### 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Facebook App** với sản phẩm Messenger được kích hoạt:
   - Tạo tại [Facebook Developers](https://developers.facebook.com/).
   - Thêm **Messenger** vào danh sách sản phẩm của app.
   - Kết nối với **Facebook Page** của doanh nghiệp.
2. **OpenAI API Key**:
   - Tạo tại [OpenAI Platform](https://platform.openai.com/api-keys).
   - Chọn **gpt-4o-mini** làm model mặc định.
3. **Page Access Token** của Facebook:
   - Sử dụng để gửi tin nhắn từ chatbot.
4. **Verify Token** cho webhook:
   - Một chuỗi ngẫu nhiên (ví dụ: `my_secure_token_123`) để xác thực webhook.
:::

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n.io/workflows/11993](https://n8n.io/workflows/11993) và import vào n8n Editor.
- **Cách 2**: Copy toàn bộ JSON từ [đây](https://n8n.io/workflows/11993) và dán vào **Import Workflow** trong n8n.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow gồm **19 node** với logic phức tạp. Dưới đây là hướng dẫn chi tiết từng phần quan trọng:

##### **A. Cấu hình Webhook & Xác thực Facebook**
1. **Node "Is Token Valid?"**:
   - Điền **Verify Token** vào trường `token` (đặt trong `webhookTrigger`).
   - Ví dụ: `token: "my_secure_token_123"`.
   - **Lưu ý**: Token này phải khớp với token trong **Facebook App Dashboard** (trong phần **Webhooks**).

2. **Node "Respond with Challenge"**:
   - Nếu Facebook gửi yêu cầu xác thực, node này tự động trả về `hub.challenge` để xác nhận webhook.

3. **Node "Respond Forbidden"**:
   - Nếu token không khớp, node này trả về mã **403 Forbidden** để Facebook biết webhook không hợp lệ.

##### **B. Lọc và Batching Tin Nhắn**
1. **Node "Filter Valid Messages"**:
   - Loại bỏ tin nhắn không cần thiết như:
     - Tin nhắn của chatbot (echo messages).
     - Tin nhắn không phải text (ảnh, video).
     - Tin nhắn trống.

2. **Node "Store Message for Batching"**:
   - Lưu tin nhắn vào **Static Data** của workflow để batching.
   - **Lưu ý**: Cần chỉnh sửa code trong node này nếu muốn thay đổi logic batching (ví dụ: thời gian chờ 3s).

3. **Node "Wait 3 Seconds"**:
   - Chờ 3 giây để kết hợp tin nhắn liên tiếp của cùng một người dùng.

##### **C. Xử lý bởi AI với GPT-4o-mini**
1. **Node "Conversation Memory"**:
   - Lưu **50 tin nhắn gần nhất** của mỗi người dùng để AI nhớ lịch sử chat.
   - **Lưu ý**: Thay đổi số lượng tin nhắn lưu trong `windowSize` nếu cần.

2. **Node "OpenAI Chat Model"**:
   - Chọn **gpt-4o-mini** trong `model`.
   - Đảm bảo **OpenAI API Key** đã được cấu hình trong credential (hướng dẫn ở phần **OpenAI Credential Setup**).

3. **Node "AI Agent"**:
   - Đây là "não" của chatbot. **Thay đổi system prompt** trong node này để điều chỉnh tính cách của AI:
     - Ví dụ: Thêm `Tôn trọng khách hàng`, `Trả lời ngắn gọn`, hoặc `Khuyến khích mua hàng`.
     - **Mẫu prompt mặc định**:
       ```json
       {
         "role": "system",
         "content": "Bạn là một trợ lý hỗ trợ khách hàng chuyên nghiệp. Trả lời ngắn gọn, thân thiện và luôn nhớ lịch sử chat của khách hàng."
       }
       ```

##### **D. Gửi Trả Lời về Facebook**
1. **Node "Format Response"**:
   - Code này loại bỏ các ký tự Markdown và cắt ngắn tin nhắn nếu quá 1900 ký tự (giá trị mặc định của Facebook).
   - **Lưu ý**: Nếu muốn thay đổi giới hạn ký tự, chỉnh sửa code trong node này.

2. **Node "Send Response to User"**:
   - Sử dụng **Facebook Graph API** để gửi tin nhắn.
   - **Lưu ý**: Đảm bảo **Page Access Token** đã được cấu hình trong credential.

---

#### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Gửi tin nhắn mẫu từ Facebook Messenger đến webhook (ví dụ: `https://tên-domain.com/facebook-messenger-webhook`).
   - Kiểm tra log trong n8n để đảm bảo workflow hoạt động.

2. **Bật Active**:
   - Chuyển trạng thái workflow từ **Inactive** sang **Active**.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Kết hợp với Slack/Telegram**:
   - Thêm node **Slack/Telegram Webhook** để gửi tin nhắn của khách hàng và phản hồi AI về kênh quản lý.

2. **Lưu log hội thoại**:
   - Sử dụng node **Google Sheets** hoặc **Airtable** để ghi lại toàn bộ lịch sử chat của khách hàng.

3. **Báo cáo tự động**:
   - Thêm node **Email** hoặc **Google Drive** để gửi báo cáo hàng ngày về số lượng tin nhắn được xử lý.

4. **Cập nhật system prompt**:
   - Thử nghiệm với các prompt khác nhau để tối ưu hóa trải nghiệm khách hàng (ví dụ: thêm tính cách hài hước hoặc chuyên nghiệp).

5. **Optimize API calls**:
   - Nếu chatbot nhận nhiều tin nhắn, giảm `windowSize` trong `Conversation Memory` để giảm chi phí API.

---

### 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho doanh nghiệp muốn tự động hóa hỗ trợ khách hàng trên Facebook Messenger **không cần code**. Với **GPT-4o-mini**, chatbot không chỉ trả lời nhanh chóng mà còn **nhớ lịch sử chat**, tạo trải nghiệm cá nhân hóa. **Hãy import ngay và thử nghiệm** để tiết kiệm thời gian và nâng cao hiệu suất hỗ trợ khách hàng!

👉 **Bắt đầu ngay**: [Tải workflow từ n8n.io](https://n8n.io/workflows/11993) và cài đặt trên VPS của bạn!