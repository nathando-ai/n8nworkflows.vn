---
title: "🚀 Tự động tìm kiếm và chấm điểm Lead doanh nghiệp địa phương với n8n, Google Sheets, RapidAPI & OpenAI"
description: "Hướng dẫn xây dựng hệ thống tự động tìm kiếm, làm giàu dữ liệu và đánh giá tiềm năng khách hàng (Lead Scoring) bằng AI hoàn toàn tự động."
slug: "tu-dong-tim-kiem-va-cham-diem-lead-doanh-nghiep-dia-phuong"
tags: [n8n, automation, no-code, lead-generation, openai, google-sheets]
keywords: [n8n workflow, tim kiem lead tu dong, openai lead scoring, google sheets automation, rapidapi]
---

# 🚀 Tự động tìm kiếm và chấm điểm Lead doanh nghiệp địa phương với n8n, Google Sheets, RapidAPI & OpenAI

Việc đi tìm khách hàng tiềm năng (Lead Generation) thủ công cho các dịch vụ địa phương luôn ngốn rất nhiều thời gian của các đội ngũ sales: từ việc tra cứu Google Maps, lọc thông tin liên hệ (email, số điện thoại, website) cho đến việc đánh giá xem doanh nghiệp đó có thực sự phù hợp để tiếp cận hay không. 

Đừng để những công việc lặp đi lặp lại làm chậm tốc độ phát triển kinh doanh của bạn! Bài viết này sẽ hướng dẫn các sếp triển khai một workflow n8n cực kỳ mạnh mẽ, tự động hóa 100% quy trình: **Đọc từ khoá -> Tìm kiếm qua API -> Làm sạch dữ liệu -> Dùng AI chấm điểm và viết nội dung outreach -> Lưu kết quả về Google Sheets**.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn:** Chạy định kỳ nhờ lịch trình (Schedule Trigger) mà không cần can thiệp thủ công.
- **Làm giàu dữ liệu chính xác:** Lấy đầy đủ thông tin liên hệ (Email, Phone, Website, Địa chỉ) từ RapidAPI.
- **AI thông minh phân loại lead:** OpenAI tự động phân tích, gán điểm số tiềm năng (Lead Score) và soạn sẵn thông điệp tiếp cận (Outreach message) cá nhân hóa cho từng doanh nghiệp.
- **Lưu trữ gọn gàng:** Tự động đồng bộ và cập nhật danh sách leads vào Google Sheets để đội ngũ sales bắt tay vào chốt đơn ngay.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Google Sheets:** File chứa từ khóa tìm kiếm (Keywords) và địa điểm (Locations).
- **RapidAPI Key:** Tài khoản RapidAPI để gọi dịch vụ tìm kiếm doanh nghiệp địa phương.
- **OpenAI API Key:** Để sử dụng model AI chấm điểm và viết nội dung.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow hoặc copy đoạn JSON trực tiếp.
- Trong giao diện n8n Editor, chọn **Add workflow** -> Nhấp vào biểu tượng ba chấm ở góc trên bên phải -> **Import from File / Import from Clipboard** và dán mã JSON vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 6 nodes chính được cấu hình mạch lạc, các sếp cần chú ý thiết lập các thông số sau:

- **Schedule Trigger:** Cài đặt tần suất chạy workflow mong muốn (ví dụ: Chạy mỗi ngày một lần hoặc hàng tuần).
- **Read Search Requests (Google Sheets):** Kết nối tài khoản Google của bạn, trỏ tới file Google Sheets chứa danh sách từ khóa (`Keyword`), địa điểm (`Location`) và mã định danh (`ID`).
- **Search Businesses API (HTTP Request):** 
  - Cấu hình endpoint API từ RapidAPI.
  - Thêm API Key của bạn vào phần header xác thực của request.
- **Format Business Results (Code):** Node này sử dụng JavaScript thuần để làm sạch, lọc và cấu trúc lại dữ liệu thô từ API trả về thành các trường gọn gàng, sẵn sàng cho AI xử lý.
- **Message a model (OpenAI):** 
  - Kết nối OpenAI Credentials.
  - Thiết lập Prompt để AI tiến hành phân loại doanh nghiệp, chấm điểm tiềm năng (Lead Score) và viết nội dung tin nhắn outreach ngắn gọn, thu hút.
- **Write to Business Results (Google Sheets):** 
  - Chọn thao tác `appendOrUpdate`.
  - Mapping các trường dữ liệu đã được làm sạch và AI chấm điểm trả về các cột tương ứng trong Google Sheets để đội ngũ sales dễ dàng theo dõi.

#### 3. Kích hoạt ⚡️
- Nhấn **Test step** hoặc **Execute Workflow** trên từng node để kiểm tra dữ liệu mẫu chạy qua có chính xác hay không.
- Sau khi test thành công, gạt công tắc **Active** ở góc trên bên phải để workflow tự động vận hành.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Nối thêm node **Slack** hoặc **Telegram** sau bước ghi vào Google Sheets để bắn thông báo ngay lập tức về nhóm Sales mỗi khi có một "Hot Lead" điểm cao xuất hiện.
- **Lọc thông minh:** Tận dụng biểu thức điều kiện (If Node) để chỉ lưu trữ hoặc gửi thông báo cho những doanh nghiệp đạt điểm số (Lead Score) từ 8/10 trở lên.
- **Tự động gửi email:** Kết hợp thêm node Gmail hoặc Resend để tự động gửi thư giới thiệu dịch vụ dựa trên nội dung mà OpenAI đã soạn sẵn.

### 📌 Kết luận
Hệ thống tìm kiếm và chấm điểm lead tự động này sẽ giải phóng toàn bộ thời gian tra cứu thủ công, giúp đội ngũ của bạn tập trung 100% vào việc chốt sales. Hãy áp dụng ngay vào quy trình kinh doanh của doanh nghiệp các sếp nhé!