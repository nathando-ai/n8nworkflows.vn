---
title: "🚀 Tự động tạo ảnh quảng cáo E-commerce không giới hạn với AI và Google Drive"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa quy trình tạo hàng loạt hình ảnh quảng cáo sản phẩm thương mại điện tử kết hợp ảnh influencer bằng AI."
slug: "tao-anh-quang-cao-e-commerce-tu-dong-voi-n8n-ai"
tags: [n8n, automation, no-code, ai-image-generator, google-drive, e-commerce]
keywords: [n8n workflow, tạo ảnh quảng cáo tự động, e-commerce ad creative, nano banana image generator, ai automation n8n]
---

# 🚀 Tự động tạo ảnh quảng cáo E-commerce không giới hạn với AI

Việc tạo ra hàng loạt hình ảnh quảng cáo (Ad Creatives) bắt mắt cho các chiến dịch E-commerce thường ngốn rất nhiều thời gian, công sức và chi phí thiết kế. Các sếp thường phải loay hoay ghép ảnh sản phẩm với người mẫu (influencer) thủ công trên Photoshop hoặc tốn kém thuê agency. 

Với workflow n8n này, các sếp sẽ sở hữu một hệ thống tự động hóa 100% không cần code. Chỉ với vài cú click trên form, hệ thống sẽ tự động lấy ảnh mẫu influencer từ Google Drive, kết hợp với ảnh sản phẩm và gọi API AI để tạo ra những bức ảnh quảng cáo siêu thực, sẵn sàng chạy chiến dịch!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian thiết kế**: Không còn phải chỉnh sửa thủ công từng ảnh một.
- **Sản xuất hàng loạt (Bulk Generation)**: Tự động lặp qua toàn bộ thư mục ảnh influencer để tạo ra các biến thể quảng cáo đa dạng.
- **Tối ưu chuyển đổi**: Dễ dàng thử nghiệm (A/B testing) nhiều mẫu quảng cáo với các người mẫu khác nhau chỉ trong vài phút.
- **Lưu trữ tự động**: Toàn bộ kết quả đầu ra được đồng bộ thẳng về thư mục Google Drive định sẵn.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance**: Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Google Drive Account**: Tài khoản Google Drive để lưu trữ ảnh mẫu influencer và ảnh kết quả.
- **Nano Banana / AI Image Generator API**: Tài khoản và API Key của dịch vụ tạo ảnh AI (được cấu hình qua HTTP Request node).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy đoạn mã JSON của workflow này và dán trực tiếp vào n8n Editor của mình, hoặc sử dụng tính năng import từ file JSON.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống chạy mượt mà, các sếp cần chú ý cấu hình các node cốt lõi sau:

- **`form_trigger`**: Node này tạo một giao diện form đơn giản để các sếp tải lên ảnh sản phẩm cần quảng cáo. Hãy kiểm tra lại các trường dữ liệu đầu vào.
- **`list_influencer_images` & `download_influencer_image` (Google Drive)**: 
  - Cần kết nối tài khoản Google Drive (`googleDriveOAuth2Api`).
  - Trỏ đường dẫn đến thư mục chứa các bức ảnh reference của influencer mà các sếp đã chuẩn bị sẵn.
- **`iterate_influencer_images` (Split In Batches)**: Node này giúp duyệt qua từng ảnh influencer một cách mượt mà, tránh việc quá tải API.
- **`product_image_to_base64` & `influencer_image_to_base_64` (Extract From File)**: Chuyển đổi dữ liệu nhị phân (binary) của ảnh sản phẩm và ảnh influencer sang định dạng Base64 để gửi qua API AI.
- **`generate_image` (HTTP Request)**: 
  - Kết nối với API tạo ảnh AI (sử dụng thông tin xác thực `httpHeaderAuth`).
  - Đảm bảo Payload truyền đi bao gồm chuỗi Base64 của cả sản phẩm và influencer.
- **`get_image` (Convert To File)**: Chuyển đổi kết quả trả về từ API AI từ dạng text/JSON thành file nhị phân (ảnh).
- **`upload_image` (Google Drive)**: Tự động lưu bức ảnh quảng cáo hoàn thành vào thư mục Google Drive đích đã chỉ định.
- **`set_result` (Set)**: Tổng hợp lại kết quả trả về cho người dùng sau khi hoàn tất quy trình.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và thử tải lên một ảnh mẫu qua form để test chạy thử (Test Run).
- Kiểm tra lại thư mục Google Drive đích xem ảnh đã được tạo và lưu thành công chưa.
- Sau khi mọi thứ chạy ngon lành, hãy gạt nút **Active** để đưa workflow vào hoạt động chính thức.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Telegram/Slack**: Thêm một node Telegram hoặc Slack ở cuối workflow để bắn thông báo ngay lập tức về máy khi bộ ảnh quảng cáo đã được tạo xong.
- **Lưu log vào Google Sheets**: Thêm bước ghi lại lịch sử tạo ảnh (Tên sản phẩm, thời gian, link ảnh kết quả) vào Google Sheets để dễ dàng quản lý.
- **Mở rộng Prompt AI**: Tùy biến thêm các tham số prompt để AI tự động thay đổi bối cảnh, trang phục hoặc phong cách ánh sáng cho phù hợp với từng chiến dịch marketing.

### 📌 Kết luận
Tự động hóa quy trình sáng tạo nội dung chưa bao giờ dễ dàng đến thế. Với workflow n8n này, các sếp có thể giải phóng toàn bộ sức lao động thủ công và tập trung vào việc tối ưu hóa chiến dịch kinh doanh. Hãy cài đặt ngay và trải nghiệm sự kỳ diệu của AI!