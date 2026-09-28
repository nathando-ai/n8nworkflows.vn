---
title: "🚀 Tự động tạo kênh Mattermost, thêm thành viên và gửi tin nhắn – Không cần code!"
description: "Giải pháp nhanh chóng để tạo kênh Mattermost, mời thành viên và gửi tin nhắn ngay lập tức, giúp doanh nghiệp tiết kiệm thời gian và giảm lỗi thủ công."
slug: "tạo-kênh-thêm-thành-vien-và-bao-gửi-tin-nhắn-mattermost"
tags: [n8n, automation, no-code, mattermost, channel, messaging]
keywords: [n8n workflow, tự động hóa, Mattermost, kênh, tin nhắn]
---

# 🚀 Tự động tạo kênh Mattermost, thêm thành viên và gửi tin nhắn – Không cần code!

Bạn đang phải tạo kênh mới, mời thành viên và gửi tin nhắn thủ công trên Mattermost? Việc này không chỉ tốn thời gian mà còn dễ gây sai sót khi phải thao tác nhiều lần. Workflow này giúp bạn **tự động 100%**: từ lúc click “execute” đến khi kênh được tạo, thành viên được mời và tin nhắn được gửi ngay lập tức – hoàn toàn không cần viết code.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

## 🎯 Kết quả các sếp nhận được

:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Từ vài phút thủ công thành vài giây tự động.
- **Độ chính xác cao**: Không còn sai sót khi nhập dữ liệu.
- **Tích hợp linh hoạt**: Dễ dàng mở rộng thêm Slack, Teams, hoặc gửi báo cáo định kỳ.
- **Hoạt động liên tục**: Chạy 24/7 mà không cần giám sát thủ công.
:::

## 🔧 Yêu cầu cần thiết

:::info[CHUẨN BỊ]
- **Mattermost API credentials** (đã được cấu hình trong n8n dưới tên `mattermostApi`).
- **Tên kênh** (string) – sẽ được tạo trong bước đầu tiên.
- **User ID** hoặc **email** của thành viên cần mời (được sử dụng trong node `addUser`).
- **Nội dung tin nhắn** (string) – sẽ được gửi trong node cuối cùng.
:::

## 🚀 Cách import & Lưu ý khi "lên đồ"

### 1. Import Workflow 📥
1. Tải file JSON của workflow từ [link gốc](https://n8n.io/workflows/832) hoặc sao chép toàn bộ JSON.
2. Mở n8n Editor → `Import` → `Import from JSON` → dán JSON → `Import`.

### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Tên Node | Tham số cần cấu hình | Hướng dẫn |
|------|----------|----------------------|-----------|
| 1 | `On clicking 'execute'` | Không cần | Đây là trigger thủ công. |
| 2 | `Mattermost` | `resource: channel`, `operation: create`, `name: <Tên kênh>` | Chỉnh `name` thành tên kênh mong muốn. |
| 3 | `Mattermost1` | `operation: addUser`, `resource: channel`, `channel_id: <ID kênh>`, `user_id: <ID thành viên>` | `channel_id` lấy từ output của node 2 (`{{ $json["id"] }}`), `user_id` nhập ID người dùng Mattermost. |
| 4 | `Mattermost2` | `operation: postMessage`, `resource: channel`, `channel_id: <ID kênh>`, `message: <Nội dung tin nhắn>` | `channel_id` như node 3, `message` là nội dung tin nhắn. |

> **Lưu ý**: Đảm bảo credential `mattermostApi` đã được cấu hình trong n8n (Settings → Credentials → Mattermost).

### 3. Kích hoạt ⚡️
1. **Test run**: Nhấn “Execute Node” trên từng node để kiểm tra dữ liệu đầu ra (đặc biệt là `channel_id`).
2. **Bật Active**: Khi mọi thứ chạy đúng, bật toggle “Active” ở góc trên bên phải của workflow.

## ✍️ Mẹo & gợi ý nâng cao
- **Gửi tin nhắn định kỳ**: Thêm node `Cron` để tự động gửi báo cáo hàng ngày/tuần.
- **Thông báo qua Slack**: Thêm node `Slack` sau khi tin nhắn được gửi để thông báo tới kênh Slack.
- **Lưu log**: Dùng node `Write Binary File` hoặc `Google Sheets` để ghi lại ID kênh, thời gian tạo, thành viên mời.
- **Xử lý lỗi**: Thêm node `If` để kiểm tra `status` của mỗi API call và gửi email cảnh báo khi có lỗi.

## 📌 Kết luận
Workflow này giúp các sếp nhanh chóng triển khai kênh Mattermost mới, mời thành viên và gửi tin nhắn mà không cần viết một dòng code. Thử ngay, áp dụng vào quy trình làm việc của bạn để tiết kiệm thời gian, giảm lỗi và tăng hiệu suất!