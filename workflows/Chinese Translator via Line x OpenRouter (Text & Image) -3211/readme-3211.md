---
title: "🤖 **Tự Động Hóa Dịch Văn Bản & Hình Ảnh Tiếng Trung Qua Line + OpenRouter (AI Miễn Phí)**"
description: "Workflow tự động hóa dịch văn bản và hình ảnh từ tiếng Việt sang tiếng Trung qua Line Messenger với OpenRouter.ai (mô hình AI miễn phí). Giúp doanh nghiệp và cá nhân tiết kiệm thời gian, cải thiện trải nghiệm khách hàng 24/7."
slug: "tich-hop-line-openrouter-dich-van-ban-hinh-anh"
tags: [n8n, automation, ai, line-messenger, openrouter, dịch thuật tự động]
keywords: [n8n workflow dịch thuật, tự động hóa dịch tiếng Trung qua Line, OpenRouter AI miễn phí, dịch văn bản hình ảnh tự động, tự động hóa chatbot Line]
---

# 🚀 **Dịch Văn Bản & Hình Ảnh Tiếng Trung Tự Động Qua Line + OpenRouter (AI Miễn Phí)**

### **Giới thiệu**
Các sếp đang gặp khó khăn khi phải dịch văn bản hoặc hình ảnh từ tiếng Việt sang tiếng Trung cho khách hàng? Hay phải trả tiền cho dịch vụ dịch thuật truyền thống? **Workflow này giải quyết vấn đề đó bằng cách tự động hóa toàn bộ quy trình chỉ với một tin nhắn trên Line!**

