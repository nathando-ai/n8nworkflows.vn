---
title: "🚀 Tự động phát hiện hóa đơn trùng lặp và rủi ro gian lận AP với n8n, Gmail, OpenAI và Supabase"
description: "Hướng dẫn cấu hình workflow n8n tự động đọc hóa đơn từ Gmail, trích xuất dữ liệu bằng AI GPT-4o, kiểm tra trùng lặp trên Supabase và cảnh báo rủi ro qua Slack."
slug: "tu-dong-phat-hien-hoa-don-trung-lap-va-rui-ro-voi-n8n"
tags: [n8n, automation, no-code, openai, supabase, finance, invoice-processing]
keywords: [n8n workflow, tự động hóa hóa đơn, phát hiện hóa đơn trùng lặp, openai gpt-4o, supabase automation, quản lý tài chính ap]
---

# 🚀 Tự động phát hiện hóa đơn trùng lặp và rủi ro gian lận AP với n8n, OpenAI và Supabase

Trong quy trình kế toán phải trả (Accounts Payable - AP), việc xử lý hàng loạt hóa đơn thủ công từ email rất dễ dẫn đến sai sót: thanh toán nhầm hóa đơn trùng lặp, bỏ sót các nhà cung cấp có lịch sử bất thường hoặc gặp phải rủi ro gian lận tinh vi. 

Workflow n8n này sẽ giải quyết triệt để nỗi đau đó bằng cách tự động hóa 100% quy trình: tiếp nhận hóa đơn qua Gmail, sử dụng AI (GPT-4o) để bóc tách dữ liệu, đối soát lịch sử trên Supabase, đánh giá điểm rủi ro gian lận và tự động cảnh báo lên Slack hoặc gửi thông báo tạm giữ hóa đơn.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Tự động hóa hoàn toàn khâu đọc email, bóc tách dữ liệu và đối chiếu sổ sách.
- **Ngăn chặn thất thoát tài chính:** Tự động phát hiện hóa đơn trùng lặp hoặc các giao dịch có dấu hiệu rủi ro cao từ nhà cung cấp.
- **Cảnh báo tức thì:** Bắn tin nhắn trực tiếp lên kênh Slack của bộ phận tài chính ngay khi phát hiện bất thường.
- **Lưu trữ minh bạch:** Mọi quyết định và trạng thái hóa đơn đều được ghi nhận tự động vào cơ sở dữ liệu Supabase.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài nguyên sau:
- Tài khoản **n8n** (Cloud hoặc Self-hosted).
- Tài khoản **Gmail** để nhận và gửi email thông báo (có cấu hình OAuth2).
- **OpenAI API Key** (sử dụng mô hình `gpt-4o`).
- Dự án **Supabase** với 2 bảng dữ liệu chính (`invoices` và `vendors`).
- Không gian làm việc **Slack** và một kênh (channel) chuyên dụng để nhận cảnh báo gian lận.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow từ nguồn cung cấp hoặc copy toàn bộ mã nguồn JSON, sau đó dán trực tiếp vào n8n Editor của các sếp thông qua tính năng Import từ Clipboard.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 15 nodes, các sếp cần chú ý cấu hình chính xác các điểm cốt lõi sau:

- **Gmail — Invoice Inbox (`gmailTrigger`):** Kết nối tài khoản Gmail qua OAuth2 để hệ thống tự động lắng nghe email hóa đơn mới đến (file PDF hoặc nội dung trong body).
- **Extract Invoice Data & Assess Fraud Risk (AI Agent + OpenAI):** Kết nối thông tin xác thực OpenAI (`gpt-4o`). Node này sử dụng cấu trúc Schema (`Invoice Data Schema` và `Fraud Risk Schema`) để bóc tách chuẩn xác số hóa đơn, tên nhà cung cấp, số tiền, hạn thanh toán và chấm điểm rủi ro.
- **Check Duplicates & Check Vendor History (`supabase`):** Kết nối API Credential của Supabase. Các sếp nhớ trỏ đúng tên bảng (`invoices` và `vendors`) đã được thiết lập sẵn trong cơ sở dữ liệu.
- **Alert Slack (`slack`):** Kết nối tài khoản Slack và cập nhật lại tên channel nhận thông báo (ví dụ: `#invoice-alerts`).
- **Send Hold Notice (`gmail`):** Kết nối lại credential Gmail để gửi email thông báo tạm giữ hóa đơn đến quản lý AP (`AP manager`) nếu phát hiện rủi ro cao.
- **Log Invoice to Supabase (`supabase`):** Cấu hình thao tác `insert` để lưu lại toàn bộ lịch sử xử lý hóa đơn vào bảng `invoices` dù kết quả rủi ro là gì.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (**Test run**) với một vài email hóa đơn mẫu để kiểm tra dữ liệu trả về từ OpenAI và Supabase.
- Kiểm tra các nhánh điều kiện tại node **High Risk? (`if`)**.
- Bật công tắc **Active** để workflow chính thức vận hành tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thêm Telegram/Zalo:** Thay vì chỉ gửi thông báo qua Slack, các sếp có thể add thêm node Telegram Bot để đẩy cảnh báo rủi ro hóa đơn ngay trên điện thoại di động.
- **Bổ sung bảng Log chi tiết:** Tạo thêm bảng `audit_logs` trên Supabase để ghi lại lịch sử thao tác của AI Agent phục vụ cho việc kiểm toán sau này.
- **Human-in-the-loop:** Kết hợp thêm node chờ phản hồi (Wait node) để bộ phận kế toán bấm nút "Phê duyệt" hoặc "Từ chối" trực tiếp từ email trước khi hệ thống chuyển tiền.

### 📌 Kết luận
Workflow tự động hóa xử lý hóa đơn AP kết hợp AI và Supabase là giải pháp hoàn hảo giúp doanh nghiệp số hóa toàn bộ quy trình tài chính, loại bỏ hoàn toàn các khoản chi trùng lặp và ngăn chặn rủi ro gian lận. Hãy cài đặt ngay hôm nay để tối ưu hóa vận hành cho đội ngũ kế toán của các sếp!