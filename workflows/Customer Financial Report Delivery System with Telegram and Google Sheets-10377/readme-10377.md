---
title: "🚀 Xây dựng hệ thống báo cáo tài chính tự động qua Telegram và Google Sheets với n8n"
description: "Hướng dẫn chi tiết cách tự động hóa quy trình tra cứu và gửi báo cáo tài chính khách hàng từ Google Sheets qua Telegram bot hoàn toàn miễn phí."
slug: "he-thong-bao-cao-tai-chinh-telegram-google-sheets-n8n"
tags: [n8n, automation, telegram, google-sheets, chatbot, finance]
keywords: [n8n workflow, telegram bot google sheets, tu dong hoa bao cao tai chinh, no-code automation, quan ly tai chinh telegram]
---

# 🚀 Xây dựng hệ thống báo cáo tài chính tự động qua Telegram và Google Sheets

Các sếp có đang gặp tình trạng khách hàng hoặc đội ngũ kinh doanh liên tục nhắn tin hỏi số dư tài chính, công nợ, hay dữ liệu giao dịch thủ công mỗi ngày? Việc tra cứu file Excel/Google Sheets rồi copy paste trả lời từng người không chỉ tốn hàng giờ đồng hồ mà còn dễ nhầm lẫn, chậm trễ.

Giải pháp ở đây là gì? Hãy tự động hóa 100% quy trình này bằng một chiếc chatbot Telegram thông minh kết hợp với Google Sheets thông qua n8n! Workflow này sẽ giúp khách hàng tự tra cứu báo cáo tài chính ngay lập tức, đồng thời bảo mật tuyệt đối dữ liệu bằng cơ chế phân quyền thông minh.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 24/7:** Khách hàng tự tra cứu số liệu tài chính bất cứ lúc nào qua Telegram mà không cần nhân sự can thiệp.
- **Bảo mật phân quyền chặt chẽ:** Hệ thống tự động kiểm tra Chat ID của người dùng có khớp với quyền truy cập trong Google Sheets hay không trước khi trả dữ liệu.
- **Báo cáo trực quan:** Tự động tính toán tổng Debit (Nợ), Credit (Có), số dư (Balance) và định dạng báo cáo đẹp mắt kèm emoji sinh động.
- **Tiết kiệm thời gian:** Xử lý hàng trăm yêu cầu tra cứu cùng lúc, loại bỏ hoàn toàn sai sót do thủ công.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Telegram Bot Token** (Tạo qua [@BotFather](https://t.me/BotFather)).
- **Google Sheets** chứa dữ liệu khách hàng, giao dịch và bảng phân quyền (Access).
- **Credentials** kết nối Telegram API và Google Sheets OAuth2 trong n8n.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy đoạn mã JSON của workflow này và dán trực tiếp vào n8n Editor, hoặc import file JSON tải từ nguồn chính thức.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống chạy mượt mà, các sếp cần cấu hình chính xác các node sau:

- **Telegram Nodes (`Input user2`, `Send Report2`, `Wellcome1`, `Enter Correct name`, `No permission`):** 
  - Chọn đúng Credentials Telegram API đã tạo.
  - Đảm bảo Bot đã được Start và có quyền gửi/nhận tin nhắn.
- **Google Sheets Nodes (`Get row(s) in sheet (Access)2`, `Get row(s) in sheet5`, `Get row(s) in sheet4`):**
  - Kết nối tài khoản Google Sheets OAuth2.
  - Thay đổi `documentId` thành Link/ID file Google Sheet của các sếp.
  - Cập nhật đúng tên sheet/tab (ví dụ: `Access`, `Sheet1`, v.v.).
  - Cấu hình lại `lookupColumn` (cột tìm kiếm như *Customer name*, *Groups*) cho khớp với cấu trúc bảng dữ liệu thực tế.
- **Code Nodes (`Code`, `Code2`, `Check Match2`, `Aggregate Summary2`, `Format Details2`, `Combine Summary + Details2`):**
  - Các đoạn code xử lý logic đã được viết sẵn sàng, tuy nhiên cần kiểm tra lại tên các cột dữ liệu trong sheet (như `ChatID1`, `ChatID2`, `Groups`) để khớp với các biến trong code.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** và thử nhắn tin cho Bot Telegram với từ khóa `/start` hoặc gõ tên một khách hàng có sẵn trong sheet để test.
- Kiểm tra kết quả trả về trên Telegram. Nếu mọi thứ hoạt động trơn tru, hãy bật công tắc **Active** để đưa workflow vào vận hành chính thức.

### ✍️ Mẹo & gợi ý nâng cao
- **Lưu Log tra cứu:** Thêm một Google Sheets Append node vào cuối luồng thành công để ghi lại lịch sử ai đã tra cứu lúc mấy giờ.
- **Mở rộng thông báo:** Kết hợp thêm node Slack hoặc Telegram Channel để cảnh báo quản lý nếu có tài khoản lạ cố gắng truy cập trái phép.
- **Bổ sung Menu Button:** Sử dụng Telegram Inline Keyboard để người dùng bấm chọn thay vì phải gõ tên thủ công, tối ưu trải nghiệm người dùng (UX).

### 📌 Kết luận
Hệ thống báo cáo tài chính tự động qua Telegram và Google Sheets là một ứng dụng thực chiến cực kỳ mạnh mẽ giúp doanh nghiệp tối ưu hóa vận hành, chăm sóc khách hàng chuyên nghiệp và bảo mật thông tin tài chính tuyệt đối. Hãy triển khai ngay hôm nay để giải phóng thời gian cho đội ngũ của các sếp!