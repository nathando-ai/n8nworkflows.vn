---
title: "🎬 Tự động hóa Video: Tạo Summary, Clip và Transcript từ bất kỳ video nào với WayinVideo AI"
description: "Hướng dẫn tự động hóa hoàn chỉnh để chuyển đổi bất kỳ video thành summary, clip viral và transcript đầy đủ chỉ với 1 lần submit"
slug: "tu-dong-hoa-video-voi-wayinvideo-ai"
tags: [n8n, automation, no-code, video-processing, ai-content]
keywords: [n8n workflow, tự động hóa video, wayinvideo, ai summary, video transcript]
---

# 🎬 Tự động hóa Video: Tạo Summary, Clip và Transcript từ bất kỳ video nào với WayinVideo AI

[Các sếp] có bao giờ phải tốn hàng giờ để xem lại video dài, tóm tắt nội dung, tìm clip hay và chuyển đổi nội dung thành văn bản? Với workflow này, các sếp có thể tự động hóa toàn bộ quá trình này chỉ với 1 lần submit URL video.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động xử lý video trong khi các sếp làm việc khác
- **Nội dung chất lượng cao**: Summary chuyên nghiệp, clip viral tự động và transcript chính xác
- **Tự động hóa hoàn chỉnh**: Không cần can thiệp thủ công sau khi submit
- **Báo cáo định kỳ**: Nhận email đầy đủ với tất cả kết quả xử lý
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản WayinVideo và API Key (để submit và poll các task)
- Tài khoản Gmail và OAuth2 credential (để gửi email báo cáo)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/14714](https://n8n.io/workflows/14714)
2. Click "Import" và chọn "Import from URL"
3. Hoặc copy toàn bộ JSON workflow và paste vào n8n Editor

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **WayinVideo Submit nodes (3, 4, 5)**:
   - Thay thế `YOUR_WAYINVIDEO_API_KEY` trong Authorization header bằng API Key thật của các sếp
   - Đảm bảo các sếp đã kích hoạt các dịch vụ cần thiết trong tài khoản WayinVideo

2. **WayinVideo Poll nodes (9, 10, 11)**:
   - Thay thế `YOUR_WAYINVIDEO_API_KEY` trong Authorization header bằng API Key thật của các sếp

3. **Gmail node (16)**:
   - Thay thế `YOUR_RECIPIENT_EMAIL` bằng địa chỉ email nhận báo cáo
   - Kết nối với Gmail OAuth2 credential của các sếp

#### 3. Kích hoạt ⚡️
1. Test run với URL video mẫu (ví dụ: video giới thiệu sản phẩm)
2. Kiểm tra email để đảm bảo nhận được báo cáo đầy đủ
3. Bật Active workflow sau khi xác nhận mọi thứ hoạt động tốt

### ✍️ Mẹo & gợi ý nâng cao
1. **Kết hợp với Slack/Teams**: Thêm node để gửi báo cáo đến kênh Slack/Teams của nhóm
2. **Lưu trữ kết quả**: Kết nối với Google Drive để lưu trữ các file kết quả
3. **Xử lý hàng loạt**: Sử dụng node "Loop Over Items" để xử lý nhiều video cùng lúc
4. **Báo cáo định kỳ**: Thiết lập workflow chạy tự động mỗi ngày với các video mới nhất

### 📌 Kết luận
Workflow này biến đổi cách các sếp làm việc với video. Từ việc phải tốn hàng giờ để xử lý thủ công, các sếp giờ đây chỉ cần submit URL video và nhận được summary, clip viral và transcript đầy đủ trong email. Hãy thử ngay và tiết kiệm thời gian quý giá cho các sếp!