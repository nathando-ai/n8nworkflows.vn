---
title: "🚀 Tự động trích xuất Đơn hàng (Purchase Orders) từ Gmail bằng Gemini AI và lưu vào Google Sheets"
description: "Hướng dẫn xây dựng workflow n8n tự động đọc email, sử dụng Gemini AI phân tích đơn hàng và lưu trữ thông tin vào Google Sheets không cần code."
slug: "trich-xuat-don-hang-gmail-gemini-ai-google-sheets"
tags: [n8n, automation, ai-agent, gemini, google-sheets, gmail]
keywords: [n8n workflow, tự động hóa đơn hàng, trích xuất email ai, gemini ai n8n, google sheets automation]
---

# 🚀 Tự động trích xuất Đơn hàng (Purchase Orders) từ Gmail bằng Gemini AI và lưu vào Google Sheets

Các sếp có đang cảm thấy mệt mỏi mỗi khi phải túc trực kiểm tra email, thủ công copy từng thông tin từ các đơn đặt hàng (Purchase Orders) của khách hàng hoặc đối tác để nhập vào Google Sheets? Việc này không chỉ tốn hàng giờ đồng hồ mỗi ngày mà còn dễ dẫn đến sai sót số liệu, nhầm lẫn mã hàng hoặc bỏ lỡ đơn hàng quan trọng.

Giải pháp đây rồi! Workflow n8n này sẽ tự động hóa 100% quy trình từ khâu quét email mới, lọc đúng email chứa đơn hàng, dùng **Gemini AI** thông minh để đọc, tóm tắt và bóc tách dữ liệu chuẩn xác, sau đó tự động lưu thẳng vào Google Sheets mà không cần một dòng code nào.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- ⏱️ **Tiết kiệm 95% thời gian:** Không cần copy-paste thủ công, hệ thống chạy ngầm tự động mỗi phút.
- 🤖 **AI thông minh:** Gemini AI tự động nhận diện và trích xuất chính xác các trường dữ liệu phức tạp từ nội dung email hoặc tệp đính kèm.
- 📊 **Dữ liệu đồng bộ tức thì:** Đơn hàng được cập nhật trực tiếp vào Google Sheets ngay khi email vừa tới, sẵn sàng cho bộ phận kho hoặc kế toán xử lý.
- 🔄 **Hoạt động 24/7:** Vận hành không nghỉ ngơi, đảm bảo không bỏ sót bất kỳ đơn hàng nào từ đối tác.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Tài khoản Gmail:** Có quyền truy cập để đọc email.
- **Google Gemini API Key:** Để kích hoạt mô hình AI đọc và phân tích văn bản.
- **Google Sheets:** Một trang tính sẵn sàng với các cột tiêu đề (headers) dành riêng cho đơn hàng (Purchase Order).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tạo một workflow trống trên n8n, sau đó copy toàn bộ JSON của workflow hoặc import file JSON mẫu từ nguồn cung cấp vào không gian làm việc của n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống vận hành trơn tru, các sếp cần cấu hình chính xác các node quan trọng sau đây:

- **Cron Node:** Mặc định workflow được thiết lập chạy định kỳ mỗi phút (`Get many messages`). Các sếp có thể điều chỉnh lại tần suất quét email tùy theo nhu cầu thực tế của doanh nghiệp.
- **Get many messages (Gmail Node):** Kết nối tài khoản Gmail của các sếp và cấu hình chế độ lấy các email chưa đọc (`getAll`).
- **Filter emails Node:** Thiết lập quy tắc lọc thông minh dựa trên tiêu đề email (`Subject`) hoặc nội dung để hệ thống chỉ nhận các email thực sự là đơn hàng (Ví dụ: Tiêu đề chứa chữ "Purchase Order" hoặc "Đơn đặt hàng").
- **AI Agent & Google Gemini Chat Model:** 
  - Kết nối Credentials cho Google Gemini.
  - Cấu hình Prompt trong AI Agent để hướng dẫn AI chính xác cách đọc, tóm tắt và trích xuất các thông tin quan trọng như: Tên khách hàng, mã đơn hàng, danh sách sản phẩm, số lượng, tổng tiền...
- **Get row(s) in sheet in Google Sheets / Append row in sheet:** 
  - Kết nối tài khoản Google OAuth2.
  - Chọn đúng file Spreadsheet và Sheet Name chứa dữ liệu đơn hàng của các sếp.
  - Map các trường dữ liệu mà Gemini AI vừa trích xuất vào đúng các cột tương ứng trên Google Sheets thông qua node `Reformatted to upload in Google sheet`.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và gửi một email mẫu chứa đơn hàng đến Gmail để kiểm tra xem dữ liệu có chảy qua các node mượt mà hay không.
- Sau khi test thành công, bật nút **Active** ở góc trên bên phải để workflow chính thức tự động chạy ngầm 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- 🔔 **Tích hợp thông báo:** Nối thêm node **Slack** hoặc **Telegram** sau bước ghi dữ liệu vào Google Sheets để bắn thông báo tức thì về group chat nội bộ mỗi khi có đơn hàng mới.
- 🏷️ **Đánh dấu email:** Thêm hành động cập nhật nhãn (Label) hoặc đánh dấu đã đọc (`Mark as Read`) trong Gmail sau khi xử lý xong để tránh việc workflow xử lý trùng lặp một email nhiều lần.
- 🛡️ **Xử lý lỗi (Error Handling):** Thêm Error Trigger để nhận cảnh báo qua email cá nhân hoặc Telegram nếu Gemini AI gặp lỗi phản hồi hoặc Google Sheets bị quá tải kết nối.

### 📌 Kết luận
Việc tự động hóa trích xuất đơn hàng từ Gmail sang Google Sheets bằng Gemini AI là bước tiến lớn giúp tối ưu hóa vận hành cho các doanh nghiệp bán lẻ, thương mại điện tử và dịch vụ. Hãy áp dụng ngay hôm nay để giải phóng thời gian cho đội ngũ nhân sự và tập trung vào việc tăng trưởng doanh số!