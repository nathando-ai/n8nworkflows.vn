---
title: "🚀 Tự động tổng hợp tweet đối thủ hàng ngày với X API, GPT-5-Nano và Gmail"
description: "Giải pháp tự động lấy 5 tweet mới nhất của đối thủ, tóm tắt bằng GPT-5-Nano và gửi báo cáo qua Gmail mỗi ngày."
slug: "tuyendung-tong-hop-tweet-do-thu-hang-ngay"
tags: [n8n, automation, no-code, twitter, openai, gmail, competitor-analysis]
keywords: [n8n workflow, tự động hóa, X API, GPT-5, Gmail, competitor analysis, X tweet summarizer]
---

# 🚀 Tự động tổng hợp tweet đối thủ hàng ngày với X API, GPT-5-Nano và Gmail

Bạn đang phải lướt qua hàng trăm tweet của đối thủ để nắm bắt xu hướng, nhưng thời gian và công sức là điều không thể thiếu? Workflow này sẽ giúp bạn **đánh giá nhanh chóng** 5 tweet mới nhất, **tóm tắt nội dung** bằng trí tuệ nhân tạo và **gửi báo cáo** tới hộp thư của mình mỗi ngày – hoàn toàn **không cần code**.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không còn lướt thủ công, workflow tự động lấy dữ liệu.  
- **Chính xác & nhất quán**: Mỗi lần chạy luôn lấy 5 tweet mới nhất, tránh sai sót.  
- **Cá nhân hóa**: Dễ dàng chỉnh sửa prompt GPT để phù hợp với mục tiêu báo cáo.  
- **Hoạt động liên tục**: Được lên lịch chạy tự động, không cần can thiệp.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Twitter OAuth2**: API key, API secret, Access token, Access token secret.  
- **OpenAI API**: Key cho mô hình `gpt-5-nano`.  
- **Gmail OAuth2**: Đăng nhập Google, cấp quyền gửi email.  
- **HTTP Bearer Auth**: Token truy cập X API (được cung cấp khi đăng ký X Developer).  
- **n8n**: Phiên bản mới nhất, cài đặt trên VPS hoặc local.  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON từ [link workflow](https://n8n.io/workflows/9355) hoặc copy toàn bộ JSON.  
- Trong n8n Editor, chọn **Import** → **Import from clipboard** hoặc **Import from file**.  
- Lưu lại workflow với tên “Daily Competitor Tweet Summarizer”.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Tên Node | Cấu hình cần chỉnh | Ghi chú |
|------|----------|---------------------|---------|
| 1 | **Schedule Trigger** | *Cron* hoặc *Interval* (định kỳ). | Mặc định: 00:00 hàng ngày. |
| 2 | **Get User** | *Username* (hardcode tên người dùng X). | Dùng để lấy `user_id`. |
| 3 | **Fetch Recent Posts** | `max_results` (số tweet). <br>URL: `https://api.twitter.com/2/users/{{ $json["data"]["id"] }}/tweets?max_results=5` | Đảm bảo token Bearer hợp lệ. |
| 4 | **Message a model** | Prompt: “Summarize the following tweets...”. <br>Model: `gpt-5-nano`. | Có thể tùy chỉnh prompt cho mục tiêu báo cáo. |
| 5 | **Send a message** | *To*: email nhận báo cáo. <br>Subject: “Daily Competitor Tweet Summary”. | Kiểm tra quyền gửi email. |

#### 3. Kích hoạt ⚡️
- **Test run**: Chạy workflow thủ công với dữ liệu mẫu để kiểm tra.  
- **Bật Active**: Đánh dấu workflow “Active” để tự động chạy theo lịch.  

### ✍️ Mẹo & gợi ý nâng cao
- **Slack/Telegram notification**: Thêm node Slack hoặc Telegram để nhận thông báo khi báo cáo được gửi.  
- **Lưu log vào Google Sheets**: Dùng node Google Sheets để ghi lại nội dung tweet và tóm tắt.  
- **Báo cáo định kỳ**: Sử dụng node “Schedule Trigger” với cron “0 8 * * *” để gửi báo cáo vào 8h sáng.  
- **Tùy chỉnh độ dài tóm tắt**: Thêm tham số `max_tokens` trong node OpenAI để giới hạn độ dài.  

### 📌 Kết luận
Workflow này giúp các sếp **đánh giá nhanh** chiến lược của đối thủ mà không tốn thời gian. Hãy thử ngay, điều chỉnh theo nhu cầu và tận dụng sức mạnh của X API, GPT-5-Nano và Gmail để luôn nắm bắt thị trường!