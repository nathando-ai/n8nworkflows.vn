---
title: "🚀 Tự động trích xuất thông tin doanh nghiệp và tính điểm ICP với Airtop trong n8n"
description: "Hướng dẫn chi tiết cách tự động hóa quy trình enrich dữ liệu công ty, tìm LinkedIn và chấm điểm ICP (Ideal Customer Profile) sử dụng Airtop và n8n."
slug: "tu-dong-trich-xuat-thong-tin-doanh-nghiep-va-tinh-diem-icp-voi-airtop"
tags: [n8n, automation, airtop, sales-automation, icp-scoring, data-enrichment]
keywords: [n8n workflow, trích xuất thông tin công ty, tính điểm ICP, Airtop automation, enrich dữ liệu bán hàng]
---

# 🚀 Tự động hóa trích xuất thông tin doanh nghiệp và chấm điểm ICP với Airtop

Các đội ngũ Sales và Growth thường tốn rất nhiều thời gian thủ công để tra cứu thông tin công ty, tìm trang LinkedIn chính thức, và đánh giá xem doanh nghiệp đó có thực sự là khách hàng lý tưởng (ICP - Ideal Customer Profile) hay không trước khi bắt đầu tiếp cận.

Workflow n8n này sẽ giải quyết triệt để bài toán trên bằng cách tự động hóa 100%: nhận diện URL LinkedIn, trích xuất toàn bộ dữ liệu doanh nghiệp và chấm điểm ICP dựa trên các tiêu chí tùy chỉnh. Nhờ tích hợp **Airtop** (nền tảng tự động hóa trình duyệt thông minh bằng AI), workflow có thể tương tác với web và trích xuất dữ liệu mượt mà ngay cả trên những nền tảng phức tạp.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian**: Không còn phải tra cứu thủ công từng công ty trên Google và LinkedIn.
- **Dữ liệu chuẩn hóa**: Tự động tổng hợp tên công ty, quy mô nhân sự, mô tả, vị trí và các chỉ số đánh giá chuyên sâu.
- **Chấm điểm ICP tự động**: Biết ngay lập tức liệu khách hàng có tiềm năng cao hay thấp dựa trên bảng điểm (rubric) cấu hình sẵn.
- **Linh hoạt đầu vào**: Có thể kích hoạt thông qua Form nhập liệu trực tiếp hoặc gọi từ một workflow n8n khác trong hệ thống của bạn.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n**: Đã hoạt động (Cloud hoặc Self-hosted).
- **Airtop API Key**: Lấy từ [Airtop Portal API Keys](https://portal.airtop.ai/api-keys).
- **Airtop Profile**: [Airtop Browser Profile](https://portal.airtop.ai/browser-profiles) đã được cấu hình và đăng nhập sẵn tài khoản LinkedIn.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow hoặc copy trực tiếp mã nguồn JSON.
- Trong giao diện n8n Editor, chọn **Add workflow** -> Nhấn vào dấu `...` ở góc trên bên phải -> Chọn **Import from File / Clipboard** và dán JSON vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần chú ý cấu hình các node cốt lõi sau trong workflow:
- **On form submission (`formTrigger`)**: Thiết lập form đầu vào để thu thập tên miền công ty (`Company domain`) và link LinkedIn (nếu có sẵn).
- **Extract company LinkedIn url (`executeWorkflow`)**: Node gọi workflow con để tìm kiếm URL LinkedIn của công ty nếu thông tin đầu vào chưa có.
- **Extract Company Information (`executeWorkflow`)**: Sử dụng Airtop để cào dữ liệu chi tiết từ trang LinkedIn doanh nghiệp (tên, tagline, website, địa điểm, quy mô nhân sự...).
- **Calclate ICP (`executeWorkflow`)**: Chạy logic chấm điểm ICP dựa trên các tiêu chí như mức độ tập trung vào công nghệ/AI, quy mô, hoặc phân loại doanh nghiệp.
- **Unify Params (`set`)**: Gom nhóm và đồng bộ toàn bộ dữ liệu đã xử lý thành một JSON object hoàn chỉnh phục vụ cho các bước tiếp theo (như lưu CRM, gửi Slack...).

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (**Test run**) với một vài tên miền mẫu (ví dụ: `example.com`) để kiểm tra dữ liệu trả về từ Airtop.
- Sau khi kết quả trả về chính xác, gạt công tắc sang **Active** để bật workflow chạy tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Đẩy dữ liệu về CRM**: Kết nối đầu ra của workflow với HubSpot, Pipedrive hoặc Google Sheets để tự động cập nhật hồ sơ khách hàng tiềm năng.
- **Kết hợp Enriched Lead**: Ghép nối workflow này với một workflow chuyên enrich thông tin cá nhân (như Founder, C-Level) của công ty đó.
- **Cảnh báo qua Slack/Telegram**: Thiết lập gửi thông báo ngay lập tức vào nhóm Sales khi hệ thống phát hiện một công ty đạt điểm ICP cao (ví dụ > 80 điểm).

### 📌 Kết luận
Với sự kết hợp giữa n8n và Airtop, việc chấm điểm và thu thập dữ liệu doanh nghiệp giờ đây đã được tự động hóa hoàn toàn. Hãy "lên đồ" ngay workflow này để tối ưu hóa phễu bán hàng và tăng tốc độ tiếp cận khách hàng tiềm năng cho đội ngũ của các sếp!