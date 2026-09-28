---
title: "🚀 Tự Động Hóa Xử Lý Hóa Đơn & Chi Phí Tài Chính Với AI Gemini & n8n - Giải Pháp Không Code Cho Doanh Nghiệp"
description: "Workflow tự động hóa hoàn toàn xử lý hóa đơn, hóa đơn chi phí và báo cáo ngân hàng bằng trí tuệ nhân tạo Google Gemini, OpenRouter và Google Sheets. Giúp tiết kiệm 10-15 giờ/ngày cho bộ phận kế toán, giảm sai sót 90% và cung cấp báo cáo tự động hóa 24/7."
slug: "tieu-dong-hoa-xu-ly-hoa-don-ai-gemini-n8n"
tags: [n8n, automation, no-code, ai-gemini, google-sheets, google-drive, openrouter, financial-automation]
keywords: [tự động hóa kế toán, ai gemini n8n, xử lý hóa đơn tự động, giảm thời gian kế toán, giải pháp không code tài chính, google sheets automation, openrouter llm]
---

# 🚀 **Tự Động Hóa Xử Lý Tài Chính Tự Động Với AI Gemini & n8n: Giải Pháp Không Code Cho Doanh Nghiệp**

## 📌 **Giới Thiệu**
Bạn đã bao giờ mệt mỏi với việc thủ công nhập liệu hóa đơn, hóa đơn chi phí và báo cáo ngân hàng? Hay phải mất hàng giờ để phân loại chi phí theo 17 danh mục kế toán chuẩn? **Workflow này giải quyết tất cả những vấn đề đó bằng trí tuệ nhân tạo (AI) và tự động hóa quy trình (RPA) 100% không cần code!**

Dùng **Google Gemini** để trích xuất dữ liệu từ hóa đơn, **OpenRouter LLM** để phân loại chi phí tự động, và **Google Sheets** để lưu trữ dữ liệu một cách có cấu trúc. Workflow này hoạt động **24/7**, giúp tiết kiệm **10-15 giờ/ngày** cho bộ phận kế toán, giảm sai sót lên đến **90%** và cung cấp báo cáo tự động hóa cho các nhà quản lý.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Giảm 10-15 giờ/ngày cho bộ phận kế toán.
- **Chính xác cao**: Trích xuất và phân loại dữ liệu bằng AI, giảm sai sót lên đến 90%.
- **Tự động hóa hoàn toàn**: Không cần can thiệp thủ công, hoạt động 24/7.
- **Báo cáo tự động**: Cung cấp dữ liệu sẵn sàng cho phân tích và báo cáo.
- **Phân loại chi phí tự động**: 17 danh mục kế toán chuẩn, giảm thời gian phân loại.
- **Tích hợp Google Sheets**: Dữ liệu luôn được cập nhật và sẵn sàng cho báo cáo.
:::

---

### 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
**1. Tài khoản Google Business (Google Workspace)**
- **Google Drive API** (để lưu trữ và theo dõi file)
- **Google Sheets API** (để lưu trữ dữ liệu tài chính)
- **Google Gemini API** (để trích xuất dữ liệu từ hóa đơn)

