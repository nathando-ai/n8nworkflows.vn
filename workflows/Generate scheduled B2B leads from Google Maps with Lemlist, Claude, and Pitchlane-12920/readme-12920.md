---
title: "🚀 Tự động quét Lead B2B từ Google Maps, tạo Video cá nhân hóa bằng AI và đổ về Lemlist với n8n"
description: "Xây dựng hệ thống tìm kiếm khách hàng tiềm năng B2B tự động từ Google Maps, kết hợp Claude AI, Pitchlane để tạo video cá nhân hóa và đồng bộ lên Lemlist hoàn toàn không cần code."
slug: "tu-dong-quet-lead-b2b-google-maps-lemlist-claude-pitchlane"
tags: [n8n, automation, lead-generation, ai, lemlist, google-maps]
keywords: [n8n workflow, tạo lead b2b tự động, google maps lead generation, lemlist automation, pitchlane video, claude ai n8n]
---

# 🚀 Tự động hóa toàn diện quy trình tìm kiếm Lead B2B & Video Outreach với AI

Các sếp có đang tốn hàng giờ mỗi ngày để tìm kiếm thông tin doanh nghiệp trên Google Maps, lọc thủ công tên chủ doanh nghiệp, tìm email rồi viết từng chiếc email hay quay từng video outreach nhàm chán không? Việc làm thủ công này vừa chậm, vừa dễ nản, lại khó scale-up đội ngũ sale.

Đừng lo, bài viết này sẽ hướng dẫn các sếp triển khai một siêu workflow n8n tự động hóa từ A-Z: Tự động quét khách hàng từ Google Maps, trích xuất thông tin người chủ (owner), phân tích website bằng AI, tạo video cá nhân hóa qua Pitchlane và đẩy thẳng vào hệ thống Lemlist từ 8h sáng mỗi ngày!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 mà không lo gián đoạn, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động 100% lịch trình:** Chạy tự động từ Thứ Hai đến Thứ Sáu lúc 9h sáng, liên tục cung cấp lead mới vào pipeline sale.
- **Cá nhân hóa đỉnh cao:** Sử dụng Anthropic Claude AI và Google Gemini/OpenAI để quét trang Imprint, tìm tên chủ doanh nghiệp, viết lời khen/tin nhắn tùy chỉnh cực kỳ tự nhiên.
- **Video Outreach chuyển đổi cao:** Tự động tạo video cá nhân hóa thông qua Pitchlane cho từng khách hàng mà không cần quay tay.
- **Đồng bộ liền mạch:** Tự động enrich email, thông tin LinkedIn và đẩy thẳng lead vào Lemlist để chiến dịch outbound chạy ngay lập tức.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow này "lên đồ" và chạy mượt mà, các sếp cần chuẩn bị sẵn các tài khoản và API Keys sau:
- **n8n Instance** (Self-hosted hoặc Cloud).
- **Google Maps Search API** (Ví dụ: Serper API hoặc dịch vụ tương đương) cho node `Search Google Maps`.
- **Anthropic API Key** (cho node `Generate message with Claude`).
- **OpenAI API Key** (cho node `Extract impressum data with AI`).
- **Google Gemini API Key** (cho node `Create marketing analysis`).
- **Pitchlane API Key** (cho node `Create video with Pitchlane`).
- **Lemlist Account & API** (cho việc enrich và add lead).
- **Google Docs OAuth2** (để lưu tài liệu báo cáo phân tích nếu cần).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow hoặc copy trực tiếp mã nguồn JSON từ nguồn cung cấp.
- Mở n8n Editor của các sếp, chọn **Add workflow** -> Nhấn vào dấu 3 chấm ở góc trên bên phải chọn **Import from File / Paste JSON**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow gồm 25 nodes được chia thành 4 giai đoạn chính, các sếp cần cấu hình kỹ các điểm sau:
- **Schedule trigger (Monday-Friday 9 AM):** Điều chỉnh lại múi giờ (Timezone) cho đúng với giờ Việt Nam (Asia/Ho_Chi_Minh) nếu muốn bot chạy đúng 9h sáng giờ VN.
- **Configure search parameters (Set):** Điền từ khóa tìm kiếm (category) và vị trí địa lý (location) cụ thể mà các sếp muốn quét trên Google Maps (Ví dụ: "Marketing Agency" tại "Berlin").
- **Search Google Maps (HTTP Request):** Cấu hình lại Header Auth với API Key từ dịch vụ tìm kiếm bản đồ (như Serper.dev).
- **Claude, OpenAI & Gemini Nodes:** Kết nối các Credentials tương ứng của các nhà cung cấp AI này. Đảm bảo tài khoản API có đủ số dư để xử lý phân tích trang web và viết nội dung.
- **Create video with Pitchlane (HTTP Request):** Điền API key của Pitchlane và trỏ đến template video cá nhân hóa đã tạo sẵn trên nền tảng này.
- **Webhook for video completion & Lemlist Nodes:** Node webhook sẽ nhận tín hiệu callback từ Pitchlane khi video render xong, sau đó node `📤 Lemlist: Add Lead1` và `Enrich lead with Lemlist` sẽ đẩy toàn bộ dữ liệu (Lead + Video + Tin nhắn AI) vào chiến dịch Lemlist của các sếp.

#### 3. Kích hoạt ⚡️
- Nhấn nút **Execute Workflow** chạy thử với một lượng dữ liệu nhỏ để kiểm tra xem các node AI, Google Maps và Pitchlane có phản hồi chính xác không.
- Sau khi test thành công không báo lỗi, hãy bật nút **Active** ở góc trên cùng bên phải để hệ thống tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Thêm thông báo Telegram/Slack:** Các sếp có thể gắn thêm một node Telegram ở cuối chuỗi để nhận thông báo ngay lập tức mỗi khi có một lead mới được tạo video và đẩy lên Lemlist thành công.
- **Lưu trữ Log Google Sheets:** Kết hợp thêm node Google Sheets để ghi lại lịch sử quét lead hàng ngày, tiện cho việc theo dõi hiệu suất chiến dịch marketing.
- **Tinh chỉnh Prompt cho AI:** Tối ưu hóa các System Prompt trong node Claude để văn phong tin nhắn outreach phù hợp hơn với văn hóa kinh doanh tại thị trường Việt Nam hoặc quốc tế mà các sếp hướng tới.

### 📌 Kết luận
Workflow này là một "vũ khí tối thượng" giúp tự động hóa toàn bộ phễu tìm kiếm khách hàng B2B, kết hợp sức mạnh của dữ liệu địa lý và AI đa phương thức (Multimodal AI). Hãy cài đặt ngay lên VPS của các sếp và tối ưu hóa quy trình sales ngay hôm nay!