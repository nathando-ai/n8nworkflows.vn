---
title: "🛡️ Tự Động Báo Cáo URL Spam & Phishing Từ Hộp Thư IMAP Sang Spamhaus (N8n)"
description: "Workflow tự động hóa 100% không code để quét, phân tích và báo cáo URL nguy hiểm từ email spam/phishing đến Spamhaus, giúp bảo vệ mạng lưới doanh nghiệp khỏi các cuộc tấn công mạng. Giảm thiểu thời gian phản ứng từ 24h xuống 0 giây."
slug: "tieu-dong-bao-cao-url-spam-phishing-imap-spamhaus"
tags: [n8n, automation, SecOps, email security, spamhaus, imap, no-code]
keywords: [n8n workflow spamhaus, tự động hóa báo cáo URL nguy hiểm, bảo mật email, quét phishing, tự động hóa SecOps, n8n imap]
---

# 🚀 **Tự Động Báo Cáo URL Spam & Phishing Từ IMAP Sang Spamhaus**

### **Giải pháp nào giúp các sếp:**
- **Tự động phát hiện và báo cáo** URL spam/phishing từ email trong thời gian thực?
- **Giảm thiểu rủi ro** từ các cuộc tấn công mạng thông qua việc loại bỏ URL nguy hiểm trước khi chúng gây hại?
- **Tiết kiệm thời gian** và công sức của đội ngũ IT phải thủ công kiểm tra từng email?

Workflow này là **công cụ tự động hóa SecOps** giúp các doanh nghiệp **quét, phân tích và báo cáo URL nguy hiểm** từ email spam/phishing đến **Spamhaus** — một trong những cơ sở dữ liệu URL đen uy tín nhất thế giới. Thay vì phải **quét thủ công hàng ngàn email** mỗi ngày, các sếp chỉ cần **cài đặt workflow này một lần**, và hệ thống sẽ **tự động xử lý mọi thứ** trong thời gian thực.

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên **VPS riêng** thay vì dùng phiên bản cloud.
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (đảm bảo tốc độ xử lý cao)
:::

---

## 🎯 **Kết quả các sếp nhận được**

:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tự động hóa 100%:** Không cần viết code, chỉ cần cấu hình IMAP và API Spamhaus.
✅ **Phát hiện URL nguy hiểm:** Quét và loại bỏ URL spam/phishing ngay từ nguồn gốc.
✅ **Giảm thiểu rủi ro:** Ngăn chặn các cuộc tấn công mạng trước khi chúng xảy ra.
✅ **Tiết kiệm thời gian:** Thay vì phải kiểm tra từng email, hệ thống làm việc **liên tục 24/7**.
✅ **Dễ mở rộng:** Thêm nhiều hộp thư IMAP hoặc logic xử lý mới mà không cần thay đổi logic chính.
:::

---

## 🔧 **Yêu cầu cần thiết**

Trước khi bắt đầu, các sếp cần chuẩn bị:
✔ **Tài khoản IMAP** (để kết nối với hộp thư spam/phishing).
✔ **API Key Spamhaus** (để gửi báo cáo URL nguy hiểm).
✔ **N8n self-hosted** (để workflow chạy liên tục).

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
Các sếp có thể **import workflow từ file JSON** hoặc **copy/paste JSON** vào **n8n Editor**.

🔹 **Cách import từ file JSON:**
1. Tải workflow từ [n8n.io/workflows/12846](https://n8n.io/workflows/12846).
2. Nhấn **Import** trong n8n Editor.
3. Chọn file JSON và **import**.

🔹 **Cách copy/paste JSON:**
1. Mở **n8n Editor**.
2. Nhấn **Import** → **Paste JSON**.
3. Dán JSON từ [n8n.io/workflows/12846](https://n8n.io/workflows/12846) và **import**.

---

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**

#### **🔹 Cấu hình IMAP (Phishing Trigger & Spam Trigger)**
- **Node:** `emailReadImap`
- **Cần thiết:**
  - **IMAP Server:** `imap.example.com` (thay bằng server của bạn).
  - **Port:** `993` (SSL) hoặc `143` (TLS).
  - **Username & Password:** Tài khoản email cần quét.
  - **Folder:** Chọn thư mục chứa email spam/phishing (ví dụ: `INBOX` hoặc `Spam`).

#### **🔹 Cấu hình Spamhaus API (Spamhaus submit url)**
- **Node:** `httpRequest`
- **Cần thiết:**
  - **API Key Spamhaus:** Mua tại [Spamhaus](https://www.spamhaus.org/).
  - **Endpoint:** `https://check.spamhaus.org/api/v2/check?ip={ip}` (hoặc `https://www.spamhaus.org/query/bl?bl={ip}`).
  - **Headers:**
    - `Authorization: Bearer {API_KEY}`
    - `Content-Type: application/json`

#### **🔹 Cấu hình logic xử lý (initial config spam & initial phish config)**
- **Node:** `set`
- **Cần thiết:**
  - **Threat Type:** Chọn `spam` hoặc `phishing`.
  - **Reason:** Ghi chú lý do báo cáo (ví dụ: "URL chứa trong email spam").

#### **🔹 Cấu hình regex để lọc URL (filter out URLs that match regexes)**
- **Node:** `filter`
- **Cần thiết:**
  - **Regex để loại bỏ URL không cần thiết:**
    - `https?://(?:www\.)?facebook\.com` (Facebook)
    - `https?://(?:www\.)?google\.com` (Google)
    - `https?://(?:www\.)?youtube\.com` (YouTube)
  - **Regex để giữ URL nguy hiểm:**
    - `https?://(?:www\.)?malicious-site\.com` (URL có dấu hiệu nguy hiểm)

#### **🔹 Xử lý trùng lặp (de-duplicate URLs)**
- **Node:** `removeDuplicates`
- **Cần thiết:**
  - **Key:** `url` (để tránh gửi cùng một URL nhiều lần).

---

### **3. Kích hoạt ⚡️**
1. **Test run** với một email mẫu để kiểm tra logic.
2. **Bật Active workflow** để nó chạy tự động.

---

## ✍️ **Mẹo & gợi ý nâng cao**

🔹 **Kết hợp với Slack/Telegram để báo cáo kết quả:**
- Thêm **node `webhook`** để gửi thông báo khi URL nguy hiểm được báo cáo.

🔹 **Lưu log để theo dõi:**
- Thêm **node `stickyNote`** để ghi lại URL đã báo cáo.

🔹 **Gửi báo cáo định kỳ:**
- Thêm **node `schedule`** để gửi báo cáo tổng hợp hàng tuần.

🔹 **Tăng cường logic phân loại:**
- Sử dụng **node `code`** để thêm logic phân tích sâu hơn (ví dụ: kiểm tra domain nguy hiểm).

---

## 📌 **Kết luận**

Workflow này là **giải pháp hoàn hảo** cho các doanh nghiệp muốn **tự động hóa bảo mật email** và **ngăn chặn URL spam/phishing** một cách hiệu quả. **Không cần code**, chỉ cần **cấu hình IMAP và API Spamhaus**, và hệ thống sẽ **làm việc 24/7** để bảo vệ mạng lưới của các sếp.

👉 **Hãy áp dụng ngay để bảo vệ doanh nghiệp của mình!** 🚀

---
**Nếu có vấn đề, hãy liên hệ với chúng tôi qua [n8n Community](https://community.n8n.io/)** để được hỗ trợ!**