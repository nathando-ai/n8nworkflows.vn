---
title: "🚀 Tự động đồng bộ dữ liệu khách hàng từ SignSnap Home sang HubSpot cùng email cảm ơn"
description: "Hướng dẫn chi tiết cách tự động đồng bộ dữ liệu khách hàng từ SignSnap Home sang HubSpot và gửi email cảm ơn tự động bằng n8n"
slug: "tu-dong-dong-bo-du-lieu-khach-hang-tu-signsnap-home-sang-hubspot"
tags: [n8n, automation, no-code, real estate, hubspot]
keywords: [n8n workflow, tự động hóa, real estate, hubspot, signsnap]
---

# 🚀 Tự động đồng bộ dữ liệu khách hàng từ SignSnap Home sang HubSpot cùng email cảm ơn

[Đoạn mở đầu: Phân tích nỗi đau thực tế của các sếp khi quản lý khách hàng từ nhiều nguồn khác nhau. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động đồng bộ dữ liệu khách hàng từ SignSnap Home sang HubSpot trong vòng vài giây
- Gửi email cảm ơn tự động cho khách hàng mới
- Tiết kiệm thời gian quản lý khách hàng thủ công
- Dữ liệu khách hàng luôn được cập nhật mới nhất
- Tăng tỷ lệ chuyển đổi khách hàng thành giao dịch
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản HubSpot với quyền truy cập API
- Tài khoản SignSnap Home
- Thiết lập SMTP để gửi email (có thể sử dụng dịch vụ email như Gmail, SendGrid...)
- Email để gửi đi (ví dụ: info@congtycuaban.com)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào trang [n8n.io/workflows/9133](https://n8n.io/workflows/9133)
2. Nhấn nút "Download" để tải file JSON về máy
3. Trong n8n Editor, nhấn vào "Import from File" và chọn file JSON vừa tải về

Hoặc bạn có thể copy/paste JSON từ trang web vào n8n Editor bằng cách:
1. Copy toàn bộ nội dung JSON từ trang web
2. Trong n8n Editor, nhấn vào "Import from Clipboard"
3. Dán nội dung JSON vào và nhấn "Import"

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node Webhook: SignSnap Home**
   - Không cần cấu hình gì thêm, chỉ cần lưu ý URL webhook sau khi kích hoạt workflow

2. **Node Parse SignSnap Data**
   - Node này đã được cấu hình sẵn, không cần thay đổi gì

3. **Node Has Email?**
   - Node này kiểm tra xem khách hàng có cung cấp email hay không
   - Không cần cấu hình gì thêm

4. **Node Create/Update HubSpot Contact**
   - Cần cấu hình credentials HubSpot:
     1. Nhấn vào biểu tượng bánh răng (credentials) bên cạnh node
     2. Chọn "Add new" và chọn "HubSpot OAuth2 API"
     3. Điền thông tin API Key và Access Token từ tài khoản HubSpot của bạn
   - Lưu ý: Các sếp cần tạo các custom properties trong HubSpot trước khi chạy workflow:
     - `last_open_house_property` (Text)
     - `last_open_house_date` (Date)
     - `has_real_estate_agent` (Dropdown)
     - `property_interest_rating` (Number)
     - `lead_score` (Number)
     - `lead_status` (Dropdown)

5. **Node Send Thank You Email**
   - Cần cấu hình credentials SMTP:
     1. Nhấn vào biểu tượng bánh răng (credentials) bên cạnh node
     2. Chọn "Add new" và chọn "SMTP"
     3. Điền thông tin SMTP từ dịch vụ email của bạn (ví dụ: Gmail, SendGrid...)
   - Cập nhật địa chỉ email gửi đi trong phần "From" của node
   - Tùy chỉnh nội dung email cảm ơn theo nhu cầu

6. **Node Log Missing Email**
   - Node này ghi lại các khách hàng không cung cấp email
   - Không cần cấu hình gì thêm

#### 3. Kích hoạt ⚡️
1. Sau khi cấu hình xong tất cả các node, nhấn vào nút "Activate" để kích hoạt workflow
2. Copy URL webhook được hiển thị sau khi kích hoạt
3. Truy cập vào trang quản lý SignSnap Home của bạn
4. Vào phần Settings → Integrations
5. Dán URL webhook vào trường tương ứng và bật tùy chọn "Send on each submission"
6. Test workflow bằng cách gửi một form mẫu từ SignSnap Home
7. Kiểm tra dữ liệu trong HubSpot và hộp thư đến của khách hàng

### ✍️ Mẹo & gợi ý nâng cao
1. **Tự động phân công cho đại lý bất động sản**
   - Thêm node để so khớp khu vực bất động sản với đại lý
   - Tự động phân công chủ sở hữu liên hệ trong HubSpot

2. **Tạo giao dịch tự động**
   - Tạo giao dịch tự động cho các khách hàng tiềm năng (điểm số ≥70)
   - Liên kết với bất động sản và liên hệ
   - Đặt giai đoạn giao dịch dựa trên điểm số

3. **Thêm vào danh sách**
   - Tạo danh sách HubSpot cho mỗi bất động sản
   - Phân đoạn theo trạng thái khách hàng
   - Sử dụng cho các chiến dịch nhắm mục tiêu

4. **Kích hoạt các quy trình HubSpot**
   - Gửi chuỗi nuôi dưỡng tự động
   - Lên lịch các nhiệm vụ theo dõi
   - Phân công cho đại lý bán hàng

5. **Thêm ảnh đính kèm**
   - Tải ảnh khách hàng lên HubSpot Files
   - Đính kèm vào hồ sơ liên hệ
   - Yêu cầu node bổ sung

6. **Theo dõi qua SMS**
   - Thêm node Twilio cho SMS tức thì
   - Song song với email
   - Tỷ lệ tương tác cao hơn

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa toàn bộ quá trình quản lý khách hàng từ SignSnap Home sang HubSpot, từ việc đồng bộ dữ liệu đến gửi email cảm ơn tự động. Với việc áp dụng workflow này, các sếp có thể tiết kiệm thời gian quý giá, đảm bảo dữ liệu khách hàng luôn được cập nhật mới nhất và tăng tỷ lệ chuyển đổi khách hàng thành giao dịch. Hãy áp dụng ngay để tối ưu hóa quy trình kinh doanh bất động sản của bạn!