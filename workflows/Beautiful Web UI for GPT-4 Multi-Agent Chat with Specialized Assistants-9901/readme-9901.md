---
title: "🤖 **Tự Động Hóa Chatbot AI Tích Hợp GPT-4 Multi-Agent Với Giao Diện Web Đẹp Mắt - Không Cần Code**"
description: "Workflow này giúp các sếp xây dựng một chatbot AI chuyên nghiệp với 4 loại trợ lý riêng biệt (Tổng quát, Cơ sở dữ liệu, Web, RAG) và giao diện web đẹp mắt, phản hồi tức thời - hoàn toàn tự động hóa, không cần viết một dòng code nào!"
slug: "tieu-dong-hoa-chatbot-gpt4-multi-agent-giao-dien-web"
tags: [n8n, automation, ai-chatbot, gpt-4, no-code, langchain, self-hosted]
keywords: [n8n workflow chatbot, tự động hóa chatbot AI, giao diện web cho AI, GPT-4 multi-agent, LangChain với n8n, không cần code]
---

# 🚀 **Chatbot AI GPT-4 Multi-Agent Với Giao Diện Web Đẹp Mắt - Cách Tạo Trong 10 Phút**

Hãy tưởng tượng một chatbot AI không chỉ thông minh mà còn **có 4 trợ lý riêng biệt** (tổng quát, cơ sở dữ liệu, web, và RAG) để xử lý các yêu cầu phức tạp của khách hàng, đồng thời **hiển thị trên một giao diện web đẹp mắt, phản hồi tức thời** mà không cần viết một dòng code nào! Đó chính là **Beautiful Web UI for GPT-4 Multi-Agent Chat** - một workflow n8n **miễn phí** do Growth Engineer Hugo thiết kế, giúp các sếp **tự động hóa hoàn toàn** quá trình tương tác với khách hàng thông qua AI.

---
## 🎯 **Kết quả các sếp nhận được**
:::tip[**LỢI ÍCH CỐT LÕI**]
- **Tiết kiệm thời gian**: Không cần thiết kế giao diện web hay viết code backend - chỉ cần import workflow và chạy!
- **Trải nghiệm khách hàng chuyên nghiệp**: Giao diện web đẹp mắt, phản hồi tức thời, hỗ trợ dark/light mode và responsive trên mobile.
- **4 trợ lý AI riêng biệt**:
  - **Trợ lý Tổng quát** (General Agent): Xử lý các câu hỏi phổ biến.
  - **Trợ lý Cơ sở dữ liệu** (Database Agent): Trích xuất và phân tích dữ liệu.
  - **Trợ lý Web** (Web Agent): Tìm kiếm và tổng hợp thông tin từ internet.
  - **Trợ lý RAG** (Retrieval-Augmented Generation): Trả lời dựa trên kiến thức từ các tài liệu riêng.
- **Hoạt động 24/7**: Workflow chạy tự động trên VPS, không cần can thiệp thủ công.
- **Tích hợp GPT-4.1-mini**: Dùng mô hình AI tiên tiến của OpenAI với chi phí thấp.
:::

---
## 🔧 **Yêu cầu cần thiết**
:::info[**CHUẨN BỊ**]
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản OpenAI**:
   - API Key từ [OpenAI](https://platform.openai.com/account/api-keys) (đăng ký miễn phí).
   - **Lưu ý**: Workflow sử dụng mô hình `gpt-4.1-mini` (rẻ hơn `gpt-4` nhưng vẫn mạnh mẽ).
2. **VPS để self-host n8n**:
   - 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%).
   - 👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (đủ để chạy workflow ổn định).
