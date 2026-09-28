---
title: "🚀 Tự động tìm kiếm, phân tích Creator và Lookalike bằng AI, đồng bộ HubSpot"
description: "Hướng dẫn xây dựng workflow n8n tự động khám phá Influencer tiềm năng, phân tích chuyên sâu bằng OpenAI và đồng bộ dữ liệu vào HubSpot CRM."
slug: "tu-dong-tim-kiem-phan-tich-creator-lookalike-hubspot"
tags: [n8n, automation, hubspot, openai, influencer-marketing, ai-agent]
keywords: [n8n workflow, influencers club, hubspot crm, ai agent, creator discovery, lookalike influencer]
---

# 🚀 Tự động tìm kiếm, phân tích Creator và Lookalike bằng AI, đồng bộ HubSpot

Việc tìm kiếm và sàng lọc Influencer (KOL/KOC) thủ công cho các chiến dịch marketing thường ngốn rất nhiều thời gian của các đội ngũ. Từ việc tìm profile, cào dữ liệu, đánh giá độ phù hợp cho đến việc đẩy vào CRM (HubSpot) để quản lý. 

Workflow n8n này sẽ giải quyết triệt để nỗi đau đó bằng cách **tự động hóa 100%**: Khám phá Creator mới từ Influencers Club API, phân tích chuyên sâu bằng OpenAI AI Agent, tự động tìm kiếm các kênh tương tự (Lookalike) có hiệu suất cao, và cuối cùng là đồng bộ sạch sẽ vào HubSpot CRM.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa toàn diện:** Chạy định kỳ theo lịch trình (Schedule Trigger) mà không cần can thiệp thủ công.
- **AI Phân tích thông minh:** Đánh giá điểm mạnh, điểm yếu, độ uy tín tệp người theo dõi, khả năng phù hợp thương hiệu và ước tính tương tác qua OpenAI GPT-4o-mini.
- **Nhân bản tệp khách hàng (Lookalike):** Tự động chọn Creator có tầm ảnh hưởng lớn nhất trong đợt quét để làm hạt giống tìm kiếm các creator tương tự.
- **Đồng bộ CRM liền mạch:** Lưu trữ toàn bộ thông tin chi tiết của Creator và Lookalike trực tiếp vào HubSpot dưới dạng Contact để đội ngũ Sales/Marketing dễ dàng tiếp cận.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Tài khoản Influencers.club** (Lấy API Key/Header Auth cho các node API Discovery, Lookalike và Enrichment).
- **Tài khoản OpenAI** (Lấy API Key cho các AI Agent node sử dụng mô hình `gpt-4o-mini`).
- **Tài khoản HubSpot** (Lấy App Token để kết nối CRM).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow từ nguồn hoặc sao chép đoạn mã JSON, sau đó dán trực tiếp vào màn hình n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 2 nhánh chính hoạt động song song (`Dual Branch Pipeline`): Nhánh **Discovery** và Nhánh **Lookalike**. Các sếp cần cấu hình kỹ các phần sau:

- **Schedule Trigger1:** Cài đặt tần suất chạy phù hợp với ngân sách Credit của Influencers Club API (tránh chạy quá dày đặc gây tốn kém).
- **Discovery API Call1 & Lookalike API Call1:** 
  - Chọn Credentials loại `httpHeaderAuth` để kết nối với Influencers.club API.
  - Tùy chỉnh tham số tìm kiếm `ai_search` trong body request để nhắm trúng ngách (niche), vị trí, độ tuổi hoặc lượng followers mong muốn.
- **Enrichment API (Discovery) & Enrichment API (Lookalike):** 
  - Cấu hình thông tin xác thực tương tự để hệ thống lấy dữ liệu chi tiết (thông tin liên hệ, nhân khẩu học, lịch sử làm brand, v.v.).
- **OpenAI Model (Discovery) & OpenAI Model (Lookalike):** 
  - Chọn credentials `openAiApi` và đảm bảo model được trỏ đến `gpt-4o-mini` để tối ưu chi phí và tốc độ.
- **HubSpot — Discovery Creator & HubSpot — Lookalike Creator:** 
  - Chọn credentials `hubspotAppToken`, ánh xạ các trường dữ liệu (Email, Tên, Handles, Thống kê từ AI Agent) vào các thuộc tính tương ứng trên HubSpot CRM.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (`Test workflow`) với một vài bản ghi mẫu để kiểm tra tính toàn vẹn dữ liệu qua các bước `Normalize Profile` và `AI Agent`.
- Sau khi mọi thứ chạy mượt mà, gạt công tắc sang chế độ **Active**.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp kênh thông báo:** Thêm node Slack hoặc Telegram ngay sau node HubSpot để bắn thông báo về channel nội bộ mỗi khi hệ thống tìm thấy một Creator "triệu view" tiềm năng.
- **Lưu log dự phòng:** Thêm node Google Sheets để lưu trữ dữ liệu thô song song cùng HubSpot nhằm phục vụ việc phân tích báo cáo dài hạn.
- **Chia nhỏ batch:** Với tệp tìm kiếm lớn, hãy điều chỉnh cấu hình trong `Loop Over Items (Discovery)` để hệ thống không bị quá tải API rate limit.

### 📌 Kết luận
Workflow này là cỗ máy tự động hóa hoàn hảo cho các đội ngũ Influencer Marketing muốn tối ưu hóa quy trình từ khâu tìm kiếm, phân tích bằng AI cho đến lưu trữ CRM mà không tốn một phút làm tay nào. Áp dụng ngay để bứt phá hiệu suất chiến dịch của các sếp!