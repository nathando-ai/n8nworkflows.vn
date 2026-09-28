---
title: "🚀 Tự động hóa thu thập tin tuyển dụng mỗi 6 giờ với n8n + Scrapeless"
description: "Hướng dẫn chi tiết cách tự động hóa thu thập tin tuyển dụng từ website bất kỳ mỗi 6 giờ, xử lý dữ liệu và lưu vào Google Sheets hoàn toàn không cần code."
slug: "tu-dong-hoa-thu-thap-tin-tuyen-dung-moi-6-gio"
tags: [n8n, automation, no-code, scrapeless, google-sheets]
keywords: [n8n workflow, tự động hóa tuyển dụng, scrapeless, google sheets, no-code]
---

# 🚀 Tự động hóa thu thập tin tuyển dụng mỗi 6 giờ với n8n + Scrapeless

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm 60% thời gian thủ công thu thập tin tuyển dụng
- Dữ liệu tuyển dụng được xử lý tự động, chính xác và cập nhật liên tục
- Dễ dàng tích hợp với các công cụ phân tích dữ liệu khác
- Hoạt động liên tục 24/7 mà không cần can thiệp
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Scrapeless (để crawl dữ liệu)
- Tài khoản Google Cloud Platform (để kết nối Google Sheets)
- Quyền truy cập vào website cần thu thập dữ liệu
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor của bạn
2. Click vào "Import from URL" và nhập link: https://n8n.io/workflows/5737
3. Hoặc copy JSON từ link trên và paste vào n8n Editor

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Schedule Trigger**:
   - Đặt thời gian chạy (mặc định là mỗi 6 giờ)
   - Có thể điều chỉnh theo nhu cầu của bạn

2. **Scrapeless**:
   - Cấu hình credentials "scrapelessApi"
   - Thiết lập URL của website cần crawl
   - Cấu hình selector để trích xuất dữ liệu cần thiết

3. **Code Nodes (Code, Code1, Code2)**:
   - Đây là các hàm xử lý dữ liệu thô
   - Các sếp có thể chỉnh sửa logic xử lý theo nhu cầu
   - Đảm bảo đầu ra của Code2 là dữ liệu đã được xử lý và định dạng đúng

4. **Google Sheets**:
   - Cấu hình credentials "googleSheetsOAuth2Api"
   - Chỉ định Spreadsheet ID và tên Sheet cần lưu dữ liệu
   - Đảm bảo có quyền ghi dữ liệu vào Google Sheets

#### 3. Kích hoạt ⚡️
1. Test run dữ liệu mẫu để đảm bảo workflow hoạt động đúng
2. Bật Active workflow để chạy tự động

### ✍️ Mẹo & gợi ý nâng cao
1. Thêm node Slack/Telegram để nhận thông báo khi có tin tuyển dụng mới
2. Kết hợp với node Email để gửi báo cáo hàng tuần
3. Thêm node LLM để phân tích dữ liệu tuyển dụng
4. Lưu log hoạt động để theo dõi hiệu suất workflow

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm thời gian đáng kể trong việc thu thập và xử lý dữ liệu tuyển dụng. Với khả năng tự động hóa hoàn toàn, các sếp có thể tập trung vào các nhiệm vụ quan trọng hơn trong quá trình tuyển dụng. Hãy thử ngay và tối ưu hóa workflow theo nhu cầu của mình!