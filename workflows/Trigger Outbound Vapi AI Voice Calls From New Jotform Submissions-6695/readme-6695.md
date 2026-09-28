---
title: "📞 Tự động gọi điện thoại AI từ dữ liệu Jotform - Workflow n8n hoàn chỉnh"
description: "Hướng dẫn tự động hóa cuộc gọi điện thoại AI từ dữ liệu Jotform bằng workflow n8n. Tiết kiệm thời gian và nâng cao trải nghiệm khách hàng với cuộc gọi tự động hóa thông minh."
slug: "tu-dong-goi-dien-thoai-ai-tu-jotform"
tags: [n8n, automation, no-code, ai, vapi, jotform]
keywords: [n8n workflow, tự động hóa cuộc gọi, ai voice call, vapi, jotform]
---

# 📞 Tự động gọi điện thoại AI từ dữ liệu Jotform - Workflow n8n hoàn chỉnh

[Các sếp đang mệt mỏi với việc phải gọi điện thoại thủ công cho hàng trăm khách hàng mỗi ngày? Workflow này sẽ giúp các sếp tự động hóa quy trình này hoàn toàn bằng công nghệ AI, tiết kiệm thời gian và nâng cao hiệu quả chăm sóc khách hàng.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn**: Không cần can thiệp thủ công cho mỗi cuộc gọi
- **Tiết kiệm thời gian**: Xử lý hàng trăm cuộc gọi trong ngày mà không phải chờ đợi
- **Trải nghiệm khách hàng tốt hơn**: Cuộc gọi được thực hiện bởi AI với giọng nói tự nhiên
- **Dữ liệu được quản lý tốt**: Tất cả cuộc gọi và phản hồi được lưu trữ và phân tích
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Jotform với API đã kích hoạt trong n8n
- Form Jotform đã xuất bản chứa trường số điện thoại
- Tài khoản Vapi với số điện thoại đã kết nối
- Assistant đã tạo sẵn trong Vapi
- API key của Vapi
- Tài khoản OpenAI với API key
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [trang workflow gốc](https://n8n.io/workflows/6695)
2. Click vào nút "Download" để tải file JSON
3. Trong n8n Editor, click vào "Import from File" và chọn file JSON vừa tải về

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "JotForm Trigger"**:
   - Kích hoạt credentials "jotFormApi"
   - Chọn form Jotform chứa trường số điện thoại

2. **Node "Set fields"**:
   - Thiết lập các trường bắt buộc cho Vapi:
     - Phone number ID (ID số điện thoại trong tài khoản Vapi)
     - Assistant ID (ID của assistant đã tạo trong Vapi)
     - Vapi API key (API key của tài khoản Vapi)

3. **Node "OpenAI Chat Model"**:
   - Kích hoạt credentials "openAiApi"
   - Chọn model "gpt-4.1" hoặc model tương thích khác

4. **Node "Information Extractor"**:
   - Cấu hình để trích xuất thông tin cần thiết từ dữ liệu Jotform

#### 3. Kích hoạt ⚡️
1. Test run với dữ liệu mẫu để đảm bảo workflow hoạt động đúng
2. Bật Active workflow để bắt đầu tự động hóa cuộc gọi

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Telegram để nhận thông báo khi có cuộc gọi mới
- Lưu log cuộc gọi vào Google Sheets hoặc cơ sở dữ liệu
- Thiết lập báo cáo định kỳ về hiệu suất cuộc gọi
- Tích hợp với CRM để cập nhật trạng thái khách hàng sau cuộc gọi

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa hoàn toàn quy trình gọi điện thoại AI từ dữ liệu Jotform, nâng cao hiệu quả chăm sóc khách hàng và tiết kiệm thời gian quý giá. Hãy áp dụng ngay để thấy được sự khác biệt trong hoạt động kinh doanh của mình!