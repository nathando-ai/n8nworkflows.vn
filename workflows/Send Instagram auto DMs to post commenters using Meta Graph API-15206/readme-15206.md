---
title: "🚀 Tự động gửi tin nhắn Instagram (Auto-DM) khi có người bình luận bài viết bằng n8n và Meta Graph API"
description: "Hướng dẫn cài đặt workflow n8n tự động bắt sự kiện bình luận trên Instagram, lọc từ khóa và gửi tin nhắn trực tiếp (DM) chứa tài liệu hoặc link ưu đãi cực nhanh."
slug: "tu-dong-gui-instagram-auto-dm-meta-graph-api-n8n"
tags: [n8n, automation, instagram, meta-graph-api, social-media, marketing]
keywords: [n8n workflow, instagram auto dm, meta graph api n8n, tu dong hoa instagram, nhan tin tu dong instagram]
---

# 🚀 Tự động gửi tin nhắn Instagram (Auto-DM) cho người bình luận với n8n

Các sếp chạy quảng cáo hoặc làm content marketing trên Instagram chắc chắn hiểu cảm giác "ngợp" khi có hàng trăm comment xin tài liệu, hỏi giá, hoặc xin link ưu đãi. Việc ngồi nhắn tay từng người vừa tốn thời gian, vừa dễ bỏ sót khách hàng tiềm năng.

Giải pháp là gì? Workflow n8n này sẽ tự động hóa 100% quy trình: Lắng nghe bình luận -> Lọc từ khóa chuẩn xác -> Gửi tin nhắn trực tiếp (Direct Message) ngay lập tức qua Meta Graph API. Khách hàng nhận được link ngay lập tức, tỷ lệ chuyển đổi tăng vọt mà đội ngũ không tốn một phút nhân công nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 bắt trọn mọi tương tác từ Instagram, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Phản hồi tức thì (Instant Reply):** Khách vừa comment từ khóa là nhận ngay tin nhắn trong tích tắc, giữ chân khách hàng khi họ đang có hứng thú cao nhất.
- **Tiết kiệm 100% thời gian thủ công:** Không còn cảnh phải copy/paste link gửi cho từng tài khoản.
- **Tăng tương tác và thuật toán:** Kéo tương tác bài viết cực tốt nhờ lượng comment bùng nổ, thuật toán Instagram sẽ đẩy bài viết của các sếp lên xu hướng.
- **Hoạt động bền bỉ 24/7:** Chạy ngầm trên n8n không mệt mỏi, không bỏ lỡ bất kỳ lead nào kể cả ban đêm.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Tài khoản Meta Business / Meta Developer Account** để cấu hình Webhook và lấy Page/Account Access Token.
- **Meta Graph API Credentials** để xác thực trong node gửi tin nhắn.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy đoạn mã JSON của workflow này và paste trực tiếp vào màn hình n8n Editor, hoặc import file JSON thông qua menu tuỳ chọn.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow gồm 5 nodes chính, các sếp cần cấu hình kỹ các điểm sau để hệ thống chạy mượt mà:

- **Trigger on Instagram Comment (`webhook`):** Cấu hình Meta Developer App kết nối với webhook này và đăng ký lắng nghe sự kiện `comments` từ Instagram.
- **Match Post ID (`if`):** 👉 **CỰC KỲ QUAN TRỌNG:** Mở node này và điền **Instagram Post ID** của bài viết Lead Magnet cùng với **Instagram Account ID** của các sếp để tránh vòng lặp tự động trả lời chính mình (self-looping).
- **Match Comment Text (`filter`):** Thiết lập từ khóa kích hoạt chính xác (Ví dụ: "DM", "Gửi mình", "Link"). Nếu bình luận chứa từ khóa này, workflow mới cho phép chạy tiếp.
- **Data (`set`):** Nơi các sếp soạn nội dung tin nhắn. Thay thế đoạn chữ mẫu `"Your-Message-Here"` bằng thông điệp chào mừng kèm đường link tài liệu/ưu đãi thực tế muốn gửi cho khách.
- **Send DM (`httpRequest`):** Thiết lập phương thức gọi API, chọn đúng Credentials kết nối với Meta Graph API để thực hiện lệnh gửi tin nhắn trực tiếp qua hộp thư Instagram.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (Test Run) bằng cách để một tài khoản khác vào comment thử vào bài viết mẫu.
- Kiểm tra kết quả trong n8n execution log và hộp thư Instagram.
- Sau khi mọi thứ mượt mà, gạt nút **Active** để workflow chính thức trực chiến 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp Telegram/Slack Notification:** Thêm một node Telegram hoặc Slack ở cuối luồng để bắn thông báo về cho sales team mỗi khi có khách hàng nhận được Auto-DM thành công.
- **Lưu trữ Lead vào Google Sheets:** Mở rộng workflow bằng cách thêm node Google Sheets để lưu lại Instagram Username, nội dung comment và thời gian nhằm phục vụ cho các chiến dịch remarketing sau này.
- **AI hóa nội dung:** Thay vì cố định một câu trả lời ở node `Data`, các sếp có thể tích hợp OpenAI (ChatGPT) để sinh ra nội dung phản hồi linh hoạt, cá nhân hóa theo từng câu hỏi của khách hàng.

### 📌 Kết luận
Instagram Auto-DM là vũ khí bí mật của các nhà sáng tạo nội dung và doanh nghiệp e-commerce hiện đại để biến lượt tương tác thành khách hàng tiềm năng chất lượng cao. Triển khai ngay workflow này trên n8n để tối ưu hóa phễu bán hàng của các sếp ngay hôm nay!