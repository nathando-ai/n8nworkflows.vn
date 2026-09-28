---
title: "🚀 Tự động hóa theo dõi trạng thái Deal CRM với HighLevel, ClickUp và Slack trên n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động đồng bộ deal từ HighLevel CRM, phân loại theo thời gian, tạo task trên ClickUp cho deal mới và bắn thông báo Slack cho deal cũ."
slug: "tu-dong-hoa-theo-doi-trang-thai-deal-highlevel-clickup-slack"
tags: [n8n, automation, highlevel, clickup, slack, crm]
keywords: [n8n workflow, highlevel crm automation, clickup integration, slack notification n8n, tự động hóa crm]
---

# 🚀 Tự động hóa theo dõi trạng thái Deal CRM với HighLevel, ClickUp và Slack

Các sếp có đang gặp tình trạng nhân viên sales quên cập nhật trạng thái deal, hoặc tốn quá nhiều thời gian thủ công để chuyển từ CRM sang công cụ quản lý dự án như ClickUp? Việc bỏ sót các cơ hội kinh doanh (deal) hoặc không phân loại được deal mới và cũ chắc chắn sẽ làm giảm tỷ lệ chốt sale của đội ngũ.

Giải pháp ở đây là gì? Workflow n8n này sẽ tự động hóa toàn bộ quy trình: lấy danh sách deal từ **HighLevel CRM**, lọc theo mốc thời gian cập nhật, tự động tạo task hành động trên **ClickUp** đối với deal mới, đồng thời gửi cảnh báo qua **Slack** cho các deal cũ cần xem xét lại. Tất cả diễn ra hoàn toàn tự động mà không cần tốn một phút nhập liệu thủ công nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Không còn lo nhân viên quên tạo task follow-up trên ClickUp sau mỗi thay đổi trạng thái deal.
- **Phân loại thông minh:** Tự động tách biệt deal mới cập nhật để xử lý ngay và deal cũ cần chú ý đặc biệt.
- **Tăng tốc độ phản hồi:** Đội ngũ làm việc nhận thông tin tức thì qua ClickUp và Slack, không bỏ lỡ bất kỳ khách hàng tiềm năng nào.
- **Vận hành liền mạch:** Kết nối trơn tru giữa hệ thống CRM (HighLevel), Task Management (ClickUp) và Team Chat (Slack).
:::

### 📦 Các Nodes chính trong Workflow
Workflow này sử dụng 6 nodes được tối ưu hóa hoàn hảo:
1. **Manual Trigger** (`manualTrigger`): Khởi chạy thủ công để test hoặc chạy đồng bộ theo nhu cầu.
2. **Fetch All Deals from CRM1** (`highLevel`): Lấy toàn bộ danh sách cơ hội (opportunities) từ HighLevel CRM.
3. **Filter Recent Deal Updates1** (`if`): Lọc và phân chia deal dựa trên mốc thời gian cập nhật (ví dụ: từ 30/09/2025 trở về sau).
4. **Get Contact Details1** (`highLevel`): Lấy thông tin chi tiết liên hệ của deal mới cập nhật.
5. **Create ClickUp Task1** (`clickUp`): Tự động tạo task mới trên ClickUp kèm theo thông tin khách hàng.
6. **Notify Old Deal Update1** (`slack`): Gửi cảnh báo qua Slack cho các deal cũ chưa được cập nhật gần đây.

---

### 🔧 Yêu cầu cần thiết
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản và quyền truy cập sau:
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **HighLevel CRM Account:** Có tài khoản quản trị và quyền API/OAuth2 để lấy thông tin cơ hội và liên hệ.
- **ClickUp Account:** Đã tạo sẵn Space, Folder và List để workflow tự động đổ task vào.
- **Slack Workspace:** Đã cài đặt bot/app n8n để gửi tin nhắn thông báo.

---

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow hoặc copy đoạn mã JSON được cung cấp.
- Mở giao diện n8n Editor, chọn **Add workflow** -> **Import from File** hoặc dán trực tiếp vào màn hình làm việc.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Khi đã đưa workflow lên canvas, các sếp cần cấu hình chính xác các thông số sau:

- **Node `Fetch All Deals from CRM1` (HighLevel):**
  - Kết nối Credentials tài khoản HighLevel CRM qua OAuth2.
  - Kiểm tra lại Resource (`opportunity`) và Operation (`getAll`) để đảm bảo hệ thống lấy đúng danh sách deal.
- **Node `Filter Recent Deal Updates1` (IF):**
  - Cấu hình điều kiện thời gian (Date Filter) phù hợp với thực tế doanh nghiệp của các sếp (Mặc định trong template đang check mốc từ ngày 30/09/2025). Nhánh **TRUE** dành cho deal mới cập nhật, nhánh **FALSE** dành cho deal cũ.
- **Node `Get Contact Details1` (HighLevel):**
  - Sử dụng `contactId` được trả về từ danh sách deal ở bước trước để gọi API lấy thông tin chi tiết khách hàng.
- **Node `Create ClickUp Task1` (ClickUp):**
  - Kết nối Credentials ClickUp API.
  - Chọn đúng Workspace, Space, Folder và List mà các sếp muốn tạo task.
  - Map các trường dữ liệu (Task Name, Description) với tên khách hàng và thông tin location từ HighLevel.
- **Node `Notify Old Deal Update1` (Slack):**
  - Kết nối Credentials Slack API.
  - Chọn kênh hoặc người nhận thông báo (`n8n_workspace` hoặc channel riêng của đội ngũ sales) để nhận cảnh báo về các deal cũ cần chăm sóc.

#### 3. Kích hoạt ⚡️
- Nhấn nút **Execute Workflow** trên node **Manual Trigger** để chạy thử nghiệm với dữ liệu thực tế.
- Kiểm tra xem task đã được tạo bên ClickUp và tin nhắn đã bắn về Slack hay chưa.
- Sau khi test thành công, bật công tắc **Active** ở góc trên bên phải để workflow tự động vận hành.

---

### ✍️ Mẹo & gợi ý nâng cao
Để tối ưu hóa hơn nữa quy trình này, các sếp có thể cân nhắc:
- **Thay thế Trigger:** Chuyển từ `Manual Trigger` sang `Webhook` hoặc `HighLevel Trigger` để hệ thống tự động chạy ngay khi có deal mới thay đổi trạng thái trong CRM mà không cần bấm tay.
- **Ghi Log vào Google Sheets:** Thêm một node Google Sheets để lưu lại lịch sử các deal đã được đồng bộ sang ClickUp hoặc Slack nhằm phục vụ việc kiểm tra sau này.
- **Mở rộng kênh thông báo:** Kết hợp thêm Zalo ZNS hoặc Telegram bên cạnh Slack để đội ngũ sales nhận tin nhắn theo nhiều kênh khác nhau.

---

### 📌 Kết luận
Việc tự động hóa đồng bộ deal từ HighLevel CRM sang ClickUp và Slack không chỉ giúp tiết kiệm hàng giờ đồng hồ làm việc thủ công mỗi tuần mà còn đảm bảo không có khách hàng tiềm năng nào bị bỏ sót. Hãy cài đặt ngay workflow này để tối ưu hóa hiệu suất làm việc cho đội ngũ sales của các sếp ngay hôm nay!