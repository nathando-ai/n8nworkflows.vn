---
title: "🤖 Trợ lý tri thức cá nhân: Trích xuất & Tóm tắt tự động từ YouTube/Article qua Telegram + Google Sheets"
description: "Workflow tự động hóa 100% không code giúp các sếp trích xuất nội dung từ video YouTube hoặc bài viết, tóm tắt bằng AI Gemini, lưu trữ trên Google Sheets và truy vấn nhanh qua Telegram. Giúp tiết kiệm thời gian nghiên cứu lên đến 80%!"
slug: "tro-ly-tri-thuc-ca-nhan-tu-dong-hoa-youtube-telegram"
tags: [n8n, automation, personal-productivity, ai-gemini, google-sheets, telegram-bot]
keywords: [n8n workflow tự động hóa, trích xuất nội dung YouTube, tóm tắt bài viết bằng AI, lưu trữ Google Sheets, truy vấn thông tin qua Telegram]
---

# 🚀 **Trợ lý Tri thức Cá nhân: Tóm tắt & Lưu trữ thông tin từ YouTube/Article qua Telegram**

## **💡 Giải pháp cho vấn đề gì?**
Các sếp thường phải mất **giờ đồng hồ** để:
- **Tìm kiếm** và đọc video YouTube dài hàng giờ để tìm thông tin cần thiết.
- **Tóm tắt** bài viết dài 10 trang thành những điểm chính.
- **Lưu trữ** và **tìm kiếm lại** thông tin sau này một cách hiệu quả.

**Workflow này tự động hóa toàn bộ quá trình!** Chỉ cần gửi **link YouTube hoặc bài viết** vào Google Sheets, AI sẽ:
✅ **Trích xuất** nội dung chính từ video/đoạn văn.
✅ **Tóm tắt** bằng **Google Gemini** (AI tiên tiến nhất hiện nay).
✅ **Lưu trữ** kết quả vào Google Sheets.
✅ **Truy vấn** thông tin nhanh chóng qua **Telegram Bot**.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow hoạt động **24/7** mà không bị gián đoạn, các sếp nên **self-host n8n** trên VPS.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần đọc toàn bộ video/đoạn văn, chỉ cần AI tóm tắt.
- **Truy vấn nhanh**: Gửi tin nhắn Telegram, AI trả lời ngay từ kho dữ liệu.
- **Lưu trữ thông minh**: Tất cả dữ liệu được **sắp xếp, tóm tắt và lưu trữ** trên Google Sheets.
- **Hoạt động liên tục**: Workflow chạy tự động **mỗi khi có dữ liệu mới** vào Google Sheets.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
✔ **Tài khoản Telegram Bot** (để nhận và gửi tin nhắn tự động).
✔ **API Key của Google Gemini** (để sử dụng AI tóm tắt).
✔ **Google Sheets** (để lưu trữ dữ liệu, cần chia sẻ quyền cho n8n).
✔ **API Token của Apify** (để trích xuất transcript YouTube, **không bắt buộc** nếu chỉ làm với bài viết).

---
## **🚀 Cách import & Cấu hình workflow**

