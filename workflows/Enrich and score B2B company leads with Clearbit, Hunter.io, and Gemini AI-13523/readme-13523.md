---
title: "🚀 Tự động làm giàu và chấm điểm lead B2B thông minh với Clearbit, Hunter.io và Google Gemini AI"
description: "Hướng dẫn xây dựng hệ thống tự động hóa n8n giúp khai thác thông tin công ty, tìm kiếm liên hệ, phân tích uy tín và dùng AI chấm điểm lead B2B cực kỳ chuẩn xác."
slug: "tu-dong-lam-giau-va-cham-diem-lead-b2b-clearbit-hunter-gemini"
tags: [n8n, automation, lead-generation, ai-summarization, clearbit, gemini, google-sheets]
keywords: [n8n workflow, làm giàu lead b2b, chấm điểm lead ai, clearbit n8n, hunter io n8n, google gemini ai]
---

# 🚀 Tự động làm giàu và chấm điểm lead B2B thông minh với Clearbit, Hunter.io và Google Gemini AI

Các sếp có bao giờ cảm thấy mệt mỏi khi đội ngũ sales phải "bới lông tìm vết", mất hàng giờ tra cứu thông tin từng công ty, tìm email liên hệ, kiểm tra website rồi mới dám nhấc máy gọi không? Công việc thủ công này vừa tốn thời gian, vừa dễ bỏ sót khách hàng tiềm năng chất lượng cao (Hot Lead).

Đừng lo, bài toán đó sẽ được giải quyết triệt để với workflow n8n cực kỳ mạnh mẽ này. Hệ thống sẽ tự động hóa từ A-Z quy trình: Nhận thông tin tên miền công ty -> Làm giàu dữ liệu từ Clearbit -> Tìm kiếm email/liên hệ từ Hunter.io -> Cào và phân tích thông tin website -> Sử dụng sức mạnh siêu việt của **Google Gemini AI** để chấm điểm, đánh giá tiềm năng -> Lưu trữ vào Google Sheets và ngay lập tức bắn thông báo "nóng hổi" về Slack nếu đó là khách hàng VIP!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Sales không còn phải tra cứu thủ công hàng loạt tab trình duyệt nữa.
- **Chấm điểm thông minh (AI Lead Scoring):** Google Gemini AI tự động phân tích độ phù hợp dựa trên dữ liệu thực tế thu thập được.
- **Cảnh báo tức thì:** Phát hiện ngay Hot Lead và gửi thông báo về Slack để đội ngũ sales chốt đơn thần tốc.
- **Dữ liệu đồng bộ:** Tự động lưu toàn bộ thông tin chi tiết vào Google Sheets để tracking và chăm sóc dài hạn.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Clearbit API Key:** Dùng để lấy dữ liệu tổng quan về công ty.
- **Hunter.io API Key:** Dùng để tìm kiếm danh sách liên hệ, email trong doanh nghiệp.
- **Google Gemini API Key:** Cung cấp trí tuệ nhân tạo để phân tích và chấm điểm lead.
- **Google Sheets:** Tạo sẵn một file Google Sheets để lưu danh sách lead.
- **Slack Webhook / Integration:** Để nhận cảnh báo Lead nóng.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy toàn bộ mã nguồn JSON của workflow (hoặc tải file từ n8n.io) và Paste trực tiếp vào n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 15 nodes được thiết kế tỉ mỉ. Các sếp cần cấu hình chính xác các điểm sau:
- **Lead Input Form (`formTrigger`):** Thiết kế form thu thập thông tin đầu vào (Tên công ty, Website, v.v.) từ khách hàng hoặc đội ngũ sales.
- **Clearbit Enrichment (`httpRequest`) & Hunter.io Contacts (`httpRequest`):** Điền API Key tương ứng của các dịch vụ này vào phần Header Authentication của node.
- **Google Maps Reputation (`httpRequest`) & Fetch Company Website (`httpRequest`):** Kiểm tra lại các endpoint hoặc tham số truyền vào để đảm bảo việc cào dữ liệu hoạt động mượt mà.
- **AI Lead Scorer (`chainLlm`) & Google Gemini Chat Model (`lmChatGoogleGemini`):** Kết nối tài khoản Google Gemini và tinh chỉnh câu lệnh (Prompt) trong node AI để AI hiểu tiêu chí chấm điểm lead phù hợp nhất với sản phẩm/dịch vụ của công ty các sếp.
- **Save to Google Sheets (`googleSheets`):** Chọn đúng file Google Sheets và Sheet Name đã chuẩn bị sẵn, map các trường dữ liệu từ node `Prepare Final Output` vào các cột tương ứng.
- **Slack Hot Lead Alert (`slack`):** Cấu hình kênh Slack nhận thông báo và tùy chỉnh nội dung tin nhắn khi có lead đạt điểm số cao vượt ngưỡng từ node `Hot Lead Filter`.

#### 3. Kích hoạt ⚡️
- Bấm nút **Execute Workflow** và test thử bằng một vài dữ liệu công ty mẫu qua Form.
- Kiểm tra kết quả trên Google Sheets và Slack xem dữ liệu đã đổ về chính xác chưa.
- Sau khi mọi thứ chạy mượt mà, gạt công tắc sang **Active** để hệ thống tự động hóa hoạt động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo:** Thay vì chỉ dùng Slack, các sếp có thể nối thêm node Telegram hoặc gửi Email tự động chúc mừng/cảm ơn khách hàng vừa điền form.
- **Tích hợp CRM:** Thay vì chỉ lưu Google Sheets, có thể đẩy thẳng lead vào HubSpot, Salesforce hoặc Notion để tối ưu quy trình quản trị quan hệ khách hàng.
- **Tự động gửi email outreach:** Kết nối thêm một bước gửi email giới thiệu dịch vụ tự động nếu điểm số Lead Scorer đạt mức A+ (Hot Lead).

### 📌 Kết luận
Hệ thống tự động hóa làm giàu và chấm điểm B2B lead này sẽ giúp doanh nghiệp của các sếp đi trước đối thủ một bước trong việc tiếp cận khách hàng tiềm năng. Hãy thiết lập ngay hôm nay để giải phóng sức lao động cho đội ngũ sales và tối ưu hóa tỷ lệ chuyển đổi!