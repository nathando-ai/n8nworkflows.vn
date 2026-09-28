---
title: "🚀 Tự Động Chỉnh Sửa Mô Tả Video YouTube Hàng Loạt Với n8n"
description: "Giải pháp tự động hóa giúp chèn liên kết hoặc nội dung mới vào mô tả của hàng trăm video YouTube chỉ trong vài giây, không cần code."
slug: "tu-dong-chinh-sua-mo-ta-video-youtube"
tags: [n8n, youtube-automation, marketing, no-code, content-management]
keywords: [n8n workflow youtube, tự động hóa youtube, cập nhật mô tả video, n8n marketing, youtube api]
---

# 🚀 Tự Động Chỉnh Sửa Mô Tả Video YouTube Hàng Loạt Với n8n

Bạn có bao giờ cảm thấy đau đầu khi cần cập nhật một liên kết mới, thêm một dòng giới thiệu kênh, hoặc sửa đổi thông tin trong mô tả của hàng chục, thậm chí hàng trăm video YouTube? Việc làm thủ công từng video không chỉ tốn thời gian mà còn dễ gây sai sót, dẫn đến trải nghiệm người dùng không nhất quán.

Workflow **"Automatically Update YouTube Video Descriptions with Inserted Text"** này chính là "cứu tinh" dành cho các YouTuber, Agency Marketing và Content Creator. Nó cho phép bạn tự động hóa 100% quy trình chèn một dòng văn bản hoặc liên kết cụ thể vào giữa hai dòng đã xác định trong mô tả của tất cả video trong kênh, giúp tiết kiệm hàng giờ làm việc thủ công mỗi tuần.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian cực đại:** Thay vì mất hàng giờ click chuột, toàn bộ kênh được cập nhật trong vài phút.
- **Độ chính xác tuyệt đối:** Đảm bảo dòng văn bản được chèn đúng vị trí (giữa 2 dòng cụ thể) cho mọi video, không lo sót hay sai lệch.
- **Nâng cao trải nghiệm người dùng:** Giữ cho mô tả video nhất quán, chuyên nghiệp và luôn cập nhật thông tin mới nhất (link liên hệ, playlist, v.v.).
- **Không cần code:** Chỉ cần cấu hình các biến văn bản, n8n sẽ xử lý logic phức tạp phía sau.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n:** Bản Cloud hoặc Self-hosted.
- **Tài khoản YouTube:** Kênh cần được cập nhật.
- **YouTube Data API v3:**
  - Tạo OAuth Client ID trong Google Cloud Console.
  - Cấp quyền cho n8n để truy cập YouTube (Scopes: `youtube.readonly` và `youtube`).
  - **Lưu ý quan trọng:** Video cần có quyền chỉnh sửa mô tả (thường là video thuộc về kênh đó).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Mở n8n Editor.
2. Chọn **Import from URL** và dán link: `https://n8n.io/workflows/3080` HOẶC copy toàn bộ JSON của workflow và dán vào n8n.
3. Workflow sẽ hiển thị với các node chính: `Manual Trigger`, `Set String to Insert`, `Get All Videos`, `Loop Over Videos`, `Get Specific Video`, `Create New Video Description with Row Inserted`, và `Update Video Description`.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

**Node: `Set String to Insert`**
Đây là node quan trọng nhất để định nghĩa nội dung bạn muốn chèn. Các sếp cần cấu hình 3 trường dữ liệu (String):
- **`rowBefore`**: Dòng văn bản hiện có trong mô tả mà dòng mới sẽ được chèn **SAU** nó.
  - *Ví dụ:* Nếu mô tả có dòng "🔗 Links:" và bạn muốn chèn link mới ngay sau dòng này, hãy nhập `🔗 Links:` vào đây.
- **`rowToInsert`**: Nội dung (dòng văn bản hoặc link) mà bạn muốn thêm vào.
  - *Ví dụ:* `https://yournewlink.com`
