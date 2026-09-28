---
title: "🎬 Tự động tạo video AI đa phân cảnh từ kịch bản với Claude, Stability AI và Runway"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa quy trình sản xuất video đa phân cảnh từ kịch bản văn bản bằng sức mạnh của Claude AI, Stability AI và Runway Gen-2."
slug: "tao-video-ai-da-phan-cảnh-tu-kich-ban-voi-claude-stability-runway"
tags: [n8n, automation, no-code, AI video, Claude AI, Stability AI, Runway]
keywords: [n8n workflow, tạo video AI, tự động hóa video, Claude AI, Stability AI, Runway, content creation]
---

# 🎬 Tự động tạo video AI đa phân cảnh từ kịch bản với Claude, Stability AI và Runway

Việc sản xuất video marketing, video ngắn cho TikTok/Reels hay video giải trí thủ công thường ngốn rất nhiều thời gian: từ khâu viết kịch bản, chia cảnh, tạo hình ảnh minh họa cho đến dựng hình động và ghép nối. Nỗi đau này khiến các nhà sáng tạo nội dung và doanh nghiệp thường bị giới hạn số lượng video sản xuất mỗi ngày.

Workflow n8n này chính là giải pháp tự động hóa 100% không cần code (No-code), giúp các sếp biến một đoạn kịch bản văn bản thô sơ thành một video đa phân cảnh hoàn chỉnh bằng cách kết hợp chuỗi các AI hàng đầu hiện nay: **Claude** (phân tích và chia kịch bản), **Stability AI** (tạo hình ảnh gốc cho từng cảnh) và **Runway** (biến ảnh thành video động).

:::info[Gợi ý hạ tầng cho n8n]
Để workflow xử lý các tác vụ AI nặng và chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa toàn diện:** Chuyển từ text sang video đa phân cảnh mà không cần can thiệp thủ công từng bước.
- **Tối ưu chi phí & thời gian:** Sản xuất hàng loạt video chất lượng cao chỉ trong vài phút thay vì mất hàng giờ dựng phim.
- **Chất lượng AI đỉnh cao:** Kết hợp logic thông minh của Claude, khả năng tạo ảnh sắc nét của Stability AI và chuyển động mượt mà từ Runway.
- **Quy trình module hóa:** Dễ dàng mở rộng, tuỳ chỉnh kịch bản hoặc thay thế các mô hình AI theo nhu cầu.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản và API Keys sau:
- **n8n Instance** (phiên bản Cloud hoặc Self-hosted).
- **Anthropic API Key** (để sử dụng Claude phân tích kịch bản).
- **Stability AI API Key** (để tạo hình ảnh từ prompt).
- **Runway API Key** (hoặc tài khoản tương ứng để tạo video từ ảnh).
- **Google Sheets / Webhook** (để nhận đầu vào kịch bản và lưu trữ dữ liệu nếu cần).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Các sếp tiến hành copy mã JSON của workflow từ nguồn cung cấp.
- Trong giao diện n8n Editor, chọn **Add workflow** -> Dán (Paste) mã JSON vào màn hình làm việc.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống vận hành trơn tru, các sếp cần cấu hình chính xác các node quan trọng sau:
- **Webhook Node / Google Sheets Node:** Cấu hình nguồn nhận dữ liệu kịch bản đầu vào (có thể là một Form đăng ký, một dòng mới trong Google Sheets hoặc nhận trực tiếp qua Webhook API).
- **HTTP Request (Claude AI) Node:** Nhập `Anthropic API Key` vào phần Credentials và cấu hình prompt để Claude tiếp nhận kịch bản thô, sau đó tách thành mảng các phân cảnh (scenes) kèm prompt tạo ảnh chi tiết cho từng cảnh.
- **Split In Batches Node:** Quản lý vòng lặp để xử lý từng phân cảnh một cách tuần tự, tránh vượt quá giới hạn API (Rate limit) của các bên Stability AI và Runway.
- **HTTP Request (Stability AI) Node:** Đưa prompt tiếng Anh của từng cảnh vào Stability AI để sinh ra bức ảnh nền tảng cho phân cảnh đó.
- **HTTP Request (Runway) Node:** Gửi hình ảnh vừa tạo từ Stability AI sang Runway kèm theo tham số chuyển động để xuất ra file video ngắn cho từng phân cảnh.
- **Wait Node / Code Node:** Thiết lập thời gian chờ (Polling) để kiểm tra trạng thái render video từ Runway cho đến khi hoàn tất.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (**Test workflow**) với một kịch bản ngắn khoảng 2-3 phân cảnh để kiểm tra luồng dữ liệu qua từng node.
- Sau khi kiểm tra mọi thứ hoạt động ổn định, gạt công tắc sang **Active** để đưa workflow vào vận hành chính thức.

---

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Thêm node Telegram hoặc Slack ở cuối workflow để gửi thông báo kèm link video hoàn thiện ngay khi render xong cho đội ngũ kiểm duyệt.
- **Lưu trữ tự động:** Đẩy toàn bộ video của các phân cảnh vào Google Drive hoặc một thư mục trên cloud để tiện cho việc ghép nối (Editing) sau này.
- **Kết hợp công cụ ghép video:** Có thể sử dụng thêm các API dựng phim tự động để gộp các video phân cảnh lại, chèn nhạc nền và lồng tiếng (Text-to-Speech) tạo thành video hoàn chỉnh 100%.

### 📌 Kết luận
Workflow tự động hóa sản xuất video đa phân cảnh từ Claude, Stability AI và Runway chính là "vũ khí bí mật" giúp các nhà sáng tạo nội dung bứt phá năng suất. Hãy cài đặt ngay hôm nay để tối ưu hóa quy trình làm việc và đưa kênh truyền thông của các sếp lên một tầm cao mới!