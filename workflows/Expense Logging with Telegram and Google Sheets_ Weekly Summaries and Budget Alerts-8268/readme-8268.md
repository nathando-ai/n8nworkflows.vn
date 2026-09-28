---
title: "🚀 Quản lý chi tiêu cá nhân qua Telegram và Google Sheets tự động hóa với n8n"
description: "Tự động ghi nhận chi tiêu hàng ngày từ Telegram vào Google Sheets, tổng kết tài chính hàng tuần và cảnh báo vượt ngân sách thông minh."
slug: "quan-ly-chi-tieu-telegram-google-sheets-n8n"
tags: [n8n, automation, telegram, google-sheets, personal-productivity]
keywords: [n8n workflow, quan ly chi tieu, telegram expense tracker, google sheets automation, tu dong hoa chi tieu]
---

# 🚀 Quản lý chi tiêu cá nhân qua Telegram và Google Sheets tự động hóa với n8n

Các sếp có bao giờ cảm thấy mệt mỏi khi cuối tháng nhìn lại ví và tự hỏi tiền đã bay đi đâu mất? Việc ghi chép thủ công từng ly cà phê, bữa trưa vào sổ tay hay ứng dụng nhớ nhớ quên quên khiến chúng ta rất dễ bỏ cuộc. 

Giải pháp hoàn hảo đây rồi! Workflow n8n này sẽ biến Telegram thành một trợ lý tài chính cá nhân siêu tốc. Các sếp chỉ cần nhắn tin nhanh cho bot, mọi thứ sẽ được tự động lưu vào Google Sheets, tính toán tổng kết hàng tuần và cảnh báo ngay lập tức nếu lỡ tay "vung tay quá trán". Hoàn toàn tự động 100% và không tốn một đồng phí code nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Ghi chép tức thì:** Nhập chi phí nhanh chóng qua cú pháp đơn giản ngay trên Telegram (ví dụ: `/spent 5 coffee`).
- **Lưu trữ khoa học:** Tự động đồng bộ hóa toàn bộ lịch sử chi tiêu vào Google Sheets theo thời gian thực.
- **Báo cáo tự động:** Nhận tổng kết chi tiêu hàng tuần vào Chủ Nhật hàng tuần mà không cần động tay.
- **Cảnh báo ngân sách thông minh:** Bot sẽ hú còi ngay lập tức khi tổng chi tiêu chạm hoặc vượt hạn mức (mặc định là €100).
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Telegram Bot Token** (Lấy từ BotFather).
- **Tài khoản Google** để kết nối Google Sheets (Google OAuth2 API).
- **File Google Sheets mẫu** (Đã có sẵn cấu trúc chuẩn).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy toàn bộ mã JSON của workflow này và dán trực tiếp vào n8n Editor của mình, hoặc import file JSON theo hướng dẫn của n8n.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống chạy mượt mà, các sếp cần cấu hình chính xác các node sau:

- **Telegram - Get Expense Command & TelegramTrigger:** 
  - Tạo một bot mới qua `@BotFather` trên Telegram để lấy API Token.
  - Tạo Credentials loại `telegramApi` và điền Token vào.
- **Google Sheets - Log Expense, Get Weekly Expenses, Get Expenses (Realtime), Clean Up:**
  - Chuẩn bị Google Sheet bằng cách [Make a copy of the template tại đây](https://docs.google.com/spreadsheets/d/1uyQpX9_ZZUhLtBhyxfjdU80D6Q6cqbMV286MnhF5QBY/edit?usp=sharing).
  - Kết nối tài khoản Google Sheets thông qua `googleSheetsOAuth2Api`.
  - Trỏ đúng Document ID và tên Sheet tương ứng trong từng node Google Sheets.
- **Check Weekly Budget (Node Code):**
  - Mở node này để cấu hình lại hạn mức ngân sách (`budget threshold`) theo ý muốn của các sếp (mặc định đang để là 100 đơn vị tiền tệ).

#### 3. Kích hoạt ⚡️
- Thử nghiệm gửi tin nhắn `/spent 50` vào bot Telegram của các sếp để test luồng chạy thực tế.
- Kiểm tra xem dữ liệu đã nhảy vào Google Sheets chưa.
- Sau khi mọi thứ chạy ngon nghẻ, bật công tắc **Active** xanh rờn cho workflow là xong!

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thêm thông báo:** Kết nối thêm node Slack hoặc Discord để thông báo chi tiêu nhóm nếu các sếp muốn quản lý quỹ chung.
- **Phân loại danh mục thông minh:** Nâng cấp node `Parse Telegram Message` kết hợp với OpenAI/LLM node để tự động phân loại chi phí (Ăn uống, Giải trí, Hóa đơn...) dựa trên nội dung tin nhắn.
- **Báo cáo hàng tháng:** Nhân bản `Weekly Summary Trigger` thành `Monthly Summary Trigger` để nhận báo cáo tài chính hoành tráng hơn vào ngày cuối tháng.

### 📌 Kết luận
Một workflow cực kỳ thiết thực giúp tối ưu hóa thói quen quản lý tài chính cá nhân mà không tốn chút sức lực thủ công nào. Hãy cài đặt ngay hôm nay để làm chủ dòng tiền của mình các sếp nhé!