---
title: "📈 **Báo Cáo Phân Tích Cổ Phiếu Tự Động Hóa: Kết Hợp Phân Tích Kỹ Thuật + Xét Dựng Tin Tức bằng GPT-4o (Miễn Code!)**"
description: "Workflow tự động hóa phân tích cổ phiếu toàn diện bằng GPT-4o, kết hợp dữ liệu kỹ thuật (Bollinger Bands, MACD) và phân tích cảm xúc tin tức từ Alpha Vantage. Tạo báo cáo HTML động, gửi email định kỳ với gợi ý đầu tư dữ liệu hóa - hoàn toàn không cần viết code."
slug: "auto-stock-analysis-gpt4o"
tags: [n8n, automation, finance, ai, gpt-4o, technical-analysis, sentiment-analysis, email-automation]
keywords: [n8n workflow phân tích cổ phiếu, tự động hóa đầu tư, GPT-4o phân tích kỹ thuật, báo cáo cổ phiếu tự động, API Twelve Data, Alpha Vantage sentiment]
---

# 🚀 **Báo Cáo Phân Tích Cổ Phiếu Tự Động Hóa: Kết Hợp Kỹ Thuật + Xét Dựng Tin Tức bằng GPT-4o**

## **🔍 Nỗi Đau Của Các Sếp Trong Phân Tích Cổ Phiếu**
Bạn đã bao giờ phải:
- **Tốn thời gian** tra cứu dữ liệu lịch sử, chỉ số kỹ thuật (RSI, MACD) và tin tức tài chính từ nhiều nguồn khác nhau?
- **Mất nhiều giờ** để tổng hợp báo cáo từ các công cụ phân tích khác biệt, rồi phải viết lại bằng tay?
- **Không chắc chắn** về quyết định đầu tư vì thiếu sự kết hợp giữa dữ liệu kỹ thuật và cảm xúc thị trường?
- **Không có thời gian** theo dõi thị trường hàng ngày mà vẫn muốn cập nhật thông tin mới nhất?

**Workflow này giải quyết tất cả!** Với **GPT-4o** và các API chuyên dụng, nó tự động:
✅ **Phân tích kỹ thuật** (Bollinger Bands, MACD, Support/Resistance) từ dữ liệu lịch sử.
✅ **Xét dựng tin tức** (sentiment analysis) từ Alpha Vantage để đánh giá tâm lý thị trường.
✅ **Tạo báo cáo HTML động** với thiết kế phù hợp (RTL cho tiếng Hebrew, dễ đọc trên mobile).
✅ **Gửi email tự động** với gợi ý đầu tư chi tiết **mỗi tuần** (hoặc theo lịch bạn đặt).

---
### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**Lợi Ích Cốt Lõi**]
- **Tiết kiệm 10-15 giờ/tuần** so với cách làm thủ công.
- **Độ chính xác cao** nhờ kết hợp phân tích kỹ thuật + cảm xúc thị trường.
- **Báo cáo cá nhân hóa** với thiết kế chuyên nghiệp, dễ đọc trên mọi thiết bị.
- **Hoạt động 24/7** mà không cần can thiệp của bạn.
- **Gợi ý đầu tư dữ liệu hóa** dựa trên mô hình AI tiên tiến.
:::

---
### 🔧 **Yêu Cầu Cần Thiết**
:::info[**CHUẨN BỊ TRƯỚC KHI BẮT ĐẦU**]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **API Keys** (miễn phí hoặc trả phí):
   - **OpenAI API Key** (để sử dụng GPT-4o).
   - **Chart-img API Key** (trích xuất biểu đồ cổ phiếu).
   - **Twelve Data API Key** (dữ liệu lịch sử và chỉ số kỹ thuật).
   - **Alpha Vantage API Key** (tin tức tài chính và sentiment analysis).
2. **SMTP Credentials** (để gửi email báo cáo):
   - Host (ví dụ: `smtp.gmail.com`).
   - Port (465 hoặc 587).
   - Tài khoản email và mật khẩu (sử dụng **mật khẩu ứng dụng** nếu là Gmail).