### **1️⃣ Import Workflow từ file JSON**
- Tải file JSON từ [n8n.io/workflows/7215](https://n8n.io/workflows/7215).
- Trong **n8n Editor**, nhấn **Import Workflow** và chọn file JSON.
- **Hoặc** copy toàn bộ JSON và dán vào **Import Workflow** (tab "Import").

### **2️⃣ Cấu hình các node quan trọng (BẮT BUỘC chỉnh!)**

#### **🔹 Node Telegram Trigger (Bắt đầu workflow)**
- **Credentials**: Chọn `telegramApi` (đã cấu hình trước khi import).
- **Chat ID**: Nhập ID chat của Telegram Bot (có thể lấy từ [@userinfobot](https://t.me/userinfobot)).
- **Command**: Để trống (workflow sẽ phản ứng với tất cả tin nhắn).

#### **🔹 Node Google Sheets Trigger (Lắng nghe dữ liệu mới)**
- **Credentials**: Chọn `googleSheetsTriggerOAuth2Api`.
- **Sheet Name**: Chọn **Sheet2** (đây là sheet chứa link YouTube/Article).
- **Trigger Type**: Chọn **"Row added"** (hoặc **"Row updated"**).

#### **🔹 Node Google Gemini Chat Model (AI Tóm tắt)**
- **Credentials**: Chọn `googlePalmApi` (đã cấu hình API Key Gemini).
- **Model**: Chọn **"gemini-pro"** (mô hình mạnh nhất).
- **Prompt**: Để mặc định (n8n sẽ tự động điều chỉnh).

#### **🔹 Node HTTP Request (Trích xuất transcript YouTube - OPTIONAL)**
- **URL**: Thay thế `YOUR_APIFY_TOKEN` bằng token Apify của bạn.
- **Headers**: Thêm `Authorization: Bearer YOUR_APIFY_TOKEN`.
- **Nếu không dùng YouTube**: Bỏ qua node này và chuyển dữ liệu từ **HTTP Request1** (trích xuất từ bài viết).

#### **🔹 Node Google Sheets (Lưu dữ liệu tóm tắt)**
- **Credentials**: Chọn `googleSheetsOAuth2Api`.
- **Sheet Name**: Chọn **Sheet1** (đây là sheet lưu kết quả tóm tắt).
- **Operation**: Để mặc định (`append` hoặc `appendOrUpdate`).

#### **🔹 Node Send a text message (Trả lời Telegram)**
- **Credentials**: Chọn `telegramApi`.
- **Chat ID**: Nhập ID chat của Telegram Bot.
- **Text**: Sử dụng **Markdown** để định dạng tin nhắn trả lời.

---

### **3️⃣ Kích hoạt workflow**
1. **Test Run** với dữ liệu mẫu:
   - Gửi **link YouTube** hoặc **bài viết** vào **Sheet2**.
   - Kiểm tra **Sheet1** xem có dữ liệu tóm tắt mới không.
   - Gửi tin nhắn Telegram để kiểm tra phản hồi AI.
2. **Bật Active** workflow.

---

## **✍️ Mẹo & gợi ý nâng cao**

### **🔹 Kết hợp với Slack/Telegram để thông báo**
- Thêm node **Slack** hoặc **Telegram** để gửi thông báo khi có dữ liệu mới.
- Ví dụ: Khi AI hoàn thành tóm tắt, gửi tin nhắn **"Đã tóm tắt xong! Kết quả ở Sheet1"** qua Telegram.

### **🔹 Lưu log hoạt động**
- Thêm node **Sticky Note** để ghi lại lịch sử hoạt động (giúp debug dễ dàng).
- Ví dụ: `"[2024-05-20] Trích xuất video: [Link] → Tóm tắt: [Nội dung]"`.

### **🔹 Tự động gửi báo cáo định kỳ**
- Sử dụng **Google Sheets Trigger** để chạy workflow hàng ngày.
- Ví dụ: **"Mỗi sáng 7h, AI tóm tắt tất cả link mới trong Sheet2 và gửi báo cáo qua Telegram."**

### **🔹 Cải thiện prompt AI**
- Thay đổi **prompt** trong node **Google Gemini** để AI trả lời chính xác hơn.
- Ví dụ:
  ```plaintext
  "Tóm tắt video/đoạn văn này thành 3 điểm chính, không quá 200 từ. Nếu có thông tin quan trọng, hãy nhấn mạnh."
  ```

---

## **📌 Kết luận**
Workflow này là **công cụ tự động hóa tri thức cá nhân hoàn hảo** cho các sếp:
✔ **Tiết kiệm thời gian** khi nghiên cứu.
✔ **Truy vấn thông tin nhanh** qua Telegram.
✔ **Lưu trữ thông minh** trên Google Sheets.

**Hãy áp dụng ngay để không phải mất thời gian đọc toàn bộ video/đoạn văn nữa!** 🚀

---
**💬 Cần hỗ trợ?** Đăng ký **VPS n8n** trên [TinoHost](https://tino.vn/vps-n8n?affid=388) để workflow chạy 24/7 mà không lo gián đoạn!