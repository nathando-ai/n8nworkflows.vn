---
title: "🚀 Tự động hóa săn việc làm mỗi ngày từ JSearch lên Google Sheets và Telegram với n8n"
description: "Hướng dẫn cài đặt workflow n8n tự động tìm kiếm việc làm hàng ngày từ JSearch API, lọc trùng lặp, lưu vào Google Sheets và gửi báo cáo tổng hợp qua Telegram."
slug: "tu-dong-hoa-san-viec-lam-jsearch-google-sheets-telegram"
tags: [n8n, automation, no-code, jsearch, google-sheets, telegram, hr]
keywords: [n8n workflow, tự động hóa tìm việc, JSearch API, Google Sheets, Telegram bot, quản lý tuyển dụng]
---

# 🚀 Tự động hóa săn việc làm mỗi ngày từ JSearch lên Google Sheets và Telegram

Các sếp có đang tốn hàng giờ mỗi ngày để lên các trang tuyển dụng tìm kiếm việc làm, copy thông tin thủ công vào bảng Excel rồi gửi báo cáo cho team không? Công việc lặp đi lặp lại này vừa nhàm chán, tốn thời gian lại rất dễ bỏ sót các cơ hội việc làm mới.

Đừng lo! Workflow n8n siêu việt này sẽ thay các sếp làm tất cả từ A-Z: tự động quét việc làm từ JSearch API, lọc bỏ các job đã tồn tại, lưu trữ gọn gàng vào Google Sheets và bắn thông báo báo cáo trực quan qua Telegram mỗi ngày. Hoàn toàn tự động, 0% công sức thủ công!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 mà không lo gián đoạn, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động 100%:** Chạy định kỳ hàng ngày, không cần can thiệp thủ công.
- **Không trùng lặp:** Hệ thống tự đối chiếu với Google Sheets hiện tại, chỉ thêm các job hoàn toàn mới.
- **Kiểm soát thông minh:** Có cơ chế Delay thông minh tránh vượt quá giới hạn (Rate limit) của Google API.
- **Báo cáo tức thì:** Nhận ngay tổng số lượng job mới và link truy cập trực tiếp qua Telegram Bot.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **RapidAPI Account:** Để lấy API Key kết nối với **JSearch API**.
- **Google Account:** Tài khoản Google Sheets để lưu trữ dữ liệu.
- **Telegram Bot:** Một Telegram Bot Token và Chat ID để nhận thông báo.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy đoạn mã JSON của workflow (từ nguồn cung cấp) và paste trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 14 nodes được chia thành 3 phần chính. Các sếp cần cấu hình kỹ các điểm sau:

- **Node `Set Search Parameters` & `Build Search Query`:**
  - Điền từ khóa tìm kiếm việc làm mong muốn thay thế cho placeholder `[YOUR_JOB_NAME_HERE]` (ví dụ: "Nodejs Developer", "Product Manager",...).
- **Node `Fetch Jobs from JSearch API`:**
  - Cấu hình Credentials loại `httpHeaderAuth` với RapidAPI Key của các sếp.
- **Node `Load Existing Job IDs` & `Save Job to Google Sheet`:**
  - Kết nối Credentials `googleSheetsOAuth2Api`.
  - Chuẩn bị sẵn một Google Sheet với các tiêu đề cột chuẩn: `Status`, `ID`, `Job Title`, `Company Name`, `Apply Link`, `Company Website`, `Source`, `Type`, `Direct Apply`, `Remote`, `Date Posted (UTC)`, `Fetched At`, `Location`, `Google Link`, `Salary`, `Minimum`, `Maximum`.
  - Thay thế `[YOUR_GOOGLE_SHEET_HERE]` bằng Document ID và tên Sheet chính xác của các sếp.
- **Node `Send Telegram Report`:**
  - Cấu hình Credentials loại `telegramApi` với Bot Token.
  - Điền Chat ID của các sếp vào trường `[YOUR_CHAT_ID_HERE]`.

#### 3. Kích hoạt ⚡️
- Bấm nút **Execute Workflow** để chạy thử nghiệm và kiểm tra dữ liệu đổ về Google Sheets cũng như tin nhắn Telegram.
- Nếu mọi thứ hoạt động mượt mà, hãy gạt công tắc sang **Active** để workflow tự động chạy theo lịch hẹn (Mặc định: 22:00 hàng ngày tại node `Run Daily at 22:00`).

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh nhận tin:** Kết hợp thêm node Slack hoặc Discord để bắn thông báo tuyển dụng vào group chung của team HR hoặc team Sales.
- **Tích hợp AI lọc CV/Job:** Thêm một node OpenAI hoặc Anthropic Claude để phân tích độ phù hợp của Job Description trước khi lưu vào sheet.
- **Lưu log lỗi:** Thêm nhánh Error Trigger để gửi cảnh báo về Telegram nếu JSearch API lỗi hoặc hết hạn ngạch.

### 📌 Kết luận
Workflow này là một "vũ khí" cực mạnh cho các nhà tuyển dụng, headhunter hoặc các lập trình viên đang muốn tự động hóa quá trình tìm kiếm cơ hội việc làm mỗi ngày. Hãy cài đặt ngay hôm nay để tối ưu hóa thời gian của mình các sếp nhé!