---
title: "💰 **Tự Động Hóa Xử Lý Phiếu Thu Chi Ngân Hàng Sang QuickBooks Online Với AI (Không Cần Code!)**"
description: "Workflow này tự động hóa việc nhập liệu phiếu thu chi ngân hàng từ PDF sang QuickBooks Online bằng AI OpenRouter, tiết kiệm thời gian cho các sếp lên đến 10 giờ/tuần. Hỗ trợ phân loại giao dịch, tạo khách hàng/nợ phải trả tự động, và xử lý tất cả giao dịch một cách chính xác 100%."
slug: "tieu-dong-hoa-phieu-thu-chi-quickbooks-ai"
tags: [n8n, automation, no-code, quickbooks, ai-summarization, openrouter, pdf-processing]
keywords: [tự động hóa phiếu thu chi ngân hàng, quickbooks online automation, ai xử lý pdf, openrouter n8n, workflow tự động hóa kế toán]
---

# 🚀 **Tự Động Hóa Xử Lý Phiếu Thu Chi Ngân Hàng Sang QuickBooks Online Với AI**

### **Giải Phóng Tay Các Sếp Từ Công Việc Nhập Liệu Mệt Mỏi!**
Hàng tuần, các sếp phải mất **tối thiểu 5-10 giờ** để nhập liệu phiếu thu chi từ ngân hàng sang QuickBooks Online. Công việc này không chỉ tẻ nhạt mà còn dễ gây lỗi do nhập sai thông tin khách hàng, mã chi phí, hoặc loại giao dịch. **Workflow này giải quyết vấn đề này bằng AI + tự động hóa 100% không cần code!**

:::info[Gợi ý hạ tầng cho n8n]
Để workflow hoạt động **ổn định 24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS chuyên dụng:
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (Đảm bảo tốc độ xử lý nhanh cho AI)
:::

---

## 🎯 **Kết Quả Các Sếp Nhận Được**
Sau khi triển khai workflow này, các sếp sẽ:
✅ **Tiết kiệm 8-10 giờ/tuần** (tương đương **1 ngày làm việc** mỗi tuần).
✅ **Giảm thiểu lỗi nhập liệu** đến **95%** nhờ AI phân loại giao dịch tự động.
✅ **Tự động tạo khách hàng/nợ phải trả** khi chưa tồn tại trong QuickBooks.
✅ **Phân loại giao dịch chính xác** (thu vs chi) và gán mã chi phí phù hợp.
✅ **Hoạt động liên tục 24/7** mà không cần can thiệp thủ công.

---

## 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
📌 **Tài khoản QuickBooks Online** (cả Sandbox và Production đều được hỗ trợ).
📌 **API Key OpenRouter** (miễn phí với mô hình `openai/gpt-oss-20b:free`).
📌 **Mật khẩu bảo vệ PDF** (nếu phiếu thu chi có bảo vệ).
📌 **ID Công ty QuickBooks** (để cấu hình trong các node HTTP Request).
📌 **Account IDs** (để phân loại giao dịch):
   - **35** (Checking Account)
   - **79/80** (Income/Expense Account)

---

## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
```bash
# Cách import từ file JSON:
1. Tải workflow từ [n8n.io/workflows/12344](https://n8n.io/workflows/12344) (nếu link còn hoạt động).
2. Trên trang n8n Editor, nhấn **Import** và chọn file JSON.
3. Hoặc copy toàn bộ JSON từ [đây](https://n8n.io/workflows/12344) và paste vào **Import Workflow** trong n8n.

# Cách copy/paste JSON:
1. Mở n8n Editor.
2. Nhấn **Import** → **Paste JSON**.
3. Dán toàn bộ mã JSON từ file hoặc link trên.
```

### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này gồm **24 node** và cần cấu hình cẩn thận các phần sau:

#### **A. Cấu Hình QuickBooks Online**
1. **Node `Get many customers`** và `Create a Customer`:
   - Đăng nhập QuickBooks Online và tạo **OAuth Credentials** trong **Developer Portal**.
   - Trong node `QuickBooks`, chọn **Credentials** và nhập:
     - `Consumer Key` và `Consumer Secret` từ QuickBooks.
     - `Company ID` (đã chuẩn bị trước).

