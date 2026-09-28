---
title: "🚀 Đồng bộ danh bạ từ Microsoft Entra ID lên Zammad tự động với n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động đồng bộ danh bạ từ Microsoft Entra (Azure AD) sang hệ thống Helpdesk Zammad, giúp quản lý người dùng chính xác và tiết kiệm thời gian."
slug: "dong-bo-danh-ba-entra-to-zammad-n8n"
tags: [n8n, automation, zammad, entra-id, microsoft, helpdesk, sync]
keywords: [n8n workflow, đồng bộ entra id zammad, tự động hóa zammad, microsoft graph api n8n, quan ly nguoi dung zammad]
---

# 🚀 Đồng bộ danh bạ từ Microsoft Entra ID lên Zammad tự động với n8n

Việc quản lý người dùng thủ công giữa hệ thống danh bạ nhân sự Microsoft Entra (trước đây là Azure AD) và hệ thống hỗ trợ khách hàng (Helpdesk) Zammad thường tiêu tốn rất nhiều thời gian của bộ phận IT. Khi có nhân sự mới, thay đổi thông tin hay nghỉ việc, việc cập nhật không đồng bộ dễ dẫn đến việc sót tài khoản hoặc phân quyền nhầm lẫn.

Giải pháp tuyệt vời cho các sếp chính là **Workflow n8n: Entra Contacts to Zammad User Sync** – tự động hóa toàn bộ quy trình lấy danh bạ từ Microsoft Entra ID, so sánh và tự động tạo mới, cập nhật hoặc vô hiệu hóa người dùng trên Zammad một cách chính xác 100% không cần can thiệp thủ công.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Danh bạ Zammad luôn đồng bộ sát sao với Microsoft Entra ID mà không cần nhập liệu thủ công.
- **Xử lý thông minh:** Tự động phát hiện user mới để **tạo mới**, user thay đổi thông tin để **cập nhật**, và user bị xóa/nghỉ việc để **vô hiệu hóa** (Deactivate).
- **Tiết kiệm thời gian & Loại bỏ sai sót:** Giảm thiểu gánh nặng cho bộ phận IT, đảm bảo tính bảo mật khi nhân sự nghỉ việc sẽ bị vô hiệu hóa quyền truy cập hệ thống support ngay lập tức.
- **Vận hành liên tục:** Có thể cấu hình chạy định kỳ (Cron trigger) để cập nhật ngầm hàng ngày hoặc hàng giờ.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản và quyền hạn sau:
- **n8n Instance:** Đã cài đặt sẵn sàng (Cloud hoặc Self-hosted).
- **Microsoft Entra ID (Azure AD):** Quyền truy cập qua Microsoft Graph API (cần App Registration với scope phù hợp để đọc contacts/users).
- **Zammad Helpdesk:** Tài khoản quản trị viên và **API Token** hoặc thông tin xác thực để kết nối qua `zammadTokenAuthApi`.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON từ trang n8n templates (link gốc workflow #2599) hoặc copy toàn bộ JSON của workflow dán trực tiếp vào n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 13 nodes hoạt động nhịp nhàng. Các sếp cần chú ý cấu hình kỹ các node trọng điểm sau:

- **Get Contacts from Entra (`httpRequest`):**
  - Cấu hình kết nối `microsoftOAuth2Api` hoặc `microsoftGraphSecurityOAuth2Api`.
  - Trỏ Endpoint tới Microsoft Graph API để lấy danh sách contacts/users (ví dụ: `https://graph.microsoft.com/v1.0/users` hoặc `contacts`).
- **Entra Contacts (`splitOut`) & Các bộ lọc (`if`):**
  - Sử dụng node **Entra Contacts** để tách mảng dữ liệu trả về từ Microsoft.
  - Các node **Filter contacts if needed** và **Filter if needed** giúp các sếp lọc ra các đối tượng cụ thể cần đồng bộ (ví dụ: chỉ lấy nhân viên thuộc phòng ban cụ thể, loại bỏ tài khoản hệ thống).
- **Zammad Nodes (`zammad`):**
  - **Get Zammad Users:** Lấy toàn bộ danh sách user hiện tại trên Zammad bằng `zammadTokenAuthApi` để làm dữ liệu đối chiếu.
  - **Create Zammad User:** Tạo mới user khi phát hiện nhân sự mới từ Entra.
  - **Update Zammad User:** Cập nhật thông tin khi nhân sự có thay đổi.
  - **Deactivate Zammad User:** Vô hiệu hóa tài khoản trên Zammad khi không còn tồn tại trong danh bạ Entra.
- **So sánh dữ liệu (`compareDatasets`):**
  - Node **Find new Zammad Users** và **Find removed Users** đóng vai trò cốt lõi để so sánh sự chênh lệch giữa danh bạ Entra và Zammad, từ đó quyết định hành động Create, Update hay Deactivate.

#### 3. Kích hoạt ⚡️
- Nhấn **Test workflow** (sử dụng node `manualTrigger`) để chạy thử nghiệm và kiểm tra dữ liệu trả về qua từng node.
- Sau khi kiểm tra mọi thứ chạy mượt mà, hãy thay thế node `manualTrigger` bằng **Schedule Trigger** (đặt lịch chạy hàng ngày/hàng tuần) và chuyển trạng thái workflow sang **Active**.

### ✍️ Mẹo & gợi ý nâng cao
- **Thêm thông báo qua Telegram/Slack:** Gắn thêm node Telegram hoặc Slack vào cuối chuỗi xử lý để nhận báo cáo mỗi khi có nhân sự mới được tạo hoặc vô hiệu hóa trên Zammad.
- **Lưu lịch sử đồng bộ (Log):** Thêm một node Google Sheets hoặc Database phụ để ghi log lại các thao tác đồng bộ phục vụ việc kiểm tra sau này.
- **Xử lý lỗi (Error Handling):** Bật tính năng *Error Workflow* của n8n để nhận cảnh báo ngay lập tức nếu việc kết nối với Microsoft Graph API hoặc Zammad gặp sự cố.

### 📌 Kết luận
Workflow **Entra Contacts to Zammad User Sync** là trợ thủ đắc lực giúp tự động hóa khâu quản trị người dùng giữa hệ thống định danh Microsoft và hệ thống Support Zammad. Hãy triển khai ngay hôm nay để tối ưu hóa quy trình vận hành CNTT cho doanh nghiệp của các sếp!