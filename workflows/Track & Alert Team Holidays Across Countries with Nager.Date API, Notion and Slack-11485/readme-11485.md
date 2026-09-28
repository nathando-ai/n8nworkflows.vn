---
title: "🌍 Tự động theo dõi & cảnh báo ngày lễ của team đa quốc gia với n8n"
description: "Workflow n8n giúp quản lý team đa quốc gia tránh xung đột lịch làm việc nhờ tự động theo dõi ngày lễ từ Nager.Date API và đồng bộ với Notion/Slack."
slug: "tu-dong-theo-doi-ngay-le-team-da-quoc-gia-n8n"
tags: [n8n, automation, no-code, project-management, team-collaboration]
keywords: [n8n workflow, tự động hóa, quản lý dự án, team đa quốc gia, ngày lễ quốc gia]
---

# 🌍 Tự động theo dõi & cảnh báo ngày lễ của team đa quốc gia với n8n

[Các sếp đang quản lý team đa quốc gia đang gặp khó khăn khi phải tự động theo dõi ngày lễ của từng quốc gia để tránh xung đột lịch làm việc. Workflow này sẽ giúp các sếp tự động hóa quy trình này 100% không cần code nhờ kết hợp Nager.Date API, Notion và Slack.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động theo dõi ngày lễ của 20+ quốc gia trên thế giới
- Nhận cảnh báo ngay khi có ngày lễ chung giữa các quốc gia trong team
- Đồng bộ lịch làm việc với Notion và Slack một cách tự động
- Tránh xung đột lịch làm việc nhờ có thông tin ngày lễ cập nhật liên tục
- Tiết kiệm thời gian quản lý thủ công cho các sếp
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Notion với Database có sẵn (hoặc tạo mới)
- Tài khoản Slack với Channel đã tạo
- API Key của Notion (có thể lấy từ [Notion Integrations](https://www.notion.so/my-integrations))
- Các sếp cần chuẩn bị danh sách mã quốc gia (2 chữ cái) của các thành viên trong team
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [Workflow gốc trên n8n.io](https://n8n.io/workflows/11485)
2. Click vào nút "Import" và chọn "Import from URL"
3. Dán link workflow vào ô nhập liệu
4. Click "OK" để hoàn tất import

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Define Team Countries"**:
   - Chỉnh sửa danh sách các quốc gia trong team (ví dụ: ["KR", "US", "JP"])
   - Mỗi quốc gia được biểu diễn bằng mã 2 chữ cái (ISO 3166-1 alpha-2)

2. **Node "Define Days to Lookahead"**:
   - Thiết lập khoảng thời gian cần theo dõi (ví dụ: 50 ngày)
   - Giá trị này quyết định phạm vi thời gian để tìm kiếm ngày lễ

3. **Node "Add to Notion"**:
   - Chọn credentials của Notion
   - Chọn Database cần đồng bộ (hoặc tạo mới với cấu trúc sau):
     - Name (Title)
     - Date (Date)
     - Shared Countries (Text)

4. **Node "Notify Slack"**:
   - Chọn credentials của Slack
   - Chọn Channel cần gửi thông báo

#### 3. Kích hoạt ⚡️
1. Click vào nút "Execute Node" để test workflow với dữ liệu mẫu
2. Kiểm tra kết quả trên Notion và Slack
3. Sau khi xác nhận hoạt động bình thường, click vào nút "Activate" để kích hoạt workflow

### ✍️ Mẹo & gợi ý nâng cao
- Các sếp có thể kết hợp với workflow khác để tự động gửi email thông báo cho team
- Có thể thêm node để lưu log các ngày lễ đã được theo dõi
- Để nhận báo cáo định kỳ, các sếp có thể thêm node gửi báo cáo hàng tuần qua Slack/Email
- Nếu team có nhiều quốc gia hơn, các sếp có thể chia nhỏ workflow thành các phần nhỏ hơn để dễ quản lý

### 📌 Kết luận
Workflow này giúp các sếp quản lý team đa quốc gia một cách hiệu quả hơn nhờ tự động hóa quy trình theo dõi ngày lễ. Bằng cách tích hợp Nager.Date API, Notion và Slack, các sếp có thể tránh xung đột lịch làm việc và duy trì sự đồng bộ trong team một cách dễ dàng. Hãy áp dụng ngay để tiết kiệm thời gian và tránh những rắc rối không đáng có!