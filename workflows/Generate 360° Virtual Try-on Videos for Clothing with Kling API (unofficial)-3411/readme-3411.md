---
title: "🚀 Tự Động Tạo Video Thử Quần Áo 360° (Virtual Try-on) Với Kling API và n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa quy trình tạo video thời trang ảo 360 độ từ ảnh người mẫu và trang phục sử dụng PiAPI và Kling API."
slug: "tao-video-thu-quan-ao-360-do-kling-api-n8n"
tags: [n8n, automation, ai, piapi, kling-api, e-commerce, video-generation]
keywords: [n8n workflow, virtual try-on, kling api, piapi, tu dong hoa video thoi trang, ai fashion video]
---

# 🚀 Tự Động Tạo Video Thử Quần Áo 360° (Virtual Try-on) Với Kling API và n8n

Trong ngành thương mại điện tử và thời trang hiện nay, việc sản xuất nội dung video người mẫu mặc thử trang phục (Virtual Try-on) với góc quay 360 độ tốn rất nhiều chi phí và thời gian studio. Việc làm thủ công khiến các brand khó scale số lượng mẫu mã lên các nền tảng TikTok, Reels hay Shopee Video.

Giải pháp ở đây là gì? Workflow n8n này sẽ giúp các sếp tự động hóa 100% quy trình: chỉ cần tải lên hình ảnh người mẫu và trang phục, hệ thống sẽ kết nối với PiAPI/Kling API để xử lý và trả về video 360 độ cực kỳ chân thực mà không cần một dòng code nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow xử lý các tác vụ gọi API nặng và chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% chi phí studio:** Không cần thuê người mẫu, thợ quay phim hay dựng hình phức tạp cho từng bộ quần áo mới.
- **Tốc độ thần tốc:** Tạo hàng loạt video thời trang 360° để bắt trend trên TikTok, Instagram Reels, YouTube Shorts.
- **Tùy biến linh hoạt:** Hỗ trợ cả trang phục liền thân (dress) hoặc phối đồ rời (upper/lower).
- **Quy trình khép kín:** Tự động gửi request, chờ xử lý (polling status) và trả về URL video hoàn chỉnh.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Self-hosted hoặc Cloud).
- **PiAPI Account:** Tài khoản PiAPI có sẵn số dư/API Key để sử dụng dịch vụ Kling API.
- **Image URLs:** Link ảnh gốc của người mẫu và ảnh trang phục (được lưu trên Cloudinary, AWS S3 hoặc Google Drive có public link).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow này hoặc copy toàn bộ mã nguồn JSON từ n8n.
- Mở n8n Editor, chọn **Add workflow** -> **Import from File** / **Paste Workflow**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 13 nodes hoạt động tuần tự từ việc tạo ảnh thử đồ cho đến xuất video cuối cùng:

- **Preset Parameters (`Preset Parameters`):** Nơi các sếp cấu hình các thông số đầu vào cho AI như link ảnh người mẫu (`model_url`) và link trang phục (`dress_input` hoặc `upper_input` / `lower_input`).
- **Kling Virtual Try-On Task (`Kling Virtual Try-On Task`):** Node HTTP Request gửi yêu cầu tạo ảnh thử đồ ảo đến PiAPI. Cần thiết lập Credentials kiểu Header Auth với API Key của PiAPI.
- **Wait for Image Generation (`Wait for Image Generation`):** Node chờ AI xử lý xong lớp ảnh thử đồ.
- **Get Kling Virtual Try-On Task (`Get Kling Virtual Try-On Task`) & Check Data Status (`Check Data Status`):** Kiểm tra trạng thái hoàn thành của việc tạo ảnh. Nếu xong, chuyển sang bước tạo video.
- **Generate kling video (`Generate kling video`):** Node HTTP Request gọi API tạo video 360° dựa trên ảnh thử đồ vừa tạo.
- **Wait for Video Generation (`Wait for Video Generation`), Check Video Data Status (`Check Video Data Status`), Get Video Data Status (`Get Video Data Status`):** Cơ chế vòng lặp chờ đợi (polling) cho đến khi video được render hoàn tất.
- **Get Final Video URL (`Get Final Video URL`):** Trích xuất đường dẫn URL video cuối cùng để các sếp sử dụng.

#### 3. Kích hoạt ⚡️
- Nhấn **Test workflow** trên node `When clicking ‘Test workflow’` để chạy thử với dữ liệu mẫu.
- Kiểm tra kết quả trả về tại node `Get Final Video URL`.
- Sau khi test thành công, bật nút **Active** để đưa workflow vào trạng thái vận hành tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Google Sheets:** Thay vì dùng node `Preset Parameters` thủ công, các sếp có thể kết nối Google Sheets chứa danh sách link ảnh sản phẩm để hệ thống tự động chạy hàng loạt (Batch Processing).
- **Gửi thông báo Telegram/Slack:** Thêm node Telegram ở cuối workflow để bắn ngay video hoàn thành vào nhóm chat của đội ngũ Marketing.
- **Tự động đăng bài:** Kết nối URL video trả về trực tiếp với các API Social Media để tự động lên lịch đăng bài sản phẩm.

### 📌 Kết luận
Workflow tự động hóa tạo video thời trang 360° với Kling API là một "vũ khí bí mật" giúp các shop thời trang và nhà sáng tạo nội dung tối ưu hóa hiệu suất làm việc, tạo ra hàng loạt thước phim sản phẩm chuyên nghiệp với chi phí tối thiểu. Hãy triển khai ngay hôm nay để bứt phá doanh số!