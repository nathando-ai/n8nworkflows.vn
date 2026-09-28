---
title: "🚀 Tự động giám sát chứng chỉ PKI & CRL với cảnh báo qua Telegram & SMS"
description: "Hướng dẫn cài đặt workflow n8n tự động kiểm tra thời hạn chứng chỉ CA, danh sách thu hồi CRL và trạng thái dịch vụ web, gửi cảnh báo tức thì qua Telegram và SMS."
slug: "giam-sat-chung-chi-pki-crl-telegram-sms"
tags: [n8n, automation, pki, security, telegram, monitoring]
keywords: [n8n workflow, giám sát chứng chỉ, pki certificate monitor, crl alert, telegram sms automation]
---

# 🚀 Tự động giám sát chứng chỉ PKI & CRL với cảnh báo qua Telegram & SMS

Việc bỏ lỡ thời hạn gia hạn của chứng chỉ số (CA Certificates) hay danh sách thu hồi chứng chỉ (CRL) có thể dẫn đến gián đoạn dịch vụ nghiêm trọng, lỗi bảo mật hoặc mất lòng tin từ khách hàng. Thao tác kiểm tra thủ công bằng tay vừa tốn thời gian lại rất dễ bỏ sót.

Workflow n8n này sẽ giải quyết triệt để vấn đề trên bằng cách tự động hóa 100 quy trình: quét danh sách TSL XML, phân tích hạn sử dụng bằng OpenSSL, theo dõi trạng thái website và tự động đẩy cảnh báo qua Telegram hoặc SMS trước 17 tiếng khi chứng chỉ hết hạn.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Chủ động phòng ngừa:** Cảnh báo trước 17 giờ trước khi chứng chỉ CA hoặc CRL hết hạn, giúp đội ngũ kỹ thuật kịp thời xử lý.
- **Giám sát toàn diện:** Tự động phân loại và kiểm tra cả chứng chỉ CA, file CRL và trạng thái sống/chết của các dịch vụ web liên quan.
- **Đa kênh thông báo:** Nhận tin nhắn tức thì qua Telegram Bot và SMS (tích hợp Textbelt) khi có sự cố xảy ra.
- **Vận hành tự động 24/7:** Chạy định kỳ mỗi 12 giờ mà không cần sự can thiệp thủ công từ con người.
:::

### Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một hệ thống n8n Self-hosted (hoặc n8n Cloud) hỗ trợ chạy các lệnh hệ thống (`executeCommand`) vì workflow sử dụng các công cụ như `OpenSSL`, `curl`, `jq`, `libxml2-utils`.
- Telegram Bot Token & Chat ID (để gửi thông báo qua Telegram).
- Tài khoản/API Key từ nhà cung cấp dịch vụ SMS (ví dụ: Textbelt) nếu muốn gửi tin nhắn SMS.
- Nguồn TSL XML (mặc định sử dụng nguồn Hungarian TSL từ NMHH: `http://www.nmhh.hu/tl/pub/HU_TL.xml`).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow hoặc copy toàn bộ mã JSON từ link gốc.
- Mở giao diện n8n Editor, chọn **Add workflow** -> **Import from File** hoặc dán trực tiếp vào vùng làm việc.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Collect Checking URL list (Node Execute Command):** Node này dùng để tải file TSL XML và trích xuất danh sách URL. Nếu muốn đổi nguồn TSL khác, các sếp nhớ sửa lại biến `URL` trong lệnh của node này.
- **Cấu hình thời gian cảnh báo:** Mặc định hệ thống đặt ngưỡng cảnh báo trước 17 giờ. Các sếp có thể điều chỉnh logic này tại hai node:
  - `nextUpdate - TimeFilter` (cho CRL).
  - `nextUpdate - TimeFilter1` (cho CA).
  - Thay đổi điều kiện trong mã JavaScript: `if (diffHours < 17)`.
- **Cấu hình Alert (Telegram & SMS):** Các sếp cần tìm đến 3 node cảnh báo sau để thay thế thông tin cấu hình của mình:
  - `CRL Alert --- Telegam & SMS`
  - `CA Alert --- Telegam & SMS`
  - `Send Website Down - Telegram & SMS`
  - *Thay thế các placeholder:* `YOUR-TELEGRAM-BOT-TOKEN`, `YOUR-TELEGRAM-CHANNEL-ID`, số điện thoại nhận SMS (vd: `+36301234567`) và `YOUR-TEXTBELT-API-KEY`.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** chạy thủ công lần đầu (thông qua node `Execute With Manual Start`) để kiểm tra luồng dữ liệu chạy qua các bước `splitOut`, `splitInBatches` và OpenSSL parse file.
- Sau khi test thành công, bật công tắc **Active** để workflow tự động chạy theo lịch trình từ node `Execute With Scheduled Start` (mỗi 12 giờ).

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thêm kênh thông báo:** Ngoài Telegram và SMS, các sếp có thể nối thêm node Slack, Microsoft Teams hoặc Discord để bắn thông báo vào kênh chung của đội ngũ DevOps/SysAdmin.
- **Lưu lịch sử kiểm tra:** Thêm một node Google Sheets hoặc cơ sở dữ liệu (PostgreSQL/MySQL) vào cuối luồng để ghi log trạng thái của từng chứng chỉ qua các lần quét, phục vụ việc làm báo cáo định kỳ hàng tháng.
- **Tinh chỉnh ngưỡng cảnh báo:** Nếu hệ thống của các sếp có quy trình phê duyệt phức tạp và cần thời gian gia hạn lâu hơn, hãy đổi ngưỡng `17` giờ thành `72` giờ (3 ngày) hoặc `168` giờ (7 ngày).

### 📌 Kết luận
Workflow giám sát PKI Certificates & CRLs này là một trợ thủ đắc lực giúp tự động hóa khâu vận hành hạ tầng an ninh mạng, loại bỏ hoàn toàn rủi ro quên gia hạn chứng chỉ số. Hãy cài đặt ngay lên hệ thống n8n của các sếp để bảo vệ các dịch vụ trực tuyến luôn hoạt động an toàn và thông suốt!