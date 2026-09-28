---
title: "🚀 Tóm tắt nội dung trang web với OpenAI GPT-5-mini và bộ nhớ cache 24h"
description: "Tự động hóa việc tóm tắt nội dung trang web với AI, giảm thời gian xử lý và tối ưu hóa hiệu suất với bộ nhớ cache 24 giờ"
slug: "tom-tat-noi-dung-trang-web-voi-openai-gpt-5-mini-va-bo-nho-cache-24h"
tags: [n8n, automation, no-code, AI, summarization]
keywords: [n8n workflow, tự động hóa, tóm tắt nội dung, AI, OpenAI]
---

# 🚀 Tóm tắt nội dung trang web với OpenAI GPT-5-mini và bộ nhớ cache 24h

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian xử lý: Với bộ nhớ cache 24h, workflow chỉ xử lý lại nội dung khi cần thiết.
- Tăng hiệu quả làm việc: Tự động tóm tắt nội dung trang web với độ chính xác cao của OpenAI GPT-5-mini.
- Tối ưu hóa tài nguyên: Giảm tải cho hệ thống bằng cách lưu trữ kết quả tóm tắt.
- Tích hợp dễ dàng: Kết nối liền mạch với các workflow khác trong hệ thống n8n.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản OpenAI với API key hợp lệ.
- URL của trang web cần tóm tắt.
- (Tùy chọn) CSS selector để trích xuất nội dung cụ thể từ trang web.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [link workflow gốc](https://n8n.io/workflows/15776)
2. Click vào nút "Download" để tải file JSON workflow.
3. Trong n8n Editor, click vào "Import from File" và chọn file JSON vừa tải về.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "OpenAI Chat Model"**:
   - Đảm bảo đã tạo và cấu hình credentials cho OpenAI.
   - Chọn model "gpt-5-mini" trong danh sách model.

2. **Node "GET URL"**:
   - Cấu hình URL của trang web cần tóm tắt.
   - Đặt phương thức HTTP thành "GET".

3. **Node "Extract HTML Content"**:
   - (Tùy chọn) Thêm CSS selector nếu chỉ muốn trích xuất phần nội dung cụ thể từ trang web.

4. **Node "Summarization Chain"**:
   - (Tùy chọn) Điều chỉnh prompt tóm tắt nếu cần độ dài hoặc phong cách tóm tắt khác.

#### 3. Kích hoạt ⚡️
1. Test run workflow với dữ liệu mẫu.
2. Kiểm tra kết quả tóm tắt được tạo ra.
3. Bật Active workflow để sử dụng trong môi trường sản xuất.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Telegram để nhận thông báo khi có nội dung mới được tóm tắt.
- Lưu log các lần tóm tắt để theo dõi hiệu suất của workflow.
- Gửi báo cáo định kỳ về các nội dung đã được tóm tắt.
- Tùy chỉnh thời gian cache để phù hợp với nhu cầu cập nhật nội dung.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa việc tóm tắt nội dung trang web một cách hiệu quả, tiết kiệm thời gian và tài nguyên. Với bộ nhớ cache 24h và khả năng tích hợp với các hệ thống khác, workflow này là giải pháp hoàn hảo cho việc quản lý và phân tích thông tin từ các trang web. Hãy thử ngay và trải nghiệm sự khác biệt!