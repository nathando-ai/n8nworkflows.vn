---
title: "🚀 Tự động tìm kiếm Leads LinkedIn và soạn tin nhắn cá nhân hóa với Apify, Google Sheets & Gemini"
description: "Khám phá quy trình tự động hóa n8n giúp tìm kiếm khách hàng tiềm năng trên LinkedIn, quét thông tin chi tiết và sử dụng AI Gemini để viết tin nhắn outreach cực kỳ thuyết phục."
slug: "tu-dong-tim-kiem-linkedin-leads-apify-google-sheets-gemini"
tags: [n8n, automation, no-code, lead-generation, apify, google-sheets, google-gemini]
keywords: [n8n workflow, tìm kiếm leads linkedin, apify linkedin scraper, google sheets automation, google gemini ai outreach]
---

# 🚀 Tự động tìm kiếm Leads LinkedIn và soạn tin nhắn outreach chuẩn AI với Apify, Google Sheets & Gemini

Các sếp có đang đau đầu vì tốn hàng giờ mỗi ngày để tìm kiếm khách hàng tiềm năng (leads) trên LinkedIn, thủ công copy/paste thông tin vào Google Sheets, rồi lại vắt óc suy nghĩ từng câu mở lời (outreach message) để nhắn tin mà tỷ lệ phản hồi lại thấp? Việc làm thủ công này vừa nhàm chán, tốn thời gian lại khó scale (mở rộng quy mô) đội ngũ sales.

Đừng lo, bài toán này sẽ được giải quyết triệt để với **Workflow n8n: Discover LinkedIn leads and draft outreach using Apify, Google Sheets, and Gemini** do tác giả *Dinakar Selvakumar* thiết kế. Workflow này sẽ tự động hóa toàn bộ phễu tìm kiếm, làm giàu dữ liệu (enrichment) và ứng dụng Trí tuệ Nhân tạo (AI) để "đo ni đóng giày" nội dung kết nối cực kỳ tinh tế cho từng khách hàng!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động 100% phễu Sales LinkedIn**: Từ việc tạo từ khóa tìm kiếm, quét profile, lưu trữ đến soạn tin nhắn chào hỏi (Connection Message) và tin nhắn theo dõi (Follow-up Message).
- **Cá nhân hóa đỉnh cao bằng AI**: Google Gemini sẽ phân tích dữ liệu profile thực tế của leads để viết thông điệp outreach tự nhiên, đúng trọng tâm ngành nghề của họ, tăng gấp đôi tỷ lệ chấp nhận kết nối.
- **Quản lý dữ liệu trực quan**: Mọi thông tin leads và bản nháp tin nhắn được đồng bộ mượt mà vào Google Sheets giúp đội ngũ Sales dễ dàng kiểm duyệt và thực thi.
- **Vận hành không gián đoạn**: Sử dụng cơ chế chia lô (Batch Processing) giúp xử lý lượng lớn dữ liệu mà không lo vượt quá giới hạn API (Rate Limits).
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Tài khoản Apify**: Cần có API Token để gọi các actor trích xuất dữ liệu LinkedIn.
- **Tài khoản Google Workspace / Google Sheets**: Chuẩn bị sẵn một file Google Sheet làm cơ sở dữ liệu lưu trữ leads.
- **Google Gemini API Key**: Để cung cấp năng lượng AI cho các node tạo thông điệp.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON từ link gốc của workflow trên n8n.io, sau đó vào giao diện n8n Editor chọn **Add workflow** -> **Import from File** (hoặc copy toàn bộ JSON và dán trực tiếp vào n8n).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống chạy mượt mà, các sếp cần cấu hình chính xác các node trọng điểm sau:
- **Search in Apify & Scrape LinkedIn Profile Data (`httpRequest`)**: Cần thiết lập Apify API Token hợp lệ trong phần Credentials của node để tiến hành tìm kiếm và quét thông tin profile LinkedIn theo yêu cầu.
- **Save in Database, Load Unenriched Profiles, Save Enriched Lead Data, Update Follow-Up in Sheet, Mark Profile as Enriched (`googleSheets`)**: Kết nối với tài khoản Google Drive/Sheets của các sếp. Chọn đúng file Google Sheets và tên Sheet (Tab) tương ứng để lưu thông tin leads, cập nhật trạng thái đã xử lý (*Enriched*).
- **Generate Connection Message & Generate Follow-Up Message (`googleGemini`)**: Nhập Google Gemini API Key. Các sếp có thể tùy chỉnh lại System Prompt trong node này để AI viết tin nhắn theo đúng văn phong (formal, thân thiện, hài hước...) của thương hiệu mình.
- **Generate LinkedIn Search Queries, Flatten Apify Results (`code`)**: Các node xử lý dữ liệu bằng JavaScript giúp làm sạch cấu trúc dữ liệu trả về từ Apify trước khi đẩy vào database.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** với một vài dòng dữ liệu mẫu để kiểm tra xem Apify có quét được dữ liệu, Gemini có sinh ra tin nhắn và Google Sheets có ghi nhận thành công hay không.
- Sau khi test xanh mướt (success), các sếp gạt công tắc sang **Active** để workflow tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp kênh thông báo**: Thêm node Telegram hoặc Slack ngay sau khi tạo xong tin nhắn để gửi thông báo về máy cho nhân sự sales vào duyệt trước khi gửi.
- **Mở rộng kịch bản Follow-up**: Thêm các mốc thời gian chờ (Wait node) và kịch bản Gemini sinh tin nhắn follow-up lần 2, lần 3 nếu khách hàng chưa phản hồi sau 3-5 ngày.
- **Tự động hóa gửi tin nhắn**: Nếu có giải pháp phù hợp, có thể kết hợp thêm các công cụ tự động hóa trình duyệt để gửi thẳng tin nhắn kết nối lên LinkedIn.

### 📌 Kết luận
Workflow *Discover LinkedIn leads and draft outreach* là trợ thủ đắc lực giúp tối ưu hóa quy trình Sales B2B thời đại AI. Thay vì tốn hàng giờ cày cuốc thủ công, các sếp giờ đây chỉ cần ngồi duyệt danh sách khách hàng tiềm năng chất lượng cao do hệ thống tự động chuẩn bị sẵn. Lên đồ ngay và tối ưu hóa doanh số cùng n8n thôi nào!