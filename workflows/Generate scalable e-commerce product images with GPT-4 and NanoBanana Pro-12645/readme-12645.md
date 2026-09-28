---
title: "🚀 Tự động tạo ảnh sản phẩm E-commerce chuyên nghiệp với GPT-4 và NanoBanana Pro trên n8n"
description: "Hướng dẫn chi tiết cách xây dựng hệ thống AI tự động hóa hoàn toàn quy trình tạo ảnh sản phẩm thương mại điện tử chất lượng cao từ 3 ảnh gốc bằng n8n, OpenAI và NanoBanana Pro."
slug: "tao-anh-san-pham-thuong-mai-dien-tu-tu-dong-gpt-4-nanobanana-pro"
tags: [n8n, automation, ai, e-commerce, openai, google-drive]
keywords: [n8n workflow, tạo ảnh sản phẩm ai, gpt-4 vision, nanobanana pro, tự động hóa e-commerce, n8n tiếng việt]
---

# 🚀 Tự động tạo ảnh sản phẩm E-commerce chuyên nghiệp với GPT-4 và NanoBanana Pro

Các sếp kinh doanh online chắc chắn hiểu rõ việc tạo ra những bức ảnh sản phẩm chuẩn studio tốn kém và mất thời gian thế nào. Thay vì thuê nhiếp ảnh gia và tốn hàng giờ chỉnh sửa, workflow n8n này sẽ giúp các sếp **tự động hóa 100% quy trình tạo ảnh sản phẩm thương mại điện tử chất lượng cao** chỉ từ 3 bức ảnh gốc thông qua sức mạnh của AI Vision (GPT-4) và NanoBanana Pro (AtlasCloud).

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa toàn diện:** Thu thập 3 ảnh từ Form, phân tích bằng AI, tạo prompt, sinh ảnh mới và lưu trữ tự động.
- **Chất lượng chuẩn studio:** Ứng dụng GPT-4 vision để hiểu sâu về sản phẩm và NanoBanana Pro để render ra những bức ảnh e-commerce cực kỳ bắt mắt.
- **Lưu trữ thông minh:** Tự động backup ảnh vào Google Drive và ghi log kết quả chi tiết lên Google Sheets.
- **Tiết kiệm chi phí:** Cắt giảm tối đa ngân sách thiết kế và chụp ảnh sản phẩm truyền thống.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để bắt đầu, các sếp cần chuẩn bị sẵn các tài khoản và API sau:
- **n8n Instance** (Self-hosted hoặc Cloud).
- **OpenAI API Key** (Dùng cho GPT-4 Vision và GPT-4.1-mini).
- **AtlasCloud API Key** (Dùng cho NanoBanana Pro API).
- **Google Drive & Google Sheets** (Tài khoản Google để lưu trữ file và ghi log).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp tiến hành copy mã JSON của workflow từ nguồn gốc hoặc import trực tiếp file JSON vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import thành công, các sếp cần cấu hình các thành phần sau:
- **Form Trigger (3 images):** Nơi người dùng tải lên đúng 3 bức ảnh sản phẩm gốc. Hãy giữ nguyên giới hạn đầu vào này để đảm bảo logic hoạt động chính xác.
- **Upload file & Upload file Nanobanana (Google Drive):** Kết nối tài khoản Google Drive qua OAuth2 và chọn thư mục lưu trữ đích trên Drive của sếp để lưu ảnh gốc và ảnh thành phẩm.
- **Analyze image & OpenAI Chat Model (OpenAI):** Thêm OpenAI API Credentials. Node này dùng GPT-4 để phân tích chi tiết nội dung của từng bức ảnh.
- **NanoBanana: Create Image & Build Public Image URL (HTTP Request):** Cấu hình AtlasCloud API Key để gửi yêu cầu tạo ảnh dựa trên public URL của ảnh gốc và prompt do AI sinh ra.
- **Append row in sheet (Google Sheets):** Kết nối Google Sheets API để ghi lại đường dẫn và thông tin chi tiết mỗi khi có ảnh mới được tạo thành công.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và test thử bằng cách điền form với 3 ảnh mẫu.
- Kiểm tra kết quả trên Google Drive, Google Sheets và bật trạng thái **Active** để đưa workflow vào vận hành thực tế.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Nối thêm node Telegram hoặc Slack sau bước hoàn thành để gửi ngay bức ảnh sản phẩm mới tạo về điện thoại cho các sếp kiểm tra.
- **Mở rộng lưu trữ:** Có thể thay thế hoặc bổ sung thêm lưu trữ ảnh lên các dịch vụ đám mây khác như AWS S3 hoặc Cloudinary.
- **Tạo bảng quản lý hàng loạt:** Kết hợp Google Sheets để xử lý danh sách hàng loạt (Batch processing) nếu các sếp có nhu cầu tạo ảnh cho hàng trăm sản phẩm cùng lúc.

### 📌 Kết luận
Workflow này là một "vũ khí" cực kỳ mạnh mẽ giúp tối ưu hóa quy trình sản xuất nội dung hình ảnh cho các doanh nghiệp thương mại điện tử. Hãy thiết lập ngay hôm nay để bứt phá doanh số với những hình ảnh sản phẩm triệu đô!