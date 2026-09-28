---
title: "🚀 Tự động tạo Vlog Bigfoot triệu view với Veo 3 và n8n AI"
description: "Xây dựng hệ thống tự động hóa hoàn toàn quy trình tạo video vlog Bigfoot triệu view bằng AI, kết hợp Claude 4 Sonnet, Veo 3 và Google Drive."
slug: "tao-vlog-bigfoot-trieu-view-voi-veo-3-va-n8n"
tags: [n8n, automation, no-code, ai-video, claude-ai, google-drive]
keywords: [n8n workflow, tạo video AI, Veo 3, Claude 4 Sonnet, tự động hóa video, automation n8n]
---

# 🚀 Tự động tạo Vlog Bigfoot triệu view với Veo 3 và n8n AI

Việc sáng tạo nội dung video ngắn, vlog theo các chủ đề hot (như Bigfoot hay các câu chuyện kỳ bí) đòi hỏi rất nhiều thời gian lên kịch bản, chia phân cảnh, tạo prompt và render video thủ công. Nếu các sếp đang muốn tối ưu hóa quy trình sản xuất nội dung video quy mô lớn mà không cần tốn hàng giờ ngồi cắt ghép, đây chính là giải pháp tự động hóa 100% không cần code (No-Code) dành cho các sếp. Workflow này được thiết kế bởi chuyên gia Lucas Walter (The Recap AI), giúp tự động hóa toàn bộ từ việc viết kịch bản bằng AI, xin phê duyệt qua Slack, cho đến gọi API tạo video bằng Veo 3 và lưu trữ tự động lên Google Drive.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa từ A-Z:** Từ ý tưởng ban đầu qua Form đến kịch bản chi tiết, phân cảnh và render video hoàn chỉnh.
- **Kiểm soát chất lượng (Human-in-the-loop):** Tích hợp Slack để xét duyệt kịch bản và phân cảnh trước khi tiến hành render video tốn kém tài nguyên.
- **Xử lý hàng đợi thông minh:** Tự động chia batch, gọi API tạo video, kiểm tra trạng thái và tải kết quả về liền mạch.
- **Lưu trữ chuyên nghiệp:** Tự động tổng hợp và đẩy toàn bộ video hoàn thành lên Google Drive một cách ngăn nắp.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động mượt mà, các sếp cần chuẩn bị sẵn:
- **n8n Instance** (Self-hosted hoặc Cloud).
- **Anthropic API Key** (cho node `claude-4-sonnet` sử dụng mô hình Claude 4 Sonnet).
- **Slack Workspace & Bot Token** (cho các node `slack` gửi thông báo và chờ phê duyệt).
- **Veo 3 API / HTTP Header Auth** (tài khoản và API truy cập hệ thống tạo video Veo 3).
- **Google Drive Account** (cấp quyền OAuth2 cho node `upload_video`).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần tải file JSON của workflow từ nguồn gốc, mở n8n editor, chọn **Import from File** hoặc copy toàn bộ mã JSON và dán trực tiếp vào không gian làm việc của n8n.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow gồm 23 nodes được chia thành 3 giai đoạn chính (Write Video Script, Get Human Approval, Generate Video). Các sếp cần chú ý cấu hình các node sau:
- **`form_trigger`**: Nơi người dùng nhập yêu cầu/chủ đề khởi tạo video ban đầu.
- **`claude-4-sonnet`** và **`scene_director` / `narrative_writer`**: Kết nối với credentials của Anthropic. Đảm bảo model được chọn là `claude-sonnet-4-20250514`.
- **`send_and_wait` & `send_narrative_msg` (Slack)**: Chọn đúng `slackOAuth2Api` credentials và cấu hình Channel ID để nhận thông báo chờ duyệt kịch bản từ hệ thống.
- **`queue_create_video`, `fetch_status`, `fetch_result` (HTTP Request)**: Cấu hình Header Auth chính xác để kết nối với API tạo video của Veo 3.
- **`upload_video` (Google Drive)**: Kết nối tài khoản Google Drive qua OAuth2 và chọn thư mục (Folder ID) lưu trữ video đầu ra.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và điền thử một form mẫu để test luồng chạy từ đầu đến cuối.
- Kiểm tra thông báo trên Slack, duyệt kịch bản và theo dõi quá trình tạo video.
- Khi mọi thứ chạy trơn tru, hãy chuyển trạng thái workflow sang **Active**.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo:** Có thể bổ sung node Telegram hoặc Discord bên cạnh Slack để đội ngũ sản xuất dễ dàng theo dõi tiến độ mọi lúc mọi nơi.
- **Tự động đăng tải:** Kết hợp thêm node YouTube, TikTok hoặc Instagram Graph API để sau khi video đẩy lên Google Drive, hệ thống sẽ tự động lên lịch đăng bài luôn.
- **Lưu log chi tiết:** Đưa dữ liệu trạng thái vào Google Sheets hoặc Airtable để thống kê số lượng video đã sản xuất mỗi ngày/tuần.

### 📌 Kết luận
Workflow tự động hóa tạo vlog Bigfoot với Veo 3 và Claude 4 Sonnet là một cỗ máy kiếm traffic cực mạnh cho các nhà sáng tạo nội dung. Hãy thiết lập ngay hôm nay để tiết kiệm 90% thời gian sản xuất video và tối ưu hóa hiệu suất làm việc của đội ngũ!