3. **n8n Self-hosted** (không dùng phiên bản cloud để đảm bảo dữ liệu an toàn).
   👉 [**Đăng ký VPS TinoHost**](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới 39%).
   👉 [**Đăng ký VPS Xeon 4GB chỉ 50k/tháng**](https://my.bnix.one/aff.php?aff=172).

---
### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Cách 1:** Tải file JSON từ [n8n.io/workflows/3790](https://n8n.io/workflows/3790) và import vào **n8n Editor**.
- **Cách 2:** Copy toàn bộ JSON từ link trên và **paste** vào **Import Workflow** trong n8n.
- **Lưu ý:** Chọn **Create a new workflow** khi import.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này gồm **33 node** phức tạp, nhưng chỉ cần chú ý đến các bước sau:

##### **A. Cấu Hình API Keys**
Tất cả các node sử dụng API đều **bắt buộc** phải điền **credentials** (API Key). Các node quan trọng:
- **`GPT 4o`** (`lmChatOpenAi`):
  - Điền **OpenAI API Key** vào **Credentials** (tên: `openAiApi`).
  - Chọn model: `gpt-4o`.
- **`Get Price History`**, **`Get Bollinger Bands`**, **`Get MACD`** (`httpRequest`):
  - Điền **Twelve Data API Key** vào **Headers** (chìa khóa: `X-TWELVE-DATA-API-KEY`).
- **`Get News Data`** (`httpRequest`):
  - Điền **Alpha Vantage API Key** vào **Headers** (chìa khóa: `apikey`).
- **`Get Chart URL`** (`httpRequest`):
  - Điền **Chart-img API Key** vào **Headers** (chìa khóa: `Authorization`).

##### **B. Cấu Hình SMTP (Gửi Email)**
- Node **`Send Stock Analysis`** (`emailSend`):
  - Chọn **Credentials**: `smtp`.
  - Điền thông tin SMTP:
    - **Host**: `smtp.gmail.com` (hoặc SMTP của nhà cung cấp email khác).
    - **Port**: `465` (SSL) hoặc `587` (TLS).
    - **Username**: Email của bạn.
    - **Password**: **Mật khẩu ứng dụng** (không phải mật khẩu đăng nhập Gmail).
  - **Lưu ý:** Nếu dùng Gmail, bật **2FA** và tạo mật khẩu ứng dụng tại [My Account > Security](https://myaccount.google.com/security).

##### **C. Cấu Hình Schedule Trigger**
- Node **`Schedule Trigger1`** (`scheduleTrigger`):
  - Chọn **Cron expression** theo lịch bạn muốn chạy (ví dụ: `0 0 * * 1` để chạy mỗi thứ 2 hàng tuần).
  - **Lưu ý:** Nếu muốn chạy theo yêu cầu (không tự động), bỏ qua node này và sử dụng **Form Trigger** (`on form submission`).

##### **D. Cấu Hình Form Trigger (Nếu Sử Dụng)**
- Node **`On form submission`** (`formTrigger`):
  - Nếu muốn người dùng nhập mã cổ phiếu thủ công, cấu hình **Form** trong n8n Editor.
  - Các biến cần thiết:
    - `stockSymbol`: Mã cổ phiếu (ví dụ: `AAPL`).
    - `email`: Email nhận báo cáo.

##### **E. Cấu Hình AI Agent**
- Node **`AI Agent`** (`agent`):
  - Được cấu hình sẵn để phân tích kết hợp dữ liệu kỹ thuật và tin tức.
  - **Không cần chỉnh sửa** trừ khi muốn thay đổi **prompt** (hướng dẫn cho GPT-4o).

##### **F. Cấu Hình Email Template**
- Node **`Generate HTML`** (`html`):
  - Báo cáo sẽ tự động tạo ra **HTML động** với dữ liệu từ các node trước.
  - **Không cần chỉnh sửa** nếu muốn giữ thiết kế mặc định (phù hợp RTL cho tiếng Hebrew).

---
#### **3. Kích Hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Chọn node **`Schedule Trigger1`** (hoặc **`Form Trigger`**).
   - Nhấn **Execute Workflow** và kiểm tra kết quả.
2. **Bật Active**:
   - Sau khi kiểm tra thành công, chuyển **Status** từ **Inactive** sang **Active**.
3. **Kiểm tra Email**:
   - Báo cáo sẽ được gửi đến email đã cấu hình trong **SMTP Credentials**.

---
### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[**TẠO BÁO CÁO CHUYÊN NGHIỆP HƠN**]
1. **Thêm Logo Công Ty**:
   - Sử dụng node **`Adjust HTML Colors`** (`code`) để chèn logo vào báo cáo.
   - Mẫu code:
     ```javascript
     $input.all().forEach(item => {
       item.json.html = item.json.html.replace('<!-- LOGO -->', '<img src="https://tên-file-logo.com/logo.png" width="150" />');
     });
     ```
2. **Gửi Báo Cáo Đến Slack/Telegram**:
   - Thêm node **`slackSend`** hoặc **`telegramSend`** sau **`Send Stock Analysis`** để thông báo kết quả.
3. **Lưu Log Dữ Liệu**:
   - Sử dụng node **`stickyNote`** để lưu lịch sử phân tích.
4. **Tự Động Cập Nhật API Key**:
   - Sử dụng node **`set`** để lưu API Key vào **n8n Context** và tránh phải nhập lại.
5. **Phân Tích Nhiều Cổ Phiếu Đồng Thời**:
   - Sử dụng node **`merge`** để kết hợp dữ liệu từ nhiều mã cổ phiếu vào một báo cáo duy nhất.

---
### 📌 **Kết Luận: Áp Dụng Ngay Để Đầu Tư Thông Minh Hơn!**
Workflow này là **giải pháp hoàn hảo** cho các nhà đầu tư, trader hoặc phân tích tài chính muốn:
✔ **Tiết kiệm thời gian** với báo cáo tự động hóa.
✔ **Nhận quyết định đầu tư dữ liệu hóa** từ AI.
✔ **Theo dõi thị trường 24/7** mà không cần can thiệp thủ công.

**Hành động ngay!**
1. **Import workflow** và cấu hình API Keys/SMTP.
2. **Chạy test** với mã cổ phiếu mẫu (ví dụ: `AAPL`).
3. **Bật Active** và **nhận báo cáo hàng tuần** vào email.

**⚠️ Lưu ý quan trọng:**
> Báo cáo này **không phải là lời khuyên đầu tư chính thức**. Luôn **tư vấn với chuyên gia tài chính** trước khi quyết định đầu tư.

---
### 🔗 **Tài Liệu Tham Khảo**
- [Tài liệu chính thức n8n](https://docs.n8n.io/)
- [Twelve Data API](https://twelvedata.com/)
- [Alpha Vantage API](https://www.alphavantage.co/)
- [Chart-img API](https://chart-img.com/)

**Chúc các sếp thành công với đầu tư thông minh!** 💰📈