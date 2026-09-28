```yaml
---
title: "🚀 Theo dõi danh mục tiền điện tử của bạn trong Airtable - Tự động hóa hoàn toàn"
description: "Hướng dẫn chi tiết cách tự động theo dõi giá trị danh mục tiền điện tử của bạn trong Airtable bằng n8n. Tiết kiệm thời gian và giảm thiểu lỗi thủ công."
slug: "theo-doi-danh-muc-tien-dien-tu-trong-airtable"
tags: [n8n, automation, no-code, airtable, cryptocurrency]
keywords: [n8n workflow, tự động hóa, airtable, tiền điện tử, coinGecko]
---
```

# 🚀 Theo dõi danh mục tiền điện tử của bạn trong Airtable - Tự động hóa hoàn toàn

[Đoạn mở đầu: Phân tích nỗi đau thực tế của các sếp khi theo dõi danh mục tiền điện tử thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động cập nhật giá trị danh mục tiền điện tử hàng giờ
- Giảm thiểu lỗi thủ công
- Theo dõi lịch sử giá trị danh mục trong Airtable
- Nhận cảnh báo khi giá trị danh mục thay đổi đáng kể
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Airtable với bảng chứa danh mục tiền điện tử của bạn
- API Key từ CoinGecko
- Credentials cho Airtable trong n8n
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [workflow gốc](https://n8n.io/workflows/859)
2. Copy JSON workflow
3. Trong n8n Editor, nhấn "Import from Clipboard" và dán JSON

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node CoinGecko**:
   - Chọn operation "get"
   - Điền ID của đồng tiền điện tử bạn muốn theo dõi

2. **Node Get Portfolio**:
   - Chọn credentials Airtable của bạn
   - Điền Base ID và Table Name chứa danh mục tiền điện tử

3. **Node Set**:
   - Cấu hình các biến cần thiết cho workflow

4. **Node Run Top of Hour**:
   - Đặt lịch chạy workflow hàng giờ (ví dụ: "0 * * * *")

5. **Node Get Portfolio Values**:
   - Chọn credentials Airtable của bạn
   - Điền Base ID và Table Name chứa danh mục tiền điện tử

6. **Node Determine Total Value**:
   - Kiểm tra và điều chỉnh hàm tính toán nếu cần

7. **Node Update Values**:
   - Chọn credentials Airtable của bạn
   - Điền Base ID và Table Name chứa danh mục tiền điện tử

8. **Node Append Portfolio Value**:
   - Chọn credentials Airtable của bạn
   - Điền Base ID và Table Name để lưu lịch sử giá trị

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu.
- Bật Active workflow.

### ✍️ Mẹo & gợi ý nâng cao
- Thêm cảnh báo Slack/Telegram khi giá trị danh mục thay đổi đáng kể
- Tự động gửi báo cáo hàng tuần về hiệu suất danh mục
- Kết hợp với các công cụ phân tích dữ liệu khác để đánh giá hiệu suất đầu tư
- Thêm các chỉ số kỹ thuật để đánh giá xu hướng thị trường

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm thời gian đáng kể khi theo dõi danh mục tiền điện tử. Bằng cách tự động hóa quy trình này, các sếp có thể tập trung vào các quyết định đầu tư quan trọng hơn. Hãy thử ngay và nâng cao hiệu suất đầu tư của bạn!