---
title: "🚀 Tự động quét thông tin doanh nghiệp & trích xuất email với n8n, SerpAPI, Apify và GPT-4o"
description: "Hướng dẫn xây dựng workflow n8n tự động tìm kiếm danh bạ doanh nghiệp địa phương qua Google Maps, cào website bằng Apify và dùng GPT-4o trích xuất email chuyên nghiệp."
slug: "tu-dong-quet-thong-tin-doanh-nghiep-email-n8n"
tags: [n8n, automation, lead-generation, gpt-4o, serpapi, apify, google-sheets]
keywords: [n8n workflow, cào dữ liệu doanh nghiệp, tìm kiếm khách hàng tiềm năng, trích xuất email tự động, serpapi google maps, apify web scraper]
---

# 🚀 Tự động quét thông tin doanh nghiệp & trích xuất email với n8n, SerpAPI, Apify và GPT-4o

Việc tìm kiếm khách hàng tiềm năng (Lead Generation) theo cách thủ công như lướt Google Maps, vào từng website copy email thực sự là một cơn ác mộng tốn kém thời gian và nhân lực. Các sếp có bao giờ tự hỏi liệu mình có thể tự động hóa 100% quy trình này không?

Câu trả lời là **CÓ!** Workflow n8n đỉnh cao được thiết kế bởi chuyên gia Robert Breen sẽ giúp các sếp quét sạch thông tin doanh nghiệp địa phương, cào nội dung website và sử dụng AI (GPT-4o) để trích xuất email chính xác, sau đó tự động lưu toàn bộ vào Google Sheets mà không cần động tay chân.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa toàn diện:** Quét từ từ khóa tìm kiếm trên Google Sheet đến khi ra được kết quả email doanh nghiệp.
- **Dữ liệu chất lượng cao:** Kết hợp SerpAPI (Google Maps) lấy thông tin chuẩn xác và Apify cào sâu vào website doanh nghiệp.
- **Sức mạnh AI (GPT-4o-mini):** Đọc hiểu nội dung website phức tạp để bóc tách chính xác địa chỉ email liên hệ.
- **Lưu trữ đồng bộ:** Tự động ghi nhận kết quả vào Google Sheets và đánh dấu trạng thái hoàn thành để tránh lặp dữ liệu.
:::

### Yêu cầu cần thiết
:::info[CHUẨN BỊ TRƯỚC KHI BẮT ĐẦU]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Google Sheets:** Tài khoản Google để kết nối và quản lý danh sách từ khóa/kết quả.
- **SerpAPI Account:** Lấy API key tìm kiếm Google Maps (`serpApi`).
- **Apify Account:** Lấy API key cào dữ liệu website (`httpQueryAuth`).
- **OpenAI API Key:** Sử dụng cho các node LangChain và GPT-4o-mini (`openAiApi`).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Copy toàn bộ mã JSON của workflow này, vào giao diện n8n của các sếp, chọn **Add workflow** -> **Import from JSON** và dán vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình các bước sau:

- **Chuẩn bị Google Sheet:** 
  Sao chép bảng mẫu của tác giả vào Google Drive cá nhân tại [Google Sheets Template](https://docs.google.com/spreadsheets/d/1QgcVMlXRlM_5ZFFUHr6bVK-93Tzia9XseTX03ZYnowI/edit?usp=sharing).
- **Cấu hình Google Sheets Nodes:**
  - Ở node `Extract Search Terms` và `Save Emails to Sheet` (và `Mark Row as Completed`), kết nối tài khoản qua `Google Sheets OAuth2 API`. Trỏ đường dẫn đến file Google Sheet vừa copy và chọn đúng tên Tab (`Searches` và `Results`).
- **Cấu hình SerpAPI (`Search Google Maps` Node):**
  - Đăng ký tài khoản tại [SerpAPI Dashboard](https://serpapi.com/dashboard) lấy API Key.
  - Tạo credential mới dạng `serpApi` trong node `Search Google Maps`.
- **Cấu hình Apify Crawler (`Scrape Web Page` Node):**
  - Đăng ký tài khoản [Apify](https://apify.com), thêm Actor *Fast Website Content Crawler* vào tài khoản.
  - Tại node HTTP Request `Scrape Web Page`, thêm token Apify vào dạng query parameter (`token=YOUR_API_KEY`) với loại credential `httpQueryAuth`.
- **Cấu hình OpenAI (`OpenAI Chat Model` & `Extract Email - AI Agent` Nodes):**
  - Nhập OpenAI API Key vào credentials `openAiApi` để mô hình `gpt-4o-mini` và Structured Output Parser hoạt động chính xác.

#### 3. Kích hoạt ⚡️
- Nhấn nút **"Execute Workflow"** để test thử với 1-2 dòng từ khóa mẫu.
- Kiểm tra kết quả hiển thị ở Tab `Results` trên Google Sheet.
- Nếu mọi thứ ổn thỏa, bật công tắc **Active** để workflow tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Nối thêm node Telegram hoặc Slack sau bước `Save Emails to Sheet` để nhận thông báo ngay lập tức mỗi khi quét xong một danh sách doanh nghiệp.
- **Lọc trùng lặp tự động:** Thêm một bước kiểm tra email trước khi lưu vào Google Sheets để tránh lưu trùng lặp khách hàng cũ.
- **Mở rộng chiến dịch:** Thiết lập lịch chạy định kỳ (Schedule Trigger) thay vì bấm tay thủ công để nuôi phễu data đều đặn mỗi tuần.

### 📌 Kết luận
Workflow này là một "vũ khí tối tân" giúp tối ưu hóa 90% thời gian tìm kiếm khách hàng B2B. Hãy cài đặt ngay hôm nay để đội ngũ sales của các sếp có một nguồn leads chất lượng, tự động và cực kỳ hiệu quả!