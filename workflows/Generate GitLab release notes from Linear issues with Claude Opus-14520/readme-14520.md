---
title: "🚀 Tự động tạo Release Notes trên GitLab từ Linear Issues với Claude AI"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa quy trình viết Release Notes, tổng hợp Linear Issues và tích hợp Claude Opus AI để cập nhật trực tiếp lên GitLab Merge Request."
slug: "tu-dong-hoa-gitlab-release-notes-linear-claude-ai"
tags: [n8n, automation, gitlab, linear, ai, claude, devops]
keywords: [n8n workflow, gitlab release notes, linear issues integration, claude ai automation, devops automation]
---

# 🚀 Tự động hóa tạo Release Notes trên GitLab từ Linear Issues với Claude AI

Các sếp làm kỹ sư phần mềm, Product Manager hay DevOps chắc chắn đều ngán ngẩm cảnh mỗi khi release phiên bản mới lại phải lọ mọ gom từng task từ Linear, tổng hợp thay đổi rồi ngồi viết Release Notes thủ công dán vào GitLab Merge Request (MR). Vừa mất thời gian, vừa dễ sót ý, lại chẳng chuyên nghiệp chút nào.

Đừng lo, workflow n8n được thiết kế bởi chuyên gia Romain Jouhannet này sẽ giải quyết triệt để "nỗi đau" đó. Workflow này sẽ tự động hóa từ A-Z: bắt sự kiện từ GitLab, truy vấn Linear issues, sử dụng sức mạnh của Claude Opus AI để phân tích và tạo nội dung tổng hợp, sau đó tự động "push" trực tiếp kết quả vào GitLab MR. Tiết kiệm 100% thời gian thủ công, không cần viết một dòng code nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Desky VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn:** Kích hoạt ngay khi có sự kiện Merge Request trên GitLab mà không cần can thiệp thủ công.
- **Tích hợp thông minh:** Tự động đồng bộ thông tin từ Linear Issues và RSS feed để nắm bắt chính xác các task liên quan đến phiên bản.
- **AI-Powered Release Notes:** Ứng dụng mô hình Claude AI thông minh để tạo tóm tắt cấp cao (high-level summary) và các gợi ý chi tiết, sắc bén.
- **Cập nhật liền mạch:** Tự động đăng nội dung tóm tắt, cập nhật nhãn (labels) và ghi chú trực tiếp vào GitLab MR.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **GitLab Account & Personal Access Token:** Để lắng nghe Webhook sự kiện MR và gọi GitLab API.
- **Linear API Key / Workspace:** Để truy vấn danh sách issues và labels.
- **Anthropic API Key:** Để kết nối với Claude AI (Claude Opus).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow này và paste trực tiếp vào n8n Editor của mình, hoặc import file JSON tải từ nguồn gốc.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 18 nodes được bố trí mạch lạc, các sếp cần chú ý cấu hình kỹ các node sau:

- **When GitLab MR Event Occurs (`gitlabTrigger`):** Kết nối với tài khoản GitLab của các sếp, chọn Repository và cấu hình sự kiện kích hoạt khi Merge Request được mở hoặc cập nhật.
- **Fetch GitLab MR Labels & Update GitLab MR Label (`httpRequest`):** Thiết lập thông tin xác thực (GitLab API Credentials) để node có thể đọc và ghi nhãn cho MR.
- **Post Linear Issues to GraphQL & Post Linear Labels to GraphQL (`httpRequest`):** Cấu hình API endpoint và token của Linear để node tiến hành truy vấn GraphQL lấy danh sách issues và nhãn phiên bản tương ứng.
- **Read RSS Feed (`rssFeedRead`):** Trỏ đường dẫn tới RSS Feed của Linear để hệ thống quét các nhãn phát hành (release labels) ban đầu.
- **Claude AI Message (`anthropic`):** Chọn credentials của Anthropic, chọn model (khuyên dùng Claude Opus hoặc Sonnet mới nhất) và tinh chỉnh Prompt hệ thống để AI hiểu cách tổng hợp Release Notes chuẩn kỹ thuật.
- **Các node Code (`Generate Summary with Links`, `Filter Labels Starting With v2`, `Parse Linear Version Labels`, v.v.):** Xử lý dữ liệu JavaScript thuần túy, các sếp giữ nguyên logic bên trong trừ khi muốn thay đổi định dạng hiển thị.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (**Test run**) với một Merge Request mẫu trên GitLab để kiểm tra luồng dữ liệu qua các node điều kiện (`Check Release Label`, `Check MR for RN Inputs`, `Check Linear Issues Exist`).
- Sau khi mọi thứ chạy mượt mà, gạt công tắc sang **Active** để workflow chính thức làm việc tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Thông báo qua Slack/Telegram:** Thêm node gửi tin nhắn vào kênh DevOps/Engineering của công ty ngay sau khi Release Notes được đăng lên GitLab để team kịp thời nắm bắt.
- **Lưu trữ Log:** Kết nối thêm Google Sheets hoặc Notion để lưu lịch sử các phiên bản đã phát hành làm báo cáo định kỳ.
- **Tùy biến Prompt AI:** Tinh chỉnh system prompt trong node Claude AI để ép định dạng Release Notes theo đúng văn phong nội bộ của công ty (bullet points, emoji, phân loại Bug/Feature/Improvement rõ ràng).

### 📌 Kết luận
Tự động hóa quy trình viết Release Notes không chỉ giúp tiết kiệm hàng giờ đồng hồ mỗi tuần cho đội ngũ phát triển mà còn nâng tầm chuyên nghiệp cho sản phẩm. Hãy thiết lập ngay workflow này để đội ngũ engineering có thêm thời gian tập trung vào việc code những tính năng tuyệt vời thay vì làm báo cáo thủ công!