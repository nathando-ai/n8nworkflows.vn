---
title: "🚀 Tự động tạo ảnh Stock bằng Flux1-schnell, gắn Metadata & Lưu trữ Google Drive"
description: "Hướng dẫn sử dụng workflow n8n tự động hóa quy trình tạo ảnh Stock bằng AI (Flux1-schnell), phân tích nội dung bằng OpenAI, gắn thẻ metadata và lưu trữ gọn gàng lên Google Drive kết hợp Google Sheets."
slug: "tu-dong-tao-anh-stock-flux1-schnell-google-drive-n8n"
tags: [n8n, automation, ai-images, flux1-schnell, google-drive, openai]
keywords: [n8n workflow, tạo ảnh ai tự động, flux1-schnell, gắn metadata ảnh stock, google sheets google drive automation]
---

# 🚀 Tự động tạo ảnh Stock bằng Flux1-schnell, gắn Metadata & Google Drive

Các sếp đang tốn quá nhiều thời gian để nghĩ ý tưởng prompt, tạo ảnh hàng loạt, resize, gắn thẻ tag (metadata) và quản lý chúng trên Google Drive hay Google Sheets? Việc làm thủ công này không chỉ ngốn hàng giờ đồng hồ mà còn dễ gây nhàm chán, thiếu đồng bộ.

Giải pháp ở đây là gì? Workflow n8n siêu cấp này sẽ giúp các sếp tự động hóa **100% quy trình từ A-Z**: Tự sinh prompt bằng OpenAI, tạo ảnh chất lượng cao qua mô hình **Flux1-schnell**, tự động phân tích ảnh để viết tiêu đề/mô tả/tag, lưu trữ vào thư mục Google Drive riêng biệt, đồng thời cập nhật toàn bộ dữ liệu vào Google Sheets và gửi thông báo qua Telegram!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 mà không sợ sập giữa chừng, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn:** Chạy định kỳ theo lịch trình (Schedule Trigger) mà không cần can thiệp thủ công.
- **Kho ảnh Stock chuẩn SEO:** Ảnh được AI phân tích (Analyze images) để tự động tạo từ khóa, tiêu đề và mô tả, sẵn sàng để upload lên các trang bán ảnh stock.
- **Quản lý khoa học:** Tự động tạo thư mục trên Google Drive và lưu trữ bảng dữ liệu chi tiết trên Google Sheets cho từng ngày/chủ đề.
- **Cảnh báo thông minh:** Tích hợp Telegram thông báo tiến độ và Error Trigger ghi lại lỗi tự động vào Google Sheets.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Khuyến nghị bản Self-hosted trên VPS).
- **Tài khoản OpenAI:** Lấy API Key để dùng cho OpenAI Model (`Prompt Generator` và `Analyze images`).
- **API tạo ảnh Flux1-schnell:** Tài khoản hoặc dịch vụ API hỗ trợ gọi mô hình Flux1-schnell (qua node `Generate Image` / `Get Images`).
- **Google Cloud / Workspace Account:** Cần cấu hình OAuth2 hoặc Service Account để n8n tương tác với **Google Drive** và **Google Sheets**.
- **Telegram Bot:** Tạo sẵn bot qua `@BotFather` để nhận thông báo.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Copy mã JSON của workflow này hoặc tải file JSON từ nguồn gốc.
- Trong giao diện n8n Editor, chọn **Add workflow** -> Dán (Paste) nội dung JSON vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Vì workflow có tới 46 nodes, các sếp cần chú ý cấu hình kỹ các điểm sau để chạy mượt mà:

- **Schedule Trigger & Schedule Trigger1:** Cài đặt lại mốc thời gian chạy workflow phù hợp với nhu cầu (hàng ngày, hàng tuần...).
- **Google Sheets & Google Sheets1, 2, 3, 4:** Trỏ tới file Google Sheets quản lý chủ đề, lưu trữ metadata và log lỗi của các sếp. Đảm bảo cấu trúc cột khớp với dữ liệu code xử lý.
- **Create Folder for images & Create New Sheet (Google Drive):** Cấu hình ID thư mục gốc trên Google Drive nơi n8n sẽ tạo các thư mục con chứa ảnh stock.
- **Prompt Generator & OpenAI (OpenAI / lmChatOpenAi):** Thêm OpenAI Credentials và kiểm tra lại System Prompt để AI tạo ra các prompt ảnh chuẩn xác nhất.
- **Generate Image / Get Images (HTTP Request):** Điền Endpoint API và Token xác thực cho mô hình Flux1-schnell.
- **Telegram & Telegram1:** Điền Chat ID và Bot Token để nhận tin nhắn báo cáo kết quả.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm thủ công (**Test workflow**) với 1-2 dòng dữ liệu mẫu để kiểm tra luồng từ tạo ảnh đến đẩy lên Drive/Sheets.
- Sau khi kiểm tra mọi thứ chạy xanh mướt (success), các sếp bật công tắc **Active** ở góc trên cùng bên phải để workflow tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo:** Ngoài Telegram, các sếp có thể kết nối thêm node Slack hoặc Discord để đội ngũ cùng theo dõi tiến độ sản xuất ảnh.
- **Tự động đăng mạng xã hội:** Nối thêm node Twitter/X hoặc Facebook vào cuối luồng để tự động chia sẻ ảnh stock vừa tạo kèm hashtag lên mạng xã hội.
- **Quản lý lỗi thông minh:** Tận dụng node `Error Trigger` và `Log Error` (Google Sheets) để dễ dàng kiểm tra lại các prompt bị lỗi cấu trúc hoặc lỗi gọi API sinh ảnh.

### 📌 Kết luận
Với workflow n8n tích hợp AI Flux1-schnell và hệ sinh thái Google này, việc sản xuất hàng loạt ảnh stock chưa bao giờ nhẹ nhàng đến thế. Hãy cài đặt ngay lên VPS của các sếp và tận hưởng sức mạnh của tự động hóa!