Dùng **OpenRouter.ai** (mô hình AI miễn phí như Qwen-2.5-72B) kết hợp với **Line Messenger**, workflow này sẽ:
- **Dịch văn bản** từ tiếng Việt sang tiếng Trung.
- **Dịch hình ảnh** (nhận diện và mô tả) bằng AI.
- **Trả lời tự động** ngay lập tức, không cần can thiệp thủ công.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian**: Không cần dịch thủ công, trả lời khách hàng ngay lập tức.
✅ **Chính xác cao**: Sử dụng mô hình AI Qwen-2.5-72B (OpenRouter) với độ chính xác gần như người.
✅ **Hoạt động 24/7**: Khách hàng có thể gửi tin nhắn bất kỳ lúc nào, workflow tự động xử lý.
✅ **Hỗ trợ cả văn bản và hình ảnh**: Dịch cả text và mô tả hình ảnh một cách tự động.
✅ **Miễn phí (hoặc chi phí thấp)**: Sử dụng mô hình AI miễn phí của OpenRouter.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Line Developer**:
   - Đăng ký tại [Line Developers](https://developers.line.biz/) để lấy **Channel Secret** và **Channel Access Token**.
   - **Cần thiết**: Cài đặt **Webhook** từ workflow vào Line Manager (hướng dẫn chi tiết dưới phần "Cách import").
2. **API Key OpenRouter**:
   - Đăng ký tại [OpenRouter.ai](https://openrouter.ai/) để lấy **API Key** (miễn phí cho mô hình Qwen-2.5-72B).
3. **Tài khoản n8n**:
   - Cài đặt n8n trên máy chủ hoặc VPS (self-hosted) để chạy workflow 24/7.

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/3211](https://n8n.io/workflows/3211) hoặc copy JSON từ trang này.
- Mở **n8n Editor** → Nhấn **Import Workflow** → Chọn file JSON hoặc dán JSON vào ô nhập liệu.
- **Không quên**: Xóa phần `"test"` trong URL Webhook trước khi đi sản xuất (hướng dẫn chi tiết dưới đây).

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
##### **A. Cấu hình Webhook Line**
- **Node**: `Line Webhook` (type: `webhook`)
  - **Bước 1**: Copy **URL Webhook** từ node này (ví dụ: `https://tên-máy-chủ-n8n.com/webhook/cn`).
  - **Bước 2**: Đăng nhập vào [Line Manager](https://manager.line.biz/) → Chọn **Messaging API** → **Add Channel** → Nhập URL Webhook.
  - **Bước 3**: Lưu **Channel Secret** và **Channel Access Token** để sử dụng trong các node sau.
  - **Lưu ý**: Xóa phần `test` trong URL (nếu có) trước khi đi sản xuất.

##### **B. Cấu hình Line Token (Loading Animation)**
- **Node**: `Line Loading Animation` (type: `httpRequest`)
  - **Tham số cần điền**:
    - **URL**: `https://notify-api.line.me/api/notify`
    - **Headers**:
      - `Authorization: Bearer <Channel Access Token>`
      - `Content-Type: application/x-www-form-urlencoded`
    - **Body**:
      ```json
      {
        "message": "Đang xử lý tin nhắn của bạn...",
        "stickerPackageId": 1,
        "stickerId": 100
      }
      ```
  - **Mục đích**: Hiển thị animation loading cho người dùng khi workflow đang xử lý.

##### **C. Cấu hình OpenRouter (Dịch Văn Bản & Hình Ảnh)**
- **Node**: `OpenRouter : qwen/qwen2.5-vl-72b-instruct:free` (dịch hình ảnh) và `OpenRouter: qwen-2.5-72b-instruct:free` (dịch văn bản)
  - **Tham số chung**:
    - **URL**: `https://openrouter.ai/api/v1/chat/completions`
    - **Headers**:
      - `Authorization: Bearer <API Key OpenRouter>`
      - `Content-Type: application/json`
    - **Body (dịch văn bản)**:
      ```json
      {
        "messages": [
          {"role": "user", "content": "{{$json.text}}"}
        ],
        "model": "qwen-2.5-72b-instruct:free",
        "max_tokens": 1024
      }
      ```
    - **Body (dịch hình ảnh)**:
      ```json
      {
        "messages": [
          {"role": "user", "content": ["<image_base64>", "Dịch hình ảnh này sang tiếng Trung"]}
        ],
        "model": "qwen/qwen2.5-vl-72b-instruct:free",
        "max_tokens": 1024
      }
      ```
  - **Lưu ý**:
    - Đối với **hình ảnh**, node `Extract from File` sẽ chuyển dữ liệu từ Line sang định dạng base64 trước khi gửi đến OpenRouter.
    - **Không hỗ trợ**: Tin nhắn âm thanh hoặc file khác (node `Line Reply (Not Supported 1/2)` sẽ trả lời tự động).

##### **D. Cấu hình Trả Lời Line**
- **Node**: `Line Reply (Text)`, `Line Reply (Image)`, `Line Reply (Not Supported 1/2)`
  - **Tham số chung**:
    - **URL**: `https://api.line.me/v2/bot/message/push`
    - **Headers**:
      - `Authorization: Bearer <Channel Access Token>`
      - `Content-Type: application/json`
    - **Body (dịch văn bản)**:
      ```json
      {
        "to": "{{$json.replyToken}}",
        "messages": [
          {
            "type": "text",
            "text": "{{$json.output.text}}"
          }
        ]
      }
      ```
    - **Body (dịch hình ảnh)**:
      ```json
      {
        "to": "{{$json.replyToken}}",
        "messages": [
          {
            "type": "image",
            "originalContentUrl": "{{$json.output.imageUrl}}",
            "previewImageUrl": "{{$json.output.imageUrl}}"
          }
        ]
      }
      ```
    - **Body (không hỗ trợ)**:
      ```json
      {
        "to": "{{$json.replyToken}}",
        "messages": [
          {
            "type": "text",
            "text": "Loại tin nhắn này chưa được hỗ trợ!"
          }
        ]
      }
      ```

---

#### **3. Kích hoạt ⚡️**
- **Test Run**:
  - Gửi tin nhắn từ **@405jtfqs** (tài khoản test của Line) để kiểm tra workflow.
  - Kiểm tra các node:
    - `Switch` để phân loại tin nhắn (text/hình ảnh/âm thanh).
    - `Extract from File` để chuyển hình ảnh thành base64.
    - `OpenRouter` để gọi API dịch thuật.
    - `Line Reply` để trả lời tự động.
- **Bật Active**:
  - Sau khi test thành công, nhấn **Active** để workflow chạy liên tục.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Kết hợp với Slack/Telegram**:
   - Sử dụng node `webhook` để nhận tin nhắn từ Slack/Telegram và chuyển sang Line.
2. **Lưu log hoạt động**:
   - Thêm node `stickyNote` hoặc `httpRequest` để ghi log vào Google Sheets/Notion.
3. **Gửi báo cáo định kỳ**:
   - Sử dụng node `schedule` để gửi báo cáo tổng hợp dịch thuật hàng ngày qua email.
4. **Cải thiện mô hình AI**:
   - Thay đổi mô hình OpenRouter (ví dụ: `deepseek-llm-7b-instruct`) nếu cần độ chính xác cao hơn.

---

### 📌 **Kết luận**
Workflow này giúp các sếp **tự động hóa dịch thuật tiếng Trung qua Line một cách hoàn toàn miễn phí (hoặc chi phí thấp)**. Không cần viết code, chỉ cần cấu hình vài bước đơn giản là có thể trả lời khách hàng 24/7 với độ chính xác cao.

**Hãy áp dụng ngay và tiết kiệm thời gian cho đội ngũ dịch thuật của mình!** 🚀

---
**🔗 [Tải workflow nguyên bản](https://n8n.io/workflows/3211)**
**📌 [Hướng dẫn chi tiết Line Developer](https://developers.line.biz/en/docs/messaging-api/receiving-messages/)**
**🤖 [OpenRouter Docs](https://openrouter.ai/docs/quickstart)**