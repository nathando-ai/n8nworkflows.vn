---
title: "🚀 Tự động tạo video chuyển động AI bằng Kling v2.6 và đăng lên TikTok"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa quy trình tạo video AI chuyển động nhân vật từ ảnh và video mẫu bằng Kling v2.6 (Kie.ai) và tự động đăng lên TikTok qua Postiz."
slug: "tu-dong-tao-video-ai-kling-v2-6-dang-tiktok-n8n"
tags: [n8n, automation, no-code, kling-ai, tiktok, postiz, ai-video]
keywords: [n8n workflow, kling v2.6, kie ai, tự động hóa tiktok, postiz n8n, ai motion video]
---

# 🚀 Tự động tạo video chuyển động AI bằng Kling v2.6 và đăng lên TikTok

Việc sản xuất nội dung video ngắn (Shorts, TikTok, Reels) theo xu hướng đòi hỏi lượng thời gian và công sức khổng lồ nếu làm thủ công. Từ khâu chuẩn bị hình ảnh nhân vật, tìm kiếm video chuyển động mẫu, gọi API tạo video AI cho đến việc tải xuống và lên lịch đăng bài thủ công lên từng nền tảng.

Workflow n8n này sẽ giúp các sếp giải quyết triệt để vấn đề đó bằng một quy trình khép kín 100% tự động. Kết hợp sức mạnh của **Kling v2.6 Motion Control** (thông qua Kie.ai) để biến một tấm ảnh tĩnh thành video chuyển động theo video mẫu, sau đó tự động hóa việc upload và xuất bản lên TikTok thông qua **Postiz**.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn:** Từ lúc kích hoạt workflow cho đến khi video xuất hiện trên TikTok mà không cần thao tác tay.
- **Video AI chất lượng cao:** Sử dụng model Kling v2.6 tiên tiến để điều khiển chuyển động nhân vật chính xác từ ảnh gốc và video tham chiếu.
- **Quản lý đa kênh dễ dàng:** Tích hợp Postiz giúp đồng bộ và lên lịch đăng bài mượt mà lên TikTok và các mạng xã hội khác.
- **Lưu trữ an toàn:** Tự động sao lưu bản render video hoàn chỉnh vào Google Drive để dễ dàng tái sử dụng.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Self-hosted hoặc Cloud).
- **Kie.ai API Key** (để sử dụng model Kling v2.6 Motion Control).
- **Tài khoản Postiz** (kết nối với kênh TikTok và lấy API Key).
- **Tài khoản Google Drive** (để lưu trữ video xuất ra).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể copy mã JSON của workflow này và paste trực tiếp vào n8n Editor của mình, hoặc import file JSON tải về từ kho lưu trữ n8n.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow hoạt động chính xác, các sếp cần cấu hình kỹ các node sau:

- **Set params**: Cập nhật các thông số đầu vào bao gồm:
  - `image_url`: Đường dẫn trực tiếp đến hình ảnh nhân vật tĩnh của sếp.
  - `video_url`: Đường dẫn trực tiếp đến video mẫu chứa chuyển động tham chiếu.
  - `tiktok_desc`: Caption (tiêu đề/mô tả) muốn hiển thị khi đăng lên TikTok.
- **Run Kling v2.6 Motion Control** & **Result**: Thêm credentials loại `httpBearerAuth` chứa **Kie.ai API Key** của sếp để gửi yêu cầu render video và nhận kết quả.
- **Upload Video to Postiz**: Thêm credentials loại `httpHeaderAuth` để xác thực khi gửi file video lên hệ thống Postiz.
- **TikTok (Postiz)**: Thay thế chuỗi placeholder `XXX` bằng **Integration ID** chính xác của kênh TikTok đã được kết nối trong bảng điều khiển Postiz của sếp.
- **Upload video (Google Drive)**: Cấu hình tài khoản `googleDriveOAuth2Api` để chọn thư mục lưu trữ video tự động.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm thủ công (`Manual Trigger`) bằng cách bấm **‘Execute workflow’** để kiểm tra toàn bộ luồng từ tạo video, chờ xử lý (Wait node), đến đăng bài.
- Sau khi test thành công, bật nút **Active** để workflow sẵn sàng hoạt động.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp thông báo qua Telegram/Slack:** Thêm một node Telegram ở cuối workflow để gửi tin nhắn kèm hình ảnh/video thông báo ngay khi video đã được lên lịch thành công trên TikTok.
- **Nguồn dữ liệu đầu vào tự động:** Thay thế node `Manual Trigger` bằng Google Sheets hoặc Airtable, cho phép các sếp thêm hàng loạt danh sách ảnh và video mẫu để hệ thống tự động chạy theo hàng đợi (Queue).
- **Lưu log lỗi:** Thiết lập Error Trigger để bắt các sự cố thiếu quỹ API hoặc lỗi render từ Kie.ai, giúp tiết kiệm thời gian kiểm tra.

### 📌 Kết luận
Workflow tích hợp AI Kling v2.6 và Postiz là chìa khóa giúp các nhà sáng tạo nội dung và Marketer tối ưu hóa thời gian sản xuất video ngắn vạn năng. Hãy "lên đồ" ngay hôm nay để tự động hóa kênh TikTok của các sếp!