3. **Cài đặt n8n trên VPS**:
   - Hướng dẫn cài đặt: [Tutorial cài n8n trên Ubuntu](https://docs.n8n.io/hosting/installation/installation-on-ubuntu/).
4. **Cấu hình CORS (nếu cần)**:
   - Nếu chạy trên VPS khác domain, cần mở rộng CORS cho webhook.
:::

---
## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
Workflow được chia thành **2 phần chính**:
- **Workflow 1**: Hiển thị giao diện web (3 nodes).
- **Workflow 2**: Xử lý yêu cầu từ khách hàng (5+ nodes).

#### **Cách import**:
1. **Tải workflow từ n8n.io**:
   - Truy cập [link gốc](https://n8n.io/workflows/9901) và nhấn **"Import"** (hoặc tải file JSON).
2. **Import vào n8n Editor**:
   - Mở n8n trên VPS, nhấn **"Import"** và dán JSON từ file.
   - **Lưu ý**: Nếu import từ file JSON, chọn **"Import from file"** và tải file đã tải từ n8n.io.

#### **Cách copy/paste JSON**:
1. Tải file JSON từ [đây](https://n8n.io/workflows/9901) (nhấn **"Export"**).
2. Mở file JSON và copy toàn bộ nội dung.
3. Trong n8n Editor, nhấn **"Import"** → **"Import from JSON"** và dán nội dung.

---

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này **không hoạt động ngay** sau khi import - các sếp cần cấu hình các phần sau:

#### **A. Cấu hình OpenAI API Key**
1. Trong n8n, đi đến **"Credentials"** (phía trên bên trái).
2. Nhấn **"Add"** → **"OpenAI API"**.
3. Điền:
   - **Name**: `openAiApi` (phải trùng với credential trong workflow).
   - **API Key**: Dán API Key từ OpenAI.
   - **Organization ID** (nếu có).
   - **Model**: `gpt-4.1-mini` (đã được thiết lập trong workflow).

#### **B. Cấu hình Webhook**
Workflow sử dụng **2 webhook**:
1. **Webhook GET** (hiển thị giao diện):
   - Path: `/b6f698e9-c16c-4273-8af2-20a958f691c1` (không cần thay đổi).
   - **Lưu ý**: Nếu muốn thay đổi path, phải chỉnh trong **Code Node** (Workflow 1).
2. **Webhook POST** (xử lý yêu cầu):
   - Path: `/webhook-endpoint` (được sử dụng trong **Workflow 2**).
   - **Lưu ý**: Trong file `main.js` (nằm trong **Code Node** của Workflow 1), dòng **847** cần thay đổi URL webhook:
     ```javascript
     const WEBHOOK_URL = '/webhook/webhook-endpoint'; // Đảm bảo trùng với path trong Workflow 2
     ```

#### **C. Cấu hình Switch Node**
- **Switch Node** (`Switch`) trong Workflow 2 **phân loại yêu cầu** sang các trợ lý AI khác nhau dựa trên `{{ $json.body.agent_type }}`.
- Các giá trị có thể:
  - `general` → Trợ lý Tổng quát.
  - `database` → Trợ lý Cơ sở dữ liệu.
  - `web` → Trợ lý Web.
  - `rag` → Trợ lý RAG.
- **Lưu ý**: Nếu muốn thêm loại trợ lý mới, cần chỉnh **Switch Node** và thêm **AI Agent** tương ứng.

#### **D. Cấu hình Code Node (Format Response)**
- Các **Code Node** (`Format Response - Code`, `Format Response - Code1`, ...) **định dạng phản hồi** từ AI trước khi trả về cho khách hàng.
- **Lưu ý**: Nếu muốn thay đổi cách định dạng, mở **Code Node** và chỉnh mã JavaScript:
  ```javascript
  const webhookData = $('Webhook').first().json.body;
  const aiResponse = $input.first().json;

  return [{
    json: {
      response: aiResponse.output || aiResponse.text || aiResponse.response,
      agent_type: webhookData.agent_type
    }
  }];
  ```

#### **E. Kích hoạt Workflow**
1. **Test Run**:
   - Chạy **Workflow 1** (hiển thị giao diện) và mở trong trình duyệt:
     ```
     http://[IP_VPS]:5678/b6f698e9-c16c-4273-8af2-20a958f691c1
     ```
   - Chạy **Workflow 2** (xử lý yêu cầu) và gửi request POST đến:
     ```
     http://[IP_VPS]:5678/webhook-endpoint
     ```
   - **Dữ liệu mẫu** để test:
     ```json
     {
       "agent_type": "general",
       "message": "Giúp tôi giải thích cách tự động hóa với n8n?"
     }
     ```
2. **Bật Active**:
   - Sau khi test thành công, nhấn **"Active"** trên cả 2 workflow.

---

### **3. Cấu hình Reverse Proxy (Nếu cần)**
Nếu muốn chạy trên domain riêng (ví dụ: `chatbot.thesếp.com`), cần cấu hình **Nginx** hoặc **Caddy**:
```nginx
server {
    listen 80;
    server_name chatbot.thesếp.com;

    location / {
        proxy_pass http://localhost:5678;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
    }

    location /webhook-endpoint {
        proxy_pass http://localhost:5678/webhook-endpoint;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
    }
}
```
Sau đó restart Nginx:
```bash
sudo systemctl restart nginx
```

---

## ✍️ **Mẹo & gợi ý nâng cao**
:::info[**CÁCH TIẾP CẬN THÊM**]
1. **Tích hợp Slack/Telegram**:
   - Sử dụng **Slack Node** hoặc **Telegram Bot Node** để nhận yêu cầu từ chatbot và chuyển sang n8n.
   - **Cách làm**:
     - Tạo **Webhook Slack** (Settings → Custom Integrations → Incoming Webhooks).
     - Sử dụng **Webhook Node** trong n8n để nhận dữ liệu từ Slack và chuyển sang **Switch Node**.
2. **Lưu log phản hồi**:
   - Thêm **Google Sheets Node** hoặc **Database Node** để lưu tất cả lịch sử tương tác.
   - **Cách làm**:
     - Sau **Respond to Webhook**, thêm **Google Sheets Node** để ghi dữ liệu vào sheet.
3. **Gửi báo cáo định kỳ**:
   - Sử dụng **Set Interval Node** để chạy định kỳ (ví dụ: hàng ngày) và gửi báo cáo qua email.
   - **Cách làm**:
     - Tạo workflow mới với **Set Interval Node** (chạy hàng ngày).
     - Sử dụng **Google Sheets Node** để lấy dữ liệu và **Email Node** để gửi báo cáo.
4. **Cập nhật kiến thức cho Trợ lý RAG**:
   - Nếu sử dụng **Trợ lý RAG**, cần cung cấp tài liệu để AI học hỏi.
   - **Cách làm**:
     - Thêm **File System Node** để đọc tài liệu từ local hoặc cloud.
     - Sử dụng **LangChain Node** để xử lý và lưu trữ kiến thức.
5. **Thay đổi giao diện**:
   - Mở file `main.js` trong **Code Node** (Workflow 1) và chỉnh sửa CSS/JS để thay đổi giao diện.
   - **Lưu ý**: File này rất dài, các sếp có thể tham khảo [n8n AI Agent Interface Template](https://n8n.io/workflows/9901) để hiểu cấu trúc.
:::

---

## 📌 **Kết luận**
Workflow **Beautiful Web UI for GPT-4 Multi-Agent Chat** là **giải pháp hoàn hảo** cho các sếp muốn xây dựng một **chatbot AI chuyên nghiệp, tự động hóa hoàn toàn** mà không cần viết code. Với **4 trợ lý riêng biệt** và **giao diện web đẹp mắt**, nó giúp cải thiện trải nghiệm khách hàng và tiết kiệm thời gian cho đội ngũ hỗ trợ.

**Hành động ngay!**
1. **Đăng ký VPS** (nếu chưa có) và cài đặt n8n.
2. **Import workflow** và cấu hình OpenAI API Key.
3. **Test và bật Active** cả 2 workflow.
4. **Tích hợp với Slack/Telegram** hoặc **lưu log** để nâng cao tính năng.

👉 **Bắt đầu tự động hóa chatbot AI của mình ngay hôm nay!** 🚀

---
:::note[**LƯU Ý CUỐI CÙNG**]
- Workflow này **miễn phí** và **open-source**, nhưng cần **VPS để self-host**.
- Nếu gặp vấn đề, tham khảo [forum n8n](https://community.n8n.io/) hoặc liên hệ Hugo (tác giả) qua [GitHub](https://github.com/hugolabs).
- Để tối ưu chi phí, các sếp có thể **sử dụng mô hình `gpt-3.5-turbo`** thay vì `gpt-4.1-mini` (chỉnh trong **OpenAI Node**).
:::

---
**Chúc các sếp thành công với dự án tự động hóa AI của mình!** 🤖✨