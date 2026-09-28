---
title: "🚀 Tự động trích xuất dữ liệu Fax và PDF thông minh bằng Google Gemini và Google Sheets"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa quy trình đọc file PDF, trích xuất dữ liệu thông minh bằng AI Gemini và lưu trữ trực tiếp vào Google Sheets."
slug: "tu-dong-trich-xuat-du-lieu-pdf-gemini-google-sheets"
tags: [n8n, automation, no-code, google-gemini, google-sheets, ai]
keywords: [n8n workflow, trích xuất pdf, google gemini api, google sheets automation, xử lý tài liệu ai]
---

# 🚀 Tự động trích xuất dữ liệu Fax và PDF thông minh bằng Google Gemini và Google Sheets

Các sếp có bao giờ cảm thấy mệt mỏi khi phải mở từng file PDF hoặc bản fax nhận được, thủ công đọc thông tin rồi gõ lại vào file Excel hay Google Sheets chưa? Việc này không chỉ ngốn hàng giờ đồng hồ mỗi ngày mà còn dễ xảy ra sai sót, nhầm lẫn con số.

Đừng lo, bài toán đó sẽ được giải quyết triệt để với workflow n8n cực kỳ thông minh này. Sử dụng sức mạnh đa phương thức (Multimodal AI) của **Google Gemini** kết hợp cùng **Google Sheets**, workflow này sẽ tự động hóa 100% quy trình: nhận file tải lên qua form, đọc hiểu nội dung tài liệu, trích xuất thông tin chính xác theo cấu trúc định sẵn và lưu thẳng lên Google Sheets mà không cần một dòng code thủ công nào.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không còn cảnh đọc file và gõ tay thủ công, hệ thống tự động xử lý chỉ trong vài giây.
- **Độ chính xác cao:** Tận dụng khả năng AI của Google Gemini để đọc và hiểu các tài liệu phức tạp, hóa đơn hoặc bản fax mờ.
- **Cấu trúc dữ liệu chuẩn hóa:** Xuất dữ liệu dưới dạng JSON nghiêm ngặt và đồng bộ thẳng vào Google Sheets theo từng cột định sẵn.
- **Hoạt động 24/7:** Giao diện Form trực quan giúp nhân viên hoặc đối tác dễ dàng tải file lên bất cứ lúc nào.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài nguyên sau:
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Google Gemini API Key** (Google Palm/Gemini API credentials) để gọi mô hình AI.
- **Tài khoản Google Drive** (để lưu trữ file PDF/Fax được tải lên).
- **Tài khoản Google Sheets** (để lưu trữ dữ liệu trích xuất).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này và import trực tiếp vào n8n Editor của các sếp, hoặc sử dụng tính năng copy/paste JSON trực tiếp vào màn hình làm việc.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình chính xác các node trọng điểm sau:

- **On form submission (`formTrigger`):** Đây là điểm khởi đầu, tạo một web form thân thiện để người dùng tải file FAX hoặc PDF lên.
- **Upload file & Google Drive (`googleDrive`):** 
  - Chọn tài khoản Google Drive OAuth2 trong mục *Credentials*.
  - Thay đổi **Folder ID** thành ID thư mục cụ thể trên Google Drive nơi các sếp muốn lưu trữ các file fax/PDF này.
- **Call Gemini 2.0 Flash / Basic LLM Chain & Google Gemini Chat Model:** 
  - **ACTION REQUIRED:** Chọn credentials API của Google Palm/Gemini.
  - Tùy chỉnh prompt tại node **Define Prompt** (`set`) hoặc trong LLM Chain để điều chỉnh luật trích xuất hoặc yêu cầu lấy các trường thông tin khác nhau (ví dụ: Tên khách hàng, Mã đơn hàng, Tổng tiền...).
- **Structured Output Parser:** Định nghĩa schema JSON với các keys và giá trị kỳ vọng để đảm bảo AI trả về đúng cấu trúc phục vụ cho bước đẩy vào Google Sheets.
- **Append row in sheet (`googleSheets`):**
  - Cấu hình credentials Google Sheets OAuth2.
  - Cập nhật **Document ID** bằng ID file Google Sheet của các sếp.
  - Đảm bảo tên các cột (Column names) trong node này khớp hoàn toàn với hàng tiêu đề (header row) tại Google Sheets đích.

#### 3. Kích hoạt ⚡️
- Nhấn **Test step** hoặc **Execute Workflow** tải thử một file PDF mẫu lên Form để kiểm tra dòng dữ liệu chạy qua các node AI và đổ về Google Sheets.
- Nếu dữ liệu đã chuẩn xác, gạt công tắc sang **Active** để đưa vào sử dụng thực tế.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Nối thêm node Telegram hoặc Slack ở cuối workflow để bắn tin nhắn thông báo ngay lập tức về nhóm khi có bản fax/PDF mới được xử lý thành công.
- **Quản lý lỗi (Error Handling):** Thêm Error Trigger để ghi log hoặc gửi email cảnh báo nếu file tải lên bị lỗi định dạng hoặc API AI gặp sự cố.
- **Tự động phân loại:** Kết hợp thêm một nhánh AI phân loại nội dung fax trước khi trích xuất để điều hướng dữ liệu đến các Google Sheets khác nhau tùy thuộc vào phòng ban (Kế toán, Kinh doanh, Vận hành...).

### 📌 Kết luận
Tự động hóa quy trình xử lý tài liệu, fax và PDF chưa bao giờ dễ dàng đến thế với sức mạnh của n8n và Google Gemini. Hãy áp dụng ngay workflow này để giải phóng sức lao động cho đội ngũ back-office và tối ưu hóa vận hành doanh nghiệp ngay hôm nay các sếp nhé!