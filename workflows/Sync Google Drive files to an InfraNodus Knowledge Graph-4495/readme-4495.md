---
title: "🚀 Tự động hóa: Đồng bộ file Google Drive lên Knowledge Graph của InfraNodus"
description: "Hướng dẫn chi tiết cách tự động hóa việc đồng bộ file từ Google Drive lên Knowledge Graph của InfraNodus bằng n8n, tiết kiệm thời gian và nâng cao hiệu suất làm việc."
slug: "tu-dong-hoa-dong-bo-file-google-drive-len-infranodus"
tags: [n8n, automation, no-code, google-drive, knowledge-graph]
keywords: [n8n workflow, tự động hóa, google drive, infranodus, knowledge graph]
---

# 🚀 Tự động hóa: Đồng bộ file Google Drive lên Knowledge Graph của InfraNodus

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

Các sếp có thể đã từng gặp tình trạng phải thủ công upload từng file từ Google Drive lên Knowledge Graph của InfraNodus để phân tích nội dung. Quá trình này tốn thời gian, dễ gây lỗi và không thể thực hiện liên tục. Workflow này sẽ giúp các sếp tự động hóa toàn bộ quy trình này chỉ trong vài bước đơn giản.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động hóa toàn bộ quy trình đồng bộ file từ Google Drive lên InfraNodus
- Tiết kiệm thời gian đáng kể (từ 15-30 phút/ngày tùy số lượng file)
- Đảm bảo dữ liệu luôn được cập nhật mới nhất
- Hệ thống hoạt động liên tục 24/7 mà không cần can thiệp
- Tăng hiệu suất làm việc và giảm thiểu lỗi thủ công
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Drive đã kích hoạt API
- Tài khoản InfraNodus với API key
- Các file cần đồng bộ đã được upload vào thư mục Google Drive chỉ định
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể import workflow này vào n8n bằng 2 cách:
1. **Tải file JSON**: Download file JSON từ [đây](https://n8n.io/workflows/4495) và import vào n8n Editor.
2. **Copy/Paste JSON**: Copy toàn bộ nội dung JSON từ file và paste vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Node "New File Created in the Google Folder?"**:
   - Chọn credentials là tài khoản Google Drive của các sếp
   - Điền ID của thư mục Google Drive cần theo dõi (cần tạo trước)
   - Thiết lập các trigger events (ví dụ: "create", "modify")

2. **Node "Retrieve File"**:
   - Chọn credentials là tài khoản Google Drive của các sếp
   - Đảm bảo quyền truy cập vào thư mục đã chọn

3. **Node "InfraNodus Save to Graph"**:
   - Chọn credentials là API key của tài khoản InfraNodus
   - Điền tên graph cần lưu (có thể tạo mới hoặc sử dụng graph hiện có)
   - Thiết lập các tham số xử lý trong phần body của request

4. **Node "Map PDF to Text" (tùy chọn)**:
   - Nếu sử dụng ConvertAPI, cần đăng ký tài khoản và điền API key
   - Thiết lập các tham số chuyển đổi PDF theo yêu cầu

#### 3. Kích hoạt ⚡️
- Sau khi cấu hình xong, các sếp nên test run với 1-2 file mẫu trước khi kích hoạt workflow chính thức.
- Kích hoạt workflow bằng cách bật nút Active ở góc trên bên phải của n8n Editor.

### ✍️ Mẹo & gợi ý nâng cao
- Các sếp có thể kết hợp workflow này với Slack/Telegram để nhận thông báo khi có file mới được đồng bộ thành công.
- Để quản lý tốt hơn, các sếp nên tạo một thư mục riêng cho các file cần đồng bộ và thiết lập quyền truy cập phù hợp.
- Nếu xử lý nhiều file lớn, các sếp nên cân nhắc nâng cấp tài nguyên cho VPS chạy n8n.
- Để tối ưu hiệu suất, các sếp có thể thiết lập workflow chạy theo lịch định kỳ thay vì theo sự kiện.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa hoàn toàn quá trình đồng bộ file từ Google Drive lên Knowledge Graph của InfraNodus, tiết kiệm thời gian đáng kể và đảm bảo dữ liệu luôn được cập nhật mới nhất. Hãy áp dụng ngay để nâng cao hiệu suất làm việc và giảm thiểu công việc thủ công!