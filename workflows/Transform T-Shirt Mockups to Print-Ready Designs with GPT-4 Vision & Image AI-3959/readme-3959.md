---
title: "🚀 Tự động hóa thiết kế áo thun với GPT-4 Vision & Image AI"
description: "Hướng dẫn tự động hóa quy trình chuyển đổi mockup áo thun thành thiết kế in sẵn sàng sử dụng trí tuệ nhân tạo GPT-4 Vision và Image AI"
slug: "tu-dong-hoa-thiet-ke-ao-thun-voi-gpt-4-vision-image-ai"
tags: [n8n, automation, no-code, design, ai]
keywords: [n8n workflow, tự động hóa, thiết kế áo thun, GPT-4 Vision, Image AI]
---

# 🚀 Tự động hóa thiết kế áo thun với GPT-4 Vision & Image AI

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian thiết kế: Tự động hóa quy trình từ 30-50% thời gian làm thủ công
- Tăng tính cá nhân hóa: Tạo ra nhiều phiên bản thiết kế khác nhau từ cùng một mockup
- Tăng hiệu quả làm việc: Xử lý hàng loạt thiết kế đồng thời
- Tiết kiệm chi phí: Giảm nhu cầu tuyển dụng nhân viên thiết kế chuyên nghiệp
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản OpenAI với API key (cần GPT-4 Vision)
- URL của các mockup áo thun cần chuyển đổi
- Kiến thức cơ bản về sử dụng n8n
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập trang workflow gốc: [Transform T-Shirt Mockups to Print-Ready Designs with GPT-4 Vision & Image AI](https://n8n.io/workflows/3959)
2. Nhấn nút "Copy JSON" để sao chép cấu hình workflow
3. Trong n8n Editor, nhấn nút "+" → "Import from JSON" và dán JSON đã sao chép

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "When chat message received"**:
   - Cấu hình webhook để nhận URL ảnh mockup
   - Đảm bảo webhook có thể truy cập được từ bên ngoài

2. **Node "OpenAI"**:
   - Chọn credentials "openAiApi" đã được cấu hình
   - Đảm bảo tài khoản OpenAI có đủ credit để sử dụng GPT-4 Vision

3. **Node "OpenAI Chat Model"**:
   - Chọn model "gpt-4o-mini" hoặc "gpt-4-vision-preview" tùy theo nhu cầu
   - Điều chỉnh prompt trong node "AI Agent" để phù hợp với yêu cầu thiết kế

4. **Node "Convert to File"**:
   - Đảm bảo URL ảnh được cung cấp là hợp lệ và có thể truy cập được

#### 3. Kích hoạt ⚡️
1. Test run với một URL ảnh mẫu để kiểm tra quy trình hoạt động
2. Sau khi xác nhận hoạt động đúng, bật Active workflow
3. Gửi URL ảnh mockup qua webhook để bắt đầu quá trình chuyển đổi

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Telegram để nhận thông báo khi thiết kế hoàn thành
- Lưu log các phiên thiết kế để theo dõi quá trình phát triển
- Tạo báo cáo định kỳ về số lượng thiết kế được tạo và thời gian trung bình xử lý
- Kết hợp với các công cụ thiết kế khác để hoàn thiện thiết kế cuối cùng

### 📌 Kết luận
Workflow này cung cấp giải pháp toàn diện cho việc tự động hóa quy trình chuyển đổi mockup áo thun thành thiết kế in sẵn sàng sử dụng trí tuệ nhân tạo. Với việc áp dụng workflow này, các sếp có thể tiết kiệm thời gian đáng kể và tập trung vào các nhiệm vụ sáng tạo hơn trong quá trình thiết kế sản phẩm.