---
title: "🤖 Tự Động Hóa AI Tự Do: Chạy Mô Hình AI Mở Source Hugging Face Trên n8n Với Webhook (Không Cần Code)"
description: "Workflow này giúp các sếp tự động hóa việc gọi API mô hình AI mở nguồn từ Hugging Face thông qua webhook trong n8n, tiết kiệm thời gian và tối ưu hóa quá trình tạo nội dung, tổng hợp thông tin hoặc phân tích dữ liệu bằng AI. Hoàn toàn miễn phí và không cần kỹ năng lập trình."
slug: "tieu-dong-hoa-ai-hugging-face-tren-n8n"
tags: [n8n, automation, ai, hugging-face, content-creation]
keywords: [n8n workflow ai, tự động hóa ai, hugging face api, webhook n8n, mô hình ai mở nguồn]
---

# 🚀 **Tự Động Hóa AI Tự Do: Chạy Mô Hình AI Mở Nguồn Hugging Face Trên n8n Với Webhook**

### **Nỗi Đau Của Các Sếp**
Hiện nay, việc sử dụng AI để tự động hóa tạo nội dung, tổng hợp báo cáo hoặc phân tích dữ liệu vẫn còn gặp nhiều trở ngại:
- **Phải code**: Nhiều sếp không biết lập trình hoặc không muốn tốn thời gian viết code để gọi API Hugging Face.
- **Phức tạp**: Cấu hình API và xử lý kết quả từ mô hình AI thường đòi hỏi kiến thức kỹ thuật.
- **Tốn thời gian**: Gọi API thủ công hoặc qua các công cụ khác khiến quá trình trở nên chậm chạp và dễ sai sót.

**Workflow này giải quyết tất cả!** Các sếp chỉ cần **cài đặt n8n, import workflow và kích hoạt webhook**, mô hình AI sẽ tự động xử lý yêu cầu và trả về kết quả một cách nhanh chóng và chính xác.

---
### **🎯 Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần gọi API thủ công, mọi thứ tự động hóa chỉ với một cú nhấp chuột.
- **Chính xác và ổn định**: Mô hình AI mở nguồn từ Hugging Face đảm bảo kết quả chất lượng cao.
- **Không cần code**: Thiết kế workflow hoàn toàn không cần kỹ năng lập trình.
- **Hoạt động 24/7**: Webhook cho phép gọi API bất kỳ lúc nào, ngay cả khi các sếp ngủ.
:::

---
### **🔧 Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần:
1. **Tài khoản Hugging Face**:
   - Đăng ký tại [Hugging Face](https://huggingface.co/) và lấy **API Key** từ [Settings > Access Tokens](https://huggingface.co/settings/tokens).
   - Chọn mô hình AI muốn sử dụng (ví dụ: `facebook/bart-large-cnn` cho tổng hợp bài viết, `distilbert-base-uncased` cho phân loại văn bản).
2. **n8n Self-hosted**:
   - Cài đặt n8n trên VPS để workflow chạy ổn định 24/7.
   - 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%).
   - 👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172).
3. **Tham số mô hình**:
   - **Model ID**: Tên mô hình Hugging Face (ví dụ: `facebook/bart-large-cnn`).
   - **Prompt**: Văn bản đầu vào cho mô hình AI (ví dụ: "Tóm tắt bài viết này: [text]").
   - **Max Length**: Độ dài tối đa của kết quả trả về (ví dụ: 100).
---

### **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Workflow này được thiết kế để gọi API Hugging Face thông qua **webhook**. Các sếp có thể:
- **Tải file JSON** từ [n8n.io/workflows/13809](https://n8n.io/workflows/13809) và import vào n8n Editor.
- **Copy JSON** từ link trên và dán vào **Import Workflow** trong n8n.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này sử dụng các node chính sau:
- **`n8n-nodes-base.webhook`**: Node nhận yêu cầu từ bên ngoài (ví dụ: từ Slack, Telegram hoặc một trang web).
- **`n8n-nodes-base.httpRequest`**: Node gọi API Hugging Face với tham số đã cấu hình.
- **`n8n-nodes-base.set`**: Node xử lý và truyền dữ liệu vào mô hình AI.
- **`n8n-nodes-base.respondToWebhook`**: Node trả về kết quả từ mô hình AI.

##### **Cách cấu hình chi tiết:**
1. **Webhook Node**:
   - Đặt **Path**: `/run-ai-model` (hoặc bất kỳ đường dẫn nào các sếp muốn).
   - Chọn **Method**: `POST`.
   - **Credentials**: Không cần (hoặc sử dụng OAuth nếu cần).

2. **HTTP Request Node**:
   - **URL**: `https://api-inference.huggingface.co/models/{MODEL_ID}` (thay `{MODEL_ID}` bằng tên mô hình).
   - **Headers**:
     ```
     Authorization: Bearer {HUGGING_FACE_API_KEY}
     Content-Type: application/json
     ```
   - **Body**:
     ```json
     {
       "inputs": "{prompt}"
     }
     ```
     (Thay `{prompt}` bằng biến từ Webhook Node, ví dụ: `{{ $json.body.prompt }}`).

3. **Set Node**:
   - Đặt biến `prompt` từ Webhook Node vào `inputs` của API.

4. **Respond To Webhook**:
   - Chọn **Response Type**: `JSON`.
   - **Response Data**: `{{ $json.body }}` (hoặc cấu trúc JSON tùy chỉnh).

#### **3. Kích Hoạt ⚡️**
- **Test Run**:
  - Gửi một yêu cầu mẫu đến Webhook (ví dụ: từ Postman hoặc cURL):
    ```bash
    curl -X POST https://your-n8n-domain.com/webhook/run-ai-model \
    -H "Content-Type: application/json" \
    -d '{"prompt": "Tóm tắt bài viết sau: Đây là một bài viết về tự động hóa với n8n."}'
    ```
  - Kiểm tra kết quả trả về từ mô hình AI.

- **Bật Active**:
  - Sau khi test thành công, bật **Active** cho workflow.

---
### **✍️ Mẹo & Gợi Ý Nâng Cao**
1. **Kết Nối Với Slack/Telegram**:
   - Sử dụng node `n8n-nodes-slack` hoặc `n8n-nodes-telegram` để gửi yêu cầu AI qua kênh chat và nhận kết quả tự động.

2. **Lưu Log Kết Quả**:
   - Thêm node `n8n-nodes-base.googleSheets` hoặc `n8n-nodes-base.database` để lưu lịch sử yêu cầu và kết quả AI vào bảng tính hoặc cơ sở dữ liệu.

3. **Tự Động Hóa Quá Trình Tạo Nội Dung**:
   - Kết hợp với node `n8n-nodes-base.email` để gửi kết quả tổng hợp AI qua email định kỳ (ví dụ: tổng hợp tin tức hàng ngày).

4. **Chọn Mô Hình Phù Hợp**:
   - Nếu cần **tóm tắt văn bản**, chọn mô hình `facebook/bart-large-cnn`.
   - Nếu cần **phân loại cảm xúc**, chọn mô hình `distilbert-base-uncased-finetuned-sst-2-english`.

---
### **📌 Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn tự động hóa việc sử dụng AI mà **không cần code**. Chỉ với một webhook và một cú nhấp chuột, các sếp có thể gọi bất kỳ mô hình AI mở nguồn từ Hugging Face và nhận kết quả ngay lập tức.

**Hãy áp dụng ngay và tự động hóa công việc của mình!** 🚀
Nếu có bất kỳ câu hỏi hoặc gặp khó khăn, hãy để lại comment dưới đây. Chúng tôi sẽ hỗ trợ!