**2. Tài khoản OpenRouter API**
- Đăng ký tại [OpenRouter](https://openrouter.ai/) để sử dụng LLM cho phân loại chi phí.

**3. Folder và Sheet chuẩn bị sẵn**
- **Google Drive**:
  - Folder **"Invoices"** (để lưu hóa đơn đã xử lý)
  - Folder **"Expense Receipts"** (để theo dõi hóa đơn chi phí mới)
  - Folder **"Bank Statements"** (để theo dõi báo cáo ngân hàng mới)
- **Google Sheets**:
  - **"Test Invoice Records"** (dữ liệu hóa đơn)
  - **"Expenses Recording"** (dữ liệu chi phí)
  - **"Bank Transactions Record"** (dữ liệu giao dịch ngân hàng)

**4. API Keys và Credentials**
- **Google Drive OAuth 2.0 API Key**
- **Google Sheets OAuth 2.0 API Key**
- **Google Gemini API Key**
- **OpenRouter API Key**
:::

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
- **Tải workflow** từ [n8n.io/workflows/9054](https://n8n.io/workflows/9054) hoặc copy JSON từ trang này.
- **Import vào n8n Editor**:
  - Mở **n8n Editor** trên trang web hoặc máy chủ self-hosted.
  - Nhấn **Import** và dán JSON từ file hoặc copy/paste từ trang này.
  - Chọn **Import** để hoàn tất.

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này gồm **4 phần chính** (Invoice, Expense, Bank Statement, và Financial Analysis). Dưới đây là hướng dẫn chi tiết để cấu hình:

#### **📄 Phần 1: Xử lý Hóa Đơn (Invoice Processing)**
- **Trigger**: **"When chat message received"** (để người dùng upload hóa đơn qua chat).
- **Node "Upload PDF to Google Gemini"**:
  - Điền **Google Palm API Key** vào **credentials**.
  - Chọn **httpHeaderAuth** và điền **Authorization** với định dạng:
    ```
    Bearer YOUR_GOOGLE_GEMINI_API_KEY
    ```
- **Node "Table ERP" (Google Sheets)**:
  - Chọn **Google Sheets OAuth2 API** và chọn **Sheet "Test Invoice Records"**.
  - Đảm bảo cột trong sheet phù hợp với dữ liệu trích xuất (Vendor Name, Invoice Number, Invoice Date, ...).

#### **🧾 Phần 2: Xử lý Hóa Đơn Chi Phí (Expense Processing)**
- **Trigger**: **"Google Drive Trigger"** (theo dõi folder **"Expense Receipts"**).
- **Node "Upload PDF to Google Gemini"**:
  - Sử dụng cùng **Google Palm API Key** như phần Invoice.
- **Node "OpenRouter Chat Model"**:
  - Điền **OpenRouter API Key** vào **credentials**.
  - Chọn mô hình **openai/gpt-4.1** (hoặc mô hình khác nếu muốn).
- **Node "Structured Output Parser"**:
  - Đảm bảo cấu trúc JSON trả về phù hợp với danh mục chi phí (17 danh mục).

#### **🏦 Phần 3: Xử lý Báo Cáo Ngân Hàng (Bank Statement Processing)**
- **Trigger**: **"Google Drive Trigger"** (theo dõi folder **"Bank Statements"**).
- **Node "Code"**:
  - Đây là phần xử lý dữ liệu giao dịch từ AI. Đảm bảo **JavaScript code** trong node này hoạt động chính xác.
  - Nếu cần, chỉnh sửa code để phù hợp với định dạng báo cáo ngân hàng của bạn.

#### **📈 Phần 4: Phân Tích Tài Chính (Financial Analysis Agent)**
- **Trigger**: **"When Executed by Another Workflow"** (hoặc kích hoạt thủ công).
- **Node "OpenRouter Chat Model1"**:
  - Chọn mô hình **openai/gpt-4.1** để phân tích dữ liệu.
- **Node "AI Agent"**:
  - Đảm bảo **credentials** của **OpenRouter API** được điền chính xác.
  - Cấu hình **Google Sheets Tools** để kết nối với 3 sheet: **Invoices, Expenses, Transactions**.

### **3. Kích hoạt ⚡️**
- **Test Run**:
  - Upload một hóa đơn mẫu vào folder **"Expense Receipts"** và kiểm tra kết quả trong **Google Sheets**.
  - Gửi một câu hỏi phân tích tài chính qua **AI Agent** để kiểm tra tính năng.
- **Bật Active**:
  - Sau khi kiểm tra, bật **Active** cho workflow.

---

## ✍️ **Mẹo & gợi ý nâng cao**
1. **Tích hợp Slack/Telegram**:
   - Sử dụng **Slack Webhook** hoặc **Telegram Bot** để thông báo kết quả xử lý hóa đơn chi phí.
   - Ví dụ: Khi một hóa đơn chi phí được xử lý, gửi thông báo đến Slack với thông tin chi tiết.

2. **Lưu log hoạt động**:
   - Thêm **Google Sheets** hoặc **Google Drive** để lưu log hoạt động của workflow.
   - Ví dụ: Lưu thời gian xử lý, tên file, và kết quả thành công/thất bại.

3. **Gửi báo cáo định kỳ**:
   - Sử dụng **Google Sheets** kết hợp với **n8n Schedule Node** để gửi báo cáo chi phí hàng tháng qua email.
   - Ví dụ: Tạo một workflow mới để gửi báo cáo chi phí tháng qua cho bộ phận quản lý.

4. **Tự động hóa báo cáo thuế**:
   - Sử dụng **AI Agent** để phân tích dữ liệu chi phí và tự động tạo báo cáo thuế VAT.
   - Ví dụ: "Tính tổng VAT cho tháng này và tạo báo cáo tự động."

5. **Cập nhật danh mục chi phí**:
   - Nếu doanh nghiệp có thêm danh mục chi phí mới, cập nhật **Structured Output Parser** trong node **OpenRouter Chat Model** để AI phân loại chính xác.

---

## 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các doanh nghiệp muốn tự động hóa xử lý tài chính mà không cần viết code. Bằng cách sử dụng **Google Gemini, OpenRouter LLM, và Google Sheets**, bạn có thể tiết kiệm thời gian, giảm sai sót và tập trung vào việc phân tích dữ liệu chứ không phải nhập liệu.

**Hãy áp dụng ngay và tự động hóa bộ phận kế toán của mình!** 🚀

---
**📌 Lưu ý cuối cùng**:
- Đảm bảo **Google Drive** và **Google Sheets** có quyền truy cập đầy đủ cho workflow.
- Kiểm tra **API Key** thường xuyên để đảm bảo không bị hết hạn.
- Nếu gặp vấn đề, tham khảo **n8n Community** hoặc liên hệ với **AutoSolutions.ai** (Didac Fernandez) để hỗ trợ.