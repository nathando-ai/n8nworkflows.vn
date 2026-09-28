---
title: "🚀 Tự động giám sát đánh giá App Store iOS và gửi Email thông báo với n8n"
description: "Hướng dẫn tự động hóa quy trình theo dõi đánh giá ứng dụng trên iOS App Store, lọc đánh giá mới nhất và gửi email thông báo tức thì bằng n8n."
slug: "tu-dong-giam-sat-danh-gia-app-store-ios-va-gui-email"
tags: [n8n, automation, no-code, app-store, monitoring, email, productivity]
keywords: [n8n workflow, tự động hóa app store, giám sát đánh giá ios, n8n gmail, tinoshost vps]
---

# 🚀 Tự động giám sát đánh giá App Store iOS và gửi Email thông báo

Bạn là nhà phát triển ứng dụng hoặc Product Manager và luôn đau đầu vì phải thủ công kiểm tra App Store mỗi ngày để xem người dùng khen hay chê? Việc bỏ lỡ các đánh giá tiêu cực hoặc phản hồi chậm trễ có thể làm giảm uy tín ứng dụng và giữ chân người dùng kém.

Giải pháp là đây! Workflow n8n này sẽ giúp các sếp tự động hóa 100% quy trình: Định kỳ quét App Store, lọc ra các đánh giá mới nhất và gửi ngay email thông báo chi tiết đến hộp thư của bạn. Không cần code phức tạp, cài đặt một lần chạy mãi mãi!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian:** Không cần mất công check App Store thủ công hằng ngày.
- **Phản ứng nhanh chóng:** Nhận email thông báo ngay khi có đánh giá mới từ người dùng.
- **Không bỏ sót:** Tự động so sánh thời gian để chỉ lấy đánh giá mới nhất, tránh tình trạng spam thông báo trùng lặp.
- **Vận hành 24/7:** Chạy ngầm liên tục trên hệ thống tự động hóa của bạn.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một hệ thống n8n (Self-hosted hoặc n8n Cloud).
- App Store ID của ứng dụng cần theo dõi (lấy từ URL trên App Store).
- Tài khoản Gmail để cấu hình node gửi email (hoặc tài khoản Google Cloud OAuth2 Credentials).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tạo một workflow mới trong n8n, sau đó copy toàn bộ mã nguồn JSON của workflow (hoặc import file JSON) vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình chính xác các node quan trọng sau:

- **Schedule Trigger**: Mặc định workflow được thiết lập chạy mỗi 6 giờ một lần để kiểm tra đánh giá mới. Các sếp có thể tùy chỉnh lại tần suất này trong cài đặt của node tùy theo nhu cầu thực tế.
- **App Config (Node Set)**: Đây là nơi quan trọng nhất. Các sếp cần cấu hình các thông số:
  - App Store ID của ứng dụng.
  - Quốc gia (ví dụ: `us`, `gb`, `vn`...).
  - Ngôn ngữ (ví dụ: `en`, `vi`...).
- **Fetch Reviews (Node HTTP Request)**: Node này gọi trực tiếp vào iTunes API chính thức của Apple để lấy danh sách các đánh giá được sắp xếp theo thời gian mới nhất.
- **Extract Reviews & Filter latest Review (Node Code)**: Xử lý dữ liệu trả về từ Apple, trích xuất thông tin chi tiết và so sánh với mốc thời gian kiểm tra trước đó để chỉ lọc ra các **đánh giá hoàn toàn mới**.
- **Any new reviews? (Node IF)**: Kiểm tra xem có đánh giá mới hay không. Nếu có, chuyển sang nhánh gửi email; nếu không, đi qua nhánh **False Case**.
- **Send notification (Node Gmail)**: Kết nối tài khoản Gmail của các sếp qua OAuth2 để tự động soạn và gửi email nội dung đánh giá mới (gồm tiêu đề, nội dung review, số sao, tên người dùng...).

#### 3. Kích hoạt ⚡️
- Nhấn nút **Test Workflow** để chạy thử nghiệm xem các node có kết nối và lấy dữ liệu thành công hay không.
- Sau khi test thành công, bật công tắc **Active** ở góc trên cùng bên phải để workflow chính thức tự động vận hành.

### ✍️ Mẹo & gợi ý nâng cao
- **Đa kênh thông báo:** Ngoài Gmail, các sếp có thể bổ sung thêm node Telegram hoặc Slack để bắn tin nhắn thông báo vào nhóm chat của team dev ngay lập tức.
- **Lưu trữ dữ liệu:** Kết nối thêm node Google Sheets hoặc Airtable để lưu lại lịch sử tất cả các đánh giá phục vụ việc phân tích xu hướng sản phẩm về lâu dài.
- **Phân loại cảm xúc (AI):** Tích hợp thêm một node AI (OpenAI/Anthropic) để phân tích xem đánh giá đó là tích cực, trung tính hay tiêu cực trước khi gửi email.

### 📌 Kết luận
Việc theo dõi sức khỏe ứng dụng và phản hồi của khách hàng chưa bao giờ dễ dàng đến thế. Hãy triển khai ngay workflow này để nâng cao chất lượng dịch vụ và chăm sóc khách hàng tốt hơn mỗi ngày!