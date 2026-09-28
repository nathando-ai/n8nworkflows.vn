---
title: "🤖 Tự Động Hóa Tóm Tắt Nội Dung Bằng Webhook (ApyHub) - Không Cần Code"
description: "Workflow n8n tự động nhận nội dung từ API/Webhook, tóm tắt bằng AI, trả về kết quả ngay lập tức - tiết kiệm 80% thời gian so với làm thủ công. Phù hợp cho blogger, marketer, và doanh nghiệp cần xử lý lượng nội dung lớn."
slug: "tu-dong-hoa-tom-tat-noi-dung-bang-webhook"
tags: [n8n, automation, apyhub, ai-summarizer, no-code]
keywords: [n8n workflow tự động tóm tắt, tự động hóa nội dung bằng AI, apyhub n8n, webhook tóm tắt văn bản, tự động hóa blogger]
---

# 🚀 **Tự Động Hóa Tóm Tắt Nội Dung Bằng Webhook (ApyHub) - Không Cần Code**

### **Giải pháp cho ai?**
Các sếp blogger, marketer, hoặc doanh nghiệp phải **tóm tắt hàng chục bài viết/email hàng ngày** để chia sẻ trên mạng xã hội, email marketing, hoặc báo cáo nội bộ? Hoặc đang **mất thời gian** để copy-paste nội dung dài vào các công cụ tóm tắt AI như ApyHub, rồi chờ kết quả? **Workflow này sẽ tự động hóa toàn bộ quy trình chỉ trong vài giây!**

Thay vì:
❌ Gõ tay vào ApyHub → Chờ kết quả → Copy-paste → Lặp lại hàng trăm lần.
✅ **Nhấn một nút trên API/Webhook → Kết quả tóm tắt tự động trả về** (hoặc gửi qua Slack/Email).

---
### **🎯 Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80% thời gian**: Không cần làm thủ công cho mỗi bài viết.
- **Tự động hóa liên tục 24/7**: Chạy trên VPS, không phụ thuộc vào thời gian làm việc.
- **Kết quả chính xác**: Sử dụng API ApyHub (AI tiên tiến) để tóm tắt nội dung với độ dài tùy chọn.
- **Kết nối dễ dàng**: Hoàn toàn tương thích với API, Webhook, hoặc các hệ thống khác (Slack, Telegram, CRM...).
- **Mở rộng dễ dàng**: Có thể kết nối thêm node để lưu kết quả vào Google Sheets, Notion, hoặc gửi qua Email.
:::

---
### **🔧 Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi sử dụng, các sếp cần chuẩn bị:
1. **Tài khoản ApyHub**:
   - Đăng ký tại [ApyHub](https://apyhub.ai/) và lấy **apy-token** (API Key).
   - [Hướng dẫn lấy API Key ApyHub](https://docs.apyhub.ai/docs/api-reference/authentication) (nếu cần).
2. **VPS để self-host n8n** (không dùng phiên bản miễn phí trên cloud):
   - 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%).
   - 👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172).
3. **Cấu hình Webhook** (nếu muốn gọi từ bên ngoài):
   - URL Webhook sẽ được tạo tự động khi import workflow (dạng: `https://<your-n8n-domain>/summarize-content`).
4. **Tham số tùy chọn (optional)**:
   - `summary_length`: Có thể gửi `short`, `medium`, hoặc `long` trong body JSON (ví dụ: `{"content": "Tên bài viết...", "summary_length": "medium"}`).
---

