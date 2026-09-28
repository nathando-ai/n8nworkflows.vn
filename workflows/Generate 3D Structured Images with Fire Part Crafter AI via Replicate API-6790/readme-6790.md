---
title: "🚀 Tự động tạo mô hình 3D cấu trúc từ ảnh 2D với Fire Part Crafter AI qua Replicate API trên n8n"
description: "Hướng dẫn cài đặt và sử dụng workflow n8n tự động hóa việc biến ảnh 2D thành mô hình 3D đa phần (multi-part 3D mesh) sử dụng mô hình Fire Part Crafter AI trên Replicate."
slug: "tao-mo-hinh-3d-tu-anh-2d-voi-fire-part-crafter-replicate-n8n"
tags: [n8n, automation, no-code, replicate, ai-3d, image-generation]
keywords: [n8n workflow, part-crafter ai, replicate api, tạo mô hình 3d tự động, tự động hóa n8n, 3d mesh generation]
---

# 🚀 Tự động tạo mô hình 3D cấu trúc từ ảnh 2D với Fire Part Crafter AI qua Replicate API

Chào các sếp! Việc chuyển đổi các ý tưởng hoặc hình ảnh 2D thông thường thành các mô hình 3D có cấu trúc (3D mesh) thường đòi hỏi rất nhiều công sức thủ công hoặc các phần mềm đồ họa chuyên dụng nặng nề. Với sự bùng nổ của AI đa phương thức (Multimodal AI), chúng ta hoàn toàn có thể tự động hóa quy trình này.

Workflow n8n này sẽ giúp các sếp kết nối trực tiếp với mô hình **Fire Part Crafter** thông qua **Replicate API**. Hệ thống sẽ tự động gửi ảnh đầu vào, theo dõi trạng thái xử lý (polling status với logic chờ thông minh) và trả về kết quả mô hình 3D hoàn chỉnh một cách hoàn toàn tự động!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn**: Biến ảnh RGB thành mô hình 3D đa phần mà không cần thao tác thủ công trên giao diện web của Replicate.
- **Xử lý thông minh**: Tích hợp vòng lặp kiểm tra trạng thái (`Wait`, `Check Status`, `If`) giúp theo dõi tiến trình tạo ảnh và xử lý lỗi linh hoạt.
- **Giám sát chặt chẽ**: Ghi log mọi request giúp các sếp dễ dàng debug khi gặp sự cố.
- **Tiết kiệm thời gian**: Tối ưu hóa quy trình sản xuất nội dung 3D cho các nhà sáng tạo, marketer và nhà thiết kế.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một hệ thống **n8n** đang hoạt động (Cloud hoặc Self-hosted).
- Tài khoản trên **[Replicate](https://replicate.com)** và lấy sẵn **Replicate API Token**.
- Hình ảnh đầu vào (định dạng URL công khai) để đưa vào mô hình PartCrafter.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow hoặc copy toàn bộ mã JSON từ template gốc.
- Trong giao diện n8n Editor, chọn **Add workflow** -> **Import from File** hoặc dán trực tiếp vào vùng làm việc.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 13 nodes, trong đó các sếp cần chú ý cấu hình kỹ các điểm sau:
- **Set API Token**: Mở node này và thay thế chuỗi `'YOUR_REPLICATE_API_TOKEN'` bằng mã API Token thực tế từ tài khoản Replicate của các sếp.
- **Set Image Parameters**: Cấu hình các tham số đầu vào cho mô hình:
  - `image`: Đường dẫn URL của bức ảnh 2D muốn chuyển đổi.
  - `num_parts`: Số lượng các phần/đối tượng muốn tạo (Mặc định: 16).
  - `guidance_scale`: Độ bám sát prompt/ảnh (Mặc định: 7).
  - `remove_background`: Bật/tắt tính năng xóa phông ảnh gốc (`True`/`False`).
- **Create Image Prediction & Check Status**: Hai node `httpRequest` này gọi trực tiếp đến endpoint `https://api.replicate.com/v1/predictions` của Replicate, đảm bảo API Token ở bước trên đã được truyền đúng biến.

#### 3. Kích hoạt ⚡️
- Nhấn nút **Execute Workflow** tại node **Manual Trigger** để chạy thử nghiệm với dữ liệu mẫu.
- Theo dõi các nhánh **Is Complete?** và **Has Failed?** để đảm bảo quá trình gọi API diễn ra suôn sẻ.
- Sau khi test thành công, bật công tắc **Active** góc trên bên phải để kích hoạt workflow chạy tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết nối thông báo**: Thêm node Telegram hoặc Slack ở nhánh **Success Response** để nhận thông báo và link kết quả ngay lập tức về điện thoại.
- **Lưu trữ dữ liệu**: Đẩy kết quả trả về (URL của mô hình 3D) vào **Google Sheets** hoặc Airtable để quản lý kho tài nguyên 3D của doanh nghiệp.
- **Mở rộng Trigger**: Thay thế `Manual Trigger` bằng `Webhook` hoặc `Google Drive Trigger` để tự động biến bất kỳ ảnh nào mới tải lên thành mô hình 3D.

### 📌 Kết luận
Với workflow n8n tích hợp Fire PartCrafter AI này, việc tạo mô hình 3D từ ảnh 2D nay đã được tự động hóa tối đa, giúp các sếp tiết kiệm hàng giờ thao tác thủ công. Hãy import ngay vào hệ thống n8n của các sếp và bắt đầu sáng tạo những mô hình 3D ấn tượng!