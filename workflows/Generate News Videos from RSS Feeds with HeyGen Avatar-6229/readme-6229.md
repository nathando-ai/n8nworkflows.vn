---
title: "🚀 Tự động hóa tạo video tin tức từ RSS Feed với HeyGen AI Avatar trên n8n"
description: "Hướng dẫn chi tiết cách xây dựng workflow n8n tự động đọc tin tức từ nguồn RSS, chuyển đổi thành nội dung và gọi HeyGen API để tạo video AI Avatar chuyên nghiệp chỉ trong vài nốt nhạc."
slug: "tu-dong-hoa-tao-video-tin-tuc-tu-rss-feed-voi-heygen-avatar"
tags: [n8n, automation, no-code, heygen, ai-video, content-creation]
keywords: [n8n workflow, tạo video tự động, heygen ai avatar, rss feed to video, tự động hóa nội dung]
---

# 🚀 Tự động hóa tạo video tin tức từ RSS Feed với HeyGen AI Avatar

Việc sản xuất video tin tức thủ công hàng ngày đòi hỏi rất nhiều thời gian từ khâu biên tập kịch bản, chọn giọng đọc cho đến dựng hình. Các sếp có bao giờ nghĩ đến việc tự động hóa toàn bộ quy trình này? Với workflow n8n kết hợp cùng HeyGen API, các sếp có thể tự động lấy tin tức mới nhất từ các trang báo RSS và biến chúng thành những video có người đại diện AI (AI Avatar) phát biểu một cách chuyên nghiệp mà không cần tốn một giọt mồ hôi dựng hình nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Bỏ qua khâu viết kịch bản thủ công và dựng video phức tạp.
- **Cập nhật liên tục:** Lấy tin tức nóng hổi từ các nguồn RSS Feed yêu thích (ví dụ: Prothom Alo hoặc bất kỳ báo điện tử nào) ngay khi vừa lên sóng.
- **Cá nhân hóa cao:** Tận dụng công nghệ AI Avatar của HeyGen để tạo các video có người thật đọc tin tức với độ phân giải HD (1280x720).
- **Tối ưu chi phí & nhân sự:** Tiết kiệm hàng chục giờ làm việc mỗi tuần cho đội ngũ sản xuất nội dung mạng xã hội (TikTok, YouTube Shorts, Reels).
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một hệ thống n8n đang hoạt động (Cloud hoặc Self-hosted).
- Tài khoản HeyGen và **API Key** hợp lệ để gọi dịch vụ tạo video.
- Đường dẫn (URL) của nguồn RSS Feed tin tức mà các sếp muốn sử dụng.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể sao chép đoạn mã JSON của workflow này và dán trực tiếp vào n8n Editor của mình, hoặc import file JSON theo tài nguyên được cung cấp từ tác giả Sarfaraz Muhammad Sajib.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 3 nodes chính, các sếp cần cấu hình cẩn thận các điểm sau:

- **When clicking ‘Execute workflow’ (Manual Trigger):** 
  - Node kích hoạt thủ công để kiểm tra (test run). Sau khi hoàn thiện, các sếp có thể thay thế bằng *Schedule Trigger* để workflow tự động chạy theo khung giờ cố định hàng ngày.
- **Read RSS Feed from Prothom Alo (RSS Feed Read):** 
  - Điền URL của nguồn RSS Feed mà các sếp muốn lấy tin (mặc định trong mẫu là nguồn tin tức tiếng Bengal từ Prothom Alo, các sếp có thể đổi thành RSS của VnExpress, Dân Trí, hoặc kênh tin tức yêu thích của mình).
- **Generate Video News (HTTP Request):** 
  - Node này sẽ gửi một yêu cầu `POST` tới HeyGen API.
  - **Headers:** Cần cấu hình chuẩn xác API Key của HeyGen (giữ bảo mật tuyệt đối, không chia sẻ cho người khác).
  - **Body / Payload:** Lấy nội dung tóm tắt từ node RSS Feed để làm kịch bản (input text) cho AI Avatar.
  - **Cấu hình Video:** Định dạng kích thước video được thiết lập sẵn ở độ phân giải chuẩn **1280x720 pixels** (phù hợp cho nhiều nền tảng).

#### 3. Kích hoạt ⚡️
- Nhấn **Test Step** từng node để kiểm tra xem dữ liệu RSS có trả về không và HeyGen API có nhận lệnh tạo video thành công hay không.
- Khi mọi thứ mượt mà, hãy gạt công tắc sang **Active** để hệ thống tự động vận hành ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Schedule Trigger:** Thay vì bấm nút chạy bằng tay, hãy gắn thêm node định giờ để cứ 8:00 sáng mỗi ngày là tự động tạo video điểm tin sáng.
- **Lưu trữ Log:** Thêm node Google Sheets hoặc Notion để lưu lại danh sách các tiêu đề tin tức đã được chuyển đổi thành video, giúp quản lý kho nội dung không bị trùng lặp.
- **Gửi thông báo:** Kết nối thêm node Telegram hoặc Slack để bot gửi thông báo về máy ngay khi HeyGen xử lý xong video mới.

### 📌 Kết luận
Việc ứng dụng AI vào sản xuất nội dung chưa bao giờ dễ dàng đến thế với các công cụ No-Code như n8n và HeyGen. Hãy áp dụng ngay workflow này để tối ưu hóa kênh truyền thông của các sếp ngay hôm nay!