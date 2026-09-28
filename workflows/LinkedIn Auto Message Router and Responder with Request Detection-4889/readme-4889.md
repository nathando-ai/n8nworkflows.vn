---
title: "🚀 Tự động hóa tin nhắn LinkedIn thông minh bằng AI Agent, Unipile, Notion và Slack"
description: "Xây dựng hệ thống định tuyến, làm giàu dữ liệu người dùng và phản hồi tin nhắn LinkedIn tự động bằng AI, tích hợp Slack để duyệt nội dung trước khi gửi."
slug: "tu-dong-hoa-tin-nhan-linkedin-voi-ai-va-slack"
tags: [n8n, automation, no-code, linkedin, ai-agent, slack, notion]
keywords: [n8n workflow, tự động hóa linkedin, unipile api, ai agent n8n, slack bot automation, notion database]
keywords: [n8n workflow, tự động hóa, tự động hóa tin nhắn linkedin, quản lý tin nhắn ai, unipile slack integration]
---

# 🚀 Tự động hóa tin nhắn LinkedIn thông minh bằng AI Agent, Unipile, Notion và Slack

Chào các sếp! Việc quản lý hàng đống tin nhắn trên LinkedIn mỗi ngày, phân loại khách hàng tiềm năng, và viết câu trả lời phù hợp thực sự là một "cực hình" ngốn rất nhiều thời gian. Chưa kể nếu bỏ lỡ các đối tác quan trọng hoặc influencer thì doanh nghiệp sẽ mất đi cơ hội lớn.

Giải pháp cho các sếp đây: Một siêu workflow n8n được thiết kế bởi chuyên gia Angel Menendez từ n8n.io. Workflow này sẽ tự động hóa toàn bộ quy trình: nhận tin nhắn LinkedIn qua **Unipile**, làm giàu dữ liệu người dùng, sử dụng **AI Agent (GPT-4o)** kết hợp tri thức từ **Notion Database** để phân tích và soạn câu trả lời, đồng thời gửi thông báo kèm nút bấm phê duyệt đến **Slack** trước khi chính thức gửi tin nhắn đi.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Không cần tẻ nhạt check và trả lời từng tin nhắn LinkedIn thủ công.
- **Cá nhân hóa thông minh:** AI tự động quét số lượng người theo dõi, kết nối của người gửi để đưa ra quyết định phù hợp (VD: Influencer được cấp ngay link đặt lịch hẹn, người chưa đủ điều kiện sẽ được từ chối khéo léo).
- **Kiểm soát tuyệt đối qua Slack:** Mọi tin nhắn do AI soạn thảo đều được gửi về Slack để đội ngũ duyệt (Approve/Deny) trước khi gửi lên LinkedIn.
- **Cập nhật quy trình linh hoạt:** Tri thức định tuyến được lưu trữ trên Notion, giúp thay đổi kịch bản phản hồi của AI mà không cần sửa code hay sửa workflow.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Bản self-hosted hoặc cloud.
- **Unipile Account:** Lấy API key (`X-API-KEY`) để kết nối và nhận webhook tin nhắn LinkedIn.
- **OpenAI API Key:** Sử dụng mô hình GPT-4o cho AI Agent.
- **Slack Workspace:** Tạo Slack App để nhận thông báo và tương tác nút bấm (Approve/Deny).
- **Notion Workspace:** Tạo Database lưu trữ quy tắc định tuyến (Routing Directory).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Copy toàn bộ mã JSON của workflow từ n8n template (hoặc file JSON được cung cấp), sau đó dán trực tiếp vào giao diện n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Node `Webhook` & `Slack Button Press`:** Cấu hình đường dẫn URL webhook trong Unipile Dashboard và Slack App Interactivity & Shortcuts tab trỏ về các endpoint này.
- **Các node gọi API Unipile (`Get Linkedin User Data from Unipile`, `Send Message to LinkedIn via Unipile`...):** Cấu hình Generic Header Authentication với tên Header là `X-API-KEY` sử dụng token từ Unipile.
- **Node `Check if from me`:** Cập nhật `Unipile UserID` của chính các sếp (lấy bằng cách gửi 1 tin nhắn thử nghiệm để xem senderID xuất hiện ở đâu).
- **Node `Get Request Router Directory Database`:** Kết nối tài khoản Notion và trỏ tới Database chứa quy trình/kịch bản định tuyến yêu cầu.
- **OpenAI & Slack Credentials:** Đảm bảo điền đầy đủ API key cho **OpenAI Chat Model** và cấu hình Bot Token/Signing Secret cho các node **Slack** (`Send User Message`, `Delete Approved Message from Slack`...).

#### 3. Kích hoạt ⚡️
- Bấm **Execute Node** hoặc test thử bằng cách gửi 1 tin nhắn mẫu trên LinkedIn để kiểm tra luồng dữ liệu qua từng node (`Webhook` -> `AI Agent` -> `Slack`).
- Sau khi kiểm tra mọi thứ mượt mà, bật công tắc **Active** góc trên cùng bên phải để hệ thống tự động chạy 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo:** Thay vì chỉ dùng Slack, các sếp có thể nhân bản luồng gửi thông báo sang **Telegram** hoặc **Microsoft Teams**.
- **Lưu trữ lịch sử:** Thêm một node Google Sheets hoặc Airtable để lưu lại toàn bộ lịch sử tin nhắn khách hàng và kết quả xử lý của AI để phân tích chiến dịch sau này.
- **Tinh chỉnh Prompt:** Tùy chỉnh system prompt trong **AI Agent** để ép AI tuân thủ sát sao văn phong thương hiệu của công ty.

### 📌 Kết luận
Workflow này là một "vũ khí tối thượng" giúp tự động hóa toàn bộ phễu chăm sóc khách hàng và đối tác trên LinkedIn mà vẫn giữ được sự kiểm soát chặt chẽ của con người. Hãy triển khai ngay hôm nay để tối ưu hóa hiệu suất đội ngũ sales và CSKH của các sếp nhé!