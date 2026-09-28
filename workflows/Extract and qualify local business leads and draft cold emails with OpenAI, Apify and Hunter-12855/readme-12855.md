---
title: "🚀 Tự động quét Lead doanh nghiệp địa phương, chấm điểm và viết Cold Email bằng AI"
description: "Khám phá quy trình tự động hóa n8n hoàn chỉnh giúp trích xuất lead từ Apify, cào website, lọc chất lượng bằng OpenAI, xác thực email với Hunter và lưu trữ vào Google Sheets."
slug: "tu-dong-quet-lead-doanh-nghiep-dia-phuong-openai-apify-hunter"
tags: [n8n, automation, lead-generation, openai, apify, google-sheets, ai-agents]
keywords: [n8n workflow, quét lead tự động, apify lead generation, openai cold email, hunter email verify, google sheets crm]
---

# 🚀 Tự động quét Lead doanh nghiệp địa phương, chấm điểm và viết Cold Email bằng AI

Các sếp có đang mệt mỏi với việc tìm kiếm khách hàng tiềm năng (lead) thủ công? Phải mò mẫm trên Google Maps, copy từng website, đoán email rồi ngồi soạn từng nội dung chào hàng nhàm chán? 

Việc này ngốn hàng tá thời gian mà hiệu quả lại thấp. Quy trình n8n này sẽ thay các sếp làm trọn gói từ A-Z: **Tự động kéo lead từ Apify, cào nội dung website, dùng AI chuẩn hóa và chấm điểm, kiểm tra độ sống của email, lưu vào CRM Google Sheets và tự động soạn sẵn các mẫu Cold Email siêu cá nhân hóa.** Không cần viết một dòng code nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 mà không sợ sập, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100% phễu lọc Lead:** Thay vì tốn hàng chục giờ thủ công, hệ thống tự động gom và phân loại hàng trăm lead mỗi ngày.
- **Chấm điểm thông minh bằng AI:** Các AI Agent (`Lead Qualification Agent`, `Lead Normalize Agent`) giúp đánh giá chính xác nhu cầu và mức độ tiềm năng của doanh nghiệp.
- **Xác thực email sạch:** Node `Hunter` giúp loại bỏ ngay các email chết, bảo vệ uy tín domain gửi mail của các sếp.
- **Cá nhân hóa Cold Email:** AI tự động viết nội dung tiếp cận dựa trên dữ liệu thực tế của website doanh nghiệp đó, sẵn sàng cho các chiến dịch Outreach.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow vận hành trơn tru, các sếp cần chuẩn bị sẵn các tài khoản và API Keys sau:
- **Apify Account:** Để trích xuất dữ liệu doanh nghiệp từ Google Search/Maps (dataset).
- **OpenAI Account:** Cung cấp API Key cho các AI Agents xử lý ngôn ngữ, chuẩn hóa và viết email.
- **Google Sheets:** Tạo sẵn một file Google Sheets để lưu trữ dữ liệu CRM (Lead và Cold Email).
- **Hunter.io:** Lấy API Key để xác thực tính sống/chết của email.
- **Tavily API:** Dùng để tra cứu và bổ sung thông tin (enrichment) nếu cần.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow này hoặc copy toàn bộ mã nguồn JSON.
- Trong giao diện n8n, chọn **Add workflow** -> Click vào menu ba chấm (...) ở góc trên bên phải -> Chọn **Import from File** hoặc **Import from Clipboard** và dán mã vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Node `Get dataset items` (Apify):** Cần kết nối tài khoản Apify OAuth2 và thay thế Dataset ID bằng ID dữ liệu trích xuất của các sếp.
- **Node `Limit`:** Workflow để sẵn node Limit nhằm giới hạn số lượng chạy thử nghiệm. *Đừng vội xóa node này* cho đến khi các sếp đã test thành công toàn bộ hệ thống.
- **Các node AI (`Lead Normalize Agent`, `Lead Qualification Agent`, `Cold Email Writer AI Agent1`):** Kết nối OpenAi API Credentials và kiểm tra cấu hình model (mặc định sử dụng các model tối ưu chi phí như `gpt-4o-mini` hoặc tương đương).
- **Node `Hunter`:** Kết nối Hunter API để hệ thống tự động kiểm tra email.
- **Node `Write Qualified Leads to CRM` & `Write Cold Email to CRM` (Google Sheets):** Kết nối tài khoản Google Sheets OAuth2, chọn đúng file Spreadsheet ID và Sheet Name. Cấu hình dùng chế độ `appendOrUpdate` để tránh trùng lặp dữ liệu khi chạy lại workflow.
- **Node `Filter Qualified Leads`:** Tùy chỉnh các tiêu chí lọc lead sao cho phù hợp với ngành hàng kinh doanh thực tế của các sếp.

#### 3. Kích hoạt ⚡️
- Click nút **Execute Workflow** trên node `When clicking ‘Execute workflow’` để test chạy thử với số lượng nhỏ từ node Limit.
- Kiểm tra kết quả trả về trên Google Sheets xem dữ liệu đã đổ đúng ý chưa.
- Sau khi kiểm tra mọi thứ mượt mà, gạt công tắc sang **Active** để workflow chạy tự động theo lịch hoặc trigger.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Thêm node Telegram hoặc Slack ở cuối workflow để nhận thông báo ngay lập tức mỗi khi có một Qualified Lead mới xuất hiện trên CRM.
- **Tự động gửi email:** Mặc định workflow chỉ lưu bản nháp vào Google Sheets (`Write Cold Email to CRM`) để các sếp review thủ công. Nếu tự tin, các sếp có thể gắn thêm node Gmail hoặc Resend để hệ thống tự động gửi mail đi.
- **Mở rộng nguồn Lead:** Ngoài Apify Google Maps, có thể kết hợp thêm các scraper nền tảng khác như LinkedIn, YellowPages tùy theo mô hình B2B hay B2C.

### 📌 Kết luận
Xây dựng một hệ thống quét lead và outreach tự động bằng AI chưa bao giờ dễ dàng đến thế với n8n. Hãy áp dụng ngay workflow này để tối ưu hóa đội ngũ sales và bùng nổ doanh số trong thời gian ngắn nhất các sếp nhé!