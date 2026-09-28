---
title: "🚀 Biến quá trình học Toán thành game nhập vai (RPG) cực cuốn với n8n, Google Sheets và OpenRouter"
description: "Tự động hóa việc biến nhật ký học tập nhàm chán thành các thử thách toán học phong cách RPG (game nhập vai) hấp dẫn bằng AI, lưu trữ trực quan qua Google Sheets."
slug: "bien-hoc-toan-thanh-game-rpg-voi-n8n-google-sheets-openrouter"
tags: [n8n, automation, ai, openrouter, google-sheets, gamification, education]
keywords: [n8n workflow, gam hóa học tập, AI math RPG, OpenRouter gpt-4o-mini, tự động hóa n8n, google sheets automation]
---

# 🚀 Biến quá trình học Toán thành game nhập vai (RPG) cực cuốn với n8n, Google Sheets và OpenRouter

Các sếp có bao giờ cảm thấy việc học tập, đặc biệt là môn Toán, thường rất khô khan và dễ nản lòng? Việc duy trì động lực mỗi ngày là một bài toán khó cho cả học sinh, phụ huynh lẫn giáo viên. 

Thay vì bắt ép học viên học theo cách truyền thống, tại sao chúng ta không **Gamify (Biến thành trò chơi)** quá trình đó? Workflow n8n này sẽ tự động hóa việc tiếp nhận nhật ký học tập, tính toán điểm kinh nghiệm (EXP), tra cứu cấp độ và sử dụng AI (thông qua OpenRouter) để sinh ra một con quái vật cùng câu hỏi toán học mang phong cách game nhập vai (RPG) hoàn toàn tự động!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Biến học tập thành trò chơi:** Kích thích sự hào hứng, tò mò qua từng thử thách tiêu diệt quái vật toán học.
- **Cá nhân hóa theo cấp độ:** Câu hỏi và độ khó được AI điều chỉnh thông minh dựa trên level hiện tại của người dùng lấy từ Google Sheets.
- **Tự động hóa 100%:** Từ việc nhận form đầu vào, ghi nhận dữ liệu, tính toán EXP cho đến lưu trữ quest mà không cần can thiệp thủ công.
- **Lưu trữ minh bạch:** Mọi dữ liệu nhật ký, thông tin người dùng và thử thách đều được quản lý gọn gàng trên Google Sheets.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n:** (Cloud hoặc Self-hosted).
- **Google Account:** Để kết nối và thao tác với Google Sheets.
- **OpenRouter API Key:** Để sử dụng mô hình AI thông minh (mặc định cấu hình sẵn `openai/gpt-4o-mini`).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp hãy copy mã JSON của workflow này hoặc import trực tiếp file vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 7 nodes chính được liên kết mượt mà. Các sếp cần chú ý cấu hình các điểm sau:

- **Chuẩn bị Google Sheets:** Tạo một file Google Sheet mới với 3 tab (sheets) có tên chính xác là:
  1. `StudyLogs` (Lưu nhật ký thời gian học)
  2. `Users` (Lưu thông tin cấp độ, EXP của người dùng)
  3. `Quests` (Lưu các nhiệm vụ/câu hỏi được AI sinh ra với trạng thái `pending`)

- **Các Nodes Google Sheets (`Add to StudyLogs`, `Get User Status`, `Save Quest`):**
  - Kết nối tài khoản của các sếp bằng `Google Sheets OAuth2 API`.
  - Trỏ đúng đến file Google Sheet vừa tạo và chọn đúng tên 3 tab tương ứng cho từng node.

- **Node AI (`OpenRouter Chat Model` & `Basic LLM Chain`):**
  - Thêm OpenRouter API Key vào credentials của node `OpenRouter Chat Model`.
  - Model mặc định được thiết lập là `openai/gpt-4o-mini` - vừa nhanh, thông minh lại cực kỳ tối ưu chi phí.

- **Node kích hoạt (`Study Log Input Form`):**
  - Cung cấp giao diện form để người dùng nhập thời gian và nội dung học tập mỗi ngày.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** và test thử bằng cách điền thông tin vào `Study Log Input Form`.
- Kiểm tra xem Google Sheets đã ghi nhận dữ liệu và AI đã tạo ra thử thách RPG chưa.
- Nếu mọi thứ chạy mượt mà, hãy gạt công tắc sang **Active** để hệ thống tự động hoạt động 24/7!

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng chủ đề:** Không chỉ riêng môn Toán, các sếp có thể dễ dàng sửa Prompt trong node LLM để biến nó thành hệ thống đố vui Lịch sử, từ vựng Tiếng Anh hoặc Khoa học.
- **Tích hợp thông báo:** Nối thêm node Telegram hoặc Slack sau bước `Save Quest` để ngay khi AI tạo xong thử thách, hệ thống sẽ bắn tin nhắn trực tiếp báo động cho người chơi vào "chiến đấu".
- **Làm thêm Part 2:** Như tác giả gợi ý, các sếp có thể làm thêm một workflow nhận đáp án trả lời của người dùng để tính thưởng EXP và thăng cấp (Level Up) tự động.

### 📌 Kết luận
Một workflow tuyệt vời để ứng dụng AI vào giáo dục và tự động hóa thói quen cá nhân. Hãy "lên đồ" ngay để biến việc học tập mỗi ngày thành một cuộc phiêu lưu thú vị cùng n8n và Google Sheets các sếp nhé!