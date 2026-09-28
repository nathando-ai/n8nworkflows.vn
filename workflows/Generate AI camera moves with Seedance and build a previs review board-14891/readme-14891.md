---
title: "🚀 Tự động hóa sản xuất Previs điện ảnh với AI Camera Moves, Seedance và n8n"
description: "Xây dựng bảng đánh giá tiền kỳ (Previs Review Board) tự động 100% bằng AI Agent, Azure OpenAI, Seedance API và n8n giúp đạo diễn và giám sát hình ảnh tối ưu quy trình quay phim."
slug: "tu-dong-hoa-previs-dien-anh-ai-seedance-n8n"
tags: [n8n, automation, ai-agent, azure-openai, content-creation, multimedia]
keywords: [n8n workflow, tự động hóa previs, seedance ai, azure openai gpt-4o, virtual cinematography, quản lý sản xuất phim]
---

# 🚀 Tự động hóa sản xuất Previs điện ảnh với AI Camera Moves, Seedance và n8n

Trong ngành sản xuất phim và video chuyên nghiệp, việc lên ý tưởng góc máy (previs) cho các phân cảnh phức tạp thường ngốn rất nhiều thời gian phác thảo, dựng hình 3D thủ công và phối hợp qua lại giữa nhiều bộ phận. 

Workflow này ra đời nhằm giải quyết triệt để nỗi đau đó: Tự động hóa hoàn toàn quy trình nhận yêu cầu kịch bản, sử dụng AI phân tích góc máy, gọi API Seedance để dựng video ngắn minh họa, và đồng thời phát hành bộ sưu tập góc máy (A/B/C options) lên Slack, Jira, ClickUp, Telegram và Google Drive. Các sếp chỉ việc ngồi thưởng thức và chốt phương án!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tăng tốc 300%:** Chuyển đổi nhanh chóng từ kịch bản thô (script snippet) sang 3 phương án chuyển động camera (camera choreography) trực quan.
- **Đồng bộ đa nền tảng:** Tự động tạo task trên Jira, bản ghi trên ClickUp, thông báo trên Slack và gửi trực tiếp qua Telegram cho giám sát.
- **Lưu trữ thông minh:** Tự động archive video render vào Google Drive làm tài liệu tham khảo ánh sáng cho team hậu kỳ (comp team).
- **Giám sát lỗi 24/7:** Hệ thống Error Handler tự động bắt lỗi và cảnh báo ngay lập tức qua Slack/Telegram khi có sự cố.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản và API keys sau:
- **n8n Instance** (Self-hosted hoặc Cloud).
- **Azure OpenAI Account** (với model `gpt-4o-mini` được triển khai).
- **Seedance API Key** (Dùng cho việc render video camera move).
- **Slack App / Bot Credentials** (OAuth2).
- **Jira Cloud Credentials & Project ID**.
- **ClickUp API Token & Workspace IDs**.
- **Google Drive OAuth2 Credentials**.
- **Telegram Bot Token & Chat ID**.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow từ n8n template (ID: 14891) hoặc copy toàn bộ mã nguồn JSON, sau đó paste trực tiếp vào n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow gồm 22 nodes được thiết kế mạch lạc từ nhận form đến trả kết quả. Các sếp cần chú ý cấu hình các node sau:
- **Form: Previs Brief Input1**: Lấy URL Webhook tự động sinh ra và chia sẻ cho đội ngũ sản xuất nhập yêu cầu kịch bản.
- **Azure OpenAI: GPT-4o Mini**: Kết nối credential Azure OpenAI và xác nhận tên deployment đúng là `gpt-4o-mini` (hoặc tên deployment tương ứng của các sếp).
- **Seedance: Submit Camera Move Job**: Thay thế Bearer Token trong phần Header Auth bằng Seedance API key thực tế của các sếp.
- **Slack: Publish Previs Board1** & **Slack: Error Alert**: Kết nối Slack qua OAuth2 và cấu hình lại `channelId` nhận thông báo.
- **Jira: Create Previs Review Task**: Kết nối Jira Cloud credential, cập nhật `project` và `issueType` ID khớp với bảng quản lý của team.
- **ClickUp: Create Previs Production Record**: Cấu hình ClickUp credentials, cập nhật các thông số `team`, `space`, `folder`, và `list` IDs.
- **Google Drive: Archive Lighting Ref**: Kết nối qua OAuth2 và trỏ `folderId` đến thư mục lưu trữ previs trên Google Drive.
- **Telegram: Deliver Previs to Supervisor**: Kết nối Telegram Bot và điền chính xác `chatId` của giám sát viên.

#### 3. Kích hoạt ⚡️
- Thực hiện chạy thử (`Test run`) bằng một miêu tả cảnh quay đơn giản qua form để kiểm tra toàn bộ luồng xử lý từ AI Agent đến Seedance rendering.
- Sau khi test thành công, bật công tắc **Active** để đưa workflow vào vận hành thực tế.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Confluence:** Có thể mở rộng workflow để tự động tạo trang tài liệu tổng hợp trên Confluence kèm theo các keyframe video.
- **Human-in-the-loop qua Slack/Telegram:** Thêm các nút bấm tương tác (Interactive Buttons) vào thông báo Slack/Telegram để đạo diễn bấm duyệt trực tiếp phương án A, B hoặc C ngay trên chat app.
- **Mở rộng kho lưu trữ:** Kết hợp gửi bản tóm tắt qua email cho các bên liên quan ngoài giờ làm việc.

### 📌 Kết luận
Với workflow tự động hóa này, khâu chuẩn bị tiền kỳ (Previs) cho các dự án video/phim ảnh không còn là gánh nặng tốn kém thời gian. Hãy triển khai ngay lên hệ thống n8n của các sếp để tối ưu hóa năng suất cho toàn bộ ê-kip sản xuất!