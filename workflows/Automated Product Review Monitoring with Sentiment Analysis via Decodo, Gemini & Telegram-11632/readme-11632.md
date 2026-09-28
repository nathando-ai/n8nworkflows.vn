---
title: "🚀 Tự Động Hóa Theo Dõi Đánh Giá Sản Phẩm Với Phân Tích Sentiment AI (Decodo + Gemini + Telegram Alert)"
description: "Workflow tự động hóa 24/7 theo dõi đánh giá sản phẩm trên Amazon, phân tích cảm xúc (sentiment) bằng AI Gemini, gửi cảnh báo Telegram tự động - giúp các sếp tiết kiệm thời gian và cải thiện chiến lược sản phẩm mà không cần viết code."
slug: "tieu-dong-hoa-theo-doi-danh-gia-san-pham-ai-sentiment"
tags: [n8n, automation, no-code, ai-summarization, market-research, telegram-alert, google-sheets, decodo]
keywords: [tự động hóa theo dõi đánh giá sản phẩm, phân tích sentiment ai, n8n workflow amazon review, cảnh báo telegram tự động, google sheets + gemini, decodo scraper]
---

# 🚀 **Tự Động Hóa Theo Dõi Đánh Giá Sản Phẩm Với Phân Tích Sentiment AI (Decodo + Gemini + Telegram Alert)**

### **Nỗi Đau Của Các Sếp Khi Theo Dõi Đánh Giá Sản Phẩm Thủ Công**
Hàng ngày, các sếp phải:
- **Quét thủ công** hàng chục trang đánh giá trên Amazon, Shopee, Lazada...
- **Tóm tắt nội dung** dài dòng của khách hàng để đưa ra quyết định cải thiện sản phẩm.
- **Phân tích cảm xúc** (positive/negative) của khách hàng một cách chủ quan, dễ bỏ lỡ điểm quan trọng.
- **Bị mất thời gian** để cập nhật lại thông tin, dẫn đến phản hồi chậm trễ với khách hàng.

**Workflow này giải quyết tất cả!** Với **AI Gemini + Decodo Scraper**, n8n sẽ tự động:
✅ **Lấy dữ liệu** từ URL sản phẩm trên Amazon.
✅ **Phân tích sentiment** (tích cực/ trung tính/ tiêu cực) bằng AI.
✅ **Tóm tắt nội dung** đánh giá dài dòng thành văn bản ngắn gọn.
✅ **Gửi cảnh báo Telegram** khi có đánh giá tiêu cực mới.
✅ **Lưu lịch sử** tất cả đánh giá vào Google Sheets để phân tích dài hạn.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7**, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để tránh giới hạn của n8n Cloud.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới **39%**)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ/tuần** theo dõi đánh giá thủ công.
- **Phân tích sentiment chính xác** bằng AI Gemini, không còn chủ quan.
- **Cảnh báo Telegram tự động** khi có đánh giá tiêu cực mới.
- **Lưu trữ lịch sử** tất cả đánh giá vào Google Sheets, dễ dàng phân tích xu hướng.
- **Cải thiện sản phẩm** dựa trên phản hồi khách hàng thực tế.
- **Hoạt động 24/7** mà không cần can thiệp thủ công.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi chạy workflow, các sếp cần chuẩn bị:
✔ **Tài khoản Decodo API** (để scraper dữ liệu đánh giá Amazon).
✔ **Google Sheets** với:
   - **1 sheet** chứa danh sách URL sản phẩm (một URL/row).
   - **1 sheet khác** để lưu kết quả phân tích (tên sheet: **"user review aggregations"**).
✔ **Google Gemini API** (để phân tích sentiment và tóm tắt nội dung).
✔ **Tài khoản Telegram** (để nhận cảnh báo tự động).
✔ **Credentials OAuth 2.0** cho Google Sheets (để n8n có quyền đọc/giới thiệu dữ liệu).

