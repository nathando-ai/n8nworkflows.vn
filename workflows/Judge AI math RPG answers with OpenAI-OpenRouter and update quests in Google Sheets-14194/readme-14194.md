---
title: "🚀 Tự động hóa hệ thống RPG Toán học với AI: Chấm điểm bài tập qua Form và Google Sheets"
description: "Biến việc học toán thành trò chơi nhập vai (RPG) thú vị. Workflow n8n tự động chấm điểm bài tập, cập nhật Google Sheets và tạo thông điệp chiến thắng bằng AI cực kỳ hấp dẫn."
slug: "tu-dong-hoa-he-thong-rpg-toan-hoc-voi-ai-n8n"
tags: [n8n, automation, no-code, google-sheets, openrouter, ai-rpg]
keywords: [n8n workflow, tự động hóa google sheets, AI math RPG, openrouter gpt-4o-mini, chấm điểm tự động n8n]
---

# 🚀 Chấm điểm bài tập Toán phong cách RPG bằng AI và Google Sheets

Các sếp có bao giờ cảm thấy việc học tập, giải bài tập hay giao bài cho học sinh/con em mình quá nhàm chán? Việc làm bài tập thủ công thường thiếu đi sự hứng thú và tốn nhiều thời gian theo dõi tiến độ. 

Workflow này chính là **Phần 2** trong hệ thống **"AI Math RPG"** do tác giả *TAKUTO ISHIKAWA* xây dựng. Nó giúp tự động hóa hoàn toàn quy trình nhận đáp án từ Form, kiểm tra kết quả một cách thông minh, cập nhật trạng thái nhiệm vụ (quest) lên Google Sheets và sử dụng AI để tạo ra những thông điệp chúc mừng đậm chất game nhập vai! Điểm hay nhất là workflow này tối ưu chi phí tối đa: **không tốn token AI cho các phép tính cơ bản**, chỉ dùng AI khi người chơi chiến thắng để tạo sự hào hứng.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 và xử lý các form tương tác mượt mà, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Gamification hóa việc học:** Biến bài tập khô khan thành một tựa game RPG với hệ thống nhiệm vụ và phần thưởng.
- **Tiết kiệm chi phí API:** Sử dụng node `IF` thuần túy để check đáp án toán học thay vì bắt AI đọc và tính toán, tiết kiệm tối đa token.
- **Tự động hóa hoàn toàn:** Tự động tra cứu quest `pending` trên Google Sheets, cập nhật trạng thái thành `solved` để tránh việc người chơi "cày" EXP vô hạn.
- **Cá nhân hóa trải nghiệm:** Dùng mô hình `openai/gpt-4o-mini` qua OpenRouter để sinh ra các thông điệp chúc mừng chiến thắng cực kỳ hoành tráng, sinh động.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Google Account:** Có chứa file Google Sheets (Hệ thống nhiệm vụ RPG từ Phần 1).
- **OpenRouter API Key** (hoặc OpenAI API Key) để kết nối với mô hình LLM.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể copy mã JSON của workflow từ trang chủ n8n hoặc sử dụng template có sẵn, sau đó paste trực tiếp vào n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống chạy trơn tru, các sếp cần cấu hình chính xác các node sau:
- **Find Pending Quest & Update Quest Status (Google Sheets):** 
  - Kết nối `googleSheetsOAuth2Api` credentials của các sếp.
  - Thay thế chuỗi `ENTER_YOUR_SPREADSHEET_ID_HERE` bằng ID bảng Google Sheets thực tế của các sếp.
  - Đảm bảo cấu trúc bảng đã đồng bộ với hệ thống nhiệm vụ (có cột trạng thái `status` với giá trị `pending`/`solved`).
- **OpenRouter Chat Model & Generate Victory Message:**
  - Kết nối `openRouterApi` credentials.
  - Kiểm tra lại model được chọn là `openai/gpt-4o-mini` (hoặc thay đổi tùy ý).
- **Quiz Answer Form:**
  - Mở node Form Trigger để lấy link form công khai, cấu hình các trường nhập ID người dùng và đáp án để tiến hành test "trận chiến"!

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và gửi thử một đáp án qua Form để test luồng chạy.
- Sau khi kiểm tra mọi thứ OK, gạt công tắc sang **Active** để đưa hệ thống vào vận hành thực tế 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Biến hóa cốt truyện:** Các sếp có thể chỉnh sửa prompt trong node `Generate Victory Message` để thay đổi chủ đề chiến thắng: từ phong cách kiếm hiệp, khoa học viễn tưởng (Sci-fi), trường phái phép thuật, cho đến các sự kiện lịch sử thú vị!
- **Tích hợp thông báo:** Nối thêm node Telegram hoặc Slack sau node cập nhật thành công để bắn thông báo "Chúc mừng sếp vừa vượt qua thử thách toán học!" về máy cá nhân ngay lập tức.
- **Lưu lịch sử:** Tạo thêm một bảng log phụ để thống kê thời gian hoàn thành nhiệm vụ của từng user.

### 📌 Kết luận
Một workflow tuyệt vời để áp dụng gamification vào giáo dục hoặc tự học cá nhân mà không tốn kém chi phí vận hành. Hãy "lên đồ" ngay trên n8n để biến việc giải toán thành một cuộc phiêu lưu thú vị nhé các sếp!