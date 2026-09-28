---
title: "🚀 Tự động tạo Mockup sản phẩm Thương mại điện tử từ hình ảnh gốc với OpenAI DALL-E, remove.bg và Google Drive"
description: "Hướng dẫn chi tiết cách xây dựng workflow n8n tự động xóa phông, tạo hình ảnh mockup sản phẩm chuyên nghiệp bằng AI và lưu trữ trực tiếp lên Google Drive."
slug: "tu-dong-tao-mockup-san-pham-thuong-mai-dien-tu-n8n"
tags: [n8n, automation, no-code, ecommerce, ai, openai, dalle, googledrive]
keywords: [n8n workflow, tạo mockup sản phẩm, remove bg, openai dalle, google drive automation, tự động hóa e-commerce]
---

# 🚀 Tự động tạo Mockup sản phẩm Thương mại điện tử với OpenAI DALL-E và Google Drive

Trong ngành Thương mại điện tử, việc sở hữu những hình ảnh sản phẩm (mockup) bắt mắt, đặt trong bối cảnh thực tế đóng vai trò quyết định tỷ lệ chuyển đổi của khách hàng. Tuy nhiên, quy trình truyền thống đòi hỏi designer phải tốn hàng giờ đồng hồ để chụp ảnh, tách nền thủ công bằng Photoshop và ghép vào các background khác nhau. 

Được phát triển bởi **SpaGreen Creative**, workflow n8n này sẽ giúp các sếp tự động hóa toàn bộ quy trình: nhận ảnh gốc từ form, tự động xóa phông, sử dụng AI (OpenAI DALL-E) để tạo mockup sinh động và lưu trữ toàn bộ file kết quả lên Google Drive một cách chuyên nghiệp!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Không cần thao tác thủ công trên Photoshop cho từng sản phẩm.
- **Hình ảnh chuyên nghiệp:** Kết hợp sức mạnh AI từ OpenAI DALL-E tạo ra các mockup bối cảnh chân thực, thu hút khách hàng mua sắm.
- **Tự động hóa lưu trữ:** Phân loại và lưu trữ ảnh gốc tách nền (PNG) và ảnh mockup trực tiếp vào các thư mục Google Drive tương ứng.
- **Giao diện thân thiện:** Tích hợp Form trực quan giúp người dùng dễ dàng tải ảnh lên và nhận kết quả nhanh chóng.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Tài khoản OpenAI:** Cần có API Key đã nạp tiền để sử dụng node **Generate an image** (DALL-E).
- **Tài khoản remove.bg (hoặc API tương đương):** Dùng cho các node **Remove Image Background** để tách nền sản phẩm.
- **Google Drive Account:** Đã cấu hình Credentials OAuth2 để các node **Upload Mockup Image** và **Upload PNG Image** có quyền đẩy file lên Drive.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow này và dán trực tiếp vào n8n Editor của mình, hoặc import file JSON tải từ kho lưu trữ.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống hoạt động mượt mà, các sếp cần chú ý cấu hình các node cốt lõi sau:

- **Form submission (`formTrigger`)**: Thiết lập giao diện form đầu vào để khách hàng hoặc nhân viên kho tải file ảnh sản phẩm lên.
- **Remove Image Background & Remove Image Background2 (`httpRequest`)**: Cấu hình API endpoint và API Key của dịch vụ xóa phông (như remove.bg) để làm sạch nền ảnh sản phẩm ban đầu.
- **Generate an image & Generate an image2 (`openAi`)**: Kết nối tài khoản OpenAI Credentials, tinh chỉnh câu lệnh (prompt) mô tả bối cảnh mockup mong muốn (ví dụ: đặt trên bàn gỗ, phòng khách hiện đại, ánh sáng studio...) để DALL-E tạo ra hình ảnh chất lượng cao.
- **HTTP (download image...) (`httpRequest`)**: Các node này chịu trách nhiệm tải hình ảnh đã được tạo ra từ URL trả về của OpenAI về bộ nhớ tạm của n8n trước khi đẩy lên Drive.
- **Upload Mockup Image & Upload PNG Image (`googleDrive`)**: Chọn đúng tài khoản Google Drive và trỏ đến ID thư mục (Folder ID) cụ thể trên Drive để lưu trữ file ảnh gọn gàng, tránh thất lạc.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và test thử bằng cách gửi dữ liệu qua form để kiểm tra toàn bộ luồng chạy từ đầu đến cuối.
- Kiểm tra kết quả trên Google Drive xem file ảnh mockup và ảnh tách nền đã xuất hiện chưa.
- Nếu mọi thứ trơn tru, bật công tắc **Active** góc trên bên phải để đưa workflow vào vận hành chính thức 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Thêm node Telegram hoặc Slack ở cuối luồng để gửi tin nhắn thông báo kèm link Google Drive ngay khi mockup được tạo xong.
- **Quản lý Database:** Kết nối thêm Google Sheets hoặc Airtable để lưu lại lịch sử tạo mockup kèm theo link hình ảnh phục vụ việc tra cứu sau này.
- **Đa dạng hóa phong cách:** Tạo nhiều nhánh form khác nhau cho phép người dùng chọn style mockup (hiện đại, tối giản, vintage) rồi truyền biến đó vào prompt của OpenAI DALL-E.

### 📌 Kết luận
Workflow tự động hóa tạo mockup sản phẩm từ SpaGreen Creative là một "vũ khí" cực kỳ lợi hại cho các doanh nghiệp E-commerce muốn tối ưu hóa hình ảnh sản phẩm với chi phí và thời gian tối thiểu. Hãy triển khai ngay hôm nay để nâng tầm chuyên nghiệp cho gian hàng của các sếp!