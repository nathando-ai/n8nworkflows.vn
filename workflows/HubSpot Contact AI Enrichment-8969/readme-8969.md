---
title: "🚀 Tự động làm giàu dữ liệu khách hàng HubSpot bằng AI Agent và Google Gemini"
description: "Hướng dẫn xây dựng workflow n8n tự động quét liên hệ mới trên HubSpot trong 24h, tìm kiếm thông tin công ty qua SerpAPI và cập nhật lại CRM bằng AI."
slug: "hubspot-contact-ai-enrichment-n8n"
tags: [n8n, automation, hubspot, ai-agent, google-gemini, crm]
keywords: [n8n workflow, hubspot automation, ai enrichment, google gemini, serpapi, crm automation]
keywords: [n8n workflow, tự động hóa, hubspot enrichment, ai agent, gemini, serpapi]
---

# 🚀 Tự động làm giàu dữ liệu khách hàng HubSpot bằng AI Agent và Google Gemini

Các sếp có bao giờ cảm thấy mệt mỏi khi phải tốn hàng giờ tra cứu thông tin công ty của khách hàng mới trên Google để điền vào CRM HubSpot? Việc nhập liệu thủ công này không chỉ chậm chạp mà còn dễ bỏ sót các thông tin quan trọng.

Đừng lo, bài viết này sẽ hướng dẫn các sếp thiết lập một workflow n8n cực kỳ mạnh mẽ: **HubSpot Contact AI Enrichment**. Workflow này sẽ tự động tìm kiếm, nghiên cứu và làm giàu thông tin công ty cho các liên hệ mới trên HubSpot hoàn toàn bằng AI mà không cần tốn một giọt mồ hôi nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 100% thời gian:** Tự động hóa hoàn toàn quy trình nghiên cứu công ty của khách hàng tiềm năng.
- **Dữ liệu CRM luôn sạch và đầy đủ:** Tự động điền các thông tin chi tiết về doanh nghiệp vào HubSpot ngay sau khi có liên hệ mới.
- **Cá nhân hóa bán hàng:** Giúp đội ngũ sales có ngay bức tranh toàn cảnh về khách hàng trước khi gọi điện tư vấn.
- **Hoạt động tự động 24/7:** Chạy ngầm định kỳ hàng ngày mà không cần sự can thiệp thủ công.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Tài khoản HubSpot** (với quyền truy cập API/OAuth2).
- **Tài khoản SerpAPI** để AI có thể tìm kiếm thông tin trên web (Lấy API key tại [serpapi.com](https://serpapi.com/manage-api-key)).
- **Tài khoản Google AI Studio** để sử dụng mô hình Google Gemini (Lấy API key tại [Google AI Studio](https://aistudio.google.com/)).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể sử dụng file JSON của workflow này, copy và paste trực tiếp vào n8n Editor của mình. Workflow bao gồm 8 nodes chính phối hợp nhịp nhàng với nhau:
- **Run daily (`scheduleTrigger`):** Kích hoạt lịch chạy tự động mỗi ngày.
- **Get recently created/updated contacts (`hubspot`):** Lấy danh sách các liên hệ mới tạo hoặc cập nhật gần đây từ HubSpot.
- **Filter contacts created in the last 24h (`filter`):** Lọc ra các liên hệ được tạo trong vòng 24 giờ qua (loại bỏ các liên hệ Gmail cá nhân nếu cần).
- **Company Research Agent (`agent`), Google Gemini Chat Model (`lmChatGoogleGemini`), Search the web with SerpAPI (`toolSerpApi`), Structured Output Parser (`outputParserStructured`):** Bộ não AI kết hợp khả năng tìm kiếm web để nghiên cứu sâu về công ty của khách hàng và chuẩn hóa dữ liệu đầu ra.
- **Add company info (`hubspot`):** Đẩy thông tin công ty đã được làm giàu ngược trở lại HubSpot.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp nhớ cấu hình kỹ các điểm sau:
- **Kết nối HubSpot Credentials:** Tại cả 2 node **Get recently created/updated contacts** và **Add company info**, các sếp cần cấu hình xác thực `hubspotOAuth2Api` để n8n có quyền đọc/ghi dữ liệu trên CRM của các sếp.
- **Cấu hình SerpAPI:** Nhập API Key lấy từ SerpAPI vào credentials của node **Search the web with SerpAPI** để AI có thể "lướt web" tìm kiếm thông tin doanh nghiệp.
- **Cấu hình Google Gemini:** Thêm Google Palm/Gemini API Key vào node **Google Gemini Chat Model** để cung cấp AI LLM cho Agent.
- **Tùy chỉnh Prompt Agent:** Tại node **Company Research Agent**, các sếp có thể tinh chỉnh câu lệnh (prompt) để AI thu thập đúng những trường thông tin mà đội ngũ sales của các sếp đang cần (quy mô công ty, ngành nghề, sản phẩm chính,...).

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** để chạy thử nghiệm với dữ liệu mẫu xem hệ thống đã bốc tách và cập nhật chuẩn xác chưa.
- Sau khi test OK, gạt công tắc sang **Active** để workflow tự động chạy ngầm mỗi ngày.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Nối thêm node Telegram hoặc Slack sau bước cập nhật HubSpot để bắn thông báo về nhóm sale ngay khi có khách hàng tiềm năng mới được "làm giàu" thông tin.
- **Lưu log vào Google Sheets:** Thêm node Google Sheets để lưu lại lịch sử các công ty đã được AI nghiên cứu nhằm phục vụ việc kiểm tra và báo cáo.
- **Mở rộng bộ nhớ AI:** Có thể tích hợp thêm Vector Store hoặc tài liệu nội dung sản phẩm của công ty để AI đánh giá mức độ phù hợp (Lead Scoring) của khách hàng ngay trong quá trình nghiên cứu.

### 📌 Kết luận
Workflow **HubSpot Contact AI Enrichment** là một ví dụ điển hình cho thấy sức mạnh của việc kết hợp n8n và AI Agent trong việc tối ưu hóa vận hành CRM. Hãy cài đặt ngay hôm nay để giải phóng thời gian cho đội ngũ sales và tăng tốc độ tiếp cận khách hàng tiềm năng của doanh nghiệp các sếp nhé!