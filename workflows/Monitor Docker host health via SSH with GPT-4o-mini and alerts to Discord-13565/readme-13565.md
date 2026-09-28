---
title: "🚀 Tự động giám sát sức khỏe Docker & Homelab qua SSH với GPT-4o-mini và cảnh báo Discord"
description: "Xây dựng hệ thống giám sát Homelab toàn diện tự động 100%: Thu thập 30+ chỉ số hệ thống và Docker qua SSH, phân tích thông minh bằng OpenAI GPT-4o-mini, lưu trữ lịch sử Google Sheets và đẩy cảnh báo trực quan vào Discord."
slug: "giam-sat-suc-khoe-docker-homelab-ssh-gpt4-discord"
tags: [n8n, automation, devops, docker, ai, discord, google-sheets]
keywords: [n8n workflow, giám sát docker, homelab health check, ssh monitoring, gpt-4o-mini n8n, discord alert automation]
---

# 🚀 Tự động giám sát sức khỏe Docker & Homelab qua SSH với GPT-4o-mini và cảnh báo Discord

Các sếp đang vận hành hệ thống Homelab, VPS hay cụm Docker chắc chắn đã từng trải qua cảm giác "đứng tim" khi server bỗng dưng chết giữa đêm, ổ cứng đầy 100% hay container sập ngầm mà không hề hay biết. Việc kiểm tra thủ công bằng tay (`htop`, `docker ps`, `df -h`) vừa tốn thời gian vừa mang tính bị động.

Workflow n8n này sẽ giải quyết triệt để nỗi đau đó bằng cách tự động hóa toàn bộ quy trình: SSH vào máy chủ Docker, thu thập hơn 30 chỉ số phần cứng & container, sử dụng **AI (GPT-4o-mini)** để phân tích xu hướng lịch sử, chấm điểm sức khỏe, đưa ra lệnh fix lỗi cụ thể và gửi báo cáo đẹp mắt vào **Discord** (bao gồm cả chế độ cảnh báo khẩn cấp mỗi 5 phút).

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Giám sát chủ động 24/7:** Tự động kiểm tra sức khỏe hàng ngày (hoặc theo lịch tùy chỉnh) và quét lỗi khẩn cấp mỗi 5 phút.
- **Phân tích chuyên sâu bằng AI:** GPT-4o-mini không chỉ báo cáo số liệu mà còn chấm điểm 100-point health score, phân loại mức độ nghiêm trọng và cung cấp sẵn câu lệnh CLI để fix lỗi.
- **Dashboard trực quan trên Discord:** Báo cáo tổng hợp chia thành 4 embed mượt mà: trạng thái hệ thống, cảnh báo thông minh kèm lệnh fix, sinh thái Docker và thông tin chi phí/thời gian thực thi.
- **Lưu trữ dữ liệu lịch sử:** Tự động lưu 16 cột chỉ số vào Google Sheets giúp dễ dàng theo dõi xu hướng (trend analysis) qua 7 ngày gần nhất.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Self-hosted hoặc Cloud).
- **SSH Access:** Quyền SSH vào Docker host (cần chuẩn bị SSH Private Key).
- **OpenAI API Key:** Tài khoản OpenAI để sử dụng mô hình `gpt-4o-mini`.
- **Google Account:** Tài khoản Google Sheets để tạo bảng điều khiển và lưu lịch sử.
- **Discord Webhook:** Webhook URL từ kênh Discord để nhận tin nhắn cảnh báo.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow từ nguồn cung cấp hoặc copy trực tiếp JSON dán vào giao diện n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình kỹ các node trọng điểm sau:
- **`▶️ Run first-time setup` (manualTrigger):** Chạy thử lần đầu tiên để workflow tự động tạo một Google Sheet chuẩn hóa tên *"Homelab Health Dashboard"* với đầy đủ định dạng màu sắc, tiêu đề.
- **`⚙️ Configure monitoring settings` (set):** Dán Sheet ID (lấy từ URL của bảng Google Sheet vừa tạo ở bước trên) vào cấu hình này, đồng thời điền Webhook URL của Discord.
- **Các node SSH (`Collect system metrics`, `Collect Docker container metrics`, `Quick system health check`):** Kết nối với **Credentials** kiểu `sshPrivateKey` để n8n có quyền đăng nhập vào máy chủ của các sếp.
- **Node `OpenAI GPT-4o-mini` (lmChatOpenAi):** Thêm Credentials API Key của OpenAI và đảm bảo model được chọn là `gpt-4o-mini`.
- **Node `Store today's metrics in history` & `Read metrics history (last 7 days)`:** Kết nối tài khoản Google Sheets OAuth2 để n8n đọc/ghi dữ liệu.
- **`⚙️ Alert settings` (set):** Tùy chỉnh các ngưỡng cảnh báo khẩn cấp (ví dụ: ổ cứng > 90%, RAM > 95%, CPU quá tải, container sập...).

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm thủ công (Test run) đường dẫn báo cáo hàng ngày để kiểm tra kết quả đổ về Discord và Google Sheets.
- Sau khi mọi thứ mượt mà, gạt công tắc sang **Active** để workflow tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo:** Ngoài Discord, các sếp có thể nhân bản nhánh HTTP Request sang Telegram Bot, Slack, hoặc ntfy để nhận cảnh báo đa kênh.
- **Tùy chỉnh mô hình AI:** Có thể thay thế OpenAI bằng Claude (Anthropic) hoặc mô hình nội bộ qua Ollama bằng cách thay đổi node LLM sub-node tương ứng.
- **Tối ưu lịch trình:** Thay đổi lịch chạy tại node `Run daily health check` từ 7:00 AM sang khung giờ khác tùy theo nhu cầu vận hành của đội ngũ.

### 📌 Kết luận
Với workflow n8n này, việc quản trị Homelab hay hệ thống Docker của các sếp sẽ trở nên chuyên nghiệp, tự động hóa hoàn toàn và không bao giờ bỏ sót bất kỳ sự cố tiềm ẩn nào nữa. Hãy "lên đồ" ngay hôm nay để tối ưu hóa vận hành hạ tầng!