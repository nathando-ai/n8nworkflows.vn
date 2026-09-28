---
title: "🚀 Tự động tạo và chỉnh sửa ảnh đỉnh cao với Havis AI Nano Banana 2 trên n8n"
description: "Hướng dẫn cài đặt và sử dụng workflow n8n tích hợp Havis AI Nano Banana 2 giúp tự động hóa quy trình tạo ảnh, chỉnh sửa hình ảnh đa phương thức thông qua giao diện Web Form tiện lợi."
slug: "tu-dong-tao-va-chinh-sua-anh-voi-havis-ai-nano-banana-2"
tags: [n8n, automation, ai-image-generation, havis-ai, no-code, content-creation]
keywords: [n8n workflow, havis ai, nano banana 2, tạo ảnh bằng ai, tự động hóa n8n, ai multimodal]
---

# 🚀 Tự động tạo và chỉnh sửa ảnh đỉnh cao với Havis AI Nano Banana 2 trên n8n

Việc tạo và chỉnh sửa hình ảnh hàng loạt bằng AI thường tốn rất nhiều thời gian khi phải thao tác thủ công trên các giao diện web, cấu hình thông số lặp đi lặp lại và chờ đợi kết quả. Giải pháp sử dụng **Havis AI Nano Banana 2** kết hợp cùng **n8n** sẽ giúp các sếp xây dựng một hệ thống tự động hóa hoàn toàn (100% no-code): nhận yêu cầu qua Web Form, gửi lệnh tạo ảnh, tự động kiểm tra trạng thái (polling) và trả về kết quả ngay khi hoàn tất.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Web Form tiện lợi:** Cung cấp giao diện công khai để nhập prompt, cấu hình chế độ, tỷ lệ khung hình và tải ảnh lên nhanh chóng.
- **Xử lý bất đồng bộ thông minh:** Tự động gọi API, chờ đợi (poll) trạng thái tác vụ cho đến khi hoàn thành mà không sợ bị timeout.
- **Quản lý tài nguyên tối ưu:** Trả về metadata chi tiết, số lượng credit đã sử dụng và đường dẫn URL hình ảnh kết quả.
- **Hoạt động 24/7:** Tích hợp cơ chế phân nhánh (If nodes) để xử lý thành công hoặc trả về lỗi rõ ràng khi tiến trình thất bại.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Hệ thống n8n (Cloud hoặc Self-hosted).
- Tài khoản và **Havis API Key** (Lấy tại [Havis AI Manager Profile](https://havis.ai/manager/profile)).
- Tài khoản Havis AI đã được nạp đủ credit để thực hiện các yêu cầu tạo/chỉnh sửa ảnh.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow từ [Havis AI Nano Banana 2 Workflow](https://n8n.io/workflows/15586), sau đó tiến hành import trực tiếp vào n8n Editor của các sếp bằng tính năng **Import from File** hoặc copy/paste mã nguồn JSON.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm các node chính sau đây cần nắm rõ cách vận hành:
- **Form - Nano Banana 2 (`formTrigger`):** Node khởi chạy giao diện Web Form. Sau khi import, các sếp có thể mở URL của form để nhập các thông số đầu vào như: `prompt`, `mode`, `aspect_ratio`, `resolution`, `output_format`, và các URL ảnh gốc (`image_url_1`,...).
- **Build Payload (`code`):** Node xử lý mã nguồn JavaScript giúp làm sạch dữ liệu, loại bỏ các giá trị trống, áp dụng các tùy chọn mặc định và đóng gói thành JSON Body chuẩn xác gửi lên Havis API.
- **Submit - Havis API (`httpRequest`):** Node gửi yêu cầu POST đến endpoint `https://havis.ai/api/nano-banana-2` kèm theo Bearer Token (Havis API Key). Node này sẽ trả về `task_id` và số credit tiêu thụ.
- **Wait 8s & Check Task Status (`wait` & `httpRequest`):** Bộ đôi node thực hiện cơ chế chờ 8 giây và gọi endpoint `https://havis.ai/api/task/{task_id}` để kiểm tra tiến độ xử lý của AI.
- **Is Completed? & Is Failed? (`if`):** Các node phân nhánh logic kiểm tra xem tác vụ đã hoàn thành hay gặp lỗi để quyết định tiếp tục vòng lặp (`Wait 8s (loop)`) hay trả về kết quả (`Return Result` / `Return Error`).

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và test thử điền thông tin trên Web Form để kiểm tra toàn bộ luồng dữ liệu.
- Sau khi test thành công, gạt công tắc sang trạng thái **Active** để đưa workflow vào vận hành chính thức.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Nối thêm node Telegram hoặc Slack vào sau node `Return Result` để bot tự động gửi hình ảnh vừa tạo về nhóm chat ngay khi hoàn thành.
- **Lưu trữ tự động:** Kết hợp với node Google Sheets hoặc Airtable để lưu lại lịch sử prompt, thông tin task ID và link ảnh phục vụ cho việc quản lý nội dung.
- **Tùy chỉnh thời gian chờ:** Điều chỉnh thời gian ở node `Wait 8s` nếu các sếp muốn tăng hoặc giảm tốc độ kiểm tra trạng thái task tùy theo độ phức tạp của ảnh.

### 📌 Kết luận
Workflow tích hợp Havis AI Nano Banana 2 là một công cụ cực kỳ mạnh mẽ giúp cá nhân hóa và tự động hóa quy trình sáng tạo hình ảnh. Hãy import ngay vào hệ thống n8n của các sếp để tối ưu hóa hiệu suất công việc ngay hôm nay!