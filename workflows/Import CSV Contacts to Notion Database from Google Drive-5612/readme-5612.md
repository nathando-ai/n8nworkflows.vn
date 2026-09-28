---
title: "🚀 Tự động đồng bộ danh bạ CSV từ Google Drive lên Notion Database bằng n8n"
description: "Hướng dẫn chi tiết cách tự động hóa quy trình nhập danh bạ khách hàng từ file CSV trên Google Drive vào cơ sở dữ liệu Notion một cách nhanh chóng và chính xác."
slug: "import-csv-contacts-notion-google-drive-n8n"
tags: [n8n, automation, crm, notion, google-drive, no-code]
keywords: [n8n workflow, import csv notion, google drive to notion, tự động hóa crm, n8n tiếng việt]
---

# 🚀 Tự động đồng bộ danh bạ CSV từ Google Drive lên Notion Database

Các sếp có đang đau đầu mỗi khi nhận được một danh sách khách hàng mới dưới định dạng file CSV từ các chiến dịch Marketing, rồi phải cặm cụi copy-paste thủ công từng dòng vào Notion CRM không? Công việc nhàm chán này không chỉ ngốn hàng giờ đồng hồ mà còn dễ dẫn đến sai sót, nhầm lẫn thông tin liên lạc của khách hàng tiềm năng.

Đừng lo, với workflow n8n tự động hóa này, các sếp chỉ cần ném file CSV lên Google Drive, mọi việc còn lại hãy để hệ thống lo. Giải pháp giúp tự động hóa 100% quy trình đồng bộ dữ liệu mà không cần biết lập trình!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không còn cảnh nhập liệu thủ công từng dòng liên hệ vào Notion.
- **Độ chính xác tuyệt đối:** Tránh bỏ sót hoặc gõ sai tên, email, số điện thoại của khách hàng.
- **Quản lý tập trung:** Toàn bộ dữ liệu khách hàng từ file CSV được cập nhật gọn gàng vào Notion Database ngay lập tức.
- **Linh hoạt mở rộng:** Dễ dàng tùy chỉnh các trường dữ liệu (properties) trích xuất từ file CSV sang Notion theo nhu cầu thực tế của doanh nghiệp.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi bắt đầu "lên đồ", các sếp cần chuẩn bị sẵn các tài nguyên sau:
- **Tài khoản n8n:** Đã hoạt động (Cloud hoặc Self-hosted).
- **Tài khoản Google Drive:** Đã có sẵn file CSV chứa danh bạ liên hệ.
- **Tài khoản Notion:** Đã chuẩn bị sẵn một Database để lưu trữ thông tin liên hệ.
- **Credentials:**
  - Google Drive OAuth2 API (để cấp quyền đọc file).
  - Notion API Integration (để cấp quyền ghi dữ liệu vào database).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tạo một workflow mới trên n8n, sau đó copy toàn bộ mã JSON của workflow này (hoặc tải file JSON từ nguồn cấp) và dán trực tiếp vào giao diện n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này bao gồm 5 nodes chính, các sếp cần cấu hình kỹ các điểm sau:

- **Node `Download file` (Google Drive):**
  - Chọn hoặc tạo mới **Credentials** cho Google Drive.
  - Điền **File ID** của file CSV danh bạ mà các sếp muốn đồng bộ từ Google Drive của mình.
- **Node `Extract from File`:**
  - Node này có nhiệm vụ đọc và phân tích cấu trúc file CSV vừa tải về. Các sếp giữ nguyên thiết lập mặc định hoặc cấu hình lại nếu file CSV có định dạng đặc biệt (dấu phân cách, mã hóa UTF-8...).
- **Node `Code`:**
  - Xử lý dữ liệu thô từ file CSV chuyển thành định dạng chuẩn mà Notion yêu cầu. Hiện tại workflow đang xử lý 4 trường thông tin cơ bản: **Họ tên (full name), Email, Số điện thoại (phone), và Công ty (company)**. Các sếp có thể tùy chỉnh đoạn code này nếu muốn lấy thêm các trường khác.
- **Node `Create a database page` (Notion):**
  - Chọn **Credentials** kết nối tới Notion Workspace của các sếp.
  - Chọn **Database** đích đã tạo sẵn trên Notion.
  - Map (ánh xạ) các trường dữ liệu từ bước Code vào đúng các Properties tương ứng trong Notion Database.

#### 3. Kích hoạt ⚡️
- Nhấn nút **"Execute Workflow"** thông qua node `When clicking ‘Execute workflow’` để test thử nghiệm với dữ liệu mẫu.
- Kiểm tra lại trên Notion Database xem dữ liệu đã đổ về đầy đủ và chính xác chưa.
- Nếu mọi thứ mượt mà, hãy bật công tắc **Active** để workflow sẵn sàng hoạt động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tự động hóa hoàn toàn:** Thay vì dùng Trigger thủ công (`When clicking ‘Execute workflow’`), các sếp có thể thay thế bằng node **Google Drive Trigger** để workflow tự động chạy ngay khi có một file CSV mới được tải lên thư mục chỉ định.
- **Thông báo kết quả:** Thêm một node **Slack** hoặc **Telegram** ở cuối workflow để gửi thông báo về số lượng contact đã được import thành công vào nhóm chat nội bộ.
- **Xử lý trùng lặp:** Tích hợp thêm bước kiểm tra email đã tồn tại trong Notion trước khi tạo trang mới để tránh việc bị duplicate dữ liệu liên hệ.

### 📌 Kết luận
Việc tự động hóa quy trình nhập liệu danh bạ từ CSV lên Notion chưa bao giờ dễ dàng đến thế với n8n. Hãy áp dụng ngay hôm nay để giải phóng thời gian cho đội ngũ sales và CSKH, giúp họ tập trung vào việc chốt đơn thay vì nhập dữ liệu thủ công!