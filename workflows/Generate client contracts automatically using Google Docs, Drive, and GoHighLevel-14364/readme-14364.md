---
title: "🚀 Tự động hóa tạo hợp đồng khách hàng với Google Docs, Drive và GoHighLevel"
description: "Hướng dẫn xây dựng workflow n8n tự động tạo hợp đồng từ template Google Docs, chuyển đổi sang PDF và đồng bộ trực tiếp lên CRM GoHighLevel."
slug: "tu-dong-hoa-tao-hop-dong-khach-hang-n8n-google-docs-gohighlevel"
tags: [n8n, automation, no-code, google-docs, gohighlevel, crm]
keywords: [n8n workflow, tự động hóa hợp đồng, google docs api, gohighlevel integration, tạo hợp đồng tự động]
---

# 🚀 Tự động hóa tạo hợp đồng khách hàng với Google Docs, Drive và GoHighLevel

Việc soạn thảo hợp đồng thủ công cho từng khách hàng mới thường ngốn rất nhiều thời gian: nào là copy file mẫu, sửa tên, chỉnh sửa phạm vi công việc, tính toán chi phí, xuất ra PDF rồi lại tải lên CRM. Chỉ một sơ suất nhỏ cũng có thể dẫn đến sai sót thông tin quan trọng.

Được thiết kế bởi chuyên gia **Rahul Joshi**, workflow n8n này sẽ giải quyết triệt để vấn đề trên bằng cách tự động hóa 100% quy trình: Nhận dữ liệu từ Webhook $\rightarrow$ Nhân bản template hợp đồng $\rightarrow$ Điền thông tin khách hàng $\rightarrow$ Xuất file PDF $\rightarrow$ Đồng bộ lên GoHighLevel và tự động dọn dẹp file tạm trên Google Drive. Tất cả chỉ diễn ra trong vài giây!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không còn cảnh copy-paste thủ công từng điều khoản hợp đồng.
- **Loại bỏ sai sót:** Dữ liệu được đồng bộ chính xác từ hệ thống sang văn bản theo chuẩn template có sẵn.
- **Tự động hóa toàn diện:** File PDF hợp đồng tự động xuất hiện trong GoHighLevel, sẵn sàng gửi cho khách hàng.
- **Không rác hệ thống:** Tự động xóa các file tạm trên Google Drive ngay sau khi hoàn thành quy trình.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt sẵn (Self-hosted hoặc Cloud).
- **Google Drive & Google Docs Account:** Cần tạo sẵn OAuth2 Credentials để n8n có thể đọc/ghi file.
- **GoHighLevel (GHL) Account:** Chuẩn bị API Key/Bearer Token để tải file PDF lên hệ thống.
- **Webhook Source:** Nguồn gửi dữ liệu (Form trên web, hệ thống CRM khác, hoặc Make/Zapier).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow hoặc copy trực tiếp mã nguồn.
- Mở n8n Editor, chọn **Add workflow** -> Nhấn `Ctrl + V` (hoặc `Cmd + V`) để dán toàn bộ workflow lên canvas.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 6 nodes chính, các sếp cần cấu hình kỹ các điểm sau:

- **Receive Contract Request (`webhook`):** Node này nhận dữ liệu dạng POST (gồm `full_name`, `date`, `scope_of_works`, `pc_items`, `subtotal`, `gst`, `total`). Hãy copy Webhook URL này để cấu hình cho form hoặc hệ thống gọi đến.
- **Copy Master Template (`googleDrive`):** 
  - Kết nối `Google Drive OAuth2 Api`.
  - Cấu hình ID của file mẫu (Master Template) trên Google Drive để hệ thống tiến hành nhân bản.
- **Populate Contract with Client Data (`googleDocs`):**
  - Kết nối `Google Docs OAuth2 Api`.
  - Cấu hình thao tác cập nhật (update) nội dung dựa trên dữ liệu từ Webhook truyền vào.
- **Download Contract as PDF (`googleDrive`):**
  - Tải file Google Docs vừa điền thông tin dưới định dạng file PDF.
- **Upload PDF to GoHighLevel (`httpRequest`):**
  - Thay thế Bearer Token mẫu bằng **API Key/Token thực tế** của tài khoản GoHighLevel để đẩy file PDF lên mục Media của CRM.
- **Delete Temp Copy from Drive (`googleDrive`):**
  - Node này tự động xóa bản sao Google Docs tạm thời sau khi đã chuyển đổi thành công sang PDF, giúp Google Drive luôn gọn gàng.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và gửi một Payload giả lập đến Webhook để test thử toàn bộ luồng.
- Kiểm tra kết quả xem file PDF đã vào GoHighLevel chưa và file tạm trên Drive đã bị xóa sạch chưa.
- Nếu mọi thứ mượt mà, gạt công tắc sang **Active** để chính thức vận hành tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Nối thêm một node **Slack** hoặc **Telegram** ở cuối luồng để gửi thông báo về nhóm nội dung: *"Hợp đồng của khách hàng [Tên] đã được tạo và đẩy lên GHL thành công!"*.
- **Lưu trữ backup:** Thay vì xóa hoàn toàn file trên Google Drive, các sếp có thể đổi action thành chuyển file đó vào một thư mục "Archive" riêng nếu muốn lưu lịch sử.
- **Gửi email tự động:** Thêm node **Gmail** hoặc **SendGrid** để tự động gửi bản PDF hợp đồng đó trực tiếp đến email khách hàng ngay sau khi tạo xong.

### 📌 Kết luận
Tự động hóa quy trình tạo hợp đồng không chỉ giúp doanh nghiệp tăng tốc độ chốt sale mà còn thể hiện sự chuyên nghiệp trong mắt khách hàng. Hãy triển khai ngay workflow này vào hệ thống n8n của các sếp để tối ưu hóa thời gian vận hành ngay hôm nay!