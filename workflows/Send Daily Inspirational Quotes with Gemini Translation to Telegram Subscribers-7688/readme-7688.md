---
title: "🚀 Tự động gửi câu nói truyền cảm hứng hàng ngày qua Telegram tích hợp Google Gemini AI"
description: "Hướng dẫn xây dựng workflow n8n tự động lấy câu nói hay, dịch thuật thông minh bằng Google Gemini và gửi đến danh sách người đăng ký trên Telegram mỗi ngày."
slug: "tu-dong-gui-cau-noi-truyen-cam-hung-telegram-gemini"
tags: [n8n, automation, no-code, telegram, google-gemini, google-sheets, ai]
keywords: [n8n workflow, telegram bot, google gemini ai, tu dong hoa telegram, zenquotes api, quan ly subscriber telegram]
---

# 🚀 Tự động gửi câu nói truyền cảm hứng hàng ngày qua Telegram tích hợp Google Gemini AI

Các sếp có muốn bắt đầu ngày mới bằng việc gửi những câu nói truyền cảm hứng (inspirational quotes) đến cộng đồng hoặc nhóm khách hàng trên Telegram một cách tự động hoàn toàn không? Việc làm này thủ công mỗi ngày vừa tốn thời gian, lại dễ quên. 

Giải pháp tuyệt vời cho các sếp đây: Workflow n8n tự động hóa 100% giúp lấy câu nói ngẫu nhiên từ API, sử dụng sức mạnh của **Google Gemini AI** để dịch thuật, trang trí thêm emoji bắt mắt và gửi đồng loạt đến danh sách người đăng ký. Đồng thời, hệ thống còn tự động lưu trữ thông tin người dùng mới nhắn tin cho bot vào Google Sheets. Không cần biết code, chỉ cần setup một lần là chạy mãi mãi!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn 24/7:** Bot tự động lấy quote và gửi đi đúng giờ hẹn hàng ngày mà không cần chạm tay vào.
- **AI thông minh & Cá nhân hóa:** Nhờ Google Gemini, các câu nói được dịch mượt mà sang ngôn ngữ mong muốn và được chèn thêm các emoji sinh động, thu hút người đọc.
- **Quản lý Subscriber tự động:** Bất kỳ ai nhắn tin cho bot đều được tự động ghi nhận và lưu User ID vào Google Sheets để chuẩn bị nhận tin nhắn hàng ngày.
- **Mở rộng dễ dàng:** Dễ dàng thay đổi nguồn dữ liệu quote hoặc mở rộng kênh phân phối (thêm Slack, Discord, v.v.).
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Self-hosted hoặc Cloud).
- **Telegram Bot Token:** Tạo bot mới qua [@BotFather](https://t.me/BotFather) trên Telegram.
- **Google Gemini API Key:** Lấy key từ Google AI Studio để phục vụ cho node AI.
- **Google Sheets:** Tạo sẵn một file Google Sheets để lưu trữ danh sách người đăng ký (Subscriber ID).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy toàn bộ mã JSON của workflow này, sau đó vào giao diện n8n, chọn **Add workflow** -> Nhấn tổ hợp `Ctrl + V` (hoặc `Cmd + V`) để dán trực tiếp vào Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình chính xác các node sau:

- **Schedule Trigger:** Cài đặt mốc thời gian cụ thể trong ngày (ví dụ: 8:00 sáng mỗi ngày) để kích hoạt luồng gửi tin nhắn tự động.
- **HTTP Request:** Node này có nhiệm vụ gọi API từ ZenQuotes (`https://zenquotes.io/api/random`) để lấy câu nói ngẫu nhiên. Các sếp giữ nguyên cấu hình nếu sử dụng nguồn này.
- **Basic LLM Chain & Google Gemini Chat Model:** 
  - Kết nối Credentials với **Google Palm/Gemini API Key**.
  - Thiết lập Prompt để hướng dẫn Gemini dịch câu nói sang ngôn ngữ mục tiêu (ví dụ: tiếng Việt) và trang trí thêm emoji phù hợp, tạo cảm giác thân thiện, truyền động lực.
- **Set Language:** Node này dùng để cấu hình ngôn ngữ đầu ra mà các sếp muốn bot dịch sang.
- **Google Sheets & Google Sheets1:** 
  - Cấu hình kết nối tài khoản Google (OAuth2).
  - Trỏ đến file Google Sheets lưu danh sách subscriber. Một node dùng để **ghi lại User ID** khi có người dùng mới tương tác với bot (`Telegram Trigger`), và một node dùng để **đọc danh sách** người dùng khi đến giờ gửi tin nhắn định kỳ.
- **Telegram & Send a text message:**
  - Kết nối Credentials với **Telegram Bot Token** lấy từ `@BotFather`.
  - Thiết lập chat ID đích cho luồng gửi hàng ngày (hoặc loop qua danh sách từ Google Sheets để gửi cho từng subscriber).

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** để test thử nghiệm luồng lấy quote và dịch thuật xem kết quả trả về đã ưng ý chưa.
- Kiểm tra tính năng đăng ký bằng cách chat thử với Bot trên Telegram.
- Khi mọi thứ đã chạy trơn tru, hãy gạt công tắc **Active** ở góc trên cùng bên phải để bật chế độ tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Thêm tính năng gửi log/báo cáo:** Gắn thêm một node Telegram hoặc Slack để gửi thông báo về cho Admin mỗi khi bot hoàn tất việc gửi quote hàng ngày.
- **Đa dạng nguồn dữ liệu:** Thay vì chỉ lấy từ ZenQuotes API, các sếp có thể tạo một Google Sheets chứa hàng trăm câu quote tự soạn và cho n8n bốc thăm ngẫu nhiên mỗi ngày.
- **Tương tác 2 chiều:** Nâng cấp bot Telegram thành trợ lý AI trò chuyện cùng người dùng dựa trên nền tảng Gemini LangChain có sẵn trong workflow.

### 📌 Kết luận
Workflow này là một mảnh ghép hoàn vời cho những ai đang xây dựng kênh nội dung tự động, chăm sóc khách hàng hoặc tạo một góc truyền cảm hứng cho riêng mình trên Telegram. Hãy tranh thủ "lên đồ" ngay hôm nay để tối ưu hóa thời gian cho bản thân nhé các sếp!