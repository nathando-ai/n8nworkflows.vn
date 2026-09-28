---
title: "🚀 Tự động tạo hình ảnh AI độc đáo với mô hình Lorealcantara qua Replicate API trên n8n"
description: "Hướng dẫn chi tiết cách xây dựng và cấu hình n8n workflow để tự động hóa quy trình tạo ảnh nghệ thuật bằng mô hình AI ligua033/lorealcantara thông qua Replicate API."
slug: "tao-anh-ai-lorealcantara-replicate-n8n"
tags: [n8n, automation, ai-image-generation, replicate-api, content-creation, no-code]
keywords: [n8n workflow, tạo ảnh AI, Replicate API, Lorealcantara, tự động hóa n8n, AI art generation]
---

# 🚀 Tự động tạo hình ảnh AI độc đáo với mô hình Lorealcantara qua Replicate API

Các sếp có bao giờ cảm thấy quá tốn thời gian khi phải truy cập vào các nền tảng tạo ảnh AI thủ công, nhập prompt, chờ đợi và tải từng bức ảnh về máy không? Quy trình làm nội dung trực quan đôi khi bị gián đoạn chỉ vì những thao tác lặp đi lặp lại đó.

Đừng lo, giải pháp đã ở đây! Bài viết này sẽ hướng dẫn các sếp cách tự động hóa hoàn toàn quy trình tạo ảnh AI chất lượng cao bằng mô hình **ligua033/lorealcantara** thông qua **Replicate API** kết hợp với **n8n**. Không cần biết code phức tạp, các sếp vẫn có thể sở hữu một "nhà máy" sản xuất hình ảnh tự động 24/7.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%**: Gửi yêu cầu và nhận lại hình ảnh hoàn chỉnh từ mô hình Lorealcantara mà không cần thao tác thủ công trên web.
- **Tiết kiệm thời gian**: Tối ưu hóa quy trình sáng tạo nội dung, marketing hoặc thiết kế.
- **Quy trình thông minh**: Tích hợp cơ chế chờ (Wait) và kiểm tra trạng thái (Check Prediction Status) tự động để đảm bảo lấy được kết quả khi AI render xong.
- **Dễ dàng mở rộng**: Có thể kết hợp thêm Google Sheets để lưu prompt hàng loạt hoặc gửi ảnh trực tiếp về Telegram/Slack.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n**: Đã cài đặt sẵn (Self-hosted hoặc n8n Cloud).
- **Tài khoản Replicate**: Truy cập [Replicate](https://replicate.com/) để lấy **API Key**.
- **Mô hình AI**: Sử dụng mô hình `ligua033/lorealcantara` trên Replicate.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần tạo một workflow mới trên n8n, sau đó copy toàn bộ mã JSON của workflow (hoặc sử dụng file JSON được cung cấp từ nguồn gốc) và paste trực tiếp vào giao diện n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 8 nodes được bố trí thông minh để xử lý bất đồng bộ từ Replicate API:

- **On clicking 'execute' (`manualTrigger`)**: Nút bấm thủ công để bắt đầu chạy thử workflow. Các sếp có thể thay thế bằng Webhook hoặc Schedule Trigger nếu muốn chạy tự động theo lịch.
- **Set API Key (`set`)**: Node này lưu trữ Replicate API Key của các sếp. Hãy điền mã API của mình vào đây (hoặc cấu hình dưới dạng n8n Credentials để bảo mật hơn).
- **Create Prediction (`httpRequest`)**: Gửi yêu cầu tạo ảnh đến Replicate API sử dụng mô hình `ligua033/lorealcantara` với các tham số (prompt) được định nghĩa sẵn.
- **Extract Prediction ID (`code`)**: Trích xuất mã ID định danh của tiến trình tạo ảnh từ phản hồi của API.
- **Wait (`wait`)**: Tạm dừng luồng trong vài giây để hệ thống AI kịp xử lý hình ảnh.
- **Check Prediction Status (`httpRequest`)**: Gửi yêu cầu kiểm tra xem tiến trình tạo ảnh đã hoàn tất hay chưa dựa vào Prediction ID.
- **Check If Complete (`if`)**: Kiểm tra trạng thái. Nếu ảnh đã tạo xong, chuyển sang bước xử lý kết quả; nếu chưa, có thể cấu hình lặp lại.
- **Process Result (`code`)**: Nhận kết quả cuối cùng, trích xuất đường dẫn URL của bức ảnh hoàn chỉnh để các sếp sử dụng cho các bước tiếp theo.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** để test thử với prompt mặc định.
- Kiểm tra kết quả trả về ở node cuối cùng để đảm bảo link ảnh hiển thị chính xác.
- Bật **Active** để đưa workflow vào trạng thái vận hành tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết nối Google Sheets**: Thay vì dùng node Trigger thủ công, các sếp có thể đọc danh sách prompt từ Google Sheets và ghi ngược link ảnh đã tạo vào bảng tính đó.
- **Gửi thông báo Telegram/Slack**: Tích hợp thêm node gửi tin nhắn để hệ thống tự động bắn bức ảnh vừa tạo thẳng vào nhóm chat của team.
- **Lưu trữ tự động**: Kết hợp node tải file ảnh về Google Drive hoặc AWS S3 để lưu trữ lâu dài.

### 📌 Kết luận
Với workflow n8n tích hợp Replicate API này, việc tạo ra những tác phẩm nghệ thuật độc đáo từ mô hình Lorealcantara trở nên dễ dàng và tự động hơn bao giờ hết. Hãy "lên đồ" ngay cho hệ thống của các sếp để tối ưu hóa hiệu suất công việc thôi nào!