---
title: "🚀 Tự động hóa xử lý hóa đơn đầu vào: Email tới PostgreSQL với GPT-4o và Discord Alerts"
description: "Hướng dẫn xây dựng workflow n8n tự động trích xuất hóa đơn PDF từ Email, dùng GPT-4o bóc tách dữ liệu chuẩn hóa, lưu vào PostgreSQL và thông báo qua Discord."
slug: "tu-dong-hoa-xu-ly-hoa-don-email-postgres-gpt-4o"
tags: [n8n, automation, no-code, ai-extraction, postgresql, discord, invoice-processing]
keywords: [n8n workflow, xử lý hóa đơn tự động, trích xuất hóa đơn PDF, gpt-4o invoice, n8n postgresql discord]
---

# 🚀 Tự động hóa xử lý hóa đơn đầu vào: Email tới PostgreSQL với GPT-4o & Discord

Các sếp có đang mệt mỏi với việc mỗi ngày phải tải hàng chục file PDF hóa đơn từ email, đọc thủ công từng con số (tên công ty, mã số thuế, tổng tiền, ngày tháng), rồi cặm cụi nhập liệu vào database hoặc file Excel không? Công việc nhàm chán này không chỉ ngốn hàng giờ đồng hồ mà còn dễ dẫn đến sai sót số liệu tài chính.

Đừng lo nữa! Bài viết này sẽ hướng dẫn các sếp triển khai một workflow n8n siêu cấp VIP pro do **Halfbit** phát triển. Hệ thống này sẽ **tự động 100%**: lắng nghe email đến, đọc file PDF hóa đơn, nhờ AI (GPT-4o) trích xuất cấu trúc dữ liệu, kiểm tra và lưu trữ thông minh vào cơ sở dữ liệu PostgreSQL, đồng thời bắn thông báo tức thì lên Discord để đội ngũ nắm bắt.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn luồng Invoice:** Từ lúc hóa đơn chui vào inbox đến khi nằm gọn trong database mà không cần một cú click chuột thủ công nào.
- **Độ chính xác cao nhờ AI:** Sử dụng GPT-4o-mini / GPT-4o kết hợp *Structured Output Parser* giúp bóc tách đúng chuẩn các trường thông tin dù layout hóa đơn có thay đổi.
- **Quản lý nhà cung cấp thông minh:** Tự động kiểm tra xem công ty/nhà cung cấp đã tồn tại trong PostgreSQL chưa; nếu chưa, tự động tạo mới, tránh trùng lặp dữ liệu.
- **Cảnh báo tức thì:** Nhận thông báo tóm tắt hóa đơn ngay lập tức qua kênh Discord để kế toán hoặc quản lý dễ dàng theo dõi.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Tài khoản Email (IMAP):** Thông tin kết nối IMAP (Host, Port, User, Password) để đọc email chứa hóa đơn.
- **OpenAI API Key:** Tài khoản OpenAI có bật quyền gọi model GPT-4o hoặc GPT-4o-mini.
- **PostgreSQL Database:** Đã chuẩn bị sẵn database với các bảng tương ứng cho `company` và `invoice`.
- **Discord Webhook URL:** Đường dẫn Webhook của kênh Discord nhận thông báo.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải mã nguồn JSON của workflow từ link gốc (ID: `6558`) trên n8n.io, sau đó copy nội dung dán trực tiếp vào n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 23 nodes phối hợp nhịp nhàng. Các sếp cần chú ý cấu hình kỹ các phần sau:

- **Email Trigger (IMAP):** 
  - Vào phần **Credentials**, tạo mới kết nối IMAP bằng thông tin hòm thư doanh nghiệp của các sếp.
  - Cài đặt bộ lọc (Filter) chỉ nhận các email có file đính kèm là `.pdf` để tiết kiệm tài nguyên.
- **OpenAI Chat Model & Basic LLM Chain:**
  - Điền OpenAI API Key vào credentials của node **OpenAI Chat Model**.
  - Kiểm tra lại model (`gpt-4o-mini` hoặc `gpt-4o`).
  - Tại **Basic LLM Chain** và **Structured Output Parser**, định nghĩa rõ ràng các trường dữ liệu cần trích xuất (Số hóa đơn, Ngày tháng, Tên người bán, Mã số thuế, Tổng tiền, Tiền tệ...).
- **PostgreSQL Nodes (Check Company, Add Company, Check Invoice, Add Invoice):**
  - ⚠️ *Rất quan trọng:* Trong tất cả các node tương tác với PostgreSQL, các sếp **phải thủ công chọn lại credentials database của mình** từ dropdown.
  - Đảm bảo database đã thiết lập sẵn schema cho bảng nhà cung cấp (`company`) và bảng hóa đơn (`invoice`) để tránh lỗi khi node thực thi câu lệnh SQL (`executeQuery` hoặc `Insert`).
- **Discord Webhook:**
  - Vào Discord channel mong muốn $\rightarrow$ Server Settings $\rightarrow$ Integrations $\rightarrow$ Webhooks $\rightarrow$ Tạo Webhook mới.
  - Copy URL và dán vào node **Discord** trong n8n để nhận thông báo chi tiết mỗi khi có hóa đơn mới được xử lý thành công.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** và gửi một email test chứa file PDF hóa đơn mẫu vào hòm thư IMAP để kiểm tra toàn bộ đường đi dữ liệu.
- Kiểm tra xem dữ liệu đã được đẩy vào PostgreSQL và thông báo đã hiện lên Discord chưa.
- Nếu mọi thứ mượt mà, gạt công tắc sang **Active** để hệ thống tự chạy ngầm 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Đổi kênh thông báo:** Nếu công ty không dùng Discord, các sếp có thể thay thế node Discord bằng **Slack**, **Telegram Bot**, hoặc **Microsoft Teams** cực kỳ dễ dàng.
- **Mở rộng lưu trữ:** Thay vì PostgreSQL, nếu sếp thích no-code hoàn toàn có thể thay bằng **Airtable**, **Google Sheets**, hoặc **Supabase**.
- **Xử lý ngoại lệ (Error Handling):** Thêm node *Error Trigger* để nếu AI không đọc được file PDF lạ hoặc lỗi kết nối DB, hệ thống sẽ gửi cảnh báo về Telegram cá nhân để xử lý kịp thời.

### 📌 Kết luận
Việc tự động hóa quy trình xử lý hóa đơn đầu vào không chỉ giúp tiết kiệm hàng chục giờ nhập liệu thủ công mỗi tháng mà còn loại bỏ hoàn toàn sai sót số liệu. Hãy áp dụng ngay workflow này để tối ưu hóa vận hành cho doanh nghiệp của các sếp nhé!