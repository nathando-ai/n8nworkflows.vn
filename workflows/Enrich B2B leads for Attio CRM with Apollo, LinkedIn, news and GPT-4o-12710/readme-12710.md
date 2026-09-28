---
title: "🚀 Tự động hóa Enrich B2B Leads cho Attio CRM bằng Apollo, LinkedIn, Tavily & GPT-4o"
description: "Hướng dẫn xây dựng workflow n8n siêu cấp giúp tự động thu thập thông tin công ty, tin tức mới nhất, phân tích profile lãnh đạo qua LinkedIn và tổng hợp bằng GPT-4o đẩy thẳng vào Attio CRM."
slug: "tu-dong-enrich-b2b-leads-attio-crm-apollo-gpt4o"
tags: [n8n, automation, no-code, crm, ai-agent, lead-generation]
keywords: [n8n workflow, Attio CRM, Apollo API, GPT-4o, lead enrichment, tự động hóa sales]
---

# 🚀 Tự động hóa Enrich B2B Leads cho Attio CRM bằng Apollo, LinkedIn, Tavily & GPT-4o

Các đội ngũ Sales và BDR (Business Development Representative) thường tốn rất nhiều thời gian quý báu để "google" thông tin khách hàng tiềm năng, đọc báo cáo tài chính, tìm kiếm bài đăng LinkedIn của lãnh đạo công ty mục tiêu trước khi thực hiện một cuộc gọi hay gửi email cold outreach. Việc làm thủ công này vừa tốn thời gian, dễ sai sót lại vừa khó duy trì tính nhất quán của dữ liệu trong CRM.

Workflow n8n này chính là giải pháp tự động hóa 100% không cần code (No-code), thay thế hoàn toàn công sức nghiên cứu thủ công của BDR bằng sức mạnh của **Apollo, Tavily, Scrape Creators (LinkedIn), kết hợp AI Agents sử dụng mô hình GPT-4o đỉnh cao**, sau đó tự động đồng bộ hóa toàn bộ dữ liệu sạch sẽ vào **Attio CRM**.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80% thời gian nghiên cứu:** Giảm thời gian BDR phải tra cứu thủ công từ hàng giờ xuống chỉ còn vài giây mỗi lead.
- **Dữ liệu CRM cực kỳ chất lượng:** Tự động enrich thông tin công ty, tin tức mới nhất, bài đăng mạng xã hội và thông tin người ra quyết định (Leadership).
- **Cá nhân hóa sâu sắc:** AI phân tích bối cảnh công ty giúp BDR có góc nhìn sắc bén để tạo ra các chiến dịch outreach có tỷ lệ chuyển đổi cao.
- **Hoạt động tin cậy & Fallback thông minh:** Tích hợp cơ chế xử lý lỗi linh hoạt, đảm bảo hệ thống không bị gián đoạn khi một số nguồn dữ liệu gặp sự cố.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động mượt mà, các sếp cần chuẩn bị sẵn các tài khoản và API keys sau:
- **n8n Instance** (Self-hosted hoặc Cloud).
- **OpenAI API Key** (Sử dụng model `gpt-4o`).
- **Apollo.io API Key** (Dùng cho các node `Apollo:EnrichCompany`, `Apollo:LatestNews`, `Apollo:Fetch Person`).
- **Tavily API Key** (Dùng cho node `Extract` để cào và trích xuất nội dung web).
- **Scrape Creators API Key** (Dùng cho các node `Get a linked in company page` và `Get a LinkedIn Profile`).
- **Attio CRM API Key** (Dùng cho các node `Assert a record`, `Assert Record: Company`, v.v.).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Các sếp copy đoạn mã JSON của workflow này (hoặc tải file JSON từ nguồn gốc).
- Vào giao diện n8n Editor, chọn **Add workflow** -> **Import from File** hoặc dán trực tiếp vào màn hình làm việc.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Vì workflow có tới 53 nodes xử lý đa tầng, các sếp cần chú ý cấu hình kỹ các thành phần sau:
- **Credentials:** Gán đúng các API Keys đã chuẩn bị vào các node tương ứng:
  - `Apollo:*` nodes: Chọn HTTP Header Auth chứa Apollo API Key.
  - `Get a linked in company page` & `Get a LinkedIn Profile`: Chọn Scrape Creators API.
  - `Extract`: Chọn Tavily API.
  - `OpenAI Chat Model*`: Chọn OpenAI API Credentials và cấu hình model `gpt-4o`.
  - `Assert a record` / `Assert Record: Company`: Chọn Attio API Credentials và trỏ tới đúng Object/List trong CRM của các sếp.
- **Node khởi chạy (`When clicking 'Execute workflow'`):** Thiết lập dữ liệu đầu vào mẫu (Test Data) bao gồm tên công ty, tên miền website hoặc URL LinkedIn của doanh nghiệp cần enrich.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** với dữ liệu mẫu để kiểm tra toàn bộ chuỗi Agents xử lý (Apollo Summary, LinkedIn Company Summary, Leadership Search Agent, v.v.).
- Kiểm tra kết quả trên Attio CRM xem dữ liệu đã được cập nhật chính xác chưa.
- Sau khi test thành công, bật công tắc **Active** góc trên cùng bên phải để workflow sẵn sàng hoạt động tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Webhook / Trigger tự động:** Thay vì dùng `Manual Trigger`, các sếp có thể đổi thành Webhook nhận dữ liệu từ Typeform, Webflow khi khách hàng điền form đăng ký, hoặc kết nối trực tiếp với một Google Sheet danh sách khách hàng.
- **Bổ sung thông báo:** Thêm node gửi tin nhắn qua **Telegram** hoặc **Slack** để báo cáo cho team Sales ngay khi một lead VIP được enrich và đẩy lên Attio CRM thành công.
- **Lưu trữ Log:** Sử dụng thêm Google Sheets hoặc một database phụ để lưu lại log chạy của AI Agents nhằm phục vụ việc kiểm tra và tối ưu Prompt sau này.

### 📌 Kết luận
Workflow Enrich B2B Leads bằng AI và Apollo kết hợp Attio CRM là một "vũ khí hạng nặng" giúp tối ưu hóa quy trình Sales của bất kỳ doanh nghiệp B2B nào. Hãy cài đặt ngay hôm nay để giải phóng thời gian cho đội ngũ BDR và bứt phá doanh số!