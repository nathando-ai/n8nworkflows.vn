---
title: "🚀 Tự động tạo ảnh AI độc đáo với mô hình Digitalhera Herathaisbragatto trên Replicate qua n8n"
description: "Hướng dẫn cấu hình workflow n8n tích hợp Replicate API để tự động hóa quy trình tạo ảnh nghệ thuật với mô hình digitalhera/herathaisbragatto nhanh chóng và hiệu quả."
slug: "tao-anh-ai-digitalhera-herathaisbragatto-replicate-n8n"
tags: [n8n, automation, no-code, replicate, ai-image-generation]
keywords: [n8n workflow, tự động hóa tạo ảnh ai, replicate api, digitalhera herathaisbragatto, n8n httpRequest]
---

# 🚀 Tự động tạo ảnh AI đỉnh cao với mô hình Digitalhera Herathaisbragatto qua Replicate

Các sếp có đang tốn quá nhiều thời gian để truy cập thủ công vào các nền tảng tạo ảnh AI, nhập prompt, chờ đợi và tải xuống từng bức hình phục vụ cho chiến dịch Marketing hay sáng tạo nội dung không? Việc làm thủ công này không chỉ ngốn thời gian mà còn khó scale khi cần sản xuất số lượng lớn hình ảnh chất lượng cao.

Giải pháp ở đây là gì? Workflow n8n tích hợp **Replicate API** sẽ giúp các sếp tự động hóa 100% quy trình gọi mô hình AI **digitalhera/herathaisbragatto** để tạo ảnh tự động chỉ bằng một cú click hoặc thông qua một trigger bất kỳ!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn**: Gửi prompt và nhận kết quả hình ảnh từ mô hình Replicate mà không cần thao tác thủ công trên giao diện web.
- **Tiết kiệm thời gian**: Loại bỏ hoàn toàn các bước chờ đợi thủ công nhờ cơ chế kiểm tra trạng thái (Polling) thông minh bằng node `Wait` và `If`.
- **Dễ dàng mở rộng**: Có thể tích hợp thêm các bước lưu trữ ảnh vào Google Drive, gửi về Telegram/Slack hoặc đăng tự động lên mạng xã hội.
- **Hoạt động liên tục**: Xử lý mượt mà, ổn định trên nền tảng n8n self-hosted hoặc cloud.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một instance n8n đang hoạt động.
- Tài khoản **Replicate** và **API Token** cá nhân để xác thực các HTTP Request.
- Prompt mô tả ý tưởng bức ảnh các sếp muốn tạo.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể sử dụng file JSON của workflow này, copy đoạn mã nguồn JSON và paste trực tiếp vào giao diện n8n Editor của mình để bắt đầu.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này bao gồm 8 nodes được liên kết chặt chẽ để xử lý quá trình gọi API bất đồng bộ từ Replicate:
- **Set API Key (`set`)**: Node này lưu trữ Replicate API Key của các sếp. Hãy điền Token của sếp vào phần giá trị cấu hình của node này.
- **Create Prediction (`httpRequest`)**: Node này gửi yêu cầu khởi tạo tiến trình tạo ảnh đến endpoint của Replicate kèm theo prompt và model `digitalhera/herathaisbragatto`. Hãy kiểm tra lại phần body để đảm bảo prompt truyền vào chính xác theo ý muốn.
- **Extract Prediction ID (`code`)**: Trích xuất mã định danh (Prediction ID) từ kết quả phản hồi của bước khởi tạo để phục vụ cho việc theo dõi tiến độ.
- **Wait (`wait`)**: Tạo độ trễ nhất định giữa các lần kiểm tra trạng thái để tránh việc gửi quá nhiều request liên tục (Rate Limit) lên phía Replicate.
- **Check Prediction Status (`httpRequest`)**: Gửi request kiểm tra xem bức ảnh đã được render xong hay chưa dựa trên Prediction ID đã lấy ở bước trước.
- **Check If Complete (`if`)**: Kiểm tra điều kiện xem trạng thái trả về từ Replicate đã ở trạng thái `succeeded` hay chưa. Nếu chưa, vòng lặp sẽ quay lại chờ tiếp; nếu rồi, sẽ chuyển sang bước xử lý kết quả.
- **Process Result (`code`)**: Xử lý dữ liệu đầu ra, trích xuất đường dẫn URL của bức ảnh hoàn chỉnh để các sếp có thể sử dụng cho các bước tiếp theo.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** để chạy thử nghiệm (Manual Trigger) với dữ liệu mẫu.
- Kiểm tra kết quả trả về ở node cuối cùng để đảm bảo link ảnh hiển thị chính xác.
- Bật công tắc **Active** để đưa workflow vào trạng thái sẵn sàng hoạt động tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo**: Kết nối thêm node Telegram hoặc Slack ngay sau node `Process Result` để bot tự động gửi ảnh vừa tạo về nhóm chat ngay khi hoàn thành.
- **Lưu trữ tự động**: Thêm node Google Drive hoặc S3 để tải và lưu trữ vĩnh viễn các bức ảnh AI tạo ra, tránh việc link ảnh trên Replicate hết hạn.
- **Webform Input**: Thay thế node `On clicking 'execute'` bằng node `Webhook` hoặc `Form Trigger` để tạo một giao diện nhập prompt đơn giản cho team sử dụng.

### 📌 Kết luận
Workflow tự động hóa tạo ảnh AI với mô hình `digitalhera/herathaisbragatto` trên Replicate là một mảnh ghép tuyệt vời giúp tối ưu hóa quy trình sáng tạo nội dung hình ảnh của doanh nghiệp. Hãy áp dụng ngay hôm nay để tiết kiệm thời gian và bứt phá hiệu suất công việc cùng n8n!