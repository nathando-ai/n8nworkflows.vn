---
title: "🚀 Tự động giám sát hồ sơ bất động sản Lis Pendens qua Telegram, BrowserAct và Gemini"
description: "Hướng dẫn xây dựng hệ thống tự động quét hồ sơ pháp lý bất động sản Lis Pendens từ cổng thông tin công cộng, phân tích bằng AI và gửi cảnh báo trực tiếp về Telegram."
slug: "tu-dong-giam-sat-ho-so-bat-dong-san-lis-pendens-telegram-browseract-gemini"
tags: [n8n, automation, no-code, real-estate, telegram, ai-agent]
keywords: [n8n workflow, giám sát bất động sản, Lis Pendens, BrowserAct, Google Gemini, Telegram bot tự động hóa]
---

# 🚀 Tự động giám sát hồ sơ bất động sản Lis Pendens qua Telegram, BrowserAct và Gemini

Việc theo dõi các hồ sơ pháp lý bất động sản công khai (đặc biệt là các đơn kiện tranh chấp quyền sở hữu - *Lis Pendens*) theo cách thủ công là một cơn ác mộng thực sự đối với các nhà đầu tư và môi giới. Các sếp thường phải mất hàng giờ lướt qua các cổng thông tin công cộng chậm chạp, lọc dữ liệu thủ công trước khi có thể tìm thấy cơ hội đầu tư tiềm năng. 

Giải pháp? Workflow n8n này sẽ tự động hóa 100% quy trình từ việc nhận lệnh qua Telegram, cào dữ liệu web tự động bằng **BrowserAct**, phân tích thông tin bằng AI (**Google Gemini** & **OpenRouter GPT-4**) và trả kết quả gọn gàng ngay trên điện thoại của các sếp!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn:** Nhận dữ liệu hồ sơ mới nhất chỉ bằng một tin nhắn chat trên Telegram mà không cần mở trình duyệt.
- **Xử lý thông minh bằng AI:** Phân loại ý định người dùng (chat thông thường hay yêu cầu dữ liệu) và cấu trúc hóa dữ liệu thô thành các báo cáo dễ đọc.
- **Chống tràn giới hạn (Rate Limits):** Tích hợp cơ chế chờ thông minh (`Wait`) và chia nhỏ dữ liệu (`Split Out`) để gửi tin nhắn Telegram an toàn, không sợ bị chặn API.
- **Hoạt động 24/7:** Chạy ngầm liên tục, tự động tính toán khoảng thời gian (ví dụ: quét dữ liệu trong 5 ngày gần nhất) để đảm bảo không bỏ lỡ bất kỳ cơ hội nào.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản và API sau:
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Telegram Bot Token** (tạo qua BotFather).
- **BrowserAct API** (kèm theo template mẫu **Texas Foreclosure Leads**).
- **Google Gemini API Key** (Google Palm API).
- **OpenRouter API Key** (dùng cho mô hình OpenAI GPT-4.1).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy toàn bộ mã JSON của workflow và dán trực tiếp vào giao diện n8n Editor của mình, hoặc sử dụng tính năng import file JSON.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 23 nodes phối hợp nhịp nhàng. Các sếp cần chú ý cấu hình kỹ các node sau:
- **User Sends Message to Bot & Send Alert / Answer the User / Send Lead Data to Telegram:** Kết nối các node Telegram này với **Telegram API Credentials** của bot do các sếp quản lý.
- **Google Gemini:** Thiết lập **Google Palm API Credentials** để AI hỗ trợ xử lý ngôn ngữ.
- **OpenRouter Model & OpenRouter Model1:** Nhập **OpenRouter API Credentials** và đảm bảo chọn đúng model `openai/gpt-4.1` theo cấu hình gốc.
- **Extract Lis Pendens Data (BrowserAct):** Cấu hình **BrowserAct API Credentials** và trỏ tới template mẫu **Texas Foreclosure Leads** đã được lưu trong tài khoản BrowserAct của các sếp.
- **Calculate "From_Date" & Format Date nodes:** Kiểm tra lại logic tính toán thời gian (mặc định lấy dữ liệu trong khoảng 5 ngày gần nhất) để đảm bảo phù hợp với múi giờ của trang web mục tiêu.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và gửi một tin nhắn test (ví dụ: *"Get recent filings"*) tới Telegram bot của các sếp để kiểm tra luồng chạy.
- Sau khi test thành công, gạt công tắc sang chế độ **Active** để bot chính thức hoạt động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Lưu trữ dữ liệu:** Thêm node **Google Sheets** hoặc **Airtable** ngay sau bước phân tích dữ liệu để lưu trữ toàn bộ lịch sử lead, phục vụ cho việcRemarketing hoặc chăm sóc sau này.
- **Mở rộng kênh nhận tin:** Ngoài Telegram, các sếp có thể clone nhánh gửi tin nhắn sang **Slack** hoặc **Discord** nếu team làm việc trên các nền tảng đó.
- **Tùy chỉnh khoảng thời gian quét:** Thay vì cố định 5 ngày, các sếp có thể yêu cầu AI bóc tách thời gian linh hoạt hơn dựa trên câu lệnh người dùng nhập vào (ví dụ: *"Quét hồ sơ tuần trước"*).

### 📌 Kết luận
Với sự kết hợp hoàn hảo giữa n8n, BrowserAct và sức mạnh phân tích từ Gemini/GPT-4, các sếp đã có trong tay một hệ thống săn lead bất động sản tự động cực kỳ mạnh mẽ. Hãy triển khai ngay hôm nay để đi trước đối thủ một bước!