---
### **🚀 Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có **2 cách** để import workflow này:
- **Tải file JSON**:
  1. Tải workflow từ [n8n.io/workflows/4603](https://n8n.io/workflows/4603) (chọn "Download JSON").
  2. Trên n8n Editor, nhấn **Import** → Chọn file JSON vừa tải.
- **Copy/Paste JSON**:
  1. Mở n8n Editor → Tạo workflow mới.
  2. Nhấn **Import** → Chọn **Paste JSON** → Dán nội dung JSON từ [n8n.io/workflows/4603](https://n8n.io/workflows/4603) (chọn "Copy JSON").

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này gồm **4 node chính**, các sếp cần cấu hình như sau:

##### **Node 1: "Receive Content Webhook" (n8n-nodes-base.webhook)**
- **Địa chỉ Webhook**: Tự động tạo khi import (ví dụ: `https://<your-n8n-domain>/summarize-content`).
- **Phương thức HTTP**: **POST** (đã cấu hình sẵn).
- **Lưu ý**:
  - Các sếp **không cần chỉnh sửa** node này, chỉ cần lưu ý URL để gọi từ bên ngoài.
  - **Body JSON yêu cầu**:
    ```json
    {
      "content": "Nội dung cần tóm tắt (bắt buộc)",
      "summary_length": "short|medium|long" (tùy chọn)
    }
    ```
  - **Header yêu cầu**:
    - `apy-token`: Gán giá trị là **API Key của ApyHub** (lấy từ [ApyHub Dashboard](https://apyhub.ai/)).

##### **Node 2: "Start Summarization Job" (n8n-nodes-base.httpRequest)**
- **URL**: `https://api.apyhub.ai/v1/summarize` (đã cấu hình sẵn).
- **Method**: POST.
- **Headers**:
  - `apy-token`: **Sao chép từ node Webhook** (để tự động truyền API Key).
- **Body**:
  - **Raw**: Chọn `JSON`.
  - **Content**:
    ```json
    {
      "content": "{{$json.content}}",
      "summary_length": "{{$json.summary_length}}"
    }
    ```
  - **Lưu ý**: `$json.content` và `$json.summary_length` là **dynamic values** từ node Webhook.

##### **Node 3: "Get Summarization Result" (n8n-nodes-base.httpRequest)**
- **URL**: `https://api.apyhub.ai/v1/jobs/{job_id}/status` (đã cấu hình sẵn).
- **Method**: GET.
- **Headers**:
  - `apy-token`: **Sao chép từ node Webhook**.
- **Path Parameters**:
  - `{job_id}`: Lấy từ response của node **Start Summarization Job** (cần **set expression**).
    - **Cách set**:
      1. Nhấn vào **Path Parameters** → Chọn `{job_id}`.
      2. Nhấn **Expression** → Gõ:
        ```javascript
        {{ $json.job_id }}
        ```
- **Polling (Lặp lại yêu cầu)**:
  - Node này **auto-polling** (lặp lại yêu cầu) cho đến khi trạng thái `status` = `"finished"`.
  - **Lưu ý**: Nếu ApyHub trả về lỗi, các sếp cần kiểm tra **API Key** và **nội dung input**.

##### **Node 4: "Respond with Summarized Content" (n8n-nodes-base.respondToWebhook)**
- **Trả về kết quả** cho người gọi Webhook.
- **Content**:
  - **JSON Path**: `$.summarized_text` (lấy từ response của node **Get Summarization Result**).
  - **Lưu ý**: Các sếp có thể **thêm node** trước node này để lưu kết quả vào Google Sheets, Notion, hoặc gửi qua Email (xem phần **Mẹo nâng cao**).

---
#### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Gửi một request mẫu đến Webhook bằng **Postman** hoặc **cURL**:
     ```bash
     curl -X POST \
       https://<your-n8n-domain>/summarize-content \
       -H "apy-token: YOUR_APYHUB_API_KEY" \
       -H "Content-Type: application/json" \
       -d '{"content": "Nội dung dài cần tóm tắt...", "summary_length": "medium"}'
     ```
   - Kiểm tra response trong **n8n Editor** (tab **Execution**).
2. **Bật Active**:
   - Nhấn **Active** trên workflow để chạy liên tục.

---
### **✍️ Mẹo & gợi ý nâng cao**
:::info[CÁCH KẾT NỐI VỚI SLACK/TELEGRAM]
Các sếp có thể **thêm node Slack/Telegram** sau node **Respond with Summarized Content** để tự động gửi kết quả:
1. **Thêm node Slack/Telegram**:
   - Tìm node `n8n-nodes-base.slack` hoặc `n8n-nodes-base.telegram`.
   - Cấu hình:
     - **Message**: `{{ $json.summarized_text }}`.
     - **Channel**: Chọn channel cần gửi.
2. **Thêm node Email (n8n-nodes-base.email)**:
   - Cấu hình để gửi kết quả tóm tắt qua Email định kỳ (ví dụ: hàng ngày).

:::info[LƯU KẾT QUẢ VÀO GOOGLE SHEETS]
- **Thêm node Google Sheets**:
  - Tìm node `n8n-nodes-base.googleSheets`.
  - Cấu hình:
    - **Sheet Name**: Tên sheet cần lưu.
    - **Row Data**: `{{ $json }}` (để lưu toàn bộ response).
    - **Credentials**: Chọn account Google đã kết nối.

:::info[SỬ DỤNG TRONG BLOGGER/WORDPRESS]
- **Kết nối với WordPress**:
  - Sử dụng plugin **WP REST API** để gọi Webhook từ bài viết.
  - Cấu hình trong **Settings → Reading → RSS** để tự động tóm tắt bài mới.
- **Tự động tóm tắt email**:
  - Kết nối với **Gmail API** để lấy nội dung email → Gửi đến Webhook → Trả về tóm tắt.

---
### **📌 Kết luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc tóm tắt nội dung thủ công, đồng thời **tăng cường hiệu suất** với kết quả AI chính xác. **Chỉ cần 5 phút setup**, các sếp có thể tự động hóa quy trình cho **blog, email marketing, báo cáo nội bộ**, hoặc bất kỳ ứng dụng nào cần tóm tắt văn bản.

**Hành động ngay!**
1. **Đăng ký VPS** để self-host n8n (không phụ thuộc phiên bản cloud).
2. **Import workflow** và cấu hình API Key ApyHub.
3. **Test Run** và bật Active để tự động hóa ngay!

👉 **Cần hỗ trợ?** Để lại comment bên dưới hoặc liên hệ tác giả [ist00dent](https://n8n.io/workflows/4603) để tối ưu workflow!

---