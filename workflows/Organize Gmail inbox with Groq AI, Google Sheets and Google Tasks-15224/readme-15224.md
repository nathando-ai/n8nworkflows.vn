---
title: "🤖 Tự Động Hóa Inbox Gmail Với AI Groq, Google Sheets & Google Tasks - Sắp Xếp Email Như Bác Sĩ"
description: "Workflow tự động phân loại, nhãn và quản lý email Gmail bằng AI Groq, đồng thời ghi log vào Google Sheets và tạo nhiệm vụ tự động trên Google Tasks. Giúp các sếp tiết kiệm 10+ giờ/tuần và giảm thiểu rủi ro bỏ qua tin nhắn quan trọng."
slug: "tu-dong-hoa-gmail-voi-groq-google-sheets-google-tasks"
tags: [n8n, automation, gmail, google-sheets, google-tasks, ai-summarization, groq-ai]
keywords: [tự động hóa gmail, phân loại email bằng ai, groq ai n8n, quản lý email tự động, google sheets log email, google tasks tự động]
---

# 🚀 **Tự Động Hóa Inbox Gmail Của Các Sếp Với AI Groq, Google Sheets & Google Tasks**

### **📧 Nỗi Đau Của Các Sếp Hiện Nay**
Hàng ngày, các sếp phải mất **30-60 phút** để:
- **Lọc và nhãn** hàng trăm email từ Work, Finance, Personal đến Newsletter.
- **Bỏ qua** những tin nhắn quan trọng trong "All Mail" vì quá nhiều spam.
- **Ghi chép thủ công** vào Google Sheets để theo dõi lịch sử giao dịch, hợp đồng hoặc yêu cầu của khách hàng.
- **Quên** tạo nhiệm vụ cho những email cần xử lý sau (ví dụ: thanh toán, hợp đồng ký kết).

**Kết quả?** Email trở thành "đống rác" không quản lý được, làm giảm hiệu suất và tăng stress.

---
### **🎯 Kết Quả Các Sếp Nhận Được**
Sau khi áp dụng workflow này, các sếp sẽ:
✅ **Tiết kiệm 10+ giờ/tuần** bằng cách tự động phân loại và nhãn email.
✅ **Không bỏ qua email quan trọng** nhờ AI Groq phân loại chính xác (Work, Finance, Personal, Newsletter).
✅ **Ghi log tự động** tất cả email vào Google Sheets với thông tin chi tiết (người gửi, chủ đề, danh mục, thời gian).
✅ **Tạo nhiệm vụ tự động** cho email liên quan đến tài chính (ví dụ: thanh toán, hợp đồng) trên Google Tasks.
✅ **Inbox luôn sạch sẽ** nhờ nhãn tự động và email được chuyển đến folder phù hợp.

---
### **🔧 Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
📌 **Tài khoản và API Key:**
- **Gmail OAuth2** (để đọc và nhãn email).
- **Google Sheets OAuth2** (để ghi log dữ liệu).
- **Google Tasks OAuth2** (để tạo nhiệm vụ tự động).
- **Groq API Key** (để sử dụng mô hình AI `openai/gpt-oss-20b`).

📌 **Cấu hình trước:**
- **Tạo 4 nhãn Gmail** (Work, Personal, Finance, Newsletter) trong Gmail.
- **Chuẩn bị Google Sheet** với các cột: **Sender, Subject, Category, Timestamp**.
- **Cài đặt n8n** trên VPS (Self-hosted) để workflow hoạt động 24/7.

