---
title: "🚀 Tự động tạo ảnh sản phẩm và video thương mại điện tử bằng Gemini AI, DeepSeek & GoAPI"
description: "Xây dựng hệ thống tự động hóa 100% giúp tạo hình ảnh mẫu sản phẩm và video quảng cáo chuyên nghiệp cho thương mại điện tử từ mô tả văn bản và ảnh gốc nhờ AI."
slug: "tu-dong-tao-anh-video-san-pham-gemini-deepseek-goapi"
tags: [n8n, automation, ai, e-commerce, gemini, deepseek, goapi]
keywords: [n8n workflow, tạo ảnh sản phẩm ai, video marketing tự động, deepseek n8n, gemini ai n8n, goapi]
---

# 🚀 Tự động tạo ảnh sản phẩm và video thương mại điện tử bằng Gemini AI, DeepSeek & GoAPI

Việc sản xuất hình ảnh và video quảng cáo chất lượng cao cho các gian hàng thương mại điện tử (E-commerce) thường tốn rất nhiều thời gian, chi phí thuê studio, người mẫu và dựng phim thủ công. Khi cần cập nhật hàng trăm sản phẩm mỗi tuần, đội ngũ Marketing dễ rơi vào trạng thái quá tải và chậm trễ tiến độ.

Workflow n8n này chính là giải pháp tự động hóa toàn diện (All-in-One AI Automation) giúp các sếp giải quyết triệt để bài toán trên. Hệ thống kết hợp sức mạnh của các mô hình AI hàng đầu như **Google Gemini AI**, **DeepSeek** và **GoAPI** để tự động biến ý tưởng hoặc hình ảnh sản phẩm thô thành bộ ảnh mẫu (model & product images) cùng video quảng cáo chuyên nghiệp chỉ trong vài phút.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, xử lý các tác vụ nặng gọi API AI liên tục mà không lo bị ngắt quãng, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100% quy trình sáng tạo nội dung:** Từ một form yêu cầu đơn giản, AI tự sinh prompt, tạo ảnh sản phẩm gắn người mẫu và dựng video chuyển động.
- **Tiết kiệm 90% chi phí sản xuất:** Không cần thuê studio chụp ảnh hay editor dựng video đắt đỏ cho từng sản phẩm mới.
- **Đồng bộ hóa chất lượng & tốc độ:** Xử lý hàng loạt sản phẩm liên tục, trả kết quả trực tiếp qua giao diện Web Form, Chat hoặc lưu vết trên Discord.
- **Xử lý lỗi thông minh:** Tự động bắt lỗi và gửi thông báo qua Discord để đội ngũ kỹ thuật xử lý ngay khi có sự cố API.
:::

### Yêu cầu cần thiết
:::info[CHUẨN BỊ TRƯỚC KHI "LÊN ĐỒ"]
- **n8n Instance:** Đã cài đặt n8n (Khuyên dùng bản Self-hosted phiên bản mới nhất).
- **Google Palm / Gemini API Credentials:** Để sử dụng các node phân tích hình ảnh và ngôn ngữ (`Google Gemini Chat Model`, `Creative Visualiser`, `Product Visualiser`).
- **OpenRouter API Credentials:** Kết nối với các mô hình DeepSeek (`DeepSeek Chat V3`) cho các Agent sinh Prompt (`Model`, `Model1`, `Model2`, `Nano Banana Image`, `Generate Model with Product`).
- **GoAPI / Media Upload Service:** Dịch vụ lưu trữ/upload media trung gian (Node `Upload to MediaUpload`, `Generate Video`,...). *Lưu ý: Có thể thay thế bằng các dịch vụ upload ảnh như vgy.me hoặc Imgur nếu chưa có sẵn hệ thống host nội bộ.*
- **Discord Webhook API Credentials:** Để nhận log hệ thống và thông báo lỗi (Node `Send the Error`, `Discord1`).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow hoặc copy toàn bộ mã nguồn JSON.
- Trong giao diện n8n, chọn **Add workflow** -> Nhấp vào biểu tượng menu (3 chấm) ở góc trên bên phải -> Chọn **Import from File** hoặc **Import from Clipboard** và dán mã JSON vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Khi đã import thành công 37 nodes, các sếp cần cấu hình các thành phần trọng yếu sau:
- **Form 1 - Alpha (`formTrigger`)**: Điểm khởi đầu của quy trình. Các sếp có thể chỉnh sửa các trường thông tin đầu vào cho phép người dùng tải lên ảnh sản phẩm và nhập yêu cầu mô tả.
- **Google Gemini & OpenRouter Credentials**: Gắn các khóa API chính chủ vào các node AI Agent (`Product Prompt Agent`, `Model Prompt Generator`, `Creative Director`) và các mô hình ngôn ngữ (`Model`, `Model1`, `Model2`, `Google Gemini Chat Model...`).
- **HTTP Request / Media Upload Nodes** (`Nano Banana Image`, `Generate Model with Product`, `Upload to MediaUpload`, `Generate Video`):
  - Kiểm tra lại endpoint API của dịch vụ tạo ảnh/video (GoAPI hoặc các bên thứ ba tương đương).
  - Thay thế hoặc cấu hình lại service upload ảnh (như lưu ý trên canvas: *"Replace this any image uploader like vgy.me if you dont have a hosted version of mediaupload"*).
- **Discord Webhook (`Send the Error`, `Discord1`)**: Cấu hình URL Webhook của kênh Discord nội bộ để hệ thống tự động bắn thông báo kết quả hình ảnh/video hoặc báo cáo lỗi phát sinh (`Error Trigger`).

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (**Test run**) bằng cách điền thông tin qua Form hoặc sử dụng node `Only for Testing in n8n` (`chatTrigger`) để kiểm tra từng bước sinh prompt và gọi API ảnh/video.
- Sau khi test thành công và không còn lỗi, gạt công tắc **Active** ở góc trên cùng bên phải để đưa workflow vào vận hành tự động thực tế.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Google Sheets / Airtable:** Thêm một node Google Sheets ở cuối quy trình để lưu trữ lại link ảnh gốc, link ảnh mẫu và link video vừa tạo kèm theo thông tin sản phẩm phục vụ việc quản lý kho nội dung marketing.
- **Mở rộng kênh thông báo:** Thay vì chỉ gửi Discord, các sếp có thể kết nối thêm node **Telegram** hoặc **Slack** để gửi trực tiếp sản phẩm hoàn thiện đến nhóm duyệt bài của các sếp ngay lập tức.
- **Tối ưu Prompt AI:** Tùy chỉnh hệ thống prompt bên trong các AI Agent (`Product Prompt Agent`, `Creative Director`) để AI hiểu sâu hơn về phong cách thương hiệu (Brand Guidelines) của doanh nghiệp các sếp.

### 📌 Kết luận
Workflow tự động hóa kết hợp Gemini AI, DeepSeek và GoAPI là một "vũ khí tối tân" giúp tối ưu hóa toàn bộ khâu sản xuất hình ảnh và video thương mại điện tử. Hãy cài đặt ngay hôm nay để giải phóng sức lao động thủ công và bứt phá doanh số cùng AI!