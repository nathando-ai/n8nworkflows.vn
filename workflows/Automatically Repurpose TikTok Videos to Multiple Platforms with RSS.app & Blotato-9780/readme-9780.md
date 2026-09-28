---
title: "🚀 Tự Động Chuyển Đổi Video TikTok Sang Nhiều Platform Khác Với RSS.app & Blotato – Không Cần Code!"
description: "Workflow này tự động phát hiện video TikTok mới của bạn, tải xuống và chia sẻ trên Instagram, Facebook, YouTube, LinkedIn, Twitter, Threads, Pinterest và Bluesky – tất cả chỉ với một workflow n8n. Tiết kiệm 10+ giờ/tháng cho các sếp marketing!"
slug: "tich-hop-video-tiktok-sang-many-platform"
tags: [n8n, automation, tiktok, social-media, blotato, rss-app, google-drive]
keywords: [tự động hóa tiktok, chia sẻ video nhiều nền tảng, n8n workflow tiktok, repurpose tiktok, blotato api, rss feed tiktok]
---

# 🚀 **Tự Động Chuyển Đổi Video TikTok Sang Nhiều Platform Khác – Không Cần Code!**

### **Nỗi Đau Của Các Sếp Marketing**
Các sếp đang mất **10+ giờ/tuần** để:
- Tải xuống video TikTok mới (với watermark).
- Chỉnh sửa hình ảnh/video cho phù hợp với từng nền tảng.
- Chia sẻ trên Instagram, Facebook, YouTube, LinkedIn, Twitter, Threads, Pinterest và Bluesky.
- Lo lắng về **spam** nếu post quá nhiều lần cùng một nội dung.

**Workflow này giải quyết tất cả!** Nó tự động:
✅ **Phát hiện** video TikTok mới của bạn qua RSS.
✅ **Tải xuống** video **không watermark** và lưu vào Google Drive.
✅ **Chia sẻ** trên **8 nền tảng** (Instagram, Facebook, YouTube, LinkedIn, Twitter, Threads, Pinterest, Bluesky) **một cách tự động**.
✅ **Tùy chỉnh** thời gian post và nội dung cho mỗi nền tảng.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7**, các sếp nên cài **n8n trên VPS riêng (Self-hosted)**.
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 Mã giảm giá: **VPSN8N** - giảm tới **39%**).
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (đảm bảo tốc độ cao).
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ/tháng** cho việc chia sẻ video.
- **Tăng độ phủ** trên **8 nền tảng** với **một công việc**.
- **Không bị spam** vì hệ thống tự động **tùy chỉnh** thời gian post.
- **Dữ liệu an toàn** với Google Drive làm lưu trữ trung tâm.
- **Cập nhật liên tục** khi bạn post mới trên TikTok.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
✔ **Tài khoản TikTok** (để tạo RSS feed).
✔ **Tài khoản RSS.app** ([Đăng ký miễn phí](https://rss.app)) để tạo RSS feed cho TikTok.
✔ **Tài khoản Google Drive** (để lưu video).
✔ **Tài khoản Blotato** ([Đăng ký miễn phí](https://blotato.com)) để chia sẻ trên các nền tảng.
✔ **API Key Blotato** (cài đặt trong n8n).
✔ **Các tài khoản mạng xã hội** (Instagram, Facebook, YouTube, LinkedIn, Twitter, Threads, Pinterest, Bluesky) để kết nối với Blotato.

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/9780) hoặc copy/paste JSON vào **n8n Editor**.
- **Nhấp vào "Import"** và chọn file JSON đã tải.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này gồm **15 node**, các sếp cần chú ý cấu hình **các node quan trọng** sau:

##### **🔹 Node 1: RSS Feed Trigger (RSS.app)**
- **Cấu hình:**
  - **Feed URL:** Dán URL RSS từ RSS.app (cách tạo ở phần **Setup 1**).
  - **Number of Posts:** Đặt thành **1** (chỉ lấy video mới nhất).
  - **Active:** Bật để kích hoạt trigger.

##### **🔹 Node 2-3: Get TikTok Page & Get Video URL (HTTP Request + Code)**
- **Không cần chỉnh sửa** (n8n tự động lấy video từ RSS feed).

##### **🔹 Node 4: Get Video (HTTP Request)**
- **Không cần chỉnh sửa** (n8n tự động tải video từ URL TikTok).

##### **🔹 Node 5: Upload to Google Drive**
- **Cấu hình:**
  - **Credentials:** Chọn `googleDriveOAuth2Api` (đã cài đặt trước).
  - **Parent Drive:** Chọn Google Drive muốn lưu.
  - **Parent Folder:** Chọn thư mục cụ thể (ví dụ: "TikTok Videos").
  - **File Name:** Đặt tên tự động (ví dụ: `TikTok_${currentDate}`).

##### **🔹 Node 6-13: Blotato (Instagram, Facebook, YouTube, LinkedIn, Twitter, Threads, Pinterest, Bluesky)**
- **Cấu hình chung:**
  - **Credentials:** Chọn `blotatoApi` (đã cài đặt trong n8n).
  - **Social Account:** Chọn tài khoản mạng xã hội tương ứng.
  - **Post Type:** Chọn `video` (nếu video) hoặc `image` (nếu screenshot).
  - **Media URL:** Đặt là **Google Drive URL** (từ node Upload to Google Drive).
  - **Caption:** Có thể tùy chỉnh (ví dụ: `🔥 Video mới từ TikTok! Link: [TikTok Link] #Marketing #Automation`).
  - **Schedule Time:** Đặt thời gian post (ví dụ: 9h sáng để tối ưu engagement).

##### **🔹 Node 14: Merge1 (Merge)**
- **Không cần chỉnh sửa** (n8n tự động hợp nhất dữ liệu từ các nền tảng).

##### **🔹 Node 15: Upload Media (Blotato)**
- **Không cần chỉnh sửa** (n8n tự động upload media từ Google Drive).

#### **3. Kích Hoạt ⚡️**
- **Test Run:** Nhấp vào **Run Workflow** và kiểm tra log.
- **Active Workflow:** Sau khi test thành công, bật **Active** để workflow chạy tự động.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tùy chỉnh caption cho mỗi nền tảng:**
   - Sử dụng **node Code** để thay đổi caption trước khi post (ví dụ: caption Instagram khác với Facebook).
2. **Lưu log hoạt động:**
   - Thêm **node Google Sheets** để ghi lại lịch sử post (giúp theo dõi hiệu quả).
3. **Gửi báo cáo định kỳ:**
   - Sử dụng **node Email** (n8n-nodes-base.email) để gửi báo cáo tuần/month về số lượng post thành công.
4. **Sử dụng AI để tạo caption:**
   - Kết hợp với **node LLM** (n8n-nodes-base.llm) để tự động generate caption từ video.
5. **Chỉ post trên 1-2 nền tảng đầu tiên khi test:**
   - Tránh overpost và gây spam. Sau khi test thành công, mở rộng dần.

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp để tập trung vào **strategy** thay vì công việc lặp lại. **Chỉ cần 10 phút setup**, bạn đã có **tự động hóa chia sẻ video TikTok sang 8 nền tảng**!

**🚀 Hãy áp dụng ngay và tăng **tầm ảnh hưởng** của mình trên mạng xã hội!**

---
**🔗 [Tải workflow nguyên bản](https://n8n.io/workflows/9780)**
**📚 [Hướng dẫn chi tiết từ Blotato](https://help.blotato.com/api/templates/8-repurpose-tiktoks-on-autopilot)**