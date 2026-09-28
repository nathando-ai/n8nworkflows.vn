---
title: "🚀 Tự động gửi cảnh báo hết hạn giấy tờ xe công ty từ Google Sheets qua Gmail"
description: "Hướng dẫn xây dựng hệ thống tự động kiểm tra hạn bảo hiểm, đăng kiểm, đường bộ và bảo dưỡng xe fleet qua Google Sheets và gửi email cảnh báo qua Gmail bằng n8n."
slug: "tu-dong-gui-canh-bao-het-han-giay-to-xe-tu-google-sheets-qua-gmail"
tags: [n8n, automation, google-sheets, gmail, fleet-management]
keywords: [n8n workflow, tự động hóa giấy tờ xe, quản lý fleet google sheets, cảnh báo hết hạn đăng kiểm n8n, gmail automation]
---

# 🚀 Tự động gửi cảnh báo hết hạn giấy tờ xe công ty từ Google Sheets qua Gmail

Các sếp đang quản lý đội xe (fleet) có đau đầu khi bỏ lỡ hạn bảo hiểm, đăng kiểm (MOT), phí đường bộ hay lịch bảo dưỡng định kỳ của xe? Việc kiểm tra thủ công từng tờ giấy tờ trong danh sách Excel dài dằng dặc rất dễ dẫn đến sai sót, đối mặt với các khoản phạt tiền nặng hoặc xe không đủ điều kiện lưu thông.

Bài viết này sẽ hướng dẫn các sếp thiết lập một workflow n8n hoàn toàn tự động: Định kỳ mỗi sáng, hệ thống sẽ quét qua Google Sheets, kiểm tra hạn các loại giấy tờ, phân loại mức độ khẩn cấp (Đã hết hạn, Cấp bách trong 7 ngày, Sắp hết hạn trong 30 ngày) và tổng hợp thành một báo cáo HTML đẹp mắt gửi trực tiếp đến quản lý qua Gmail!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động 100%:** Chạy lịch trình định kỳ mỗi sáng ngày làm việc, không cần con người nhúng tay.
- **Cảnh báo thông minh:** Phân loại rõ ràng 3 mức độ (🔴 Đã hết hạn, 🟠 Cấp bách dưới 7 ngày, 🟡 Sắp hết hạn dưới 30 ngày).
- **Giao diện email chuyên nghiệp:** Báo cáo dạng bảng HTML tổng hợp trực quan, kèm tiêu đề động hiển thị chính xác số lượng xe cần xử lý.
- **Không làm phiền hộp thư:** Nếu không có xe nào hết hạn, workflow tự động kết thúc lặng lẽ mà không bắn email rác.
:::

### 📦 Thông tin Workflow
- **Tác giả:** Federico
- **Tổng số nodes:** 7 nodes (`Schedule Trigger`, `Google Sheets`, `Code`, `If`, `Gmail`, `NoOp`)
- **Danh mục:** Document Extraction / Fleet Management

---

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản n8n (Cloud hoặc Self-hosted).
- Tài khoản Google (Google Sheets chứa dữ liệu đội xe).
- Tài khoản Google Workspace / Gmail (để gửi email cảnh báo).
:::

---

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow từ n8n, sau đó dán (Paste) trực tiếp vào giao diện n8n Editor của mình.

#### 2. Cấu trúc Google Sheets chuẩn 📊
Tạo một Google Sheet với tên tab (sheet name) là **`Fleet`** và các cột bắt buộc sau:

| Plate | Model | Driver | Insurance Date | MOT Date | Road Tax Date | Service Date |
|-------|-------|--------|----------------|----------|---------------|--------------|
| AB123CD | Ford Transit | John Smith | 2025-06-15 | 2025-01-20 | 2025-03-01 | 2025-02-10 |

⚠️ **Lưu ý quan trọng:** Định dạng ngày tháng bắt buộc phải là **`YYYY-MM-DD`**.

#### 3. Các node quan trọng cần cấu hình 📌
- **Every weekday at 8 AM (`scheduleTrigger`):** Mặc định chạy vào 8:00 sáng từ Thứ Hai đến Thứ Sáu. Các sếp có thể đổi biểu thức Cron nếu muốn đổi lịch.
- **Read Fleet Sheet (`googleSheets`):** 
  - Kết nối **Google Sheets OAuth2 credential**.
  - Thay thế `YOUR_GOOGLE_SHEET_ID` bằng ID bảng tính của các sếp (lấy đoạn ký tự trên URL giữa `/d/` và `/edit`).
- **Check Expiries (`code`):** Node này chứa đoạn mã Javascript quét toàn bộ dữ liệu, so sánh với ngày hiện tại dựa trên ngưỡng `warningDays = 30`. Các sếp có thể tuỳ chỉnh số ngày cảnh báo tại đây nếu muốn.
- **Send Email to Fleet Manager (`gmail`):** 
  - Kết nối **Gmail OAuth2 credential**.
  - Thay đổi địa chỉ email nhận (`fleet.manager@yourcompany.com`) thành email của quản lý đội xe.

#### 4. Kích hoạt ⚡️
- Nhấn **Test step** hoặc **Execute Workflow** để chạy thử nghiệm dữ liệu mẫu.
- Sau khi kiểm tra mọi thứ trơn tru, hãy bật công tắc **Active** ở góc trên bên phải để hệ thống tự động chạy ngầm.

---

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo:** Các sếp có thể kết nối thêm node **Telegram** hoặc **Slack** ngay sau node kiểm tra điều kiện để gửi tin nhắn tức thời vào nhóm chat thay vì chỉ nhận email.
- **Lưu lịch sử cảnh báo:** Thêm một node Google Sheets ở nhánh "True" để ghi log lịch sử các xe đã bị cảnh báo nhằm phục vụ việc kiểm toán sau này.
- **Tuỳ chỉnh ngưỡng cảnh báo:** Trong code node *Check Expiries*, nếu công ty có quy trình gia hạn sớm hơn, các sếp có thể nâng `warningDays` lên 45 hoặc 60 ngày.

---

### 📌 Kết luận
Việc tự động hóa quy trình theo dõi hạn kiểm định và giấy tờ xe giúp doanh nghiệp tiết kiệm hàng giờ kiểm tra thủ công, loại bỏ hoàn toàn rủi ro quên hạn phạt tiền. Hãy áp dụng ngay workflow này vào hệ thống vận hành của các sếp ngay hôm nay!