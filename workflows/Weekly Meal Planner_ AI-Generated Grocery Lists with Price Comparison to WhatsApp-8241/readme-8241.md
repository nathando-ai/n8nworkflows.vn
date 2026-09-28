---
title: "🍽️ Tự động hóa bữa ăn hàng tuần: Tạo danh sách mua sắm AI + so sánh giá gửi WhatsApp"
description: "Hướng dẫn tự động hóa workflow n8n tạo kế hoạch bữa ăn hàng tuần bằng AI, so sánh giá và gửi danh sách mua sắm qua WhatsApp - tiết kiệm thời gian và tối ưu chi phí"
slug: "tu-dong-hoa-ke-hoach-bua-an-hang-tuan-ai-whatsapp"
tags: [n8n, automation, no-code, ai, productivity]
keywords: [n8n workflow, tự động hóa bữa ăn, ai meal planner, so sánh giá, whatsapp automation]
---

# 🍽️ Tự động hóa bữa ăn hàng tuần: Tạo danh sách mua sắm AI + so sánh giá gửi WhatsApp

[Các sếp nhà hàng, quán ăn hoặc gia đình thường phải tốn nhiều thời gian để lên kế hoạch bữa ăn hàng tuần và so sánh giá hàng ngày. Workflow này sẽ giúp các sếp tự động hóa toàn bộ quá trình này chỉ trong vài phút, tiết kiệm thời gian và tối ưu hóa chi phí mua sắm.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động hóa toàn bộ quá trình lên kế hoạch bữa ăn hàng tuần
- **Tối ưu chi phí**: So sánh giá từ nhiều nguồn để tìm được giá tốt nhất
- **Tiện lợi**: Nhận danh sách mua sắm qua WhatsApp ngay lập tức
- **Chính xác**: Kế hoạch bữa ăn được tạo bởi AI với dữ liệu chính xác
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Fillout (để thu thập dữ liệu về sở thích bữa ăn)
- API key OpenAI (để tạo kế hoạch bữa ăn bằng AI)
- Tài khoản PDF4me (để chuyển đổi HTML thành PDF)
- Số điện thoại WhatsApp (để gửi danh sách mua sắm)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [link workflow gốc](https://n8n.io/workflows/8241)
2. Click vào nút "Import" ở góc trên bên phải
3. Copy toàn bộ JSON workflow và dán vào n8n Editor của bạn

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Fetch Fillout Submission (HTTP)"**:
   - Thêm credentials Fillout
   - Cập nhật URL API của Fillout form (nếu có thay đổi)

2. **Node "OpenAI Chat (HTTP)"**:
   - Thêm credentials OpenAI
   - Kiểm tra và điều chỉnh prompt trong node "Prep Prompt from Fillout" nếu cần

3. **Node "PDF4me: HTML to PDF"**:
   - Thêm credentials PDF4me
   - Kiểm tra và điều chỉnh HTML template trong node "Build HTML for PDF" nếu cần

4. **Node cuối cùng (gửi WhatsApp)**:
   - Cập nhật số điện thoại nhận tin nhắn
   - Kiểm tra và điều chỉnh nội dung tin nhắn nếu cần

#### 3. Kích hoạt ⚡️
1. Click vào nút "Execute Node" trên node "Trigger: Weekly Meal Workflow" để test workflow
2. Kiểm tra kết quả trên WhatsApp
3. Sau khi test thành công, bật workflow bằng cách click vào nút "Activate" ở góc trên bên phải

### ✍️ Mẹo & gợi ý nâng cao
1. **Tự động hóa định kỳ**: Thiết lập workflow chạy tự động vào mỗi thứ Hai hàng tuần
2. **Kết hợp với Google Sheets**: Thêm node để lưu trữ lịch sử mua sắm
3. **Thêm tính năng so sánh giá**: Kết nối với các API giá hàng ngày khác
4. **Tùy chỉnh template**: Điều chỉnh HTML template để phù hợp với thương hiệu của bạn

### 📌 Kết luận
Workflow này sẽ giúp các sếp tiết kiệm thời gian đáng kể trong việc lên kế hoạch bữa ăn hàng tuần. Bằng cách kết hợp AI, so sánh giá và tự động gửi danh sách mua sắm qua WhatsApp, các sếp có thể tối ưu hóa chi phí và tập trung vào những việc quan trọng hơn. Hãy thử ngay và trải nghiệm sự tiện lợi mà tự động hóa mang lại!