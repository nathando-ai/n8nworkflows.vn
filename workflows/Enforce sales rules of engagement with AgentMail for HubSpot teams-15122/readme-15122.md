---
title: "🚀 Tự động hóa quy tắc Sales Engagement cho HubSpot với AgentMail & n8n"
description: "Giải pháp tự động hóa 49 nodes giúp quản lý hộp thư, thực thi quy tắc phân cấp bán hàng (AE, BDR, Marketing), và tự động bật Reply Shield khi khách hàng phản hồi."
slug: "tu-dong-hoa-quy-tac-sales-engagement-hubspot-agentmail-n8n"
tags: [n8n, automation, hubspot, agentmail, crm, sales-ops]
keywords: [n8n workflow, sales engagement, hubspot automation, agentmail, quan ly hop thu sales]
---

# 🚀 Tự động hóa quy tắc Sales Engagement cho HubSpot với AgentMail

Trong các đội ngũ Sales hiện đại, việc phối hợp giữa các kênh Marketing, BDR và AE (Account Executive) thường gặp tình trạng chồng chéo email, gửi nhầm email marketing khi khách hàng đã phản hồi, hoặc không đồng bộ được quy tắc phân cấp (hierarchy). Làm thủ công việc này vừa tốn thời gian vừa dễ gây mất điểm trước khách hàng lớn.

Workflow này giải quyết triệt để vấn đề trên với **49 nodes thông minh**, tự động hóa toàn bộ quy trình: từ khởi tạo schema database, đồng bộ webhook, thực thi phân cấp gửi email, cho đến tính năng **Reply Shield** tự động ngắt chuỗi nurture khi khách hàng có tín hiệu tương tác.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Loại bỏ trùng lặp:** Tự động chặn các inbox cấp thấp hơn (Marketing, BDR) khi AE đã bắt đầu gửi email cho prospect.
- **Bảo vệ cuộc trò chuyện (Reply Shield):** Ngay khi khách hàng phản hồi (`message.received`), hệ thống tự động gắn nhãn (label) và chặn toàn bộ email tự động gửi đi để tránh làm phiền khách.
- **Quản lý tập trung:** Sử dụng `Team_Config` Data Table trong n8n làm nguồn chân lý (source of truth), không cần hardcode email hay cấu hình phức tạp.
- **Tự động dọn dẹp (Decay Timer & Cleanup):** Tự động xóa block list theo hạn định (decay days) và dọn dẹp các inbox mồ côi hàng tuần.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Phiên bản hỗ trợ Data Table).
- **AgentMail Account & API Key:** Cần có tài khoản và Bearer Token để kết nối với hệ thống AgentMail qua các HTTP Request nodes.
- **HubSpot CRM:** Nền tảng quản lý quan hệ khách hàng (tùy chọn kết hợp theo quy trình sales của đội ngũ).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Copy toàn bộ mã JSON của workflow và paste trực tiếp vào trình soạn thảo n8n của các sếp, hoặc import file JSON trực tiếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Khởi tạo Database lần đầu:** Chạy node `1. Create Schema` và `3. Populate Database` **ĐÚNG MỘT LẦN DUY NHẤT** (hoặc làm theo ghi chú `DATABASE SETUP`) để tạo bảng `Team_Config` với cấu hình 3 tầng (AE, BDR, Marketing). Sau đó vào menu Data bên trái n8n để tùy chỉnh lại email của team.
- **Cấu hình Webhook URL:** Tại các node `📡 Register Webhook` và các Webhook trigger (`⚡ Webhook: message.sent`, `⚡ Webhook: message.received`), hãy đảm bảo URL trỏ đúng về địa chỉ n8n công khai của các sếp (Production URL).
- **Credentials:** Thiết lập thông tin xác thực `httpBearerAuth` cho toàn bộ các node `httpRequest` gọi tới API của AgentMail.

#### 3. Kích hoạt ⚡️
- Bấm `Execute Workflow` thủ công với node `When clicking ‘Execute workflow’` để kiểm tra kết quả khởi tạo cấu hình.
- Bật công tắc **Active** ở góc trên bên phải để kích hoạt các Webhook lắng nghe sự kiện từ AgentMail chạy 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Slack/Telegram:** Thêm node gửi thông báo vào kênh chat nội bộ ngay khi node `📊 Compile Audit Report` hoặc `✅ Provisioning Report` chạy xong để Sales Manager nắm tình hình.
- **Mở rộng Decay Window:** Tùy chỉnh cột `decay_days` trong bảng `Team_Config` Data Table để kéo dài hoặc rút ngắn thời gian chặn block list phù hợp với chiến dịch của công ty.
- **Báo cáo định kỳ:** Tận dụng `Weekly (Sun 00:00) - hoặc put it to ANYTHING you like` Schedule Trigger để tự động tổng hợp báo cáo tuần gửi qua email.

### 📌 Kết luận
Workflow này là cỗ máy tự động hóa hoàn hảo giúp siết chặt quy trình sales engagement, bảo vệ uy tín thương hiệu và tối ưu hóa hiệu suất làm việc nhóm giữa các tầng Marketing, BDR và AE. Áp dụng ngay hôm nay để tối ưu hóa đội ngũ sales của các sếp!