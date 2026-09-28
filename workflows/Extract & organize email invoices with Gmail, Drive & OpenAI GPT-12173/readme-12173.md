---
title: "🚀 Tự động hóa trích xuất hóa đơn email với Gmail, Google Drive và OpenAI GPT"
description: "Hướng dẫn xây dựng workflow n8n tự động bắt email hóa đơn, phân tích thông tin bằng AI, lưu file lên Google Drive và đồng bộ dữ liệu vào Google Sheets 100% không cần code."
slug: "tu-dong-hoa-trich-xuat-hoa-don-email-voi-gmail-drive-openai"
tags: [n8n, automation, no-code, gmail, google-drive, google-sheets, openai, ai-agents]
keywords: [n8n workflow, trich xuat hoa don, tu dong hoa hoa don, gmail to google sheets, ai invoice extractor, n8n openai gpt]
---

# 🚀 Tự động hóa trích xuất hóa đơn email với Gmail, Google Drive và OpenAI GPT

Các sếp có đang cảm thấy mệt mỏi mỗi cuối tháng khi phải lục tung hộp thư Gmail để tìm từng chiếc hóa đơn PDF, file biên lai thanh toán, sau đó thủ công copy số tiền, tên nhà cung cấp vào Excel hay Google Sheets? Việc này không chỉ tốn hàng giờ đồng hồ mà còn rất dễ dẫn đến sai sót, nhầm lẫn số liệu kế toán.

Đừng lo, bài viết này sẽ hướng dẫn các sếp thiết lập một siêu phẩm automation bằng **n8n** mang tên **"Extract & organize email invoices with Gmail, Drive & OpenAI GPT"** do tác giả Feras Dabour chia sẻ. Workflow này sẽ thay các sếp làm sạch mọi việc từ A-Z: tự động quét email, nhận diện hóa đơn thông minh bằng AI, trích xuất dữ liệu chuẩn xác, lưu trữ file khoa học và cập nhật sổ cái tức thì!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Không cần động tay vào việc tải file hay copy-paste dữ liệu hóa đơn từ email nữa.
- **AI thông minh:** Sử dụng OpenAI GPT để phân biệt chính xác đâu là hóa đơn, đâu là email rác/thông thường; đồng thời bóc tách dữ liệu cực kỳ chuẩn xác.
- **Lưu trữ đồng bộ:** Tự động đẩy file PDF lên Google Drive và ghi nhận toàn bộ thông số vào Google Sheets (kèm link truy cập nhanh).
- **Hoạt động không nghỉ:** Lắng nghe hòm thư liên tục, xử lý ngay lập tức khi có email hóa đơn mới và đánh dấu đã đọc để tránh xử lý trùng lặp.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt sẵn (Cloud hoặc Self-hosted).
- **Tài khoản Gmail:** Có quyền cấu hình OAuth2 để n8n đọc và quản lý hòm thư.
- **Google Drive & Google Sheets:** Tài khoản Google Workspace/Gmail để lưu trữ file hóa đơn và ghi dữ liệu.
- **OpenAI API Key:** Đã cấu hình để sử dụng các mô hình GPT cho AI Agent.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể truy cập link gốc trên n8n templates (ID: 12173), copy mã JSON của workflow, sau đó vào giao diện n8n của mình -> Chọn **Workflows** -> **Import from JSON** và dán vào là xong.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần chú ý cấu hình kỹ các node sau:

- **Gmail Trigger:** Cấu hình tài khoản thông qua **Gmail OAuth2**. Tùy chỉnh bộ lọc (khoảng thời gian quét, nhãn email, hoặc từ khóa tìm kiếm như "invoice", "receipt") để tránh workflow quét nhầm email không cần thiết.
- **OpenAI Chat Model (các node):** Kết nối credentials **openAiApi** và kiểm tra lại model đang sử dụng (mặc định trong workflow là `gpt-5.1` hoặc các dòng model tương đương hỗ trợ Structured Output).
- **Invoice Recognition Agent & Invoice Data extractor:** Kiểm tra kỹ system prompt của AI Agents để đảm bảo các trường thông tin cần bóc tách đúng ý muốn doanh nghiệp (`date_email`, `date_invoice`, `invoice_nr`, `description`, `provider`, `net_amount`, `vat`, `gross_amount`, `label`, `currency`).
- **Upload file (Google Drive):** Chọn đúng thư mục (Folder ID) trên Google Drive nơi các sếp muốn lưu trữ toàn bộ hóa đơn PDF được tải về từ email.
- **Document the invoice parameters & Update Invoice parameters (Google Sheets):** Trỏ tới file Google Sheets quản lý tài chính của doanh nghiệp, chọn đúng sheet và map các cột dữ liệu tương ứng với các biến mà AI vừa trích xuất.
- **Mark a message as read (Gmail):** Node này sẽ tự động gắn nhãn/đánh dấu email là "Đã đọc" sau khi xử lý thành công, giúp các sếp quản lý hòm thư gọn gàng, không bị lặp lại đơn hàng cũ.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và gửi một email test chứa hóa đơn PDF vào hòm thư để kiểm tra xem dữ liệu có bay thẳng lên Google Drive và Google Sheets hay không.
- Sau khi test thành công, gạt công tắc sang **Active** để hệ thống tự động chạy ngầm 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Thêm cảnh báo Slack/Telegram:** Nối thêm một node Slack hoặc Telegram ngay sau bước ghi nhận Google Sheets để bắn thông báo ngay lập tức về nhóm kế toán khi có hóa đơn giá trị cao xuất hiện.
- **Mở rộng danh mục nhãn (Label):** Tùy chỉnh thêm các phân loại chi phí trong prompt của AI (ví dụ: *marketing, software, hardware, office supplies*) để tối ưu hóa việc phân bổ ngân sách.
- **Quản lý mã dự án/Cost Center:** Bổ sung thêm trường dữ liệu vào prompt của AI extractor nếu doanh nghiệp cần hạch toán chi phí theo từng mã dự án cụ thể.

### 📌 Kết luận
Workflow này chính là "vũ khí bí mật" giúp các nhà sáng lập, đội ngũ kế toán và các freelancer giải phóng bản thân khỏi những tác vụ thủ công nhàm chán. Hãy triển khai ngay hôm nay để tối ưu hóa quy trình quản lý tài chính doanh nghiệp các sếp nhé!