---
title: "🚀 Validate JSON và CSV dữ liệu nhập qua Webhook với quy tắc có thể cấu hình"
description: "Hướng dẫn tự động hóa kiểm tra dữ liệu nhập từ JSON/CSV qua webhook với quy tắc có thể tùy chỉnh, giúp phát hiện lỗi trước khi dữ liệu vào hệ thống"
slug: "validate-json-csv-import-data-via-webhook"
tags: [n8n, automation, no-code, data-validation, import-data]
keywords: [n8n workflow, tự động hóa dữ liệu, kiểm tra dữ liệu nhập, webhook, import data]
---

# 🚀 Validate JSON và CSV dữ liệu nhập qua Webhook với quy tắc có thể cấu hình

[Các sếp đang gặp khó khăn khi nhập dữ liệu từ JSON/CSV vào hệ thống ERP, CRM hay cơ sở dữ liệu. Dữ liệu lỗi có thể gây hỏng hệ thống và làm mất thời gian. Workflow này sẽ giúp các sếp tự động hóa quá trình kiểm tra dữ liệu nhập qua webhook với quy tắc có thể tùy chỉnh, phát hiện lỗi trước khi dữ liệu vào hệ thống.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Phát hiện lỗi sớm**: Kiểm tra dữ liệu nhập trước khi vào hệ thống, giảm thiểu rủi ro dữ liệu lỗi.
- **Tùy chỉnh quy tắc**: Cấu hình quy tắc kiểm tra theo nhu cầu cụ thể của từng trường dữ liệu.
- **Báo cáo chi tiết**: Nhận báo cáo rõ ràng về số lượng bản ghi hợp lệ/không hợp lệ và lỗi cụ thể.
- **Tiết kiệm thời gian**: Tự động hóa quá trình kiểm tra, giảm thiểu công việc thủ công.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản n8n đã cài đặt và chạy.
- Dữ liệu nhập dưới dạng JSON array (mảng các đối tượng).
- Quy tắc kiểm tra (nếu không sử dụng quy tắc mặc định).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor.
2. Click vào "Import from URL" và nhập link: [https://n8n.io/workflows/13999](https://n8n.io/workflows/13999).
3. Hoặc copy JSON từ link trên và paste vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Node "Receive Data" (webhook)**:
  - Đảm bảo đường dẫn webhook là duy nhất và bảo mật.
  - Có thể thay đổi đường dẫn trong tham số `path` của node này.

- **Node "Set Default Rules" (set)**:
  - Cấu hình quy tắc kiểm tra mặc định cho dữ liệu nhập.
  - Chỉnh sửa JSON trong node này để phù hợp với cấu trúc dữ liệu của các sếp.
  - Ví dụ quy tắc kiểm tra email:
    ```json
    {
      "email": {
        "required": true,
        "type": "email"
      }
    }
    ```

- **Node "Validate Data" (code)**:
  - Node này đã được cấu hình sẵn, không cần chỉnh sửa.
  - Node này thực hiện kiểm tra dữ liệu theo quy tắc được cung cấp.

- **Node "Respond with Report" (respondToWebhook)**:
  - Node này trả về báo cáo kiểm tra dữ liệu.
  - Có thể tùy chỉnh thông điệp trả về nếu cần.

#### 3. Kích hoạt ⚡️
1. Kiểm tra kết nối và cấu hình các node.
2. Chạy thử với dữ liệu mẫu để đảm bảo workflow hoạt động đúng.
3. Bật Active workflow để sử dụng.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp với Slack/Telegram**: Thêm node gửi thông báo lỗi qua Slack hoặc Telegram.
- **Lưu log kiểm tra**: Thêm node lưu log kiểm tra vào Google Sheets hoặc cơ sở dữ liệu.
- **Tự động gửi báo cáo**: Thêm node gửi báo cáo kiểm tra qua email hàng ngày.
- **Tích hợp với ERP/CRM**: Kết nối trực tiếp với hệ thống ERP/CRM để tự động nhập dữ liệu hợp lệ.

### 📌 Kết luận
Workflow này cung cấp một giải pháp tự động hóa kiểm tra dữ liệu nhập qua webhook với quy tắc có thể tùy chỉnh. Các sếp có thể dễ dàng tích hợp workflow này vào quy trình nhập liệu của mình để đảm bảo dữ liệu nhập vào hệ thống luôn chính xác và an toàn. Hãy áp dụng ngay để tiết kiệm thời gian và giảm thiểu rủi ro dữ liệu lỗi!