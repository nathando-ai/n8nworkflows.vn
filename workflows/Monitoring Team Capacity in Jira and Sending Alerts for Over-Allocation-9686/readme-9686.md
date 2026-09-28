---
title: "🚀 Tự Động Theo Dõi Năng Lực Nhóm Trên Jira & Cảnh Báo Quá Tải Với n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động đồng bộ dữ liệu từ Jira, tính toán công suất làm việc, ghi log Google Sheets và gửi email cảnh báo quá tải nhân sự."
slug: "tu-dong-theo-doi-nang-luc-jira-va-canh-bao-qua-tai"
tags: [n8n, automation, jira, google-sheets, gmail]
keywords: [n8n workflow, tự động hóa jira, quản lý capacity team, cảnh báo quá tải nhân sự, n8n viet nam]
---

# 🚀 Tự Động Theo Dõi Năng Lực Nhóm Trên Jira & Cảnh Báo Quá Tải Với n8n

Trong quản lý dự án Agile/Scrum, việc nhân sự bị quá tải (Over-allocation) thường dẫn đến tình trạng chậm tiến độ, giảm chất lượng công việc và kiệt sức (burnout). Tuy nhiên, việc theo dõi thủ công giờ làm việc của từng thành viên trên Jira tốn rất nhiều thời gian. 

Bài viết này sẽ hướng dẫn các sếp triển khai một workflow n8n cực kỳ thông minh do chuyên gia **Rahul Joshi** thiết kế. Workflow này giúp tự động hóa 100% quy trình: lấy dữ liệu từ Jira, tính toán hiệu suất công việc, ghi nhận lịch sử vào Google Sheets và tự động gửi email cảnh báo chi tiết đến Quản lý dự án (Project Manager) ngay khi phát hiện nhân sự quá tải.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Phát hiện sớm quá tải:** Tự động rà soát workload và cảnh báo ngay khi nhân sự vượt mức 100% công suất.
- **Ra quyết định dựa trên dữ liệu (Data-driven):** Tự động ghi lại lịch sử capacity vào Google Sheets giúp tối ưu hóa việc phân bổ công việc ở các sprint sau.
- **Tiết kiệm hàng giờ đồng hồ:** Loại bỏ hoàn toàn việc phải tổng hợp báo cáo thủ công hàng tuần.
- **Bảo vệ sức khỏe đội ngũ:** Ngăn ngừa tình trạng kiệt sức (burnout) cho nhân viên thông qua việc can thiệp kịp thời.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động mượt mà, các sếp cần chuẩn bị sẵn:
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Jira Cloud Account** với quyền truy cập API/Projects.
- **Google Account** (để kết nối Google Sheets lưu log capacity và error).
- **Gmail Account** (hoặc SMTP credentials để gửi email cảnh báo).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể lấy mã nguồn JSON từ trang chính thức của n8n (ID: `9686`), sau đó copy và paste trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 9 nodes chính, các sếp cần chú ý cấu hình các điểm sau:
- **Jira Get Issues Node (`jira`):** Kết nối tài khoản Jira Cloud của các sếp. Kiểm tra lại câu lệnh JQL mặc định (`statusCategory != Done AND status = 'In Progress'`) để đảm bảo lấy đúng các task đang thực hiện.
- **Data Validation (`if`) & Over-Allocation Check (`if`):** Các node rẽ nhánh logic kiểm tra dữ liệu đầu vào và lọc danh sách nhân sự có utilization > 100%.
- **Capacity Calculator & Alert Report Generator (`code`):** Các đoạn mã JavaScript chạy ngầm để tính toán giờ làm việc, quy đổi từ giây sang giờ (dựa trên tiêu chuẩn 8 giờ/ngày) và định dạng nội dung báo cáo.
- **Log Capacity Data & Log Query Failures (`googleSheets`):** Kết nối tài khoản Google Sheets và chỉ định đúng tệp (spreadsheet) cùng tên trang tính (sheet name) để ghi nhận lịch sử capacity và lỗi query (nếu có).
- **Send Over-Allocation Alert to Manager (`gmail`):** Kết nối tài khoản Gmail, điền email người nhận (Project Manager) để hệ thống tự động gửi thư cảnh báo với tiêu đề động kèm số lượng thành viên quá tải.

#### 3. Kích hoạt ⚡️
- Bấm nút **‘Execute workflow’** ở node `When clicking ‘Execute workflow’` để test chạy thử với dữ liệu thực tế.
- Kiểm tra lại các bảng Google Sheets xem dữ liệu đã được ghi nhận chuẩn xác chưa.
- Gạt công tắc **Active** góc trên bên phải để workflow tự động vận hành.

### ✍️ Mẹo & gợi ý nâng cao
Để hệ thống hoàn hảo hơn, các sếp có thể mở rộng workflow với các ý tưởng sau:
- **Tích hợp Slack/Telegram:** Thay vì chỉ gửi email, hãy đẩy thông báo quá tải vào nhóm chat chung của ban quản lý để xử lý nhanh hơn.
- **Lên lịch tự động (Schedule Trigger):** Thay thế node Manual Trigger bằng Schedule Trigger để workflow tự động chạy định kỳ vào mỗi sáng thứ Hai đầu tuần.
- **Mở rộng ngưỡng cảnh báo:** Tùy chỉnh code tính toán capacity để cảnh báo sớm ở mức 80-90% thay vì chờ đến khi vượt 100%.

### 📌 Kết luận
Việc quản lý nguồn lực đội ngũ chưa bao giờ dễ dàng đến thế với sức mạnh của tự động hóa n8n. Hãy thiết lập ngay workflow này để tối ưu hóa năng suất và bảo vệ đội ngũ của các sếp!