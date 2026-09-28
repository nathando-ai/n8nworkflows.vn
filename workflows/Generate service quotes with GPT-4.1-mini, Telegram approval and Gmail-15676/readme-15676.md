---
title: "🚀 Tự động hóa tạo báo giá dịch vụ với GPT-4.1-mini, Phê duyệt qua Telegram & Gửi Email tự động"
description: "Xây dựng hệ thống tự động hóa tiếp nhận yêu cầu từ Tally Form/Webhook, phân loại thông minh bằng AI, duyệt báo giá qua Telegram và gửi PDF cho khách hàng qua Gmail."
slug: "tu-dong-hoa-tao-bao-gia-dich-vu-ai-telegram-gmail"
tags: [n8n, automation, ai, openai, telegram, gmail, pdfmonkey, tally]
keywords: [n8n workflow, tạo báo giá tự động, openai gpt-4, telegram approval, pdfmonkey, tự động hóa dịch vụ]
---

# 🚀 Tự động hóa tạo báo giá dịch vụ với AI, Telegram và Gmail

Các doanh nghiệp dịch vụ (như thi công, sửa chữa, vệ sinh công nghiệp, điện nước, quản lý tòa nhà) thường mất rất nhiều thời gian thủ công để tiếp nhận yêu cầu, tính toán, soạn thảo báo giá dưới dạng PDF rồi gửi cho khách hàng. Vừa chậm trễ, vừa dễ sai sót.

Workflow n8n này sẽ giải quyết triệt để vấn đề đó bằng cách tự động hóa 100% quy trình từ khâu tiếp nhận, sử dụng AI phân loại yêu cầu, tự động tạo file PDF, gửi yêu cầu phê duyệt qua Telegram cho sếp duyệt trước khi tự động gửi email cho khách hàng. Không cần viết code, tối ưu thời gian và giữ vững quyền kiểm soát!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tốc độ phản hồi tức thì**: Khách hàng vừa điền form hoặc gọi điện là hệ thống xử lý ngay lập tức.
- **AI thông minh phân loại**: Tự động phân chia yêu cầu thành báo giá nhà đơn (EFH), nhà nhiều hộ (MFH), sự cố khẩn cấp, lịch hẹn khảo sát...
- **Kiểm soát tuyệt đối**: Sử dụng tính năng `sendAndWait` của Telegram, sếp có thể bấm Duyệt hoặc Từ chối báo giá trực tiếp trên điện thoại trước khi gửi đi.
- **Hoạt động 24/7 không mệt mỏi**: Thay thế hoàn toàn các tác vụ hành chính lặp đi lặp lại.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để vận hành trơn tru, các sếp cần chuẩn bị sẵn các tài khoản và API Keys sau:
- Tài khoản **n8n** (Self-hosted hoặc Cloud).
- Tài khoản **OpenAI** (để sử dụng GPT-4.1-mini hoặc model tương đương).
- Tài khoản **Tally.so** (tạo form thu thập thông tin khách hàng).
- **Telegram Bot Token** và Chat ID (tạo qua `@BotFather`).
- Tài khoản **Gmail** (cấu hình OAuth2 để gửi email).
- Tài khoản **PDFMonkey** (với 2 template báo giá cho EFH và MFH).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy toàn bộ mã JSON của workflow này và paste trực tiếp vào n8n Editor, hoặc import file JSON tải từ nguồn gốc.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, các sếp cần cấu hình các node quan trọng sau:
- **Tally Trigger: New Form Submission**: Kết nối credentials Tally API và thay thế `YOUR_TALLY_FORM_ID` bằng Form ID của các sếp. Map các trường dữ liệu như tên, email, diện tích, loại dịch vụ...
- **Classify Request with GPT-4.1-mini**: Kết nối credentials OpenAI, kiểm tra lại prompt phân loại nếu muốn thay đổi các nhóm dịch vụ của doanh nghiệp mình.
- **Webhook: Alternative Intake**: (Tùy chọn) Nếu các sếp dùng AI Voice Agent hoặc hệ thống khác gọi vào, hãy cấu hình đường dẫn Webhook tại đây.
- **Telegram Nodes** (`Telegram: Approval Request EFH`, `MFH` và các node thông báo): Thay thế toàn bộ `YOUR_TELEGRAM_CHAT_ID` bằng Chat ID thật của quản lý hoặc nhóm quản lý trên Telegram. Lưu ý các node phê duyệt sử dụng operation `sendAndWait`.
- **PDFMonkey Nodes**: Kết nối API Key, tạo 2 template trên PDFMonkey và thay thế ID vào `YOUR_PDFMONKEY_TEMPLATE_ID_EFH` và `_MFH`.
- **Gmail Nodes**: Kết nối credentials Gmail OAuth2 và thay thế email gửi đi bằng email doanh nghiệp của các sếp.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (Test run) bằng cách gửi một form mẫu từ Tally.
- Kiểm tra các nhánh Switch, AI phân loại, Telegram gửi tin nhắn và PDF được tạo.
- Bật công tắc **Active** để workflow chính thức chạy tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo**: Có thể bổ sung node Slack hoặc Microsoft Teams bên cạnh Telegram để đội ngũ sales cùng theo dõi.
- **Lưu trữ dữ liệu**: Thêm node Google Sheets hoặc Airtable ngay sau bước nhận form để lưu lại toàn bộ lịch sử khách hàng phục vụ cho việc marketing sau này.
- **Tự động hóa toàn phần**: Đối với các yêu cầu giá trị nhỏ, các sếp có thể bỏ qua bước chờ duyệt trên Telegram để hệ thống tự động gửi báo giá 100%.

### 📌 Kết luận
Workflow "Generate service quotes with GPT-4.1-mini, Telegram approval and Gmail" là một giải pháp tự động hóa mẫu mực giúp các doanh nghiệp dịch vụ tối ưu hóa quy trình bán hàng và chăm sóc khách hàng. Hãy triển khai ngay hôm nay để tiết kiệm hàng chục giờ làm việc thủ công mỗi tuần!