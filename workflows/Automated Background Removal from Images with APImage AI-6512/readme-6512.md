---
title: "🚀 Tự động loại bỏ nền ảnh với APImage AI – Giải pháp nhanh chóng, không code"
description: "Giải quyết vấn đề xử lý hình ảnh thủ công bằng cách tự động loại bỏ nền cho bất kỳ ảnh nào, đạt hiệu quả 100% không cần viết mã."
slug: "tuy-dong-loai-bo-nang-anh-voi-apimage-ai"
tags: [n8n, automation, no-code, ai, image-processing]
keywords: [n8n workflow, tự động hóa, APImage, loại bỏ nền, AI image processing]
---

# 🚀 Tự động loại bỏ nền ảnh với APImage AI – Giải pháp nhanh chóng, không code

Bạn đang phải xử lý hàng trăm, hàng nghìn ảnh mỗi ngày, nhưng việc **loại bỏ nền** vẫn phải làm thủ công, tốn thời gian và dễ gây sai sót. Workflow này giúp bạn **tự động** gửi ảnh tới API APImage, nhận lại ảnh đã loại bỏ nền và lưu trữ ngay tại nơi bạn muốn – hoàn toàn **không cần viết code**.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

## 🎯 Kết quả các sếp nhận được

:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Từ vài phút thành vài giây cho mỗi ảnh.  
- **Độ chính xác cao**: API APImage hỗ trợ AI tiên tiến, giảm lỗi thủ công.  
- **Tự động hoá liên tục**: Chạy 24/7, không cần can thiệp.  
- **Dễ dàng mở rộng**: Thêm lưu trữ, báo cáo, hoặc tích hợp với Slack/Telegram chỉ vài bước.  
:::

## 🔧 Yêu cầu cần thiết

:::info[CHUẨN BỊ]
- **Tài khoản APImage**: Đăng ký tại <https://apimage.org> và lấy **API Key**.  
- **Dịch vụ lưu trữ** (tùy chọn): Google Drive, Dropbox, S3, Airtable, v.v.  
- **n8n**: Cài đặt phiên bản mới nhất (>= v0.200).  
:::

## 🚀 Cách import & Lưu ý khi "lên đồ"

### 1. Import Workflow 📥

1. Tải file JSON từ <https://n8n.io/workflows/6512> hoặc sao chép nội dung JSON.  
2. Mở **n8n Editor**, chọn **Import** → **Import from Clipboard** hoặc **Import from File**.  
3. Đảm bảo workflow được import thành công và hiển thị 3 node: `APImage Integration`, `Download`, `Remove Background`.

### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

| Node | Tên node | Kiểu | Cấu hình cần chỉnh |
|------|----------|------|---------------------|
| 1 | **APImage Integration** | httpRequest | - **URL**: `https://api.apimage.org/v1/remove` <br> - **Method**: POST <br> - **Headers**: `Authorization: Bearer _YOUR_API_KEY_` <br> - **Body**: `{"image_url":"{{ $json["image_url"] }}"}` |
| 2 | **Download** | httpRequest | - **URL**: `{{ $json["output_url"] }}` <br> - **Method**: GET <br> - **Response Format**: Binary (đặt `Response Format` thành `File`) |
| 3 | **Remove Background** | formTrigger | - **Form Fields**: `image_url` (URL của ảnh cần loại bỏ nền) <br> - **Trigger**: Manual hoặc từ nguồn dữ liệu khác (SQLite, Google Sheets, v.v.) |

> **Lưu ý**: Thay thế `_YOUR_API_KEY_` bằng API Key thực tế của bạn. Bạn có thể lấy API Key trong Dashboard của tài khoản APImage.

### 3. Kích hoạt ⚡️

1. **Test run**: Nhấn nút **Execute Node** trên node `Remove Background`, nhập URL ảnh mẫu.  
2. Kiểm tra kết quả: Node `Download` sẽ trả về file ảnh đã loại bỏ nền.  
3. Khi mọi thứ ổn, bật **Active** cho workflow. Workflow sẽ tự động chạy khi có dữ liệu mới.

## ✍️ Mẹo & gợi ý nâng cao

- **Lưu trữ ảnh**: Thêm node `Google Drive`, `Dropbox`, `S3` ngay sau node `Download`. Đặt tên file mặc định là `data` hoặc tùy chỉnh theo nhu cầu.  
- **Tích hợp Slack**: Thêm node `Slack` để gửi thông báo khi ảnh đã được xử lý.  
- **Báo cáo định kỳ**: Sử dụng node `Cron` để gửi báo cáo hàng ngày về số lượng ảnh đã xử lý.  
- **Xử lý hàng loạt**: Kết nối workflow với nguồn dữ liệu như Google Sheets hoặc Airtable để tự động lấy danh sách URL và xử lý từng ảnh.

## 📌 Kết luận

Workflow **Automated Background Removal from Images with APImage AI** là công cụ mạnh mẽ giúp các sếp tiết kiệm thời gian, giảm sai sót và tăng hiệu suất làm việc. Hãy **đăng ký API**, **import workflow**, **điều chỉnh cấu hình** và **bật chạy** ngay hôm nay để trải nghiệm tự động hóa 100% không code!

Nếu gặp bất kỳ vấn đề nào khi thiết lập APImage API, hãy liên hệ:

✉ [ask@support.apimage.org](mailto:ask@support.apimage.org)