---
title: "🚀 Tự động hóa SEO Weekly Audit với Gemini và Decodo - N8N Workflow"
description: "Tự động hóa quá trình kiểm tra SEO hàng tuần với Google Sheets, Gemini và Decodo. Giúp tiết kiệm thời gian và tối ưu hóa nội dung website một cách hiệu quả."
slug: "tu-dong-hoa-seo-weekly-audit-voi-gemini-va-decodo"
tags: [n8n, automation, no-code, seo, google-sheets, ai, gemini, decodo]
keywords: [n8n workflow, tự động hóa seo, gemini ai, decodo, google sheets, kiểm tra seo hàng tuần]
---

# 🚀 Tự động hóa SEO Weekly Audit với Gemini và Decodo - N8N Workflow

[Đoạn mở đầu: Phân tích nỗi đau thực tế của các sếp khi phải kiểm tra SEO hàng tuần một cách thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian đáng kể trong việc kiểm tra SEO hàng tuần.
- Tự động hóa quá trình lấy nội dung trang web và tạo báo cáo SEO chi tiết.
- Dữ liệu được lưu trữ và cập nhật tự động trên Google Sheets, giúp theo dõi và phân tích dễ dàng.
- Tối ưu hóa nội dung website một cách hiệu quả với các gợi ý và hướng dẫn cụ thể từ AI.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Sheets với quyền truy cập đầy đủ.
- API Key từ Google Gemini và Decodo.
- Danh sách URL cần kiểm tra được lưu trong Google Sheets với cột tên là "URL".
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào trang [Weekly SEO Watchlist Audit to Google Sheets with Gemini and Decodo](https://n8n.io/workflows/9982).
2. Nhấn vào nút "Import" để tải xuống file JSON của workflow.
3. Trong n8n Editor, nhấn vào nút "Import from File" và chọn file JSON vừa tải xuống.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Set Node**:
   - Thiết lập `sheet_id` cho các tab Input, Output và All Issues trong Google Sheets.
   - Đảm bảo các tab này đã được tạo trước đó trong Google Sheets.

2. **Google Sheets Nodes**:
   - Đảm bảo các tab trong Google Sheets có các cột phù hợp với dữ liệu được ghi vào.
   - Ví dụ: Tab "Input" phải có cột "URL", tab "Output" phải có các cột như "URL", "Decodo Score", "Priority", v.v.

3. **Decodo Node**:
   - Đăng ký tài khoản Decodo [tại đây](https://visit.decodo.com/discount) để nhận mã giảm giá.
   - Thêm credentials cho Decodo trong n8n Editor.

4. **Gemini Node**:
   - Thêm credentials cho Google Gemini trong n8n Editor.

5. **Schedule Trigger Node**:
   - Điều chỉnh lịch trình để workflow chạy hàng tuần (ví dụ: mỗi thứ Hai lúc 09:00 UTC).

#### 3. Kích hoạt ⚡️
1. Nhấn vào nút "Execute Node" để kiểm tra workflow với dữ liệu mẫu.
2. Sau khi kiểm tra thành công, nhấn vào nút "Activate" để kích hoạt workflow.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack hoặc Telegram để nhận thông báo khi workflow hoàn thành.
- Lưu log các lần chạy workflow để theo dõi hiệu suất và lỗi.
- Gửi báo cáo định kỳ qua email với các thống kê và biểu đồ từ Google Sheets.

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm thời gian đáng kể trong việc kiểm tra SEO hàng tuần. Với sự tự động hóa từ Decodo và Gemini, các sếp có thể nhận được báo cáo SEO chi tiết và tối ưu hóa nội dung website một cách hiệu quả. Hãy áp dụng ngay để nâng cao hiệu suất làm việc của mình!