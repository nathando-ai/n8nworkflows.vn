---
title: "🚀 Tự động hóa tạo và đăng bài Instagram Carousel với Google Gemini và Google Slides"
description: "Hướng dẫn chi tiết workflow n8n tự động tạo nội dung carousel bằng AI, thiết kế qua Google Slides, xử lý ảnh và đăng tự động lên Instagram."
slug: "tu-dong-hoa-instagram-carousel-gemini-google-slides"
tags: [n8n, automation, instagram, google-gemini, google-slides, content-creation]
keywords: [n8n workflow, tạo instagram carousel tự động, google gemini n8n, google slides automation, auto post instagram]
---

# 🚀 Tự động hóa tạo và đăng bài Instagram Carousel với Google Gemini và Google Slides

Chào các sếp! Việc lên ý tưởng, thiết kế từng slide (carousel) và đăng bài đều đặn lên Instagram tốn vô vàn thời gian của đội ngũ Marketing. Nếu các sếp đang tìm giải pháp tự động hóa toàn bộ quy trình này – từ việc "nhờ" AI viết nội dung, tự động đắp vào template Google Slides, xuất ra ảnh và tự động "bơm" lên Instagram – thì đây chính là "vũ khí tối thượng" do chuyên gia Bakdaulet xây dựng.

Workflow này giúp các sếp giải phóng 100% sức lao động thủ công, duy trì kênh Instagram đều như vắt chanh với những nội dung trực quan, bắt mắt.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hoàn toàn:** Từ kích hoạt lịch trình hàng ngày (`Run daily schedule`) đến khi bài đăng xuất hiện trên Instagram.
- **AI thông minh & có cấu trúc:** Sử dụng Google Gemini kết hợp `Structured Output Parser1` để tạo nội dung từng slide chuẩn xác, không lệch pha.
- **Thiết kế chuyên nghiệp:** Tự động nhân bản Google Slides template, thay thế nội dung, xuất thumbnail ảnh cực nét.
- **Quản lý thông minh:** Theo dõi trạng thái đăng bài qua Google Sheets (`update status`), tự động retry nếu Meta chưa xử lý kịp xong media.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (bản cloud hoặc self-hosted).
- **Tài khoản Google:** Google Drive, Google Sheets, Google Slides, và Google Gemini API Key.
- **Tài khoản Meta/Instagram Business:** Đã kết nối trang Instagram với Facebook Page và lấy được Instagram Account ID.
- **Template Google Slides:** Copy mẫu Carousel Template chuẩn tại [đây](https://docs.google.com/presentation/d/13N2Fykd9YYG6qvpobbuw4J-igaXztx7jUfI2FW0QTqg/edit) về Google Drive của các sếp.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này từ n8n.io (hoặc copy toàn bộ JSON), sau đó paste trực tiếp vào n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow gồm 29 nodes hoạt động nhịp nhàng, các sếp cần chú ý cấu hình kỹ các điểm sau:
- **Google Gemini Chat Model1:** Thêm Credential API Key của Gemini để AI bắt đầu "sáng tác" nội dung.
- **Generate carousel content (Agent) & Structured Output Parser1:** Tinh chỉnh Prompt của AI nếu các sếp muốn đổi chủ đề, ngôn ngữ (Tiếng Việt/Anh) hoặc phong cách viết bài.
- **Duplicate carousel template (Google Drive):** Trỏ tới file Template Google Slides mà các sếp vừa copy về Drive ở phần chuẩn bị.
- **Google Sheets nodes (`get data`, `add data`, `update status`):** Kết nối tới file Google Sheets quản lý chủ đề, nguồn dữ liệu đầu vào và lưu log trạng thái bài đăng.
- **Instagram HTTP Request nodes (`publish`, `Container HTTP Carousel1`, v.v.):** Cấu hình Meta Graph API credentials, điền đúng Instagram Account ID của doanh nghiệp để hệ thống có quyền đăng bài.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (`Test workflow`) thủ công từ node `Run daily schedule` để kiểm tra xem quá trình tạo slide và upload container Instagram có lỗi hay không.
- Sau khi test thành công, gạt công tắc **Active** để workflow tự động chạy ngầm theo lịch trình.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Thông báo:** Thêm node Telegram hoặc Slack vào cuối nhánh `update status` để bot hú lên mỗi khi có bài viết mới lên sóng hoặc báo lỗi nếu Instagram API gặp sự cố.
- **Quản lý lịch biên tập:** Mở rộng Google Sheets đầu vào để chứa danh sách chủ đề dài hạn, giúp AI chủ động bốc ý tưởng theo tuần/tháng.
- **Kiểm duyệt trước khi đăng (Human-in-the-loop):** Thay vì đăng tự động 100%, các sếp có thể thêm bước gửi thông báo kèm ảnh preview vào Telegram/Slack, kèm nút duyệt/hủy trước khi gọi lệnh `publish` lên Instagram.

### 📌 Kết luận
Workflow tạo và đăng Instagram Carousel tự động với Gemini và Google Slides là giải pháp đỉnh cao giúp tối ưu hóa hiệu suất truyền thông mạng xã hội mà không cần đội ngũ thiết kế thủ công từng slide. Hãy thiết lập ngay hôm nay để kênh Instagram của các sếp luôn tràn ngập nội dung chất lượng!