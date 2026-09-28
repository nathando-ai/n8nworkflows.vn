---
title: "🚀 Tự động phân loại email VIP Outlook bằng Excel, GPT-4o và Microsoft To Do"
description: "Workflow n8n tự động hóa phân loại email quan trọng từ Outlook, phân tích độ khẩn cấp bằng AI và tạo task trong Microsoft To Do - tiết kiệm thời gian 80% cho các sếp"
slug: "tu-dong-phan-loai-email-vip-outlook"
tags: [n8n, automation, no-code, outlook, microsoft, ai, gpt-4o]
keywords: [n8n workflow, tự động hóa email, phân loại email, ai phân tích, microsoft to do]
---

# 🚀 Tự động phân loại email VIP Outlook bằng Excel, GPT-4o và Microsoft To Do

[Các sếp] có bao giờ phải ngồi hàng giờ mỗi ngày để đọc hàng trăm email chỉ để tìm ra những tin nhắn quan trọng? Với workflow này, hệ thống sẽ tự động phân loại email VIP từ Outlook, phân tích độ khẩn cấp bằng AI và tạo task trong Microsoft To Do - tiết kiệm thời gian 80% cho các sếp.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động xử lý hàng trăm email mỗi ngày
- **Phân loại chính xác**: Chỉ tập trung vào email quan trọng từ danh sách VIP
- **Phân tích thông minh**: AI GPT-4o tự động đánh giá độ khẩn cấp của email
- **Hệ thống hóa**: Tạo task tự động trong Microsoft To Do cho email quan trọng
- **Báo cáo lỗi**: Nhận thông báo ngay khi có lỗi xảy ra trong quá trình xử lý
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Microsoft Outlook (đã kích hoạt API)
- Tài khoản Microsoft Excel (đã kích hoạt API)
- API key OpenAI (đã kích hoạt GPT-4o)
- Tài khoản Microsoft To Do
- Danh sách email VIP trong file Excel (cột đầu tiên chứa địa chỉ email)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [workflow gốc trên n8n.io](https://n8n.io/workflows/15895)
2. Click vào nút "Import" ở góc trên bên phải
3. Trong n8n Editor, chọn "Import from URL" và dán link workflow
4. Hoặc copy JSON từ trang web và paste vào n8n Editor

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Outlook Trigger**:
   - Kết nối với tài khoản Outlook chính xác
   - Đảm bảo đã kích hoạt API Outlook

2. **Excel: Read VIP Sheet**:
   - Kết nối với file Excel chứa danh sách VIP
   - Đảm bảo cột đầu tiên chứa địa chỉ email
   - Thay đổi tên sheet nếu cần (mặc định là "Sheet1")

3. **AI: Analyze Urgency**:
   - Kết nối với tài khoản OpenAI có API key
   - Đảm bảo đã kích hoạt GPT-4o
   - Có thể điều chỉnh prompt trong node này nếu cần

4. **Create VIP To Do Task**:
   - Kết nối với tài khoản Microsoft To Do chính xác
   - Có thể thay đổi danh sách To Do mặc định

5. **Send Error Email**:
   - Cấu hình địa chỉ email nhận thông báo lỗi
   - Có thể thay đổi nội dung email lỗi nếu cần

#### 3. Kích hoạt ⚡️
1. Sau khi cấu hình xong tất cả các node quan trọng, click vào nút "Activate" ở góc trên bên phải
2. Chạy test với 1 email mẫu để kiểm tra workflow
3. Sau khi xác nhận hoạt động bình thường, bật chế độ "Always On"

### ✍️ Mẹo & gợi ý nâng cao
1. **Kết hợp với Slack/Teams**: Thêm node gửi thông báo đến Slack/Teams khi có email quan trọng
2. **Lưu log xử lý**: Thêm node ghi log xử lý email vào Google Sheets/Excel
3. **Báo cáo hàng ngày**: Tạo workflow phụ để gửi báo cáo tổng hợp email đã xử lý hàng ngày
4. **Xử lý email đính kèm**: Thêm node xử lý các file đính kèm trong email quan trọng

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa hoàn toàn quá trình phân loại và xử lý email quan trọng, giảm thiểu thời gian xử lý thủ công và tăng hiệu suất làm việc. Với sự kết hợp của Excel, GPT-4o và Microsoft To Do, hệ thống đảm bảo email quan trọng luôn được xử lý kịp thời và chính xác. Hãy áp dụng ngay để trải nghiệm sự khác biệt!