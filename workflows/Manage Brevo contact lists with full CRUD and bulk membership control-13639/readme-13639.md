---
title: "🚀 Quản lý danh sách liên hệ Brevo toàn diện với CRUD và Bulk Membership trong n8n"
description: "Hướng dẫn tích hợp đầy đủ các API quản lý Contact List của Brevo vào n8n giúp tự động hóa CRUD, phân loại nhóm và thêm/xóa contact hàng loạt."
slug: "quan-ly-danh-sach-lien-he-brevo-n8n"
tags: [n8n, automation, no-code, brevo, marketing-automation, crm]
keywords: [n8n workflow, brevo api, quản lý contact brevo, tự động hóa marketing, n8n http request]
---

# 🚀 Quản lý danh sách liên hệ Brevo toàn diện với CRUD và Bulk Membership trong n8n

Việc quản lý các danh sách liên hệ (Contact Lists) trên Brevo (trước đây là Sendinblue) theo cách thủ công đôi khi gặp nhiều giới hạn khi các node mặc định của n8n chưa hỗ trợ đầy đủ các tính năng nâng cao. Nếu các sếp đang đau đầu vì không thể dễ dàng tạo, sửa, xóa danh sách hay quản lý thành viên hàng loạt (bulk add/remove) một cách tự động, thì đây chính là "vũ khí tối thượng" dành cho các sếp.

Workflow này cung cấp bộ khung hoàn chỉnh sử dụng các HTTP Request kết nối trực tiếp với Brevo API, giúp các sếp thực hiện trọn vẹn các thao tác CRUD và điều phối thành viên trong danh sách một cách mượt mà, tự động hóa 100% không cần code phức tạp.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa toàn diện CRUD:** Dễ dàng tạo, xem chi tiết, cập nhật (đổi tên/thư mục) và xóa danh sách liên hệ trên Brevo.
- **Quản lý thành viên hàng loạt (Bulk):** Thêm hoặc xóa hàng loạt contact khỏi danh sách thông qua email hoặc ID cực kỳ nhanh chóng.
- **Xử lý phân trang thông minh:** Các node Aggregate và HTTP Request hỗ trợ tự động gom dữ liệu từ nhiều trang (pagination) trả về kết quả gộp hoàn chỉnh.
- **Linh hoạt tích hợp:** Dễ dàng ghép nối workflow này với CRM, Google Sheets, biểu mẫu đăng ký hoặc hệ thống chatbot của doanh nghiệp.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản n8n (Cloud hoặc Self-hosted).
- Tài khoản [Brevo](https://n8nplaybook.com/go/brevo/) và lấy **Brevo API Key** (Sendinblue API).
- Credentials loại `sendInBlueApi` được cấu hình sẵn trong n8n để xác thực với các HTTP Request nodes.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow từ [n8n template gốc](https://n8n.io/workflows/13639) hoặc sao chép mã JSON và dán trực tiếp vào n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Vì workflow này tập hợp các API Endpoints nâng cao của Brevo, các sếp cần chú ý cấu hình kỹ các node sau:
- **Credentials chung (`sendInBlueApi`):** Gắn API Key của tài khoản Brevo vào toàn bộ các HTTP Request nodes (*Get All Lists, Create a List, Update a List, Get a List’s Details, Delete a List, Get Contacts in a List, Add Existing Contacts to a List, Delete Contacts from a List*).
- **Tham số đường dẫn (`listId`):** Ở các node như *Get a List’s Details, Update a List, Delete a List, Get Contacts in a List, Add Existing Contacts to a List, Delete Contacts from a List*, hãy đảm bảo điền chính xác `listId` tương ứng trên Brevo vào phần Path Parameters.
- **Body JSON cho Bulk Actions:** 
  - Tại node **Add Existing Contacts to a List**: Cấu hình body chứa mảng `emails` (tối đa 150 email trong một request) hoặc `ids`/`extIds`.
  - Tại node **Delete Contacts from a List**: Cấu hình tương tự để chỉ định các contact cần loại bỏ khỏi danh sách mà không xóa hẳn khỏi hệ thống database chính.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (Test run) từng node đơn lẻ để kiểm tra kết nối API trả về dữ liệu thành công.
- Sau khi mọi thứ hoạt động trơn tru, bật trạng thái **Active workflow** để hệ thống tự động vận hành.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết nối Google Sheets / Airtable:** Tự động đồng bộ danh sách khách hàng mới từ file Excel/Google Sheets lên thẳng một List cụ thể trên Brevo thông qua node *Add Existing Contacts to a List*.
- **Thông báo qua Telegram/Slack:** Thiết lập thêm node gửi tin nhắn cảnh báo mỗi khi một List mới được tạo thành công hoặc khi xảy ra lỗi API.
- **Báo cáo định kỳ:** Kết hợp node *Get Contacts in a List* và *Aggregate Contacts Pages* để thống kê số lượng thành viên trong từng chiến dịch và gửi báo cáo về email hoặc Slack hàng tuần.

### 📌 Kết luận
Bộ template quản lý danh sách Brevo này là mảnh ghép hoàn hảo giúp tối ưu hóa quy trình Email Marketing và CRM của doanh nghiệp. Hãy áp dụng ngay vào hệ thống n8n để tiết kiệm hàng giờ thao tác thủ công mỗi ngày!