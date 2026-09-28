---
title: "🚀 Tự động cập nhật phiên bản n8n tự host qua Coolify và Mattermost"
description: "Hướng dẫn tự động hóa cập nhật phiên bản n8n tự host hàng tuần qua Coolify và thông báo kết quả qua Mattermost"
slug: "tu-dong-cap-nhat-n8n-tu-host-qua-coolify-mattermost"
tags: [n8n, automation, no-code, devops, coolify]
keywords: [n8n workflow, tự động hóa, devops, coolify, mattermost]
---

# 🚀 Tự động cập nhật phiên bản n8n tự host qua Coolify và Mattermost

[Các sếp đang gặp khó khăn khi phải theo dõi và cập nhật phiên bản n8n tự host một cách thủ công. Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình kiểm tra và cập nhật phiên bản hàng tuần, giảm thiểu thời gian và lỗi con người.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động kiểm tra phiên bản n8n hàng tuần
- Cập nhật phiên bản mới một cách tự động qua Coolify
- Nhận thông báo kết quả qua Mattermost
- Giảm thiểu thời gian bảo trì thủ công
- Đảm bảo hệ thống luôn chạy phiên bản mới nhất
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản n8n API key (Settings → API → Generate Key)
- Tài khoản Coolify với quyền tạo API token
- (Tùy chọn) Tài khoản Mattermost để nhận thông báo
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/15740](https://n8n.io/workflows/15740)
2. Click vào nút "Import" ở góc trên bên phải
3. Chọn "Import from URL" và dán link trên vào ô nhập liệu
4. Click "OK" để hoàn tất import

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "GET audit"**:
   - Tạo credential "n8n API" với API key của bạn
   - Gán credential này cho node này

2. **Node "CALL Coolify to update image"**:
   - Tạo credential "HTTP Bearer Auth" với token API của Coolify
   - Gán credential này cho node này
   - Thay thế `<your-coolify-domain>` và `<APP_UUID>` trong URL bằng domain và UUID của dịch vụ n8n trong Coolify

3. **Node "post to channel" (tùy chọn)**:
   - Thay thế URL, Bearer token và channel ID bằng thông tin của Mattermost của bạn
   - Nếu không sử dụng Mattermost, có thể xóa node này

4. **Node "Run weekly update check"**:
   - Điều chỉnh lịch chạy theo nhu cầu (mặc định là mỗi thứ Hai lúc 01:00)

#### 3. Kích hoạt ⚡️
1. Click vào nút "Execute Workflow" để kiểm tra workflow hoạt động
2. Sau khi kiểm tra thành công, click vào nút "Activate" để kích hoạt workflow

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node gửi email thông báo thay vì Mattermost
- Kết hợp với Slack để nhận thông báo
- Thiết lập lịch chạy theo nhu cầu cụ thể của doanh nghiệp
- Thêm bước kiểm tra trạng thái sau khi cập nhật thành công
- Tạo bản sao lưu trước khi cập nhật phiên bản mới

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa toàn bộ quy trình cập nhật phiên bản n8n tự host, giảm thiểu thời gian bảo trì và đảm bảo hệ thống luôn chạy phiên bản mới nhất. Hãy áp dụng ngay để tối ưu hóa quy trình DevOps của bạn!