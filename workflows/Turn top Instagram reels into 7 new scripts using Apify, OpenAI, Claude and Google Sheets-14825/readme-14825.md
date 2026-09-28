---
title: "🚀 Tự động hóa: Chuyển đổi Top Reels Instagram thành 7 kịch bản mới bằng Apify, OpenAI, Claude và Google Sheets"
description: "Hướng dẫn tự động hóa 100% không cần code để phân tích top reels Instagram, chuyển đổi thành kịch bản mới và lưu vào Google Sheets - tiết kiệm 80% thời gian soạn thảo nội dung"
slug: "tu-dong-hoa-instagram-reels-sang-kich-ban-moi"
tags: [n8n, automation, no-code, content-creation, ai-tools]
keywords: [n8n workflow, tự động hóa nội dung, AI content creation, Instagram analytics, Google Sheets automation]
---

# 🚀 Tự động hóa: Chuyển đổi Top Reels Instagram thành 7 kịch bản mới bằng Apify, OpenAI, Claude và Google Sheets

[Các sếp] có biết không? Với workflow này, các sếp có thể tiết kiệm tới 80% thời gian soạn thảo nội dung khi chuyển đổi top reels Instagram thành 7 kịch bản mới hoàn chỉnh, chỉ trong vài phút!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Chuyển đổi từ 10-15 phút thành 2-3 phút
- **Nội dung cá nhân hóa**: Phân tích và tạo kịch bản phù hợp với thương hiệu
- **Chính xác cao**: Sử dụng AI để đảm bảo chất lượng nội dung
- **Hoạt động liên tục**: Tự động hóa hoàn toàn không cần can thiệp
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Apify (để crawl dữ liệu Instagram)
- API key OpenAI (để transcribe audio)
- API key Anthropic (để tạo kịch bản mới)
- Google Sheets OAuth (để lưu kết quả)
- URL profile Instagram cần phân tích
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [workflow gốc trên n8n.io](https://n8n.io/workflows/14825)
2. Click "Copy JSON" và lưu file JSON vào máy
3. Trong n8n Editor, click "Import from File" và chọn file JSON đã lưu

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Run an Actor"**:
   - Thêm credentials Apify
   - Thay đổi URL profile Instagram trong input data

2. **Node "Transcribe a recording"**:
   - Thêm credentials OpenAI
   - Đảm bảo có đủ credit trong tài khoản OpenAI

3. **Node "Message a model"**:
   - Thêm credentials Anthropic
   - Có thể điều chỉnh prompt trong node để phù hợp với thương hiệu

4. **Node "Append row in sheet"**:
   - Thêm credentials Google Sheets
   - Tạo trước các cột: Script Number, Hook, Problem, Solution, How To Implement, CreatedAt, Source
   - Chọn đúng spreadsheet và worksheet đích

#### 3. Kích hoạt ⚡️
1. Click "Execute workflow" để test với dữ liệu mẫu
2. Sau khi test thành công, click "Activate" để bật workflow

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Teams để nhận thông báo khi workflow hoàn thành
- Lưu log hoạt động vào Google Sheets để theo dõi hiệu suất
- Tạo báo cáo định kỳ từ dữ liệu trong Google Sheets
- Kết hợp với workflow khác để tự động đăng bài lên Instagram

### 📌 Kết luận
Với workflow này, các sếp có thể:
1. Phân tích top reels Instagram một cách tự động
2. Tạo 7 kịch bản mới hoàn chỉnh chỉ trong vài phút
3. Lưu kết quả vào Google Sheets để quản lý dễ dàng
4. Tiết kiệm tới 80% thời gian soạn thảo nội dung

Hãy áp dụng ngay để tăng tốc quá trình tạo nội dung và giữ chân khách hàng với nội dung hấp dẫn hơn! 🚀