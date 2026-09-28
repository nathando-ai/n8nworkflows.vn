---
title: "🔁 Sao chép toàn bộ danh sách phát YouTube từ kênh này sang kênh khác"
description: "Hướng dẫn tự động hóa sao chép tất cả danh sách phát từ kênh YouTube này sang kênh khác bằng n8n, tiết kiệm thời gian và công sức cho quản trị viên nội dung."
slug: "sao-chep-danh-sach-phat-youtube-tu-dong"
tags: [n8n, automation, no-code, youtube, content-management]
keywords: [n8n workflow, tự động hóa, youtube, sao chép danh sách phát, quản lý nội dung]
---

# 🔁 Sao chép toàn bộ danh sách phát YouTube từ kênh này sang kênh khác

[Đoạn mở đầu: Phân tích nỗi đau thực tế của quản trị viên nội dung khi phải sao chép thủ công danh sách phát từ kênh này sang kênh khác. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian đáng kể khi không cần sao chép thủ công từng danh sách phát
- Đảm bảo tính nhất quán và chính xác trong quá trình sao chép
- Tự động hóa toàn bộ quá trình sao chép mà không cần can thiệp thủ công
- Hoạt động liên tục 24/7 mà không cần giám sát
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Developer Console đã kích hoạt YouTube Data API v3
- 2 tài khoản YouTube credentials (một cho kênh nguồn, một cho kênh đích)
- Quyền truy cập quản trị viên cho cả hai kênh YouTube
- API keys hoặc OAuth credentials cho cả hai tài khoản YouTube
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/4154](https://n8n.io/workflows/4154)
2. Click vào nút "Download" để tải file JSON workflow
3. Trong n8n Editor, click vào "Import from File" và chọn file JSON vừa tải về

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:
- **Node "Get all playlists from origin channel"**: Cần cấu hình credentials cho kênh nguồn (origin channel)
- **Node "Create new playlist in the target channel"**: Cần cấu hình credentials cho kênh đích (target channel)
- **Node "Add items to target playlist"**: Cần cấu hình credentials cho kênh đích (target channel)
- **Node "Format fields properly"**: Có thể cần điều chỉnh các trường dữ liệu nếu cấu trúc dữ liệu của kênh nguồn khác với kênh đích

#### 3. Kích hoạt ⚡️
1. Sau khi cấu hình xong các node quan trọng, click vào nút "Test workflow" để kiểm tra
2. Kiểm tra kết quả đầu ra để đảm bảo danh sách phát đã được sao chép chính xác
3. Nếu kết quả ổn, click vào nút "Active workflow" để kích hoạt workflow

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node gửi email thông báo khi quá trình sao chép hoàn thành
- Kết hợp với Slack để nhận thông báo tức thời khi có lỗi xảy ra
- Thêm node lưu log hoạt động để theo dõi quá trình sao chép
- Tự động hóa quá trình sao chép định kỳ (ví dụ: hàng tuần) để đồng bộ nội dung mới nhất

### 📌 Kết luận
Workflow này cung cấp giải pháp tự động hóa hoàn hảo cho việc sao chép danh sách phát YouTube giữa các kênh. Bằng cách áp dụng workflow này, các sếp có thể tiết kiệm thời gian đáng kể và đảm bảo tính nhất quán trong quá trình quản lý nội dung. Hãy thử ngay và trải nghiệm sự tiện lợi mà tự động hóa mang lại!