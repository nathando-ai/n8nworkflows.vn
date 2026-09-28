---
title: "🚀 Tự động làm giàu dữ liệu khách hàng tiềm năng (Lead Enrichment) với Firecrawl, OpenRouter AI và Supabase"
description: "Hướng dẫn xây dựng workflow n8n tự động thu thập thông tin website, phân tích bằng AI và lưu trữ vào Supabase để tối ưu hóa quy trình Sales và Marketing."
slug: "tu-dong-lam-giau-du-lieu-khach-hang-firecrawl-openrouter-supabase"
tags: [n8n, automation, firecrawl, openrouter, supabase, lead-generation, ai]
keywords: [n8n workflow, lead enrichment, firecrawl, openrouter ai, supabase tự động hóa, crm data enrichment]
---

# 🚀 Tự động làm giàu dữ liệu khách hàng tiềm năng (Lead Enrichment) với Firecrawl, OpenRouter AI và Supabase

Các sếp trong ngành Sales và Marketing chắc chắn hiểu rõ nỗi đau: mỗi khi có một danh sách lead công ty mới, việc phải thủ công truy cập vào từng website, tìm hiểu xem công ty đó làm gì, mô hình kinh doanh ra sao, dùng công nghệ gì, có đang tuyển dụng hay gọi vốn không... ngốn rất nhiều thời gian và cực kỳ nhàm chán.

Chưa kể dữ liệu thu thập thường không đồng bộ, thiếu sót và chậm trễ khiến đội ngũ Sales mất đi "thời điểm vàng" để tiếp cận khách hàng.

Giải pháp đây rồi các sếp! Workflow n8n này sẽ tự động hóa **100%** quy trình trên: Nhận URL công ty 👉 Cào và tìm kiếm thông tin qua **Firecrawl** 👉 Dùng AI thông minh từ **OpenRouter (Claude)** phân tích tín hiệu kinh doanh 👉 Kiểm tra trùng lặp và lưu trữ gọn gàng vào **Supabase**. Tất cả diễn ra chỉ trong vài giây!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa toàn diện:** Biến một URL đơn thuần thành một bộ hồ sơ doanh nghiệp chi tiết (ngành nghề, mô hình giá, tech stack, vòng gọi vốn, tình trạng tuyển dụng...).
- **Tiết kiệm 95% thời gian:** Không còn cảnh nhân sự phải "lướt web" thủ công để soi thông tin khách hàng.
- **Dữ liệu chuẩn hóa & Sạch sẽ:** Kiểm tra trùng lặp tự động (Duplicate Check) qua Supabase trước khi lưu trữ, tránh rác dữ liệu.
- **Tích hợp API linh hoạt:** Nhận request qua Webhook và trả kết quả ngay lập tức cho các ứng dụng khác (CRM, Form, Telegram...).
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ TRƯỚC KHI "LÊN ĐỒ"]
- **n8n Instance:** Đã cài đặt n8n (bản cloud hoặc self-hosted).
- **Firecrawl API Key:** Dùng để cào dữ liệu website và tìm kiếm thông tin.
- **OpenRouter API Key:** Cung cấp mô hình AI (mặc định dùng `anthropic/claude-sonnet-4.6` siêu thông minh).
- **Supabase Project:** Cơ sở dữ liệu để lưu trữ thông tin lead đã được làm giàu.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Copy mã JSON của workflow này.
- Mở n8n Editor, chọn **Add workflow** -> **Import from JSON** và dán mã vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow hoạt động mượt mà, các sếp cần cấu hình các thành phần sau:

- **Node `Receive company URL` (Webhook):** Node này nhận request POST chứa URL. Các sếp hãy lấy Production/Test URL để gửi request mẫu dạng `{"url": "firecrawl.dev"}`.
- **Node `OpenRouter LLM`:** 
  - Chọn hoặc tạo mới **Credentials** cho OpenRouter bằng API Key của các sếp.
  - Cấu hình model (mặc định `anthropic/claude-sonnet-4.6` hoặc đổi sang model khác tùy ý).
- **Node `Scrape company website` & `Search company data` (Firecrawl):**
  - Thêm **Credentials** cho Firecrawl bằng API Key được cấp từ trang chủ Firecrawl.
- **Node `Check for duplicate in Supabase` & `Save enriched profile to Supabase`:**
  - Thêm **Credentials** Supabase (bao gồm URL và Service Role Key).
  - Trước khi chạy, các sếp nhớ tạo bảng `lead_enrichment` trong Supabase bằng câu lệnh SQL migration để hệ thống tự động lưu trữ và quản lý thời gian (`timestamps`).

#### 3. Kích hoạt ⚡️
- Gửi một request thử nghiệm bằng Postman, cURL hoặc công cụ test HTTP với body: `{"url": "firecrawl.dev"}` tới Webhook URL.
- Kiểm tra kết quả trả về từ node `Return enriched profile`.
- Nếu mọi thứ xanh đèn (Success), các sếp gạt công tắc sang **Active** để đưa vào vận hành thực tế!

### ✍️ Mẹo & gợi ý nâng cao
Để tối ưu hóa quy trình kinh doanh, các sếp có thể mở rộng workflow này bằng các cách sau:
1. **Bắn thông báo về Telegram/Slack:** Thêm một node Telegram ngay sau bước lưu Supabase để báo cho đội Sales ngay khi có một Lead "khủng" vừa được phân tích xong.
2. **Tự động đẩy vào CRM:** Kết nối trực tiếp kết quả cấu trúc từ AI vào HubSpot, Salesforce hoặc Google Sheets.
3. **Lên lịch quét hàng loạt (Batch Processing):** Thay vì nhận từng URL qua Webhook, các sếp có thể kết nối với một Google Sheets chứa danh sách hàng trăm website để workflow tự động quét định kỳ.

### 📌 Kết luận
Workflow **Enrich company leads with Firecrawl, OpenRouter AI, and Supabase** là một vũ khí cực kỳ mạnh mẽ giúp tự động hóa khâu nghiên cứu khách hàng (Research/Prospecting). Hãy cài đặt ngay hôm nay để giải phóng sức lao động cho đội ngũ Sales và chốt deal nhanh hơn các đối thủ!