2. **Node `Create QuickBooks SalesReceipt` và `Create QuickBooks Expense`**:
   - Đảm bảo **API URL** trong node `httpRequest` có chứa `company_id` của bạn.
   - Ví dụ:
     ```json
     "url": "https://sandbox-quickbooks.api.intuit.com/v3/company/{company_id}/salesreceipt"
     ```

#### **B. Cấu Hình OpenRouter AI**
1. **Node `OpenRouter Chat Model`**:
   - Đăng ký tài khoản [OpenRouter](https://openrouter.ai/) và lấy **API Key**.
   - Trong node, nhập:
     - `model`: `openai/gpt-oss-20b:free`
     - `apiKey`: API Key từ OpenRouter.

2. **Node `Extract PDF Text`**:
   - Nếu PDF có **mật khẩu bảo vệ**, nhập mật khẩu trong **keyParameters** của node này.

#### **C. Cấu Hình Phân Loại Giao Dịch**
1. **Node `Credit or Debit?` (Switch)**:
   - AI sẽ tự động phân loại giao dịch thành **Thu (Credit)** hoặc **Chi (Debit)**.
   - Nếu cần điều chỉnh logic, mở node `code` liên quan để sửa logic phân loại.

2. **Node `Build Salesreceipt Payload` và `Build Expense Payload`**:
   - Các node này sử dụng **JavaScript** để xây dựng payload cho QuickBooks.
   - Nếu cần thay đổi cách gán **mã chi phí** hoặc **khách hàng**, mở node `code` và chỉnh sửa.

---

### **3. Kích Hoạt ⚡️**
1. **Test Run với Dữ Liệu Mẫu**:
   - Tải một **phiếu thu chi PDF mẫu** (có thể là phiếu thu chi ngân hàng thực tế).
   - Upload lên **Bank Statement Form** và chạy **Test Execution**.
   - Kiểm tra kết quả trong QuickBooks Online để đảm bảo dữ liệu nhập chính xác.

2. **Bật Active Workflow**:
   - Sau khi test thành công, chuyển workflow sang **Active** để tự động xử lý tất cả phiếu thu chi mới.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**
### **1. Tích Hợp Slack/Telegram để Báo Lỗi**
- Thêm node **Slack Webhook** hoặc **Telegram Bot** sau node `Error Handling` (nếu có) để nhận thông báo khi workflow gặp lỗi.

### **2. Lưu Log Xử Lý Giao Dịch**
- Sử dụng node **StickyNote** hoặc **Google Sheets** để lưu lịch sử xử lý giao dịch, giúp theo dõi và debug dễ dàng.

### **3. Tự Động Gửi Báo Cáo Định Kỳ**
- Thêm node **Google Calendar** hoặc **Email** để gửi báo cáo tổng hợp giao dịch hàng tháng tự động.

### **4. Cập Nhật Danh Mục Chi Phí**
- Nếu QuickBooks có **Chart of Accounts** mới, cập nhật trong node `Search Categories` để AI phân loại chính xác hơn.

---

## 📌 **Kết Luận**
Workflow này **giải phóng các sếp khỏi công việc nhập liệu mệt mỏi**, giảm thiểu lỗi và tăng hiệu suất kế toán lên **3-5 lần**. Với **AI OpenRouter** và **QuickBooks API**, tất cả giao dịch đều được xử lý tự động, từ **phân loại thu/chí** đến **tạo khách hàng/nợ phải trả** một cách chính xác.

**Hành động ngay hôm nay!**
1. **Import workflow** theo hướng dẫn trên.
2. **Cấu hình QuickBooks + OpenRouter** theo các bước chi tiết.
3. **Test với phiếu thu chi mẫu** và bật **Active** để tự động hóa ngay!

👉 [Tải workflow từ n8n.io](https://n8n.io/workflows/12344) (nếu link còn hoạt động) hoặc **copy/paste JSON** từ bài viết này.

---
**Chia sẻ và đánh giá nếu workflow này giúp ích!** 🚀