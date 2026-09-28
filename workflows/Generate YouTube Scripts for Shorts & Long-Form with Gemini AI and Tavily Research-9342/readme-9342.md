---
title: "🚀 Tự động hóa sản xuất kịch bản YouTube Shorts & Long-Form với Gemini AI và Tavily Research"
description: "Hướng dẫn sử dụng n8n workflow để tự động nghiên cứu từ khóa với Tavily và tạo kịch bản video YouTube dạng ngắn (Shorts) lẫn dạng dài chuyên sâu bằng Gemini AI, sau đó lưu trực tiếp vào Google Docs."
slug: "tu-dong-hoa-kich-ban-youtube-gemini-tavily"
tags: [n8n, automation, no-code, youtube, ai-agent, gemini, google-docs]
keywords: [n8n workflow, tạo kịch bản youtube tự động, gemini ai, tavily research, youtube shorts automation, content creation n8n]
---

# 🚀 Tự động hóa sản xuất kịch bản YouTube Shorts & Long-Form với Gemini AI và Tavily Research

Các sếp có đang cảm thấy kiệt sức mỗi khi phải lên ý tưởng, nghiên cứu thông tin, rồi ngồi viết từng kịch bản cho YouTube Shorts và video dài? Việc làm thủ công này ngốn rất nhiều thời gian, từ khâu tra cứu Google cho đến lúc hoàn thành văn bản.

Giải pháp đây rồi! Workflow n8n này sẽ giúp các sếp giải phóng 100% sức lao động. Chỉ với một chủ đề nhập vào qua form, hệ thống sẽ tự động hóa toàn bộ quá trình: nghiên cứu thông tin thời gian thực qua **Tavily**, sử dụng sức mạnh của **Gemini AI** để viết ra hai phiên bản kịch bản (YouTube Shorts ngắn gọn, giật gân và Video dài có cấu trúc chuyên sâu), rồi tự động lưu gọn gàng vào **Google Docs**. 

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Nhân đôi nội dung từ 1 ý tưởng:** Tự động tạo song song kịch bản YouTube Short và Video dài từ một chủ đề duy nhất.
- **Nghiên cứu thông minh:** Tích hợp Tavily Search để cập nhật thông tin mới nhất, giúp kịch bản bám sát xu hướng thực tế.
- **Tối ưu hóa thời gian:** Giảm từ vài tiếng đồng hồ viết kịch bản xuống chỉ vài giây chờ đợi hệ thống chạy.
- **Lưu trữ tự động:** Kịch bản hoàn thiện được tạo và cập nhật thẳng vào Google Docs, sẵn sàng để quay hình bất cứ lúc nào.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Google Gemini API Key:** Dành cho các node AI Agent và Chat Model.
- **Tavily API Key:** Dành cho các node HTTP Request thực hiện tìm kiếm web.
- **Google Docs OAuth2 Credentials:** Để n8n có quyền tạo và chỉnh sửa tài liệu trên Google Drive của các sếp.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow từ n8n.io (Link gốc: [Workflow #9342](https://n8n.io/workflows/9342)) hoặc tải file JSON về, sau đó dán trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình các thành phần sau:

- **Node `On form submission` (Trigger):** Cấu hình form nhập liệu đầu vào để thu thập chủ đề video (`video topic`) từ người dùng.
- **Cụm AI & LLM (`Google Gemini Chat Model`, `Google Gemini Chat Model1`):** Kết nối thông tin xác thực Google AI/Gemini API key của các sếp.
- **Cụm tìm kiếm web (`Tavily`, `Tavily1`):** Điền Tavily API Key vào phần Header Auth để kích hoạt tính năng tra cứu thông tin web.
- **Cụm tạo tài liệu (`Create Doc`, `Update Doc`, `Create Doc1`, `Update Doc1`):** Kết nối tài khoản Google cá nhân thông qua OAuth2 để n8n có quyền tạo Google Docs mới chứa kịch bản.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và test thử bằng một chủ đề bất kỳ trên form để kiểm tra dữ liệu chảy qua 2 nhánh (Shorts và Long-Form).
- Sau khi test thành công, bật công tắc **Active** để đưa workflow vào trạng thái hoạt động tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Thông báo qua Telegram/Slack:** Thêm một node Telegram hoặc Slack vào cuối mỗi nhánh để hệ thống gửi tin nhắn thông báo link Google Docs ngay khi kịch bản viết xong.
- **Lưu lịch lượng nội dung:** Kết nối thêm một node **Google Sheets** để lưu lại lịch sử các chủ đề và link kịch bản đã tạo nhằm dễ dàng quản lý chiến dịch content.
- **Cá nhân hóa văn phong Prompt:** Tinh chỉnh prompt bên trong các **AI Agent** để ép AI viết theo đúng giọng điệu (tone of voice) thương hiệu của kênh YouTube các sếp.

### 📌 Kết luận
Workflow này là một "vũ khí tối thượng" cho các nhà sáng tạo nội dung muốn tối ưu hóa quy trình sản xuất video. Hãy cài đặt ngay hôm nay để biến mọi ý tưởng trong đầu thành những kịch bản YouTube chuyên nghiệp chỉ trong tích tắc!