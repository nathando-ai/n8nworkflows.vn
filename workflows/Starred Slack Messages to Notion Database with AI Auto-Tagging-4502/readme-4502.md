---
title: "🚀 Tự động lưu tin nhắn Slack được sao vào Notion với AI gắn thẻ tự động"
description: "Hướng dẫn tự động hóa lưu tin nhắn Slack được sao vào Notion với AI gắn thẻ tự động, tiết kiệm thời gian và nâng cao hiệu quả quản lý thông tin"
slug: "tu-dong-luu-tin-nhan-slack-vao-notion-voi-ai-gan-the-tu-dong"
tags: [n8n, automation, no-code, Slack, Notion]
keywords: [n8n workflow, tự động hóa, Slack, Notion, AI]
---

# 🚀 Tự động lưu tin nhắn Slack được sao vào Notion với AI gắn thẻ tự động

[Các sếp đang làm việc với Slack và Notion chắc hẳn đã gặp khó khăn khi phải thủ công lưu trữ các tin nhắn quan trọng được đánh dấu sao. Với workflow này, các sếp có thể tự động hóa toàn bộ quá trình này, tiết kiệm thời gian và nâng cao hiệu quả quản lý thông tin.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động lưu trữ các tin nhắn quan trọng từ Slack vào Notion
- AI tự động gắn thẻ cho các tin nhắn dựa trên nội dung
- Tiết kiệm thời gian và công sức thủ công
- Tăng cường khả năng tìm kiếm và quản lý thông tin
- Hoạt động liên tục 24/7 mà không cần can thiệp
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Slack với quyền truy cập vào các kênh cần theo dõi
- Tài khoản Notion với quyền truy cập vào cơ sở dữ liệu (database) cần lưu trữ
- API Key của OpenAI để sử dụng AI gắn thẻ tự động
- Tài khoản n8n đã được cài đặt và cấu hình
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Để import workflow này vào n8n của bạn, các sếp có thể thực hiện theo các bước sau:

1. Truy cập vào trang workflow gốc: [Starred Slack Messages to Notion Database with AI Auto-Tagging](https://n8n.io/workflows/4502)
2. Nhấp vào nút "Download" để tải về file JSON của workflow
3. Trong giao diện n8n của bạn, nhấp vào biểu tượng "+" ở góc trái màn hình
4. Chọn "Import from File" và chọn file JSON vừa tải về
5. Hoàn tất quá trình import

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần chú ý cấu hình các node quan trọng sau:

- **Schedule Trigger**: Cấu hình thời gian kiểm tra tin nhắn mới (ví dụ: mỗi 15 phút)
- **Get Slack Messages**: Cấu hình credentials Slack và chọn kênh cần theo dõi
- **IF reaction == star**: Đảm bảo chỉ xử lý các tin nhắn có reaction là sao
- **OpenAI Chat Model**: Cấu hình API Key của OpenAI và prompt cho AI gắn thẻ
- **Structured Output Parser**: Cấu hình schema đầu ra cho AI gắn thẻ
- **Choose Notion DB**: Chọn cơ sở dữ liệu Notion cần lưu trữ tin nhắn
- **Create Notion Page**: Cấu hình các trường dữ liệu cần lưu trữ (ví dụ: tiêu đề, nội dung, thẻ)

#### 3. Kích hoạt ⚡️
Sau khi cấu hình xong, các sếp cần thực hiện các bước sau:

1. Nhấp vào nút "Execute Workflow" để kiểm tra hoạt động của workflow
2. Kiểm tra kết quả đầu ra để đảm bảo dữ liệu được lưu trữ đúng
3. Nếu mọi thứ hoạt động tốt, nhấp vào nút "Activate" để kích hoạt workflow

### ✍️ Mẹo & gợi ý nâng cao
- Các sếp có thể tùy chỉnh prompt cho AI gắn thẻ để phù hợp với nhu cầu cụ thể của mình
- Có thể kết hợp với Slack để thông báo khi có tin nhắn mới được lưu trữ
- Có thể thêm chức năng gửi báo cáo định kỳ về các tin nhắn quan trọng
- Có thể mở rộng để xử lý các loại reaction khác ngoài sao

### 📌 Kết luận
Workflow "Starred Slack Messages to Notion Database with AI Auto-Tagging" giúp các sếp tự động hóa việc lưu trữ tin nhắn quan trọng từ Slack vào Notion với AI gắn thẻ tự động. Với workflow này, các sếp có thể tiết kiệm thời gian và công sức thủ công, đồng thời nâng cao hiệu quả quản lý thông tin. Hãy áp dụng ngay để tối ưu hóa quy trình làm việc của mình!