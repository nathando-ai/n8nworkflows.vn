---
title: "🚀 Tự động gửi thông báo Jira Task qua Telegram Bot với n8n"
description: "Hướng dẫn chi tiết cách kết nối Jira Webhook với Telegram Bot qua n8n để tự động gửi thông báo khi task được tạo, cập nhật hoặc phân công."
slug: "gui-thong-bao-jira-qua-telegram-bot-bang-n8n"
tags: [n8n, automation, jira, telegram, devops, webhook]
keywords: [n8n workflow, jira telegram integration, tự động hóa jira, telegram bot n8n, webhook jira]
---

# 🚀 Tự động gửi thông báo Jira Task qua Telegram Bot với n8n

Các sếp làm trong ngành phát triển phần mềm chắc hẳn luôn đau đầu với việc quản lý thông báo task trên Jira. Đội ngũ cứ liên tục phàn nàn rằng họ bỏ lỡ các cập nhật quan trọng, task được giao nhưng không nhận được thông báo kịp thời, hay việc phải liên tục mở Jira kiểm tra rất mất thời gian. 

Giải pháp là gì? Hãy để n8n tự động hóa toàn bộ quy trình này! Workflow **"Send Jira task notifications to Telegram user via Bot"** sẽ giúp các sếp bắt sự kiện từ Jira Webhook, xử lý thông tin và gửi thông báo trực tiếp đến tài khoản Telegram của từng thành viên ngay lập tức. 100% tự động, không cần code phức tạp!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Thông báo tức thì:** Gửi tin nhắn ngay lập tức qua Telegram khi có Task mới (Create), cập nhật (Update) hoặc được giao việc (Assign Alert).
- **Cá nhân hóa cao:** Định tuyến tin nhắn đến đúng Telegram ID của người dùng dựa trên cấu hình tài khoản.
- **Tiết kiệm thời gian:** Đội ngũ không cần túc trực trên Jira mà vẫn nắm bắt trọn vẹn tiến độ công việc.
- **Vận hành 24/7:** Hoạt động liên tục, không bỏ sót bất kỳ sự kiện quan trọng nào từ hệ thống quản lý dự án.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một instance n8n đang hoạt động.
- Tài khoản **Jira** có quyền thiết lập Webhook (Administrator).
- **Telegram Bot Token** (tạo qua [@BotFather](https://t.me/BotFather)).
- Danh sách ánh xạ (mapping) giữa email/username Jira và Telegram Chat ID của các thành viên.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tạo một workflow mới trên n8n, sau đó copy toàn bộ cấu trúc JSON từ nguồn cung cấp và dán trực tiếp vào n8n Editor, hoặc import file JSON tương ứng.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống hoạt động trơn tru, các sếp cần chú ý cấu hình các node cốt lõi sau:

- **`jira-webhook` (Webhook Node):** 
  - Cấu hình phương thức `POST` và lấy đường dẫn URL được cung cấp bởi n8n.
  - Mang URL này dán vào phần Webhook settings trong cài đặt của Jira (System > Webhooks) để nhận các sự kiện `jira:issue_created`, `jira:issue_updated`, v.v.
- **`telegram account` (Code Node):** 
  - Node này dùng để ánh xạ (map) người dùng Jira với tài khoản Telegram tương ứng. Các sếp cần chỉnh sửa đoạn code JavaScript bên trong để thêm danh sách Chat ID Telegram khớp với tên hoặc email nhân sự trên Jira.
- **`check issue body, assignee and hook type` & `check tg account exists` (If Nodes):** 
  - Kiểm tra xem các trường dữ liệu bắt buộc (như nội dung, người được gán task) có tồn tại hay không và đảm bảo tài khoản Telegram của người đó đã được cấu hình trước khi gửi tin.
- **`check type` (Switch Node):** 
  - Phân loại sự kiện từ Jira (Tạo mới, Cập nhật, hay Thay đổi người phụ trách) để điều hướng dòng chảy dữ liệu chính xác.
- **`Send Update`, `Send Create`, `Send Assign Alert` (Telegram Nodes):** 
  - Kết nối với **Telegram API Credentials** của các sếp. Tùy chỉnh nội dung tin nhắn (Text template) hiển thị mã task, tiêu đề, trạng thái và đường dẫn trực tiếp đến Jira task.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và thử tạo/cập nhật một task trên Jira để kiểm tra xem dữ liệu có đổ về Telegram chính xác không.
- Sau khi test thành công, bật công tắc **Active** ở góc trên bên phải để workflow chạy tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo:** Kết hợp thêm node **Slack** hoặc **Microsoft Teams** nếu tổ chức của các sếp sử dụng đa nền tảng chat.
- **Lưu log hệ thống:** Thêm một node Google Sheets hoặc Airtable ở cuối luồng để ghi lại lịch sử các thông báo đã gửi thành công phục vụ việc kiểm tra.
- **Báo cáo định kỳ:** Tạo thêm một nhánh chạy lịch (Schedule Trigger) để tổng hợp số lượng task chưa hoàn thành gửi vào nhóm Telegram của team vào cuối mỗi ngày.

### 📌 Kết luận
Việc tự động hóa thông báo Jira qua Telegram Bot sẽ giúp tối ưu hóa luồng giao tiếp trong dự án, loại bỏ tình trạng "quên task" và đẩy nhanh tiến độ công việc của toàn đội ngũ. Hãy cài đặt ngay hôm nay để trải nghiệm sự khác biệt!