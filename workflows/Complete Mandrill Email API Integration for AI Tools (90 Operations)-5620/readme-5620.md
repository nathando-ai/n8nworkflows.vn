---
title: "🚀 Tự Động Hóa Toàn Bộ API Mandrill Cho Công Cụ AI: 90 Hoạt Động Không Cần Code"
description: "Workflow này tự động hóa 90+ hoạt động API Mandrill (gửi email, quản lý người dùng, tag, template...) để các sếp tiết kiệm thời gian và tối ưu hóa hệ thống email AI. Giúp tự động hóa từ quản lý tài khoản đến gửi email bulk với độ chính xác cao."
slug: "tieu-dong-hoa-api-mandrill-cho-ai"
tags: [n8n, automation, mandrill-api, ai-tools, email-automation, no-code]
keywords: [tự động hóa mandrill api, n8n workflow mandrill, gửi email bulk tự động, quản lý mandrill bằng n8n, tự động hóa email cho ai]
---

# 🚀 **Tự Động Hóa Toàn Bộ API Mandrill Cho Công Cụ AI: 90 Hoạt Động Không Cần Code**

### **Giải Pháp Cho Các Sếp Bị "Nghẹt Thở" Khi Quản Lý Email AI**
Các sếp đang gặp phải vấn đề gì khi quản lý hệ thống email AI?
- **Thủ công quá nhiều**: Tạo tài khoản, tag, template, gửi email bulk... phải làm thủ công?
- **Rủi ro sai sót**: Quên cập nhật thông tin người dùng, tag sai mục đích, hoặc gửi email không đúng đối tượng?
- **Không mở rộng được**: Khi hệ thống phát triển, phải viết code mới để mở rộng chức năng?

Workflow này **giải quyết tất cả** bằng cách tự động hóa **90+ hoạt động API Mandrill** chỉ với một dòng code. Từ quản lý người dùng, tạo tag, gửi email bulk đến cập nhật template, **tất cả đều được tự động hóa 100%**.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không phải làm thủ công 90+ hoạt động API.
- **Độ chính xác cao**: Tránh sai sót khi cập nhật thông tin người dùng, tag, hoặc gửi email.
- **Mở rộng dễ dàng**: Thêm hoặc sửa các hoạt động API chỉ bằng cách chỉnh sửa workflow.
- **Hoạt động liên tục**: Chạy 24/7 trên VPS, không cần can thiệp người dùng.
- **Tích hợp AI**: Sẵn sàng kết nối với các công cụ AI (RAG, LLM) để tự động hóa gửi email cá nhân hóa.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần:
- **Tài khoản Mandrill** (đã kích hoạt API).
- **API Key của Mandrill** (trong `Settings > API Keys`).
- **n8n Self-hosted** (để chạy 24/7, không phụ thuộc vào phiên bản cloud).
- **Node `@n8n/n8n-nodes-langchain`** (để kết nối với các công cụ AI).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Tải file JSON từ [n8n.io/workflows/5620](https://n8n.io/workflows/5620).
2. Mở **n8n Editor** và chọn `Import Workflow`.
3. Chọn file JSON và nhấn `Import`.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này sử dụng **91 node**, chủ yếu là `httpRequestTool` để gọi API Mandrill. Các bước quan trọng cần chú ý:

##### **A. Cấu Hình Mandrill MCP Server**
- Node đầu tiên là `Mandrill MCP Server` (loại `mcpTrigger`).
- Các sếp cần **đăng ký một Webhook** trong Mandrill để nhận dữ liệu từ API.
- **Cách làm**:
  1. Mở `Settings > Webhooks` trong Mandrill.
  2. Tạo một Webhook mới với URL là URL của n8n (ví dụ: `https://n8n.example.com/webhook/mandrill`).
  3. Điền URL này vào node `Mandrill MCP Server` trong workflow.

##### **B. Cấu Hình API Key**
- Tất cả các node `httpRequestTool` đều cần **API Key của Mandrill**.
- **Cách làm**:
  1. Mở `Settings > API Keys` trong Mandrill.
  2. Sao chép `API Key` và điền vào trường `Authorization` của các node `httpRequestTool` (dạng `Bearer YOUR_API_KEY`).

##### **C. Chỉnh Sửa Tham Số API**
- Các node như `Create User`, `Create Tag`, `Create Template`, `Send Email`... đều cần **tham số cụ thể** (ví dụ: `email`, `name`, `subject`, `html`).
- **Lưu ý**:
  - Các trường bắt buộc (như `email` trong `Create User`) **không được để trống**.
  - Nếu muốn gửi email bulk, các sếp cần **tạo một danh sách người dùng** và truyền vào node `Create Message`.

##### **D. Kết Nối Với AI (Nếu Có)**
- Nếu muốn sử dụng AI để tự động hóa nội dung email, các sếp cần kết nối với node `@n8n/n8n-nodes-langchain`.
- **Cách làm**:
  1. Cài đặt node `langchain` trong n8n.
  2. Kết nối node `Create Message` với node `langchain` để tự động tạo nội dung email.

#### **3. Kích Hoạt ⚡️**
1. **Test Run**: Chạy một test với dữ liệu mẫu (ví dụ: tạo một người dùng mẫu).
2. **Bật Active**: Sau khi kiểm tra, bật `Active` để workflow chạy tự động.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[MỞ RỘNG THÊM]
- **Gửi Email Bulk Tự Động**: Kết nối với Google Sheets hoặc CSV để lấy danh sách người dùng và gửi email bulk.
- **Lưu Log Hoạt Động**: Sử dụng node `Set` hoặc `Set Variable` để lưu lịch sử hoạt động vào cơ sở dữ liệu (ví dụ: Google Sheets).
- **Gửi Báo Cáo Định Kỳ**: Sử dụng node `Schedule` để gửi báo cáo tổng hợp về hoạt động email hàng tuần.
- **Kết Nối Với Slack/Telegram**: Thông báo lỗi hoặc thành công qua Slack/Telegram bằng node `Slack` hoặc `Telegram Bot`.
- **Tự Động Xóa Email Trùng Lặp**: Sử dụng node `If` để kiểm tra và xóa email trùng lặp trước khi gửi.
:::

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc thủ công phiền toái khi quản lý Mandrill. Từ tạo tài khoản đến gửi email bulk, **tất cả đều được tự động hóa chỉ với một dòng code**.

**Hãy thử ngay và tiết kiệm thời gian cho đội ngũ của mình!**
👉 [Tải workflow từ n8n.io](https://n8n.io/workflows/5620)
👉 [Đăng ký VPS TinoHost để self-host n8n](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)