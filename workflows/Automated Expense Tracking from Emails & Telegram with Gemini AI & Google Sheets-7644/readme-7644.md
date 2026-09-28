---
title: "💰 **Tự Động Hóa Theo Dõi Chi Phí Từ Email & Telegram Với Gemini AI + Google Sheets** – Không Cần Code!"
description: "Workflow tự động hóa hoàn toàn để phân tích, phân loại và ghi nhận chi phí từ email ngân hàng/UPI, Telegram, đồng thời so sánh với ngân sách và cảnh báo khi vượt ngưỡng. Giúp các sếp tiết kiệm thời gian, quản lý tài chính hiệu quả và nhận báo cáo chi tiết hàng tháng."
slug: "tieu-dong-hoa-theo-doi-chi-phi-gmail-telegram-gemini-ai"
tags: [n8n, automation, no-code, ai-summarization, google-sheets, gemini-ai, telegram-bot, expense-tracking]
keywords: [n8n workflow chi phí, tự động hóa theo dõi ngân hàng, gemini ai phân tích email, google sheets tự động, cảnh báo vượt ngân sách, telegram bot quản lý tài chính]
---

# **🚀 Tự Động Hóa Theo Dõi Chi Phí Từ Email & Telegram Với Gemini AI + Google Sheets**

### **🔍 Nỗi Đau Của Các Sếp Hiện Nay**
Hàng ngày, các sếp phải:
- **Lặp đi lặp lại** việc sao chép số liệu từ email ngân hàng/UPI vào Excel/Google Sheets.
- **Mất thời gian** phân loại giao dịch (thu/chi, loại chi phí, ngày tháng) một cách thủ công.
- **Không biết** mình đã chi tiêu bao nhiêu cho mỗi hạng mục (ăn uống, đi lại, giải trí...) trong tháng.
- **Bị bất ngờ** khi chi phí vượt ngân sách do không theo dõi kịp thời.
- **Không có báo cáo** tổng hợp chi tiết để so sánh với mục tiêu tài chính hàng năm.

**Giải pháp?** **Workflow này tự động hóa toàn bộ quy trình** – từ nhận email/UPI, phân tích bằng AI, phân loại, ghi vào Google Sheets, đến cảnh báo khi vượt ngân sách. **Không cần viết một dòng code nào!**

---
:::info[**Gợi ý hạ tầng cho n8n**]
Để workflow hoạt động **24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS riêng. Đây là giải pháp **ổn định, an toàn và tiết kiệm chi phí** so với dùng phiên bản cloud.
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** – giảm tới **39%**)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (đủ sức mạnh cho workflow này)
:::

---

## **🎯 Kết Quả Các Sếp Nhận Được**
Sau khi áp dụng workflow này, các sếp sẽ:
✅ **Tiết kiệm 10+ giờ/tháng** không phải nhập liệu thủ công.
✅ **Nhận báo cáo chi tiết** hàng tháng với phân loại chi phí chính xác (thu/chi, hạng mục, ngày tháng).
✅ **So sánh với ngân sách** và **nhận cảnh báo** khi chi tiêu vượt ngưỡng.
✅ **Tự động tổng hợp** chi phí hàng năm để so sánh với mục tiêu tài chính.
✅ **Quản lý gia đình/đội nhóm** dễ dàng với dữ liệu thống nhất trên Google Sheets.
✅ **Hoạt động liên tục** (không cần phải mở máy tính) nhờ tự động hóa trên VPS.

---

