---
title: "🚀 Tự Động Hóa Bài Đăng Trên 9 Mạng Xã Hội Từ Google Sheets – Không Cần Code!"
description: "Workflow tự động hóa hoàn chỉnh để đăng bài lên TikTok, Instagram, Facebook, LinkedIn, Twitter, Threads, Bluesky, YouTube và Pinterest chỉ với 1 lần setup. Giúp tiết kiệm thời gian lên đến 20 giờ/tuần và tăng cường sự hiện diện trên mạng xã hội 24/7."
slug: "tieu-dong-hoa-dang-bai-9-mang-xa-hoi"
tags: [n8n, automation, social-media, google-sheets, blotato, no-code, ai-marketing]
keywords: [tự động hóa mạng xã hội, đăng bài tự động n8n, blotato api, google sheets tự động, tự động hóa instagram tiktok]
---

# 🚀 **Tự Động Hóa Bài Đăng Trên 9 Mạng Xã Hội Từ Google Sheets – Không Cần Code!**

### **Giải pháp cho các sếp muốn tiết kiệm thời gian, tăng hiệu suất và tự động hóa toàn bộ chiến dịch mạng xã hội**

Hiện nay, việc đăng bài lên **9 mạng xã hội khác nhau** như TikTok, Instagram, Facebook, LinkedIn, Twitter, Threads, Bluesky, YouTube và Pinterest thường tốn thời gian và công sức của các sếp. Thay vì mất **20 giờ/tuần** để đăng bài thủ công, bạn có thể **tự động hóa toàn bộ quy trình** chỉ với **một workflow n8n** kết hợp **Google Sheets, Google Drive và Blotato API**.

Workflow này sẽ:
✅ **Lấy dữ liệu bài đăng từ Google Sheets** (cập nhật tự động)
✅ **Tải lên hình ảnh/video từ Google Drive** (đã công khai)
✅ **Đăng bài lên 9 mạng xã hội** (TikTok, Instagram, Facebook, LinkedIn, Twitter, Threads, Bluesky, YouTube, Pinterest)
✅ **Cập nhật trạng thái "Đã đăng" tự động** trên Google Sheets
✅ **Chạy định kỳ mỗi 3 giờ** để không làm spam

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo tính riêng tư và hiệu suất cao.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần đăng bài thủ công hàng ngày.
- **Tăng hiệu suất**: Đăng bài lên **9 mạng xã hội cùng lúc** chỉ với 1 lần setup.
- **Tự động hóa hoàn toàn**: Workflow chạy định kỳ **mỗi 3 giờ** để không làm spam.
- **Cập nhật trạng thái tự động**: Bài đăng được đánh dấu **"Đã đăng"** trên Google Sheets.
- **Hỗ trợ đa dạng nội dung**: Đăng **text, hình ảnh, video, slideshow, carousel, reels, shorts, stories**...
- **Không cần code**: Sử dụng **n8n + Blotato API** để tự động hóa toàn bộ quy trình.
:::

---

