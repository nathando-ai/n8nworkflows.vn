---
title: "🚀 Tự động tóm tắt Gmail quan trọng và gửi qua Telegram bằng AI GPT-4o-mini"
description: "Hướng dẫn cài đặt workflow n8n tự động giám sát Gmail hàng phút, lọc từ khóa thông minh, tóm tắt nội dung bằng AI GPT-4o-mini và gửi thông báo trực tiếp về Telegram."
slug: "tu-dong-tom-tat-gmail-gui-telegram-gpt-4o-mini"
tags: [n8n, automation, gmail, telegram, openai, ai-summarization]
keywords: [n8n workflow, tu dong hoa gmail, telegram bot ai, gpt-4o-mini, tom tat email tu dong]
---

# 🚀 Tự động tóm tắt Gmail quan trọng và gửi qua Telegram bằng AI GPT-4o-mini

Các sếp có bao giờ cảm thấy ngợp thở vì một ngày nhận hàng chục, thậm chí hàng trăm email rác, email thông báo linh tinh nhưng lại sợ bỏ lỡ những tin nhắn cực kỳ quan trọng như hóa đơn thanh toán, thông báo bảo mật hay cập nhật đơn hàng? Việc mở từng email ra đọc trên điện thoại đôi khi cực kỳ tốn thời gian.

Giải pháp ở đây là gì? Hãy để hệ thống tự động hóa làm thay các sếp! Workflow n8n này sẽ liên tục giám sát hộp thư Gmail của các sếp, tự động lọc ra các email chứa từ khóa quan trọng, nhờ AI **GPT-4o-mini** tóm tắt lại siêu ngắn gọn và bắn thẳng thông báo về **Telegram** ngay lập tức. 100% không cần code!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Không bỏ lỡ tin quan trọng:** Nhận thông báo ngay lập tức trên Telegram ngay khi email vừa đến.
- **Tiết kiệm 90% thời gian:** Không cần đọc nguyên văn email dài dòng, AI đã chắt lọc sẵn các ý chính (dưới 300 ký tự, kèm emoji sinh động).
- **Lọc thông minh:** Tùy chỉnh linh hoạt các từ khóa theo nhu cầu cá nhân (hóa đơn, bảo mật, đơn hàng, công việc...).
- **Hoạt động 24/7:** Chạy ngầm liên tục mà không cần can thiệp thủ công.
:::

### Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Tài khoản Gmail** (để cấu hình `Gmail Trigger`).
- **OpenAI API Key** (Sử dụng model `gpt-4o-mini` cực kỳ tiết kiệm chi phí).
- **Telegram Bot** và **Chat ID** (để nhận tin nhắn thông báo).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tạo một workflow mới trên n8n, sau đó copy toàn bộ JSON của template này (hoặc import file JSON) vào n8n Editor. Workflow bao gồm 6 nodes chính:
- `Check for New Emails` (Gmail Trigger)
- `Important Email Filter` (IF Node)
- ` Ignore Unimportant Email` (NoOp Node)
- `OpenAI Chat Model` (LM Chat OpenAI)
- `Summarize Email with GPT-4o` (AI Agent)
- `Send Summary to Telegram` (Telegram Node)

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình chính xác các node sau:

- **Check for New Emails (Gmail Trigger):**
  - Kết nối tài khoản Gmail của các sếp thông qua `Gmail OAuth2`.
  - Node này sẽ mặc định quét hộp thư đến mỗi phút một lần.
- **Important Email Filter (IF Node):**
  - Thiết lập điều kiện lọc từ khóa (Keywords) dựa trên tiêu đề (Subject) hoặc nội dung email.
  - Các từ khóa mặc định có thể dùng: `"Sales"`, `"invoice"`, `"payment due"`, `"security alert"`, `"job offer"`, `"delivery"`. Các sếp hãy thay đổi thành các từ khóa phù hợp với công việc cá nhân.
- **OpenAI Chat Model & Summarize Email with GPT-4o (AI Agent):**
  - Thêm Credentials cho OpenAI (`openAiApi`).
  - Đảm bảo model được chọn là `gpt-4o-mini`. AI Agent đã được thiết lập sẵn System Prompt để trả về bản tóm tắt thân thiện, ngắn gọn dưới 300 ký tự kèm emoji.
- **Send Summary to Telegram (Telegram Node):**
  - Kết nối `Telegram API` bằng cách nhập Token của Telegram Bot do `@BotFather` cung cấp.
  - Điền `Chat ID` của cá nhân hoặc nhóm chat Telegram nơi các sếp muốn nhận thông báo.

#### 3. Kích hoạt ⚡️
- Bấm nút **Test step** hoặc **Execute Workflow** để thử gửi một email mẫu và kiểm tra kết quả trên Telegram.
- Nếu mọi thứ hoạt động trơn tru, hãy gạt công tắc sang trạng thái **Active** để hệ thống tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Đa kênh thông báo:** Ngoài Telegram, các sếp có thể nối thêm node Slack, Discord hoặc Zalo ZNS để nhận thông báo ở nhiều nơi cùng lúc.
- **Lưu lịch sử:** Kết nối thêm node Google Sheets để lưu trữ lại danh sách các email quan trọng đã được tóm tắt phục vụ việc tra cứu sau này.
- **Mở rộng từ khóa chuyên ngành:** Thêm các từ khóa liên quan đến tên dự án, tên khách hàng lớn hoặc mã đơn hàng riêng của doanh nghiệp.

### 📌 Kết luận
Với workflow n8n cực kỳ tinh gọn này, việc quản lý email hằng ngày sẽ trở nên nhẹ nhàng hơn bao giờ hết. Không còn cảnh "bơi" trong biển email, mọi thông tin quan trọng đều được tổng hợp gọn gàng ngay trên chiếc điện thoại qua Telegram. Chúc các sếp cài đặt thành công và "lên đồ" tự động hóa thành công!