## **🔧 Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
### **1. Tài Khoản & API Keys**
| **Dịch Vụ**               | **Thông Tin Cần Thiết**                                                                 | **Lưu Ý**                                                                 |
|---------------------------|------------------------------------------------------------------------------------------|---------------------------------------------------------------------------|
| **Gmail**                 | - Tài khoản Google (đã kích hoạt "Gmail API")                                           | - **Bật "Less Secure Apps"** (nếu cần) hoặc sử dụng OAuth 2.0.           |
|                           | - **API Key** (tạo tại [Google Cloud Console](https://console.cloud.google.com/))          | - Chọn **Gmail API** và **Google Sheets API**.                            |
| **Google Sheets**         | - **File Google Sheets** có 3 tab: `Expenses`, `Budgets`, `Yearly Summary` (sẵn sàng).    | - **Chia sẻ file** với n8n (quyền "Sửa").                                  |
| **Telegram Bot**          | - **Bot Token** (tạo tại [@BotFather](https://t.me/BotFather)).                          | - **Chat ID** của bot (lấy từ [@userinfobot](https://t.me/userinfobot)).    |
| **Google Gemini API**     | - **API Key** (tạo tại [Google AI Studio](https://aistudio.google.com/)).                 | - Chọn **Gemini Pro** hoặc **Gemini 1.5**.                                 |
| **Ngân Hàng/UPI**        | - Email nhận thông báo giao dịch (ví dụ: `alerts@hdfcbank.net`, `ealerts@iobnet.co.in`). | - Thêm email này vào **danh sách cho phép** trong Gmail.                     |

### **2. File Google Sheets Mẫu**
Workflow yêu cầu **1 file Google Sheets** với **3 tab** sau:
- **`Expenses`**: Ghi chi tiết giao dịch (ngày, loại, số tiền, mô tả...).
- **`Budgets`**: Định nghĩa ngân sách hàng tháng cho từng hạng mục (ăn, đi lại, giải trí...).
- **`Yearly Summary`**: Tự động tổng hợp chi phí hàng năm.

👉 **[Tải file mẫu](https://docs.google.com/spreadsheets/d/1EXAMPLEFILE/edit?usp=sharing)** *(thay thế bằng link thực tế)*

---

## **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. **Tải workflow** từ [n8n.io/workflows/7644](https://n8n.io/workflows/7644) (chọn **Download JSON**).
2. **Mở n8n Editor** (trên VPS hoặc phiên bản cloud).
3. Nhấn **Import** → Chọn file JSON vừa tải → **Import**.

#### **Phương pháp 2: Copy/Paste JSON**
1. **Copy toàn bộ mã JSON** từ [n8n.io/workflows/7644](https://n8n.io/workflows/7644).
2. Trong **n8n Editor**, nhấn **Import** → Chọn **Paste JSON** → Dán và **Import**.

---
### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này có **2 nhánh chính**:
- **Nhánh Telegram** (nhận tin nhắn từ bot Telegram).
- **Nhánh Gmail** (nhận email từ ngân hàng/UPI).

#### **🔹 Cấu Hình Telegram Trigger**
1. **Node: `Telegram Trigger`**
   - **Credentials**: Chọn `telegramApi` (đã cấu hình trước).
   - **Chat ID**: Nhập **Chat ID** của bot (lấy từ `@userinfobot`).
   - **Message Type**: Chọn `text`.

2. **Node: `Information extraction from telegram input` (LLM Chain)**
   - **Model**: Chọn `Google Gemini Chat Model` (sử dụng `googlePalmApi`).
   - **Prompt**: Sẵn sàng trong workflow (không cần chỉnh sửa).
   - **Output Format**: Đảm bảo trả về **JSON** với schema:
     ```json
     {
       "date": "DD/MM/YYYY",
       "account": "Tên ngân hàng/UPI",
       "from": "Người gửi",
       "to": "Người nhận",
       "type": "Credit/Debit",
       "category": "Hạng mục chi phí",
       "description": "Mô tả",
       "amount": "Số tiền",
       "currency": "INR/VND/USD",
       "source": "Telegram"
     }
     ```

#### **🔹 Cấu Hình Gmail Trigger**
1. **Node: `Gmail Trigger`**
   - **Credentials**: Chọn `gmailOAuth2Api`.
   - **Query**: Điền **email của ngân hàng/UPI** (ví dụ: `from:(alerts@hdfcbank.net OR ealerts@iobnet.co.in)`).
   - **Label**: Chọn `UNLABELED` (nếu muốn lấy tất cả email mới).

2. **Node: `Extract the email only from specified bank/UPI apps` (Code)**
   - **Code**: Sẵn sàng trong workflow (không cần chỉnh sửa).
   - **Lưu ý**: Nếu email có nhiều người gửi, **cần filter** để chỉ lấy email từ ngân hàng/UPI.

3. **Node: `Generate the structured data from the raw emails` (LLM Chain)**
   - **Model**: Chọn `Google Gemini Chat Model`.
   - **Prompt**: Sử dụng **schema JSON** như trên (để AI phân tích email thành dữ liệu có cấu trúc).
   - **Output**: Đảm bảo trả về **JSON** với schema:
     ```json
     {
       "date": "DD/MM/YYYY",
       "account": "Tên ngân hàng/UPI",
       "from": "Người gửi",
       "to": "Người nhận",
       "type": "Credit/Debit",
       "category": "Hạng mục chi phí",
       "description": "Mô tả",
       "amount": "Số tiền",
       "currency": "INR/VND/USD",
       "source": "Gmail",
       "messageId": "ID email",
       "status": "Posted/Pending"
     }
     ```

#### **🔹 Cấu Hình Google Sheets**
1. **Node: `Append transaction data to budget sheet` & `Append transaction data to expense sheet`**
   - **Credentials**: Chọn `googleSheetsOAuth2Api`.
   - **Sheet Name**: Điền tên tab (`Budgets` hoặc `Expenses`).
   - **Range**: Điền `A1:Z` (hoặc chỉ định cột cụ thể).
   - **Operation**: Chọn `append` (thêm dữ liệu mới vào cuối sheet).

2. **Cấu trúc dữ liệu trong Google Sheets**
   - **Tab `Expenses`**:
     | Date       | Account   | From       | To         | Type    | Category   | Description | Amount | Currency | Source   | Message ID | Status     |
     |------------|-----------|------------|------------|---------|------------|-------------|---------|-----------|-----------|------------|-------------|
     | 10/10/2024 | HDFC Bank | alert@hdfc | John Doe   | Debit   | Food       | Breakfast   | 50000   | INR       | Gmail     | EM1234567  | Posted     |
   - **Tab `Budgets`**:
     | Category   | Monthly Budget | Remaining |
     |------------|----------------|-----------|
     | Food       | 500,000        | 450,000   |
     | Travel     | 200,000        | 200,000   |
   - **Tab `Yearly Summary`**:
     | Month      | Total Expense | Budget Variance |
     |------------|---------------|-----------------|
     | October    | 1,200,000     | -50,000        |

#### **🔹 Cấu Hình Cảnh Báo Vượt Ngân Sách**
1. **Node: `Check if the transaction is 'Budget' or 'Expense'` (IF)**
   - **Condition**: Kiểm tra nếu `category` trong `Budgets` sheet.
   - **Nếu đúng**: So sánh `amount` với `Remaining` trong `Budgets`.
   - **Nếu vượt ngưỡng**: Gửi **cảnh báo** qua Telegram/Email.

2. **Node: `Send a confirmation reply to the user` (Telegram)**
   - **Credentials**: Chọn `telegramApi`.
   - **Chat ID**: Nhập **Chat ID** của bot.
   - **Message**: Thông báo xác nhận đã ghi nhận giao dịch.

---

### **3. Kích Hoạt Workflow ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Gửi **email mẫu** từ ngân hàng/UPI vào Gmail.
   - Gửi **tin nhắn mẫu** qua Telegram bot.
   - Kiểm tra **Google Sheets** có ghi dữ liệu không.
2. **Bật Active**:
   - Nhấn **Active** trên workflow.
   - **Lưu ý**: Nếu dùng **Gmail Trigger**, workflow sẽ chạy **liên tục** (nhận email mới).
   - Nếu dùng **Telegram Trigger**, workflow sẽ chạy khi **nhận tin nhắn**.

---

## **✍️ Mẹo & Gợi Ý Nâng Cao**
### **1. Tích Hợp Slack/Telegram cho Cảnh Báo**
- Thay vì chỉ gửi thông báo qua Telegram, các sếp có thể **tích hợp Slack** để cảnh báo vượt ngân sách.
- **Cách làm**:
  - Thêm **node `slack`** (nếu dùng Slack).
  - Cấu hình **webhook Slack** và gửi thông báo tự động.

### **2. Lưu Log Lịch Sử Giao Dịch**
- Thêm **node `googleSheets`** mới để ghi **lịch sử chi tiết** vào tab `Transaction Logs`.
- **Schema**:
  ```json
  {
    "timestamp": "DD/MM/YYYY HH:MM:SS",
    "transactionId": "ID duy nhất",
    "status": "Processed/Failed",
    "error": "Nếu có"
  }
  ```

### **3. Gửi Báo Cáo Hàng Tháng qua Email**
- Sử dụng **node `gmail`** để tự động gửi **báo cáo tổng hợp** vào cuối tháng.
- **Cách làm**:
  - Thêm **node `date`** để kiểm tra ngày tháng.
  - Nếu ngày là **ngày cuối tháng**, gửi email với **báo cáo chi tiết** từ `Yearly Summary`.

### **4. Phân Loại Chi Phí Tự Động**
- Cải thiện **prompt của Gemini AI** để phân loại chi phí chính xác hơn.
- **Ví dụ prompt nâng cao**:
  ```plaintext
  "Analyze the following email and extract structured data. Classify the transaction into one of these categories: Food, Transport, Rent, Utilities, Entertainment, Shopping, Health, Education, Savings. If the category is unclear, default to 'Other'."
  ```

### **5. Tích Hợp với Xero/QuickBooks (Nâng Cao)**
- Nếu các sếp dùng **phần mềm kế toán**, có thể **tích hợp với Xero/QuickBooks** để đồng bộ dữ liệu.
- **