### 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi import workflow, các sếp cần chuẩn bị:
✔ **Tài khoản Blotato** (đăng ký tại [blotato.com](https://blotato.com/))
✔ **API Key Blotato** (phí, sinh tại **Settings > API**)
✔ **Google Sheets** (sử dụng mẫu đã cung cấp, **không được đổi tên cột**)
✔ **Google Drive** (đặt folder chứa hình ảnh/video thành **public**)
✔ **N8n Community Node Blotato** (cài đặt tại **n8n Admin Panel**)
✔ **Credentials Google Sheets & Blotato** (cấu hình trong n8n)
✔ **Tài khoản mạng xã hội** (TikTok, Instagram, Facebook, LinkedIn, Twitter, Threads, Bluesky, YouTube, Pinterest)
:::

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/8524) hoặc copy/paste JSON vào **n8n Editor**.
- **Nhấn "Import"** để thêm workflow vào n8n.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này gồm **15 node**, các sếp cần chú ý cấu hình sau:

##### **🔹 Node "Ready to Post" (Google Sheets)**
- **Lựa chọn Credentials**: Chọn **"googleSheetsOAuth2Api"** (đã cấu hình trước).
- **Sheet Name**: Đảm bảo tên sheet **không đổi** so với mẫu (cột: `Caption`, `Media URL`, `Status`).
- **Query**: Lấy dữ liệu bài đăng có `Status = "Ready to Post"`.

##### **🔹 Node "Get Google Drive ID" (Set)**
- **Lấy ID file từ URL**: Nếu hình ảnh/video trên Google Drive, node này tự động trích xuất ID.

##### **🔹 Node "Upload Image/Video to BLOTATO" (Blotato)**
- **Chọn Credentials**: Chọn **"blotatoApi"** (đã cấu hình API Key).
- **Resource**: Đặt `"media"` để upload hình ảnh/video.

##### **🔹 Node "Post to Social Platforms" (Blotato)**
- **Chọn tài khoản mạng xã hội**:
  - TikTok, Instagram, Facebook, LinkedIn, Twitter, Threads, Bluesky, YouTube, Pinterest.
  - **Không cần cấu hình gì thêm**, chỉ cần **chọn tài khoản** trong node tương ứng.
  - **Lưu ý**:
    - TikTok & Pinterest cần **warm up account** trước khi sử dụng API.
    - YouTube có giới hạn **post/day** cho tài khoản mới.

##### **🔹 Node "Update Status to 'Posted'" (Google Sheets)**
- **Cập nhật trạng thái**: Sau khi đăng thành công, node này sẽ **đánh dấu bài đăng thành "Posted"** trên Google Sheets.

##### **🔹 Node "Check Every 3 Hours" (Schedule Trigger)**
- **Thiết lập lịch chạy**: Workflow sẽ chạy **mỗi 3 giờ** để tránh spam.

##### **🔹 Node "Final Report" (Merge)**
- **Hiển thị kết quả**: Gộp tất cả log thành một báo cáo cuối cùng.

---

#### **3. Kích hoạt ⚡️**
- **Test Run**: Chạy thử với **1 bài đăng mẫu** để kiểm tra kết quả.
- **Bật Active**: Sau khi kiểm tra thành công, **bật workflow** để chạy tự động.

---

### ✍️ **Mẹo & gợi ý nâng cao**
:::tip[CÁC Ý TƯỞNG MỞ RỘNG]
- **Gửi báo cáo định kỳ**: Sử dụng **n8n + Email/Slack** để gửi báo cáo thành công/thất bại hàng ngày.
- **Lưu log chi tiết**: Sử dụng **Google Sheets + n8n** để lưu tất cả log post.
- **Tích hợp AI**: Sử dụng **n8n + LLM** để tự động tạo caption cho bài đăng.
- **Chỉnh lịch chạy**: Thay đổi **thời gian chạy** (ví dụ: 8h sáng, 12h trưa, 6h chiều) để phù hợp với audience.
- **Bộ lọc bài đăng**: Sử dụng **n8n + Google Sheets** để chỉ đăng bài có **keyword cụ thể**.
:::

---

### 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn **tự động hóa toàn bộ chiến dịch mạng xã hội** mà **không cần code**. Với **chỉ 1 lần setup**, bạn có thể **đăng bài lên 9 mạng xã hội khác nhau** chỉ với **một lần nhấp chuột**.

**Hãy áp dụng ngay và tiết kiệm thời gian cho công việc quan trọng hơn!** 🚀

---
**🔗 [Tải workflow từ nguồn gốc](https://n8n.io/workflows/8524)**
**📌 [Hướng dẫn Blotato API](https://help.blotato.com/api)**
**💬 [Hỗ trợ từ Sabrina Ramonov](https://my.blotato.com/api-dashboard)** (trả lời trong 24h)