---
title: "🎬 Tự động hóa tạo video hướng dẫn nhân sự từ PDF bằng AI và n8n"
description: "Hướng dẫn tự động hóa quy trình chuyển đổi PDF nhân sự thành video hướng dẫn bằng AI, HeyGen và Google Drive. Tiết kiệm thời gian và nâng cao trải nghiệm nhân viên."
slug: "tu-dong-hoa-tao-video-huong-dan-nhan-su-tu-pdf"
tags: [n8n, automation, no-code, AI, content creation, Google Drive, HeyGen, OpenAI]
keywords: [n8n workflow, tự động hóa, AI video, nhân sự, onboarding, Google Drive, HeyGen, OpenAI]
---

# 🎬 Tự động hóa tạo video hướng dẫn nhân sự từ PDF bằng AI và n8n

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp khi phải tạo video hướng dẫn nhân sự từ PDF thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian xử lý từ 80% với quy trình tự động hoàn toàn
- Tạo nội dung chuyên nghiệp từ tài liệu PDF nhân sự
- Tự động hóa quy trình phê duyệt và phân phối video hướng dẫn
- Tăng tính cá nhân hóa cho từng nhân viên với nội dung động
- Hoạt động liên tục 24/7 mà không cần can thiệp thủ công
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Drive với quyền truy cập đầy đủ
- API key từ HeyGen và OpenAI
- Tài liệu PDF nhân sự mẫu để test workflow
- Kiến thức cơ bản về n8n và cấu hình webhook
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor của bạn
2. Nhấn vào "Import from URL" và dán link workflow gốc: https://n8n.io/workflows/11735
3. Hoặc tải file JSON về và import từ local

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Webhook - Receive Policy PDF** (Node: Webhook - Receive Policy PDF)
   - Đảm bảo đường dẫn webhook là `hr-onboarding-upload`
   - Kiểm tra phương thức HTTP là POST

2. **Google Drive Credentials** (Nodes: Upload Video to Google Drive, Download file1)
   - Thêm credentials Google Drive OAuth2
   - Cấu hình quyền truy cập đầy đủ cho tài khoản

3. **HeyGen API Configuration** (Nodes: Check HeyGen Video Status, Create HeyGen Video Task1)
   - Thêm API key từ HeyGen
   - Thay thế placeholder IDs cho avatar và voice

4. **OpenAI Configuration** (Nodes: OpenAI Chat Model, OpenAI Chat Model1)
   - Thêm API key từ OpenAI
   - Đảm bảo model được chọn là `gpt-4.1-mini`

5. **Memory Nodes** (Nodes: Simple Memory, Simple Memory1)
   - Cấu hình kích thước bộ nhớ phù hợp với tài liệu PDF
   - Thiết lập thời gian lưu trữ dữ liệu tạm thời

#### 3. Kích hoạt ⚡️
1. Test run với tài liệu PDF mẫu
2. Kiểm tra từng bước xử lý từ extract text đến tạo video
3. Bật Active workflow sau khi xác nhận hoạt động ổn định

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Teams để thông báo khi video hoàn thành
- Thêm bước lưu log xử lý để theo dõi hiệu suất
- Tạo báo cáo định kỳ về số lượng video đã tạo
- Tích hợp với hệ thống HR để tự động kích hoạt workflow khi có tài liệu mới

### 📌 Kết luận
Workflow này biến đổi quy trình tạo video hướng dẫn nhân sự từ một công việc thủ công tốn thời gian thành một quy trình tự động hoàn toàn. Với khả năng tích hợp AI và các dịch vụ chuyên nghiệp như HeyGen và Google Drive, các sếp có thể tạo nội dung chất lượng cao một cách nhanh chóng và hiệu quả. Hãy thử ngay và nâng cao trải nghiệm nhân viên của bạn!