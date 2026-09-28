---
title: "🚀 Tự động hóa quy trình quản lý báo giá nhà cung cấp với Gmail, Google Sheets, GPT-4o-mini và WhatsApp"
description: "Loại bỏ 90% công việc thủ công trong mua hàng (procurement) bằng cách tự động gửi yêu cầu báo giá, theo dõi phản hồi, trích xuất giá qua AI và nhắc nhở nhà cung cấp."
slug: "quan-ly-bao-gia-nha-cung-cap-tu-dong-n8n"
tags: [n8n, automation, no-code, gmail, google-sheets, openai, twilio]
keywords: [n8n workflow, tự động hóa mua hàng, trích xuất hóa đơn AI, quản lý báo giá, whatsapp automation]
---

# 🚀 Tự động hóa quy trình quản lý báo giá nhà cung cấp với Gmail, Google Sheets, GPT-4o-mini và WhatsApp

Các sếp làm trong lĩnh vực mua hàng (procurement) chắc hẳn luôn đau đầu với việc gửi yêu cầu báo giá thủ công, mỏi mắt check email xem nhà cung cấp nào đã phản hồi, tốn hàng giờ copy dữ liệu từ PDF báo giá sang Excel và liên tục phải gọi điện/nhắn tin giục giã nhà cung cấp. 

Workflow n8n mạnh mẽ này sẽ giúp các sếp giải quyết triệt để 100% công việc thủ công đó, biến quy trình mua hàng trở nên mượt mà, tự động hoàn toàn mà không cần viết code phức tạp!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Tự động gửi email yêu cầu báo giá, check phản hồi mỗi giờ và đồng bộ dữ liệu vào Google Sheets.
- **Trích xuất thông tin thông minh:** Sử dụng OpenAI (GPT-4o-mini) kết hợp `Information Extractor` để tự động bóc tách tên sản phẩm, giá cả, số lượng từ file PDF báo giá/hóa đơn của nhà cung cấp.
- **Theo dõi & Nhắc nhở tự động:** Tự động gửi email hoặc tin nhắn WhatsApp nhắc nhở các nhà cung cấp chưa gửi báo giá đúng hạn.
- **Hoạt động liên tục 24/7:** Chạy ngầm ổn định, không bỏ lỡ bất kỳ phản hồi nào từ đối tác.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản sau:
- **Tài khoản Gmail / Google Workspace:** Để gửi email yêu cầu báo giá và quét hộp thư đến tìm phản hồi.
- **Google Sheets:** Lưu trữ danh sách nhà cung cấp và bảng so sánh giá.
- **OpenAI API Key:** Dùng cho model AI trích xuất dữ liệu báo giá từ file PDF đính kèm.
- **Twilio Account:** Cung cấp SID + Auth Token để gửi tin nhắn WhatsApp nhắc nhở tự động.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này và import trực tiếp vào n8n Editor của các sếp (hoặc copy toàn bộ JSON và dán trực tiếp vào màn hình làm việc của n8n).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này được chia thành 4 module độc lập phối hợp nhịp nhàng với nhau:

* **Chuẩn bị Google Sheets:**
  - Tạo sheet `Supplier_list` với các cột: `supplier_name`, `supplier_email`, `category`, `request_date`, `status`, `quote_received`, `phone_number`, `last_follow_up`, `follow_up_count`.
  - Tạo sheet `Price Comparison` với các cột: `supplier_name`, `supplier_email`, `product_name`, `price`, `currency`, `quantity`, `extracted_date`, `source_file`.
  - Cập nhật lại toàn bộ **Google Sheet IDs** trong các node: `Save to Price Sheet`, `Log to suppliers sheet`, `Update supplier sheet`, `Get quotes to process`, `Update supplier sheet with phone number`, `Update follow up count in supplier sheet`, `Get all quotes`.

* **Cấu hình Credentials:**
  - **Gmail OAuth2:** Kết nối tài khoản Gmail cho các node: `Reach out to suppliers`, `Search for quote replies`, `Get email details`, `Get supplier email`, `Download all attachments`, `Send follow-up mail`.
  - **Google Sheets OAuth2:** Kết nối tài khoản Google cho các node Google Sheets.
  - **OpenAI API:** Kết nối API Key cho node `Extract key information from invoice` (sử dụng GPT-4o-mini thông qua `lmChatOpenAi`).
  - **Twilio API:** Cấu hình thông tin Twilio cho node `Send WhatsApp follow-up message`.

* **Cấu hình Twilio WhatsApp Sandbox (Dành cho Module 4):**
  1. Vào Twilio Console → Messaging → Try it out → WhatsApp.
  2. Gửi mã tham gia từ điện thoại của các sếp (ví dụ: `join happy-elephant`).
  3. Sao chép số sandbox (ví dụ: `+1 415 523 8886`) và cập nhật vào trường "From" của node `Send WhatsApp follow-up message`.

* **Tùy chỉnh dữ liệu Nhà cung cấp:**
  - Node `Hardcode suppliers details` chứa mã JavaScript định nghĩa sẵn danh sách nhà cung cấp. Các sếp có thể thay thế bằng node đọc dữ liệu từ Google Sheets hoặc Database của doanh nghiệp.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (**Test run**) thủ công qua node `Execute workflow` để kiểm tra luồng dữ liệu từ việc gửi email đến lưu Google Sheets.
- Sau khi mọi thứ hoạt động trơn tru, bật công tắc **Active** để các trigger định kỳ (`Trigger workflow every hour`, `Trigger workflow daily`) tự động vận hành hệ thống.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp kênh thông báo nội bộ:** Thêm node Telegram hoặc Slack ở cuối luồng nhận báo giá để đội ngũ Sales/Purchasing nhận được thông báo ngay khi nhà cung cấp gửi báo giá mới.
- **Xử lý ngoại lệ (Error Handling):** Thêm Error Trigger để ghi log hoặc gửi cảnh báo về Telegram nếu OpenAI gặp lỗi khi đọc các file PDF định dạng khó.
- **Mở rộng nguồn dữ liệu:** Thay vì hardcode thông tin nhà cung cấp, hãy kết nối node Google Sheets để quản lý danh sách nhà cung cấp trực quan hơn.

### 📌 Kết luận
Với workflow tự động hóa này, quy trình thu thập và quản lý báo giá từ nhà cung cấp sẽ được tối ưu toàn diện, tiết kiệm thời gian và giảm thiểu tối đa sai sót thủ công. Hãy triển khai ngay hôm nay để nâng tầm chuyên nghiệp cho bộ phận mua hàng của doanh nghiệp!