---
title: "🚀 Tự động ẩn danh dữ liệu cá nhân (PII) trong tài liệu chuẩn GDPR bằng Postgres và Claude"
description: "Hướng dẫn xây dựng workflow n8n tự động phát hiện, mã hóa PII (Email, SĐT, Địa chỉ) và xử lý AI an toàn với Claude mà không lo lộ lọt dữ liệu."
slug: "mask-pii-documents-gdpr-ai-processing-postgres-claude"
tags: [n8n, automation, ai, gdpr, claude, postgres, security]
keywords: [n8n workflow, ẩn danh PII, GDPR AI, Claude AI, bảo mật dữ liệu, Postgres vault]
---

# 🚀 Tự động ẩn danh dữ liệu cá nhân (PII) trong tài liệu chuẩn GDPR bằng Postgres và Claude

Các doanh nghiệp hiện nay rất muốn tận dụng sức mạnh của Trí tuệ Nhân tạo (AI) để phân tích, tóm tắt tài liệu hợp đồng, hồ sơ khách hàng. Tuy nhiên, rào cản lớn nhất chính là **quy định bảo mật dữ liệu nghiêm ngặt như GDPR**. Việc đưa trực tiếp tài liệu chứa thông tin cá nhân (PII - Personally Identifiable Information) như email, số điện thoại, căn cước, địa chỉ lên các mô hình AI bên thứ ba tiềm ẩn rủi ro pháp lý và lộ lọt dữ liệu cực lớn.

Workflow n8n chuyên nghiệp này từ *ResilNext* sinh ra để giải quyết triệt để nỗi đau đó. Nó hoạt động như một "tấm khiên" bảo vệ tự động 100%: Nhận tài liệu, bóc tách văn bản, quét và thay thế toàn bộ PII bằng các token bảo mật (ví dụ: `<<EMAIL_AB12>>`) lưu vào **Postgres Vault**, sau đó mới đẩy dữ liệu đã ẩn danh sang AI Claude xử lý, và cuối cùng có thể khôi phục lại dữ liệu gốc một cách có kiểm soát.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow xử lý tài liệu lớn và chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tuân thủ tuyệt đối GDPR:** Đảm bảo không một thông tin nhạy cảm nào của khách hàng bị lộ ra ngoài hệ thống AI.
- **Tự động hóa toàn diện:** Từ khâu nhận file qua Webhook, OCR, quét PII, mã hóa token đến gọi AI và ghi log kiểm toán (Audit Log).
- **Lưu trữ an toàn:** Tách biệt hoàn toàn dữ liệu gốc (lưu trong Postgres Vault) và dữ liệu đưa vào AI.
- **Kiểm soát linh hoạt:** Cơ chế kiểm soát khôi phục (Re-injection) giúp chỉ giải mã PII khi thực sự cần thiết và đúng phân quyền.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Khuyên dùng Self-hosted để đảm bảo bảo mật dữ liệu nội bộ).
- **Database PostgreSQL:** Cần chuẩn bị sẵn cơ sở dữ liệu Postgres để làm Vault lưu token và bảng Audit Log.
- **AI Credentials:** 
  - API Key của Anthropic (cho model **Claude Sonnet 4.5**).
  - (Tùy chọn) Local Ollama cho một số tác vụ bóc tách địa chỉ nâng cao.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow (hoặc copy từ nguồn ResilNext) và import trực tiếp vào n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống vận hành trơn tru, các sếp cần cấu hình kỹ các node trọng điểm sau:
- **`Document Upload Webhook`**: Điểm tiếp nhận tài liệu PDF đầu vào qua phương thức `POST` tại đường dẫn `/gdpr-document-upload`.
- **`OCR Extract Text`**: Node thực hiện bóc tách chữ từ file PDF tải lên. Hãy đảm bảo định dạng file đầu vào chuẩn xác.
- **`Store Tokens in Vault` & `Retrieve Original Values` (Postgres Nodes)**: Cần kết nối credential tới cơ sở dữ liệu Postgres của doanh nghiệp. Các sếp nhớ tạo trước 2 bảng `pii_vault` (lưu cặp token và giá trị thật) và `pii_audit_log` (lưu vết sự kiện).
- **`AI Processing Model` (Claude Anthropic)**: Chọn model `claude-sonnet-4-5-20250929` và điền Anthropic API Key hợp lệ.
- **`Send Alert Notification` (HTTP Request)**: Cấu hình Webhook tới Slack/Telegram của đội ngũ kỹ thuật để nhận cảnh báo nếu quy trình kiểm tra an toàn (Masking Safety Check) phát hiện lỗi rò rỉ dữ liệu.

#### 3. Kích hoạt ⚡️
- Gửi một file PDF mẫu chứa thông tin cá nhân (email, SĐT giả lập) tới endpoint Webhook để tiến hành Test Run.
- Kiểm tra các bảng trong Postgres xem token đã được tạo và lưu trữ đúng chưa.
- Sau khi test thành công, bật trạng thái **Active** cho workflow.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp kênh thông báo:** Kết nối node `Send Alert Notification` với Slack hoặc Telegram để nhận báo cáo ngay lập tức mỗi khi có tài liệu được xử lý hoặc có cảnh báo bảo mật.
- **Mở rộng bộ lọc PII:** Ngoài Email, SĐT, Địa chỉ và Mã định danh có sẵn, các sếp có thể viết thêm các Regex Pattern trong các node Code detector để phát hiện thêm số tài khoản ngân hàng, mã số thuế... tùy theo đặc thù ngành nghề.
- **Lưu trữ Audit Trail:** Tận dụng bảng `Store Audit Log` để phục vụ cho các đợt kiểm toán bảo mật (Security Audit) hàng năm của công ty.

### 📌 Kết luận
Việc tích hợp AI vào quy trình doanh nghiệp không thể đánh đổi bằng sự rủi ro về rò rỉ dữ liệu khách hàng. Với workflow n8n kết hợp Postgres và Claude này, các sếp hoàn toàn có thể yên tâm khai thác sức mạnh của AI một cách an toàn, minh bạch và chuẩn mực tuân thủ GDPR. Hãy triển khai ngay hôm nay!