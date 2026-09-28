---
title: "📧 Xác minh địa chỉ email đơn giản với Icypeas trên n8n"
description: "Hướng dẫn tự động hóa xác minh email đơn giản với Icypeas trên n8n. Tiết kiệm thời gian và nâng cao độ chính xác trong quá trình quản lý danh sách email."
slug: "xac-minh-email-don-gian-voi-icypeas-tren-n8n"
tags: [n8n, automation, no-code, email-verification, marketing]
keywords: [n8n workflow, tự động hóa email, xác minh email, Icypeas, marketing automation]
---

# 📧 Xác minh địa chỉ email đơn giản với Icypeas trên n8n

[Các sếp] có bao giờ phải đối mặt với tình trạng danh sách email chất lượng kém do địa chỉ không tồn tại hoặc không hoạt động? Với workflow này, các sếp có thể tự động hóa quá trình xác minh email một cách đơn giản và hiệu quả, giúp tối ưu hóa danh sách email cho chiến dịch marketing.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian đáng kể trong quá trình xác minh email thủ công.
- Đảm bảo danh sách email chất lượng cao cho các chiến dịch marketing.
- Tự động hóa toàn bộ quá trình xác minh mà không cần can thiệp thủ công.
- Kết quả chính xác và đáng tin cậy từ dịch vụ Icypeas.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Icypeas (đăng ký tại [https://icypeas.com](https://icypeas.com)).
- API Key, API Secret và User ID từ tài khoản Icypeas của bạn.
- Module Crypto được kích hoạt trên instance n8n của bạn (chi tiết xem phần lưu ý dưới đây).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor của bạn.
2. Nhấp vào biểu tượng "+" ở góc trái màn hình.
3. Chọn "Import from URL".
4. Dán đường dẫn sau vào ô nhập liệu: [https://n8n.io/workflows/2011](https://n8n.io/workflows/2011).
5. Nhấp vào "Import" để hoàn tất quá trình import.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Authenticates to your Icypeas account"**:
   - Mở node này và thay thế các giá trị sau trong đoạn mã:
     ```javascript
     const API_KEY = "**PUT_API_KEY_HERE**";
     const API_SECRET = "**PUT_API_SECRET_HERE**";
     const USER_ID = "**PUT_USER_ID_HERE**";
     ```
     bằng các thông tin thực tế từ tài khoản Icypeas của bạn. Các thông tin này có thể tìm thấy trên trang profile của bạn tại [https://app.icypeas.com/bo/profile](https://app.icypeas.com/bo/profile).

2. **Node "Run email verification (single)"**:
   - Tạo một credential mới cho HTTP Header Auth:
     - Nhấp vào "Create new Credential".
     - Trong phần "Name", nhập "Authorization".
     - Trong phần "Value", chọn "expression" và nhập `{{ $json.api.key + ':' + $json.api.signature }}`.
     - Nhấp vào "Save" để lưu thay đổi.
   - Trong phần "Body Parameters", tạo một tham số mới:
     - Nhập "email" vào trường "Name".
     - Nhập địa chỉ email bạn muốn xác minh vào trường "Value".

#### 3. Kích hoạt ⚡️
1. Nhấp vào nút "Execute Workflow" để chạy workflow với dữ liệu mẫu.
2. Kiểm tra kết quả xác minh email tại [https://app.icypeas.com/bo/singlesearch?task=email-verification](https://app.icypeas.com/bo/singlesearch?task=email-verification).
3. Bật "Active" workflow để tự động hóa quá trình xác minh email.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với các node khác để tự động gửi email thông báo kết quả xác minh.
- Lưu trữ kết quả xác minh vào Google Sheets hoặc cơ sở dữ liệu để theo dõi lịch sử xác minh.
- Tự động hóa quá trình xác minh email định kỳ để duy trì danh sách email chất lượng cao.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa quá trình xác minh email một cách đơn giản và hiệu quả. Bằng cách tích hợp với Icypeas, các sếp có thể đảm bảo danh sách email chất lượng cao cho các chiến dịch marketing của mình. Hãy áp dụng ngay để tiết kiệm thời gian và nâng cao hiệu quả marketing!