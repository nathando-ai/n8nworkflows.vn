---
title: "🤖 Tự Động Hóa Chat AI Gemini Trên Server Cục Bộ Với SSH - Không Cần Code"
description: "Hướng dẫn chi tiết cách kết nối Gemini AI với CLI trên server cục bộ qua SSH trong n8n, giúp các sếp tự động hóa chatbot AI cá nhân hóa, truy cập file nội bộ và tối ưu hóa công việc 24/7. Đặc biệt phù hợp cho doanh nghiệp tự host n8n."
slug: "tieu-dong-hoa-chat-gemini-ssh-n8n"
tags: [n8n, automation, ai-chatbot, ssh, google-gemini, self-hosted]
keywords: [n8n workflow gemini, tự động hóa chat ai, gemini cli ssh, chatbot cá nhân hóa, tự host n8n]
---

# 🚀 **Tự Động Hóa Chat AI Gemini Trên Server Cục Bộ Với SSH - Không Cần Code**

### **Giải pháp cho các sếp muốn:**
- **Truy cập Gemini AI từ terminal** trên server cục bộ mà không cần UI web.
- **Tự động hóa chatbot AI** để hỗ trợ khách hàng, phân tích dữ liệu hoặc xử lý công việc nội bộ.
- **Truy cập file nội bộ** mà chỉ Gemini có thể đọc (ví dụ: dữ liệu doanh nghiệp, script Python, hoặc log server).
- **Tiết kiệm chi phí** so với các giải pháp cloud như Google Vertex AI.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động ổn định 24/7, các sếp nên cài n8n trên **VPS riêng** (Self-hosted) với SSH truy cập.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Chat AI cá nhân hóa** trên server cục bộ, không phụ thuộc vào internet.
✅ **Truy cập file nội bộ** mà chỉ Gemini có thể đọc (ví dụ: script Python, log doanh nghiệp).
✅ **Tự động hóa công việc** như phân tích dữ liệu, hỗ trợ khách hàng, hoặc xử lý ticket qua CLI.
✅ **Tiết kiệm chi phí** so với các giải pháp cloud như Google Vertex AI.
✅ **Hoạt động liên tục** 24/7, không cần restart.
:::

---

## 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **n8n Self-hosted** (không dùng phiên bản cloud).
2. **NodeJS >= 20.x** cài đặt trên máy chủ (host).
3. **Gemini CLI** được cài đặt:
   ```bash
   npm install -g @google/gemini-cli
   ```
4. **SSH Access** từ n8n đến máy chủ để thực thi lệnh.
5. **Google Account** để kết nối với Gemini AI.
6. **Workflow phụ (Sub-workflow)** sẽ được tách riêng sau.

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
- **Tải workflow gốc** từ [đây](https://n8n.io/workflows/11843).
- **Import vào n8n Editor**:
  - Nhấn **Import** → Chọn file JSON đã tải.
  - Hoặc **copy/paste** JSON từ file vào n8n Editor.

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
#### **Bước 1: Tách Sub-workflow**
Workflow này gồm **2 phần**:
- **Phần chính** (chat trigger + AI agent).
- **Sub-workflow** (thực thi lệnh Gemini CLI qua SSH).

**Cách thực hiện:**
1. Trong n8n Editor, **chọn tất cả các node** của sub-workflow (từ `When Executed by Another Workflow` đến `Execute a command`).
2. Nhấn **Save as New Workflow** và đặt tên (ví dụ: **"Gemini CLI Tool"**).
3. **Lưu workflow mới** và **đóng lại**.

#### **Bước 2: Kết nối Sub-workflow**
- Trong node **"Call 'Gemini CLI'"**, chọn **workflow mới** vừa tạo ở bước trên.

#### **Bước 3: Cấu hình SSH**
- Mở node **"Execute a command"** trong sub-workflow.
- **Điền thông tin SSH**:
  - **Host**: IP hoặc domain của máy chủ.
  - **Port**: Cổng SSH (thường là `22`).
  - **Username**: Tên người dùng SSH.
  - **Private Key**: Nếu sử dụng key SSH, paste nội dung từ file `~/.ssh/id_rsa` (hoặc tương tự).
  - **Command**: Để trống (n8n sẽ truyền lệnh từ sub-workflow).

#### **Bước 4: Cấu hình Gemini AI**
- Mở node **"Google Gemini Chat Model"**.
- **Điền API Key**:
  - Tạo **Google Cloud Project** và bật **Generative AI API**.
  - Tạo **Service Account** và copy **JSON Key**.
  - Paste vào **Authentication** trong node.

#### **Bước 5: Cấu hình AI Agent**
- Mở node **"AI Agent"**.
- **Customize System Prompt** (ví dụ):
  ```plaintext
  Bạn là một trợ lý AI chuyên nghiệp. Khi được yêu cầu, hãy sử dụng công cụ "Gemini CLI" để truy cập file nội bộ hoặc xử lý dữ liệu. Không sử dụng công cụ này cho các câu hỏi đơn giản.
  ```
- **Thêm Tool** (nếu cần):
  - Nếu muốn thêm công cụ khác (ví dụ: Google Search), thêm node `toolWorkflow` tương tự.

#### **Bước 6: Test & Bật Workflow**
1. **Test Run** với dữ liệu mẫu:
   - Gửi một câu hỏi đơn giản như `"Hãy cho tôi biết doanh thu tháng trước"`.
   - Kiểm tra nếu Gemini trả lời chính xác và có truy cập file nội bộ (nếu cấu hình đúng).
2. **Bật Active** workflow.

---

## ✍️ **Mẹo & gợi ý nâng cao**
### **1. Tích hợp với Slack/Telegram**
- Sử dụng **webhook** từ Slack/Telegram để gửi tin nhắn vào workflow.
- Cấu hình node **"When chat message received"** để nhận dữ liệu từ webhook.

### **2. Lưu log chat**
- Thêm node **Google Sheets** hoặc **Airtable** để lưu lịch sử chat.
- Cấu hình node **"Edit Fields"** để thêm dữ liệu vào sheet.

### **3. Gửi báo cáo định kỳ**
- Sử dụng **n8n Scheduler** để chạy workflow hàng ngày và gửi báo cáo qua email (node **Email**).

### **4. Cải thiện System Prompt**
- Để AI Agent **hiểu rõ hơn** về công việc của doanh nghiệp, cập nhật System Prompt với:
  - Danh sách file nội bộ AI có quyền truy cập.
  - Quy tắc sử dụng công cụ Gemini CLI.

---

## 📌 **Kết luận**
Workflow này giúp các sếp **tự động hóa chat AI Gemini trên server cục bộ**, không cần code và không phụ thuộc vào internet. Đặc biệt phù hợp cho:
- **Doanh nghiệp** muốn cá nhân hóa chatbot AI với dữ liệu nội bộ.
- **DevOps/Tech Lead** muốn tối ưu hóa công việc CLI.
- **Marketing/Sales** muốn hỗ trợ khách hàng 24/7 mà không tốn chi phí cloud cao.

**Hành động ngay!**
1. **Tải workflow** và **cấu hình SSH**.
2. **Test với dữ liệu mẫu**.
3. **Bật Active** và bắt đầu tự động hóa!

---
**Có thắc mắc?** Liên hệ với **Alex** qua [elitiv.com](https://www.elitiv.com) để hỗ trợ chi tiết!