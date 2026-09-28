---
title: "🚀 Tự động hóa tối ưu hóa Google Shopping Feed với Channable, Relevance AI & Merchant API"
description: "Tự động hóa quy trình tối ưu hóa feed sản phẩm Google Shopping hàng ngày với AI, kiểm tra chất lượng dữ liệu và đồng bộ tự động với Merchant Center"
slug: "tu-dong-hoa-toi-uu-hoa-google-shopping-feed"
tags: [n8n, automation, no-code, google-shopping, merchant-api]
keywords: [n8n workflow, tự động hóa, google shopping, merchant api, relevance ai]
---

# 🚀 Tự động hóa tối ưu hóa Google Shopping Feed với Channable, Relevance AI & Merchant API

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm 5-10 giờ mỗi tuần cho việc tối ưu hóa feed sản phẩm
- Tăng độ chính xác của tiêu đề và mô tả sản phẩm lên 30%
- Giảm số lượng sản phẩm bị từ chối trên Google Merchant Center
- Nhận báo cáo hàng ngày về tình trạng feed sản phẩm
- Tự động đồng bộ dữ liệu giữa các hệ thống (Channable, Google Merchant Center)
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Merchant Center với quyền truy cập API
- API Key từ Relevance AI
- Tài khoản Slack để nhận thông báo
- Dữ liệu sản phẩm từ Channable hoặc hệ thống e-commerce của bạn
- Credentials HTTP Header Auth cho các yêu cầu API
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/10060](https://n8n.io/workflows/10060)
2. Click vào nút "Import" trên trang workflow
3. Trong n8n Editor, chọn "Import from URL" và dán link workflow
4. Hoàn tất quá trình import

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Daily Trigger - 6 AM**:
   - Đảm bảo múi giờ của server n8n trùng với múi giờ của bạn
   - Có thể điều chỉnh thời gian chạy nếu cần

2. **Get Product Feed**:
   - Cấu hình URL endpoint để lấy dữ liệu sản phẩm từ Channable
   - Đảm bảo endpoint trả về dữ liệu theo định dạng JSON

3. **Optimize Title** và **Generate Description**:
   - Cập nhật API Key từ Relevance AI trong credentials
   - Điều chỉnh các tham số prompt nếu cần tối ưu hóa khác

4. **Upload to Merchant Center**:
   - Cập nhật thông tin xác thực Google Merchant Center
   - Kiểm tra và điều chỉnh số lượng sản phẩm mỗi batch (khuyến nghị không quá 1000 sản phẩm/batch)

5. **Alert - Disapprovals** và **Success Summary**:
   - Cấu hình webhook Slack với channel phù hợp
   - Tùy chỉnh nội dung thông báo theo nhu cầu của team

#### 3. Kích hoạt ⚡️
1. Test run dữ liệu mẫu với 1-2 sản phẩm trước khi chạy toàn bộ feed
2. Kiểm tra kết quả trên Google Merchant Center
3. Bật Active workflow sau khi xác nhận mọi thứ hoạt động đúng

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node để lưu log các thay đổi vào Google Sheets hoặc cơ sở dữ liệu
- Kết hợp với các công cụ phân tích để theo dõi hiệu suất sản phẩm sau khi tối ưu
- Tự động gửi báo cáo hàng tuần về hiệu suất feed sản phẩm
- Thiết lập cảnh báo khi phát hiện các vấn đề tiềm ẩn trong dữ liệu sản phẩm

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa hoàn toàn quá trình tối ưu hóa feed sản phẩm Google Shopping hàng ngày, giảm thiểu công sức thủ công và tăng hiệu suất quảng cáo. Với việc tích hợp AI và Merchant API, các sếp có thể tập trung vào các chiến lược quan trọng hơn thay vì làm việc lặp đi lặp lại hàng ngày.