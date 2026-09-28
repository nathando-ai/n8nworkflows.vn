---
title: "🚀 Tự động hóa Triage Bug từ Video Hỗ trợ bằng WayinVideo + GPT-4o-mini + Google Sheets"
description: "Hướng dẫn tự động hóa xử lý bug từ video hỗ trợ sử dụng công nghệ AI WayinVideo và GPT-4o-mini, lưu kết quả vào Google Sheets"
slug: "tu-dong-hoa-triage-bug-tu-video-ho-tro"
tags: [n8n, automation, no-code, ai, google-sheets]
keywords: [n8n workflow, tự động hóa, xử lý bug, video hỗ trợ, gpt-4o-mini, wayinvideo]
---

# 🚀 Tự động hóa Triage Bug từ Video Hỗ trợ bằng WayinVideo + GPT-4o-mini + Google Sheets

[Các sếp] có bao giờ phải xử lý hàng trăm video báo lỗi từ khách hàng mỗi ngày không? Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình từ phát hiện lỗi trong video đến tạo ticket hỗ trợ chuyên nghiệp, chỉ với vài bước cấu hình đơn giản.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động xử lý video báo lỗi trong vòng 45 giây
- **Chính xác cao**: WayinVideo AI phát hiện chính xác thời điểm lỗi trong video
- **Ticket chuyên nghiệp**: GPT-4o-mini tạo ticket hỗ trợ có cấu trúc rõ ràng
- **Quản lý tập trung**: Tất cả ticket được lưu tự động vào Google Sheets
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản WayinVideo và API Key
- Tài khoản OpenAI và API Key
- Tài khoản Google và Google Sheet ID
- URL video báo lỗi từ khách hàng
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/14553](https://n8n.io/workflows/14553)
2. Click nút "Import" ở góc trên bên phải
3. Đặt tên workflow: "Triage video bug support tickets"
4. Click "Create" để tạo workflow mới

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "1. Form — Bug Recording + Details"**:
   - Cấu hình form với 3 trường:
     - `videoUrl`: URL video báo lỗi
     - `customerName`: Tên khách hàng
     - `bugType`: Loại bug (UI, chức năng, hiệu năng...)

2. **Nodes "2. WayinVideo — Find Bug Moments" và "4. WayinVideo — Get Bug Moments"**:
   - Thay thế `YOUR_WAYINVIDEO_API_KEY` bằng API Key thật của bạn
   - Trong tab "Authentication", chọn "Header Auth" và thêm header:
     - Key: `Authorization`
     - Value: `Bearer YOUR_WAYINVIDEO_API_KEY`

3. **Node "6a. OpenAI — Chat Model (GPT-4o-mini)"**:
   - Thêm OpenAI API Key vào credential
   - Đảm bảo chọn model `gpt-4o-mini` trong dropdown

4. **Node "7. Google Sheets — Save Bug Ticket"**:
   - Thay thế `YOUR_GOOGLE_SHEET_ID` bằng ID của Google Sheet thật
   - Thêm credential Google OAuth2
   - Cấu hình các cột trong Google Sheet:
     - `Timestamp`: Thời gian tạo ticket
     - `Customer`: Tên khách hàng
     - `Bug Type`: Loại bug
     - `Priority`: Mức độ ưu tiên (Low/Medium/High)
     - `Steps to Reproduce`: Các bước tái hiện lỗi
     - `Fix Suggestion`: Gợi ý sửa lỗi
     - `Video URL`: URL video gốc
     - `Bug Moments`: Các thời điểm lỗi trong video

#### 3. Kích hoạt ⚡️
1. Test run workflow với dữ liệu mẫu
2. Kiểm tra kết quả trong Google Sheet
3. Bật Active workflow để chạy tự động

### ✍️ Mẹo & gợi ý nâng cao
1. **Tăng số lượng bug moments**: Thay đổi tham số `limit` từ 3 lên 5 trong node "2. WayinVideo — Find Bug Moments" để bắt được nhiều lỗi hơn
2. **Nâng cấp model AI**: Thay `gpt-4o-mini` bằng `gpt-4o` trong node "6a. OpenAI — Chat Model" để có ticket chất lượng cao hơn
3. **Thông báo tức thời**: Thêm node Slack sau node "7. Google Sheets — Save Bug Ticket" để thông báo ngay khi có ticket mới
4. **Xử lý lỗi tự động**: Thêm node "Error Trigger" để xử lý các trường hợp lỗi trong quá trình chạy workflow

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa hoàn toàn quy trình xử lý bug từ video, từ phát hiện lỗi đến tạo ticket chuyên nghiệp. Với sự kết hợp của công nghệ AI WayinVideo và GPT-4o-mini, các sếp có thể tiết kiệm hàng giờ làm việc mỗi ngày và tập trung vào những công việc có giá trị hơn.

Hãy thử ngay và trải nghiệm cách làm việc thông minh hơn với n8n! 🚀