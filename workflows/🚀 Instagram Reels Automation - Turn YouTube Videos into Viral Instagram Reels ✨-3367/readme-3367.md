---
title: "🚀 Tự động hóa Instagram Reels từ YouTube - Chuyển đổi Video thành Reels Viral ✨"
description: "Hướng dẫn tự động hóa hoàn toàn quá trình tạo và đăng Instagram Reels từ YouTube bằng n8n. Tiết kiệm thời gian, tăng tương tác và tối ưu hóa nội dung một cách thông minh."
slug: "tu-dong-hoa-instagram-reels-tu-youtube"
tags: [n8n, automation, no-code, instagram, youtube]
keywords: [n8n workflow, tự động hóa, instagram reels, youtube, marketing]
---

# 🚀 Tự động hóa Instagram Reels từ YouTube - Chuyển đổi Video thành Reels Viral ✨

[Các sếp marketing đang gặp khó khăn khi phải chuyển đổi hàng loạt video YouTube thành Instagram Reels thủ công. Quá trình này tốn thời gian, dễ gây lỗi và không thể cá nhân hóa cho từng video. Workflow này sẽ giúp các sếp tự động hóa hoàn toàn quy trình này với n8n.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động hóa hoàn toàn quá trình chuyển đổi và đăng tải.
- **Tăng tương tác**: Tối ưu hóa nội dung cho Instagram Reels với các sếp có thể tùy chỉnh.
- **Chính xác cao**: Giảm thiểu lỗi so với làm thủ công.
- **Hoạt động liên tục**: Tự động xử lý hàng loạt video mà không cần can thiệp.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Instagram Business hoặc Creator.
- API Key của Instagram Graph API.
- Tài khoản YouTube với quyền truy cập vào các video cần chuyển đổi.
- Tài khoản n8n đã được cài đặt và cấu hình.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor.
2. Nhấn vào nút "Import from URL".
3. Dán link sau vào ô nhập liệu: `https://n8n.io/workflows/3367`.
4. Nhấn "Import" để tải workflow vào n8n.

Hoặc có thể copy/paste JSON sau vào n8n Editor:

```json
{
  "nodes": [
    {
      "name": "Fill information to Start",
      "type": "formTrigger"
    },
    {
      "name": "Wait #1",
      "type": "wait"
    },
    {
      "name": "Wait #2",
      "type": "wait"
    },
    {
      "name": "Prepare Reels",
      "type": "httpRequest"
    },
    {
      "name": "Download the Reels in the Right Format",
      "type": "httpRequest"
    },
    {
      "name": "Post To Instagram",
      "type": "httpRequest"
    },
    {
      "name": "Structure Reels",
      "type": "splitOut"
    },
    {
      "name": "Filter the Best Reels to Upload",
      "type": "code"
    },
    {
      "name": "Send Reels 1 at a time",
      "type": "splitInBatches"
    },
    {
      "name": "Download Reels When Ready",
      "type": "httpRequest"
    },
    {
      "name": "Reels Ready?",
      "type": "if"
    }
  ]
}
```

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Fill information to Start** (formTrigger):
   - Cấu hình form để nhập thông tin cần thiết như URL video YouTube, tiêu đề, mô tả, hashtags.
   - Đảm bảo các trường bắt buộc được điền đầy đủ.

2. **Prepare Reels** (httpRequest):
   - Cấu hình endpoint API để chuẩn bị video từ YouTube.
   - Điền thông tin xác thực (credentials) cho YouTube API.

3. **Download the Reels in the Right Format** (httpRequest):
   - Cấu hình endpoint API để tải video về định dạng phù hợp với Instagram Reels.
   - Đảm bảo định dạng video là MP4 và độ phân giải phù hợp.

4. **Post To Instagram** (httpRequest):
   - Cấu hình endpoint API để đăng tải video lên Instagram.
   - Điền thông tin xác thực (credentials) cho Instagram Graph API.

5. **Filter the Best Reels to Upload** (code):
   - Viết mã JavaScript để lọc và chọn các video phù hợp để đăng tải.
   - Có thể tùy chỉnh logic lọc dựa trên tiêu chí như lượt xem, thời lượng, từ khóa.

6. **Send Reels 1 at a time** (splitInBatches):
   - Cấu hình số lượng video được xử lý cùng một lúc.
   - Có thể điều chỉnh batch size để tối ưu hóa hiệu suất.

#### 3. Kích hoạt ⚡️
1. Test run dữ liệu mẫu để đảm bảo workflow hoạt động đúng.
2. Bật Active workflow để bắt đầu tự động hóa quá trình chuyển đổi và đăng tải video.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp với Slack/Telegram**: Thêm node để gửi thông báo khi video được đăng tải thành công.
- **Lưu log**: Thêm node để lưu log các video đã được xử lý để theo dõi và quản lý.
- **Gửi báo cáo định kỳ**: Tạo báo cáo tổng hợp các video đã được đăng tải và hiệu suất của chúng.
- **Tối ưu hóa nội dung**: Sử dụng LLM để tự động tạo tiêu đề, mô tả và hashtags phù hợp cho từng video.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa hoàn toàn quá trình chuyển đổi video YouTube thành Instagram Reels, tiết kiệm thời gian và tăng hiệu suất marketing. Hãy áp dụng ngay để tối ưu hóa nội dung và tăng tương tác trên Instagram!