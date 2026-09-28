---
title: "🚀 Tự động khám phá và lưu trữ nội dung ngách từ web với Kagi và OpenRouter AI"
description: "Hướng dẫn xây dựng workflow n8n tự động tìm kiếm nội dung ngách bằng Kagi API, phân loại và chấm điểm bằng AI qua OpenRouter, sau đó lưu kết quả vào Google Sheets."
slug: "tu-dong-kham-pha-va-luu-tru-noi-dung-ngach-voi-kagi-va-ai"
tags: [n8n, automation, no-code, kagi, openrouter, google-sheets, ai-summarization]
keywords: [n8n workflow, tu dong hoa, kagi api, openrouter ai, google sheets automation, market research]
---

# 🚀 Tự động khám phá và lưu trữ nội dung ngách từ web với Kagi và OpenRouter AI

Các sếp đang làm nghiên cứu thị trường (Market Research) hoặc tổng hợp tin tức ngách chắc hẳn rất ngán ngẩm cảnh phải tìm kiếm thủ công hàng giờ trên Google, sau đó copy từng đường link, đọc lướt nội dung, phân loại rồi nhập tay vào bảng Excel/Google Sheets. Công việc lặp đi lặp lại này không chỉ tốn thời gian mà còn dễ gây mệt mỏi, sót thông tin quan trọng.

Giải pháp ở đây là gì? Workflow n8n này sẽ tự động hóa **100%** quy trình trên: Nhận yêu cầu qua Webhook, sử dụng công cụ tìm kiếm thông minh Kagi để khai thác dữ liệu web ngách, giao cho OpenRouter AI phân tích, chấm điểm, phân loại, rồi tự động đổ dữ liệu sạch sẽ vào Google Sheets. Các sếp chỉ việc ngồi thụ hưởng kết quả!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa toàn diện:** Biến một chuỗi các thao tác tìm kiếm, đọc hiểu, phân loại và lưu trữ thủ công thành một cú "click" hoặc gọi API tự động.
- **Dữ liệu chất lượng cao:** Tận dụng Kagi Enrich API để đào sâu các nguồn thông tin ngách ít bị bão hòa SEO hơn Google truyền thống.
- **AI thông minh hóa:** OpenRouter AI (với các mô hình mạnh mẽ) tự động đọc, tóm tắt, chấm điểm mức độ tiềm năng và phân loại nội dung chính xác.
- **Đồng bộ thời gian thực:** Kết quả được lưu trực tiếp vào Google Sheets kèm thông báo phản hồi ngược lại cho Webhook caller.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài nguyên sau:
1. **n8n Instance:** Đã cài đặt sẵn sàng (Self-hosted hoặc n8n Cloud).
2. **Kagi API Token:** Tài khoản Kagi có quyền truy cập API tìm kiếm (Enrich endpoint).
3. **OpenRouter API Key:** Tài khoản OpenRouter để sử dụng các mô hình ngôn ngữ lớn (LLM).
4. **Google Sheets:** Tạo sẵn một file Google Sheet với các cột tương ứng để lưu thông tin (Tiêu đề, URL, Điểm số, Phân loại, Tóm tắt...).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow này và dán trực tiếp vào n8n Editor của mình, hoặc import file JSON theo cách thông thường.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này bao gồm 10 nodes phối hợp nhịp nhàng. Các sếp cần chú ý cấu hình kỹ các điểm sau:
- **Small Web Discovery Trigger (Webhook Node):** Lấy URL Webhook được sinh ra để cấu hình cho hệ thống bên ngoài gọi vào kích hoạt workflow.
- **Set Kagi API Token (Set Node):** Điền `Kagi API Token` của các sếp vào tham số của node này (hoặc cấu hình qua Credentials nếu muốn bảo mật tốt hơn).
- **GET Kagi Enrich Web Data (HTTP Request Node):** Kiểm tra lại Endpoint gọi tới Kagi API đảm bảo đã đúng định dạng yêu cầu.
- **OpenRouter Chat Model (OpenRouter Node):** Chọn credentials `openRouterApi` và chọn model phù hợp (mặc định cấu hình sẵn `openai/gpt-oss-120b:free` hoặc thay bằng model tùy ý các sếp).
- **AI Categorize and Score Content (Agent Node):** Tinh chỉnh System Prompt bên trong agent nếu các sếp muốn thay đổi tiêu chí chấm điểm, cách phân loại hoặc định dạng nội dung đầu ra.
- **Append Content Row to Sheets (Google Sheets Node):** Kết nối tài khoản Google thông qua OAuth2, sau đó chọn đúng file Spreadsheet và Worksheet mục tiêu, map các trường dữ liệu từ node `Merge AI Output with Metadata` vào các cột tương ứng.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** và gửi một request thử nghiệm mẫu đến Webhook để kiểm tra luồng chạy.
- Sau khi test thành công, gạt công tắc sang **Active** để workflow chính thức đi vào vận hành tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Nối thêm node Telegram hoặc Slack sau bước ghi dữ liệu vào Google Sheets để bắn tin nhắn cảnh báo ngay lập tức khi có nội dung ngách điểm số cao xuất hiện.
- **Mở rộng xử lý hàng loạt:** Tăng số lượng item xử lý trong node `Loop Over Enrich Results` (`splitInBatches`) nếu nguồn dữ liệu trả về từ Kagi lớn.
- **Lưu trữ backup:** Kết thêm node lưu vào Airtable hoặc Notion song song với Google Sheets để đa dạng hóa kho lưu trữ tri thức.

### 📌 Kết luận
Workflow "Discover and save niche web content to Google Sheets with Kagi and OpenRouter AI" là một thứ vũ khí cực kỳ lợi hại cho các nhà sáng tạo nội dung, nghiên cứu thị trường và các marketer muốn đón đầu xu hướng ngách. Hãy cài đặt ngay hôm nay để tối ưu hóa hàng giờ làm việc thủ công của các sếp!