---
title: "🚀 Tự động gửi lời mời kết nối LinkedIn cá nhân hóa cho người bình luận bài viết"
description: "Hướng dẫn tự động hóa gửi lời mời kết nối LinkedIn cá nhân hóa cho người bình luận bài viết của bạn bằng n8n và ConnectSafely.ai"
slug: "tu-dong-gui-loi-moi-ket-noi-linkedin-ca-nhan-hoa"
tags: [n8n, automation, no-code, LinkedIn, lead nurturing]
keywords: [n8n workflow, tự động hóa LinkedIn, gửi lời mời kết nối, ConnectSafely.ai]
---

# 🚀 Tự động gửi lời mời kết nối LinkedIn cá nhân hóa cho người bình luận bài viết

[Các sếp] có biết rằng mỗi ngày có hàng nghìn người bình luận bài viết LinkedIn của bạn, nhưng chỉ có một phần nhỏ được bạn kết nối lại? Với workflow này, các sếp có thể tự động hóa quy trình gửi lời mời kết nối cá nhân hóa cho tất cả người bình luận một cách nhanh chóng và chuyên nghiệp, mà không cần phải làm thủ công từng cái một.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động xử lý hàng trăm lời mời kết nối trong vài phút.
- **Cá nhân hóa cao**: Mỗi lời mời kết nối đều được cá nhân hóa với thông tin chi tiết về bài viết và người nhận.
- **Chính xác tuyệt đối**: Không gửi lời mời cho những người đã kết nối hoặc có lời mời đang chờ.
- **Hoạt động liên tục**: Workflow chạy tự động 24/7 mà không cần can thiệp.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản ConnectSafely.ai với API key hợp lệ.
- URL bài viết LinkedIn cần xử lý.
- Thông tin cá nhân để cá nhân hóa lời mời kết nối.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor của bạn.
2. Nhấn vào nút "Import from URL" và dán link sau: [https://n8n.io/workflows/11530](https://n8n.io/workflows/11530).
3. Hoặc tải file JSON về máy và import từ file.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Form Trigger**:
   - Đảm bảo đường dẫn "auto-connect-commenters" được đặt chính xác trong node này.

2. **ConnectSafely LinkedIn**:
   - Thêm credentials "connectSafelyApi" với API key của bạn.
   - Đảm bảo các tham số chính xác:
     - `operation`: `getAllPostComments` cho node đầu tiên.
     - `operation`: `checkRelationship` cho node thứ hai.
     - `operation`: `sendConnectionRequest` cho node thứ ba.

3. **Generate Message**:
   - Chỉnh sửa mã JavaScript trong node này để cá nhân hóa lời mời kết nối của bạn.

4. **Wait 1-2 Hours**:
   - Điều chỉnh thời gian chờ giữa các lời mời kết nối để phù hợp với chính sách của LinkedIn.

#### 3. Kích hoạt ⚡️
1. Nhấn nút "Execute Workflow" để kiểm tra với dữ liệu mẫu.
2. Sau khi kiểm tra thành công, nhấn nút "Activate" để kích hoạt workflow.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp với Slack/Telegram**: Thêm node để nhận thông báo khi workflow hoàn thành.
- **Lưu log**: Lưu log các lời mời kết nối đã gửi để theo dõi hiệu quả.
- **Gửi báo cáo định kỳ**: Thêm node để gửi báo cáo tổng hợp hàng tuần về số lượng lời mời kết nối đã gửi.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa quy trình gửi lời mời kết nối LinkedIn một cách chuyên nghiệp và hiệu quả. Bằng cách sử dụng n8n và ConnectSafely.ai, các sếp có thể tiết kiệm thời gian và tăng cường mạng lưới kết nối của mình một cách tự động. Hãy áp dụng ngay để bắt đầu xây dựng mạng lưới kết nối LinkedIn của bạn!