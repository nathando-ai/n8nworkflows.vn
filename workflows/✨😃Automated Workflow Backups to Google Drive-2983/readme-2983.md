---
title: "🚀 Tự động sao lưu workflow n8n lên Google Drive hàng ngày"
description: "Hướng dẫn chi tiết cách tự động sao lưu workflow n8n lên Google Drive hàng ngày, giữ lại 7 ngày gần nhất và nhận thông báo qua Telegram"
slug: "tu-dong-sao-luu-workflow-n8n-len-google-drive"
tags: [n8n, automation, no-code, google-drive, telegram]
keywords: [n8n workflow, tự động hóa, sao lưu workflow, google drive, telegram]
---

# 🚀 Tự động sao lưu workflow n8n lên Google Drive hàng ngày

[Các sếp] có biết không? Việc quản lý hàng trăm workflow n8n thủ công là một công việc cực kỳ tẻ nhạt và dễ gây lỗi. Bạn phải nhớ mỗi ngày phải backup lại, phải xóa những bản sao lưu cũ, phải kiểm tra xem có bị thiếu workflow nào không... Đó là những công việc mà workflow này sẽ giúp các sếp tự động hóa hoàn toàn!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn**: Không cần can thiệp thủ công mỗi ngày
- **Quản lý phiên bản**: Giữ lại 7 ngày sao lưu gần nhất, tự động xóa các bản cũ
- **Thông báo tức thì**: Nhận thông báo qua Telegram khi quá trình hoàn tất
- **Bảo mật dữ liệu**: Tất cả workflow được lưu trữ an toàn trên Google Drive
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Drive với quyền truy cập đầy đủ
- API key của n8n (để lấy danh sách workflow)
- Bot Telegram và Chat ID (để nhận thông báo)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/2983](https://n8n.io/workflows/2983)
2. Click vào nút "Import" ở góc trên bên phải
3. Chọn "Import from URL" và dán link trên vào
4. Hoàn tất quá trình import

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Node "Create Folder with DateTime Stamp"**: Cần cấu hình Google Drive OAuth2 credentials
- **Node "Get Workflows"**: Cần cấu hình n8n API credentials
- **Node "Complete Message"**: Cần cấu hình Telegram API credentials
- **Node "Every Day"**: Thay đổi thời gian chạy theo nhu cầu (mặc định là 12h đêm hàng ngày)

#### 3. Kích hoạt ⚡️
1. Click vào nút "Execute" để chạy thử workflow
2. Kiểm tra xem:
   - Folder mới đã được tạo trên Google Drive
   - Tất cả workflow đã được lưu thành file JSON
   - Thông báo Telegram đã được gửi
3. Sau khi kiểm tra thành công, bật chế độ "Active" cho workflow

### ✍️ Mẹo & gợi ý nâng cao
- Thay đổi số lượng ngày lưu trữ bằng cách chỉnh sửa node "Find Folders to Delete"
- Thêm node gửi email báo cáo sau mỗi lần backup
- Kết hợp với Slack để nhận thông báo thay vì Telegram
- Tạo bản sao lưu định kỳ hàng tuần/tháng

### 📌 Kết luận
Workflow này không chỉ giúp các sếp tiết kiệm thời gian mà còn đảm bảo dữ liệu luôn được bảo vệ. Hãy áp dụng ngay để tránh những rủi ro không đáng có khi làm việc thủ công!