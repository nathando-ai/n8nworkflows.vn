---
title: "🚀 Tự động đăng nội dung Reddit mới nhất lên Discord với trích xuất hình ảnh"
description: "Giải pháp tự động 100% không cần code để lấy bài viết mới nhất từ subreddit, lọc và trích xuất hình ảnh, rồi đăng lên Discord."
slug: "tuyendung-reddit-nhat-nhien-len-discord"
tags: [n8n, automation, no-code, reddit, discord, ai]
keywords: [n8n workflow, tự động hóa, reddit, discord, AI, trích xuất hình ảnh]
---

# 🚀 Tự động đăng nội dung Reddit mới nhất lên Discord với trích xuất hình ảnh

Bạn đang phải mất hàng giờ mỗi ngày để kiểm tra subreddit, sao chép bài viết, trích xuất hình ảnh và đăng lên Discord? Đừng lo, workflow n8n này sẽ giúp bạn hoàn toàn tự động hoá quy trình, tiết kiệm thời gian và giảm sai sót. Bạn chỉ cần cấu hình một lần, workflow sẽ chạy 24/7, lấy bài viết mới nhất, lọc những bài không cần thiết, trích xuất URL hình ảnh và gửi ngay lên kênh Discord mà không cần viết một dòng code.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

## 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Từ vài phút thành vài giây.  
- **Chính xác 100%**: Không còn lỗi copy‑paste hay trích xuất sai URL.  
- **Cá nhân hóa**: Dễ dàng điều chỉnh tiêu chí lọc, nội dung, định dạng tin nhắn.  
- **Hoạt động liên tục**: Chạy tự động theo lịch, không cần can thiệp thủ công.  
:::

## 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản Reddit**: Tạo ứng dụng OAuth2, lấy `Client ID`, `Client Secret` và `Redirect URI` (địa chỉ base URL của n8n).  
- **Tài khoản Discord**: Tạo webhook trong kênh cần đăng, sao chép `Webhook URL`.  
- **N8n**: Đã cài đặt và chạy (Self‑hosted hoặc n8n.cloud).  
- **Cấu hình subreddit**: Cần nhập tên subreddit trong hai node Reddit (`getAll` và `get`).  
:::

## 🚀 Cách import & Lưu ý khi "lên đồ"

### 1. Import Workflow 📥
1. Tải file JSON của workflow từ [link gốc](https://n8n.io/workflows/5105).  
2. Trong n8n, vào **Workflows → Import** → **Upload JSON**.  
3. Chọn file vừa tải, nhấn **Import**.

### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Tên node | Cấu hình cần chỉnh | Ghi chú |
|------|----------|---------------------|---------|
| 1 | `Schedule Trigger` | **Cron**: `0 */6 * * *` (tùy chỉnh) | Thời gian kiểm tra mới nhất. |
| 2 | `Fetch latest reddit posts` | **Subreddit**: `r/your_subreddit` | Lấy danh sách bài viết mới nhất. |
| 3 | `Filter out announcement posts` | **Conditions**: `{{ $json["data"]["children"][0]["data"]["post_hint"] !== "self" }}` | Loại bỏ bài thông báo, chỉ lấy bài có hình ảnh. |
| 4 | `Fetch Reddit Post` | **Post ID**: `{{ $json["data"]["children"][0]["data"]["id"] }}` | Lấy chi tiết bài viết. |
| 5 | `Extract Image URL` | **Code**: `return [{ json: { imageUrl: $json.data.url } }];` | Trích xuất URL hình ảnh trực tiếp. |
| 6 | `Send to discord` | **Webhook URL**: `{{ $json["webhookUrl"] }}` | Định dạng tin nhắn: `{{ $json["data"]["title"] }}` + hình ảnh. |
| 7 | `Sticky Note` | **Note**: Ghi chú công việc, ghi nhớ các bước cấu hình. | Dùng để ghi chú nhanh. |

> **Lưu ý**: Đảm bảo các credentials (`redditOAuth2Api`, `discordWebhookApi`) đã được tạo và gắn vào các node tương ứng.

### 3. Kích hoạt ⚡️
1. **Test run**: Nhấn **Execute Workflow** với dữ liệu mẫu để kiểm tra.  
2. Kiểm tra Discord: Đảm bảo tin nhắn xuất hiện đúng định dạng.  
3. Bật **Active**: Khi mọi thứ ổn, bật trạng thái **Active** để workflow tự động chạy theo lịch.

## ✍️ Mẹo & gợi ý nâng cao
- **Thêm Slack**: Thêm node `Slack` để gửi thông báo đồng thời.  
- **Lưu log**: Dùng node `Google Sheets` hoặc `MySQL` để ghi lại lịch sử bài viết đã đăng.  
- **Báo cáo định kỳ**: Thêm node `Schedule Trigger` khác để gửi báo cáo hàng ngày về số bài đăng.  
- **Tùy chỉnh nội dung**: Sử dụng `Set` node để thay đổi tiêu đề, mô tả trước khi gửi.  

## 📌 Kết luận
Workflow này giúp các sếp tiết kiệm thời gian, giảm sai sót và duy trì sự hiện diện liên tục trên Discord mà không cần viết code. Hãy thử ngay, cấu hình nhanh chóng và tận hưởng lợi ích của tự động hoá 100%!

---