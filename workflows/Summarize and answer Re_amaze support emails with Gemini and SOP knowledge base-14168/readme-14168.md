---
title: "🚀 Tự động hóa Hỗ trợ Khách hàng với Gemini và Re:amaze - Workflow n8n"
description: "Hướng dẫn chi tiết cách tự động phân loại và trả lời email hỗ trợ khách hàng từ Re:amaze bằng AI Gemini trong n8n. Tiết kiệm thời gian xử lý, đảm bảo chính xác và tuân thủ SOP."
slug: "tu-dong-hoa-ho-tro-khach-hang-gemini-reamaze-n8n"
tags: [n8n, automation, no-code, ai, customer-support]
keywords: [n8n workflow, tự động hóa hỗ trợ khách hàng, AI Gemini, Re:amaze, SOP]
---

# 🚀 Tự động hóa Hỗ trợ Khách hàng với Gemini và Re:amaze - Workflow n8n

[Đoạn mở đầu: Phân tích nỗi đau thực tế của các sếp khi xử lý hàng nghìn email hỗ trợ khách hàng hàng ngày. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động phân loại email theo chủ đề (setup, pricing, security...)
- Tạo phản hồi chính xác theo SOP của doanh nghiệp
- Tiết kiệm 80% thời gian xử lý email hàng ngày
- Tránh trùng lặp phản hồi cho cùng một yêu cầu
- Đảm bảo phản hồi tuân thủ chính sách nội bộ
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Re:amaze với quyền truy cập API
- API Key từ Google Gemini (đã cấu hình trong n8n)
- Cơ sở dữ liệu SOP (Google Sheets hoặc công cụ nội bộ)
- Thông tin xác thực HTTP Basic Auth cho Re:amaze API
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [Workflow gốc trên n8n.io](https://n8n.io/workflows/14168)
2. Click vào nút "Copy to clipboard" để sao chép JSON workflow
3. Trong n8n Editor, click vào "Import from Clipboard" và dán JSON đã sao chép

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Fetch Conversations from Re:amaze API"**:
   - Cấu hình credentials HTTP Basic Auth với thông tin đăng nhập Re:amaze
   - Điền URL API endpoint (tham khảo [tài liệu API Re:amaze](https://www.reamaze.com/api/get_messages))

2. **Node "Email Category Classifier" và "LLM Response Generator"**:
   - Cấu hình credentials Google Palm API với API Key của Gemini
   - Đảm bảo mô hình Gemini đã được kích hoạt trong tài khoản Google Cloud

3. **Node "📚 Knowledge Base"**:
   - Nếu sử dụng Google Sheets: Cấu hình credentials Google Sheets và điền ID Sheet
   - Nếu sử dụng công cụ nội bộ: Cập nhật mã code phù hợp với hệ thống SOP của doanh nghiệp

4. **Node "Send Reply to Customer (Re:amaze API)"**:
   - Cấu hình credentials HTTP Basic Auth giống như node đầu tiên
   - Điền URL API endpoint cho chức năng gửi phản hồi

#### 3. Kích hoạt ⚡️
1. Test run dữ liệu mẫu:
   - Sử dụng node "Manual Trigger (Test Workflow)" để kiểm tra toàn bộ luồng
   - Đảm bảo các node xử lý dữ liệu đầu ra như mong đợi

2. Bật Active workflow:
   - Sau khi test thành công, chuyển workflow sang chế độ Active
   - Cấu hình lịch chạy phù hợp (ví dụ: mỗi 15 phút để xử lý email mới)

### ✍️ Mẹo & gợi ý nâng cao
1. **Kết hợp với Slack/Telegram**:
   - Thêm node gửi thông báo đến kênh Slack/Telegram khi có email cần xử lý đặc biệt
   - Ví dụ: Gửi cảnh báo khi nhận email thuộc danh mục "escalate_support"

2. **Lưu log hoạt động**:
   - Thêm node ghi log vào Google Sheets hoặc cơ sở dữ liệu để theo dõi hiệu suất
   - Lưu trữ lịch sử phản hồi để kiểm tra chất lượng

3. **Tích hợp với hệ thống CRM**:
   - Kết nối với Salesforce/Zoho CRM để cập nhật trạng thái ticket
   - Tự động tạo lead từ email khách hàng mới

4. **Báo cáo định kỳ**:
   - Thêm node tạo báo cáo hàng tuần/tháng về hiệu suất hỗ trợ
   - Gửi báo cáo tự động đến quản lý qua email

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa 100% quy trình xử lý email hỗ trợ khách hàng, giảm thiểu lỗi và tăng hiệu suất làm việc. Bằng cách tích hợp AI Gemini với cơ sở dữ liệu SOP của doanh nghiệp, workflow đảm bảo phản hồi luôn chính xác và tuân thủ chính sách nội bộ. Hãy thử ngay và trải nghiệm cách làm việc thông minh hơn với n8n!