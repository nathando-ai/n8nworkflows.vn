```yaml
---
title: "🚀 Tự động đồng bộ nội dung từ Notion sang Webflow CMS với theo dõi trạng thái"
description: "Hướng dẫn tự động hóa đồng bộ nội dung từ Notion sang Webflow CMS với theo dõi trạng thái, tiết kiệm thời gian và đảm bảo tính nhất quán dữ liệu"
slug: "tu-dong-dong-bo-notion-sang-webflow-cms"
tags: [n8n, automation, no-code, notion, webflow]
keywords: [n8n workflow, tự động hóa nội dung, đồng bộ dữ liệu, webflow cms, notion api]
---
```

# 🚀 Tự động đồng bộ nội dung từ Notion sang Webflow CMS với theo dõi trạng thái

[Đoạn mở đầu: Phân tích nỗi đau thực tế của các sếp khi phải đồng bộ nội dung giữa hai nền tảng này thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động đồng bộ nội dung từ Notion sang Webflow CMS
- Theo dõi trạng thái của các mục nội dung
- Tiết kiệm thời gian và giảm lỗi thủ công
- Đảm bảo tính nhất quán dữ liệu giữa hai nền tảng
- Tự động xử lý cả việc tạo mới và cập nhật nội dung
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Notion với cơ sở dữ liệu chứa nội dung cần đồng bộ
- Tài khoản Webflow với CMS cần cập nhật
- API keys cho cả Notion và Webflow
- Biết cách truy cập và cấu hình các node trong n8n
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor của bạn
2. Nhấn vào "Import from URL" và dán link: https://n8n.io/workflows/7935
3. Hoặc tải file JSON về và import từ local

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Node "Get Notion Pages"**:
   - Cấu hình credentials cho Notion API
   - Chỉ định database ID trong Notion chứa nội dung cần đồng bộ
   - Có thể thêm các filter nếu chỉ muốn đồng bộ một phần nội dung

2. **Node "Get Webflow Items"**:
   - Cấu hình credentials cho Webflow API
   - Điền URL endpoint của Webflow CMS
   - Thiết lập các tham số query nếu cần

3. **Node "Update Webflow Item (Draft)"**:
   - Cấu hình credentials cho Webflow API
   - Điền URL endpoint của Webflow CMS
   - Thiết lập các tham số cho mục nháp

4. **Node "Create Webflow Item"**:
   - Cấu hình credentials cho Webflow API
   - Điền URL endpoint của Webflow CMS
   - Thiết lập các tham số cho mục mới

5. **Node "Get Notion Block"**:
   - Cấu hình credentials cho Notion API
   - Chỉ định block ID nếu cần lấy nội dung cụ thể

6. **Node "hold" và "Done"**:
   - Cấu hình credentials cho Notion API
   - Thiết lập các thuộc tính cần cập nhật trong Notion

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu trước khi kích hoạt
- Bật Active workflow sau khi đã cấu hình đầy đủ
- Có thể thiết lập lịch chạy tự động nếu cần

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node gửi thông báo qua Slack/Telegram khi đồng bộ hoàn thành
- Lưu log các hoạt động đồng bộ vào Google Sheets
- Thiết lập báo cáo định kỳ về tiến độ đồng bộ
- Kết hợp với các node khác để xử lý các định dạng nội dung phức tạp
- Tự động xử lý các trường hợp lỗi và gửi cảnh báo

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm thời gian đáng kể trong việc đồng bộ nội dung giữa Notion và Webflow CMS. Với khả năng theo dõi trạng thái và xử lý tự động cả việc tạo mới và cập nhật nội dung, workflow này là giải pháp hoàn hảo cho các doanh nghiệp cần duy trì tính nhất quán dữ liệu giữa hai nền tảng này. Hãy thử ngay và trải nghiệm sự tiện lợi mà tự động hóa mang lại!