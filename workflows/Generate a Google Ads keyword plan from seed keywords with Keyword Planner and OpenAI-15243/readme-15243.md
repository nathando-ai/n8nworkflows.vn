---
title: "🚀 Tự động hóa lập kế hoạch từ khóa Google Ads với Keyword Planner & OpenAI"
description: "Hướng dẫn chi tiết workflow n8n giúp tự động nghiên cứu từ khóa Google Ads từ seed keyword, phân tích bằng AI và lưu kết quả vào Google Sheets."
slug: "tu-dong-hoa-lap-ke-hoach-tu-khoa-google-ads-n8n"
tags: [n8n, automation, google-ads, openai, google-sheets, marketing-automation]
keywords: [n8n workflow, google ads keyword planner, openai gpt, tự động hóa marketing, nghiên cứu từ khóa]
---

# 🚀 Tự động hóa lập kế hoạch từ khóa Google Ads với Keyword Planner & OpenAI

Việc nghiên cứu từ khóa và xây dựng kế hoạch chạy Google Ads thủ công thường ngốn rất nhiều thời gian: từ việc cào dữ liệu từ Keyword Planner, lọc hàng trăm từ khóa, chấm điểm mức độ liên quan, phân loại ý định tìm kiếm (search intent) cho đến việc đưa vào Google Sheets để báo cáo. 

Được thiết kế bởi chuyên gia marketing Zeljislav Petrovic, workflow n8n này sẽ tự động hóa **100%** quy trình trên. Chỉ với một biểu mẫu (Form) điền thông tin cơ bản, hệ thống sẽ kết hợp sức mạnh của Google Keyword Planner API và OpenAI để phân tích, đánh giá, gợi ý thêm từ khóa thông minh và tự động xuất ra một file Google Sheets hoàn chỉnh.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Thay vì mất hàng giờ tổng hợp dữ liệu, toàn bộ kế hoạch từ khóa được tạo ra chỉ trong vài phút.
- **Phân tích chuyên sâu bằng AI:** AI tự động chấm điểm độ liên quan (1-10), phân loại *Search Intent*, đề xuất loại đối sánh (match type) và giá thầu tối ưu.
- **Tự động hóa Google Sheets:** Tự động tạo Spreadsheet mới và lưu trữ chi tiết cả 2 bảng: Kế hoạch từ khóa đã qua AI xử lý và danh sách từ khóa thô từ Keyword Planner.
- **Giao diện thu thập dữ liệu chuyên nghiệp:** Sử dụng `Form Trigger` giúp dễ dàng lấy thông tin đầu vào từ đội ngũ hoặc khách hàng.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Google Ads API Access:** Cần có Developer Token, Customer ID và OAuth 2.0 Credentials.
- **OpenAI API Key** (Sử dụng mô hình GPT-4o-mini hoặc tương đương).
- **Google Account:** Để kết nối với Google Sheets và tạo tự động Spreadsheet.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow từ n8n template hoặc copy đoạn mã JSON, sau đó dán trực tiếp vào n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình kỹ các node trọng điểm sau:
- **Form trigger - User input:** Nơi điền các thông tin đầu vào như Website URL, Tên công ty, Ngành nghề, Seed keywords, Sản phẩm/Dịch vụ.
- **Get keyword ideas from Google Keyword Planner (HTTP Request node):** 
  - Cập nhật `YOUR_GOOGLE_ADS_CUSTOMER_ID` trên URL.
  - Điền `YOUR_GOOGLE_ADS_DEVELOPER_TOKEN` vào phần header `developer-token`.
  - Điền `YOUR_MANAGER_ACCOUNT_ID` vào header `login-customer-id` (chỉ bắt buộc nếu truy cập qua tài khoản MCC / Manager account).
  - Kết nối đúng **Google Ads OAuth 2.0 credentials**.
- **GPT 5.4-mini & Analyze & enrich keywords with AI:** Kết nối tài khoản **OpenAI API** của các sếp.
- **Create spreadsheet / Save keyword plan / Save all keyword ideas (Google Sheets nodes):** Kết nối **Google Sheets OAuth 2.0 credentials** để cho phép workflow tự động tạo file và ghi dữ liệu.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (**Test run**) bằng cách submit form mẫu để kiểm tra toàn bộ luồng dữ liệu.
- Sau khi dữ liệu đổ về Google Sheets chính xác, bật công tắc **Active** để đưa workflow vào vận hành thực tế.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Thêm node Telegram hoặc Slack ở cuối workflow để gửi thông báo kèm link Google Sheets ngay khi hoàn tất việc tạo kế hoạch từ khóa.
- **Mở rộng AI Prompt:** Tùy chỉnh phần prompt trong AI Agent để phân tích thêm đối thủ cạnh tranh hoặc viết sẵn mẫu quảng cáo (Ad Copy) dựa trên danh sách từ khóa đạt điểm cao.
- **Lưu lịch sử chạy:** Lưu thông tin các lần nghiên cứu vào một bảng tổng hợp để dễ dàng theo dõi các chiến dịch marketing theo thời gian.

### 📌 Kết luận
Workflow tích hợp giữa Google Keyword Planner và OpenAI này là trợ thủ đắc lực cho các chuyên viên PPC, Agency và doanh nghiệp muốn tối ưu hóa quy trình nghiên cứu từ khóa. Hãy áp dụng ngay hôm nay để nâng tầm tự động hóa cho các chiến dịch Google Ads của các sếp!