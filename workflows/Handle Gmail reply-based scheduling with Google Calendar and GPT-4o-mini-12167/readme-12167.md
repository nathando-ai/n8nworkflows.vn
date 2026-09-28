---
title: "🚀 Tự động hóa lịch họp qua Email với Gmail, Google Calendar và GPT-4o-mini"
description: "Hướng dẫn thiết lập workflow n8n tự động lên lịch họp, kiểm tra lịch trống trên Google Calendar, xử lý phản hồi qua Gmail và tích hợp AI thông minh."
slug: "tu-dong-hoa-lich-hop-gmail-google-calendar-gpt-4o-mini"
tags: [n8n, automation, no-code, gpt-4o-mini, google-calendar, gmail]
keywords: [n8n workflow, tu dong hoa lich hop, google calendar api, gmail automation, openai n8n]
---

# 🚀 Tự động hóa lịch họp qua Email với Gmail, Google Calendar và GPT-4o-mini

Các sếp có bao giờ cảm thấy mệt mỏi khi phải mất hàng tá email chỉ để chốt được một lịch họp? Nào là "Anh/chị bận giờ này không?", "Em rảnh lúc đó nhưng phòng họp full rồi...", việc tra cứu thủ công lịch trống trên Google Calendar và trao đổi qua lại khiến chúng ta lãng phí quá nhiều thời gian quý báu.

Giải pháp ở đây là gì? Hãy để n8n gánh vác phần việc nhàm chán này! Workflow thông minh này sẽ tự động kiểm tra lịch bận, đề xuất thời gian, lắng nghe phản hồi qua email và tự động tạo lịch hẹn mà các sếp không cần tốn một giọt mồ hôi.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Tự động hóa hoàn toàn quy trình book lịch từ A-Z.
- **Tránh trùng lịch tuyệt đối:** Kiểm tra trạng thái Google Calendar real-time trước khi xác nhận.
- **Cá nhân hóa thông minh:** Sử dụng OpenAI (GPT-4o-mini) để phân tích yêu cầu đặt lịch và phản hồi tự nhiên qua Gmail.
- **Hoạt động 24/7:** Lắng nghe phản hồi từ khách hàng/đối tác qua email để tự động chốt slot hoặc đề xuất giờ mới.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản và credentials sau:
- Tài khoản n8n (Cloud hoặc Self-hosted).
- **OpenAI API Key** (để kết nối node Message a model sử dụng GPT-4o-mini).
- **Google Calendar OAuth2 API** (để kiểm tra lịch trống và tạo sự kiện).
- **Gmail OAuth2 API** (để gửi email xác nhận và nhận phản hồi).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy toàn bộ mã JSON của workflow và paste trực tiếp vào giao diện n8n Editor, hoặc import file JSON tải từ nguồn gốc.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống chạy mượt mà, các sếp cần cấu hình chính xác các node trọng điểm sau:
- **Webhook & Sample Input:** Nơi nhận dữ liệu đầu vào (tiêu đề sự kiện, thời gian bắt đầu, thời gian kết thúc). Hãy test bằng cách gửi một POST request mẫu.
- **Message a model (OpenAI):** Chọn credentials OpenAI và cấu hình model `gpt-4o-mini` để hệ thống xử lý ngôn ngữ tự nhiên, định dạng dữ liệu payload chuẩn xác.
- **Get availability in a calendar & Create an event (Google Calendar):** Kết nối tài khoản Google Calendar qua OAuth2, chọn đúng Calendar ID (thường là `primary`) để kiểm tra lịch bận và tạo lịch hẹn mới.
- **Gmail Trigger (User Reply), Send Confirmation Email & Request Alternative Slots:** Cấu hình credentials Gmail OAuth2 để hệ thống tự động theo dõi email phản hồi, gửi mail xác nhận khi chốt lịch thành công hoặc gửi danh sách khung giờ thay thế nếu lịch bị trùng.

#### 3. Kích hoạt ⚡️
- Thực hiện **Test run** với nút *Execute Workflow* và truyền dữ liệu mẫu vào node Webhook để kiểm tra luồng chạy.
- Sau khi test thành công không lỗi lầm, bật nút **Active** ở góc trên bên phải để workflow chính thức trực tuyến 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thêm thông báo:** Nối thêm một node Telegram hoặc Slack vào nhánh `Create Calendar Event` để nhận thông báo ngay lập tức trên điện thoại mỗi khi có lịch họp mới được chốt.
- **Ghi log dữ liệu:** Thêm node Google Sheets để lưu trữ toàn bộ lịch sử đặt lịch nhằm phục vụ việc thống kê, báo cáo định kỳ.
- **Mở rộng múi giờ:** Đảm bảo cấu hình đúng múi giờ (Timezone) trong các node thời gian để tránh việc lệch giờ họp với đối tác quốc tế.

### 📌 Kết luận
Workflow xử lý đặt lịch họp qua Gmail kết hợp Google Calendar và AI thực sự là một "vũ khí bí mật" giúp tối ưu hóa hiệu suất làm việc cá nhân cũng như doanh nghiệp. Hãy cài đặt ngay hôm nay để trải nghiệm sự rảnh tay mà tự động hóa mang lại nhé các sếp!