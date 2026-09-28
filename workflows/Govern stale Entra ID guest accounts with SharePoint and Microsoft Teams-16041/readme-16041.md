---
title: "🚀 Tự động quản trị tài khoản khách Entra ID (Guest Accounts) với SharePoint và Microsoft Teams"
description: "Hướng dẫn chi tiết workflow n8n giúp tự động phát hiện tài khoản khách Entra ID không hoạt động, thông báo người bảo trợ qua Microsoft Teams và xử lý xóa/giữ lại qua SharePoint."
slug: "quan-tri-tai-khoan-khach-entra-id-sharepoint-teams"
tags: [n8n, automation, microsoft-entra, sharepoint, microsoft-teams, secops]
keywords: [n8n workflow, quản lý entra id, guest accounts, tự động hóa secops, microsoft graph api, sharepoint automation]
usecase: "SecOps & IT Administration"
---

# 🚀 Tự động quản trị tài khoản khách Entra ID với SharePoint và Microsoft Teams

Các sếp làm trong lĩnh vực IT Security hay System Administration chắc chắn đều đau đầu với việc quản lý tài khoản khách (Guest Accounts) trên Microsoft Entra ID (Azure AD). Khách mời ra vào công ty, tài khoản được tạo ra nhưng rất ít khi được dọn dẹp thủ công, dẫn đến rủi ro bảo mật nghiêm trọng khi các tài khoản "ma" này vẫn còn quyền truy cập hệ thống.

Giải pháp thủ công vừa tốn thời gian, vừa dễ bỏ sót. Workflow n8n hoành tráng gồm 54 nodes này sinh ra để giải quyết triệt để bài toán đó: **Tự động quét hàng tuần, đối soát qua SharePoint, cảnh báo người bảo trợ (Sponsor) hoặc đội ngũ IT qua Microsoft Teams, và tự động xóa hoặc lưu giữ tài khoản theo chính sách bảo mật.**

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Quét định kỳ hàng tuần tìm tài khoản khách không hoạt động (stale accounts) và thực thi dọn dẹp hàng ngày.
- **Bảo mật & Minh bạch:** Tự động ghi lại nhật ký kiểm toán (Audit logs) trên SharePoint cho mọi hành động xóa hoặc giữ lại tài khoản.
- **Tương tác thông minh:** Gửi thông báo trực tiếp đến Sponsor qua Microsoft Teams hoặc cảnh báo IT Security nếu tài khoản không có người bảo trợ hợp lệ.
- **Kiểm soát ngoại lệ:** Dễ dàng cấu hình danh sách ngoại lệ (Retention exceptions) để tránh xóa nhầm các tài khoản khách quan trọng.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã kích hoạt và sẵn sàng sử dụng (khuyên dùng bản Self-hosted trên VPS).
- **Microsoft Entra ID / Graph API Credentials:** Cấp quyền đọc người dùng (Read users) và xóa tài khoản khách (Delete guest accounts).
- **Microsoft SharePoint:** Đã tạo sẵn các danh sách (Lists) phục vụ cho:
  - Pending Deletions (Chờ xóa)
  - Audit Logs (Nhật ký kiểm toán)
  - Retention Exceptions (Danh sách ngoại lệ)
- **Microsoft Teams Credentials:** Quyền gửi tin nhắn vào Channel cụ thể.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow từ nguồn cấp hoặc copy toàn bộ JSON dán trực tiếp vào n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Vì workflow có tới 54 nodes chia thành 2 luồng chính (Quét hàng tuần và Thực thi hàng ngày), các sếp cần chú ý các điểm sau:
- **Các node Config (`Config`, `Config (Executioner)`, `Set Configuration Parameters`,...):** Điền chính xác các thông số quan trọng như:
  - SharePoint Site ID
  - List IDs (Pending Deletions, Audit Log, Retention Exceptions)
  - Microsoft Teams Team ID và Channel ID
- **Nodes Microsoft Entra & Graph API (`Get Guest Users`, `Delete Stale Guest Account`, v.v.):** Đảm bảo cấu hình OAuth2 hoặc App Credentials đã được cấp đủ Scope (`User.Read.All`, `User.ReadWrite.All`, `Directory.ReadWrite.All`).
- **Nodes Code lọc tài khoản (`Filter Stale Accounts`, `Filter Stale Per Page`, v.v.):** Kiểm tra lại ngưỡng thời gian không hoạt động (stale-account age threshold) trong code JavaScript cho phù hợp với chính sách nội bộ của công ty.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm thủ công (Test run) trên một vài bản ghi mẫu để kiểm tra luồng thông báo Teams và ghi dữ liệu SharePoint.
- Sau khi mọi thứ chạy mượt mà, bật công tắc **Active** để hệ thống tự động chạy ngầm theo lịch trình (Cron Trigger hàng tuần và hàng ngày).

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thêm kênh liên lạc:** Ngoài Microsoft Teams, các sếp có thể mở rộng nhánh thông báo lỗi sang **Telegram** hoặc **Slack** để đội ngũ SecOps nhận tin nhanh hơn.
- **Báo cáo định kỳ:** Thêm một node Cron chạy vào cuối tháng để tổng hợp số lượng tài khoản khách đã dọn dẹp và gửi báo cáo tóm tắt qua Email.
- **Quản lý ngoại lệ động:** Xây dựng một giao diện nhỏ trên SharePoint để các phòng ban có thể tự đăng ký gia hạn tài khoản khách mà không cần làm phiền đến IT.

### 📌 Kết luận
Workflow quản trị tài khoản khách Entra ID này là một "vũ khí tối thượng" giúp tự động hóa khâu dọn dẹp rác kỹ thuật số, nâng cao điểm số bảo mật (Security Posture) cho tổ chức của các sếp. Hãy triển khai ngay hôm nay để tiết kiệm hàng giờ đồng hồ kiểm tra thủ công mỗi tuần!