---
:::note[LƯU Ý QUYỀN HẠN]
- **Decodo API** có giới hạn scraper (check [Decodo Docs](https://decodo.com/docs)).
- **Google Sheets** phải cho phép **n8n có quyền truy cập** (cài đặt trong **Settings > Add-ons > n8n**).
- **Telegram Bot Token** phải được tạo trước (hướng dẫn [đây](https://core.telegram.org/bots/api#creating-a-new-bot)).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có **2 cách** để import:
- **Tải file JSON** từ [n8n.io/workflows/11632](https://n8n.io/workflows/11632) và import vào **n8n Editor**.
- **Copy JSON** từ link trên và **paste** vào **n8n Editor** (tab **Import/Export**).

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow gồm **10 node** quan trọng, các sếp phải cấu hình kỹ như sau:

##### **🔹 Node 1: Schedule Trigger (Đặt lịch chạy)**
- **Thiết lập thời gian chạy** (ví dụ: **09:00 AM hàng ngày**).
- **Chọn "Active"** để workflow bắt đầu chạy tự động.

##### **🔹 Node 2: Decodo (Scraper Dữ Liệu Đánh Giá)**
- **Credentials**: Chọn `decodoApi` (đã cấu hình trước).
- **Operation**: Đặt là `amazon`.
- **Input**: N8n sẽ tự động lấy **URL sản phẩm** từ **Google Sheets** (node sau).

##### **🔹 Node 3: Get row(s) in sheet (Lấy URL từ Google Sheets)**
- **Credentials**: Chọn `googleSheetsOAuth2Api`.
- **Sheet Name**: Đặt là **tên sheet chứa URL sản phẩm** (ví dụ: `"Product URLs"`).
- **Range**: Chọn toàn bộ sheet (`"Sheet1!A:Z"`).
- **Output**: N8n sẽ lấy **một URL/row** và gửi vào **Loop Over Items** (node sau).

##### **🔹 Node 4: Loop Over Items (Lặp qua từng URL)**
- **Split Mode**: Chọn `Batch` (để xử lý từng URL một).
- **Batch Size**: Đặt là `1` (mỗi lần xử lý 1 URL).

##### **🔹 Node 5: Code (JavaScript) - Chuyển JSON thành Text**
- **Mã JavaScript** (sẵn trong workflow) sẽ chuyển dữ liệu từ Decodo thành **dạng text đơn giản**:
  ```javascript
  // Ví dụ: "<Tên Khách Hàng> – <Đánh Giá> – <Nội Dung>"
  return {
    text: `${item.reviewerName} – ${item.rating}/5 – ${item.content}`
  };
  ```
- **Lưu ý**: Nếu Decodo trả về dữ liệu khác, các sếp phải **sửa mã** để phù hợp.

##### **🔹 Node 6: Sentiment Analyzer (Phân Tích Cảm Xúc)**
- **Credentials**: Chọn `googlePalmApi` (API Gemini).
- **Model**: Chọn `gemini-pro` (hoặc `text-bison` nếu không có).
- **Prompt**: Sẵn trong workflow, nhưng các sếp có thể **tùy chỉnh** để phù hợp:
  ```plaintext
  Analyze sentiment of this review: "{text}". Return "positive", "neutral", or "negative".
  ```
- **Output**: N8n sẽ trả về **sentiment** (tích cực/trung tính/t tiêu cực).

##### **🔹 Node 7: Summarize Reviews (Tóm Tắt Nội Dung)**
- **Credentials**: Chọn `googlePalmApi`.
- **Model**: Chọn `gemini-pro`.
- **Prompt**: Tóm tắt nội dung đánh giá thành **1-2 câu ngắn gọn**.
- **Output**: Văn bản tóm tắt sẵn sàng gửi Telegram.

##### **🔹 Node 8: Alert Group (Gửi Cảnh Báo Telegram)**
- **Credentials**: Chọn `telegramApi`.
- **Chat ID**: Đặt là **ID chat cá nhân** (các sếp có thể lấy bằng cách gửi tin nhắn cho bot Telegram và copy ID từ link).
- **Message**: Sẽ hiển thị:
  ```
  🚨 **New Negative Review Alert!**
  Product: [URL]
  Review: "{text}"
  Sentiment: "{sentiment}"
  Summary: "{summary}"
  ```

##### **🔹 Node 9: Store to Sheet (Lưu Kết Quả vào Google Sheets)**
- **Credentials**: Chọn `googleSheetsOAuth2Api`.
- **Sheet Name**: Đặt là **"user review aggregations"**.
- **Operation**: Chọn `append` (thêm mới).
- **Columns**: Các sếp phải **đặt tên cột** phù hợp với dữ liệu:
  - `Product URL`, `Review Text`, `Sentiment`, `Summary`, `Timestamp`.

---
#### **3. Kích Hoạt ⚡️ Workflow**
- **Test Run**: Chạy **manual** với **1 URL mẫu** để kiểm tra.
- **Active**: Đặt **Schedule Trigger** thành **Active** để workflow chạy tự động hàng ngày.

---
### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Thêm Node Slack Alert** (nếu muốn cảnh báo trên Slack thay vì Telegram).
2. **Lưu Log vào Google Drive** (để backup dữ liệu).
3. **Tự động gửi báo cáo hàng tuần** bằng **Google Sheets + Email**.
4. **Phân tích xu hướng** bằng **Google Data Studio** (nối với Google Sheets).
5. **Tự động gửi phản hồi** cho khách hàng tiêu cực (nếu kết hợp với **Email Node**).

---
### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp để tập trung vào **chiến lược sản phẩm** thay vì theo dõi đánh giá thủ công. Với **AI Gemini + Decodo**, n8n sẽ:
✔ **Tự động scraper** dữ liệu đánh giá.
✔ **Phân tích sentiment** chính xác.
✔ **Tóm tắt nội dung** dài dòng.
✔ **Gửi cảnh báo Telegram** khi có vấn đề.
✔ **Lưu lịch sử** để phân tích dài hạn.

**Hành động ngay!** Import workflow này và **cải thiện sản phẩm của mình** chỉ trong vài phút. 🚀

---
**🔗 [Tải Workflow Mẫu](https://n8n.io/workflows/11632)**
**📌 [Cài Đặt n8n Self-Hosted](https://docs.n8n.io/hosting/installation/)**