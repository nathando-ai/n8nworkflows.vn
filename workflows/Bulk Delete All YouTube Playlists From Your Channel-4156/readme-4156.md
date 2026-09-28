---
title: "🧹 Xóa Toàn Bộ Playlist YouTube Tự Động Trong 1 Click (n8n)"
description: "Hướng dẫn sử dụng workflow n8n để dọn dẹp hàng loạt playlist trên kênh YouTube. Giải pháp tự động hóa giúp tiết kiệm thời gian và quản lý kênh chuyên nghiệp."
slug: "xa-toan-bo-playlist-youtube-tu-dong"
tags: [n8n, youtube-automation, channel-management, no-code, cleanup]
keywords: [xoa playlist youtube, n8n youtube workflow, tu dong hoa youtube, quan ly ket youtube, n8n template]
---

# 🧹 Xóa Toàn Bộ Playlist YouTube Tự Động Trong 1 Click (n8n)

Các sếp có bao giờ cảm thấy kênh YouTube của mình bị "lộn xộn" với hàng chục, thậm chí hàng trăm playlist cũ, không còn phù hợp hoặc được tạo ra một cách ngẫu nhiên trong quá khứ? Việc xóa từng playlist thủ công trên giao diện YouTube Studio không chỉ tốn thời gian mà còn dễ gây nhầm lẫn, đặc biệt khi số lượng playlist rất lớn.

Workflow **"Bulk Delete All YouTube Playlists"** này chính là giải pháp "cứu tinh" dành cho các sếp. Với chỉ 3 nodes đơn giản, quy trình này sẽ tự động quét toàn bộ playlist trên kênh và xóa sạch chúng trong chớp mắt. Không cần code, không cần lo lắng về việc bỏ sót, các sếp chỉ cần một cú click duy nhất để hoàn thành công việc dọn dẹp kênh.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian tối đa:** Xóa hàng trăm playlist trong vài giây thay vì hàng giờ làm thủ công.
- **Chính xác tuyệt đối:** Workflow đảm bảo quét và xử lý tất cả các playlist hiện có, không bỏ sót.
- **Quản lý kênh chuyên nghiệp:** Giúp kênh YouTube gọn gàng, tập trung vào nội dung chính, nâng cao trải nghiệm người xem.
- **Dễ dàng triển khai:** Chỉ cần 3 nodes, cấu hình cực nhanh, phù hợp cho cả người mới bắt đầu với n8n.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n:** Các sếp cần có tài khoản n8n (cloud hoặc self-hosted).
- **Tài khoản YouTube:** Kênh YouTube mà các sếp muốn dọn dẹp playlist.
- **YouTube OAuth2 Credential:** Các sếp cần tạo credential OAuth2 cho YouTube API trong n8n.
    - *Lưu ý:* Khi tạo credential, hãy đảm bảo cấp quyền `youtube.readonly` và `youtube.force-ssl` (hoặc quyền quản lý playlist nếu cần).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Mở n8n Editor.
2. Chọn **"Import from File"** hoặc **"Import from URL"**.
3. Tải file JSON của workflow hoặc dán link gốc: [https://n8n.io/workflows/4156](https://n8n.io/workflows/4156).
4. Workflow sẽ được import với 3 nodes: `Manual Trigger`, `Get all playlists`, và `Remove playlist`.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Đây là phần quan trọng nhất. Workflow này thực hiện hành động **không thể hoàn tác**, vì vậy các sếp cần kiểm tra kỹ trước khi chạy.

- **Node: `When clicking ‘Test workflow’` (Manual Trigger)**
    - Đây là nút khởi động. Các sếp không cần chỉnh gì thêm, chỉ cần click vào nút **"Test workflow"** trên thanh công cụ để bắt đầu.

- **Node: `Get all playlists` (YouTube)**
    - **Credentials:** Chọn credential YouTube OAuth2 mà các sếp đã tạo ở bước chuẩn bị.
    - **Resource:** Đảm bảo đang chọn `playlist`.
    - **Operation:** Mặc định là `getAll`. Node này sẽ lấy danh sách tất cả playlist trên kênh.
    - *Mẹo:* Nếu kênh có quá nhiều playlist, các sếp có thể thêm một node `Filter` sau node này để chỉ xóa những playlist có tên chứa từ khóa cụ thể (ví dụ: "Old", "Test", "Draft") thay vì xóa tất cả.

- **Node: `Remove playlist` (YouTube)**
    - **Credentials:** Chọn cùng credential YouTube OAuth2.
    - **Operation:** Chọn `delete`.
    - **Resource:** Chọn `playlist`.
    - **Playlist ID:** Node này sẽ tự động nhận ID playlist từ node `Get all playlists`. Các sếp không cần điền thủ công.
    - *Lưu ý quan trọng:* Workflow này sẽ xóa **TẤT CẢ** playlist. Nếu các sếp muốn giữ lại một số playlist quan trọng, hãy thêm một node `Filter` hoặc `IF` trước node `Remove playlist` để loại trừ chúng.

:::note[CẢNH BÁO QUAN TRỌNG]
**🚨 HÀNH ĐỘNG KHÔNG THỂ HOÀN TÁC:**
Khi chạy workflow này, tất cả playlist trên kênh sẽ bị xóa vĩnh viễn. Các video trong playlist vẫn còn trên kênh, nhưng playlist sẽ biến mất. Các sếp **không thể khôi phục** playlist đã xóa. Hãy cân nhắc kỹ và chỉ chạy workflow khi thực sự cần dọn dẹp toàn bộ.
:::

#### 3. Kích hoạt ⚡️
1. **Test run:** Click vào nút **"Test workflow"** trên thanh công cụ.
2. Quan sát các node:
    - `Get all playlists` sẽ hiển thị danh sách playlist.
    - `Remove playlist` sẽ thực hiện xóa từng playlist.
3. Kiểm tra kênh YouTube của các sếp để xác nhận playlist đã bị xóa.
4. Nếu mọi thứ hoạt động đúng, các sếp có thể **bật Active** workflow nếu muốn chạy lại sau này (tuy nhiên, do đây là hành động một lần, các sếp có thể không cần bật Active).

### ✍️ Mẹo & gợi ý nâng cao
- **Lọc theo tên playlist:** Thêm node `Filter` sau `Get all playlists` để chỉ xóa playlist có tên chứa từ khóa cụ thể (ví dụ: "Old", "Test", "Draft").
- **Gửi thông báo:** Thêm node `Slack` hoặc `Telegram` sau node `Remove playlist` để gửi thông báo khi quá trình xóa hoàn tất.
- **Lưu log:** Thêm node `Google Sheets` hoặc `Postgres` để lưu lại danh sách playlist đã xóa, giúp các sếp có thể theo dõi và khôi phục nếu cần (bằng cách tạo lại playlist).
- **Chạy định kỳ:** Nếu các sếp muốn tự động xóa playlist cũ hàng tháng, có thể thay `Manual Trigger` bằng `Cron` và thêm điều kiện lọc theo ngày tạo playlist.

### 📌 Kết luận
Workflow **"Bulk Delete All YouTube Playlists"** là công cụ đơn giản nhưng cực kỳ hiệu quả để dọn dẹp kênh YouTube. Với chỉ 3 nodes, các sếp có thể tiết kiệm hàng giờ làm việc thủ công và giữ cho kênh của mình luôn gọn gàng, chuyên nghiệp. Hãy nhớ kiểm tra kỹ và chỉ chạy workflow khi thực sự cần thiết, vì hành động xóa playlist là không thể hoàn tác. Chúc các sếp thành công trong việc quản lý kênh YouTube của mình! 🚀