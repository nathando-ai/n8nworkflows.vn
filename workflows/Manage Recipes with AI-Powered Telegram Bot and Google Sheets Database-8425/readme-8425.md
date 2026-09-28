---
title: "🚀 Xây dựng Bot Telegram Quản lý Công thức Nấu ăn Thông minh bằng n8n và AI"
description: "Hướng dẫn tích hợp Telegram Bot với Google Sheets và AI Agent để tự động hóa việc lưu trữ, tìm kiếm và gợi ý công thức nấu ăn hằng ngày."
slug: "quan-ly-cong-thuc-nau-an-telegram-bot-ai-google-sheets"
tags: [n8n, automation, no-code, telegram-bot, google-sheets, ai-agent, gemini, openai]
keywords: [n8n workflow, bot telegram nấu ăn, quản lý công thức bằng AI, google sheets automation, n8n ai agent]
---

# 🚀 Tự động hóa Quản lý Công thức Nấu ăn với Telegram Bot & AI

Các sếp có bao giờ đau đầu vì sưu tầm hàng trăm công thức nấu ăn trên mạng nhưng đến lúc cần tìm thì lục tung cả Zalo, Facebook, ghi chú điện thoại mà không thấy? Việc quản lý thực đơn hay công thức món ăn thủ công vừa tốn thời gian, vừa lộn xộn.

Đừng lo, bài toán đó sẽ được giải quyết triệt để với workflow n8n cực xịn sò này! Workflow sẽ biến một con **Telegram Bot** thành trợ lý bếp trưởng thông minh. Bot không chỉ kết nối trực tiếp với **Google Sheets** để lưu trữ cơ sở dữ liệu công thức, mà còn tích hợp sức mạnh của **AI Agent (Gemini/OpenAI)** để trò chuyện, thêm món mới, cập nhật hoặc tìm kiếm công thức bằng ngôn ngữ tự nhiên.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tra cứu chớp nhoáng:** Xem danh sách hoặc tìm kiếm chi tiết công thức nấu ăn ngay trên Telegram chỉ trong một nốt nhạc.
- **Trợ lý AI thông minh:** Thêm món mới, sửa công thức hoặc hỏi cách chế biến món ăn bằng văn bản tự nhiên nhờ AI Agent hỗ trợ.
- **Đồng bộ tự động:** Mọi dữ liệu món ăn, nguyên liệu đều được lưu trữ trực quan và an toàn trên Google Sheets.
- **Hoạt động 24/7:** Trợ lý ảo luôn sẵn sàng phục vụ bất cứ lúc nào các sếp bước vào bếp.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài nguyên sau:
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Telegram Bot Token** (Tạo qua [@BotFather](https://t.me/BotFather)).
- **Google Sheets** (Tạo sẵn một file Google Sheets chứa các cột thông tin công thức món ăn).
- **API Key** của Google Gemini hoặc OpenAI để làm "bộ não" cho AI Agent.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy toàn bộ mã JSON của workflow này, vào giao diện n8n Editor, chọn **Import from JSON** và dán vào là xong.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow hoạt động trơn tru, các sếp cần cấu hình chính xác các node quan trọng sau:

- **Telegram Trigger & Telegram Send... nodes:** Kết nối với Credentials của Telegram Bot Token mà các sếp đã tạo từ trước.
- **Read Recipe Names / Lookup Recipe Row / Read Recipes Sheet / Update Recipes Sheet:** 
  - Kết nối tài khoản Google account.
  - Chọn đúng file Google Sheets (`Spreadsheet ID`) và tên bảng (`Sheet Name`) lưu trữ công thức nấu ăn của các sếp.
- **Recipe AI Agent & Google Gemini Chat Model / OpenAI Chat Model:** 
  - Cấu hình API Key cho Model LLM (Gemini hoặc OpenAI).
  - Đảm bảo các tool đi kèm như `Read Recipes Sheet` và `Update Recipes Sheet` được liên kết chính xác với Agent để AI có quyền đọc/ghi dữ liệu.
- **Command Router (Switch node):** Dùng để phân loại các lệnh hoặc câu lệnh từ người dùng gửi qua Telegram (Xem danh sách, tìm kiếm, trò chuyện với AI...).

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và thử nhắn tin cho Telegram Bot của các sếp (ví dụ: gõ lệnh xem danh sách món ăn hoặc nhờ AI gợi ý một món bất kỳ).
- Sau khi test thành công, bật công tắc **Active** ở góc trên bên phải để bot hoạt động tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
Để hệ thống xịn hơn nữa, các sếp có thể mở rộng workflow với các ý tưởng sau:
- **Tích hợp thêm OpenAI Whisper:** Cho phép gửi tin nhắn thoại (Voice message) vào Telegram để bot tự động nghe, chuyển thành văn bản và lưu công thức vào Google Sheets.
- **Gửi thông báo thực đơn hàng ngày:** Kết hợp thêm Cron Node để vào 8h sáng mỗi ngày, bot tự động nhắn tin gợi ý thực đơn cho cả ngày.
- **Lưu trữ hình ảnh món ăn:** Thêm tính năng nhận diện hình ảnh món ăn gửi qua Telegram, dùng AI phân tích và tự động lưu ảnh vào Google Drive.

### 📌 Kết luận
Một workflow cực kỳ thiết thực cho cuộc sống hằng ngày, vừa giúp quản lý kho tàng công thức nấu ăn khoa học vừa ứng dụng AI đỉnh cao. Chúc các sếp cài đặt thành công và có những trải nghiệm tuyệt vời cùng trợ lý bếp trưởng AI của mình!