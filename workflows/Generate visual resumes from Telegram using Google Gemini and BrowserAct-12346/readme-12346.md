---
title: "🚀 Tạo CV trực quan siêu đẹp từ Telegram với Google Gemini và BrowserAct tự động"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa quy trình tạo CV trực quan chuyên nghiệp trực tiếp từ Telegram sử dụng Google Gemini AI và BrowserAct."
slug: "tao-cv-truc-quan-tu-telegram-voi-google-gemini-va-browseract"
tags: [n8n, automation, telegram, google-gemini, ai, browseract, hr]
keywords: [n8n workflow, tao cv tu dong, telegram bot ai, google gemini cv, browseract n8n, tu dong hoa hr]
---

# 🚀 Tạo CV trực quan siêu đẹp từ Telegram với Google Gemini và BrowserAct tự động

Việc tạo ra một bản CV chuyên nghiệp, bắt mắt thường ngốn rất nhiều thời gian chỉnh sửa định dạng, căn chỉnh bố cục trên các công cụ thiết kế. Nếu các sếp đang tìm kiếm một giải pháp tự động hóa toàn diện giúp ứng viên chỉ cần gửi thông tin qua **Telegram**, sau đó hệ thống tự động phân tích bằng AI (**Google Gemini**) và xuất ra một bản CV trực quan đỉnh cao nhờ **BrowserAct**, thì đây chính là workflow sinh ra dành riêng cho các sếp. 

Workflow này giúp loại bỏ hoàn toàn các bước thủ công, biến việc tạo CV trở thành một trải nghiệm mượt mà và hiện đại 100% không cần code!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Tiếp nhận thông tin từ Telegram, xử lý bằng AI và trả kết quả mà không cần sự can thiệp thủ công.
- **AI thông minh:** Google Gemini hỗ trợ trích xuất, cấu trúc hóa và viết nội dung CV chuyên nghiệp, thu hút nhà tuyển dụng.
- **Trực quan hóa đỉnh cao:** Kết hợp BrowserAct và các công cụ xử lý tệp tin (như CloudConvert) để render CV thành dạng hình ảnh hoặc tài liệu đẹp mắt.
- **Trải nghiệm người dùng mượt mà:** Ứng viên hoặc nhân sự chỉ cần chat qua Telegram là có ngay CV hoàn chỉnh để sử dụng.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Khuyên dùng Self-hosted trên VPS).
- **Telegram Bot:** Tạo một Bot qua `@BotFather` để lấy Token và cấu hình Trigger.
- **Google Gemini API Key:** Tài khoản Google AI Studio để kết nối mô hình ngôn ngữ lớn Gemini.
- **Google Sheets / BrowserAct / CloudConvert:** Tài khoản và API tương ứng cho các dịch vụ lưu trữ dữ liệu, render trang web và chuyển đổi định dạng.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow này từ kho lưu trữ n8n.
- Trong giao diện n8n Editor, nhấn vào menu **Add workflow** -> Chọn **Import from File** và tải file JSON lên, hoặc copy toàn bộ mã nguồn JSON và paste trực tiếp vào giao diện n8n.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Khi đã đưa workflow lên sàn n8n, các sếp cần chú ý cấu hình kỹ các node trọng điểm sau:
- **Telegram Trigger & Telegram Nodes:** Nhập Telegram Bot Token đã tạo từ `@BotFather` để bot có thể lắng nghe tin nhắn từ người dùng và gửi trả file CV hoàn thành.
- **Google Gemini / LM Chat Google Gemini Nodes:** Cung cấp Google Gemini API Key và thiết lập `Output Parser Structured` để đảm bảo AI trả về đúng cấu trúc dữ liệu cần thiết cho CV.
- **Google Sheets Node:** Kết nối tài khoản Google, chỉ định file Sheet dùng để lưu trữ thông tin ứng viên hoặc log lại lịch sử tạo CV (nếu cần).
- **BrowserAct Node:** Cấu hình thông số kết nối dịch vụ BrowserAct để thực hiện thao tác chụp ảnh/render trang web thành CV trực quan.
- **CloudConvert Node:** Cấu hình API Key để hỗ trợ chuyển đổi định dạng file đầu ra (ví dụ: HTML sang PDF hoặc PNG).
- Các node phụ trợ như `Code`, `Switch`, `Split In Batches`, `Aggregate`: Kiểm tra lại logic nhánh điều kiện để đảm bảo luồng dữ liệu không bị nghẽn.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và gửi một tin nhắn mẫu qua Telegram Bot để test thử nghiệm toàn bộ luồng xử lý.
- Kiểm tra kết quả trả về trên Telegram. Nếu mọi thứ đã mượt mà, hãy gạt công tắc sang **Active** để đưa bot vào hoạt động chính thức 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thêm CRM hoặc Notion:** Lưu trữ thông tin chi tiết của ứng viên vào Notion hoặc hệ thống CRM nội bộ ngay sau khi tạo CV thành công.
- **Thông báo qua Slack/Telegram Admin:** Thiết lập một nhánh gửi thông báo về nhóm nội bộ công ty mỗi khi có một ứng viên mới hoàn tất việc tạo CV.
- **Đa dạng hóa mẫu CV:** Sử dụng node `Switch` để cho phép người dùng Telegram lựa chọn các mẫu giao diện (template) CV khác nhau trước khi tiến hành render.

### 📌 Kết luận
Workflow tích hợp Telegram, Google Gemini và BrowserAct là một giải pháp tự động hóa cực kỳ mạnh mẽ giúp tối ưu hóa quy trình làm việc, tiết kiệm thời gian thiết kế và mang lại trải nghiệm ấn tượng cho người dùng. Hãy triển khai ngay hôm nay để nâng tầm hệ thống tự động hóa của các sếp!