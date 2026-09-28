---
title: "🚀 Biến việc tập luyện thành trò chơi nhập vai với AI Multi-Agents và Google Sheets"
description: "Hướng dẫn xây dựng hệ thống gamification theo dõi sức khỏe tự động 100% sử dụng GPT-4o-mini qua OpenRouter, Google Sheets và n8n."
slug: "gamify-fitness-tracking-multi-agents-n8n"
tags: [n8n, automation, no-code, ai-agents, openrouter, google-sheets]
keywords: [n8n workflow, gamification fitness, ai multi agents, openrouter gpt-4o-mini, google sheets automation]
---

# 🚀 Biến việc tập luyện thành trò chơi nhập vai với AI Multi-Agents và Google Sheets

Việc duy trì chế độ tập luyện, ăn uống lành mạnh thường rất dễ nản lòng nếu thiếu đi động lực. Các phương pháp theo dõi truyền thống thường khô khan và nhàm chán. Giải pháp gì để biến hành trình rèn luyện sức khỏe thành một tựa game phiêu lưu kỳ thú? 

Workflow n8n này sẽ biến việc theo dõi sức khỏe của các sếp thành một cuộc phiêu lưu cướp biển đích thực. Hệ thống sử dụng mô hình đa tác nhân (**Multi-Agents**) thông qua **OpenRouter (GPT-4o-mini)** để đánh giá các hoạt động, tính điểm thưởng "Bounty" (Tiền thưởng truy nã) và đưa ra những lời khuyên cực kỳ thú vị từ các nhân vật chuyên gia khác nhau!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Biến việc tập luyện thành trò chơi:** Tăng động lực nhờ hệ thống tích điểm "Bounty" độc đáo như One Piece.
- **Tư vấn đa chuyên gia AI:** Tự động định tuyến câu hỏi đến đúng chuyên gia (Đầu bếp dinh dưỡng, Kiếm sĩ rèn luyện thể lực, Bác sĩ phục hồi, Hoa tiêu định hướng).
- **Lưu trữ dữ liệu thông minh:** Tự động cập nhật điểm số và ghi lại lịch sử trò chuyện trên Google Sheets để theo dõi tiến độ dài hạn.
- **Tự động hóa 100% không cần code:** Vận hành trơn tru ngay trên n8n với chi phí tối ưu từ GPT-4o-mini.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Tài khoản Google** (để cấu hình Google Sheets).
- **API Key từ OpenRouter** (hoặc OpenAI) để kết nối các node AI Agent.
- **File Google Sheets mẫu** với cấu trúc 2 tab: `Profile` và `Log`.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tạo một workflow mới trên n8n, sau đó copy toàn bộ JSON của workflow hoặc import file trực tiếp vào giao diện n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống hoạt động mượt mà, các sếp cần chú ý cấu hình các thành phần sau:

- **Google Sheets (Get row(s) in sheet, Update User Bounty, Save Logs...):** 
  - Tạo một Google Sheet mới với 2 tab:
    - Tab `Profile`: Các cột gồm `ID`, `Total_Bounty`.
    - Tab `Log`: Các cột gồm `Date`, `Crew`, `Inquiry`, `Response`.
  - Thay thế `YOUR_SPREADSHEET_ID` bằng ID Google Sheet thực tế của các sếp trong tất cả các node tương tác với Google Sheets.
  - Kết nối `Google Sheets OAuth2 API` credentials cho các node.
- **OpenRouter Chat Model:** 
  - Chọn model là `openai/gpt-4o-mini` (hoặc model tùy ý hỗ trợ qua OpenRouter).
  - Cấu hình API Key của OpenRouter vào phần credentials.
- **AI Scorer & Intent Classifier, Chef Agent, Samurai Agent, Doctor Agent, Navigator Agent:**
  - Kiểm tra lại các prompt hệ thống bên trong các node LangChain này để đảm bảo các Agent phản hồi đúng phong cách nhập vai cướp biển mà các sếp mong muốn.
- **Bounty Calculator (JS Logic):**
  - Node này dùng JavaScript để tính toán số điểm "Bounty" cộng thêm dựa trên điểm số (0-100) mà `AI Scorer` đánh giá. Các sếp có thể tùy chỉnh công thức thưởng phạt tại đây.

#### 3. Kích hoạt ⚡️
- Sử dụng tính năng **Chat Trigger** để gửi tin nhắn test thử (ví dụ: *"Hôm nay tôi đã chạy bộ 5km và ăn một đĩa salad ức gà"*).
- Kiểm tra xem Google Sheets đã cập nhật điểm Bounty và lưu Log chính xác chưa.
- Bật công tắc **Active** để đưa workflow vào hoạt động chính thức 24/7!

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Telegram/Slack Bot:** Thay vì dùng widget chat mặc định của n8n, các sếp có thể kết nối Telegram Bot để báo cáo sức khỏe trực tiếp mọi lúc mọi nơi.
- **Báo cáo tuần tự động:** Tạo thêm một nhánh lịch trình (Cron node) để tổng kết tổng điểm Bounty và gửi báo cáo tóm tắt vào cuối tuần.
- **Thêm phần thưởng thực tế:** Thiết lập quy đổi mốc Bounty nhất định ra các phần thưởng ngoài đời thực (như một buổi đi chơi, món ăn yêu thích...) để tăng tính gamification.

### 📌 Kết luận
Với workflow n8n kết hợp AI Multi-Agents này, việc chăm sóc sức khỏe không còn là nghĩa vụ nặng nề mà trở thành một tựa game phiêu lưu đầy thú vị mỗi ngày. Hãy "lên đồ", import ngay workflow và bắt đầu cuộc hành trình chinh phục vóc dáng mơ ước của các sếp ngay hôm nay!