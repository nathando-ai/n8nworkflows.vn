---
title: "🚀 Tự Động Hóa Tạo & Phát Tán Tin Tức & Bài Đăng LinkedIn Từ WordPress Với AI Gemini, Google Sheets & Gmail"
description: "Workflow tự động hóa 100% không code giúp các sếp lấy nội dung từ WordPress, xử lý bằng AI Gemini, sau đó tự động đăng lên LinkedIn và gửi newsletter cá nhân hóa cho khách hàng qua Gmail. Giảm thời gian làm thủ công từ 2-3 tiếng/tháng xuống chỉ 5 phút/ngày!"
slug: "tu-dong-hoa-tao-newsletter-linkedin-tu-wordpress"
tags: [n8n, automation, ai-gemini, content-automation, social-media, google-sheets, gmail, linkedin]
keywords: [n8n workflow tự động hóa tin tức, AI Gemini tự động viết newsletter, tự động đăng LinkedIn từ WordPress, tự động hóa content marketing, n8n + Google Sheets + Gmail]
---

# 🚀 **Tự Động Hóa Tạo & Phát Tán Tin Tức & Bài Đăng LinkedIn Từ WordPress Với AI**

## **Nỗi Đau Của Các Sếp Hiện Nay**
Các sếp thường phải:
✅ **Lấy nội dung** từ WordPress (blog, bài viết mới) và **chuyển đổi** thành tin tức LinkedIn + newsletter.
✅ **Làm thủ công** việc viết teaser, cá nhân hóa email, và đăng lên LinkedIn → **Tốn 2-3 tiếng/tháng**.
✅ **Lo ngại trùng lặp** nội dung đã đăng trước → Phải kiểm tra thủ công.
✅ **Không có thời gian** để tối ưu hóa nội dung cho từng kênh (LinkedIn vs. Email).

**Workflow này giải quyết tất cả!** Sử dụng **AI Gemini** để tự động viết teaser LinkedIn và newsletter, **Google Sheets** để theo dõi nội dung đã xử lý, và **Gmail** để gửi email cá nhân hóa cho khách hàng.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian** (từ 2-3 tiếng/tháng xuống chỉ 5 phút/ngày).
- **Nội dung tự động cá nhân hóa** cho từng người nhận (email) và teaser LinkedIn.
- **Không trùng lặp nội dung** (dùng Google Sheets theo dõi ID bài viết đã xử lý).
- **Hoạt động 24/7** (không cần can thiệp thủ công).
- **Tăng engagement** với khách hàng qua LinkedIn và email tự động.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi chạy workflow, các sếp cần chuẩn bị:
✔ **Tài khoản WordPress** (API endpoint để lấy bài viết mới).
✔ **Google Sheets** với:
   - **Sheet "LastProcessedID"** (để lưu ID bài viết đã xử lý).
   - **Sheet "Email List"** (danh sách email khách hàng để gửi newsletter).
✔ **API Key Google Gemini** (để AI viết teaser và newsletter).
✔ **Tài khoản LinkedIn** (để đăng bài tự động).
✔ **Tài khoản Gmail** (để gửi email tự động).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Cách 1:** Tải file JSON từ [n8n.io/workflows/14525](https://n8n.io/workflows/14525) và import vào n8n Editor.
- **Cách 2:** Copy toàn bộ JSON và dán vào **Import Workflow** trong n8n.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow gồm **13 node**, các sếp cần chú ý cấu hình sau:

##### **🔹 Node "HTTP Request" (Lấy bài viết từ WordPress)**
- **URL:** Điền vào `Request URL` (ví dụ: `https://tên-blog.com/wp-json/wp/v2/posts?per_page=10`).
- **Headers:** Thêm `Authorization: Bearer {API_KEY_WORDPRESS}` (nếu cần).

##### **🔹 Node "Google Sheets" (Last ID & Email List)**
- **Sheet "LastProcessedID":**
  - **Range:** `Sheet1!A1` (để lưu ID bài viết mới nhất đã xử lý).
  - **Operation:** `update` (để cập nhật ID sau khi xử lý).
- **Sheet "Email List":**
  - **Range:** `Sheet1!A1:B100` (danh sách email + tên người nhận).

##### **🔹 Node "Google Gemini Chat Model" (AI Viết Teaser & Newsletter)**
- **API Key:** Điền vào `Google API Key` (mua trên [Google Cloud](https://cloud.google.com/vertex-ai)).
- **Prompt:** Sẵn sàng trong node, nhưng các sếp có thể chỉnh sửa để phù hợp với brand.

##### **🔹 Node "LinkedIn" (Đăng bài tự động)**
- **Credentials:** Chọn `LinkedIn` trong `Authentication` và đăng nhập.
- **Post Format:** Sử dụng `{{ $json["linkedin_teaser"] }}` (được AI viết).

##### **🔹 Node "Gmail" (Gửi email cá nhân hóa)**
- **Credentials:** Chọn `Gmail` và đăng nhập.
- **Template:** Sử dụng `{{ $json["newsletter_content"] }}` (được AI viết).

##### **🔹 Node "Schedule Trigger" (Chạy tự động hàng ngày)**
- **Cron:** Đặt `0 0 * * *` (chạy lúc 00:00 hàng ngày).

#### **3. Kích Hoạt ⚡️**
- **Test Run:** Chạy thử với 1 bài viết mẫu để kiểm tra.
- **Active Workflow:** Bật `Active` và để chạy tự động.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Thêm Logs & Monitoring:**
   - Sử dụng **Sticky Note** để ghi lại lỗi hoặc trạng thái xử lý.
   - Kết hợp với **Slack/Telegram** để báo cáo lỗi (thêm node `webhook` + `slack`).

2. **Tối Ưu Email:**
   - Thêm **dynamic content** (ví dụ: `{{ $json["customer_name"] }}`) để cá nhân hóa hơn.

3. **Xử Lý Lỗi:**
   - Thêm **node `if`** để kiểm tra lỗi và gửi thông báo Slack nếu AI viết sai.

4. **Kết Hợp với CRM:**
   - Nếu dùng **HubSpot/ActiveCampaign**, có thể lấy danh sách email từ đó thay vì Google Sheets.

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp để tập trung vào chiến lược content chứ không phải làm thủ công. **Chỉ cần 5 phút/ngày** để setup và sau đó **AI làm tất cả**!

🚀 **Hành động ngay:**
1. **Setup VPS** (n8n Self-hosted) để workflow chạy 24/7.
2. **Import workflow** và cấu hình theo hướng dẫn.
3. **Chạy thử** và xem kết quả!

**Nếu có vấn đề, comment bên dưới hoặc liên hệ với [iTechNotion](https://itechnotion.com) để hỗ trợ!** 💡