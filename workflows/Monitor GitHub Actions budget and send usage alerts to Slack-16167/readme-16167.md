---
title: "🚀 Tự động giám sát ngân sách GitHub Actions và gửi cảnh báo qua Slack với n8n"
description: "Xây dựng hệ thống tự động kiểm tra hạn mức GitHub Actions hằng ngày, tính toán tốc độ tiêu hao ngân sách và gửi cảnh báo khẩn cấp qua Slack trước khi hóa đơn vượt kiểm soát."
slug: "giam-sat-ngan-sach-github-actions-slack-n8n"
tags: [n8n, automation, github-actions, slack, devops, finops]
keywords: [n8n workflow, github actions budget, slack alert, devops automation, quản lý chi phí github]
---

# 🚀 Tự động giám sát ngân sách GitHub Actions và gửi cảnh báo qua Slack

Các sếp làm DevOps, Platform Engineering hay FinOps chắc chắn đã từng "thót tim" khi nhận hóa đơn GitHub Actions cuối tháng vì lượng build tăng đột biến mà không kiểm soát kịp. Việc kiểm tra thủ công từng repository vừa tốn thời gian, vừa dễ bỏ sót.

Giải pháp đây rồi! Workflow n8n này sẽ tự động hóa toàn bộ quy trình: thu thập dữ liệu sử dụng, tính toán tốc độ tiêu hao ngân sách (burn rate), gửi báo cáo tổng kết hằng ngày và lập tức cảnh báo qua Slack nếu chi phí vượt ngưỡng cho phép. Không cần code phức tạp, tự động hóa 100%!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Kiểm soát chi phí chủ động:** Nhận báo cáo chi phí và phút sử dụng GitHub Actions mỗi ngày mà không cần tra cứu thủ công.
- **Cảnh báo thông minh:** Tự động phát hiện và gửi tin nhắn khẩn cấp qua Slack ngay khi chi phí chạm hoặc vượt ngưỡng ngân sách (Threshold) đã định.
- **Dự báo chính xác:** Tính toán tốc độ tiêu hao ngân sách (burn rate) và ước tính tổng tiền phải trả cuối tháng.
- **Vận hành 24/7:** Hoạt động hoàn toàn tự động theo lịch trình đặt sẵn, giúp đội ngũ FinOps yên tâm tuyệt đối.
:::

### Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài nguyên sau:
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **GitHub Account / Organization**: Cần có Personal Access Token (PAT) hoặc OAuth2 với quyền `repo` và `admin:org` (read).
- **Slack Workspace**: Cần Slack Bot Token với quyền `chat:write` để gửi tin nhắn thông báo.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow này và dán trực tiếp vào n8n Editor, hoặc import file JSON thông qua giao diện quản lý workflow của n8n.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow gồm 11 nodes được chia thành 3 giai đoạn: Thu thập (Collect), Phân tích & Tính toán (Analyze & Calculate), Báo cáo & Cảnh báo (Report & Alert). Các sếp cần cấu hình các điểm sau:

- **Node `Configuration` (Set):** Nơi khai báo các tham số cốt lõi như danh sách repository cần theo dõi, ngân sách tháng (monthly budget), ngưỡng cảnh báo (alert threshold %), và chi phí quy đổi trên mỗi phút chạy actions.
- **Node `Fetch Recent Workflow Runs` & `Fetch Org Billing Data` (HTTP Request):** 
  - Kết nối với **GitHub Credentials** (`githubApi` hoặc `githubOAuth2Api`).
  - *Lưu ý cho tài khoản cá nhân (Personal accounts):* Nếu sếp dùng tài khoản cá nhân thay vì Organization, nhớ chỉnh lại URL trong node `Fetch Org Billing Data` thành: `/users/{{owner}}/settings/billing/actions`.
- **Node `Post Daily Summary to Slack` & `Send Urgent Budget Warning` (Slack):**
  - Kết nối với **Slack Credentials** (Bot token).
  - Chọn kênh Slack (Channel) nhận báo cáo hằng ngày và kênh nhận cảnh báo khẩn cấp khi vượt ngân sách.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (**Test run**) thủ công từng node để kiểm tra kết nối API GitHub và Slack xem dữ liệu trả về đã chính xác chưa.
- Sau khi kiểm tra mọi thứ mượt mà, gạt công tắc sang **Active** để workflow chạy tự động theo lịch hằng ngày từ node `Daily Schedule Trigger`.

### ✍️ Mẹo & gợi ý nâng cao
Để tối ưu hóa quy trình giám sát chi phí hơn nữa, các sếp có thể mở rộng workflow:
- **Tích hợp thêm Telegram / Microsoft Teams:** Ngoài Slack, có thể clone node gửi tin nhắn sang các kênh chat nội bộ khác mà team đang sử dụng.
- **Lưu lịch sử vào Google Sheets / Database:** Lưu lại dữ liệu tiêu thụ hằng ngày để vẽ biểu đồ tăng trưởng chi phí theo tuần/tháng.
- **Tự động Disable Workflow tốn phí:** Thêm điều kiện nếu một repo vượt mức giới hạn cho phép, tự động gọi API GitHub để tạm dừng các Actions bất thường.

### 📌 Kết luận
Quản lý chi phí cloud và CI/CD chưa bao giờ dễ dàng đến thế với sức mạnh của tự động hóa n8n. Hãy thiết lập ngay workflow này để bảo vệ ví tiền của doanh nghiệp khỏi những "cú sốc" hóa đơn GitHub Actions cuối tháng nhé các sếp!