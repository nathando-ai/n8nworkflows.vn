---
title: "🚀 Tự động hóa lấy dữ liệu nhân sự SAP SuccessFactors qua SAML 2.0 Bearer OAuth2 trong n8n"
description: "Hướng dẫn kết nối và trích xuất dữ liệu nhân sự PerPerson từ SAP SuccessFactors tự động bằng workflow n8n thông qua luồng xác thực OAuth2 SAML 2.0 Bearer độc quyền."
slug: "lay-du-lieu-nhan-su-sap-successfactors-n8n"
tags: [n8n, automation, sap-successfactors, hr-tech, oauth2, saml2]
keywords: [n8n workflow, sap successfactors integration, saml 2.0 bearer oauth2, tu dong hoa hr, odata v2 successfactors]
---

# 🚀 Tự động hóa lấy dữ liệu nhân sự SAP SuccessFactors qua SAML 2.0 Bearer OAuth2

Các doanh nghiệp sử dụng **SAP SuccessFactors (SF)** thường gặp khó khăn lớn khi tích hợp dữ liệu nhân sự do SF sử dụng cơ chế xác thực **SAML 2.0 Bearer Assertion** phức tạp mà các loại Credential OAuth2 thông thường của n8n không hỗ trợ trực tiếp. Việc trích xuất thủ công hoặc xây dựng script custom vừa tốn kém thời gian, vừa tiềm ẩn rủi ro bảo mật khi dùng Basic Auth.

Workflow n8n này do chuyên gia *Chris from HRX* thiết kế sẽ giải quyết triệt để bài toán trên, tự động hóa 100% quy trình từ việc tạo SAML Assertion, đổi Token cho đến gọi API OData v2 để bóc tách dữ liệu nhân sự (`PerPerson` và `employmentNav`) một cách mượt mà và an toàn.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Vượt rào cản bảo mật:** Xử lý thành công luồng SAML 2.0 Bearer Assertion khắt khe của SAP SuccessFactors mà không cần viết code phức tạp.
- **Dữ liệu chuẩn hóa (Flatten):** Tự động bóc tách kết quả trả về từ dạng lồng nhau (nested JSON) thành từng bản ghi riêng biệt cho mỗi nhân sự và thông tin việc làm (`PerPerson` & `employmentNav`).
- **Tự động hóa toàn diện:** Thay thế hoàn toàn thao tác xuất báo cáo thủ công, sẵn sàng tích hợp vào lịch trình chạy tự động hàng ngày.
- **Bảo mật tuyệt đối:** Sử dụng khóa riêng tư (Private Key / X.509 Certificate) đúng chuẩn doanh nghiệp.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Hệ thống **n8n** (phiên bản cloud hoặc self-hosted).
- Tài khoản quản trị **SAP SuccessFactors** (để đăng ký OAuth2 Client và lấy chứng chỉ).
- Các thông số kết nối: Base URL của OData v2, IDP URL, Token URL, Company ID, Client ID, User ID (Service Account) và Private Key dạng Base64.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow từ [n8n.io/workflows/14509](https://n8n.io/workflows/14509) hoặc copy toàn bộ mã nguồn JSON, sau đó dán trực tiếp vào n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 6 nodes chính, các sếp cần chú ý cấu hình kỹ lưỡng các node sau:

- **Node `Configuration` (Set):** Đây là nơi lưu trữ các tham số cấu hình quan trọng nhất của hệ thống SuccessFactors:
  - `SF_API_BASE_URL`: Đường dẫn cơ sở OData v2 của SuccessFactors.
  - `SF_IDP_URL`: Endpoint nhận assertion (`/oauth/idp`).
  - `SF_TOKEN_URL`: Endpoint lấy token (`/oauth/token`).
  - `company_id`: ID Tenant của doanh nghiệp trên SuccessFactors.
  - `client_id`: API Key nhận được khi đăng ký OAuth2 Client trong SF.
  - `user_id`: **Bắt buộc.** User ID của tài khoản dịch vụ (Service Account) mà token sẽ được cấp phát dựa trên quyền hạn của user đó.
  - `private_key`: Nội dung Base64 được trích xuất từ file `Certificate.pem` (lược bỏ dòng header `-----BEGIN ENCRYPTED PRIVATE KEY-----`, footer và các ký tự xuống dòng).
  - `top` / `select`: Các tham số truy vấn OData để lọc dữ liệu.

- **Các bước chuẩn bị Certificate trong SAP SuccessFactors:**
  1. Vào SF Admin → `Manage OAuth2 Client Applications` → `Register new client application`.
  2. Đặt tên ứng dụng tùy ý và nhấn `Generate X.509 Certificate` (có thể đặt Common Name ảo và chọn thời hạn chứng chỉ phù hợp).
  3. Lấy **API Key** (dùng cho `client_id`) và Export file `Certificate.pem`.
  4. Mở file `.pem` bằng trình soạn thảo văn bản và copy chuỗi Base64 ở giữa `-----BEGIN ENCRYPTED PRIVATE KEY-----` và `-----END ENCRYPTED PRIVATE KEY-----` để dán vào cấu hình `private_key`.

- **Các node `Get SAML Assertion`, `Get Bearer Token`, `Fetch PerPerson from SF` (HTTP Request):** Các node này đã được thiết lập sẵn phương thức POST/GET cùng các header cần thiết khớp với luồng SAML 2.0 Bearer, các sếp chỉ cần đảm bảo node `Configuration` truyền đúng biến sang.

- **Node `Flatten Results` (Code):** Node này chạy đoạn mã JavaScript để làm phẳng cấu trúc dữ liệu (`d.results` và `employmentNav.results`), giúp trả về danh sách phẳng rõ ràng, mỗi item tương ứng với một bản ghi nhân sự - việc làm.

#### 3. Kích hoạt ⚡️
- Nhấn **Test workflow** trên node `When clicking 'Test workflow'` để kiểm tra luồng chạy xem dữ liệu trả về từ SuccessFactors đã chính xác chưa.
- Sau khi test thành công, bật công tắc **Active** ở góc trên bên phải để workflow chuyển sang trạng thái tự động hoạt động.

### ✍️ Mẹo & gợi ý nâng cao
- **Thay đổi Trigger:** Thay thế `Manual Trigger` bằng `Schedule Trigger` để hệ thống tự động đồng bộ dữ liệu nhân sự định kỳ (ví dụ: chạy mỗi sáng lúc 6:00 AM).
- **Mở rộng trường dữ liệu:** Bổ sung thêm các navigation nav như `personalInfoNav`, `jobInfoNav` vào chuỗi truy vấn OData trong node cấu hình để lấy thêm thông tin chi tiết.
- **Tích hợp thông báo:** Nối thêm node **Slack** hoặc **Telegram** ở cuối workflow để gửi thông báo cáo cáo số lượng nhân sự đã đồng bộ thành công hoặc cảnh báo lỗi nếu kết nối SF thất bại.

### 📌 Kết luận
Việc tích hợp dữ liệu từ các hệ thống ERP/HR lớn như SAP SuccessFactors không còn là thử thách lớn khi đã có workflow n8n tự động hóa hoàn toàn luồng SAML 2.0 Bearer OAuth2 này. Hãy áp dụng ngay để tiết kiệm hàng giờ thao tác thủ công cho đội ngũ Nhân sự của doanh nghiệp các sếp!