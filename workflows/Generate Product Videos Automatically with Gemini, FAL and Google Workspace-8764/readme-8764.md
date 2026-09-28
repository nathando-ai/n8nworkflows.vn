---
title: "🚀 Tự động hóa tạo video sản phẩm với Gemini, FAL AI và Google Workspace bằng n8n"
description: "Xây dựng pipeline tự động hóa 100%: Lấy dữ liệu từ Google Sheets, xử lý hình ảnh bằng Gemini AI, tạo video quảng cáo qua FAL API và lưu trữ trên Google Drive."
slug: "tu-dong-hoa-tao-video-san-pham-gemini-fal-google-workspace"
tags: [n8n, automation, no-code, ai-video, google-sheets, gemini, fal-ai]
keywords: [n8n workflow, tạo video tự động, gemini ai, fal ai, google sheets automation, tự động hóa marketing]
keywords: [n8n workflow, tự động hóa, tạo video sản phẩm, ai video generator, google sheets automation]
---

# 🚀 Tự động hóa tạo video sản phẩm với Gemini, FAL AI và Google Workspace

Các sếp có đang gặp tình trạng tốn hàng giờ đồng hồ để thiết kế hình ảnh quảng cáo và dựng video thủ công cho từng sản phẩm mới không? Việc này không chỉ tốn nhân lực mà còn làm chậm trễ chiến dịch marketing khi số lượng sản phẩm lên đến hàng trăm SKU.

Đừng lo, bài viết này sẽ hướng dẫn các sếp thiết lập một workflow n8n cực kỳ mạnh mẽ do **Cong Nguyen** phát triển. Quy trình này sẽ tự động hóa toàn bộ: đọc dữ liệu từ Google Sheets, biến hóa hình ảnh sản phẩm bằng Gemini AI, tạo video chuyển động mượt mà qua FAL AI và lưu trữ gọn gàng lên Google Drive mà không cần viết một dòng code nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, xử lý các tác vụ gọi API AI nặng mà không lo bị ngắt kết nối, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động 100%:** Chỉ cần thêm dòng mới vào Google Sheets, hệ thống tự động sinh ảnh quảng cáo và video hoàn chỉnh.
- **Tận dụng sức mạnh AI:** Kết hợp đỉnh cao giữa Gemini AI (xử lý hình ảnh sáng tạo) và FAL AI (chuyển ảnh thành video chất lượng cao).
- **Lưu trữ khoa học:** Tự động phân loại và lưu ảnh/video vào đúng thư mục trên Google Drive, cập nhật link ngược lại vào bảng tính.
- **Tiết kiệm chi phí nhân sự:** Giảm thiểu 90% thời gian sản xuất nội dung media cho các chiến dịch E-commerce.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản và API keys sau:
- **n8n Instance:** Đã cài đặt và sẵn sàng sử dụng.
- **Google Account:** Kết nối Google Sheets và Google Drive (sử dụng OAuth2).
- **Gemini API Key:** Dùng cho node HTTP Request gọi model xử lý ảnh.
- **FAL API Key:** Dùng cho node HTTP Request tạo video từ ảnh (Image-to-Video).
- **Google Sheets Template:** Bảng tính với các cột tối thiểu: `STT`, `link_image`, `link_video`, `status`, `note`.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy đoạn mã JSON của workflow, sau đó vào giao diện n8n chọn **Add workflow** -> Click vào dấu ba chấm (...) ở góc trên bên phải -> Chọn **Import from Clipboard** và dán vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà không lỗi, các sếp cần chú ý cấu hình kỹ các node sau:

- **Google Sheets Trigger:** Chọn đúng Google Sheet và Sheet Name nơi các sếp sẽ thêm dòng dữ liệu sản phẩm mới.
- **Download file & Upload file (Google Drive):** Kết nối tài khoản Google Drive OAuth2 và điền **Folder ID** chính xác cho thư mục chứa ảnh đầu ra và video đầu ra trên Drive của các sếp.
- **Create product image with model (HTTP Request):** Cấu hình Endpoint của Gemini API và nhúng `x-goog-api-key` vào phần Credentials hoặc Header. Tinh chỉnh lại Prompt trong body request nếu muốn phong cách ảnh thương hiệu riêng.
- **Create video & Get Link Video & Download video (HTTP Request - FAL AI):** Cấu hình FAL API Key với header `Authorization`. Node này sử dụng cơ chế Polling (kiểm tra trạng thái liên tục qua node **Wait** và **Filter**) cho đến khi `status == completed` thì mới tiến hành tải video về.
- **Update row in sheet (Google Sheets):** Cấu hình cập nhật lại cột `link_video`, `status` và `note` khi video đã được tạo và upload thành công lên Google Drive.

#### 3. Kích hoạt ⚡️
- Thử nghiệm bằng cách thêm một dòng dữ liệu mới vào Google Sheets với một `link_image` hợp lệ.
- Bấm **Execute Workflow** để test thủ công xem quá trình từ lúc lấy ảnh -> gọi Gemini -> gọi FAL -> upload Drive -> cập nhật Sheets có trơn tru không.
- Nếu mọi thứ xanh mướt (success), các sếp hãy bật **Active** để workflow tự động chạy ngầm 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Nối thêm node Telegram hoặc Slack ở cuối workflow để nhận thông báo ngay lập tức mỗi khi video sản phẩm được tạo xong.
- **Xử lý lỗi (Error Handling):** Thêm nhánh Error Trigger để ghi lại log lỗi vào cột `note` trong Google Sheets nếu FAL API hoặc Gemini gặp sự cố quá tải.
- **Xử lý hàng loạt (Batch Processing):** Các sếp có thể paste hàng chục dòng sản phẩm cùng lúc vào Google Sheets để hệ thống tự động xếp hàng (queue) và tạo video lần lượt.

### 📌 Kết luận
Workflow tự động hóa tạo video sản phẩm với Gemini, FAL AI và Google Workspace chính là mảnh ghép hoàn hảo giúp các shop online, agency marketing tối ưu hóa hiệu suất làm việc. Hãy cài đặt ngay hôm nay để đưa công nghệ AI vào quy trình kinh doanh của các sếp nhé!