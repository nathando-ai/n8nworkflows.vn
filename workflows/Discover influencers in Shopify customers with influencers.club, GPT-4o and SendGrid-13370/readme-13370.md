---
title: "🚀 Tự động phát hiện Influencer từ khách hàng Shopify với Influencers.club, GPT-4o và SendGrid"
description: "Khám phá cách biến khách hàng mua hàng trên Shopify thành đại sứ thương hiệu tự động bằng n8n, AI và dữ liệu mạng xã hội."
slug: "tu-dong-phat-hien-influencer-tu-khach-hang-shopify"
tags: [n8n, automation, shopify, ai, gpt-4o, influencers-club, sendgrid]
keywords: [n8n workflow, shopify influencer automation, influencers.club api, gpt-4o marketing, tự động hóa influencer marketing]
---

# 🚀 Tự động phát hiện Influencer từ khách hàng Shopify với Influencers.club, GPT-4o và SendGrid

Các sếp có bao giờ tự hỏi liệu trong số hàng ngàn khách hàng mua hàng trên cửa hàng Shopify của mình, có ai đang là Influencer (KOL/KOC) tiềm năng không? Việc đi tìm kiếm thủ công từng tài khoản mạng xã hội của khách hàng cực kỳ mất thời gian và gần như bất khả thi khi lượng đơn hàng tăng lên.

Workflow n8n này sẽ giải quyết triệt để bài toán đó bằng cách tự động hóa 100% quy trình: **Lắng nghe đơn hàng Shopify ➡️ Kiểm tra dữ liệu mạng xã hội qua Influencers.club ➡️ AI phân loại và đánh giá tiềm năng ➡️ Gửi email outreach cá nhân hóa ➡️ Đồng bộ CRM HubSpot và báo cáo qua Slack**.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 mà không sợ sập nguồn hay gián đoạn, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tận dụng nguồn vàng có sẵn:** Biến ngay những khách hàng hiện tại (hoặc người đăng ký mới) thành đại sứ thương hiệu mà không cần tốn chi phí tìm kiếm tệp khách hàng lạnh.
- **Tiết kiệm 95% thời gian:** Tự động hóa hoàn toàn từ bước quét dữ liệu, phân loại bằng AI (GPT-4o/GPT-4o-mini) đến gửi email chào hàng (Outreach).
- **Cá nhân hóa đỉnh cao:** AI tự động viết email phù hợp với ngách (niche), số lượng followers và nền tảng mạng xã hội của từng Creator.
- **Vận hành minh bạch:** Tự động đồng bộ khách hàng tiềm năng lên HubSpot CRM và gửi thông báo nóng hổi về Slack khi có Creator giá trị cao xuất hiện.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động mượt mà, các sếp cần chuẩn bị sẵn các tài khoản và API Keys sau:
- **n8n Instance** (Self-hosted hoặc Cloud).
- **Shopify Account** (để cấu hình Webhook Trigger).
- **Influencers.club API Key** (dùng để quét thông tin mạng xã hội qua email).
- **OpenAI API Key** (cho các node GPT-4o và GPT-4o-mini).
- **SendGrid API Key** (để gửi chiến dịch email tự động).
- **HubSpot App Token** (để lưu trữ contact CRM).
- **Slack Bot Token / OAuth2** (để nhận thông báo real-time).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này từ n8n.io hoặc copy toàn bộ mã nguồn JSON, sau đó dán trực tiếp vào n8n Editor của các sếp bằng phím tắt `Ctrl + V` (hoặc `Cmd + V`).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 17 nodes. Các sếp cần chú ý cấu hình kỹ các điểm sau:
- **Shopify Order Trigger & Shopify Customer Trigger:** Kết nối tài khoản Shopify OAuth2 của các sếp. Khi kích hoạt workflow, các webhook sẽ tự động được đăng ký trên Shopify.
- **Get Customer Email (Set Node):** Trích xuất chính xác email từ payload của Shopify. Đảm bảo cấu hình đúng cú pháp:
  - Cho Order Trigger: `{{ $json.customer.email }}`
  - Cho Customer Trigger: `{{ $json.email }}`
- **Enrich by Email (Influencers.club):** Nhập Influencers.club API Key vào phần Header Auth để hệ thống có thể truy vấn dữ liệu từ 50+ nền tảng mạng xã hội (Instagram, TikTok, YouTube...).
- **OpenAI Chat Model1 & Classifier Model1:** Chọn đúng credentials OpenAI và đảm bảo model được chọn lần lượt là `gpt-4o` (cho Outreach Agent) và `gpt-4o-mini` (cho Classification Agent) để tối ưu chi phí.
- **Send an email (SendGrid):** Cấu hình địa chỉ email gửi đi (`From Email`) thuộc domain đã xác thực trên SendGrid.
- **Create or update a CRM contact (HubSpot) & Slack Nodes:** Chọn đúng credentials tương ứng và map lại các trường dữ liệu tùy chỉnh (Custom Properties) như tier, niche, followers để quản lý sát sao hơn.

#### 3. Kích hoạt ⚡️
- Thực hiện chạy thử (Test Run) với một đơn hàng hoặc khách hàng mẫu từ Shopify.
- Kiểm tra các đường nhánh `TRUE/FALSE` ở node **Is Creator?** để đảm bảo hệ thống lọc đúng tệp.
- Sau khi kiểm tra mọi thứ hoạt động trơn tru, hãy bật công tắc **Active workflow** để hệ thống tự động chạy 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Lọc ngưỡng followers:** Tại node **Is Creator?**, các sếp có thể bổ sung thêm điều kiện tối thiểu (ví dụ: `result.max_followers >= 1000`) để loại bỏ các tài khoản quá nhỏ, tập trung vào Nano và Micro-influencer chất lượng.
- **Mở rộng kênh thông báo:** Thay vì chỉ gửi Slack, các sếp có thể tích hợp thêm node Telegram để nhận thông báo ngay trên điện thoại cá nhân khi có Creator "cỡ bự" xuất hiện trong danh sách mua hàng.
- **Tạo bảng Log dữ liệu:** Thêm một node Google Sheets ở cuối nhánh lỗi (`Handle Failed Enrichment`) để lưu trữ lại các email không tìm thấy thông tin, phục vụ cho việcRemarketing sau này.

### 📌 Kết luận
Việc tận dụng tệp khách hàng sẵn có trên Shopify kết hợp cùng sức mạnh của AI và Influencers.club chính là chìa khóa vàng giúp doanh nghiệp tối ưu chi phí Marketing và bùng nổ doanh số từ Affiliate/Influencer. Hãy cài đặt ngay workflow này và "lên đồ" cho hệ thống tự động hóa của các sếp ngay hôm nay!