---
title: "🚀 Tự động tạo báo cáo kiểm kê Workflow n8n với định dạng JSON và Excel cực nhanh"
description: "Hướng dẫn xây dựng workflow n8n tự động trích xuất, phân tích và xuất báo cáo toàn bộ danh sách workflow dưới dạng JSON hoặc file Excel một cách chuyên nghiệp."
slug: "tu-dong-tao-bao-cao-kiem-ke-workflow-n8n"
tags: [n8n, automation, no-code, devops, workflow-management, reporting]
keywords: [n8n workflow inventory, tự động hóa n8n, export excel n8n, devops automation, quan ly workflow n8n]
---

# 🚀 Tự động tạo báo cáo kiểm kê Workflow n8n với định dạng JSON và Excel

Các sếp quản lý một hệ thống n8n lớn với hàng chục, hàng trăm workflow đang chạy ngầm? Việc kiểm tra trạng thái, đếm số lượng node, hay tổng hợp báo cáo thủ công thực sự là một cơn ác mộng tốn thời gian và dễ xảy ra sai sót. 

Giải pháp ở đây là gì? Workflow tự động hóa 100% không cần code giúp các sếp gom toàn bộ dữ liệu hệ thống, phân tích metadata và xuất thẳng ra file Excel hoặc JSON chỉ trong một nốt nhạc!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không cần tra cứu thủ công từng workflow trên giao diện n8n nữa.
- **Báo cáo đa dạng:** Hỗ trợ linh hoạt trả về định dạng JSON API hoặc file tải về (Excel/CSV) thông qua Webhook.
- **Quản trị minh bạch:** Nắm bắt toàn bộ trạng thái (Active/Inactive), cấu trúc và metadata của hệ thống tự động hóa.
- **Hoạt động liên tục:** Có thể lên lịch hoặc kích hoạt theo yêu cầu thông qua API/Webhook bất cứ lúc nào.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một hệ thống n8n (Self-hosted hoặc Cloud).
- Quyền truy cập n8n Internal API (hoặc n8n Node để gọi trực tiếp dữ liệu hệ thống).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy đoạn mã JSON của workflow này và paste thẳng vào n8n Editor của mình, hoặc tải file JSON về và chọn **Import from File**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Hệ thống gồm 11 nodes được thiết kế mạch lạc từ nhận yêu cầu đến trả kết quả. Các sếp cần chú ý các node quan trọng sau:

- **Receive Request (`webhook`):** Điểm tiếp nhận yêu cầu gọi báo cáo. Các sếp có thể cấu hình Method (GET/POST) và đường dẫn URL endpoint tùy ý.
- **Parse Query Params (`code`):** Node xử lý các tham số đầu vào (ví dụ: lọc theo trạng thái active/inactive).
- **Fetch All Workflows (`n8n`):** Node cốt lõi kết nối trực tiếp với n8n API nội bộ để lấy toàn bộ danh sách workflow hiện có trên hệ thống.
- **Filter by Status & Extract Workflow Metadata (`code`):** Các đoạn mã JavaScript giúp lọc dữ liệu và trích xuất các thông tin quan trọng như tên, ID, trạng thái, thời gian tạo/cập nhật.
- **Switch Output Type (`switch`):** Điều hướng luồng dữ liệu dựa trên định dạng mà người dùng yêu cầu (JSON hay File).
- **Convert to File (`convertToFile`):** Xử lý chuyển đổi dữ liệu cấu trúc thành định dạng file Excel/CSV để tải về dễ dàng.
- **Respond to Webhook1 & Respond to Webhook2 (`respondToWebhook`):** Trả kết quả về cho client gọi API.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** và gọi thử Webhook URL với các tham số mẫu để kiểm tra kết quả trả về.
- Sau khi test ngon lành, hãy gạt công tắc sang **Active** để đưa vào sử dụng chính thức.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Telegram/Slack:** Kết hợp thêm node gửi thông báo tự động để đẩy file Excel báo cáo vào nhóm chat của team DevOps mỗi tuần/mỗi tháng.
- **Lưu trữ tự động:** Đẩy file báo cáo vừa tạo thẳng lên Google Drive hoặc OneDrive để làm kho lưu trữ lịch sử cấu hình hệ thống.
- **Cảnh báo workflow lỗi:** Phát triển thêm nhánh lọc các workflow đang bị `Inactive` hoặc lỗi để gửi cảnh báo sớm cho đội ngũ kỹ thuật.

### 📌 Kết luận
Một hệ thống tự động hóa chuyên nghiệp luôn cần sự quản trị chặt chẽ. Với workflow kiểm kê này, các sếp hoàn toàn làm chủ được "sức khỏe" của toàn bộ hệ thống n8n trong tay. Lên đồ và áp dụng ngay thôi nào!