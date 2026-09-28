---
title: "🚀 Săn vé máy bay giá rẻ tự động qua Telegram với Google Gemini, GPT-4 và BrowserAct"
description: "Hướng dẫn cài đặt workflow n8n tự động phân tích yêu cầu săn vé qua Telegram, cào dữ liệu giá vé từ web bằng BrowserAct và gửi kết quả tối ưu qua AI."
slug: "san-ve-may-bay-gia-re-tu-dong-telegram-browseract"
tags: [n8n, automation, telegram, ai, browseract, travel]
keywords: [n8n workflow, san ve may bay, automation telegram, browseract, google gemini, gpt-4]
---

# 🚀 Săn vé máy bay giá rẻ tự động qua Telegram với Google Gemini, GPT-4 và BrowserAct

Các sếp có bao giờ mệt mỏi vì phải mò mẫm hàng giờ trên các trang web đặt vé máy bay để tìm chuyến bay rẻ nhất? Việc tìm kiếm thủ công không chỉ tốn thời gian mà còn dễ bỏ lỡ các đợt flash sale chớp nhoáng. 

Đừng lo, bài viết này sẽ hướng dẫn các sếp thiết lập một trợ lý AI "thần thánh" trên Telegram. Chỉ cần nhắn một tin nhắn, hệ thống sẽ tự động cào dữ liệu, lọc giá hời và gửi thẳng danh sách chuyến bay tối ưu về điện thoại của các sếp!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Chỉ cần chat qua Telegram bot để bắt đầu tìm kiếm chuyến bay mà không cần mở trình duyệt.
- **AI thông minh:** Sử dụng Google Gemini và GPT-4 để hiểu ngữ cảnh, xác thực điểm khởi hành và phân tích dữ liệu giá vé.
- **Cào dữ liệu thời gian thực:** Tích hợp BrowserAct để tự động thao tác trên các trang web du lịch (như Momondo) lấy giá vé chính xác nhất.
- **Báo cáo gọn gàng:** Kết quả được xử lý, lọc giá rẻ và chia nhỏ thông minh để gửi qua Telegram mà không sợ vượt giới hạn ký tự.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động trơn tru, các sếp cần chuẩn bị sẵn các tài khoản và API Keys sau:
- **Telegram Bot Token:** Tạo qua `@BotFather` trên Telegram.
- **BrowserAct Account & API:** Nền tảng tự động hóa trình duyệt (Cần chuẩn bị sẵn template **Low-Cost Travel Finder** trong tài khoản BrowserAct).
- **Google Gemini API Key:** Dùng cho các node AI xác thực input.
- **OpenRouter API Key (GPT-4.1):** Dùng cho AI phân tích và tổng hợp dữ liệu chuyến bay.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow hoặc copy toàn bộ JSON từ nguồn gốc.
- Mở n8n Editor, chọn **Add workflow** -> Nhấn tổ hợp `Ctrl + V` (hoặc `Cmd + V`) để dán workflow lên canvas.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình kỹ các node trọng điểm sau:
- **User Sends Message to Bot & Answer the User & Process Initialization Alert & Send Travel List to User:** Kết nối các node Telegram này với thông tin `Telegram API` credentials của bot các sếp vừa tạo.
- **Validate user Inputs & Google Gemini:** Chọn credentials `Google Gemini API` (`googlePalmApi`) để AI nhận diện đúng ý định người dùng (ví dụ: *"Tìm vé từ London"*).
- **OpenRouter Model:** Cấu hình `OpenRouter API` credentials và đảm bảo model được trỏ đúng đến `openai/gpt-4.1` để phân tích dữ liệu mượt mà.
- **Run "Low-Const Travel Finder" workflow:** Kết nối node `BrowserAct` với credentials tương ứng và trỏ đến template **Low-Cost Travel Finder** đã thiết lập sẵn trên nền tảng BrowserAct.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và thử gửi một tin nhắn mẫu tới Telegram Bot của sếp (ví dụ: *"Low-Cost Travel Finder For London"*).
- Kiểm tra log trên n8n xem các bước chạy đã chuẩn xác chưa.
- Sau khi test thành công, bật công tắc **Active** góc trên cùng bên phải để bot hoạt động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Google Sheets:** Thêm một node Google Sheets ở cuối chuỗi để lưu lịch sử các tìm kiếm và chuyến bay giá rẻ vào bảng tính phục vụ việc theo dõi dài hạn.
- **Thông báo đa kênh:** Ngoài Telegram, các sếp có thể clone nhánh kết quả để đẩy thêm thông báo về Slack hoặc Discord của nhóm.
- **Tránh giới hạn (Rate Limits):** Node `Avoid Rate Limits` (Wait) đã được thiết lập sẵn giúp ngắt nhịp gửi tin nhắn hợp lý, tránh việc bot Telegram bị khóa do spam quá nhiều request cùng lúc.

### 📌 Kết luận
Workflow săn vé máy bay tự động này là một minh chứng tuyệt vời cho sức mạnh kết hợp giữa n8n, AI thế hệ mới (Gemini/GPT-4) và công cụ cào web thông minh (BrowserAct). Hãy triển khai ngay để có những chuyến đi tiết kiệm thời gian và tiền bạc nhất các sếp nhé!