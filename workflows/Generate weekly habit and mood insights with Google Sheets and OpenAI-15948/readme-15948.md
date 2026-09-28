---
title: "🚀 Tự động hóa Nhật ký Tâm trạng & Thói quen hàng tuần với n8n và OpenAI"
description: "Hướng dẫn xây dựng hệ thống tự động ghi nhận check-in hàng ngày, tính điểm sức khỏe, thói quen và tổng hợp báo cáo AI hàng tuần qua Google Sheets và Gmail."
slug: "tu-dong-hoa-nhat-ky-tam-trang-thoi-quen-n8n-openai"
tags: [n8n, automation, no-code, openai, googlesheets, productivity]
keywords: [n8n workflow, tu dong hoa nhat ky, habit tracker, mood tracking, openai n8n, google sheets automation]
keywords: [n8n workflow, tự động hóa, habit tracker, mood insights, openai, google sheets]
---

# 🚀 Tự động hóa Nhật ký Tâm trạng & Thói quen hàng tuần với n8n và OpenAI

Các sếp có bao giờ cảm thấy việc theo dõi thói quen (habit tracking) và nhật ký tâm trạng (mood journal) cá nhân thủ công rất dễ bỏ cuộc? Việc ghi chép mỗi ngày rồi cuối tuần ngồi tổng hợp lại xem tuần qua mình sống thế nào thường tốn rất nhiều thời gian và thiếu tính kỷ luật.

Workflow n8n này chính là giải pháp tự động hóa 100% giúp các sếp giải quyết triệt để bài toán trên. Hệ thống sẽ tự động thu thập form check-in hàng ngày, tính toán điểm số sức khỏe/thói quen bằng code thông minh, lưu trữ vào Google Sheets, và đặc biệt là dùng **OpenAI** để phân tích, đưa ra lời khuyên huấn luyện (coaching insights) cá nhân hóa gửi vào email mỗi tuần!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa toàn diện:** Không cần thủ công tổng hợp số liệu mỗi tuần.
- **Chấm điểm thông minh:** Tự động tính điểm Wellbeing (sức khỏe tinh thần/thể chất) và Habit (thói quen) dựa trên các chỉ số đầu vào.
- **Phân tích chuyên sâu từ AI:** OpenAI đóng vai trò như một "Life Coach" phân tích xu hướng tuần, tìm ra ngày tốt nhất/tệ nhất và đề xuất 1 thử nghiệm nhỏ cho tuần tới.
- **Hệ thống cảnh báo an toàn:** Tự động gửi email động viên nhẹ nhàng (`Send Supportive Confirmation`) khi phát hiện mức độ căng thẳng cao hoặc tâm trạng xuống thấp.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản n8n (Cloud hoặc Self-hosted).
- Tài khoản **Google** (Google Sheets để lưu dữ liệu và Gmail để gửi email).
- Tài khoản **OpenAI API** (hoặc tích hợp model tương thích qua LangChain).
- File Google Sheet cấu trúc sẵn 2 tab: `daily_entries` và `weekly_reports`.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow từ nguồn hoặc copy toàn bộ JSON dán trực tiếp vào n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 2 nhánh chính hoạt động độc lập:

*   **Nhánh 1: Check-in hàng ngày (Daily Check-in Branch)**
    - **On form submission (`formTrigger`)**: Form thu thập dữ liệu hàng ngày của người dùng.
    - **Normalize Answers (`set`) & Calculate Daily Scores (`code`)**: Chuyển đổi dữ liệu thô và tính điểm `wellbeing_score`, `habit_score`, `risk_flag`.
    - **Append Daily Entry (`googleSheets`)**: Chọn đúng file Google Sheets và chọn sheet tab `daily_entries`.
    - **Check Support Flag (`if`)**: Kiểm tra nếu `risk_flag` là `needs_support` sẽ chuyển hướng sang node **Send Supportive Confirmation**, ngược lại gửi **Send Normal Confirmation** qua **Gmail**.

*   **Nhánh 2: Tổng hợp hàng tuần (Weekly Insights Branch)**
    - **Weekly Report Trigger (`scheduleTrigger`)**: Cài đặt chạy định kỳ (Ví dụ: 8:00 sáng thứ Hai hàng tuần).
    - **Get Daily Entries (`googleSheets`)**: Lấy toàn bộ dữ liệu từ tab `daily_entries`.
    - **Calculate Weekly Analytics (`code`)**: Lọc dữ liệu trong vòng 7 ngày qua, tính điểm trung bình, tìm ngày tốt nhất/tệ nhất.
    - **Enough Entries? (`if`)**: Đảm bảo số lượng bản ghi tối thiểu (>= 3 ngày) mới tiến hành gọi AI để đảm bảo độ chính xác. Nếu không đủ dữ liệu sẽ gửi email nhắc nhở qua **Send Not Enough Data Message**.
    - **Basic LLM Chain (`chainLlm`) & OpenAI Chat Model (`lmChatOpenAi`)**: Cấu hình credentials OpenAI và model (khuyên dùng `llama-3.1-8b-instant` hoặc `gpt-4o-mini`). LLM nhận prompt yêu cầu phân tích dữ liệu dạng JSON ngắn gọn, không dùng Markdown rườm rà.
    - **Parse AI Reflection JSON (`code`)**: Xử lý chuỗi JSON trả về từ AI thành các trường dữ liệu n8n sạch sẽ.
    - **Append Weekly Report (`googleSheets`)**: Lưu báo cáo vào tab `weekly_reports`.
    - **Email Weekly Insights (`gmail`)**: Gửi báo cáo tổng hợp tuần tới email của các sếp.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm thủ công (Test run) từng node để kiểm tra kết nối Google Sheets và Gmail OAuth2.
- Bật công tắc **Active** ở góc trên cùng bên phải để workflow tự động vận hành.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Chatbot:** Thay vì chỉ nhận email hàng tuần, các sếp có thể nối thêm node **Telegram** hoặc **Slack** để bot chủ động bắn thông báo vào nhóm chat cá nhân.
- **Lưu trữ Log lỗi:** Thêm một nhánh nhỏ xử lý ngoại lệ (Error Trigger) để đề phòng trường hợp OpenAI API lỗi hoặc hết hạn ngạch Google Sheets.
- **Mở rộng chỉ số:** Các sếp có thể tùy chỉnh code tính điểm trong node `Calculate Daily Scores` để thêm các thói quen cá nhân riêng như: số trang sách đọc được, thời gian tập thể dục, hay lượng nước uống mỗi ngày.

### 📌 Kết luận
Một hệ thống tự chăm sóc bản thân (Personal Growth Automation) cực kỳ xịn sò đã sẵn sàng hoạt động. Hãy import workflow ngay hôm nay để biến những con số check-in thô kệch thành các insight thay đổi cuộc sống của các sếp!