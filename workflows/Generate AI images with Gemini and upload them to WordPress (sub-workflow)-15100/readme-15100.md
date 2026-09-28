---
title: "🚀 Tự Động Tạo Ảnh Bằng AI Gemini Và Upload Lên WordPress Trong n8n"
description: "Hướng dẫn cấu hình sub-workflow n8n giúp tự động tạo ảnh chân thực bằng Google Gemini từ văn bản và tải trực tiếp lên Thư viện Media WordPress."
slug: "tu-dong-tao-anh-ai-gemini-upload-wordpress-n8n"
tags: [n8n, automation, no-code, google-gemini, wordpress, content-creation]
keywords: [n8n workflow, tạo ảnh ai, gemini ai, wordpress media library, tự động hóa nội dung]
---

# 🚀 Tự Động Tạo Ảnh Bằng AI Gemini Và Upload Lên WordPress

Trong quy trình sáng tạo nội dung tự động, việc minh họa bài viết bằng hình ảnh chất lượng cao thường tốn nhiều thời gian tìm kiếm hoặc thiết kế thủ công. Các sếp có bao giờ nghĩ đến việc để AI tự động vẽ tranh theo nội dung bài viết và đẩy thẳng lên website chưa? 

Bài viết này sẽ hướng dẫn chi tiết cách vận hành một **sub-workflow n8n** cực kỳ mạnh mẽ: Nhận yêu cầu từ workflow chính, dùng sức mạnh của **Google Gemini** để tạo ra bức ảnh chân thực (photorealistic), và tự động lưu trữ nó vào **Thư viện Media của WordPress** mà không cần đụng đến một dòng code thủ công nào.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Biến một đoạn mô tả text (query) thành ảnh hoàn chỉnh rồi đưa lên website ngay lập tức.
- **Tối ưu thời gian:** Không cần tải ảnh về máy rồi upload thủ công vào WordPress cho từng bài viết.
- **Đồng bộ thông minh:** Trả về đầy đủ các thông số quan trọng (`url`, `media_id`, `alt`) để workflow chính tiếp tục chèn vào bài đăng blog.
- **Hoạt động linh hoạt:** Thiết kế dưới dạng Sub-workflow, dễ dàng gọi từ bất kỳ quy trình tạo nội dung tự động nào (như Auto-blogging, Social Media Poster...).
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ TRƯỚC KHI BẮT ĐẦU]
- **n8n Instance (Self-hosted):** Yêu cầu phiên bản hỗ trợ LangChain/Google Gemini nodes.
- **Google Gemini API Key:** Tài khoản Google Cloud/AI Studio để gọi model sinh ảnh của Gemini.
- **WordPress Website:** Cần có tài khoản quản trị và chuẩn bị sẵn phương thức xác thực (Application Passwords hoặc Basic Auth) để gọi WordPress REST API.
:::

---

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần tạo một workflow mới trong n8n, sao chép mã JSON của workflow này và dán trực tiếp vào màn hình n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để sub-workflow này hoạt động trơn tru, các sếp cần cấu hình chính xác 4 nodes sau:

- **Trigger — Receive Query (`executeWorkflowTrigger`):** Node này đóng vai trò nhận dữ liệu đầu vào (một chuỗi `query`) từ workflow cha truyền sang ở chế độ *passthrough*.
- **Gemini — Generate Image (`googleGemini`):** 
  - Kết nối tài khoản thông qua **Google Gemini API Credential**.
  - Tùy chỉnh prompt trong node nếu muốn thay đổi phong cách ảnh (mặc định workflow đang cấu hình tạo ảnh chân thực chuyên nghiệp dựa trên `{{ $json.query }}`).
- **WP — Upload Image to Media Library (`httpRequest`):**
  - Cập nhật lại đường dẫn URL endpoint của WordPress: Thay thế `https://your-site.com/wp-json/wp/v2/media` bằng đường dẫn website thật của các sếp.
  - Cấu hình Authentication (Basic Auth hoặc Application Passwords) để n8n có quyền upload file lên website WordPress.
  - Node này được thiết lập tự động retry 1 lần nếu lỗi và cấu hình *Continue On Error* để không làm gián đoạn workflow cha.
- **Set — Return Image Data (`set`):** Node này có nhiệm vụ lọc và chuẩn hóa dữ liệu trả về gồm: `url` của ảnh, `media_id` trên WordPress, và thẻ `alt` để truyền ngược lại cho workflow cha sử dụng.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (Test workflow) bằng cách truyền một chuỗi text mẫu vào `query`.
- Kiểm tra kết quả trong Thư viện Media của WordPress xem ảnh đã xuất hiện chưa.
- Khi mọi thứ mượt mà, hãy bật trạng thái **Active** để sẵn sàng kết nối với các workflow tự động hóa nội dung khác.

---

### ✍️ Mẹo & gợi ý nâng cao
Để hệ thống thông minh và tối ưu hơn nữa, các sếp có thể mở rộng:
1. **Kết hợp thông báo Telegram/Slack:** Thêm một node gửi thông báo kèm hình ảnh vừa tạo về nhóm chat khi upload thành công lên WordPress.
2. **Lưu trữ backup:** Đẩy bản sao hình ảnh vừa tạo lên Google Drive hoặc AWS S3 để làm tư liệu dự phòng.
3. **Tích hợp Auto-Blogging:** Gọi sub-workflow này bên trong một quy trình lấy tin tức RSS -> Tóm tắt bằng AI -> Vẽ ảnh minh họa bằng Gemini -> Đăng bài tự động lên WordPress.

---

### 📌 Kết luận
Workflow tạo ảnh bằng Gemini và upload tự động lên WordPress là một mảnh ghép không thể thiếu cho các hệ thống Content Automation thời đại AI. Hãy cài đặt ngay để tối ưu hóa quy trình sản xuất nội dung hình ảnh của các sếp!