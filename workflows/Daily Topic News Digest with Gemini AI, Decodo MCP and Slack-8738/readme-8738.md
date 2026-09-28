---
title: "🚀 Tự động hóa bản tin tổng hợp hàng ngày với Gemini AI, Decodo MCP và Slack"
description: "Xây dựng AI Agent tự động tìm kiếm, cào dữ liệu web, tổng hợp tin tức nóng hổi trong 48h qua theo chủ đề và gửi trực tiếp lên Slack mỗi ngày bằng n8n."
slug: "tu-dong-hoa-ban-tin-tong-hop-hang-ngay-gemini-ai-decodo-mcp-slack"
tags: [n8n, automation, no-code, gemini-ai, slack, ai-agent, web-scraping]
keywords: [n8n workflow, tự động hóa bản tin, gemini ai, decodo mcp, slack automation, ai news agent]
licenses: "MIT"
---

# 🚀 Tự động hóa bản tin tổng hợp hàng ngày với Gemini AI, Decodo MCP và Slack

Các sếp có tốn hàng giờ mỗi ngày chỉ để lướt web, đọc báo, tổng hợp thông tin về ngành, đối thủ hay công nghệ mới không? Việc này vừa mất thời gian, vừa dễ bỏ lỡ các tin tức quan trọng. 

Đừng lo! Bài viết này sẽ hướng dẫn các sếp triển khai một **AI News Agent tự động hoàn toàn** bằng n8n. Workflow này sẽ tự động tìm kiếm, cào dữ liệu web, lọc tin tức trong 48 giờ qua, tổng hợp bằng **Gemini AI** và bắn thẳng bản tin đẹp mắt lên **Slack** đúng 9h sáng mỗi ngày. Không cần code tay, tự động 100%!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 mà không lo gián đoạn, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 100% thời gian:** Không còn phải thủ công tìm kiếm, đọc và tổng hợp tin tức ngành mỗi sáng.
- **Cập nhật liên tục:** AI tự động quét các bài viết mới nhất trong 48 giờ qua dựa trên danh sách chủ đề tùy chỉnh.
- **Thông minh & Chính xác:** Sử dụng Gemini AI kết hợp Decodo MCP để cào dữ liệuượt qua các cơ chế chống bot và vượt rào cản địa lý.
- **Cộng đồng gắn kết:** Bản tin tóm tắt gọn gàng, kèm link gốc click được gửi thẳng vào kênh Slack của đội ngũ.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản và API keys sau:
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Decodo MCP Credentials:** Tài khoản và API/Credentials từ [Decodo MCP](https://dashboard.decodo.com/) (có bản dùng thử miễn phí).
- **Gemini API Key:** Lấy key miễn phí tại [Google AI Studio](https://aistudio.google.com/app/apikey).
- **Slack Workspace:** Quyền cấu hình và gửi tin nhắn qua Bot trong kênh Slack của công ty.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần tải file JSON của workflow này từ kho lưu trữ n8n (Link gốc: [Workflow #8738](https://n8n.io/workflows/8738)), sau đó copy và paste trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import thành công, các sếp cần cấu hình chính xác các node trọng điểm sau:
- **Schedule Trigger:** Mặc định chạy lúc 9:00 AM mỗi ngày. Các sếp có thể đổi khung giờ khác nếu muốn.
- **Set Topics (Node `Set Topics`):** Tùy chỉnh danh sách các chủ đề quan trọng với doanh nghiệp của sếp (Ví dụ: AI, MCP, Web Scraping, FinTech, v.v.).
- **Gemini Chat Model:** Kết nối với credentials `googlePalmApi` sử dụng Gemini API Key đã chuẩn bị.
- **Decodo MCP:** Cấu hình tool cào dữ liệu web thông minh (`Decodo MCP`) giúp AI agent tìm kiếm Google và đọc nội dung trang web mượt mà.
- **Slack (Node `Slack`):** Chọn đúng credentials `slackApi` và chỉ định Channel nhận bản tin tóm tắt.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** để test thử nghiệm xem AI Agent có cào và bắn tin lên Slack thành công hay không.
- Nếu mọi thứ mượt mà, gạt công tắc sang **Active** để hệ thống tự động chạy ngầm mỗi ngày.

### ✍️ Mẹo & gợi ý nâng cao
Để tối ưu hóa workflow này cho doanh nghiệp, các sếp có thể mở rộng thêm:
1. **Đa kênh thông báo:** Ngoài Slack, có thể duplicate nhánh gửi sang **Telegram Bot** hoặc **Email** để sếp đọc trên điện thoại tiện hơn.
2. **Lưu trữ dữ liệu:** Thêm node **Google Sheets** hoặc **Airtable** để lưu lại lịch sử tất cả các bản tin đã quét, phục vụ tra cứu về sau.
3. **Phân tích cảm tính (Sentiment Analysis):** Yêu cầu Gemini AI đánh giá thêm sắc thái của tin tức (Tích cực / Tiêu cực / Trung lập) đối với thị trường.

### 📌 Kết luận
Tự động hóa bản tin tổng hợp hàng ngày với AI Agent và Decodo MCP là một "vũ khí bí mật" giúp đội ngũ của các sếp luôn đi đầu xu hướng mà không tốn một giọt mồ hôi nghiên cứu thủ công. Hãy import ngay workflow này và tối ưu hóa thời gian cho team của mình ngày hôm nay!