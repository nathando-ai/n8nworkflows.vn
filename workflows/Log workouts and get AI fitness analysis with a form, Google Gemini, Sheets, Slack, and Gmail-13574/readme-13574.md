---
title: "🏋️ Tự động hóa nhật ký tập luyện & nhận phân tích AI từ Google Gemini, Sheets, Slack và Gmail"
description: "Xây dựng hệ thống tracking tập luyện thông minh bằng n8n: nhập liệu qua form, AI phân tích bài tập, lưu Google Sheets và gửi thông báo đa kênh."
slug: "tu-dong-hoa-nhat-ky-tap-luyen-ai-n8n"
tags: [n8n, automation, ai, google-gemini, google-sheets, slack, gmail]
keywords: [n8n workflow, workout tracker ai, google gemini n8n, tu dong hoa tap luyen, n8n form trigger]
---

# 🏋️ Tự động hóa nhật ký tập luyện & nhận phân tích AI đỉnh cao

Việc ghi chép lại quá trình tập luyện (gym, chạy bộ, yoga...) thường khá thủ công, rời rạc và đôi khi chúng ta lười thống kê lại xem nhóm cơ nào chưa được tập hoặc lượng calo tiêu hao ra sao. Việc nhập liệu bằng tay vào Excel hay Google Sheets vừa mất thời gian vừa thiếu đi những lời khuyên chuyên sâu mang tính cá nhân hóa.

Workflow n8n này sinh ra để giải quyết triệt để vấn đề đó! Chỉ với một đoạn mô tả ngắn gọn bằng văn bản tự nhiên (plain text) qua Web Form, hệ thống sẽ tự động hóa từ A-Z: phân tích bài tập bằng AI, tính toán calo, lưu trữ vào Google Sheets, đồng thời gửi báo cáo chi tiết qua Slack và Gmail. Tất cả diễn ra trong vòng vài giây!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Nhập liệu siêu tốc:** Chỉ cần gõ tự do (Ví dụ: *"Bench press 60kg x10 x3, chạy bộ 5km"*), AI sẽ tự động phân tách cấu trúc.
- **Phân tích chuyên sâu từ AI:** Google Gemini tự động tính toán lượng calo đốt cháy, xác định các nhóm cơ đã tác động và gợi ý bài tập tiếp theo.
- **Lưu trữ tự động:** Tự động tạo bản ghi có cấu trúc chuyên nghiệp trên Google Sheets mà không cần thao tác tay.
- **Đa kênh thông báo:** Nhận ngay thông báo nhanh qua Slack và báo cáo chi tiết kèm lời khuyên qua Gmail ngay sau buổi tập.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Google Gemini API Key** (Lấy miễn phí từ Google AI Studio).
- **Google Sheets** (Để lưu trữ nhật ký tập luyện).
- **Slack Workspace** (Để nhận tin báo cáo nhanh).
- **Gmail Account** (Để nhận email tóm tắt và lời khuyên).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow hoặc copy trực tiếp mã JSON, sau đó dán (Paste) vào trình soạn thảo n8n của các sếp để khởi tạo hệ thống.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow hoạt động trơn tru, các sếp cần cấu hình chính xác các node sau:
- **Workout Log Form (`formTrigger`)**: Node này tạo một Web Form công cộng. Các sếp có thể lưu lại URL của form này hoặc ghim sẵn trên màn hình điện thoại để tiện nhập liệu ngay tại phòng tập giữa các hiệp.
- **Google Gemini (`lmChatGoogleGemini`) & Analyze Workout with AI (`chainLlm`)**: Nhập Google Gemini API Key để kích hoạt khả năng đọc hiểu văn bản và phân tích dữ liệu tập luyện của AI.
- **Save to Workout Sheet (`googleSheets`)**: 
  - Tạo sẵn một Google Sheet với tab tên là **`Workouts`**.
  - Đặt các tiêu đề cột (Headers) chính xác: `Date`, `Workout`, `Duration`, `Feeling`, `Type`, `Exercises`, `Calories`, `Muscles`, `Intensity`, `Tips`, `Next Suggestion`, `Notes`, `Logged At`.
  - Kết nối tài khoản Google và trỏ đúng vào file Sheet vừa tạo (Cơ chế hoạt động: `appendOrUpdate`).
- **Notify on Slack (`slack`)**: Kết nối tài khoản Slack và chọn channel nhận thông báo (ví dụ: `#fitness` hoặc channel riêng của các sếp).
- **Email Summary (`gmail`)**: Kết nối tài khoản Gmail để hệ thống gửi email tổng kết.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** và test thử bằng cách điền một bài tập mẫu vào form.
- Kiểm tra xem dữ liệu đã đổ về Google Sheets, Slack và Gmail chưa.
- Nếu mọi thứ hoạt động hoàn hảo, hãy gạt công tắc **Active** để đưa workflow vào vận hành chính thức 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Telegram:** Thay vì chỉ dùng Slack và Gmail, các sếp có thể bổ sung thêm node Telegram để nhận tin nhắn tóm tắt cực nhanh trên điện thoại cá nhân.
- **Dashboard trực quan:** Kết nối Google Sheet vừa lưu vào Looker Studio (Google Data Studio) để vẽ biểu đồ theo dõi quá trình tăng cơ/giảm mỡ theo tuần/tháng.
- **Tạo bảng nhắc nhở:** Thêm một node `Schedule Trigger` để tự động gửi thông báo động lực hoặc lịch tập vào khung giờ cố định mỗi ngày nếu phát hiện hôm đó chưa có log tập luyện nào.

### 📌 Kết luận
Một hệ thống quản lý và phân tích thể hình cá nhân hóa hoàn toàn tự động đã sẵn sàng phục vụ các sếp. Hãy triển khai ngay hôm nay để tối ưu hóa hiệu quả tập luyện và biến công nghệ thành trợ lý sức khỏe đắc lực nhất!