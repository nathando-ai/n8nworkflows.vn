---
title: "📊 Tự động hóa báo cáo hiệu suất quảng cáo Facebook hàng tuần với AI và gửi email"
description: "Workflow n8n tự động hóa báo cáo hiệu suất quảng cáo Facebook hàng tuần, tổng hợp dữ liệu bằng AI và gửi email tự động đến khách hàng"
slug: "tu-dong-hoa-bao-cao-quang-cao-facebook-hang-tuan-voi-ai-va-gui-email"
tags: [n8n, automation, no-code, facebook-ads, ai-reporting]
keywords: [n8n workflow, tự động hóa báo cáo, facebook ads, ai summarization, pdf generation]
---

# 📊 Tự động hóa báo cáo hiệu suất quảng cáo Facebook hàng tuần với AI và gửi email

[Đoạn mở đầu: Phân tích nỗi đau thực tế của các sếp marketing khi phải làm thủ công báo cáo hàng tuần. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm 5-10 giờ mỗi tuần cho việc báo cáo thủ công
- Báo cáo chuyên nghiệp, tự động cập nhật dữ liệu mới nhất
- Tự động tổng hợp và phân tích hiệu suất quảng cáo bằng AI
- Gửi báo cáo định kỳ đến khách hàng một cách tự động
- Tạo PDF báo cáo chuyên nghiệp với thương hiệu của doanh nghiệp
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Facebook Ads Manager với quyền truy cập API
- API Key từ OpenAI (để tổng hợp và viết báo cáo bằng AI)
- API Key từ PDFCrowd (để tạo PDF báo cáo)
- Tài khoản Gmail đã được cấu hình trong n8n
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập trang [Workflow gốc](https://n8n.io/workflows/10441)
2. Click vào nút "Copy JSON" để sao chép cấu hình workflow
3. Trong n8n Editor, click vào "Import from Clipboard" và dán JSON đã sao chép

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Weekly Trigger"**:
   - Đặt lịch chạy workflow vào mỗi thứ Hai hàng tuần
   - Điều chỉnh thời gian chạy phù hợp với múi giờ của bạn

2. **Node "Fetch FB Data"**:
   - Cấu hình credentials Facebook Ads Manager
   - Thêm các tham số truy vấn cần thiết (campaign_id, date_preset, fields...)
   - Đảm bảo có quyền truy cập đầy đủ vào các chiến dịch quảng cáo

3. **Node "OpenAI"**:
   - Cấu hình API Key OpenAI
   - Chọn model "gpt-4.1-mini" (hoặc model khác phù hợp)
   - Tùy chỉnh prompt nếu cần thay đổi cách AI phân tích dữ liệu

4. **Node "Generate PDF"**:
   - Cấu hình API Key PDFCrowd
   - Điều chỉnh template PDF nếu cần thay đổi thiết kế
   - Thêm logo và thương hiệu của doanh nghiệp

5. **Node "Send Email"**:
   - Cấu hình credentials Gmail
   - Điền địa chỉ email nhận báo cáo
   - Tùy chỉnh tiêu đề và nội dung email

#### 3. Kích hoạt ⚡️
1. Test run dữ liệu mẫu để đảm bảo workflow hoạt động đúng
2. Kiểm tra email để đảm bảo báo cáo được gửi đúng định dạng
3. Bật Active workflow sau khi đã kiểm tra kỹ

### ✍️ Mẹo & gợi ý nâng cao
1. **Kết hợp với Slack/Teams**: Thêm node để gửi thông báo khi báo cáo được tạo thành công
2. **Lưu log hoạt động**: Thêm node để lưu log các lần chạy workflow
3. **Tùy chỉnh báo cáo**: Thêm các chỉ số quan trọng khác vào báo cáo (CTR, CPC...)
4. **Xử lý lỗi tự động**: Thêm node để xử lý các trường hợp lỗi trong quá trình chạy

### 📌 Kết luận
Workflow này giúp các sếp marketing tiết kiệm thời gian quý giá, tự động hóa quy trình báo cáo hàng tuần và cung cấp dữ liệu chính xác đến khách hàng. Hãy thử ngay và nâng cao hiệu suất làm việc của đội ngũ marketing!