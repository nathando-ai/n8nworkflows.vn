---
title: "🚀 Tự động hóa Báo cáo Tiền Cuộc Họp với Outlook, SharePoint, Entra ID và Teams"
description: "Giải pháp tự động hóa hoàn toàn không cần code giúp các sếp tiết kiệm 30 phút mỗi ngày bằng cách tự động tổng hợp thông tin cuộc họp, tài liệu liên quan và hồ sơ người tham gia từ các hệ thống Microsoft."
slug: "tu-dong-hoa-bao-cao-tien-cuoc-hop-outlook-sharepoint-entra-id-teams"
tags: [n8n, automation, no-code, microsoft-365, sharepoint, entra-id, teams]
keywords: [n8n workflow, tự động hóa cuộc họp, báo cáo tiền cuộc họp, Microsoft 365, SharePoint, Entra ID, Teams]
---

# 🚀 Tự động hóa Báo cáo Tiền Cuộc Họp với Outlook, SharePoint, Entra ID và Teams

[Các sếp] có bao giờ phải mất 30 phút mỗi ngày để chuẩn bị báo cáo tiền cuộc họp không? Từ việc kiểm tra lịch, tìm tài liệu liên quan đến cuộc họp sắp tới, đến việc tổng hợp hồ sơ người tham gia - tất cả đều là công việc thủ công tẻ nhạt. Với workflow này, các sếp có thể tự động hóa hoàn toàn quy trình này trong vòng 30 phút đầu tiên mỗi ngày, chỉ cần một lần cài đặt.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 30 phút mỗi ngày**: Không cần phải chuẩn bị báo cáo tiền cuộc họp thủ công nữa.
- **Thông tin chính xác và đầy đủ**: Tự động tổng hợp từ Outlook, SharePoint và Entra ID.
- **Tự động hóa hoàn toàn**: Không cần can thiệp thủ công sau khi cài đặt.
- **Hỗ trợ nhiều người dùng**: Xử lý đồng thời nhiều mailbox VIP trong cùng một workflow.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Microsoft 365 với quyền truy cập Outlook, SharePoint, Entra ID và Teams.
- Quyền truy cập API Microsoft Graph với các quyền sau:
  - Calendar.Read
  - User.Read.All
  - User.ReadBasic.All
  - Files.Read.All
  - TeamMember.Read.All
  - ChannelMessage.Read.All
  - Chat.Read
  - Chat.ReadBasic
  - Chat.ReadWrite
  - Chat.Create
  - ChatMessage.Send
