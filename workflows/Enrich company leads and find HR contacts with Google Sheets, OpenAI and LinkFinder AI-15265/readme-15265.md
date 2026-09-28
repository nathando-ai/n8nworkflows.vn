---
title: "🚀 Tự động hóa Enrich Lead công ty và tìm kiếm thông tin nhân sự HR với n8n, OpenAI & Google Sheets"
description: "Xây dựng hệ thống tự động hóa 100% giúp thu thập dữ liệu doanh nghiệp, phân loại bằng AI, tìm kiếm domain website và khai thác thông tin liên hệ HR chuẩn xác từ Google Sheets."
slug: "tu-dong-hoa-enrich-lead-cong-ty-va-tim-hr-voi-n8n"
tags: [n8n, automation, lead-generation, open-ai, google-sheets, web-scraping]
keywords: [n8n workflow, enrich lead công ty, tìm kiếm HR, tự động hóa lead generation, OpenAI n8n, Firecrawl Apify]
---

# 🚀 Tự động hóa Enrich Lead công ty và tìm kiếm thông tin nhân sự HR với n8n, OpenAI & Google Sheets

Việc tìm kiếm, phân loại và làm giàu dữ liệu khách hàng tiềm năng (lead enrichment) cùng việc săn tìm thông tin liên hệ của bộ phận Nhân sự (HR) theo cách thủ công thường tốn hàng tá thời gian, dễ xảy ra sai sót và cực kỳ nhàm chán cho đội ngũ Sales & Marketing. 

Bài viết này sẽ hướng dẫn các sếp triển khai một workflow n8n cực kỳ mạnh mẽ gồm 45 nodes, hoạt động như một cỗ máy tự động hoàn toàn: đọc danh sách từ Google Sheets, sử dụng AI để phân tích domain và loại hình doanh nghiệp, cào dữ liệu website (Web Scraping) bằng Firecrawl/Apify, sau đó lọc ra các thông tin liên hệ HR chất lượng cao rồi lưu ngược lại Google Sheets. Không cần viết code phức tạp, tự động hóa 100%!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa toàn diện quy trình Lead Generation**: Từ danh sách thô (chỉ có tên hoặc email), hệ thống tự động tìm ra website, phân loại doanh nghiệp (Employer hay Agency).
- **Khai thác thông tin nhân sự (HR Contacts) chính xác**: Tìm kiếm và chọn lọc các liên hệ HR cấp cao, trích xuất email và profile LinkedIn tự động.
- **Đồng bộ dữ liệu Real-time**: Mọi thông tin sau khi được làm giàu (enrichment) sẽ được cập nhật và phân loại trực tiếp vào Google Sheets một cách ngăn nắp.
- **Tiết kiệm 90% thời gian thủ công**: Đội ngũ Sales chỉ việc nhận danh sách lead đã "sạch" và sẵn sàng outreach.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance**: Đã cài đặt n8n (Self-hosted hoặc n8n Cloud).
- **Google Sheets account**: Tài khoản Google chứa file Google Sheets quản lý lead.
- **OpenAI API Key**: Dùng cho các node `AI Classifier for Type`, `AI Select Top Contacts` để phân loại và chọn lọc thông tin.
- **Firecrawl API Key / Apify Account**: Dùng cho việc cào dữ liệu website và actors (`Initiate Firecrawl Scraping`, `Fetch Actor Dataset 4`, v.v.).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này từ nguồn gốc hoặc copy trực tiếp mã JSON, sau đó paste vào giao diện n8n Editor của các sếp qua tính năng **Import from Clipboard**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow sở hữu tới 45 nodes, tuy nhiên các sếp chỉ cần tập trung cấu hình kỹ các nhóm node cốt lõi sau:
- **Google Sheets Nodes (`Read Google Sheet Rows`, `Update with Company Domain`, `Save Contact with Email`, v.v.)**: 
  - Kết nối tài khoản Google thông qua **Google Sheets OAuth2 API**.
  - Trỏ đúng đến file Spreadsheet ID và Sheet Name chứa danh sách lead của các sếp.
- **OpenAI Nodes (`AI Classifier for Type`, `AI Select Top Contacts`)**: 
  - Thêm OpenAI Credentials và chọn model phù hợp (khuyên dùng `gpt-4o-mini` hoặc `gpt-4o` để đạt độ chính xác cao khi phân loại text và chọn contact).
- **Scraping Nodes (`Initiate Firecrawl Scraping`, `Fetch Actor Dataset 4`, `Fetch Actor Dataset 6`)**: 
  - Đảm bảo các API Key của Firecrawl và Apify đã được điền chính xác để không bị lỗi khi cào dữ liệu website và thông tin nhân sự.
- **Các node xử lý logic (`Clean Extracted Text`, `Parse AI Classification`, `Process Selected Contacts`, v.v.)**: Các đoạn mã JavaScript đã được viết sẵn để làm sạch chuỗi, các sếp không cần chỉnh sửa gì trừ khi muốn thay đổi cấu trúc dữ liệu trả ra.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** thông qua `Manual Execution Trigger` để chạy thử với vài dòng dữ liệu mẫu trong Google Sheets.
- Kiểm tra kết quả trả về trong Google Sheets xem các cột domain, trạng thái employer/agency, và thông tin HR đã được điền đầy đủ chưa.
- Sau khi test thành công, bật nút **Active** ở góc trên cùng bên phải để workflow tự động hoạt động ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp kênh thông báo**: Thêm node Telegram hoặc Slack ở cuối workflow để bắn thông báo ngay về nhóm chat mỗi khi hệ thống "enrich" thành công một batch lead mới.
- **Lưu log lỗi (Error Handling)**: Bổ sung nhánh Error Trigger để bắt các lỗi API (như lỗi kết nối OpenAI hoặc Firecrawl quá hạn mức) và ghi nhận vào một sheet riêng biệt để dễ kiểm tra.
- **Tự động hóa theo lịch**: Thay vì chỉ dùng Manual Trigger, các sếp có thể kết hợp thêm node **Schedule Trigger** để hệ thống tự động quét và làm giàu lead mới định kỳ mỗi ngày hoặc mỗi tuần.

### 📌 Kết luận
Workflow "Enrich company leads and find HR contacts" là một giải pháp tự động hóa đỉnh cao giúp tối ưu hóa toàn bộ phễu khai thác khách hàng tiềm năng. Áp dụng ngay hệ thống này để đội ngũ của các sếp có ngay nguồn dữ liệu sạch, chất lượng và chốt deal hiệu quả hơn!