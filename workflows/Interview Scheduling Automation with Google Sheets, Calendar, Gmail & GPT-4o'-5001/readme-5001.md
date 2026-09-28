---
title: "🚀 Tự động hóa lịch phỏng vấn với Google Sheets, Calendar, Gmail & GPT-4o"
description: "Hướng dẫn cài đặt workflow n8n giúp tự động hóa toàn bộ quy trình lên lịch phỏng vấn, kết hợp AI GPT-4o, Google Sheets, Google Calendar và Gmail."
slug: "tu-dong-hoa-lich-phong-vas-n8n-gpt-4o"
tags: [n8n, automation, hr, ai, gpt-4o, google-calendar, gmail]
keywords: [n8n workflow, tự động hóa tuyển dụng, interview scheduling n8n, gpt-4o n8n, google sheets trigger]
---

# 🚀 Tự động hóa lịch phỏng vấn với Google Sheets, Calendar, Gmail & GPT-4o

Các sếp trong bộ phận Nhân sự (HR) chắc hẳn đã quá quen thuộc với cảnh "đau đầu" mỗi mùa tuyển dụng: hàng trăm hồ sơ đổ về, việc nhắn tin qua lại để chọn giờ phỏng vấn, tạo lịch họp Google Meet thủ công rồi gửi email xác nhận. Chỉ vài ứng viên thôi là đã tốn nguyên một buổi làm việc, chưa kể nguy cơ chồng chéo lịch hẹn.

Giải pháp cho các sếp đây! Workflow n8n siêu cấp này được thiết kế bởi chuyên gia Rahul Joshi sẽ giúp tự động hóa 100% quy trình tuyển dụng từ A-Z. Hệ thống sẽ tự động lắng nghe dữ liệu từ Google Sheets, sử dụng sức mạnh AI của **GPT-4o** để xử lý thông tin, tự động tạo sự kiện trên **Google Calendar** và gửi email mời phỏng vấn chuyên nghiệp qua **Gmail** mà không cần con người nhúng tay vào.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không còn phải copy-paste thông tin ứng viên, kiểm tra lịch trống hay soạn email thủ công.
- **Loại bỏ trùng lịch:** Lịch phỏng vấn được tích hợp trực tiếp với Google Calendar, đảm bảo không bao giờ bị đè lịch.
- **Cá nhân hóa thông minh:** Sử dụng Azure OpenAI (GPT-4o) để phân tích và chuẩn hóa dữ liệu ứng viên một cách mượt mà.
- **Vận hành 24/7:** Ngay khi có dòng dữ liệu mới trong Google Sheets, hệ thống lập tức kích hoạt xử lý ngay lập tức.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động trơn tru, các sếp cần chuẩn bị sẵn các tài nguyên sau:
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Google Account** (để cấu hình Google Sheets Trigger, Google Calendar và Gmail).
- **Azure OpenAI API Key** (với mô hình `gpt-4o` đã được kích hoạt).
- **Google Sheet mẫu** chứa thông tin ứng viên (Tên, Email, Thời gian mong muốn...).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tạo một workflow mới trong giao diện n8n Editor, sau đó copy toàn bộ mã JSON của workflow này và dán trực tiếp vào màn hình làm việc (n8n hỗ trợ phím tắt `Ctrl + V` / `Cmd + V` để paste nhanh nodes).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống không báo lỗi, các sếp cần cấu hình chính xác các credentials và thông số cho từng node sau:

- **Google Sheets Trigger**: 
  - Kết nối tài khoản Google qua OAuth2.
  - Chọn đúng File Google Sheet quản lý ứng viên và chọn đúng Sheet Name/ID nơi dữ liệu mới được thêm vào.
- **Azure OpenAI Chat Model** (`gpt-4o`):
  - Nhập thông tin `Azure OpenAI API Key` và Endpoint của các sếp.
  - Đảm bảo model được cấu hình chính xác là `gpt-4o`.
- **Structured Output Parser & Basic LLM Chain**:
  - Kiểm tra lại các schema đầu ra để đảm bảo AI trả về đúng định dạng JSON mà các node phía sau cần (như thời gian, tên ứng viên, email).
- **Code Node**:
  - Kiểm tra đoạn mã JavaScript xử lý dữ liệu trung gian (nếu cần tinh chỉnh lại định dạng ngày giờ cho phù hợp với Google Calendar).
- **Google Calendar**:
  - Chọn lịch (Calendar) muốn tạo sự kiện phỏng vấn (ví dụ: "Primary" hoặc lịch tuyển dụng riêng).
  - Map các trường dữ liệu thời gian bắt đầu, kết thúc, tiêu đề cuộc họp và thêm email ứng viên làm người tham dự (Attendee).
- **Gmail**:
  - Kết nối tài khoản Gmail gửi đi.
  - Cấu hình nội dung email (lấy dynamic data từ các bước trước) để gửi thư mời họp kèm link Google Meet tự động cho ứng viên.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** và thử nhập một dòng dữ liệu giả lập vào Google Sheets để test xem các node có chạy xanh (thành công) hay không.
- Kiểm tra lại Google Calendar xem lịch đã được tạo chưa và Gmail đã bắn thư đi chưa.
- Nếu mọi thứ mượt mà, hãy gạt công tắc sang **Active** để đưa workflow vào trạng thái chạy tự động hoàn toàn!

### ✍️ Mẹo & gợi ý nâng cao
Để hệ thống xịn sò hơn nữa, các sếp có thể mở rộng workflow này với các ý tưởng sau:
- **Gửi thông báo nội bộ:** Thêm node **Slack** hoặc **Telegram** để bắn tin nhắn vào group của team HR ngay khi có lịch phỏng vấn mới được chốt.
- **Xử lý trạng thái (Status Update):** Sau khi gửi email thành công, thêm một bước cập nhật ngược lại trạng thái "Đã gửi lịch" vào dòng tương ứng trong Google Sheets.
- **Tự động nhắc nhở:** Thêm một luồng phụ kiểm tra lịch hẹn trước 1 tiếng và gửi tin nhắn Zalo/SMS hoặc Email nhắc nhở ứng viên tham gia đúng giờ.

### 📌 Kết luận
Tự động hóa quy trình tuyển dụng không chỉ giúp bộ phận HR giải phóng sức lao động khỏi các tác vụ lặp đi lặp lại mà còn tạo ấn tượng cực kỳ chuyên nghiệp đối với ứng viên ngay từ vòng đầu tiên. Hãy setup ngay workflow này và tận hưởng sự thảnh thơi mà n8n mang lại nhé các sếp!