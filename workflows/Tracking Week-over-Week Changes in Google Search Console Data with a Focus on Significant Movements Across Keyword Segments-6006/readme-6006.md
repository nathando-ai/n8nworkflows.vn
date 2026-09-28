---
title: "🚀 Theo dõi thay đổi tuần tự trong dữ liệu Google Search Console - Phát hiện chuyển động lớn trong các phân khúc từ khóa"
description: "Tự động hóa theo dõi thay đổi tuần tự trong dữ liệu Google Search Console, phát hiện chuyển động lớn trong các phân khúc từ khóa và gửi báo cáo qua Slack/Email - Giúp các sếp tiết kiệm thời gian và tập trung vào những thay đổi quan trọng nhất."
slug: "theo-doi-thay-doi-tuần-tự-google-search-console"
tags: [n8n, automation, no-code, google-search-console, seo]
keywords: [n8n workflow, tự động hóa, google search console, seo, từ khóa, phân tích dữ liệu]
---

# 🚀 Theo dõi thay đổi tuần tự trong dữ liệu Google Search Console - Phát hiện chuyển động lớn trong các phân khúc từ khóa

[Đoạn mở đầu: Phân tích nỗi đau thực tế của các sếp SEO khi phải theo dõi thủ công thay đổi tuần tự trong dữ liệu Google Search Console. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code để phát hiện những thay đổi quan trọng nhất.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Tự động hóa quá trình theo dõi thay đổi tuần tự
- Phát hiện nhanh: Nhận thông báo ngay khi có thay đổi lớn trong dữ liệu
- Tập trung: Chỉ nhận báo cáo về những thay đổi quan trọng nhất
- Tăng hiệu quả: Giảm thời gian xử lý dữ liệu thủ công
- Tích hợp: Kết nối dễ dàng với Slack và Email
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Search Console với quyền truy cập dữ liệu
- Tài khoản Slack để nhận thông báo
- Tài khoản Gmail để nhận báo cáo
- API keys cho Google OAuth2, Slack và Gmail OAuth2
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/6006](https://n8n.io/workflows/6006)
2. Click vào nút "Import" để tải file JSON workflow
3. Hoặc copy toàn bộ nội dung JSON và paste vào n8n Editor

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node Schedule Trigger**:
   - Cấu hình thời gian chạy workflow (mặc định là mỗi thứ Hai hàng tuần)

2. **Node priorWeek và lastWeek (HTTP Request)**:
   - Cấu hình credentials cho Google OAuth2 API
   - Thay đổi URL API nếu cần (mặc định sử dụng Google Search Console API)
   - Cập nhật tham số ngày bắt đầu và kết thúc cho tuần trước và tuần trước tuần trước

3. **Node label và label1 (Code)**:
   - Cập nhật mã code để định dạng dữ liệu đầu ra theo yêu cầu của các sếp

4. **Node Flatten và Flatten1 (Code)**:
   - Cập nhật mã code để xử lý dữ liệu thô từ Google Search Console

5. **Node Define Weeks (Code)**:
   - Cập nhật mã code để định nghĩa các tuần cần so sánh

6. **Node Merge và Merge Weeks (Code)**:
   - Cập nhật mã code để hợp nhất dữ liệu từ các tuần

7. **Node Tag Brand / Recipes / Nonbrand (Code)**:
   - Cập nhật mã code để phân loại từ khóa theo phân khúc (brand, recipes, nonbrand)
   - Thay đổi logic phân loại nếu cần

8. **Node Top Movers Filter (Code)**:
   - Cập nhật ngưỡng thay đổi (mặc định là ±200 clicks và ±30%)
   - Thay đổi logic lọc nếu cần

9. **Node Top 25 Filter (Code)**:
   - Cập nhật mã code để lọc Top 25 thay đổi lớn nhất

10. **Node Top WoW Movers Alert (Slack)**:
    - Cấu hình credentials cho Slack API
    - Cập nhật thông tin kênh Slack để nhận thông báo
    - Thay đổi nội dung thông báo nếu cần

11. **Node Top WoW Movers Email (Gmail)**:
    - Cấu hình credentials cho Gmail OAuth2
    - Cập nhật địa chỉ email nhận báo cáo
    - Thay đổi nội dung email nếu cần

12. **Node Switch**:
    - Cập nhật logic chuyển đổi giữa các phân khúc từ khóa

#### 3. Kích hoạt ⚡️
1. Test run dữ liệu mẫu để đảm bảo workflow hoạt động đúng
2. Bật Active workflow để chạy tự động hàng tuần

### ✍️ Mẹo & gợi ý nâng cao
1. Kết hợp với các công cụ phân tích khác như Google Analytics để có cái nhìn toàn diện hơn về hiệu suất SEO
2. Thêm báo cáo định kỳ hàng tháng về xu hướng thay đổi dài hạn
3. Tích hợp với các công cụ quản lý dự án như Trello hoặc Asana để theo dõi các thay đổi quan trọng
4. Tạo bản sao lưu dữ liệu định kỳ để đảm bảo không mất thông tin quan trọng

### 📌 Kết luận
Workflow này giúp các sếp SEO tiết kiệm thời gian và tập trung vào những thay đổi quan trọng nhất trong dữ liệu Google Search Console. Bằng cách tự động hóa quá trình theo dõi và phát hiện thay đổi lớn, các sếp có thể nhanh chóng phản ứng và tối ưu hóa chiến lược SEO của mình. Hãy áp dụng ngay để nâng cao hiệu quả công việc của đội SEO!