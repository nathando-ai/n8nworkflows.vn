---
title: "🚀 Tự động hóa giải quyết GitHub Issues ban đêm với AI qua CloudCLI và Telegram"
description: "Hướng dẫn thiết lập workflow n8n tự động tìm kiếm các GitHub Issue được đánh dấu AI-ready, gọi AI agent xử lý qua CloudCLI và gửi báo cáo tổng kết qua Telegram."
slug: "tu-dong-hoa-github-issues-voi-cloudcli-va-telegram"
tags: [n8n, automation, github, ai, telegram, cloudcli]
keywords: [n8n workflow, github issues automation, cloudcli ai, telegram bot n8n, tu dong hoa code]
---

# 🚀 Tự động hóa giải quyết GitHub Issues ban đêm với AI qua CloudCLI và Telegram

Các sếp làm kỹ sư phần mềm hay quản lý dự án chắc hẳn đều quen thuộc với cảnh hàng đống GitHub Issues cần xử lý mỗi ngày. Việc sàng lọc, tạo nhánh (branch), viết code giải quyết và mở Pull Request (PR) chiếm rất nhiều thời gian thủ công. 

Để giải quyết triệt để vấn đề này, chuyên gia Derek Cheung đã xây dựng một workflow n8n cực kỳ mạnh mẽ: tự động quét các GitHub Issues được gắn nhãn `ai-ready` vào lúc 2 giờ sáng hàng ngày, sử dụng AI Agent từ **CloudCLI** để viết code, tạo PR hoàn chỉnh và gửi báo cáo chi tiết qua **Telegram** ngay khi các sếp thức dậy vào buổi sáng!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian tuyệt đối:** Các Issue được xử lý xuyên đêm, sáng ra chỉ việc review PR và merge.
- **Tự động hóa hoàn toàn:** Từ việc đọc issue, gọi AI agent implement code, đến tạo branch/PR và comment lại trên GitHub.
- **Cập nhật tức thì:** Nhận ngay báo cáo tổng kết tiến độ qua tin nhắn Telegram mỗi sáng.
- **Quy trình chuẩn hóa:** Đảm bảo các task `ai-ready` được giải quyết tự động theo đúng cấu hình repo.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động mượt mà, các sếp cần chuẩn bị sẵn:
- **n8n instance** (Self-hosted hoặc Cloud).
- **GitHub Account & Personal Access Token** (quyền đọc issue, tạo comment, đẩy code và mở PR).
- **CloudCLI Account & API Key** (nền tảng AI agent để thực thi code).
- **Telegram Bot Token & Chat ID** (để nhận tin nhắn tổng kết).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow từ nguồn cấp hoặc copy toàn bộ mã nguồn JSON dán trực tiếp vào n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 7 nodes chính. Các sếp cần tập trung cấu hình kỹ các điểm sau:

- **Mỗi đêm lúc 2 giờ (`Every Night 2AM` - `scheduleTrigger`):** Node kích hoạt lịch chạy tự động hàng ngày. Có thể thay đổi thời gian nếu muốn.
- **Cấu hình thông tin (`Set Configuration` - `set`):** **(QUAN TRỌNG NHẤT)** Node này chứa các biến cốt lõi. Các sếp cần điền chính xác:
  - `repoOwner`: Tên tài khoản hoặc tổ chức sở hữu GitHub repository.
  - `repoName`: Tên repository cần tự động hóa.
  - `label`: Nhãn (label) để lọc issue (mặc định là `ai-ready`).
  - `baseBranch`: Nhánh gốc để tạo PR (ví dụ: `main` hoặc `dev`).
  - `cloudcliEnvUrl`: Đường dẫn môi trường CloudCLI.
  - `telegramChatId`: ID chat Telegram để nhận thông báo.
- **Tìm kiếm Issue (`Find AI-Ready Issues` - `github`):** Kết nối với **GitHub API credentials** để quét các open issues mang nhãn đã cấu hình.
- **Vòng lặp xử lý (`Loop Over Issues` - `splitInBatches`):** Lần lượt duyệt qua từng issue tìm được để tránh quá tải API.
- **AI thực thi (`CloudCLI Implement Issue` - `@cloudcli-ai/n8n-nodes-cloud-cli.cloudCli`):** Sử dụng **CloudCLI API credentials** kết hợp GitHub token bí mật để AI agent tự viết code, tạo nhánh và mở PR.
- **Bình luận tiến độ (`Comment On Issue` - `github`):** Tự động để lại bình luận trên GitHub Issue gốc, liên kết trực tiếp tới môi trường CloudCLI hoặc PR vừa tạo.
- **Gửi tổng kết (`Telegram Summary` - `telegram`):** Kết nối với **Telegram API credentials** để gửi thông báo kết quả sau khi hoàn tất toàn bộ danh sách issue trong đêm.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** để chạy thử với dữ liệu mẫu (hoặc tạo thử một issue gắn nhãn `ai-ready` để test).
- Kiểm tra kết quả trên GitHub và Telegram.
- Bật công tắc **Active** để hệ thống tự động chạy ngầm mỗi đêm.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Slack/Discord:** Thay thế hoặc bổ sung thông báo qua Telegram bằng Webhook gửi trực tiếp vào kênh chat của team lập trình.
- **Lưu lịch sử vào Google Sheets:** Thêm node Google Sheets để ghi log chi tiết các issue đã được AI xử lý thành công hay thất bại.
- **Cơ chế Error Handling:** Thêm Error Trigger workflow để nhận cảnh báo ngay lập tức qua Telegram nếu CloudCLI gặp lỗi trong quá trình thực thi code.

### 📌 Kết luận
Workflow tự động hóa GitHub Issues với CloudCLI và Telegram là trợ thủ đắc lực giúp tối ưu hóa năng suất cho các đội ngũ phát triển phần mềm. Hãy thiết lập ngay hôm nay để biến những ý tưởng thành code hoàn chỉnh ngay trong giấc ngủ của các sếp!