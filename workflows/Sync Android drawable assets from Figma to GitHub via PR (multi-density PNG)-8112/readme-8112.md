---
title: "🚀 Tự động đồng bộ tài nguyên Android từ Figma lên GitHub qua Pull Request (multi-density PNG)"
description: "Hướng dẫn tự động hóa quy trình đồng bộ tài nguyên Android từ Figma lên GitHub qua Pull Request với n8n, tiết kiệm thời gian và giảm lỗi thủ công"
slug: "tu-dong-dong-bo-tai-nguyen-android-tu-figma-len-github-qua-pull-request"
tags: [n8n, automation, no-code, android, figma, github]
keywords: [n8n workflow, tự động hóa, android assets, figma, github pull request]
---

# 🚀 Tự động đồng bộ tài nguyên Android từ Figma lên GitHub qua Pull Request (multi-density PNG)

[Đoạn mở đầu: Phân tích nỗi đau thực tế của các sếp khi phải đồng bộ thủ công tài nguyên Android từ Figma lên GitHub. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Tự động hóa quy trình đồng bộ tài nguyên Android từ Figma lên GitHub
- Giảm lỗi: Loại bỏ các lỗi thủ công trong quá trình đồng bộ
- Tăng hiệu quả: Tự động tạo Pull Request với các tài nguyên đã được xử lý
- Tích hợp liền mạch: Kết nối Figma, GitHub và các công cụ khác trong quy trình phát triển
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Figma với quyền truy cập vào file chứa tài nguyên Android
- Tài khoản GitHub với quyền truy cập vào repository cần đồng bộ
- API keys cho Figma và GitHub
- Các thư viện và dependencies cần thiết cho các node trong workflow
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Hướng dẫn import từ file JSON hoặc copy/paste JSON vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:
- **Execute Flow (manualTrigger)**: Node kích hoạt workflow thủ công hoặc qua webhook/schedule.
- **Get Figma Export URLs (httpRequest)**: Node lấy các URL xuất Figma (PNG/SVG) từ file hoặc node cha.
- **Find Icons & Buttons (code)**: Node lọc các node theo tên hoặc loại để lấy các thành phần UI như "Icon" và "Button".
- **Predefine Drawable Folders (code)**: Node tạo danh sách các thư mục drawable của Android (mdpi, hdpi, v.v.) dưới dạng JSON.
- **Get Figma Image URLs (httpRequest)**: Node gọi API xuất Figma với các ID từ metadata đã được merge để lấy các URL xuất hình ảnh thực tế.
- **Filter Empty Image URLs (code)**: Node loại bỏ các node có URL xuất hình ảnh trống/null để tránh tải xuống hoặc commit thất bại.
- **Download Figma Images (httpRequest)**: Node tải xuống các tệp hình ảnh nhị phân từ các URL xuất cho tất cả các node đã lọc qua các mật độ.
- **Edit File Names (code)**: Node đổi tên các tệp dựa trên quy ước đặt tên (ví dụ: chữ thường, không có khoảng trắng, thêm _icon nếu cần).
- **Prepare Pull Request (httpRequest)**: Node commit tất cả các hình ảnh vào GitHub trong các thư mục thích hợp và tạo một Pull Request sạch sẽ vào nhánh chính.

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu.
- Bật Active workflow.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Telegram để thông báo khi Pull Request được tạo.
- Lưu log các hoạt động để theo dõi và gỡ lỗi.
- Gửi báo cáo định kỳ về các tài nguyên đã được đồng bộ.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa quy trình đồng bộ tài nguyên Android từ Figma lên GitHub, tiết kiệm thời gian và giảm lỗi thủ công. Hãy áp dụng ngay để nâng cao hiệu quả phát triển!