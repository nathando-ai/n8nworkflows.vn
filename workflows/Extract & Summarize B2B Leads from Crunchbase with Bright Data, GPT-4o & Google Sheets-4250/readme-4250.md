---
title: "🚀 Trích xuất và Tóm tắt Lead B2B từ Crunchbase tự động với Bright Data, GPT-4o & Google Sheets"
description: "Hướng dẫn xây dựng workflow n8n tự động cào dữ liệu công ty tiềm năng từ Crunchbase bằng Bright Data, xử lý bằng GPT-4o và lưu trữ trực tiếp vào Google Sheets."
slug: "trich-xuat-tom-tat-lead-b2b-crunchbase-bright-data-gpt4o"
tags: [n8n, automation, no-code, sales, ai, brightdata, openai]
keywords: [n8n workflow, cào dữ liệu crunchbase, bright data, gpt-4o, google sheets, tự động hóa sales b2b]
---

# 🚀 Tự động hóa Trích xuất & Tóm tắt Lead B2B từ Crunchbase với AI

Các sếp làm trong ngành Sales và Growth chắc chắn đã thấm cảnh ngồi thủ công "cào" từng trang Crunchbase, copy-paste thông tin công ty, sau đó đọc lướt hàng đống chữ để tìm ra insight đắt giá. Việc này vừa mất thời gian, vừa dễ gây nhàm chán cho đội ngũ nhân sự.

Giải pháp ở đây là gì? Một hệ thống tự động hóa 100% không cần code (No-code) sử dụng **n8n**, kết hợp sức mạnh của **Bright Data Web Unlocker**, trí tuệ nhân tạo **GPT-4o (OpenAI)** và **Google Sheets**. Workflow này sẽ giúp các sếp tự động lấy thông tin từ Crunchbase, tóm tắt nội dung, cấu trúc hóa dữ liệu và lưu gọn gàng vào Google Sheets chỉ trong vài nốt nhạc!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 mà không lo gián đoạn, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không còn cảnh copy/paste thủ công từ Crunchbase.
- **Dữ liệu cấu trúc sạch sẽ:** GPT-4o tự động trích xuất các trường thông tin quan trọng thành dạng bảng gọn gàng.
- **Tóm tắt thông minh:** Nhanh chóng nắm bắt mô hình kinh doanh, gọi vốn và thông tin cốt lõi của công ty mục tiêu nhờ AI Summarization.
- **Đồng bộ hóa liền mạch:** Dữ liệu tự động đẩy thẳng vào Google Sheets và kích hoạt Webhook thông báo để đội ngũ Sales tiếp cận ngay lập tức.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài nguyên sau:
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Tài khoản Bright Data** (đã cấu hình Web Unlocker/Zone để cào dữ liệu Crunchbase).
- **OpenAI API Key** (để sử dụng các model GPT-4o-mini / GPT-4o cho việc trích xuất và tóm tắt).
- **Google Sheets** (tạo sẵn một file Google Sheets với các cột tương ứng để lưu thông tin Lead).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow này từ n8n.io (Link gốc: [Workflow #4250](https://n8n.io/workflows/4250)).
- Trong giao diện n8n Editor, bấm vào menu ở góc trên bên phải, chọn **Import from File** (hoặc copy toàn bộ JSON và dán thẳng vào workspace).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống chạy mượt mà, các sếp cần cấu hình chính xác các node sau:

- **Node `Set URL and Bright Data Zone`**: 
  - Điền chính xác URL trang công ty trên Crunchbase mà các sếp muốn cào.
  - Cấu hình Zone name và thông tin xác thực cho Bright Data.
- **Node `Perform Bright Data Web Request` (HTTP Request)**: 
  - Cài đặt `httpHeaderAuth` để kết nối thành công với API của Bright Data.
- **Các node OpenAI Chat Model (`OpenAI Chat Model`, `OpenAI Chat Model1`, `OpenAI Chat Model2`)**: 
  - Chọn credential `openAiApi` với API Key của các sếp. Đảm bảo model đang dùng là `gpt-4o-mini` (hoặc `gpt-4o` tùy nhu cầu tối ưu chi phí hay độ thông minh).
- **Node `Google Sheets`**: 
  - Kết nối tài khoản Google qua `googleSheetsOAuth2Api`.
  - Chọn đúng file Google Sheet và Sheet Name để node thực hiện thao tác `appendOrUpdate` (thêm mới hoặc cập nhật lead).
- **Node `Initiate a Webhook Notification for the extracted data`**: 
  - Thay đổi URL webhook thành điểm nhận thông báo của các sếp (có thể dùng Slack, Telegram hoặc Zapier/Make nếu muốn bắn thông báo lead mới về chat).

#### 3. Kích hoạt ⚡️
- Bấm **Test workflow** để chạy thử với dữ liệu mẫu từ Crunchbase.
- Kiểm tra kết quả trả về trong Google Sheets và các file log trên ổ đĩa (thông qua node `Write the summarized content to disk`).
- Nếu mọi thứ chạy trơn tru, hãy gạt công tắc sang **Active** để workflow sẵn sàng hoạt động tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Chatbot thông báo:** Nối thêm node Telegram hoặc Slack vào sau Webhook Notification để bắn thông báo "🎉 Có Lead B2B mới từ Crunchbase!" trực tiếp vào nhóm sales của công ty.
- **Mở rộng nguồn dữ liệu:** Không chỉ Crunchbase, các sếp có thể áp dụng cấu trúc Prompt tương tự để cào thêm thông tin từ LinkedIn Company Page hoặc Product Hunt.
- **Lưu lịch sử chạy:** Sử dụng thêm các node database như Supabase hoặc Airtable song song với Google Sheets để lưu trữ kho dữ liệu doanh nghiệp lớn hơn.

### 📌 Kết luận
Việc nghiên cứu thị trường và tìm kiếm khách hàng tiềm năng (B2B Lead Generation) chưa bao giờ dễ dàng đến thế khi kết hợp sức mạnh của Bright Data và AI trong n8n. Hãy cài đặt ngay workflow này để giải phóng thời gian cho đội ngũ sales và tăng tốc doanh số cho doanh nghiệp của các sếp!