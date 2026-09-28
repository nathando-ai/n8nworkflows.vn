---
title: "🚀 Tự động tìm kiếm và làm giàu số điện thoại doanh nghiệp vào Airtable với Firecrawl, Claude AI và Apify"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa tìm kiếm số điện thoại công ty từ Website, LinkedIn, Google Maps và Claude AI, sau đó cập nhật trực tiếp vào Airtable."
slug: "tu-dong-tim-kiem-so-dien-thoai-doanh-nghiep-airtable-claude-ai"
tags: [n8n, automation, airtable, claude-ai, lead-generation, apify]
keywords: [n8n workflow, tự động hóa airtable, tìm số điện thoại doanh nghiệp, claude ai, firecrawl, apify linkedin scraper]
---

# 🚀 Tự động hóa tìm kiếm & làm giàu số điện thoại doanh nghiệp vào Airtable

Các sếp có đang đau đầu vì đội ngũ sales phải mất hàng giờ đồng hồ lướt web, lục lọi LinkedIn hay Google Maps chỉ để tìm một số điện thoại công ty đưa vào CRM (Airtable)? Công việc thủ công này không chỉ nhàm chán, tốn thời gian mà còn dễ bỏ sót khách hàng tiềm năng.

Đừng lo, bài toán này sẽ được giải quyết triệt để với workflow n8n **"Enrich Airtable company phones from website, LinkedIn, Google Maps, and Claude"** do chuyên gia Allan Vaccarizi thiết kế. Đây là giải pháp tự động hóa 100% không cần code, kết hợp sức mạnh của Web Scraping, AI thông minh (Claude Sonnet) và các kênh dữ liệu lớn để tìm kiếm số điện thoại cho doanh nghiệp một cách tự động.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Tự động hóa hoàn toàn quy trình tìm kiếm số điện thoại từ nhiều nguồn khác nhau mà không cần nhân sự làm thủ công.
- **Tỷ lệ thành công cao (Multi-layer Fallback):** Quét từ Website qua Firecrawl và Claude AI trước; nếu không thấy sẽ tự động chuyển sang LinkedIn và Google Maps qua Apify.
- **Đồng bộ dữ liệu thời gian thực:** Kết quả tìm được (hoặc không tìm thấy) sẽ được cập nhật tự động ngay lập tức vào Airtable của các sếp.
- **Hoạt động không mệt mỏi:** Xử lý danh sách hàng loạt (loop qua từng bản ghi) một cách mượt mà và chuẩn xác.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow này "lên đồ" và chạy mượt mà, các sếp cần chuẩn bị sẵn các tài khoản và API keys sau:
- **n8n Instance** (Cloud hoặc Self-hosted).
- **Tài khoản Airtable** kèm theo Base/Table chứa danh sách công ty cần làm giàu dữ liệu.
- **Firecrawl API Key** (Dùng để scrape nội dung website công ty).
- **Anthropic API Key** (Dùng cho mô hình Claude Sonnet phân tích dữ liệu).
- **Apify API Token** (Dùng để chạy các actor cào dữ liệu từ LinkedIn và Google Maps).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow từ nguồn cấp, sau đó vào giao diện n8n chọn **Add workflow** -> **Import from File** (hoặc copy toàn bộ JSON và dán trực tiếp vào n8n Editor).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, các sếp cần cấu hình lại các node cốt lõi sau đây để khớp với hệ thống của mình:

- **Search Airtable Records, Update Airtable Phone Found, Update Airtable Phone Not Found (Node Airtable):** Kết nối với tài khoản Airtable của các sếp (`airtableTokenApi`), sau đó chọn đúng Base và Table chứa thông tin công ty.
- **Scrape Company Website (Node Firecrawl):** Thêm Firecrawl API Key (`firecrawlApi`) để cho phép node tiến hành cào dữ liệu trang web.
- **Claude Sonnet Model (Node lmChatAnthropic):** Thêm Anthropic API Key (`anthropicApi`) và cấu hình mô hình `Claude Sonnet` (hoặc phiên bản tương đương).
- **Fetch LinkedIn Phone via Apify & Fetch Google Maps Phone via Apify (Node HTTP Request):** Thêm Apify API Token (`apifyApi`) để gọi các Actor chuyên dụng cào dữ liệu từ LinkedIn và Google Maps khi Website không có kết quả.
- **Clean Scraped Markdown & Refine and Merge Phone Data (Node Code):** Kiểm tra lại tên các trường dữ liệu (field names) trong code JavaScript sao cho trùng khớp hoàn toàn với schema của bảng Airtable nhà các sếp.
- **Các node điều kiện (If AI Found Phone, If LinkedIn Phone Found, If Company Exists in LinkedIn, If Google Maps Phone Found):** Kiểm tra lại đường dẫn dữ liệu (field paths) trả về từ các API để đảm bảo logic nhánh chạy chính xác.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** chạy thử với một vài bản ghi mẫu từ node `When Workflow Runs Manually` để kiểm tra toàn bộ luồng dữ liệu.
- Sau khi test thành công và dữ liệu đổ về Airtable chuẩn chỉnh, các sếp bật công tắc **Active** góc trên bên phải để workflow sẵn sàng hoạt động tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng nguồn dữ liệu:** Các sếp có thể tích hợp thêm các công cụ tìm kiếm email hoặc mạng xã hội khác bằng cách nối thêm các nhánh API tương tự sau bước AI.
- **Tích hợp thông báo:** Thêm node **Slack** hoặc **Telegram** vào cuối luồng để nhận thông báo tổng kết mỗi khi workflow quét xong một batch hoặc khi tìm được số điện thoại chất lượng cao.
- **Tự động hóa theo lịch:** Thay thế node `When Workflow Runs Manually` bằng node `Schedule Trigger` để n8n tự động quét Airtable định kỳ mỗi ngày hoặc mỗi tuần.

### 📌 Kết luận
Tự động hóa tìm kiếm thông tin liên hệ chưa bao giờ dễ dàng đến thế với sự kết hợp đỉnh cao giữa n8n, Firecrawl, Claude AI và Apify. Hãy áp dụng ngay workflow này để giải phóng sức lao động cho đội ngũ sales và tăng tốc độ tiếp cận khách hàng của doanh nghiệp các sếp nhé!