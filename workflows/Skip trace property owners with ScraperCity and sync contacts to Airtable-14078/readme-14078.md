---
title: "🚀 Tự động hóa tra cứu chủ sở hữu tài sản với ScraperCity và đồng bộ dữ liệu lên Airtable"
description: "Hướng dẫn tự động hóa quy trình tra cứu thông tin chủ sở hữu tài sản bằng ScraperCity và đồng bộ dữ liệu lên Airtable để quản lý danh sách liên hệ hiệu quả"
slug: "tu-dong-hoa-tra-cuu-chu-so-huu-tai-san-scrapercity-airtable"
tags: [n8n, automation, no-code, lead generation, airtable]
keywords: [n8n workflow, tự động hóa, tra cứu chủ sở hữu, ScraperCity, Airtable]
---

# 🚀 Tự động hóa tra cứu chủ sở hữu tài sản với ScraperCity và đồng bộ dữ liệu lên Airtable

[Các sếp] có bao giờ phải tra cứu thông tin chủ sở hữu tài sản một cách thủ công không? Quá trình này thường tốn thời gian, dễ gây lỗi và không thể thực hiện hàng loạt. Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình từ tra cứu đến đồng bộ dữ liệu lên Airtable, giúp tiết kiệm thời gian và nâng cao hiệu quả quản lý danh sách liên hệ.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động hóa toàn bộ quy trình tra cứu chủ sở hữu tài sản
- Đồng bộ dữ liệu lên Airtable một cách tự động và chính xác
- Tiết kiệm thời gian và giảm thiểu lỗi thủ công
- Quản lý danh sách liên hệ hiệu quả với dữ liệu được chuẩn hóa
- Thực hiện hàng loạt tra cứu mà không cần can thiệp thủ công
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản ScraperCity với API Key
- Tài khoản Airtable với Base ID và Table ID
- Dữ liệu đầu vào bao gồm tên, số điện thoại hoặc email của chủ sở hữu cần tra cứu
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor của bạn
2. Nhấp vào nút "Import from URL" và dán link: [https://n8n.io/workflows/14078](https://n8n.io/workflows/14078)
3. Hoặc tải file JSON về và chọn "Import from File"

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Tạo Credential cho ScraperCity API Key**:
   - Trong n8n Credentials, tạo một credential mới loại **HTTP Header Auth**
   - Đặt tên credential là `ScraperCity API Key`
   - Header name: `Authorization`
   - Value: `Bearer YOUR_KEY` (thay YOUR_KEY bằng API Key thực của bạn)

2. **Cấu hình đầu vào tra cứu**:
   - Mở node **Configure Search Inputs**
   - Điền thông tin chủ sở hữu cần tra cứu (tên, số điện thoại hoặc email)
   - Có thể điều chỉnh `maxResults` (mặc định 3) để kiểm soát số lượng kết quả trả về

3. **Cấu hình Airtable**:
   - Trong node **Sync Contacts to Airtable**, kết nối credential Airtable của bạn
   - Đặt đúng Base ID và Table ID
   - Đảm bảo bảng Airtable có các cột: Full Name, Phone, Email, Address, City, State, ZIP, Age

#### 3. Kích hoạt ⚡️
1. Thực hiện test run với dữ liệu mẫu để kiểm tra workflow
2. Sau khi kiểm tra thành công, bật Active workflow để chạy tự động

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Telegram để nhận thông báo khi workflow hoàn thành
- Lưu log các kết quả tra cứu để theo dõi lịch sử
- Tự động gửi báo cáo định kỳ về danh sách liên hệ mới được cập nhật
- Kết hợp với các công cụ khác để thực hiện các hành động tiếp theo với danh sách liên hệ

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa toàn bộ quy trình tra cứu chủ sở hữu tài sản và đồng bộ dữ liệu lên Airtable một cách hiệu quả. Với việc giảm thiểu công việc thủ công và tăng độ chính xác, các sếp có thể tập trung vào các nhiệm vụ quan trọng hơn trong quản lý danh sách liên hệ. Hãy áp dụng ngay để nâng cao hiệu quả công việc của mình!