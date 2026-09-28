---
title: "🚀 Tự động hóa tổng hợp tin tức và đăng bài lên mạng xã hội với GPT-4 và GetLate"
description: "Hướng dẫn chi tiết cách tự động hóa quá trình tổng hợp tin tức từ các trang báo, tạo nội dung mạng xã hội và đăng bài đồng thời trên nhiều nền tảng với n8n và OpenAI"
slug: "tu-dong-hoa-tong-hop-tin-tuc-dang-bai-mang-xa-hoi-gpt4-getlate"
tags: [n8n, automation, no-code, content creation, social media]
keywords: [n8n workflow, tự động hóa nội dung, tổng hợp tin tức, đăng bài mạng xã hội, OpenAI]
---

# 🚀 Tự động hóa tổng hợp tin tức và đăng bài lên mạng xã hội với GPT-4 và GetLate

[Đoạn mở đầu: Phân tích nỗi đau thực tế của các sếp khi phải làm thủ công việc tổng hợp tin tức, tạo nội dung mạng xã hội và đăng bài trên nhiều nền tảng. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian đáng kể trong việc tổng hợp tin tức và tạo nội dung
- Tự động hóa quá trình đăng bài đồng thời trên nhiều nền tảng (Twitter, Instagram, Threads, LinkedIn, YouTube)
- Tạo nội dung được tối ưu hóa cho các đối tượng trẻ
- Hoạt động liên tục 24/7 mà không cần can thiệp thủ công
- Tăng hiệu quả truyền thông và tiếp cận đối tượng mục tiêu
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản OpenAI API key đã được kết nối với n8n
- Tài khoản Google Drive để lưu trữ hình ảnh từ bài báo
- Tài khoản Late API với thông tin đăng nhập các nền tảng mạng xã hội
- Danh sách URL các bài báo cần tổng hợp
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Hướng dẫn import từ file JSON hoặc copy/paste JSON vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Edit Fields** (set):
   - Cập nhật danh sách URL các bài báo cần tổng hợp trong trường "urls"

2. **HTTP Request** (httpRequest):
   - Đảm bảo node này được cấu hình để lấy nội dung HTML của các bài báo

3. **Code** (code):
   - Kiểm tra và điều chỉnh đoạn mã JavaScript để trích xuất nội dung văn bản sạch từ HTML

4. **Message a model** (openAi):
   - Cấu hình credentials OpenAI API
   - Đảm bảo prompt được thiết lập để tổng hợp tin tức một cách khách quan

5. **Message a model1** (openAi):
   - Cấu hình credentials OpenAI API
   - Điều chỉnh prompt để tạo nội dung được tối ưu hóa cho đối tượng trẻ

6. **Upload file** (googleDrive):
   - Cấu hình credentials Google Drive
   - Chọn thư mục lưu trữ hình ảnh từ bài báo

7. **GetLate multipublishing** (httpRequest):
   - Cấu hình credentials Late API
   - Kiểm tra và cập nhật các tham số nền tảng mạng xã hội cần đăng bài

#### 3. Kích hoạt ⚡️
- Test run với dữ liệu mẫu để kiểm tra toàn bộ chuỗi xử lý
- Bật Active workflow sau khi đã kiểm tra kỹ kết quả

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node để lưu log các bài đăng đã được tạo
- Kết hợp với Slack/Telegram để nhận thông báo khi có bài mới được đăng
- Tạo báo cáo định kỳ về hiệu suất các bài đăng
- Thêm chức năng phân loại nội dung theo chủ đề để tự động hóa thêm
- Tích hợp với các công cụ phân tích mạng xã hội để theo dõi hiệu quả bài đăng

### 📌 Kết luận
Workflow này cung cấp giải pháp toàn diện cho việc tự động hóa tổng hợp tin tức và tạo nội dung mạng xã hội. Với khả năng xử lý đồng thời nhiều bài báo và đăng bài trên nhiều nền tảng, các sếp có thể tiết kiệm thời gian đáng kể và tăng hiệu quả truyền thông. Hãy thử nghiệm ngay để thấy sự khác biệt trong quá trình làm việc hàng ngày!