---
title: "🚀 Tự động tạo ảnh AI chất lượng cao với Havis AI Seedream 5 Lite trên n8n"
description: "Hướng dẫn xây dựng workflow n8n tích hợp Havis AI Seedream 5 Lite để tự động hóa quy trình tạo ảnh AI từ form người dùng, xử lý hàng đợi và trả về kết quả mượt mà."
slug: "tao-anh-ai-tu-dong-voi-havis-ai-seedream-5-lite-n8n"
tags: [n8n, automation, ai-images, havis-ai, content-creation, no-code]
keywords: [n8n workflow, tạo ảnh ai tự động, havis ai seedream 5, hhtp request n8n, no-code ai automation]
---

# 🚀 Tự động tạo ảnh AI chất lượng cao với Havis AI Seedream 5 Lite trên n8n

Việc tạo ảnh bằng AI qua các giao diện web thông thường thường tốn thời gian và khó tích hợp vào quy trình làm việc tự động của doanh nghiệp. Các sếp có bao giờ gặp khó khăn khi phải vừa nhập prompt, vừa chọn tỉ lệ, lại vừa phải ngồi chờ task hoàn thành để tải ảnh về chưa? 

Giải pháp cho các sếp đây! Bài viết này sẽ hướng dẫn chi tiết cách vận hành workflow n8n tích hợp **Havis AI Seedream 5 Lite**. Workflow này giúp các sếp tạo một trang Form công khai để thu thập yêu cầu, tự động gửi đến API của Havis AI, thông minh lặp (polling) kiểm tra trạng thái và trả về kết quả ảnh tuyệt đẹp ngay khi hoàn thành mà không cần tốn một dòng code thủ công nào.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn**: Biến một quy trình thủ công thành một Web Form chuyên nghiệp để cộng sự hoặc khách hàng tự tạo ảnh.
- **Cơ chế Polling thông minh**: Workflow tự động chờ và kiểm tra tiến độ tạo ảnh từ Havis AI mà không làm treo hệ thống.
- **Linh hoạt cấu hình**: Hỗ trợ đầy đủ các tham số như prompt, chế độ (mode), tỷ lệ khung hình (aspect_ratio), chất lượng và các hình ảnh đầu vào tùy chọn.
- **Xử lý lỗi chuẩn xác**: Phân nhánh rõ ràng giữa trạng thái thành công và thất bại, trả về thông tin chi tiết credit đã sử dụng và link ảnh kết quả.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một hệ thống **n8n** đang hoạt động (Cloud hoặc Self-hosted).
- Tài khoản tại **Havis AI** và lấy **API Key** tại trang [Havis AI Profile](https://havis.ai/manager/profile).
- Tài khoản có đủ credit để thực hiện các yêu cầu tạo ảnh.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp tiến hành copy đoạn mã JSON của workflow (hoặc tải file JSON) và tiến hành Import trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import thành công, các sếp sẽ thấy một sơ đồ gồm 10 nodes. Hãy chú ý các điểm cốt lõi sau:

- **Node `Form - Seedream 5 Lite` (formTrigger)**: 
  - Đây là nơi tạo ra giao diện Public Form. Các sếp có thể mở URL của form này sau khi Active workflow để bắt đầu nhập dữ liệu (prompt, mode, aspect_ratio, quality, image_url...).
  - Đảm bảo form thu thập thêm trường nhập **Havis API Key** của người dùng để xác thực.

- **Node `Build Payload` (code)**: 
  - Node này sử dụng JavaScript để làm sạch các giá trị trống, áp dụng cấu hình mặc định và đóng gói thành JSON body chuẩn chỉnh gửi cho Havis API.

- **Node `Submit - Havis API` (httpRequest)**: 
  - Cấu hình phương thức `POST` tới endpoint `https://havis.ai/api/seedream-5`.
  - Thiết lập Header xác thực sử dụng Bearer Token lấy từ giá trị người dùng nhập ở Form (`Authorization: Bearer <Havis_API_Key>`).

- **Các Node kiểm tra trạng thái (`Wait 8s`, `Check Task Status`, `Is Completed?`, `Is Failed?`)**:
  - Workflow sử dụng vòng lặp thông minh để gọi API kiểm tra trạng thái task (`https://havis.ai/api/task/{task_id}`). Thời gian chờ giữa các lần gọi mặc định là 8 giây. Các sếp có thể điều chỉnh thời gian này nếu cần tăng tốc độ kiểm tra.

- **Node `Return Result` & `Return Error` (set)**:
  - Trả về thông tin metadata, số credit đã dùng, thông tin payload và link dẫn tới bức ảnh hoàn thiện (hoặc thông báo lỗi chi tiết nếu task thất bại).

#### 3. Kích hoạt ⚡️
- Thực hiện **Test workflow** bằng cách điền thử một prompt mẫu trên Form để kiểm tra dòng dữ liệu chạy qua từng node.
- Sau khi chạy thử nghiệm thành công và nhận được ảnh trả về, các sếp gạt công tắc sang **Active** để đưa workflow vào vận hành chính thức.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo**: Kết nối thêm node **Telegram** hoặc **Slack** ngay sau node `Return Result` để bot tự động gửi ảnh vừa tạo về nhóm chat ngay khi hoàn thành.
- **Lưu trữ tự động**: Thêm node **Google Drive** hoặc **Supabase** để tải file ảnh từ URL kết quả về lưu trữ dài hạn, tránh trường hợp link tạm của Havis AI hết hạn.
- **Mở rộng quy mô**: Cho phép tạo hàng loạt (batch generation) bằng cách kết hợp thêm node Split In Batches nếu các sếp cần tạo nhiều biến thể ảnh cùng một lúc.

### 📌 Kết luận
Workflow tích hợp Havis AI Seedream 5 Lite trên n8n là một trợ thủ đắc lực cho các nhà sáng tạo nội dung, marketer hay nhà phát triển muốn tự động hóa quy trình sản xuất hình ảnh AI. Hãy thiết lập ngay hôm nay để tối ưu hóa thời gian và nâng tầm hiệu suất công việc của các sếp nhé!