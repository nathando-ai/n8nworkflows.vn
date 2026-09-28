---
title: "🚀 Tự động hóa kiểm tra & xác thực hóa đơn với AI, Gmail, Drive & Google Sheets"
description: "Xây dựng hệ thống xử lý hóa đơn tự động 100%: Quét email qua Gmail, lưu trữ Google Drive, trích xuất OCR bằng AI (OpenRouter) và kiểm tra dữ liệu với Google Sheets."
slug: "tu-dong-hoa-kiem-tra-xac-thuc-hoa-don-ai-gmail-drive-sheets"
tags: [n8n, automation, ai, google-sheets, gmail, ocr, finance]
keywords: [n8n workflow, tự động hóa hóa đơn, OCR AI, quản lý hóa đơn Google Sheets, tự động hóa tài chính]
---

# 🚀 Tự động hóa quy trình kiểm tra và xác thực hóa đơn chuyên nghiệp

Các sếp có đang đau đầu mỗi cuối tháng khi phải đối mặt với hàng đống hóa đơn điện tử, file PDF gửi qua email? Việc nhập liệu thủ công, kiểm tra xem số tiền, mã số thuế, hay nhà cung cấp có khớp với hệ thống hay không không chỉ ngốn rất nhiều thời gian mà còn dễ xảy ra sai sót chết người. 

Đừng lo, bài toán này sẽ được giải quyết triệt để với workflow n8n **Invoice Verification and Validation with Gmail, Drive, Sheets and OCR AI** do tác giả Dhrumil Patel sáng tạo. Hệ thống này sẽ thay đội ngũ kế toán làm toàn bộ các bước từ nhận email, trích xuất dữ liệu thông minh bằng AI, lưu trữ khoa học trên Google Drive đến đối chiếu và ghi nhận tự động vào Google Sheets.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Tự động bắt email chứa hóa đơn từ Gmail hoặc quét theo lịch trình định sẵn.
- **Trích xuất thông minh bằng AI:** Sử dụng OpenRouter kết hợp AI Agent (`Text Extractor`) để bóc tách chính xác mọi trường dữ liệu từ file hóa đơn dù là PDF hay hình ảnh.
- **Lưu trữ chuẩn chỉnh:** Tự động tạo cây thư mục trên Google Drive theo Tháng/Ngày để lưu trữ file hóa đơn cực kỳ khoa học.
- **Đối chiếu và xác thực:** Tự động nạp dữ liệu vào Google Sheets, so khớp với danh mục gốc (`Fetch Master Data`) và cập nhật trạng thái xử lý rõ ràng.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Khuyên dùng bản Self-hosted trên VPS).
- **Tài khoản Google:** 
  - Gmail API Credentials (để đọc và gửi email).
  - Google Drive API Credentials (để tạo thư mục và upload hóa đơn).
  - Google Sheets API Credentials (để lưu trữ và đối chiếu dữ liệu).
- **OpenRouter API Key:** Để sử dụng các mô hình ngôn ngữ lớn (LLM) trích xuất OCR thông minh.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow từ nguồn cấp hoặc copy toàn bộ mã JSON.
- Trong giao diện n8n Editor, chọn **Add workflow** -> Nhấp vào biểu tượng ba chấm ở góc trên bên phải -> Chọn **Import from File** hoặc **Paste Workflow**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống chạy mượt mà, các sếp cần cấu hình chuẩn xác các node quan trọng sau:

- **Gmail Trigger / Read Message:** Kết nối tài khoản Gmail của doanh nghiệp. Đặt bộ lọc (filter) để chỉ bắt những email có đính kèm hóa đơn hoặc tiêu đề phù hợp.
- **OpenRouter Chat Model & Text Extractor (Agent):** Thêm OpenRouter API Key của các sếp. Node Agent này đóng vai trò "bộ não" OCR, hãy kiểm tra lại System Prompt để chắc chắn AI trả về đúng các định dạng JSON cần thiết (tên nhà cung cấp, mã số thuế, tổng tiền, tiền thuế...).
- **Google Drive Nodes (`Create Month Folder`, `Upload Invoices`, v.v.):** Kết nối tài khoản Google Drive và trỏ tới thư mục gốc (Parent Folder ID) nơi các sếp muốn lưu trữ toàn bộ hóa đơn. Workflow sẽ tự động tạo thư mục con theo Tháng và Ngày.
- **Google Sheets Nodes (`Fetch Master Data`, `Send Invoice Data`, `Update Results`):** 
  - Chuẩn bị sẵn một Google Sheet với các cấu trúc cột tương ứng (Master Data, Danh sách hóa đơn đến, Báo cáo tổng hợp).
  - Map lại ID của Google Sheet và tên Sheet (Sheet Name) trong từng node tương ứng.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** với một email test thực tế để kiểm tra luồng chạy từ Gmail -> Drive -> AI -> Google Sheets.
- Nếu dữ liệu đổ về bảng tính chính xác, hãy gạt công tắc sang **Active** để hệ thống tự động vận hành 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp kênh thông báo:** Nối thêm node Telegram hoặc Slack ở cuối workflow để bắn thông báo ngay lập tức về nhóm kế toán mỗi khi có hóa đơn mới được xác thực thành công hoặc phát hiện lỗi.
- **Xử lý ngoại lệ (Error Handling):** Thêm Error Trigger để nếu AI không đọc được hóa đơn hoặc file lỗi, hệ thống sẽ tự động gửi email phản hồi lại người gửi hoặc gắn nhãn (label) "Cần xem xét lại" trên Gmail.
- **Báo cáo định kỳ:** Kết hợp node `Schedule Trigger` để tổng hợp số liệu chi phí hàng tuần/tháng rồi gửi báo cáo tự động vào email của Ban Giám đốc.

### 📌 Kết luận
Với workflow n8n này, các sếp đã sở hữu ngay một trợ lý tài chính AI làm việc không mệt mỏi, giúp tiết kiệm hàng chục giờ nhập liệu thủ công mỗi tháng và loại bỏ hoàn toàn sai sót. Đưa ngay vào hệ thống và tối ưu hóa quy trình kế toán của doanh nghiệp ngay hôm nay thôi!