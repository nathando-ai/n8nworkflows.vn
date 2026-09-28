---
title: "🚀 Tự động hóa: Upload File Google Drive lên Graph InfraNodus bằng n8n"
description: "Hướng dẫn chi tiết cách tự động upload file từ Google Drive lên InfraNodus Graph để phân tích và trực quan hóa dữ liệu văn bản một cách chuyên nghiệp."
slug: "tu-dong-hoa-upload-google-drive-len-infranodus-graph"
tags: [n8n, automation, no-code, google-drive, infranodus, ai, knowledge-graph]
keywords: [n8n workflow, tự động hóa, google drive, infranodus, knowledge graph, text analysis]
---

# 🚀 Tự động hóa: Upload File Google Drive lên Graph InfraNodus bằng n8n

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động hóa quá trình upload file từ Google Drive lên InfraNodus Graph.
- Phân tích và trực quan hóa dữ liệu văn bản một cách chuyên nghiệp.
- Tiết kiệm thời gian và công sức cho việc xử lý thủ công.
- Tạo ra các knowledge graph để hỗ trợ cho các AI agent workflows.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Drive với các file cần upload.
- Tài khoản InfraNodus để lưu trữ và phân tích dữ liệu.
- API key từ ConvertAPI (tùy chọn, để cải thiện chuyển đổi PDF).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor của bạn.
2. Click vào "Import from URL" và nhập URL sau: [https://n8n.io/workflows/4486](https://n8n.io/workflows/4486).
3. Hoặc bạn có thể tải file JSON từ link trên và import trực tiếp vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Search Google Drive"**:
   - Chọn credentials là "googleDriveOAuth2Api".
   - Điền ID của folder Google Drive bạn muốn upload file từ đó.

2. **Node "Retrieve File"**:
   - Chọn credentials là "googleDriveOAuth2Api".
   - Đảm bảo rằng operation được đặt là "download".

3. **Node "InfraNodus Save to Graph"**:
   - Chọn credentials là "httpBearerAuth".
   - Điền URL của InfraNodus API endpoint.
   - Điền tên của graph bạn muốn lưu trữ dữ liệu (nếu không có, InfraNodus sẽ tự động tạo mới).

4. **Node "Convert File to PDF" (tùy chọn)**:
   - Chọn credentials là "httpBearerAuth".
   - Điền URL của ConvertAPI endpoint.
   - Điền API key của ConvertAPI.

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu.
- Bật Active workflow.

### ✍️ Mẹo & gợi ý nâng cao
- Sử dụng ConvertAPI để cải thiện chuyển đổi PDF, đảm bảo rằng các đoạn văn bản được giữ nguyên và không bị cắt ngắn.
- Kết hợp với các node khác để gửi thông báo qua Slack/Telegram khi quá trình upload hoàn thành.
- Lưu log các file đã được upload để theo dõi và quản lý dễ dàng hơn.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa quá trình upload file từ Google Drive lên InfraNodus Graph, tạo ra các knowledge graph để hỗ trợ cho các AI agent workflows. Với việc tự động hóa này, các sếp có thể tiết kiệm thời gian và công sức cho việc xử lý thủ công, đồng thời nâng cao hiệu quả phân tích và trực quan hóa dữ liệu văn bản.