- **`rowAfter`**: Dòng văn bản hiện có trong mô tả mà dòng mới sẽ được chèn **TRƯỚC** nó.
  - *Ví dụ:* Nếu dòng tiếp theo sau "🔗 Links:" là "📅 Upload Schedule:", hãy nhập `📅 Upload Schedule:` vào đây.
  - *Mẹo:* Nếu bạn muốn chèn ở cuối hoặc đầu, hãy đảm bảo các dòng `rowBefore`/`rowAfter` tồn tại trong mô tả gốc để logic hoạt động chính xác.

**Node: `Get All Videos`**
- Chọn **Credentials** của YouTube Data API v3.
- Đảm bảo tham số `Channel ID` hoặc `Mine` được cấu hình đúng để lấy danh sách video của kênh cần cập nhật.

**Node: `Update Video Description`**
- Chọn cùng **Credentials** YouTube Data API v3.
- Node này sẽ tự động nhận dữ liệu từ node `Create New Video Description with Row Inserted` (node Code) để thực hiện lệnh cập nhật.

**Node: `Create New Video Description with Row Inserted`**
- Đây là node Code chứa logic xử lý chuỗi. Các sếp thường không cần chỉnh sửa code này trừ khi muốn thay đổi logic chèn (ví dụ: chèn ở đầu/cuối thay vì giữa 2 dòng). Code mặc định sẽ tìm vị trí của `rowBefore` và `rowAfter` trong mô tả gốc và chèn `rowToInsert` vào giữa.

#### 3. Kích hoạt ⚡️
1. **Test Run:**
   - Nhấn vào nút **Test workflow** (hoặc icon Play) ở góc trên bên phải.
   - Workflow sẽ chạy qua các video. Hãy kiểm tra kết quả ở node `Update Video Description` để đảm bảo mô tả mới được tạo đúng ý.
   - *Lưu ý:* Khi test, n8n có thể chỉ cập nhật một số video hoặc yêu cầu xác nhận. Hãy kiểm tra kỹ trên YouTube Studio.
2. **Bật Active:**
   - Sau khi test thành công, nhấn nút **Active** ở góc trên bên phải để workflow sẵn sàng chạy.
   - *Lưu ý:* Workflow này dùng `Manual Trigger`, nghĩa là nó chỉ chạy khi các sếp bấm nút "Execute Workflow" hoặc "Test workflow". Nếu muốn chạy định kỳ (ví dụ: mỗi tháng một lần), các sếp có thể thay thế `Manual Trigger` bằng `Cron` hoặc `Schedule Trigger`.

### ✍️ Mẹo & gợi ý nâng cao
- **Thêm thông báo hoàn thành:** Kết nối thêm node `Slack`, `Telegram` hoặc `Email` sau node `Update Video Description` để nhận thông báo khi toàn bộ kênh đã được cập nhật xong.
- **Lưu log thay đổi:** Thêm node `Google Sheets` hoặc `Postgres` để ghi lại ID video, thời gian cập nhật và nội dung đã chèn. Điều này giúp audit và kiểm soát rủi ro.
- **Chèn nhiều dòng:** Nếu cần chèn nhiều liên kết khác nhau, các sếp có thể nhân bản node `Set String to Insert` và `Code` để tạo nhiều luồng xử lý, hoặc sửa code trong node `Create New Video Description` để xử lý mảng các dòng cần chèn.
- **Xử lý lỗi:** Thêm node `Error Trigger` để bắt lỗi khi một video không thể cập nhật (ví dụ: video đã bị xóa hoặc không có quyền), và gửi cảnh báo cho các sếp.

### 📌 Kết luận
Workflow **"Automatically Update YouTube Video Descriptions with Inserted Text"** là một công cụ mạnh mẽ, đơn giản nhưng cực kỳ hiệu quả cho việc quản lý nội dung YouTube quy mô lớn. Với khả năng chèn chính xác nội dung vào vị trí mong muốn trong hàng loạt video, nó giúp các sếp tiết kiệm thời gian, giảm thiểu sai sót và nâng cao tính chuyên nghiệp của kênh. Hãy áp dụng ngay để trải nghiệm sự khác biệt trong quy trình làm việc của mình!