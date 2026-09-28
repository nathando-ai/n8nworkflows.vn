---
title: "🚀 Gửi Email Gợi Ý Sản Phẩm Cá Nhân Hóa Sau Mỗi Đơn Hàng Shopify"
description: "Tự động gửi email gợi ý sản phẩm phù hợp với khách hàng ngay sau khi họ mua hàng trên Shopify. Tăng doanh thu và cải thiện trải nghiệm khách hàng với workflow n8n này."
slug: "gui-email-goi-y-san-pham-ca-nhan-hoa-sau-don-hang-shopify"
tags: [n8n, automation, no-code, shopify, email-marketing]
keywords: [n8n workflow, tự động hóa, shopify, email gợi ý sản phẩm, tăng doanh thu]
---

# 🚀 Gửi Email Gợi Ý Sản Phẩm Cá Nhân Hóa Sau Mỗi Đơn Hàng Shopify

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

Khi các sếp quản lý cửa hàng Shopify, việc phải theo dõi từng đơn hàng và gửi email gợi ý sản phẩm phù hợp với từng khách hàng là một công việc tốn thời gian và dễ gây lỗi. Hơn nữa, nếu không có hệ thống tự động, các sếp có thể bỏ lỡ cơ hội bán hàng khi khách hàng chưa sẵn sàng mua ngay lập tức.

Với workflow này, các sếp có thể tự động gửi email gợi ý sản phẩm cá nhân hóa ngay sau khi khách hàng hoàn tất đơn hàng. Workflow này sử dụng dữ liệu từ Shopify để phân tích hành vi mua hàng của khách hàng và đề xuất các sản phẩm phù hợp nhất.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Tự động gửi email gợi ý sản phẩm mà không cần can thiệp thủ công.
- Tăng doanh thu: Đề xuất sản phẩm phù hợp với từng khách hàng, tăng cơ hội bán hàng.
- Cải thiện trải nghiệm khách hàng: Gửi email cá nhân hóa ngay sau khi khách hàng mua hàng.
- Hoạt động liên tục: Workflow chạy tự động 24/7, không bị gián đoạn.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Shopify với quyền truy cập API.
- Tài khoản email (Gmail, Outlook, hoặc dịch vụ email khác) để gửi email.
- API Key và thông tin xác thực cho Shopify và email.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Để import workflow này vào n8n, các sếp có thể làm theo các bước sau:

1. Truy cập vào n8n Editor.
2. Nhấp vào nút "Import from URL" và dán liên kết sau vào ô nhập liệu: [https://n8n.io/workflows/6579](https://n8n.io/workflows/6579).
3. Nhấp vào nút "Import" để hoàn tất quá trình import.

Hoặc, các sếp cũng có thể tải xuống file JSON của workflow từ liên kết trên và import trực tiếp vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

- **Order Created Trigger**: Node này kích hoạt workflow khi có đơn hàng mới được tạo trên Shopify. Các sếp cần cấu hình thông tin xác thực Shopify và chọn các trường dữ liệu cần thiết từ đơn hàng.

- **Wait 10 Minutes**: Node này tạm dừng workflow trong 10 phút trước khi tiếp tục xử lý. Điều này giúp đảm bảo rằng đơn hàng đã được xử lý hoàn toàn trên Shopify.

- **Generate Recommendation IDs**: Node này sử dụng mã JavaScript để tạo danh sách các ID sản phẩm gợi ý dựa trên dữ liệu từ đơn hàng. Các sếp có thể chỉnh sửa mã này để phù hợp với chiến lược gợi ý sản phẩm của mình.

- **If Recommendations Exist**: Node này kiểm tra xem có sản phẩm gợi ý nào được tạo ra không. Nếu không có sản phẩm gợi ý, workflow sẽ kết thúc.

- **Split Recommended Products**: Node này chia danh sách sản phẩm gợi ý thành các lô nhỏ để xử lý từng lô một. Các sếp có thể điều chỉnh kích thước lô để phù hợp với nhu cầu của mình.

- **Get Product Details**: Node này lấy thông tin chi tiết của từng sản phẩm gợi ý từ Shopify. Các sếp cần cấu hình thông tin xác thực Shopify và chọn các trường dữ liệu cần thiết từ sản phẩm.

- **Merge Product Details (v3.2)**: Node này hợp nhất thông tin chi tiết của các sản phẩm gợi ý thành một danh sách duy nhất. Các sếp có thể điều chỉnh cách hợp nhất để phù hợp với nhu cầu của mình.

- **Format Recommendations HTML**: Node này sử dụng mã JavaScript để định dạng danh sách sản phẩm gợi ý thành HTML để gửi trong email. Các sếp có thể chỉnh sửa mã này để phù hợp với mẫu email của mình.

- **Send Upsell Email**: Node này gửi email gợi ý sản phẩm đến khách hàng. Các sếp cần cấu hình thông tin xác thực email và chọn các trường dữ liệu cần thiết từ đơn hàng và sản phẩm gợi ý.

#### 3. Kích hoạt ⚡️
Sau khi cấu hình các node quan trọng, các sếp cần thực hiện các bước sau để kích hoạt workflow:

1. Nhấp vào nút "Execute Workflow" để kiểm tra workflow với dữ liệu mẫu.
2. Kiểm tra kết quả và đảm bảo rằng workflow hoạt động như mong đợi.
3. Nhấp vào nút "Activate" để kích hoạt workflow và bắt đầu chạy tự động.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack hoặc Telegram: Các sếp có thể thêm các node để gửi thông báo đến Slack hoặc Telegram khi có đơn hàng mới hoặc khi gửi email gợi ý sản phẩm.
- Lưu log: Các sếp có thể thêm các node để lưu log của workflow để theo dõi hoạt động và giải quyết vấn đề.
- Gửi báo cáo định kỳ: Các sếp có thể thêm các node để gửi báo cáo định kỳ về hoạt động của workflow, bao gồm số lượng đơn hàng, số lượng email gợi ý sản phẩm đã gửi, và số lượng sản phẩm đã bán.

### 📌 Kết luận
Workflow này giúp các sếp tự động gửi email gợi ý sản phẩm cá nhân hóa ngay sau khi khách hàng mua hàng trên Shopify. Với workflow này, các sếp có thể tiết kiệm thời gian, tăng doanh thu, và cải thiện trải nghiệm khách hàng. Các sếp nên thử nghiệm workflow này và điều chỉnh để phù hợp với nhu cầu của mình.