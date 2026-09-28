---
title: "🚀 Tự động phân tích từ khóa đối thủ (Keyword Gap) và lưu vào Notion với DataForSEO"
description: "Khám phá workflow n8n tự động tìm kiếm khoảng trống từ khóa (keyword gap) giữa website của bạn và đối thủ bằng DataForSEO API, sau đó tự động lưu cơ hội vào Notion."
slug: "tu-dong-phan-tich-tu-khoa-doi-thu-keyword-gap-notion-dataforseo"
tags: [n8n, automation, no-code, seo, dataforseo, notion, market-research]
keywords: [n8n workflow, keyword gap analysis, phân tích từ khóa đối thủ, DataForSEO API, tự động hóa SEO, Notion automation]
---

# 🚀 Tự động phân tích từ khóa đối thủ (Keyword Gap) và lưu vào Notion với DataForSEO

Các sếp làm SEO và Content Marketing chắc chắn đã quá quen thuộc với việc mất hàng giờ đồng hồ để so sánh từ khóa của website mình với đối thủ trên các công cụ trả phí đắt đỏ, sau đó lọc thủ công và đưa vào bảng kế hoạch. Việc này vừa tốn thời gian, vừa dễ bỏ sót các cơ hội vàng.

Workflow n8n này sẽ giải quyết triệt để nỗi đau đó bằng cách tự động hóa 100% quy trình: Lấy top 100 từ khóa của bạn, lấy từ khóa của đối thủ, tìm ra khoảng trống (những từ khóa đối thủ đang có mà bạn chưa có) và tự động ghi nhận toàn bộ vào Notion database để sẵn sàng lên kế hoạch nội dung!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 và xử lý các tập dữ liệu SEO lớn, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn:** Không cần copy-paste thủ công giữa các công cụ SEO và bảng biểu.
- **Phát hiện cơ hội ẩn:** Lọc chính xác những từ khóa đối thủ đang có lượng tìm kiếm cao mà website của bạn chưa chiếm lĩnh.
- **Đồng bộ trực tiếp:** Đẩy thẳng dữ liệu vào Notion, tạo tiền đề để kết hợp Notion AI xây dựng chiến lược nội dung ngay lập tức.
- **Tiết kiệm chi phí:** Tận dụng DataForSEO API mạnh mẽ với chi phí tối ưu thay vì mua các tool SEO truyền thống đắt đỏ.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt sẵn sàng (Cloud hoặc Self-hosted).
- **DataForSEO Account:** Tài khoản và thông tin API (Login và Password) để gọi DataForSEO Labs API.
- **Notion Account:** Tài khoản Notion đã chuẩn bị sẵn một Database để lưu trữ dữ liệu từ khóa.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể copy mã JSON của workflow từ nguồn cung cấp và dán trực tiếp vào n8n Editor của mình thông qua tính năng Import từ clipboard.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow hoạt động mượt mà, các sếp cần cấu hình chính xác các node sau:

- **Get my ranked keywords (`n8n-nodes-dataforseo.dataForSeoLabsApi`):** 
  - Chọn hoặc tạo mới `dataForSeoApi` credentials bằng API login và password từ trang quản trị DataForSEO.
  - Cấu hình trang web/URL mục tiêu của các sếp, chọn vị trí (location), ngôn ngữ (language) và các thông số tìm kiếm phù hợp.
- **Get my competitor’s ranked keywords (`n8n-nodes-dataforseo.dataForSeoLabsApi`):**
  - Sử dụng chung credentials DataForSEO.
  - Nhập URL trang web của đối thủ mà các sếp muốn phân tích khoảng trống từ khóa.
- **Edit fields (myKeywords) & Filter & Split out:**
  - Các node này làm nhiệm vụ so sánh tập từ khóa của bạn và đối thủ, lọc ra những từ khóa mà đối thủ có nhưng website của bạn chưa xếp hạng.
- **Create a database page (`notion`):**
  - Tạo kết nối `notionApi`.
  - Chọn Database Page trong Notion đã được chuẩn bị trước với các trường dữ liệu được khuyến nghị:
    - *Competitor's Ranked Keyword* (Map với: `{{ $('Split Out').item.json.keyword_data.keyword }}`)
    - *Keyword Search Volume* (Map với: `{{ $('Split Out').item.json.keyword_data.keyword_info.search_volume }}`)
    - *Keyword Competition* (Map với: `{{ $('Split Out').item.json.keyword_data.keyword_info.competition }}`)
    - *Competitor's Position* (Map với: `{{ $('Split Out').item.json.ranked_serp_element.serp_item.rank_group }}`)
    - *Competitor's URL* (Map với: `{{ $('Split Out').item.json.ranked_serp_element.serp_item.url }}`)

#### 3. Kích hoạt ⚡️
- Nhấn nút **Execute workflow** thủ công ở node `When clicking ‘Execute workflow’` để test chạy thử với dữ liệu thực tế.
- Kiểm tra lại Notion Database xem các từ khóa đã được đồng bộ chuẩn xác chưa.
- Bật công tắc **Active** để sẵn sàng sử dụng bất cứ lúc nào.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Notion AI:** Sau khi dữ liệu từ khóa đã nằm trong Notion, các sếp có thể sử dụng câu lệnh gợi ý (prompt): *“Analyze the keyword gap between my website’s page {{your URL}} and competitor website’s page and build a content strategy for me”* để AI tự động lên dàn ý bài viết chuẩn SEO.
- **Thông báo qua Telegram/Slack:** Thêm một node Telegram hoặc Slack vào cuối workflow để nhận thông báo ngay khi quét xong từ khóa mới.
- **Lập lịch chạy định kỳ (Cron):** Thay thế Trigger thủ công bằng `Schedule Trigger` để n8n tự động quét đối thủ hàng tuần hoặc hàng tháng.

### 📌 Kết luận
Workflow này là trợ thủ đắc lực giúp các sếp tối ưu hóa quy trình nghiên cứu từ khóa đối thủ, tiết kiệm hàng đống thời gian và nhanh chóng xây dựng chiến lược nội dung đón đầu thị trường. Hãy triển khai ngay vào hệ thống n8n của các sếp nhé!