---
title: "🚀 Tự động hóa Hệ thống Thông tin Website & Điểm số Khách hàng với ScrapeGraphAI, HubSpot và Slack"
description: "Hướng dẫn chi tiết cách tự động thu thập thông tin công ty, phân tích hành vi khách truy cập và tự động cập nhật CRM với điểm số khách hàng thông qua n8n workflow."
slug: "tu-dong-hoa-he-thong-thong-tin-website-diem-so-khach-hang"
tags: [n8n, automation, no-code, lead-generation, ai-summarization]
keywords: [n8n workflow, tự động hóa, lead scoring, ScrapeGraphAI, HubSpot, Slack]
---

# 🚀 Tự động hóa Hệ thống Thông tin Website & Điểm số Khách hàng với ScrapeGraphAI, HubSpot và Slack

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

Các sếp đang gặp khó khăn khi phải theo dõi hàng nghìn khách truy cập website mỗi ngày, phân tích thông tin công ty và đánh giá tiềm năng khách hàng một cách thủ công. Quá trình này tốn thời gian, dễ xảy ra sai sót và không thể thực hiện liên tục 24/7.

Workflow này sẽ giúp các sếp tự động hóa toàn bộ quy trình từ thu thập dữ liệu khách truy cập đến cập nhật CRM với điểm số khách hàng, chỉ trong vài bước đơn giản.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm 80% thời gian phân tích khách hàng
- Tăng độ chính xác trong đánh giá tiềm năng khách hàng lên 95%
- Tự động cập nhật thông tin khách hàng vào CRM ngay lập tức
- Nhận cảnh báo thời gian thực về khách hàng tiềm năng
- Tăng hiệu quả làm việc của đội ngũ sales lên 30%
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản HubSpot với API key
- Tài khoản Slack với quyền gửi thông báo
- API key từ ScrapeGraphAI
- Mã theo dõi website đã được cài đặt
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor của bạn
2. Nhấp vào "Import from URL" và dán link: https://n8n.io/workflows/6570
3. Hoặc tải file JSON về và chọn "Import from File"

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Webhook Trigger**:
   - Cấu hình path: `/visitor-tracking`
   - Phương thức: `POST`
   - Đảm bảo URL webhook đã được cấu hình đúng trong mã theo dõi website

2. **ScrapeGraphAI - Company Intel**:
   - Thêm credentials của ScrapeGraphAI
   - Đảm bảo API key có quyền truy cập đầy đủ

3. **Visitor Enricher**:
   - Kiểm tra logic trong node Code để đảm bảo dữ liệu được kết hợp đúng cách
   - Cập nhật các tham số phân tích hành vi nếu cần

4. **Lead Scorer**:
   - Điều chỉnh trọng số điểm cho từng tiêu chí đánh giá
   - Cập nhật danh sách ngành nghề mục tiêu

5. **CRM Update**:
   - Thêm credentials của HubSpot
   - Ánh xạ các trường dữ liệu tùy chỉnh trong HubSpot
   - Cấu hình quy tắc phân bổ lead

6. **Sales Alert**:
   - Thêm credentials của Slack
   - Cấu hình ngưỡng cảnh báo
   - Tùy chỉnh mẫu thông báo

#### 3. Kích hoạt ⚡️
1. Chạy test với dữ liệu mẫu để kiểm tra toàn bộ workflow
2. Kích hoạt workflow bằng cách nhấp vào nút "Active"
3. Kiểm tra Slack để đảm bảo nhận được cảnh báo test

### ✍️ Mẹo & gợi ý nâng cao
1. Kết hợp với hệ thống email marketing để gửi thông báo tự động cho khách hàng tiềm năng
2. Thêm node để lưu log các hoạt động quan trọng vào Google Sheets
3. Cấu hình gửi báo cáo hàng tuần về hiệu suất lead generation
4. Kết nối với hệ thống chatbot để tự động trả lời các truy vấn từ khách hàng tiềm năng

### 📌 Kết luận
Workflow này sẽ giúp các sếp tự động hóa hoàn toàn quy trình thu thập thông tin khách hàng, đánh giá tiềm năng và cập nhật CRM, giúp đội ngũ sales tập trung vào các hoạt động quan trọng hơn. Hãy áp dụng ngay để tăng hiệu quả làm việc của doanh nghiệp!