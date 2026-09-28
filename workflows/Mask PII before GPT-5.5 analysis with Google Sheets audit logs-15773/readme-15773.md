---
title: "🚀 Tự động ẩn thông tin cá nhân (PII) trước khi phân tích AI với Google Sheets Audit Logs"
description: "Hướng dẫn xây dựng workflow n8n bảo mật dữ liệu nhạy cảm bằng cách che giấu PII trước khi gửi tới OpenAI, kết hợp lưu trữ audit log trên Google Sheets."
slug: "mask-pii-before-gpt-analysis-google-sheets"
tags: [n8n, automation, ai, security, openai, google-sheets, pii-protection]
keywords: [n8n workflow, ẩn thông tin pii, bảo mật dữ liệu ai, openai pii mask, google sheets audit log]
---

# 🚀 Tự động ẩn thông tin cá nhân (PII) trước khi phân tích AI với Google Sheets Audit Logs

Các đội ngũ pháp lý, nhân sự, chăm sóc khách hàng và tuân thủ dữ liệu thường xuyên gặp phải rủi ro lớn: Muốn tận dụng sức mạnh phân tích của các mô hình AI tiên tiến nhưng lại sợ lộ thông tin cá nhân (PII) của khách hàng hoặc nhân viên. Việc xử lý thủ công vừa mất thời gian vừa dễ xảy ra sơ suất.

Workflow n8n này chính là giải pháp tự động hóa 100% không cần code giúp quét, ẩn (tokenize) thông tin nhạy cảm trước khi gửi lên OpenAI, sau đó khôi phục lại dữ liệu ở kết quả đầu ra và ghi nhận nhật ký kiểm toán (audit log) đầy đủ.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Bảo mật tuyệt đối:** Ngăn chặn việc rò rỉ dữ liệu nhạy cảm (email, số điện thoại, thẻ ngân hàng, căn cước...) lên các mô hình AI của bên thứ ba.
- **Tự động hóa toàn trình:** Xử lý từ khâu nhận dữ liệu qua Webhook, mã hóa tạm thời, gọi OpenAI, khôi phục dữ liệu và trả kết quả chỉ trong vài giây.
- **Tuân thủ tiêu chuẩn (Compliance):** Lưu trữ toàn bộ lịch sử giao dịch và kiểm toán (Audit Trail) trên Google Sheets để dễ dàng kiểm tra.
- **Hoạt động liên tục 24/7:** Đảm bảo hệ thống proxy dữ liệu luôn sẵn sàng phục vụ các ứng dụng khác.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản n8n (Self-hosted hoặc Cloud).
- Tài khoản OpenAI có quyền truy cập mô hình AI.
- Tài khoản Google Sheets để lưu Token Vault và Audit Log.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tạo một workflow mới trên n8n, sao chép toàn bộ mã nguồn JSON của template này và dán trực tiếp vào giao diện n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống vận hành trơn tru, các sếp cần cấu hình chính xác các node sau:

- **Receive Document (`webhook`):** Cấu hình đường dẫn endpoint (`/pii-proxy`) để nhận dữ liệu đầu vào dạng POST với trường `text`.
- **Detect PII via Regex & Tokenize and Replace PII (`code`):** Các node xử lý JavaScript sẵn có giúp quét các mẫu dữ liệu như email, số điện thoại, địa chỉ và thay thế bằng các token dạng `<<PII_EMAIL_7F3A>>`. Các sếp có thể tùy chỉnh lại regex cho phù hợp với quốc gia hoặc định dạng dữ liệu riêng (như CCCD, mã số thuế tại Việt Nam).
- **Store Token Vault & Log Audit Trail (`googleSheets`):** Kết nối tài khoản Google Sheets của các sếp. Chuẩn bị sẵn một Google Sheet với 2 tab chính là `PII Vault` và `Audit Log` để hệ thống tự động ghi nhận dữ liệu phiên và lịch sử kiểm toán.
- **OpenAI Analyze Sanitized Text (`openAi`):** Kết nối credential OpenAI và chọn mô hình mong muốn (như GPT-4o hoặc GPT-5.5) để phân tích đoạn văn bản đã được làm sạch (sanitized text).
- **Restore Original PII (`code`):** Node này dùng bộ nhớ tạm của luồng thực thi hiện tại để dịch ngược các token thành dữ liệu gốc ban đầu trong kết quả trả về của AI.
- **Return Processed Document (`respondToWebhook`):** Trả về kết quả JSON cuối cùng cho ứng dụng gọi đến.

#### 3. Kích hoạt ⚡️
- Thực hiện chạy thử (Test run) với một đoạn văn bản mẫu chứa thông tin cá nhân.
- Kiểm tra kết quả trên Google Sheets và phản hồi trả về.
- Bật công tắc **Active** để đưa workflow vào vận hành chính thức.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo:** Kết hợp thêm node Telegram hoặc Slack để gửi cảnh báo ngay lập tức về đội ngũ bảo mật nếu phát hiện tài liệu có mức độ rủi ro cao.
- **Nâng cấp kho lưu trữ:** Thay thế Google Sheets bằng cơ sở dữ liệu được mã hóa (như PostgreSQL hoặc MongoDB) nếu doanh nghiệp có yêu cầu bảo mật khắt khe hơn về Token Vault.
- **Kiểm duyệt thủ công:** Thêm điều kiện nhánh (If node) để định tuyến các tài liệu có độ rủi ro cao sang hàng đợi chờ phê duyệt thủ công trước khi gửi cho AI xử lý.

### 📌 Kết luận
Việc tích hợp lớp bảo vệ PII trước khi gọi AI không chỉ giúp doanh nghiệp tuân thủ các quy định về bảo mật dữ liệu mà còn tạo sự an tâm tuyệt đối khi ứng dụng công nghệ trí tuệ nhân tạo vào quy trình vận hành thực tế. Hãy triển khai ngay hôm nay!