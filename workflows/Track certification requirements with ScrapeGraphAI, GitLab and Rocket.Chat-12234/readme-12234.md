---
title: "🚀 Theo dõi yêu cầu chứng chỉ với ScrapeGraphAI, GitLab và Rocket.Chat"
description: "Tự động hóa theo dõi yêu cầu chứng chỉ từ các cơ quan cấp chứng chỉ, phát hiện thay đổi và thông báo qua Rocket.Chat"
slug: "theo-doi-yeu-cau-chung-chi-voi-scrapegraphai-gitlab-rocketchat"
tags: [n8n, automation, no-code, AI, GitLab, Rocket.Chat]
keywords: [n8n workflow, tự động hóa, theo dõi chứng chỉ, ScrapeGraphAI, GitLab, Rocket.Chat]
---

# 🚀 Theo dõi yêu cầu chứng chỉ với ScrapeGraphAI, GitLab và Rocket.Chat

[Các sếp đang làm việc trong lĩnh vực quản lý chứng chỉ thường phải đối mặt với thách thức theo dõi các yêu cầu cập nhật liên tục từ các cơ quan cấp chứng chỉ. Việc thủ công kiểm tra từng trang web của các cơ quan này không chỉ tốn thời gian mà còn dễ bỏ sót những thay đổi quan trọng. Workflow này giúp tự động hóa toàn bộ quá trình này, từ thu thập thông tin đến phát hiện thay đổi và thông báo kịp thời.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động thu thập thông tin từ các trang web của cơ quan cấp chứng chỉ
- Phát hiện thay đổi trong yêu cầu chứng chỉ một cách chính xác
- Thông báo kịp thời qua Rocket.Chat khi có thay đổi quan trọng
- Lưu trữ lịch sử thay đổi trong GitLab để đảm bảo tuân thủ quy định
- Tiết kiệm thời gian và giảm thiểu lỗi do kiểm tra thủ công
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản ScrapeGraphAI với API key
- Tài khoản GitLab với quyền truy cập vào repository
- Tài khoản Rocket.Chat với quyền gửi tin nhắn vào kênh
- Danh sách URL của các trang web cần theo dõi
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập trang [workflow gốc](https://n8n.io/workflows/12234)
2. Click vào nút "Download" để tải file JSON
3. Trong n8n Editor, click vào menu "Workflow" > "Import from File"
4. Chọn file JSON vừa tải về và click "Open"

Hoặc bạn có thể copy/paste JSON từ trang workflow gốc vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Incoming Webhook"**:
   - Đảm bảo đường dẫn "certification-requirements" phù hợp với cấu trúc URL của bạn
   - Phương thức HTTP nên được giữ nguyên là POST

2. **Node "Prepare Certification URLs"**:
   - Chỉnh sửa danh sách URL trong code để phù hợp với các trang web bạn cần theo dõi
   - Mỗi URL nên được đặt trong một đối tượng JSON riêng biệt

3. **Node "Scrape Certification Requirements"**:
   - Thêm credentials cho ScrapeGraphAI
   - Đảm bảo API key được nhập chính xác

4. **Node "Get Baseline From GitLab" và "Update GitLab Record"**:
   - Thêm credentials cho GitLab
   - Chỉnh sửa tham số "resource" thành "repositoryFile"
   - Cấu hình đường dẫn file và nhánh phù hợp với repository của bạn

5. **Node "Send Rocket.Chat Alert"**:
   - Thêm credentials cho Rocket.Chat
   - Chỉnh sửa tên kênh để phù hợp với kênh bạn muốn gửi thông báo

#### 3. Kích hoạt ⚡️
1. Sau khi cấu hình xong tất cả các node, hãy thực hiện test run với dữ liệu mẫu
2. Kiểm tra kết quả ở các node cuối cùng (Rocket.Chat và GitLab)
3. Nếu mọi thứ hoạt động đúng, bật chế độ Active cho workflow

### ✍️ Mẹo & gợi ý nâng cao
1. Thêm lịch trình tự động gọi webhook để cập nhật thông tin định kỳ
2. Kết hợp với Slack để nhận thông báo thay đổi
3. Lưu log các lần chạy workflow để theo dõi hiệu suất
4. Tạo báo cáo định kỳ về trạng thái của các yêu cầu chứng chỉ

### 📌 Kết luận
Workflow này giúp các sếp quản lý chứng chỉ tự động theo dõi các thay đổi quan trọng từ các cơ quan cấp chứng chỉ, giảm thiểu rủi ro bỏ sót thông tin quan trọng và tiết kiệm thời gian đáng kể. Hãy thử áp dụng ngay để nâng cao hiệu quả quản lý chứng chỉ của bạn!