- Danh sách mailbox VIP cần theo dõi.
- ID người dùng Teams nhận báo cáo.
- ID site SharePoint chứa tài liệu liên quan.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/16107](https://n8n.io/workflows/16107)
2. Chọn "Import" và sao chép JSON workflow vào n8n Editor của bạn.
3. Hoặc tải file JSON về và import trực tiếp từ n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

- **When Every 30 Minutes**: Node này đã được cấu hình sẵn với lịch chạy mỗi 30 phút. Các sếp có thể điều chỉnh thời gian chạy nếu cần.

- **Set Config Parameters**: Cần cấu hình các tham số sau:
  - `vipMailboxes`: Danh sách mailbox VIP cần theo dõi (ví dụ: ["user1@company.com", "user2@company.com"]).
  - `briefingRecipient`: ID người dùng Teams nhận báo cáo (ví dụ: "user@company.com").
  - `sharePointSiteId`: ID site SharePoint chứa tài liệu liên quan (ví dụ: "company.sharepoint.com,123456,abcdef").
  - `minutesBeforeMeeting`: Số phút trước cuộc họp để gửi báo cáo (ví dụ: 30).

- **Loop Over VIP Mailboxes**: Node này đã được cấu hình sẵn để lặp qua danh sách mailbox VIP.

- **Extract VIP Mailbox Data**: Node này đã được cấu hình sẵn để trích xuất dữ liệu mailbox VIP.

- **Fetch Calendar Events**: Cần chọn credentials Microsoft Outlook và cấu hình các tham số sau:
  - `resource`: "event".
  - `operation`: "getAll".
  - `additionalFields`: Cấu hình các trường cần thiết như `filter` để lấy các sự kiện sắp tới.

- **Filter Events for Briefing**: Node này đã được cấu hình sẵn để lọc các sự kiện cần báo cáo.

- **Check Events to Brief**: Node này đã được cấu hình sẵn để kiểm tra xem có sự kiện nào cần báo cáo hay không.

- **No Events Switch Mailbox**: Node này đã được cấu hình sẵn để chuyển sang mailbox tiếp theo nếu không có sự kiện nào cần báo cáo.

- **Loop Through Events**: Node này đã được cấu hình sẵn để lặp qua các sự kiện cần báo cáo.

- **Extract Event Data**: Node này đã được cấu hình sẵn để trích xuất dữ liệu sự kiện.

- **Post to SharePoint Search API**: Cần cấu hình các tham số sau:
  - `method`: "POST".
  - `url`: "https://graph.microsoft.com/v1.0/search/query".
  - `headers.contentType`: "application/json".
  - `body`: Cấu hình các trường cần thiết như `requests` để tìm kiếm tài liệu liên quan.

- **Build Attendee Request Payload**: Node này đã được cấu hình sẵn để xây dựng payload cho yêu cầu hồ sơ người tham gia.

- **Post to Graph API for Attendees**: Cần cấu hình các tham số sau:
  - `method`: "POST".
  - `url`: "https://graph.microsoft.com/v1.0/$batch".
  - `headers.contentType`: "application/json".
  - `body`: Cấu hình các trường cần thiết như `requests` để lấy hồ sơ người tham gia.

- **Compile Event Briefing**: Node này đã được cấu hình sẵn để biên soạn báo cáo sự kiện.

- **Dispatch Briefing to Teams**: Cần chọn credentials Microsoft Teams và cấu hình các tham số sau:
  - `resource`: "chatMessage".
  - `operation`: "create".
  - `additionalFields`: Cấu hình các trường cần thiết như `chatId` để gửi báo cáo đến người dùng Teams.

- **Proceed to Next Event**: Node này đã được cấu hình sẵn để chuyển sang sự kiện tiếp theo.

- **All Mailboxes Completed**: Node này đã được cấu hình sẵn để thông báo khi đã xử lý xong tất cả mailbox.

- **Teams Briefing Error Notice**: Cần chọn credentials Microsoft Teams và cấu hình các tham số sau:
  - `resource`: "chatMessage".
  - `operation`: "create".
  - `additionalFields`: Cấu hình các trường cần thiết như `chatId` để gửi thông báo lỗi đến người dùng Teams.

- **Check Briefing Sent Status**: Node này đã được cấu hình sẵn để kiểm tra trạng thái gửi báo cáo.

- **Merge Data Before Next Event**: Node này đã được cấu hình sẵn để hợp nhất dữ liệu trước khi chuyển sang sự kiện tiếp theo.

- **Mark Event as Briefed**: Node này đã được cấu hình sẵn để đánh dấu sự kiện đã được báo cáo.

- **Combine Batch API Response**: Node này đã được cấu hình sẵn để hợp nhất phản hồi từ API batch.

- **Combine SP Search Response**: Node này đã được cấu hình sẵn để hợp nhất phản hồi từ tìm kiếm SharePoint.

- **Check for Attendee Requests**: Node này đã được cấu hình sẵn để kiểm tra xem có yêu cầu hồ sơ người tham gia hay không.

- **Skip Attendee Batch Processing**: Node này đã được cấu hình sẵn để bỏ qua xử lý batch hồ sơ người tham gia nếu không có yêu cầu.

- **Build SharePoint Query**: Node này đã được cấu hình sẵn để xây dựng truy vấn SharePoint.

#### 3. Kích hoạt ⚡️
1. Sau khi cấu hình xong các node quan trọng, các sếp cần kiểm tra workflow bằng cách chạy thử với dữ liệu mẫu.
2. Sau khi đảm bảo workflow hoạt động đúng, các sếp có thể kích hoạt workflow bằng cách bật nút "Active" ở góc trên bên phải của n8n Editor.

### ✍️ Mẹo & gợi ý nâng cao
- **Tùy chỉnh báo cáo**: Các sếp có thể điều chỉnh nội dung báo cáo trong node "Compile Event Briefing" để phù hợp với nhu cầu của tổ chức.
- **Thêm thông báo lỗi**: Các sếp có thể cấu hình node "Teams Briefing Error Notice" để gửi thông báo lỗi đến kênh Teams cụ thể.
- **Tích hợp với Slack**: Các sếp có thể thêm node Slack để gửi báo cáo đến kênh Slack thay vì Teams.
- **Lưu log hoạt động**: Các sếp có thể thêm node để lưu log hoạt động của workflow để theo dõi và phân tích hiệu suất.

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm thời gian và công sức trong việc chuẩn bị báo cáo tiền cuộc họp. Với việc tự động hóa hoàn toàn quy trình này, các sếp có thể tập trung vào các công việc quan trọng hơn. Hãy áp dụng ngay workflow này để nâng cao hiệu suất làm việc của tổ chức!