---
title: "📈 Weekly Google Search Console SEO Pulse: Theo dõi hiệu suất Organic & Brand vs Non-Brand hàng tuần"
description: "Workflow n8n tự động hóa báo cáo SEO hàng tuần từ Google Search Console, phân tích hiệu suất Brand và Non-Brand, so sánh tuần trước với tuần trước đó"
slug: "weekly-google-search-console-seo-pulse"
tags: [n8n, automation, no-code, seo, google-search-console]
keywords: [n8n workflow, tự động hóa báo cáo SEO, Google Search Console, phân tích Brand vs Non-Brand]
---

# 📈 Weekly Google Search Console SEO Pulse: Theo dõi hiệu suất Organic & Brand vs Non-Brand hàng tuần

[Các sếp SEO đang gặp khó khăn khi phải theo dõi hiệu suất hàng tuần từ Google Search Console một cách thủ công. Báo cáo này thường mất nhiều thời gian và công sức để tổng hợp, phân tích và so sánh dữ liệu giữa các tuần. Workflow này sẽ giúp các sếp tự động hóa toàn bộ quy trình này trong vòng 5-10 phút, mang lại báo cáo hàng tuần đầy đủ và chuyên nghiệp.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động tổng hợp dữ liệu từ Google Search Console hàng tuần
- **Chính xác**: So sánh hiệu suất giữa tuần trước và tuần trước đó
- **Cá nhân hóa**: Phân tích riêng biệt hiệu suất Brand và Non-Brand
- **Hoạt động liên tục**: Nhận báo cáo hàng tuần mà không cần can thiệp
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Search Console với quyền truy cập dữ liệu
- Tài khoản Gmail để gửi báo cáo
- API Key từ Google Cloud Console (nếu sử dụng Google OAuth)
- Danh sách các từ khóa Brand cần theo dõi
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/7203](https://n8n.io/workflows/7203)
2. Click vào nút "Import" để tải xuống file JSON
3. Trong n8n Editor, click vào "Import from File" và chọn file JSON vừa tải xuống

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Schedule Trigger"**:
   - Cấu hình lịch chạy hàng tuần (thường là mỗi thứ Hai)
   - Thời gian chạy nên được đặt vào lúc dữ liệu Google Search Console đã cập nhật đầy đủ

2. **Node "Brand Filter" và "Brand Filter1"**:
   - Cập nhật danh sách các từ khóa Brand cần theo dõi trong phần code
   - Sử dụng biểu thức chính quy để phân loại chính xác các truy vấn Brand và Non-Brand

3. **Node "Brand/NB Pull" và "Brand/NB Pull1"**:
   - Kết nối với tài khoản Google Search Console
   - Đảm bảo có quyền truy cập đầy đủ vào dữ liệu

4. **Node "Weekly GSC Metric Email"**:
   - Kết nối với tài khoản Gmail để gửi báo cáo
   - Cập nhật địa chỉ email nhận báo cáo
   - Tùy chỉnh nội dung email theo nhu cầu

#### 3. Kích hoạt ⚡️
1. Test run dữ liệu mẫu để đảm bảo workflow hoạt động đúng
2. Kiểm tra email báo cáo để xác nhận dữ liệu được tổng hợp chính xác
3. Bật Active workflow để chạy hàng tuần

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp với Slack**: Thay thế node Gmail bằng node Slack để nhận báo cáo trên kênh Slack
- **Lưu log**: Thêm node lưu log để theo dõi lịch sử báo cáo
- **Gửi báo cáo định kỳ**: Cấu hình gửi báo cáo hàng tháng hoặc hàng quý
- **Phân tích sâu hơn**: Kết hợp với các công cụ phân tích khác để có cái nhìn toàn diện hơn về hiệu suất SEO

### 📌 Kết luận
Workflow này giúp các sếp SEO tiết kiệm thời gian và công sức trong việc theo dõi hiệu suất hàng tuần từ Google Search Console. Với báo cáo tự động hóa đầy đủ và chuyên nghiệp, các sếp có thể tập trung vào việc phân tích và tối ưu hóa chiến lược SEO một cách hiệu quả hơn. Hãy áp dụng ngay để nâng cao hiệu quả làm việc của đội ngũ SEO!