---
### **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể:
- **Tải file JSON** từ [n8n.io/workflows/15224](https://n8n.io/workflows/15224) và import vào n8n Editor.
- **Copy/Paste JSON** từ trang trên vào n8n và nhấn **"Import Workflow"**.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này gồm **13 node** quan trọng, các sếp cần chú ý đến:

##### **🔹 Node "Watch Incoming Emails" (gmailTrigger)**
- **Chọn credentials:** `gmailOAuth2`.
- **Cấu hình:** Chọn **"Label"** là `All Mail` để bắt tất cả email mới.

##### **🔹 Node "AI Agent - Classify Email Category" (agent)**
- **Model AI:** `openai/gpt-oss-20b` (Groq).
- **Prompt mặc định:**
  ```json
  "Analyze the email content and classify it into one of these categories: Work, Personal, Finance, or Newsletter. Return only the category name."
  ```
  - **Lưu ý:** Nếu muốn cải thiện độ chính xác, các sếp có thể **tùy chỉnh prompt** bằng cách thêm ví dụ cụ thể (ví dụ: "Email từ ngân hàng là Finance, email từ khách hàng là Work").

##### **🔹 Node "Route Based on Category" (switch)**
- **Cấu hình điều kiện:**
  - **Work** → Áp dụng nhãn `Work` và ghi log vào Google Sheets.
  - **Personal** → Áp dụng nhãn `Personal` và ghi log.
  - **Finance** → Áp dụng nhãn `Finance`, ghi log **và** tạo nhiệm vụ trên Google Tasks.
  - **Newsletter** → Áp dụng nhãn `Newsletter` và ghi log.

##### **🔹 Node "Log data to Google Sheets" (googleSheets)**
- **Chọn Sheet và Range:** Đảm bảo cột `Category` được định dạng là **Text**.
- **Operation:** `append` (thêm dữ liệu mới vào cuối sheet).

##### **🔹 Node "Create Review Mail Task" (googleTasks)**
- **Chỉ áp dụng cho danh mục Finance.**
- **Tùy chỉnh tiêu đề nhiệm vụ:**
  ```json
  "Review email: {{$node["Normalize Email Fields"].json["subject"]}} (Finance)"
  ```

##### **🔹 Node "Apply [Label]"** (gmail)
- **Đảm bảo tên nhãn trong node khớp với nhãn đã tạo trong Gmail.**
- **Ví dụ:** Nếu nhãn trong Gmail là `Tài Chính` nhưng node đặt `Finance`, email sẽ **không được nhãn** và workflow sẽ lỗi.

#### **3. Kích Hoạt ⚡️**
- **Test Run:** Chạy với **1-2 email mẫu** để kiểm tra AI phân loại chính xác.
- **Bật Active:** Sau khi kiểm tra, nhấn **"Active"** để workflow hoạt động liên tục.

---
### **✍️ Mẹo & Gợi Ý Nâng Cao**
1. **Tăng độ chính xác của AI:**
   - Thêm **ví dụ cụ thể** vào prompt của Groq (ví dụ: "Email từ ngân hàng là Finance, email từ khách hàng là Work").
   - Sử dụng **các keyword điển hình** (ví dụ: "thanh toán", "hợp đồng", "quyết toán" → Finance).

2. **Gửi báo cáo định kỳ:**
   - Sử dụng **n8n + Google Sheets + Email Node** để gửi **báo cáo tổng hợp** hàng tuần về số lượng email theo danh mục.

3. **Kết hợp với Slack/Telegram:**
   - Thêm **node Slack/Telegram** để thông báo khi có email Finance mới (ví dụ: "Có email tài chính mới cần review").

4. **Lưu log chi tiết hơn:**
   - Thêm cột **`Email Body (Trích Lược)`** vào Google Sheets bằng cách sử dụng **Groq AI tóm tắt** trước khi ghi log.

5. **Tự động xóa email sau xử lý:**
   - Thêm **node Gmail "Delete Email"** sau khi đã nhãn và ghi log để giữ inbox sạch sẽ.

---
### **📌 Kết Luận**
Workflow này **giải quyết triệt để** vấn đề email rối loạn của các sếp bằng cách:
✔ **Tự động phân loại** bằng AI Groq (độ chính xác cao).
✔ **Nhãn và sắp xếp** email vào folder phù hợp.
✔ **Ghi log tự động** vào Google Sheets.
✔ **Tạo nhiệm vụ** cho email quan trọng (tài chính).
✔ **Hoạt động 24/7** mà không cần can thiệp thủ công.

**🚀 Hành động ngay:**
1. **Cài đặt n8n trên VPS** (đăng ký [VPS TinoHost](https://tino.vn/vps-n8n?affid=388) với mã giảm giá **VPSN8N**).
2. **Import workflow** và cấu hình theo hướng dẫn.
3. **Bật Active** và **quên đi việc sắp xếp email thủ công!**

---
**💡 Lời khuyên cuối cùng:**
Nếu workflow không hoạt động như mong đợi, các sếp có thể **tùy chỉnh prompt của Groq** hoặc **thêm các rule logic** trong node `switch` để phù hợp với email của riêng mình. **Hãy thử nghiệm và tối ưu hóa!** 🚀