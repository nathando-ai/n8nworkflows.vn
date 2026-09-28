```yaml
---
title: "💬 Tự động hóa nhóm WhatsApp hàng ngày với GPT-4o, Google Sheets & Evolution API"
description: "Hướng dẫn tạo workflow n8n tự động tổng hợp cuộc trò chuyện WhatsApp hàng ngày, lưu vào Google Sheets và gửi báo cáo qua Evolution API - giải pháp hoàn toàn không cần code cho quản lý nhóm."
slug: "tu-dong-hoa-nhom-whatsapp-hang-ngay-voi-gpt-4o-google-sheets-evolution-api"
tags: [n8n, automation, no-code, whatsapp, google-sheets, evolution-api, ai]
keywords: [n8n workflow, tự động hóa nhóm whatsapp, evolution api, gpt-4o, google sheets]
---
```

# 💬 Tự động hóa nhóm WhatsApp hàng ngày với GPT-4o, Google Sheets & Evolution API

[Đoạn mở đầu: Phân tích nỗi đau thực tế của quản lý nhóm WhatsApp khi phải tổng hợp thủ công hàng ngày. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm 2-3 giờ mỗi ngày cho việc tổng hợp thủ công
- Tự động lưu trữ lịch sử cuộc trò chuyện trong Google Sheets
- Báo cáo hàng ngày được gửi tự động qua Evolution API
- Tích hợp AI GPT-4o để tổng hợp nội dung chính xác và hiệu quả
- Hoạt động liên tục 24/7 mà không cần can thiệp
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Drive và Google Sheets
- API Key từ Evolution API
- API Key từ OpenAI (cho GPT-4o)
- Quyền truy cập vào nhóm WhatsApp cần quản lý
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [workflow gốc trên n8n.io](https://n8n.io/workflows/3646)
2. Click vào nút "Copy JSON" để sao chép cấu hình
3. Trong n8n Editor, click vào "Import from Clipboard" và dán JSON đã sao chép

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Webhook**: Cấu hình webhook để nhận dữ liệu từ Evolution API
2. **Google Drive**: Thiết lập credentials Google Drive và chỉ định thư mục lưu trữ
3. **Google Sheets**:
   - Cấu hình credentials Google Sheets
   - Chỉ định Spreadsheet ID và tên sheet cho lưu trữ cuộc trò chuyện
   - Chỉ định Spreadsheet ID và tên sheet cho lưu trữ báo cáo
4. **ChatModel (GPT-4o)**:
   - Thiết lập credentials OpenAI
   - Điều chỉnh prompt nếu cần thiết
5. **Evolution Groups Search**:
   - Cấu hình credentials Evolution API
   - Điền thông tin nhóm WhatsApp cần quản lý

#### 3. Kích hoạt ⚡️
1. Test run dữ liệu mẫu để kiểm tra kết nối và cấu hình
2. Bật Active workflow để chạy tự động hàng ngày

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node gửi báo cáo qua Slack/Telegram để thông báo kết quả
- Tích hợp với Google Calendar để lên lịch gửi báo cáo
- Thêm node lưu log hoạt động để theo dõi hiệu suất workflow
- Tùy chỉnh prompt cho GPT-4o để phù hợp với nhu cầu cụ thể của nhóm

### 📌 Kết luận
Workflow này giúp các sếp quản lý nhóm WhatsApp một cách hiệu quả hơn với giải pháp tự động hóa hoàn toàn không cần code. Bằng cách tích hợp GPT-4o, Google Sheets và Evolution API, workflow này không chỉ tiết kiệm thời gian mà còn cung cấp báo cáo hàng ngày một cách chính xác và tự động. Hãy thử ngay và trải nghiệm sự khác biệt!