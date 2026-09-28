---
title: "🚀 Tự động hóa báo cáo hiệu suất workflow hàng tuần với n8n API & Email"
description: "Hướng dẫn xây dựng workflow n8n tự động tổng hợp lịch sử chạy, thống kê lỗi/thành công và gửi báo cáo HTML hàng tuần qua Gmail hoặc Microsoft Outlook."
slug: "tu-dong-hoa-bao-cao-hieu-suat-workflow-hang-tuans-voi-n8n"
tags: [n8n, automation, devops, n8n-api, gmail, outlook, reporting]
keywords: [n8n workflow, tự động hóa báo cáo, n8n api executions, gửi báo cáo email tự động, quản lý n8n workflows]
---

# 🚀 Tự động hóa báo cáo hiệu suất workflow hàng tuần với n8n API & Email

Các sếp có đang quản lý hàng chục hay hàng trăm workflow trên n8n và cảm thấy mệt mỏi mỗi khi phải kiểm tra thủ công xem tuần qua có workflow nào bị lỗi (error), workflow nào chạy thành công hay tốn bao nhiêu thời gian không? Việc theo dõi thủ công không chỉ tốn thời gian mà còn dễ bỏ sót các sự cố quan trọng.

Giải pháp ở đây là để n8n tự làm việc đó! Workflow này sẽ tự động trích xuất lịch sử chạy (executions) của toàn bộ hệ thống trong 7 ngày qua, tổng hợp thành một bản báo cáo HTML cực kỳ trực quan và gửi thẳng vào hộp thư Gmail hoặc Microsoft Outlook của các sếp định kỳ mỗi tuần.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Báo cáo tự động 100%:** Nhận email tổng kết vào mỗi tuần mà không cần động tay.
- **Nắm bắt sự cố kịp thời:** Thống kê rõ số lượng lỗi, thành công và trạng thái của từng workflow.
- **Tối ưu hiệu suất:** Đánh giá chính xác tải của hệ thống automation để điều chỉnh kịp thời.
- **Linh hoạt kênh nhận:** Hỗ trợ gửi qua cả Gmail hoặc Microsoft Outlook tùy nhu cầu doanh nghiệp.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Hệ thống **n8n Self-hosted** (vì cần dùng n8n internal API nodes để lấy thông tin executions).
- Tài khoản **Gmail** (hoặc Microsoft Outlook) đã cấu hình Credentials (OAuth2) trên n8n để gửi email.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow hoặc copy đoạn code JSON từ nguồn gốc.
- Trong giao diện n8n Editor, nhấn vào menu **Add workflow** -> **Import from File** (hoặc dán trực tiếp bằng phím tắt `Ctrl+V`).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình các node cốt lõi sau để workflow chạy mượt mà:
- **Schedule Trigger:** Cài đặt lịch chạy mong muốn (ví dụ: Chạy vào 8:00 sáng thứ Hai hàng tuần).
- **Get all previous executions & Get all Workflows:** Đảm bảo cấp quyền truy cập đầy đủ cho n8n API nodes. Không cần điền tham số phức tạp vì node tự động lấy toàn bộ dữ liệu hệ thống.
- **Filter Executions Last Week:** Kiểm tra điều kiện lọc ngày `startedAt` so với `DateTime.now().minus({ days: 7 })` để đảm bảo báo cáo chỉ quét đúng dữ liệu trong 7 ngày qua.
- **Send a message gmail** / **Send a message outlook:** Chọn đúng Credentials tài khoản email của các sếp. *(Lưu ý: Mặc định node Gmail có thể đang ở trạng thái disable, các sếp nhớ Enable node lên nếu chọn dùng Gmail).*

#### 3. Kích hoạt ⚡️
- Nhấn nút **Test workflow** để chạy thử và kiểm tra xem email có được gửi về hòm thư hay không.
- Sau khi test thành công, gạt công tắc sang **Active** để hệ thống tự động chạy theo lịch trình.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp Telegram/Slack:** Ngoài gửi email, các sếp có thể nối thêm node Telegram hoặc Slack để bắn thông báo tóm tắt nhanh vào nhóm chat chung của team kỹ thuật.
- **Lưu trữ log:** Gửi kết quả JSON vào Google Sheets hoặc Notion để lưu trữ lịch sử hiệu suất theo tháng/quý.
- **Cảnh báo khẩn cấp:** Tạo thêm một nhánh Filter riêng chuyên lọc các workflow bị lỗi trong ngày để gửi cảnh báo ngay lập tức thay vì đợi báo cáo tuần.

### 📌 Kết luận
Việc tự động hóa khâu báo cáo vận hành sẽ giúp các sếp tiết kiệm rất nhiều thời gian quản trị hệ thống, đồng thời nâng cao độ tin cậy cho toàn bộ chuỗi quy trình tự động hóa. Hãy import workflow này ngay hôm nay và tối ưu hóa hệ thống n8n của mình nhé!