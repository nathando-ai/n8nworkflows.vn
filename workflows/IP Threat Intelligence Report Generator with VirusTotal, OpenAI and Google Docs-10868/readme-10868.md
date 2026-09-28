---
title: "🚀 Tự động tạo Báo cáo Tình báo Mối đe dọa IP với VirusTotal, OpenAI và Google Docs"
description: "Hướng dẫn xây dựng workflow n8n tự động phân tích địa chỉ IP độc hại, tra cứu định vị, quét VirusTotal và tổng hợp thành báo cáo chuyên nghiệp trên Google Docs bằng AI."
slug: "tu-dong-tao-bao-cao-tinh-bao-moi-de-doa-ip-n8n"
tags: [n8n, automation, secops, virustotal, openai, google-docs, ai-agent]
keywords: [n8n workflow, threat intelligence, virustotal api, openai chatgpt, google docs automation, secops automation]
---

# 🚀 Tự động tạo Báo cáo Tình báo Mối đe dọa IP với VirusTotal, OpenAI và Google Docs

Các anh em làm trong ngành bảo mật (SecOps) hoặc IT chắc chắn hiểu rõ nỗi đau khi phải xử lý các cảnh báo bảo mật. Mỗi khi phát hiện một địa chỉ IP lạ, việc tra cứu thông tin định vị (geolocation), kiểm tra lịch sử độc hại trên VirusTotal và viết báo cáo chi tiết tốn rất nhiều thời gian thủ công.

Workflow n8n này sinh ra để giải quyết triệt để vấn đề đó! Chỉ với vài cú click, hệ thống sẽ tự động hóa toàn bộ quy trình: thu thập IP từ biểu mẫu, quét dữ liệu từ các nguồn uy tín, nhờ AI phân tích đánh giá mức độ nguy hiểm và xuất thẳng kết quả thành một bản báo cáo hoàn chỉnh trên Google Docs.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Không cần tra cứu thủ công trên nhiều tab trình duyệt hay copy-paste dữ liệu vào Word/Google Docs nữa.
- **Phân tích thông minh bằng AI:** OpenAI Agent sẽ tổng hợp, đánh giá rủi ro và đưa ra khuyến nghị xử lý chuyên sâu như một chuyên gia An ninh mạng thực thụ.
- **Báo cáo chuẩn chỉnh:** Tự động tạo tài liệu Google Docs sạch đẹp, sẵn sàng chia sẻ cho ban quản lý hoặc đội ngũ ứng phó sự cố.
- **Quy trình khép kín:** Hoạt động liền mạch từ khâu nhận yêu cầu (Form) đến khâu trả kết quả cuối cùng.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động trơn tru, các sếp cần chuẩn bị sẵn các tài khoản và API keys sau:
1. **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
2. **VirusTotal API Key:** Tài khoản miễn phí hoặc trả phí trên VirusTotal để truy vấn dữ liệu IP.
3. **OpenAI API Key:** Để cấp quyền cho AI Agent phân tích và viết báo cáo.
4. **Google Account:** Tài khoản Google để kết nối và tạo/cập nhật tài liệu trên Google Docs.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể copy mã nguồn JSON của workflow từ n8n.io và dán trực tiếp vào n8n Editor của mình thông qua tính năng Import từ Clipboard.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import thành công, các sếp cần cấu hình chính xác các node quan trọng sau đây:

- **Landing Page Url (`formTrigger`):** Node này tạo một giao diện form đơn giản để nhập địa chỉ IP cần kiểm tra. Các sếp có thể tùy chỉnh lại giao diện form hoặc để mặc định để lấy URL test nhanh.
- **Set IP Address1 (`set`):** Nhận dữ liệu đầu vào từ form và chuẩn hóa định dạng địa chỉ IP để chuyển sang các bước tiếp theo.
- **Query Geolocation1 & VirusTotal HTTP Request1 (`httpRequest`):** 
  - Cần cấu hình Header chứa **VirusTotal API Key** cho node VirusTotal.
  - Kiểm tra lại endpoint API của VirusTotal để đảm bảo query đúng thông tin về IP (ví dụ: `https://www.virustotal.com/api/v3/ip_addresses/{ip}`).
- **OpenAI Chat Model1 & AI Agent1 (`lmChatOpenAi` & `agent`):**
  - Kết nối Credentials của OpenAI.
  - Cấu hình Prompt cho Agent để hướng dẫn AI cách đọc dữ liệu thô từ VirusTotal và Geolocation, từ đó viết ra một bản báo cáo phân tích mối đe dọa (Threat Intelligence Report) thật chuyên nghiệp.
- **Update a document1 (`googleDocs`):**
  - Kết nối tài khoản Google Docs của các sếp.
  - Chọn file Google Docs mẫu (Template) hoặc tạo một file trống mới, sau đó ánh xạ (map) nội dung được tổng hợp từ AI Agent vào tài liệu này.

#### 3. Kích hoạt ⚡️
- Nhấn nút **Execute Workflow** và điền một địa chỉ IP mẫu vào form để test thử xem dữ liệu có chảy qua các node suôn sẻ không.
- Kiểm tra lại kết quả trên Google Docs xem báo cáo đã hiển thị đúng ý chưa.
- Nếu mọi thứ đã hoàn hảo, hãy gạt công tắc sang chế độ **Active** để đưa workflow vào vận hành chính thức.

---

### ✍️ Mẹo & gợi ý nâng cao
Để workflow trở nên "bá đạo" hơn nữa, các sếp có thể mở rộng thêm một số tính năng:
1. **Tích hợp kênh thông báo:** Thêm node Slack hoặc Telegram ngay sau bước AI Agent để bắn tin nhắn tóm tắt cảnh báo về nhóm chat chung của team IT/SecOps ngay lập tức.
2. **Lưu trữ lịch sử:** Thêm node Google Sheets hoặc Airtable để ghi lại log tất cả các IP đã từng được kiểm tra nhằm phục vụ việc thống kê định kỳ.
3. **Quét hàng loạt (Batch Processing):** Thay vì dùng Form Trigger đơn lẻ, các sếp có thể đổi thành Webhook nhận danh sách IP từ hệ thống SIEM hoặc Firewall để tự động hóa hoàn toàn.

### 📌 Kết luận
Việc tự động hóa quy trình phân tích mối đe dọa không chỉ giúp đội ngũ bảo mật tiết kiệm thời gian mà còn tăng tốc độ phản ứng trước các cuộc tấn công mạng. Hãy áp dụng ngay workflow này vào hệ thống của các sếp để tối ưu hóa năng suất làm việc!