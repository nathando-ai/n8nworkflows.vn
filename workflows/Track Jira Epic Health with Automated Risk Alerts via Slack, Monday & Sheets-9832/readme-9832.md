---
title: "🚀 Theo dõi sức khỏe Epic Jira tự động với cảnh báo rủi ro qua Slack, Monday & Sheets"
description: "Hướng dẫn tự động hóa theo dõi sức khỏe Epic Jira, tính toán điểm sức khỏe, cảnh báo rủi ro qua Slack và đồng bộ dữ liệu lên Monday.com và Google Sheets"
slug: "theo-doi-suc-khoe-epic-jira-tu-dong"
tags: [n8n, automation, no-code, jira, monday, google-sheets]
keywords: [n8n workflow, tự động hóa, jira, monday, google sheets]
---

# 🚀 Theo dõi sức khỏe Epic Jira tự động với cảnh báo rủi ro qua Slack, Monday & Sheets

[Các sếp đang gặp khó khăn khi phải theo dõi sức khỏe các Epic trong Jira thủ công. Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình theo dõi, tính toán điểm sức khỏe và cảnh báo rủi ro một cách nhanh chóng và chính xác.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động theo dõi sức khỏe các Epic Jira hàng ngày
- Tính toán điểm sức khỏe dựa trên các chỉ số quan trọng
- Cảnh báo rủi ro qua Slack ngay khi phát hiện
- Đồng bộ dữ liệu lên Monday.com và Google Sheets
- Giảm thời gian theo dõi thủ công đến 90%
- Tăng tính chính xác trong đánh giá sức khỏe dự án
- Tạo lịch sử theo dõi để phân tích xu hướng
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Jira với quyền truy cập API
- Tài khoản Slack với quyền gửi tin nhắn
- Tài khoản Monday.com với quyền chỉnh sửa bảng
- Tài khoản Google với quyền truy cập Google Sheets
- API keys cho các dịch vụ trên
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/9832](https://n8n.io/workflows/9832)
2. Click vào nút "Import" ở góc trên bên phải
3. Chọn "Import from URL" và dán link trên vào ô nhập liệu
4. Click "Import" để hoàn tất

Hoặc có thể copy JSON từ trang workflow và paste vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Trigger Every 6 Hours** (cron):
   - Không cần cấu hình gì, node này sẽ chạy workflow mỗi 6 giờ một lần

2. **Fetch All Epics from Jira** (jira):
   - Cần cấu hình credentials "jiraSoftwareCloudApi"
   - Đảm bảo tài khoản Jira có quyền truy cập vào các Epic cần theo dõi

3. **Split Epics for Processing** (function):
   - Node này sẽ tự động xử lý dữ liệu, không cần cấu hình

4. **Fetch Epic + Linked Issues** (jira):
   - Cần cấu hình credentials "jiraSoftwareCloudApi"
   - Đảm bảo tài khoản Jira có quyền truy cập vào các issue liên quan

5. **Calculate Health Score** (function):
   - Node này chứa công thức tính điểm sức khỏe
   - Có thể điều chỉnh trọng số trong công thức nếu cần

6. **Is Score > 0.6 (At Risk)?** (if):
   - Node này sẽ tự động kiểm tra điểm sức khỏe
   - Không cần cấu hình

7. **Update Epic in Jira** (jira):
   - Cần cấu hình credentials "jiraSoftwareCloudApi"
   - Đảm bảo tài khoản Jira có quyền chỉnh sửa Epic

8. **Alert Slack Channel** (slack):
   - Cần cấu hình credentials "slackApi"
   - Chỉnh sửa kênh Slack nhận cảnh báo nếu cần

9. **Update Monday.com Pulse** (mondayCom):
   - Cần cấu hình credentials "mondayComApi"
   - Chỉnh sửa ID bảng Monday.com nếu cần

10. **Log to Google Sheets** (googleSheets):
    - Cần cấu hình credentials "googleApi"
    - Chỉnh sửa ID Google Sheet và tên sheet nếu cần

#### 3. Kích hoạt ⚡️
1. Sau khi cấu hình xong tất cả các node, click vào nút "Activate" ở góc trên bên phải
2. Chọn "Save & Activate" để lưu và kích hoạt workflow
3. Để kiểm tra workflow, có thể chạy thử với dữ liệu mẫu bằng cách click vào nút "Execute Workflow" ở góc trên bên phải

### ✍️ Mẹo & gợi ý nâng cao
- Có thể thêm node gửi email cảnh báo qua Gmail nếu cần
- Có thể mở rộng workflow để theo dõi thêm các chỉ số khác
- Có thể thiết lập lịch gửi báo cáo hàng tuần/tuần qua Slack
- Có thể tích hợp với các công cụ báo cáo khác như Power BI
- Có thể thêm node để lưu trữ dữ liệu lịch sử trong cơ sở dữ liệu

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa toàn bộ quy trình theo dõi sức khỏe Epic Jira, từ việc tính toán điểm sức khỏe đến cảnh báo rủi ro và đồng bộ dữ liệu. Với workflow này, các sếp có thể tiết kiệm thời gian, tăng tính chính xác và có cái nhìn tổng quan rõ ràng về sức khỏe của các dự án quan trọng. Hãy áp dụng ngay để nâng cao hiệu quả quản lý dự án của các sếp!