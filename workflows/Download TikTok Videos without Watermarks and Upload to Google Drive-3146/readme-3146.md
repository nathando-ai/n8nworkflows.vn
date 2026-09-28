---
title: "🚀 Tự động tải video TikTok không logo và lưu Google Drive với n8n"
description: "Hướng dẫn chi tiết cách xây dựng workflow n8n tự động tải video TikTok không dính watermark (logo ID) và lưu trữ trực tiếp lên Google Drive."
slug: "tai-video-tiktok-khong-logo-google-drive-n8n"
tags: [n8n, automation, tiktok, google-drive, marketing, scraper]
keywords: [n8n workflow, tải video tiktok không logo, no watermark tiktok, google drive automation, n8nhttpRequest, tự động hóa marketing]
---

# 🚀 Tự động tải video TikTok không logo và lưu Google Drive với n8n

Các sếp làm sáng tạo nội dung, TikTok hay Marketing chắc chắn đã quá quen với việc phải tìm các trang web bên thứ 3 kém bảo mật, đầy quảng cáo rác để tải video TikTok không logo (watermark). Việc này vừa thủ công, mất thời gian, lại vừa rủi ro về bảo mật khi cần tải số lượng lớn.

Hôm nay, em xin giới thiệu một giải pháp tự động hóa 100% bằng n8n: **Tự động trích xuất, tải xuống video TikTok nguyên bản (không dính watermark) và tự động đồng bộ lên Google Drive** chỉ với 1 cú click chuột (hoặc có thể mở rộng kết nối Webhook để chạy tự động).

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Sạch sẽ tuyệt đối:** Lấy được video gốc từ TikTok hoàn toàn không dính logo hay ID người dùng nhảy múa trên màn hình.
- **Tự động hóa lưu trữ:** Video tải về được đẩy thẳng lên Google Drive theo đúng định dạng tên `Video_ID.mp4`.
- **Tiết kiệm thời gian:** Không cần qua các trang web trung gian chứa đầy mã độc hay quảng cáo phiền toái.
- **Chia sẻ dễ dàng:** Tự động phân quyền file trên Google Drive thành công khai bằng đường link để phục vụ công việc ngay lập tức.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một hệ thống **n8n** đang hoạt động (Cloud hoặc Self-hosted).
- Tài khoản **Google Cloud Console** để cấu hình Google Drive API (OAuth2 Client ID và Client Secret).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tạo một workflow mới trong n8n, sau đó copy toàn bộ mã JSON của workflow từ nguồn gốc hoặc dựng lại dựa trên danh sách 6 nodes tiêu chuẩn bao gồm: `manualTrigger`, `httpRequest`, `code`, và `googleDrive`.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà không gặp lỗi, các sếp cần chú ý cấu hình kỹ các node sau:

- **Node `Get TikTok Video Page Data` (HTTP Request):** 
  - Mở node này và thay thế URL mặc định bằng đường dẫn video TikTok mà các sếp muốn tải (Ví dụ: `https://www.tiktok.com/@username/video/1234567890`).
  - Node này sẽ trả về mã HTML của trang kèm theo session cookies cần thiết.
- **Node `Scrape raw video URL` (Code):** 
  - Node này chạy mã JavaScript để phân tích toàn bộ HTML, bóc tách và tìm ra đường dẫn URL gốc của video (trước khi TikTok gắn watermark vào). Các sếp không cần sửa code ở đây trừ khi TikTok thay đổi cấu trúc trang web của họ.
- **Node `Output video file without watermark` (HTTP Request):** 
  - Sử dụng cookies thu được từ bước 1 để gửi yêu cầu tải file video gốc về dạng nhị phân (binary).
- **Node `Upload to Google Drive` (Google Drive):** 
  - Cần kết nối tài khoản Google Drive thông qua **Google Drive OAuth2 API**.
  - Đặt tên file đầu ra sử dụng biểu thức (expression) để lưu với định dạng `Video_ID.mp4`.
- **Node `Set file permissions to public with link` (Google Drive):** 
  - Cấu hình thao tác (`operation`: `share`) để tự động public file vừa tải lên, giúp các sếp dễ dàng lấy link gửi cho team hoặc đăng lên các nền tảng khác.

#### 3. Kích hoạt ⚡️
- Nhấn nút **Test workflow** tại node `When clicking ‘Test workflow’` để kiểm tra toàn bộ luồng chạy xem video đã vào Google Drive chưa.
- Sau khi test thành công, bật công tắc **Active** ở góc trên bên phải để sẵn sàng đưa vào vận hành thực tế.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết nối Webhook/Telegram:** Thay vì dùng `Manual Trigger`, các sếp có thể đổi thành Telegram Trigger hoặc Webhook. Chỉ cần gửi link TikTok qua chat bot Telegram, n8n sẽ tự động tải về và gửi lại link Google Drive cho các sếp ngay lập tức.
- **Lưu trữ vào Google Sheets:** Thêm một node Google Sheets để ghi lại lịch sử các video đã tải (Link TikTok, Tên File, Link Google Drive, Thời gian tải).
- **Tự động lên lịch (Cron):** Kết hợp với Schedule Trigger để tự động quét và tải danh sách video từ một kênh TikTok bất kỳ theo khung giờ định sẵn.

### 📌 Kết luận
Việc xử lý và lưu trữ video TikTok chưa bao giờ đơn giản và tự động đến thế với n8n. Hãy áp dụng ngay để tối ưu hóa quy trình làm content cho đội ngũ của mình các sếp nhé!