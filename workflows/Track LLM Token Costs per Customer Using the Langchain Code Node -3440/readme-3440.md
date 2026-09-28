---
title: "💰 Theo dõi chi phí token LLM cho từng khách hàng bằng n8n"
description: "Hướng dẫn tự động hóa chi tiết theo dõi chi phí sử dụng token LLM cho từng khách hàng bằng workflow n8n, tích hợp Google Sheets và gửi hóa đơn tự động"
slug: "theo-doi-chi-phi-token-llm-khach-hang"
tags: [n8n, automation, no-code, ai, langchain, google-sheets]
keywords: [n8n workflow, tự động hóa, langchain, token llm, google sheets, hóa đơn tự động]
---

# 💰 Theo dõi chi phí token LLM cho từng khách hàng bằng n8n

[Các sếp đang gặp khó khăn khi quản lý chi phí sử dụng LLM (Large Language Model) cho từng khách hàng một cách thủ công. Với workflow này, chúng ta sẽ tự động hóa toàn bộ quy trình từ theo dõi sử dụng đến gửi hóa đơn hàng tháng, giúp tiết kiệm thời gian và giảm thiểu sai sót.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động theo dõi chi tiết token sử dụng của từng khách hàng
- Tính toán chi phí sử dụng LLM một cách chính xác
- Tự động gửi hóa đơn hàng tháng cho khách hàng
- Giảm thiểu công việc thủ công và sai sót
- Tích hợp liền mạch với Google Sheets cho quản lý dữ liệu
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google với quyền truy cập Google Sheets
- API key của OpenAI (để sử dụng LLM)
- Tài khoản Gmail để gửi hóa đơn
- File Google Sheets mẫu (hoặc tạo mới) để lưu trữ dữ liệu
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/3440](https://n8n.io/workflows/3440)
2. Nhấn nút "Download" để tải file JSON workflow
3. Trong n8n Editor, nhấn vào "Import from File" và chọn file vừa tải về

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "On form submission"**:
   - Cấu hình form để nhận file PDF từ khách hàng
   - Đảm bảo form có trường upload file PDF

2. **Node "Custom LLM Subnode"**:
   - Cấu hình credentials cho OpenAI
   - Đặt model LLM phù hợp (ví dụ: gpt-4o-mini)
   - Cập nhật prompt phù hợp với yêu cầu của bạn

3. **Node "Client Usage Log"**:
   - Cấu hình credentials Google Sheets
   - Điền ID của Google Sheet nơi lưu trữ dữ liệu
   - Đảm bảo sheet có các cột: Client ID, Date, Tokens Used, Cost

4. **Node "Send Invoice"**:
   - Cấu hình credentials Gmail
   - Đặt template email hóa đơn phù hợp
   - Kiểm tra địa chỉ email nhận hóa đơn

5. **Node "Every End of Month"**:
   - Cấu hình lịch chạy hàng tháng (ví dụ: ngày 28 hàng tháng)
   - Đảm bảo thời gian chạy phù hợp với khu vực của bạn

#### 3. Kích hoạt ⚡️
1. Chạy test với dữ liệu mẫu để kiểm tra toàn bộ quy trình
2. Kiểm tra Google Sheet để xác nhận dữ liệu được ghi nhận đúng
3. Kiểm tra email để xác nhận hóa đơn được gửi đúng
4. Sau khi kiểm tra thành công, bật Active workflow

### ✍️ Mẹo & gợi ý nâng cao
1. **Kết hợp với Slack/Teams**: Thêm node để thông báo khi có khách hàng mới hoặc khi hóa đơn được gửi
2. **Báo cáo định kỳ**: Thêm node để tạo báo cáo tổng hợp chi phí hàng quý
3. **Xử lý lỗi**: Thêm node xử lý lỗi để thông báo khi có vấn đề xảy ra trong quy trình
4. **Tích hợp với CRM**: Kết nối với hệ thống CRM để tự động cập nhật thông tin khách hàng

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa hoàn toàn quy trình theo dõi và tính toán chi phí sử dụng LLM cho từng khách hàng. Với tích hợp Google Sheets và gửi hóa đơn tự động, quy trình trở nên hiệu quả hơn đáng kể so với cách làm thủ công. Hãy thử ngay và tiết kiệm thời gian cho công việc quan trọng hơn!