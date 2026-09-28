---
title: "🚀 Tự động trích xuất văn bản từ ảnh Google Drive bằng OCR.space, tóm tắt AI qua OpenRouter, lưu Google Sheets và gửi Gmail"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa hoàn toàn quy trình nhận diện chữ trong ảnh (OCR), tóm tắt nội dung bằng AI, lưu trữ dữ liệu và gửi email thông báo."
slug: "tu-dong-trich-xuat-van-ban-anh-ocr-ai-tom-tat-google-sheets-gmail"
tags: [n8n, automation, ocr, ai-summary, google-drive, google-sheets, gmail, openrouter]
keywords: [n8n workflow, ocr space, openrouter ai, google drive trigger, tóm tắt ảnh bằng ai, tự động hóa n8n]
---

# 🚀 Tự động trích xuất văn bản từ ảnh Google Drive với OCR & AI OpenRouter

Các sếp có bao giờ cảm thấy mệt mỏi khi phải đọc từng bức ảnh chụp tài liệu, trang sách, hay ghi chú tay rồi gõ lại thủ công để lưu trữ và báo cáo không? Việc này không chỉ tốn hàng giờ đồng hồ mà còn dễ xảy ra sai sót. 

Đừng lo, bài toán này sẽ được giải quyết triệt để với **Workflow n8n tự động hóa toàn diện**: Khi có ảnh mới đẩy lên Google Drive, hệ thống sẽ tự động quét chữ (OCR), nhờ AI (OpenRouter) tóm tắt nội dung cốt lõi, tự động lưu kết quả vào Google Sheets và gửi email thông báo qua Gmail cho các sếp ngay lập tức!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Số hóa 100% tài liệu dạng ảnh:** Không cần gõ thủ công, tự động nhận diện chữ từ ảnh chụp sách, tài liệu, biên lai hay bảng biểu.
- **Tóm tắt thông minh bằng AI:** Tận dụng sức mạnh của các mô hình AI qua OpenRouter để chắt lọc những ý chính ngắn gọn, dễ đọc.
- **Lưu trữ khoa học:** Tự động ghi nhận tên file, ngày tháng và nội dung tóm tắt vào Google Sheets để tra cứu bất cứ lúc nào.
- **Thông báo tức thì:** Nhận email báo cáo qua Gmail ngay khi tiến trình xử lý hoàn tất mà không cần mở máy kiểm tra liên tục.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản và thông tin sau:
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Google Drive Credentials:** Tài khoản Google kết nối với n8n để theo dõi thư mục ảnh.
- **OCR.space API Key:** Đăng ký một tài khoản miễn phí tại [ocr.space](https://ocr.space/) để lấy API Key thực hiện trích xuất chữ.
- **OpenRouter API Key:** Tài khoản tại [openrouter.ai](https://openrouter.ai/) để sử dụng các mô hình AI ngôn ngữ lớn.
- **Google Sheets:** Một file Google Sheet chuẩn bị sẵn các cột (Tên file, Ngày tháng, Nội dung tóm tắt, Link tài liệu...).
- **Gmail Credentials:** Kết nối tài khoản Gmail để gửi email thông báo.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể sao chép đoạn mã JSON của workflow này và dán trực tiếp vào n8n Editor của mình, hoặc import file JSON theo tài liệu gốc từ n8n template (Workflow ID: 10541).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 9 nodes chính, các sếp cần chú ý cấu hình kỹ các điểm sau để chạy mượt mà:

- **Google Drive New File Trigger1:** 
  - Chọn tài khoản Google Drive credentials của sếp.
  - Chọn thư mục đích (Folder) trên Drive nơi các sếp sẽ tải ảnh lên để hệ thống tự kích hoạt.
- **Download Image File1:** 
  - Đảm bảo node này nhận đúng file ID truyền từ trigger để tải xuống nội dung ảnh.
- **Extract Text with OCR.space1 (Node HTTP Request):** 
  - Điền `API Key` của OCR.space vào phần header hoặc query parameters theo tài liệu hướng dẫn của OCR.space.
- **Format OCR Result & Check for Empty1 (Node Code):** 
  - Kiểm tra logic code JavaScript có sẵn giúp làm sạch khoảng trắng thừa, ngắt dòng không cần thiết và lọc trường hợp ảnh trống không có chữ.
- **Generate Summary with OpenRouter AI1 (Node Agent & OpenRouter Chat Model1):** 
  - Kết nối `OpenRouter Chat Model1` bằng thông tin **OpenRouter API Key**.
  - Thiết lập System Prompt cho AI để yêu cầu định dạng tóm tắt ngắn gọn, súc tích bằng ngôn ngữ mong muốn (tiếng Việt hoặc tiếng Nhật/Anh tùy ý).
- **Append row in sheet1 (Node Google Sheets):** 
  - Chọn đúng file Google Sheet và Sheet Name mà các sếp muốn lưu dữ liệu.
  - Map các trường dữ liệu: Tên file, Kết quả tóm tắt từ AI, Ngày giờ hiện tại vào đúng các cột tương ứng.
- **Send Completion Notification via Gmail1 (Node Gmail):** 
  - Cấu hình tài khoản Gmail gửi.
  - Điền địa chỉ email nhận thông báo và soạn nội dung email gắn kèm tên file, bản tóm tắt AI và link Google Drive/Docs.
- **Process Completed1 (Node NoOp):** 
  - Điểm kết thúc workflow, không cần chỉnh sửa gì thêm.

#### 3. Kích hoạt ⚡️
- Bấm nút **Execute Workflow** và thử tải một tấm ảnh chứa văn bản lên thư mục Google Drive đã chọn để test chạy thử (Test run).
- Kiểm tra xem dữ liệu đã được đẩy lên Google Sheets và nhận được email từ Gmail chưa.
- Nếu mọi thứ chạy mượt mà, gạt công tắc sang **Active** để hệ thống tự động chạy 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng thông báo:** Thay vì chỉ gửi qua Gmail, các sếp có thể nối thêm node **Telegram** hoặc **Slack** để nhận thông báo nhanh ngay trên điện thoại khi có tài liệu mới được xử lý xong.
- **Lưu lịch sử lỗi:** Thêm các nhánh Error Trigger để gửi cảnh báo về Telegram nếu ảnh quá mờ khiến OCR không đọc được chữ hoặc API OpenRouter gặp sự cố.
- **Phân loại thông minh:** Có thể yêu cầu AI trong prompt phân loại chủ đề tài liệu (Ví dụ: Hóa đơn, Hợp đồng, Ghi chú học tập...) để tự động sắp xếp vào các sheet hoặc thư mục Google Drive khác nhau.

### 📌 Kết luận
Workflow này là một cỗ máy tự động hóa cực kỳ đắc lực cho những ai thường xuyên phải xử lý tài liệu giấy, sách báo hoặc hóa đơn dạng hình ảnh. Hãy cài đặt ngay hôm nay để tiết kiệm hàng tá thời gian và tối ưu hóa hiệu suất làm việc cho doanh nghiệp của các sếp!