---
title: "🚀 Tự động hóa tạo nội dung đa phương thức với Lemaar Door Urban AI và Replicate API trong n8n"
description: "Hướng dẫn chi tiết cách xây dựng workflow n8n tích hợp Replicate API để tự động hóa quy trình tạo nội dung hình ảnh/AI với mô hình Lemaar Door Urban một cách chuyên nghiệp."
slug: "tu-dong-hoa-tao-noi-dung-lemaar-door-urban-replicate-n8n"
tags: [n8n, automation, replicate, ai-generation, no-code, multimodal-ai]
keywords: [n8n workflow, replicate api, lemaar door urban, tao noi dung ai, tu dong hoa n8n, ai image generation]
---

# 🚀 Tự động hóa tạo nội dung đa phương thức với Lemaar Door Urban AI và Replicate API

Các sếp có đang gặp khó khăn khi phải thao tác thủ công trên các nền tảng tạo ảnh AI, mất thời gian copy-paste prompt, chờ đợi kết quả và tải xuống từng file một? Việc này không chỉ tốn thời gian mà còn đứt gãy chuỗi sáng tạo khi các sếp cần sản xuất hàng loạt nội dung trực quan cho chiến dịch Marketing.

Giải pháp ở đây là gì? Hãy để n8n lo! Bài viết này sẽ hướng dẫn các sếp triển khai một workflow tự động hóa toàn diện, kết nối trực tiếp với **Replicate API** để điều khiển mô hình AI `creativeathive/lemaar-door-urban` tạo nội dung một cách mượt mà, thông minh và có cơ chế kiểm tra trạng thái tự động.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100% quy trình gọi AI**: Không cần thao tác thủ công trên web của Replicate, mọi thứ diễn ra khép kín trong n8n.
- **Cơ chế chờ & kiểm tra thông minh**: Workflow tự động ping kiểm tra trạng thái render của AI, xử lý mượt mà các trạng thái thành công hay thất bại.
- **Tối ưu thời gian và chi phí**: Giúp các sếp dễ dàng tích hợp khả năng sinh ảnh AI vào các hệ thống CRM, Chatbot hoặc công cụ quản lý nội dung sẵn có.
- **Dễ dàng mở rộng**: Nền tảng n8n cho phép gắn thêm các bước lưu file tự động về Google Drive, gửi thông báo qua Telegram hoặc Slack ngay khi có kết quả.
:::

### ☕ Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n**: Đã cài đặt sẵn (Self-hosted hoặc n8n Cloud).
- **Tài khoản Replicate**: Truy cập [Replicate](https://replicate.com) để lấy API Token cá nhân.
- **Workflow Template**: File JSON cấu hình gồm 13 nodes (được cung cấp từ nguồn của chuyên gia Yaron Been).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow hoặc sao chép toàn bộ mã nguồn JSON.
- Mở giao diện n8n Editor, chọn **Add workflow** -> Click vào dấu ba chấm (...) ở góc trên bên phải -> Chọn **Import from File** hoặc **Import from Clipboard**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này bao gồm 13 nodes cốt lõi được thiết kế mạch lạc. Các sếp cần chú ý cấu hình các điểm sau:

- **Node `Set API Token`**: Đây là nơi lưu trữ khóa API của sếp. Hãy thay thế chuỗi `'YOUR_REPLICATE_API_TOKEN'` bằng API Token thực tế từ tài khoản Replicate của sếp.
- **Node `Set Other Parameters`**: Nơi các sếp định hình nội dung đầu ra cho AI. Các tham số quan trọng cần lưu ý:
  - `prompt`: Câu lệnh mô tả hình ảnh/nội dung mong muốn (nhớ kèm theo trigger word nếu mô hình yêu cầu).
  - Các tham số tùy chọn khác như `width`, `height`, `seed`, `aspect_ratio` để tinh chỉnh chất lượng đầu ra.
- **Node `Create Other Prediction` & `Check Status` (HTTP Request)**: Đảm bảo Endpoint gọi API trỏ chính xác tới `https://api.replicate.com/v1/predictions`.
- **Node `Wait 5s` & `Wait 10s` (Wait)**: Duy trì khoảng nghỉ hợp lý để tránh việc gửi quá nhiều request liên tục (Rate Limit) lên hệ thống của Replicate trong lúc AI đang render.
- **Node `Is Complete?` & `Has Failed?` (If)**: Các nhánh điều kiện rẽ luồng xử lý tùy thuộc vào trạng thái trả về từ API (thành công, đang chạy, hay lỗi).

#### 3. Kích hoạt ⚡️
- Bấm nút **Execute Workflow** tại node **Manual Trigger** để chạy thử nghiệm (Test run) với dữ liệu mẫu.
- Kiểm tra kết quả trả về tại node **Display Result** và **Log Request**.
- Nếu mọi thứ hoạt động trơn tru, hãy gạt công tắc **Active** ở góc trên cùng bên phải để đưa workflow vào trạng thái chạy tự động thực tế.

### ✍️ Mẹo & gợi ý nâng cao
Để nâng cấp workflow này thành một con "quái vật" tự động hóa thực thụ, các sếp có thể triển khai thêm:
1. **Tích hợp Telegram/Slack Bot**: Thêm node gửi thông báo kèm hình ảnh trực tiếp về nhóm chat ngay khi AI render xong.
2. **Lưu trữ tự động**: Kết nối node **Google Drive** hoặc **AWS S3** để tự động tải và lưu trữ vĩnh viễn các tệp hình ảnh được tạo ra.
3. **Mở rộng nguồn Trigger**: Thay thế **Manual Trigger** bằng **Webhook** hoặc **Google Sheets** để kích hoạt tạo ảnh hàng loạt từ danh sách prompt có sẵn.

### 📌 Kết luận
Việc tích hợp các mô hình AI mạnh mẽ như Lemaar Door Urban thông qua Replicate API vào n8n mở ra vô số cơ hội tối ưu hóa quy trình sản xuất nội dung số cho doanh nghiệp. Hãy bắt tay vào cài đặt ngay hôm nay để giải phóng sức lao động và tăng tốc độ sáng tạo của các sếp!