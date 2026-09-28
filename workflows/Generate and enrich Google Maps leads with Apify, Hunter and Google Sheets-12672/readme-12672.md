---
title: "🚀 Tự động quét Lead Google Maps, lọc trùng, tìm Email qua Hunter và Báo cáo qua Gmail với n8n"
description: "Xây dựng hệ thống tự động tìm kiếm khách hàng tiềm năng từ Google Maps, làm giàu dữ liệu bằng Hunter, lưu trữ vào Google Sheets và gửi báo cáo qua Gmail mỗi ngày."
slug: "tu-dong-quet-lead-google-maps-hunter-gmail-n8n"
tags: [n8n, automation, no-code, lead-generation, apify, hunter, google-sheets]
keywords: [n8n workflow, quét lead google maps, apify google maps scraper, hunter email enrichment, tự động hóa sales]
---

# 🚀 Tự động quét Lead Google Maps, lọc trùng và báo cáo qua Gmail với n8n

Các sếp có đang tốn hàng giờ mỗi ngày để tìm kiếm khách hàng tiềm năng thủ công trên Google Maps, copy số điện thoại, tìm email từng doanh nghiệp rồi nhập vào Google Sheets không? Việc này vừa mất thời gian, dễ sai sót lại vừa lãng phí nguồn nhân lực quý giá cho các công việc chốt sale giá trị cao.

Bài viết này sẽ hướng dẫn các sếp triển khai một hệ thống tự động hóa hoàn chỉnh (được phát triển bởi chuyên gia Avkash Kakdiya) giúp quét sạch data khách hàng từ Google Maps, tự động lọc trùng với dữ liệu cũ, làm giàu thông tin liên hệ bằng Hunter (tìm email doanh nghiệp), phân loại mức độ uy tín, lưu trữ gọn gàng vào Google Sheets và gửi báo cáo HTML chi tiết qua Gmail mỗi ngày!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 mà không lo sập nguồn hay gián đoạn quá trình quét lead, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Hệ thống tự động chạy theo lịch trình (Schedule Trigger) mỗi ngày mà không cần chạm tay vào.
- **Dữ liệu sạch & Không trùng lặp:** Node `Deduplicate Leads1` tự động đối chiếu với Google Sheets để loại bỏ các doanh nghiệp đã từng quét trước đó.
- **Làm giàu thông tin (Email Enrichment):** Kết hợp với Hunter API để tìm kiếm và xác thực email doanh nghiệp, chấm điểm độ tin cậy (High, Medium, Low confidence).
- **Báo cáo trực quan:** Tổng hợp kết quả thành một bản báo cáo HTML chuyên nghiệp gửi thẳng vào Gmail cá nhân/đội ngũ sales.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản và API sau:
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Apify Account & API Key:** Dùng cho node `Google Maps Scraper` để trích xuất dữ liệu doanh nghiệp.
- **Hunter.io Account & API Key:** Dùng cho node `HTTP Request1` để tìm kiếm email theo tên miền doanh nghiệp.
- **Google Sheets:** Tạo sẵn một file Google Sheets để lưu trữ danh sách lead.
- **Gmail Account:** Kết nối OAuth2 với n8n để gửi email báo cáo và thông báo lỗi.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow (từ nguồn n.8n.io/workflows/12672) và paste trực tiếp vào giao diện n8n Editor của mình, hoặc tải file JSON về và import qua menu **Add workflow > Import from File**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình chính xác các node sau:
- **Schedule Trigger1:** Cài đặt tần suất chạy mong muốn (ví dụ: Chạy 1 lần/ngày vào lúc 8 giờ sáng).
- **Check Existing Leads1 & Save to Google Sheets:** Kết nối tài khoản Google của sếp, chọn đúng file Google Sheets và Sheet Name dùng để lưu trữ thông tin lead (Node `Save to Google Sheets` được cấu hình ở chế độ `appendOrUpdate`).
- **Google Maps Scraper (HTTP Request):** Điền Apify API Key của sếp vào phần header/auth, sau đó tùy chỉnh từ khóa tìm kiếm (`search query`) và khu vực (`location`) phù hợp với thị trường mục tiêu.
- **HTTP Request1:** Cấu hình gọi API tới Hunter.io bằng cách điền Hunter API Key để thực hiện trích xuất email dựa trên website của doanh nghiệp vừa quét được.
- **Send Email Report1 & Error Notification1 & No New Leads Notification1:** Kết nối credential Gmail của sếp và điền địa chỉ email nhận báo cáo.

#### 3. Kích hoạt ⚡️
- Bấm nút **Execute Workflow** chạy thủ công lần đầu để test toàn bộ dữ liệu mẫu và kiểm tra kết nối API.
- Nếu không có lỗi xuất hiện, hãy gạt công tắc **Active** ở góc trên cùng bên phải để hệ thống tự động chạy ngầm 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Chatbot:** Thay vì chỉ gửi email qua Gmail, các sếp có thể gắn thêm node Telegram hoặc Slack để bắn thông báo ngay lập tức về điện thoại khi có lead mới thuộc nhóm "High Confidence".
- **AI Scoring:** Kết hợp thêm OpenAI node để phân tích mô tả doanh nghiệp và chấm điểm mức độ tiềm năng (Lead Scoring) sâu hơn dựa trên AI.
- **Lưu log lỗi:** Sử dụng nhánh `Error Notification1` để kết nối vào một kênh riêng (ví dụ Google Sheets Tab Log) nhằm theo dõi các trường hợp API bị lỗi hoặc hết quota.

### 📌 Kết luận
Workflow "Generate and enrich Google Maps leads with Apify, Hunter and Google Sheets" là một cỗ máy tự động hoàn hảo giúp các doanh nghiệp agency, startup và đội ngũ sales tối ưu hóa phễu tìm kiếm khách hàng. Hãy triển khai ngay hôm nay để giải phóng thời gian và gia tăng doanh số cùng n8n!