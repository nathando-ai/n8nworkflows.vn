---
title: "🚀 Tự động tạo và gửi báo giá phụ tùng với Gmail, Google Sheets và Gemini AI"
description: "Hướng dẫn xây dựng workflow n8n tự động đọc email yêu cầu báo giá phụ tùng, tra cứu dữ liệu từ Google Sheets và sử dụng Gemini AI để phản hồi chuyên nghiệp."
slug: "tu-dong-tao-va-gui-bao-gia-phu-tung-voi-gmail-google-sheets-va-gemini-ai"
tags: [n8n, automation, gmail, google-sheets, google-gemini, ai-agent]
keywords: [n8n workflow, tự động hóa báo giá, gmail automation, google sheets, gemini ai agent]
---

# 🚀 Tự động tạo và gửi báo giá phụ tùng với Gmail, Google Sheets và Gemini AI

Việc xử lý thủ công các yêu cầu báo giá phụ tùng từ khách hàng thường tốn rất nhiều thời gian: nhân viên phải đọc email, tra cứu mã dự án, kiểm tra danh mục vật tư (BoM), tính toán đơn giá từ bảng giá và soạn thảo email phản hồi. Quy trình này dễ dẫn đến chậm trễ và sai sót khi khối lượng công việc tăng cao.

Workflow n8n này sẽ giải quyết triệt để vấn đề trên bằng cách tự động hóa 100% từ khâu nhận email yêu cầu, tra cứu dữ liệu khách hàng, định mức vật tư, tính toán giá tiền cho đến việc soạn thảo và gửi email báo giá chuyên nghiệp bằng AI.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tốc độ phản hồi chớp nhoáng:** Khách hàng nhận được báo giá chi tiết chỉ vài phút sau khi gửi email yêu cầu.
- **Đa ngôn ngữ thông minh:** AI tự động phát hiện và phản hồi bằng đúng ngôn ngữ của người gửi (Tiếng Anh, Đức, Thổ Nhĩ Kỳ, v.v.).
- **Độ chính xác tuyệt đối:** Tự động liên kết dữ liệu CRM, BoM và Bảng giá qua Google Sheets, kết hợp Calculator Tool để tính toán không sai sót.
- **Quản lý hộp thư gọn gàng:** Tự động đánh dấu email đã xử lý, tránh tình trạng bỏ sót hoặc phản hồi trùng lặp.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản n8n (Cloud hoặc Self-hosted).
- Tài khoản Google Workspace / Gmail (để đọc và gửi email).
- Google Sheets chứa 3 bảng dữ liệu: Khách hàng (CRM), Định mức vật tư (BoM), và Bảng giá.
- Google Gemini API Key (từ Google AI Studio).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tạo một workflow mới trong n8n, sau đó copy toàn bộ mã JSON của workflow (hoặc import file JSON) vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow hoạt động mượt mà, các sếp cần cấu hình các thành phần sau:

- **Gmail - Get Latest Email & Gmail - Send Reply & Gmail - Mark as Read:** Kết nối tài khoản Gmail qua OAuth2. Node gửi email sẽ tự động đóng vai trò trả lời (reply) đúng thread email của khách hàng.
- **Check Spare Parts Keywords (Node IF):** Kiểm tra từ khóa yêu cầu phụ tùng trong nội dung email (Hỗ trợ từ khóa tiếng Anh: *"spare parts"*, tiếng Đức: *"Ersatzteile"*, tiếng Thổ Nhĩ Kỳ: *"yedek parça"*...). Các sếp có thể tùy chỉnh thêm từ khóa phù hợp với ngành hàng của mình.
- **AI Agent - Quote Generator & Google Gemini Chat Model:** Cấu hình credentials cho Google Gemini bằng API Key lấy từ Google AI Studio. AI Agent sẽ đóng vai trò tổng hợp thông tin và viết email HTML chuyên nghiệp.
- **Google Sheets Tools (CRM - Customer Data, BoM - Bill of Materials, Price - Pricing Data):** 
  - Kết nối Google Sheets Credentials.
  - Thay thế các `Sheet ID` mẫu bằng ID thực tế của các file Google Sheets của doanh nghiệp.
  - Cấu trúc các bảng dữ liệu yêu cầu:
    - **Sheet CRM:** Cần có các cột `Email`, `ProjectCode`, `CustomerName`.
    - **Sheet BoM:** Cần có các cột `ProjectCode`, `PartCode`, `PartDescription`, `Quantity`.
    - **Sheet Price:** Cần có các cột `PartCode`, `UnitPriceEUR`, `PartDescription`.

#### 3. Kích hoạt ⚡️
- Nhấp vào **Execute Workflow** để chạy thử với dữ liệu email mẫu hoặc email thực tế gần nhất.
- Kiểm tra kết quả trả về ở Gmail và lịch sử chạy trên n8n.
- Sau khi test thành công, bật công tắc **Active** để hệ thống tự động chạy ngầm 24/7 theo lịch trình của node **Schedule Trigger**.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp kênh thông báo:** Thêm node Slack hoặc Telegram để bắn thông báo về nhóm Sales mỗi khi có một báo giá mới được tự động gửi đi.
- **Lưu lịch sử báo giá:** Thêm một bước ghi lại nội dung báo giá và thời gian gửi vào một Google Sheet quản lý lịch sử (Audit Log).
- **Phê duyệt thủ công (Human-in-the-loop):** Thêm node Wait hoặc n8n Form để nhân viên sales duyệt nội dung báo giá trước khi AI chính thức gửi đi cho khách hàng VIP.

### 📌 Kết luận
Workflow tự động hóa báo giá phụ tùng này là một trợ thủ đắc lực giúp tối ưu hóa quy trình bán hàng b2b, tiết kiệm hàng chục giờ làm việc thủ công mỗi tuần. Hãy thiết lập ngay hôm nay để nâng cấp tốc độ phản hồi khách hàng của doanh nghiệp lên một tầm cao mới!