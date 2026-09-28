---
title: "🔍 [Workflow n8n] Phát hiện từ khóa mới trong Google Search Console - Tự động hóa 100% không cần code"
description: "Hướng dẫn chi tiết cách tự động theo dõi từ khóa mới xuất hiện trong Google Search Console bằng workflow n8n. Phát hiện cơ hội SEO mới chỉ trong 7 ngày."
slug: "phan-tich-tu-khoa-moi-google-search-console-n8n"
tags: [n8n, automation, no-code, seo, google-search-console]
keywords: [n8n workflow, tự động hóa, từ khóa mới, google search console, seo]
---

# 🔍 [Workflow n8n] Phát hiện từ khóa mới trong Google Search Console - Tự động hóa 100% không cần code

[Các sếp đang phải làm thủ công việc theo dõi từ khóa mới trong Google Search Console? Hãy để workflow n8n tự động hóa toàn bộ quy trình này chỉ trong 7 ngày!]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Phát hiện từ khóa mới**: Tự động nhận biết các từ khóa mới xuất hiện trong 7 ngày qua.
- **Phân loại chính xác**: Chia từ khóa thành 2 nhóm rõ ràng: "Zero Click" (không có click) và "Has Click" (có click).
- **Tiết kiệm thời gian**: Không cần phải kiểm tra thủ công mỗi ngày.
- **Cơ hội SEO mới**: Nắm bắt nhanh các cơ hội từ khóa mới để tối ưu hóa chiến lược SEO.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Search Console với quyền truy cập đủ cao.
- API Key của Google Search Console (có thể tạo trong Google Cloud Console).
- Quyền truy cập vào n8n Editor để import và cấu hình workflow.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor của các sếp.
2. Click vào "Import from URL" và nhập link: [https://n8n.io/workflows/7645](https://n8n.io/workflows/7645)
3. Hoặc copy JSON từ link trên và paste vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Compare search analytics between two date ranges"**:
   - Chọn credentials của Google Search Console.
   - Đảm bảo các tham số sau được cấu hình đúng:
     - `operation`: comparePageInsights
     - `dateRangeStart`: Ngày bắt đầu so sánh (ví dụ: 14 ngày trước)
     - `dateRangeEnd`: Ngày kết thúc so sánh (ví dụ: 7 ngày trước)
     - `comparisonDateRangeStart`: Ngày bắt đầu so sánh thứ hai (ví dụ: 21 ngày trước)
     - `comparisonDateRangeEnd`: Ngày kết thúc so sánh thứ hai (ví dụ: 14 ngày trước)

2. **Node "Filter (No Past Impressions)"**:
   - Đảm bảo điều kiện lọc là `json.impressions === 0` để chỉ lấy từ khóa không có impressions trong khoảng thời gian so sánh thứ hai.

3. **Node "Zero Click"**:
   - Đảm bảo điều kiện lọc là `json.clicks === 0` để chỉ lấy từ khóa mới xuất hiện nhưng không có click.

4. **Node "Has Click"**:
   - Đảm bảo điều kiện lọc là `json.clicks > 0` để chỉ lấy từ khóa mới xuất hiện và có click.

#### 3. Kích hoạt ⚡️
1. Click vào nút "Execute Workflow" để test với dữ liệu mẫu.
2. Sau khi kiểm tra kết quả, bật "Active" để workflow chạy tự động theo lịch trình.

### ✍️ Mẹo & gợi ý nâng cao
- **Tự động hóa định kỳ**: Thêm node "Schedule Trigger" để workflow chạy tự động mỗi tuần.
- **Thông báo kết quả**: Kết nối với Slack/Telegram để nhận báo cáo kết quả mỗi khi workflow chạy.
- **Lưu trữ dữ liệu**: Kết nối với Google Sheets để lưu trữ lịch sử từ khóa mới.
- **Phân tích sâu hơn**: Kết hợp với các công cụ phân tích khác để đánh giá tiềm năng của từ khóa mới.

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm thời gian đáng kể trong việc theo dõi từ khóa mới trong Google Search Console. Bằng cách tự động hóa toàn bộ quy trình, các sếp có thể tập trung vào việc phân tích và tối ưu hóa chiến lược SEO một cách hiệu quả hơn. Hãy áp dụng ngay để bắt đầu nhận biết các cơ hội từ khóa mới trong 7 ngày qua!