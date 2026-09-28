---
title: "🚀 Tự động trích xuất hóa đơn PDF quét thành Google Sheets bằng AI Sarvam và Gemini"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa quy trình xử lý hóa đơn quét (PDF scan), sử dụng AI Gemini và Sarvam để trích xuất dữ liệu thông minh và lưu thẳng vào Google Sheets."
slug: "trich-xuat-hoa-don-pdf-google-sheets-sarvam-gemini"
tags: [n8n, automation, ai, google-sheets, invoice-processing, gemini]
keywords: [n8n workflow, xử lý hóa đơn tự động, trích xuất hóa đơn pdf, google sheets ai, gemini, sarvam ai]
useStrictParsing: true
---

# 🚀 Tự động trích xuất hóa đơn PDF quét thành Google Sheets bằng AI Sarvam và Gemini

Các sếp có đang đau đầu mỗi khi cuối tháng phải ngồi nhập thủ công hàng trăm tờ hóa đơn, biên lai giấy được scan dưới dạng PDF hình ảnh không? Việc này không chỉ tốn hàng giờ đồng hồ mệt mỏi mà còn cực kỳ dễ xảy ra sai sót số liệu (như lệch tiền thuế, sai mã số thuế, nhầm tên khách hàng). 

Đừng lo, bài viết này sẽ hướng dẫn các sếp cách thiết lập một "trợ lý ảo" tự động hóa 100% bằng n8n. Workflow này sẽ tự động nhận diện hóa đơn PDF quét, nhờ sức mạnh của AI Gemini và Sarvam để bóc tách toàn bộ thông tin chuẩn xác, sau đó tự động điền gọn gàng vào Google Sheets. Các sếp chỉ việc uống cà phê và kiểm tra kết quả!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không còn cảnh gõ phím mỏi tay nhập liệu thủ công từng hóa đơn.
- **Độ chính xác cao:** Ứng dụng AI đa phương thức (Gemini & Sarvam) đọc hiểu cả các định dạng hóa đơn quét mờ, phức tạp.
- **Đồng bộ thời gian thực:** Dữ liệu tự động đẩy thẳng vào Google Sheets ngay sau khi tải lên.
- **Hoạt động 24/7:** Quy trình khép kín từ lúc nhận file qua Form đến khi lưu trữ hoàn tất mà không cần con người nhúng tay.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị sẵn các tài nguyên sau:
- **Hệ thống n8n:** Đã cài đặt sẵn sàng (Self-hosted hoặc n8n Cloud).
- **Google Account:** Để kết nối Google Sheets và tạo sẵn file quản lý hóa đơn.
- **Google Gemini API Key:** Dành cho các node AI xử lý ngôn ngữ và trích xuất thông tin (`@n8n/n8n-nodes-langchain.lmChatGoogleGemini`).
- **Sarvam AI Account/API Key:** Dành cho việc xử lý các tác vụ AI chuyên biệt đi kèm trong quy trình.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow từ nguồn cấp hoặc copy toàn bộ mã JSON.
- Trong giao diện n8n Editor, bấm vào menu góc trên bên phải, chọn **Import from File** hoặc **Import from Clipboard** và dán mã JSON vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Khi import xong, các sếp cần cấu hình lại các node cốt lõi sau để hệ thống chạy mượt mà:

- **Form Trigger (`formTrigger`):** Điểm khởi đầu nơi người dùng (hoặc kế toán) tải file PDF hóa đơn lên. Các sếp có thể tùy chỉnh giao diện form thu thập nếu cần.
- **Extract From File (`extractFromFile`):** Node chịu trách nhiệm đọc và bóc tách dữ liệu thô từ file PDF quét đầu vào.
- **Google Gemini Chat Model (`lmChatGoogleGemini`):** Kết nối tài khoản Google API của các sếp, chọn model Gemini phù hợp (ví dụ: `gemini-1.5-pro` hoặc `gemini-1.5-flash`) để làm bộ não đọc hiểu nội dung hóa đơn.
- **Information Extractor (`informationExtractor`):** Cấu hình schema (cấu trúc dữ liệu cần lấy như: Tên nhà cung cấp, Mã số thuế, Tổng tiền, Ngày hóa đơn...) để AI trả về đúng định dạng yêu cầu.
- **Google Sheets (`googleSheets`):** Chọn tài khoản Google Credentials, trỏ tới file Google Sheets và chọn Sheet Name tương ứng để lưu các trường dữ liệu mà AI vừa trích xuất.

#### 3. Kích hoạt ⚡️
- Bấm **Test workflow** và tải lên một file hóa đơn PDF mẫu để kiểm tra xem dữ liệu có chảy qua các node mượt mà và nhảy vào Google Sheets đúng chỗ không.
- Sau khi test thành công, bật nút **Active** ở góc trên cùng bên phải để đưa workflow vào trạng thái chạy tự động chính thức.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Nối thêm node Telegram hoặc Slack ở cuối workflow để bắn thông báo ngay về máy mỗi khi có hóa đơn mới được xử lý thành công.
- **Lưu trữ file:** Thêm bước tự động lưu bản gốc hóa đơn PDF vào Google Drive hoặc OneDrive theo thư mục phân loại theo tháng/năm.
- **Xử lý lỗi (Error Handling):** Thêm nhánh catch error để nếu hóa đơn quá mờ AI không đọc được, hệ thống sẽ gửi email cảnh báo người quản lý kiểm tra lại thủ công.

### 📌 Kết luận
Việc tự động hóa trích xuất hóa đơn PDF quét với n8n, Gemini và Sarvam là bước tiến tuyệt vời giúp tối ưu hóa vận hành cho phòng kế toán - tài chính. Hãy áp dụng ngay hôm nay để giải phóng sức lao động khỏi các tác vụ nhập liệu nhàm chán!