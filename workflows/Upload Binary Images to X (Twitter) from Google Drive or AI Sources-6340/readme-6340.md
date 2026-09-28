---
title: "🚀 Tự động đăng ảnh từ Google Drive lên X (Twitter) - Workflow n8n"
description: "Hướng dẫn tự động hóa việc chia sẻ ảnh từ Google Drive lên X (Twitter) bằng workflow n8n. Tiết kiệm thời gian và nâng cao hiệu quả truyền thông."
slug: "tu-dong-dang-anh-google-drive-len-x-twitter"
tags: [n8n, automation, no-code, social-media, google-drive]
keywords: [n8n workflow, tự động hóa, twitter, google drive, chia sẻ ảnh]
---

# 🚀 Tự động đăng ảnh từ Google Drive lên X (Twitter) - Workflow n8n

[Các sếp đang gặp khó khăn khi phải thủ công tải ảnh từ Google Drive lên X (Twitter) mỗi khi có bài viết mới. Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình này chỉ trong vài phút.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Không cần phải tải ảnh thủ công lên X (Twitter) mỗi khi có bài viết mới.
- Tăng hiệu quả truyền thông: Tự động chia sẻ ảnh từ Google Drive lên X (Twitter) một cách nhanh chóng và chính xác.
- Tăng cường tương tác: Tăng khả năng tương tác với người dùng thông qua việc chia sẻ ảnh một cách tự động.
- Tăng tốc độ công việc: Tự động hóa quy trình chia sẻ ảnh giúp các sếp tiết kiệm thời gian và tập trung vào các công việc quan trọng hơn.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẤN BỊ]
- Tài khoản Google Drive với ảnh cần chia sẻ.
- Tài khoản X (Twitter) với quyền truy cập API.
- API Key của X (Twitter) để thực hiện các yêu cầu HTTP.
- ID của ảnh trong Google Drive.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Để import workflow này vào n8n, các sếp có thể làm theo các bước sau:

1. Truy cập vào n8n Editor.
2. Nhấn vào nút "Import from URL" và nhập URL sau: [https://n8n.io/workflows/6340](https://n8n.io/workflows/6340).
3. Nhấn vào nút "Import" để hoàn tất quá trình import.

Hoặc, các sếp cũng có thể copy/paste JSON sau vào n8n Editor:

```json
{
  "nodes": [
    {
      "name": "Create Tweet",
      "type": "twitter"
    },
    {
      "name": "When clicking ‘Execute workflow’",
      "type": "manualTrigger"
    },
    {
      "name": "Download file",
      "type": "googleDrive"
    },
    {
      "name": "Upload Media to X",
      "type": "httpRequest"
    }
  ]
}
```

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần chú ý cấu hình các node sau:

- **Node "Download file" (Google Drive)**: Các sếp cần cấu hình thông tin tài khoản Google Drive và ID của ảnh cần chia sẻ.
- **Node "Upload Media to X" (HTTP Request)**: Các sếp cần cấu hình thông tin tài khoản X (Twitter) và API Key để thực hiện các yêu cầu HTTP.
- **Node "Create Tweet" (Twitter)**: Các sếp cần cấu hình thông tin tài khoản X (Twitter) và nội dung của tweet.

#### 3. Kích hoạt ⚡️
Sau khi cấu hình xong, các sếp có thể kích hoạt workflow bằng cách nhấn vào nút "Execute workflow" để kiểm tra xem workflow có hoạt động đúng không. Nếu mọi thứ đều ổn, các sếp có thể kích hoạt workflow để tự động chia sẻ ảnh từ Google Drive lên X (Twitter).

### ✍️ Mẹo & gợi ý nâng cao
- Các sếp có thể kết hợp workflow này với các công cụ khác như Slack, Telegram để nhận thông báo khi có ảnh mới được chia sẻ lên X (Twitter).
- Các sếp có thể lưu log của các ảnh đã được chia sẻ lên X (Twitter) để theo dõi hiệu quả của chiến dịch chia sẻ ảnh.
- Các sếp có thể gửi báo cáo định kỳ về hiệu quả của chiến dịch chia sẻ ảnh lên X (Twitter) để đánh giá và tối ưu hóa chiến dịch.

### 📌 Kết luận
Workflow này giúp các sếp tự động chia sẻ ảnh từ Google Drive lên X (Twitter) một cách nhanh chóng và chính xác. Với workflow này, các sếp có thể tiết kiệm thời gian và tăng hiệu quả truyền thông. Các sếp hãy áp dụng ngay workflow này để nâng cao hiệu quả truyền thông của mình.