---
title: "🚀 Tự động hóa Import Workflows và Map Credentials trong n8n bằng Multi-Form"
description: "Hướng dẫn chi tiết sử dụng workflow n8n để import workflow và tự động ánh xạ (map) credentials giữa các instance n8n thông qua giao diện Multi-Form trực quan."
slug: "import-workflows-and-map-credentials-using-multi-form"
tags: [n8n, automation, no-code, migration, credentials, multi-form]
keywords: [n8n workflow, import workflow n8n, map credentials n8n, migration n8n, n8n multi-form]
---

# 🚀 Tự động hóa Import Workflows và Map Credentials trong n8n bằng Multi-Form

Việc chuyển đổi (migrate) các workflow và cấu hình lại các credentials (thông tin xác thực) thủ công giữa các môi trường n8n (như từ Test sang Production, hoặc giữa các instance khác nhau) thường tốn rất nhiều thời gian và dễ xảy ra sai sót. Các sếp thường phải mất công tải file JSON lên, dò xem node nào dùng credential gì, rồi tạo lại từng cái từ đầu.

Workflow này ra đời để giải quyết triệt để bài toán đó! Với giao diện **Multi-Form** trực quan, hệ thống sẽ tự động phân tích file, trích xuất thông tin, cho phép các sếp chọn instance đích, ánh xạ credentials cũ sang mới một cách thông minh và tạo mới workflow chỉ trong vài cú click.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow xử lý mượt mà và chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Không cần thủ công mở từng workflow để đổi credential khi migrate.
- **Tránh nhầm lẫn:** Tự động lọc và map đúng tên credential tương ứng trong hệ thống đích.
- **Linh hoạt đa môi trường:** Dễ dàng quản lý và chuyển đổi workflow qua lại giữa nhiều instance n8n khác nhau.
- **Trải nghiệm mượt mà:** Tương tác hoàn toàn qua form giao diện Web (Multi-Form) thân thiện.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một instance n8n đang hoạt động (Self-hosted hoặc Cloud).
- **n8n API Credentials**: Để kết nối và tạo workflow/credentials tự động qua API.
- File JSON chứa danh sách các instance n8n (theo mẫu config bên dưới) hoặc file workflow cần import.
:::

---
## ⚙️ Cấu hình Instances mẫu
Mỗi instance cần cung cấp các thông tin cơ bản:
```json
[
  {
    "name": "n8n-test",
    "apiKey": "XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX",
    "baseUrl": "https://n8n-test.example.com/api/v1"
  }
]
```
---

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Sao chép toàn bộ mã JSON của workflow này.
- Mở n8n Editor của các sếp, chọn **Add workflow** -> **Import from Clipboard** và dán vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **On form submission / Upload File / Choose Instance / Choose Workflow / Map Credentials**: Đây là chuỗi các node Form giao diện. Các sếp có thể bật tính năng bảo mật (như Basic Auth) cho các Form này nếu cần thiết để bảo vệ dữ liệu nội bộ.
- **Create Workflow & Create Empty Credentials**: Cần cấu hình **n8nApi** credentials trỏ đến API key của instance đích mà các sếp muốn import workflow vào.
- **Các node Code & Filter / Split Out**: Xử lý logic bóc tách danh sách node, lọc các node có chứa credentials và tạo tùy chọn ánh xạ theo tên cũ/mới. Các sếp giữ nguyên logic JavaScript có sẵn trong các node Code này vì đã được tối ưu hóa toàn diện.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute workflow** và mở thử URL của form đầu tiên để test quá trình nhập liệu.
- Sau khi kiểm tra mọi bước chạy trơn tru, hãy bật công tắc **Active** để chính thức đưa workflow vào vận hành.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo**: Gắn thêm node Telegram hoặc Slack ở node **Success** hoặc **Error** để nhận thông báo tức thì mỗi khi có ai đó import workflow thành công.
- **Log lịch sử**: Lưu lại nhật ký import vào Google Sheets hoặc Notion để dễ dàng kiểm tra ai đã chuyển đổi workflow nào và vào thời gian nào.
- **Bảo mật Form**: Luôn bật chế độ xác thực (Basic Authentication) cho các form n8n để tránh người ngoài truy cập trái phép vào công cụ migrate hệ thống.

### 📌 Kết luận
Workflow **Import workflows and map their credentials using a Multi-Form** là một "vũ khí" cực kỳ lợi hại cho các DevOps, System Admin hoặc Freelancer n8n thường xuyên phải quản lý nhiều hệ thống khác nhau. Hãy áp dụng ngay để tối ưu hóa quy trình làm việc và giải phóng bản thân khỏi những tác vụ thủ công nhàm chán!