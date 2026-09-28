---
title: "🚀 Tự Động Hoá Tạo Báo Giá Chuyên Nghiệp Với AI & Google Docs (Không Cần Code)"
description: "Workflow này tự động chuyển đổi các thông tin cơ bản về báo giá thành tài liệu chuyên nghiệp, định dạng sẵn trên Google Docs, tiết kiệm thời gian lên tới 80% cho các team bán hàng và marketing. Sử dụng AI Claude 3.5 và OpenAI để tối ưu nội dung, kết hợp với Google Docs Template để đảm bảo tính chuyên nghiệp."
slug: "tu-dong-hoa-tao-bao-gia-chuyen-nghiep-ai-google-docs"
tags: [n8n, automation, no-code, ai-chatbot, google-docs, proposal-generator]
keywords: [tự động hóa báo giá, tạo báo giá chuyên nghiệp, n8n workflow, ai viết báo giá, google docs template, Claude 3.5, OpenAI]
---

# 🚀 **Tự Động Hoá Tạo Báo Giá Chuyên Nghiệp Với AI & Google Docs (Không Cần Code)**

## **📌 Nỗi Đau Của Các Sếp: Tạo Báo Giá Thường Làm Mất Thời Gian & Khó Đảm Bảo Chất Lượng**
Các sếp và team bán hàng thường phải:
- **Viết lại từ đầu** mỗi báo giá, mất từ 30 phút đến 2 giờ cho mỗi khách hàng.
- **Sao chép template** và thay đổi nội dung thủ công, dễ gây lỗi và mất thời gian.
- **Không đảm bảo tính chuyên nghiệp** vì nội dung không được tối ưu về logic và flow.
- **Không theo kịp tốc độ** khi phải xử lý nhiều yêu cầu cùng lúc.

**Workflow này giải quyết tất cả đó!** Với sự hỗ trợ của **AI Claude 3.5 (OpenRouter)** và **OpenAI**, nó tự động:
✅ **Viết nội dung chi tiết** từ các thông tin cơ bản.
✅ **Tối ưu lại** để nội dung trở nên rõ ràng, chuyên nghiệp và hấp dẫn.
✅ **Áp dụng template Google Docs** để đảm bảo định dạng nhất quán.
✅ **Tự động cập nhật** báo giá mới vào Google Drive.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để tránh giới hạn của phiên bản cloud.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian lên tới 80%** so với viết thủ công.
- **Nội dung chuyên nghiệp** do AI tối ưu, không cần chỉnh sửa nhiều.
- **Định dạng nhất quán** với template Google Docs sẵn có.
- **Hoạt động liên tục** 24/7, không phụ thuộc vào nhân viên.
- **Dễ dàng mở rộng** cho nhiều khách hàng khác nhau.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
✔ **Tài khoản OpenRouter** (để sử dụng mô hình Claude 3.5).
✔ **Tài khoản Google Drive & Google Docs** (để lưu template và báo giá).
✔ **API Key OpenAI** (để sử dụng mô hình AI viết nội dung).
✔ **Template Google Docs** (có sẵn các biến như `{{client_name}}`, `{{project_description}}`, `{{price}}`,...).
✔ **Credentials OAuth2** cho Google Drive và Google Docs (cài đặt trong n8n).

---
:::note[LƯU Ý QUAN TRỌNG]
- **Template Google Docs** phải có **các biến** (chẳng hạn: `{{client_name}}`, `{{service}}`, `{{deadline}}`,...) để workflow có thể thay thế nội dung tự động.
- **Mô hình Claude 3.5 (OpenRouter)** được sử dụng để **tối ưu lại** nội dung, trong khi **OpenAI** được dùng để viết nội dung ban đầu.
:::

---

## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
Các sếp có thể import workflow từ **file JSON** hoặc **copy/paste JSON** vào **n8n Editor**:
1. Truy cập [n8n.io](https://n8n.io/) và mở **n8n Editor**.
2. Nhấp vào **"Import"** và chọn file JSON (hoặc paste JSON).
3. Chọn **"Create Workflow"** để bắt đầu.

🔗 [Tải workflow JSON từ nguồn gốc](https://n8n.io/workflows/10856) (nếu cần).

---

### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**

#### **🔹 Node "When clicking ‘Execute workflow’" (Manual Trigger)**
- **Chức năng**: Khởi động workflow khi nhấn nút.
- **Lưu ý**: Không cần chỉnh sửa gì, chỉ cần nhấn **"Execute"** khi cần chạy.

#### **🔹 Node "OpenRouter Chat Model" (Claude 3.5)**
- **Tham số cần thiết**:
  - **Credentials**: Chọn `openRouterApi` (đã cấu hình trước).
  - **Model**: Đã mặc định là `anthropic/claude-3.5-sonnet`.
  - **Prompt**: Workflow tự động lấy dữ liệu từ **Manual Input** (node sau).
- **Lưu ý**:
  - Đảm bảo **API Key OpenRouter** được cập nhật trong **Credentials**.
  - Nếu gặp lỗi, kiểm tra **quota API** của OpenRouter.

#### **🔹 Node "Set proposal values" (Set)**
- **Tham số cần thiết**:
  - **Input Data**: Các biến từ **Manual Input** (ví dụ: `client_name`, `project_description`, `price`).
  - **Output**: Workflow sẽ sử dụng dữ liệu này để viết nội dung.
- **Lưu ý**:
  - Đảm bảo **tên biến trong template Google Docs** khớp với dữ liệu input (ví dụ: `{{client_name}}` ↔ `client_name`).

#### **🔹 Node "Rewrite proposal" (Chain LLM)**
- **Tham số cần thiết**:
  - **Model**: Đã mặc định là **Claude 3.5 (OpenRouter)**.
  - **Prompt**: Workflow tự động lấy từ **Set proposal values**.
- **Lưu ý**:
  - AI sẽ **tối ưu lại** nội dung để rõ ràng và chuyên nghiệp hơn.

#### **🔹 Node "Create proposal" (OpenAI)**
- **Tham số cần thiết**:
  - **Credentials**: Chọn `openAiApi`.
  - **Model**: Đã mặc định là mô hình OpenAI (có thể thay đổi nếu cần).
- **Lưu ý**:
  - Nếu muốn thay đổi mô hình, cập nhật trong **keyParameters**.

#### **🔹 Node "Update proposal" (Google Docs)**
- **Tham số cần thiết**:
  - **Credentials**: Chọn `googleDocsOAuth2Api`.
  - **Operation**: Đã mặc định là `update`.
  - **File ID**: Phải là **ID của template Google Docs** (có thể lấy từ URL: `https://docs.google.com/document/d/[FILE_ID]/edit`).
- **Lưu ý**:
  - **Template Google Docs** phải có **các biến** (ví dụ: `{{client_name}}`, `{{service}}`,...).
  - Nếu không có **File ID**, các sếp phải **tạo một bản sao template** và lấy ID mới.

#### **🔹 Node "Google Drive" (Copy File)**
- **Tham số cần thiết**:
  - **Credentials**: Chọn `googleDriveOAuth2Api`.
  - **Operation**: Đã mặc định là `copy`.
  - **File ID**: Phải là **ID của template Google Docs**.
- **Lưu ý**:
  - Workflow sẽ **sao chép template** và **cập nhật nội dung** vào file mới.

---

### **3. Kích Hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Nhập các thông tin cơ bản (ví dụ: `client_name = "ABC Corp"`, `project_description = "Tự động hóa quy trình bán hàng"`).
   - Nhấn **"Execute"** và kiểm tra kết quả.
2. **Bật Active Workflow**:
   - Sau khi test thành công, nhấn **"Active"** để workflow hoạt động tự động.

---
## ✍️ **Mẹo & Gợi Ý Nâng Cao**

### **🔹 Kết Nối Với Slack/Telegram**
- Thêm **node Slack/Telegram Webhook** sau **"Update proposal"** để thông báo khi báo giá hoàn thành.
- Cài đặt:
  ```json
  {
    "name": "Notify Slack",
    "type": "slackWebhook",
    "credentials": ["slackWebhookApi"],
    "keyParameters": {
      "text": "📄 Báo giá mới đã hoàn thành cho {{client_name}}!"
    }
  }
  ```

### **🔹 Lưu Log Tất Cả Các Báo Giá**
- Thêm **node Google Sheets** để ghi lại tất cả các báo giá đã tạo.
- Cài đặt:
  ```json
  {
    "name": "Log to Google Sheets",
    "type": "googleSheets",
    "credentials": ["googleSheetsOAuth2Api"],
    "keyParameters": {
      "operation": "createRow",
      "sheetName": "Báo giá",
      "data": {
        "Client": "{{client_name}}",
        "Project": "{{project_description}}",
        "Date": "{{$node["Set proposal values"].json["$date"]}}"
      }
    }
  }
  ```

### **🔹 Gửi Báo Giá Định Kỳ**
- Sử dụng **node Schedule** để tự động gửi báo giá cho khách hàng định kỳ.
- Cài đặt:
  ```json
  {
    "name": "Send Proposal Monthly",
    "type": "schedule",
    "keyParameters": {
      "cron": "0 0 1 * *" // Mỗi tháng ngày 1
    }
  }
  ```

### **🔹 Tối Ưu Template Google Docs**
- **Sử dụng biến nhất quán** (ví dụ: `{{client_name}}`, `{{price}}`, `{{deadline}}`).
- **Định dạng sẵn** (tiêu đề, danh sách, bảng giá) để báo giá trở nên chuyên nghiệp.

---
## 📌 **Kết Luận: Áp Dụng Ngay Để Tiết Kiệm Thời Gian & Tăng Doanh Thu!**

Workflow này **giải phóng thời gian** cho các sếp và team bán hàng, đồng thời **đảm bảo chất lượng** báo giá cao nhất. Với sự hỗ trợ của **AI Claude 3.5 và OpenAI**, nội dung được viết và tối ưu tự động, trong khi **Google Docs Template** đảm bảo định dạng chuyên nghiệp.

**Hành động ngay hôm nay!**
1. **Chuẩn bị tài khoản** (OpenRouter, Google Drive, OpenAI).
2. **Tạo template Google Docs** với các biến cần thiết.
3. **Import workflow** và **cấu hình credentials**.
4. **Test và kích hoạt** để tự động hóa báo giá!

🚀 **Không cần code, không cần lo lắng – chỉ cần nhấn nút và AI làm tất cả!**

---
**🔗 Xem video hướng dẫn chi tiết:** [Watch the video](https://waveten.neetorecord.com/watch/bd8c7fc6122a3bc3df25)