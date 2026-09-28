---
title: "🚀 Tự động gửi Email tổng hợp Reddit hàng ngày với Google Sheets và AI Scoring"
description: "Hướng dẫn xây dựng workflow n8n tự động cào bài viết Reddit qua RSS, chấm điểm bằng từ khóa thông minh, lọc tin trùng lặp và gửi email tóm tắt mỗi sáng."
slug: "tu-dong-gui-email-tong-hop-reddit-hang-ngay"
tags: [n8n, automation, reddit, google-sheets, email-digest]
keywords: [n8n workflow, tự động hóa reddit, email digest, google sheets scoring, market research]
---

# 🚀 Tự động gửi Email tổng hợp Reddit hàng ngày với việc chấm điểm từ khóa

Mỗi ngày, hàng ngàn chủ đề hữu ích xuất hiện trên Reddit liên quan đến ngách kinh doanh hoặc thị trường của các sếp. Việc dò tìm thủ công từng subreddit không chỉ tốn thời gian mà còn dễ bỏ sót các cơ hội vàng để tiếp cận khách hàng tiềm năng.

Đừng lo, workflow n8n này sẽ giúp các sếp "bắt trọn" mọi xu hướng và thảo luận nóng hổi mà không cần tốn một phút lướt web thủ công nào. Hệ thống sẽ tự động đọc danh nguồn Reddit, quét qua danh sách từ khóa chấm điểm trên Google Sheets, lọc ra những bài viết mới nhất và gửi ngay một bản tin (Digest Email) gọn gàng vào hộp thư của các sếp mỗi sáng.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian tuyệt đối:** Không cần mở Reddit hay lướt qua hàng trăm bài rác mỗi ngày.
- **Chính xác theo chủ đề:** Hệ thống tự động chấm điểm dựa trên từ khóa mong muốn (Include/Exclude Keywords) được quản lý tập trung trên Google Sheets.
- **Không sợ trùng lặp:** Tự động lưu vết các bài viết đã xem, đảm bảo các sếp chỉ nhận tin mới tinh mỗi ngày.
- **Tự động hóa 100%:** Chạy ngầm đều đặn mỗi sáng nhờ Schedule Trigger kết hợp SMTP gửi email mượt mà.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản n8n (Self-hosted hoặc Cloud).
- **Google Sheets:** File Google Sheets chứa danh sách Subreddits, từ khóa (Include/Exclude), và bảng ghi nhận bài viết đã xem (Seen posts).
- **Tài khoản SMTP:** Thông tin kết nối SMTP (Gmail, SendGrid, Mailgun, v.v.) để gửi email.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow hoặc copy trực tiếp mã nguồn JSON và paste vào n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình chính xác các node trọng điểm sau:
- **Schedule:** Thiết lập khung giờ chạy tự động mỗi sáng (ví dụ: 7:00 AM hàng ngày).
- **Read Sources, Read Keywords, Read Seen, Append Seen (Google Sheets Nodes):** 
  - Kết nối tài khoản Google Sheets thông qua `googleSheetsOAuth2Api`.
  - Trỏ đến đúng File ID và Sheet Name chứa danh sách Subreddits, bộ từ khóa (bao gồm từ khóa bắt buộc có và từ khóa loại trừ), và sheet lưu lịch sử bài viết đã quét.
- **Fetch Feed XML1 (HTTP Request Node):** Kéo dữ liệu RSS từ các Subreddit đã cấu hình.
- **Scoring & Filter New Only (Code Nodes):** Xử lý logic tính điểm bài viết dựa trên từ khóa và lọc bỏ những bài đã từng xuất hiện trong Google Sheets.
- **Send email (Email Send Node):** 
  - Chọn credentials loại `smtp`.
  - Điền email người gửi, người nhận và cấu hình tiêu đề email linh hoạt.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Node** từng bước (hoặc Test run) để kiểm tra xem Google Sheets và luồng dữ liệu XML có trả về kết quả chính xác không.
- Sau khi test thành công, bật công tắc **Active** góc trên cùng bên phải để workflow tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thêm Chatops:** Thay vì chỉ gửi Email, các sếp có thể bổ sung node Telegram hoặc Slack để bắn tin nóng ngay lập tức khi có bài viết đạt điểm số vượt ngưỡng (High-score post).
- **Mở rộng nguồn dữ liệu:** Không chỉ Reddit, các sếp có thể kết hợp thêm các nguồn RSS từ các trang tin tức ngành, Medium, hoặc Hacker News.
- **Lưu lịch sử chi tiết:** Tận dụng Google Sheets để lưu trữ toàn bộ lịch sử điểm số, giúp phân tích xu hướng từ khóa theo tuần/tháng.

### 📌 Kết luận
Workflow này là trợ thủ đắc lực cho các nhà sáng lập, chuyên gia marketing và nghiên cứu thị trường. Hãy cài đặt ngay hôm nay để tối ưu hóa thời gian thu thập thông tin và không bao giờ bỏ lỡ các cơ hội kinh doanh đắt giá!