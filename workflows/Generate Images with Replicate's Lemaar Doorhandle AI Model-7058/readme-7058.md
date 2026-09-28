---
title: "🚀 Tự động tạo hình ảnh thiết kế tay nắm cửa AI với Replicate và n8n"
description: "Hướng dẫn cấu hình và sử dụng workflow n8n để tự động hóa việc tạo nội dung hình ảnh sản phẩm sáng tạo bằng mô hình AI Lemaar Doorhandle trên Replicate."
slug: "tao-hinh-anh-tay-nam-cua-ai-replicate-n8n"
tags: [n8n, automation, replicate, ai-image-generation, content-creation, no-code]
keywords: [n8n workflow, tạo ảnh ai, replicate api, lemaar doorhandle, tự động hóa n8n]
---

# 🚀 Tự động tạo hình ảnh thiết kế tay nắm cửa AI với Replicate và n8n

Việc tạo ra các concept thiết kế sản phẩm hoặc hình ảnh marketing độc đáo thường đòi hỏi nhiều thời gian làm việc với các công cụ đồ họa thủ công hoặc thao tác đơn lẻ trên các nền tảng AI. Điều này gây tốn kém thời gian và khó khăn khi cần tạo ra số lượng lớn hình ảnh theo ý muốn.

Giải pháp ở đây là gì? Workflow n8n này sẽ giúp các sếp tự động hóa 100% quy trình gọi API đến mô hình AI **Lemaar Doorhandle** trên Replicate, từ việc gửi yêu cầu, kiểm tra trạng thái xử lý cho đến khi nhận được kết quả hoàn chỉnh mà không cần viết code phức tạp.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn**: Loại bỏ các thao tác thủ công khi phải truy cập web Replicate để tạo và chờ đợi kết quả từng ảnh một.
- **Tiết kiệm thời gian**: Xử lý các yêu cầu tạo ảnh số lượng lớn thông qua hệ thống tự động chạy nền.
- **Tích hợp linh hoạt**: Dễ dàng kết nối đầu ra hình ảnh với các nền tảng khác như Google Drive, Slack, hoặc Telegram.
- **Vận hành trơn tru**: Cơ chế kiểm tra trạng thái thông minh (Polling) giúp đảm bảo lấy được kết quả hình ảnh ngay khi AI hoàn thành quá trình render.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n**: Đã hoạt động (Self-hosted hoặc n8n Cloud).
- **Tài khoản Replicate**: Cần có tài khoản và lấy **Replicate API Key** để xác thực các HTTP Request.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow này từ thư viện n8n (Link gốc: [Replicate Lemaar Doorhandle AI Model](https://n8n.io/workflows/7058)) và tiến hành Import trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 8 nodes chính được thiết kế để xử lý vòng lặp gọi API bất đồng bộ. Các sếp cần chú ý cấu hình các node sau:

- **Node `Set API Key`**: 
  - Tại đây, các sếp cần cấu hình biến chứa Replicate API Key của mình để các node HTTP Request phía sau có quyền gọi tới API của Replicate.
- **Node `Create Prediction` (`httpRequest`)**: 
  - Kiểm tra endpoint gọi tới mô hình `creativeathive/lemaar-doorhandle-newset` trên Replicate.
  - Đảm bảo tham số đầu vào (`prompt`) được truyền đúng theo ý tưởng thiết kế tay nắm cửa mà các sếp muốn tạo.
- **Node `Extract Prediction ID` (`code`)**: 
  - Node này dùng đoạn mã JavaScript ngắn để trích xuất `prediction_id` trả về từ bước khởi tạo, phục vụ cho việc kiểm tra tiến độ.
- **Node `Wait`**: 
  - Khoảng thời gian chờ giữa các lần kiểm tra trạng thái render của AI, giúp tránh việc gửi quá nhiều request liên tục (Rate Limit).
- **Node `Check Prediction Status` (`httpRequest`)**: 
  - Gửi request kiểm tra xem mô hình AI đã render xong hình ảnh chưa dựa vào `prediction_id`.
- **Node `Check If Complete` (`if`)**: 
  - Kiểm tra điều kiện xem trạng thái trả về đã là `succeeded` (thành công) hay chưa để quyết định kết thúc vòng lặp hay tiếp tục đợi.
- **Node `Process Result` (`code`)**: 
  - Xử lý dữ liệu đầu ra cuối cùng, lấy link hình ảnh hoàn thiện để các sếp có thể sử dụng cho các bước tiếp theo trong quy trình.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** tại node `On clicking 'execute'` để chạy thử nghiệm với prompt mặc định và kiểm tra kết quả trả về.
- Sau khi test thành công, các sếp có thể chuyển trạng thái workflow sang **Active** để đưa vào vận hành thực tế.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng lưu trữ**: Kết nối thêm node Google Drive hoặc AWS S3 sau node `Process Result` để tự động tải và lưu trữ vĩnh viễn các hình ảnh AI vừa tạo.
- **Nhận thông báo qua Chat**: Thêm node Telegram hoặc Slack để gửi hình ảnh trực tiếp về nhóm làm việc ngay khi quá trình tạo ảnh hoàn tất.
- **Tự động hóa theo lịch trình**: Thay thế node `On clicking 'execute'` bằng node `Schedule Trigger` để hệ thống tự động tạo các mẫu thiết kế mới định kỳ mỗi ngày.

### 📌 Kết luận
Workflow tạo hình ảnh sản phẩm với Replicate và Lemaar Doorhandle là một công cụ mạnh mẽ giúp các doanh nghiệp, designer tự động hóa quy trình sáng tạo nội dung hình ảnh. Hãy cài đặt ngay hôm nay để tối ưu hóa hiệu suất công việc của các sếp!