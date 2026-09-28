---
title: "🚀 Tự Động Viết Nháp Bản Tin AI Từ Google Sheets Lên Notion Với GPT-5-Mini"
description: "Hướng dẫn chi tiết workflow n8n tự động hóa quy trình tổng hợp chủ đề từ Google Sheets, sử dụng AI Agent với GPT-5-mini để viết bản tin chất lượng và lưu trữ trực tiếp vào Notion."
slug: "tu-dong-viet-nhap-ban-tin-ai-tu-google-sheets-len-notion-gpt-5-mini"
tags: [n8n, automation, no-code, openai, google-sheets, notion, content-creation]
keywords: [n8n workflow, tự động hóa bản tin, AI Agent viết content, Google Sheets to Notion, GPT-5-mini n8n]
---

# 🚀 Tự Động Viết Nháp Bản Tin AI Từ Google Sheets Lên Notion Với GPT-5-Mini

Các sếp làm nội dung hay Digital Marketer chắc chắn đều hiểu cảm giác "bí từ" và tốn hàng giờ liền mỗi tuần để lên ý tưởng, viết nháp và biên tập các bản tin (newsletter) gửi khách hàng. Việc gom nhặt chủ đề từ Google Sheets rồi chuyển thủ công qua Notion để chỉnh sửa cực kỳ mất thời gian và dễ đứt gãy mạch sáng tạo.

Giải pháp là gì? Workflow n8n này sẽ tự động hóa toàn bộ quy trình: Đọc danh sách chủ đề từ **Google Sheets**, giao việc cho **AI Agent (sử dụng GPT-5-mini)** viết nội dung hoàn chỉnh, sau đó tự động tạo trang nháp (Draft Page) trên **Notion** và cập nhật lại trạng thái trong Google Sheets. 100% tự động, không cần tốn một giọt mồ hôi thủ công nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80% thời gian:** Không còn cảnh copy-paste thủ công từ bảng tính sang công cụ soạn thảo.
- **Nội dung sắc sảo, thông minh:** Ứng dụng sức mạnh của GPT-5-mini thông qua AI Agent giúp biến các tiêu đề thô thành bài viết nháp chi tiết, chuyên nghiệp.
- **Đồng bộ hóa mượt mà:** Tự động tạo trang Notion kèm nội dung và đánh dấu trạng thái "Đã xử lý" ngay trong Google Sheets.
- **Hoạt động linh hoạt:** Dễ dàng chạy thử thủ công hoặc mở rộng tích hợp trigger định kỳ hàng tuần.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Tài khoản OpenAI API** (Có quyền truy cập mô hình `gpt-5-mini`).
- **Google Sheets** (File chứa danh sách các chủ đề / ý tưởng bản tin).
- **Notion Account & Database** (Nơi lưu trữ các bản nháp newsletter được tạo tự động).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow (từ nguồn n8n.io/workflows/7848) và dán trực tiếp vào n8n Editor của mình, hoặc sử dụng tính năng import file JSON.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống chạy trơn tru, các sếp cần cấu hình chính xác các node trọng điểm sau:

- **Get row(s) in sheet & Update row in sheet (Google Sheets Nodes):**
  - Kết nối tài khoản Google thông qua `googleSheetsOAuth2Api`.
  - Chọn đúng file Spreadsheet và Sheet chứa danh sách chủ đề bản tin của các sếp.
- **OpenAI Chat Model & AI Agent:**
  - Kết nối credentials `openAiApi` với API Key của các sếp.
  - Kiểm tra thông số model tại `OpenAI Chat Model` đảm bảo đang chọn `gpt-5-mini` đúng như thiết kế gốc.
- **Loop Over Items (`splitInBatches`):**
  - Node này giúp xử lý từng dòng dữ liệu trong Google Sheets một cách tuần tự, tránh tình trạng gọi API quá tải (Rate limit).
- **Create Page & UpdateNotionBlock (Notion Nodes & HTTP Request):**
  - Kết nối credentials `notionApi` bằng cách tạo một Notion Integration và chia sẻ quyền truy cập với Database đích.
  - Map các trường dữ liệu đầu ra từ AI Agent vào các thuộc tính (Properties) của trang Notion (Tiêu đề, Nội dung, Trạng thái...).

#### 3. Kích hoạt ⚡️
- Nhấn nút **Execute Workflow** tại node `When clicking ‘Execute workflow’` để test chạy thử với một vài dòng dữ liệu mẫu đầu tiên.
- Kiểm tra kết quả trên Notion và Google Sheets xem dữ liệu đã đồng bộ chuẩn chỉnh chưa.
- Sau khi kiểm tra mọi thứ hoàn hảo, bật nút **Active** để workflow chính thức đi vào vận hành tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Thêm Trigger tự động:** Thay vì dùng `Manual Trigger`, các sếp có thể đổi thành `Schedule Trigger` để n8n tự động quét Google Sheets và viết bài nháp vào mỗi sáng thứ Hai hàng tuần.
- **Thông báo qua Telegram/Slack:** Thêm một node Telegram hoặc Slack ở cuối workflow để bắn thông báo: *"Đã viết xong bản tin tuần này, mời sếp vào Notion duyệt!"*.
- **Tùy chỉnh System Prompt:** Trong `AI Agent`, các sếp có thể tùy biến lại văn phong (Tone of voice) cho phù hợp với thương hiệu cá nhân hoặc doanh nghiệp của mình.

### 📌 Kết luận
Việc tự động hóa quy trình sản xuất nội dung chưa bao giờ dễ dàng đến thế với sự kết hợp của n8n, Google Sheets, Notion và AI Agent. Hãy thiết lập ngay hôm nay để giải phóng thời gian sáng tạo và tối ưu hóa hiệu suất làm việc của các sếp!