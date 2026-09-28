---
title: "🚀 Trích xuất Insights Marketing từ Google Reviews tự động với Dumpling AI và GPT-4"
description: "Hướng dẫn xây dựng workflow n8n tự động lấy đánh giá Google Reviews, sử dụng GPT-4 phân tích insights marketing và lưu kết quả vào Google Sheets."
slug: "trich-xuat-marketing-insights-google-reviews-dumpling-ai-gpt-4"
tags: [n8n, automation, ai, gpt-4, google-sheets, marketing-research]
keywords: [n8n workflow, google reviews insights, dumpling ai gpt4, phan tich voice of customer, tu dong hoa marketing]
---

# 🚀 Trích xuất Insights Marketing từ Google Reviews tự động với GPT-4

Các sếp làm marketing, product hay brand strategist có bao giờ cảm thấy đuối sức khi phải đọc hàng trăm, hàng ngàn đánh giá (Google Reviews) của khách hàng để tìm ra "Voice of Customer" (VOC)? Việc ngồi đọc thủ công, phân loại điểm đau (frictions), động lực mua hàng hay góc độ marketing vừa tốn thời gian vừa dễ bỏ sót ý tưởng đắt giá.

Giải pháp đây rồi! Workflow n8n này sẽ tự động hóa 100% quy trình: Nhập tên doanh nghiệp và Place ID -> Lấy review qua Dumpling AI -> Tổng hợp và dùng GPT-4 phân tích chuyên sâu -> Lưu thẳng kết quả vào Google Sheets. Các sếp chỉ việc ngồi chờ nhận insights xịn xò để lên chiến dịch!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Thay vì mất hàng giờ đọc review thủ công, AI xử lý và tóm tắt chỉ trong vài giây.
- **Phân tích toàn diện:** Tự động trích xuất góc độ marketing (marketing angles), động lực khách hàng, rào cản (frictions), cơ hội sản phẩm và các câu nói đắt giá từ khách hàng (VOC quotes).
- **Lưu trữ khoa học:** Mọi insights tự động đổ về Google Sheets để team dễ dàng truy xuất và lên kế hoạch content, ads.
- **Hoạt động theo yêu cầu:** Giao diện Form đơn giản giúp bất kỳ ai trong team cũng có thể chủ động tra cứu dữ liệu.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản n8n (Cloud hoặc Self-hosted).
- Tài khoản **Dumpling AI** (để lấy API key gọi Google Reviews).
- Tài khoản **OpenAI API Key** (dùng cho model GPT-4o).
- Tài khoản **Google Sheets** (để lưu trữ kết quả phân tích).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow hoặc copy trực tiếp và dán vào n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình chính xác các node sau:

- **Submit Business Name + Place ID (`formTrigger`):** Node khởi đầu dạng Form, cho phép người dùng nhập tên doanh nghiệp và Google Place ID cần phân tích.
- **🔎 Dumpling AI: Fetch Google Reviews (`httpRequest`):** Kết nối API của Dumpling AI để lấy top 30 reviews mới nhất dựa trên Place ID. Cần cấu hình `httpHeaderAuth` với API key tương ứng.
- **🤖 GPT-4: Extract Marketing Insights (`agent` & `lmChatOpenAi`):** Node AI trung tâm sử dụng model `gpt-4o` kết hợp với `LangChain Tools (for Agents)` để phân tích ngữ nghĩa và trích xuất các thông tin chiến lược.
- **📊 Parse: Format Insights for Output (`outputParserStructured`):** Đảm bảo đầu ra từ AI trả về đúng cấu trúc định dạng JSON mong muốn (marketing angles, motivations, frictions, product opportunities, VOC quotes).
- **📄 Google Sheets: Save Insights (`googleSheets`):** Cấu hình tài khoản `googleSheetsOAuth2Api`, chọn file Google Sheets và sheet tương ứng để lưu các insights đã được cấu trúc. Chọn thao tác `appendOrUpdate`.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (Test workflow) bằng cách điền form mẫu để kiểm tra dữ liệu trả về từ đầu đến cuối.
- Nếu không có lỗi xuất hiện, bật nút **Active** để chính thức đưa workflow vào vận hành tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Slack/Telegram:** Thêm node gửi thông báo về nhóm chat của công ty ngay sau khi GPT-4 phân tích xong insights mới.
- **Mở rộng nguồn dữ liệu:** Kết hợp thêm đánh giá từ Shopee, Lazada, hoặc TripAdvisor bên cạnh Google Reviews.
- **Tạo dashboard tự động:** Nối Google Sheets với Looker Studio để vẽ biểu đồ trực quan về tâm lý khách hàng theo thời gian.

### 📌 Kết luận
Việc thấu hiểu khách hàng chưa bao giờ dễ dàng và tự động hóa đến thế. Hãy cài đặt ngay workflow này để nâng cấp quy trình nghiên cứu thị trường của doanh nghiệp các sếp nhé!