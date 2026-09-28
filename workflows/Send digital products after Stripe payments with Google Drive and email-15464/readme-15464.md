---
title: "🚀 Tự Động Gửi Sản Phẩm Số Sau Khi Khách Thanh Toán Stripe Với Google Drive và Email"
description: "Hướng dẫn xây dựng workflow n8n tự động xác thực webhook Stripe, tìm kiếm và tải file từ Google Drive rồi gửi email sản phẩm số cho khách hàng 24/7."
slug: "tu-dong-gui-san-pham-so-stripe-google-drive-email-n8n"
tags: [n8n, automation, no-code, stripe, google-drive, ecommerce]
keywords: [n8n workflow, tự động hóa stripe, gửi file google drive tự động, bán hàng số tự động, webhook stripe n8n]
---

# 🚀 Tự Động Gửi Sản Phẩm Số Sau Khi Thanh Toán Stripe: Giải Pháp "Ngủ Mà Vẫn Ra Đơn"

Việc bán các sản phẩm số (e-book, khóa học, tài liệu, phần mềm...) mang lại biên lợi nhuận tuyệt vời, nhưng quy trình xử lý thủ công (kiểm tra tiền về tài khoản -> tìm file -> soạn email -> gửi file cho khách) lại cực kỳ tốn thời gian và dễ xảy ra sai sót, đặc biệt là khi khách hàng mua vào lúc nửa đêm.

Được thiết kế bởi **Blukaze Automations**, workflow n8n này sẽ giải quyết triệt để nỗi đau đó. Hệ thống sẽ tự động bắt sự kiện thanh toán thành công từ Stripe, bảo mật bằng chữ ký số, tìm đúng sản phẩm trên Google Drive và gửi ngay email đính kèm hoặc link tải cho khách hàng trong tích tắc mà không cần sự can thiệp thủ công nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Ngay khi khách thanh toán thành công trên Stripe, email chứa sản phẩm sẽ được gửi đi ngay lập tức (dưới 5 giây).
- **Bảo mật tuyệt đối:** Sử dụng node **Crypto** và **If** để xác thực chữ ký Webhook từ Stripe, ngăn chặn hoàn toàn các request giả mạo.
- **Quản lý file thông minh:** Tự động tìm kiếm đúng file sản phẩm trên Google Drive dựa theo mã sản phẩm hoặc danh mục thanh toán.
- **Nâng cao trải nghiệm khách hàng:** Khách hàng nhận được sản phẩm ngay lập tức, gia tăng sự hài lòng và uy tín cho thương hiệu của các sếp.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị sẵn các tài nguyên sau:
1. **Tài khoản n8n** (Cloud hoặc Self-hosted).
2. **Tài khoản Stripe** đã cấu hình sản phẩm và Webhook Endpoint.
3. **Tài khoản Google Drive** chứa các file sản phẩm số cần phân phối.
4. **SMTP Server / Email Account** (Gmail, SendGrid, Resend, hoặc SMTP riêng) để gửi email tự động qua node **Send email**.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tạo một workflow mới trên n8n, sau đó copy đoạn JSON của workflow (hoặc import file JSON) vào giao diện làm việc của n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống vận hành trơn tru, các sếp cần cấu hình chính xác các node cốt lõi sau:

- **Webhook:** 
  - Tạo một Webhook URL trong n8n và đem dán vào phần cài đặt Webhook của bảng điều khiển Stripe (chọn sự kiện `checkout.session.completed`).
  - Lấy chuỗi **Webhook Secret** (`whsec_...`) từ Stripe để cấu hình cho node tiếp theo.
- **Crypto:** 
  - Node này dùng để giải mã và xác thực chữ ký (Signature) gửi từ Stripe. Các sếp cần điền đúng Webhook Secret vào tham số của node này để đảm bảo tính bảo mật.
- **Is Signature Valid? (If):** 
  - Node điều kiện kiểm tra xem chữ ký có hợp lệ hay không. Nếu hợp lệ (`true`), luồng mới được phép chạy tiếp sang các bước xử lý đơn hàng.
- **Switch:** 
  - Dùng để phân loại sản phẩm dựa trên thông tin nhận được từ Stripe (ví dụ: Khách mua sản phẩm A thì trỏ sang nhánh tải file A, mua sản phẩm B trỏ sang nhánh file B trên Google Drive).
- **Search files and folders & Download file (Google Drive):** 
  - Kết nối tài khoản Google Drive của các sếp.
  - Cấu hình thư mục lưu trữ sản phẩm số và thiết lập từ khóa tìm kiếm (Search Query) khớp với tên hoặc ID sản phẩm trên Stripe.
- **Send email:** 
  - Cấu hình thông tin người gửi (Sender), tiêu đề và nội dung email chăm sóc khách hàng.
  - Đính kèm file vừa tải từ Google Drive hoặc chèn link tải trực tiếp vào nội dung email.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và thực hiện một giao dịch test (hoặc dùng tính năng Test Webhook của Stripe) để kiểm tra dữ liệu chạy qua từng node.
- Sau khi test thành công, bật trạng thái **Active** cho workflow để hệ thống bắt đầu tự động hóa thực tế.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết nối Telegram/Slack:** Thêm một node thông báo vào kênh Telegram nội bộ mỗi khi có khách hàng thanh toán thành công để đội ngũ sales nắm bắt.
- **Lưu trữ thông tin khách hàng:** Tích hợp thêm node Google Sheets hoặc Airtable để lưu lại lịch sử mua hàng, phục vụ cho việcRemarketing sau này.
- **Cá nhân hóa nội dung email:** Sử dụng AI (OpenAI/Anthropic node) để viết lời cảm ơn độc đáo dựa trên tên khách hàng và sản phẩm họ vừa mua.

### 📌 Kết luận
Với workflow n8n này, các sếp đã sở hữu một hệ thống bàn hàng số tự động chuyên nghiệp chẳng thua kém các sàn thương mại điện tử lớn. Hãy triển khai ngay hôm nay để tiết kiệm thời gian và tối ưu hóa doanh thu cùng các giải pháp tự động hóa từ **Blukaze Automations**!