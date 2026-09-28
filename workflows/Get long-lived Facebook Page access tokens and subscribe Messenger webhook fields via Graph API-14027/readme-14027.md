---
title: "🚀 Tự Động Lấy Long-Lived Facebook Page Access Token & Subscribe Webhook"
description: "Hướng dẫn chi tiết cách tự động hóa quy trình đổi token ngắn hạn sang dài hạn, lấy Page Access Token và đăng ký Webhook fields qua Facebook Graph API bằng n8n."
slug: "tu-dong-lay-long-lived-facebook-page-access-token-va-subscribe-webhook"
tags: [n8n, automation, facebook-api, chatbot, messenger, graph-api]
keywords: [n8n workflow, facebook access token, long lived token, facebook webhook, graph api n8n, nguyen thieu toan]
---

# 🚀 Tự Động Lấy Long-Lived Facebook Page Access Token & Subscribe Webhook

Các sếp có bao giờ cảm thấy mệt mỏi mỗi khi làm các dự án chatbot Facebook Messenger hoặc tự động hóa Fanpage mà phải liên tục vào Meta for Developers để copy token ngắn hạn (hết hạn sau vài tiếng), hay thủ công điền từng webhook fields cho từng Page chưa? Việc này vừa mất thời gian, vừa dễ sai sót và làm gián đoạn hệ thống khi token đột ngột "lăn đùng ra chết".

Được chia sẻ bởi chuyên gia **Nguyễn Thiệu Toàn (Jay Nguyen)**, workflow n8n này sẽ giải quyết trọn gói bài toán trên chỉ với 1 cú click chuột. Hệ thống sẽ tự động đổi token ngắn hạn sang **token dài hạn (~60 ngày)**, lấy toàn bộ **Page Access Token** của các Trang mà các sếp quản lý, và tự động **đăng ký (subscribe) các trường webhook** cần thiết thông qua Facebook Graph API một cách trơn tru.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Bỏ hoàn toàn thao tác copy/paste token thủ công từ Meta App Dashboard.
- **Duy trì kết nối bền vững:** Tự động quy đổi và quản lý token dài hạn (~60 ngày) cho toàn bộ Page kết nối.
- **Cấu hình Webhook hàng loạt:** Tự động đồng bộ các trường dữ liệu cần thiết (`messages`, `feed`, v.v.) lên toàn bộ Fanpage trong một nốt nhạc.
- **An toàn giới hạn API:** Tích hợp sẵn cơ chế chờ (Rate limit) thông minh giữa các lần gọi API, tránh việc bị Meta chặn yêu cầu (Rate limit error).
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt sẵn sàng (Cloud hoặc Self-hosted).
- **Meta App:** Có sẵn một ứng dụng trên [Meta for Developers](https://developers.facebook.com/apps/) để lấy **App ID** và **App Secret**.
- **Short-lived User Access Token:** Tạo sẵn một token người dùng ngắn hạn thông qua [Graph API Explorer](https://developers.facebook.com/tools/explorer/) với quyền tối thiểu `pages_manage_metadata`.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow này từ n8n template store.
- Trong giao diện n8n Editor, chọn **Add workflow** -> **Import from File** (hoặc copy toàn bộ JSON và dán trực tiếp vào màn hình làm việc của n8n).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 11 nodes được chia thành 2 phần chính. Các sếp cần chú ý đặc biệt đến node sau:

- **Node `Needed Value` (Loại: Set):** 
  Đây là nơi các sếp phải khai báo 4 tham số cốt lõi trước khi chạy:
  - `app_id`: Lấy từ Meta App Dashboard của các sếp.
  - `app_secret`: Lấy từ Meta App Dashboard (phần cài đặt ứng dụng).
  - `short_user_access_token`: Token ngắn hạn vừa tạo từ Graph API Explorer.
  - `field_to_add`: Các trường webhook muốn đăng ký (Ví dụ: `messages,messaging_postbacks,feed`).

- **Các node `HTTP Request` (Token Exchange & Webhook Subscription):**
  - `Get long-lived user access token`
  - `Get app scoped user id`
  - `Get long-lived page access token`
  - `GET Current Fields`
  - `POST Merged Fields`
  *Lưu ý:* Các node này đã được cấu hình sẵn endpoint chuẩn của Facebook Graph API (`graph.facebook.com/v...`), các sếp chỉ cần giữ nguyên và đảm bảo node `Needed Value` truyền dữ liệu chính xác vào là hệ thống tự chạy.

- **Node `Wait 1s (rate limit)`:** Giúp giãn cách các request khi vòng lặp (`Loop Over Items`) duyệt qua từng Fanpage, giữ cho tài khoản không bị phía Facebook khóa tạm thời do spam API.

#### 3. Kích hoạt ⚡️
- Click vào nút **"Execute Workflow"** để test chạy thủ công lần đầu tiên.
- Kiểm tra kết quả đầu ra tại node cuối cùng để lấy danh sách **Page Access Token** chính xác phục vụ cho các chatbot workflows khác.
- Sau khi kiểm tra mọi thứ mượt mà, bật công tắc **Active** ở góc trên cùng bên phải để hoàn tất.

### ✍️ Mẹo & gợi ý nâng cao
- **Tự động hóa chu kỳ token:** Thay thế node `Manual Trigger` bằng `Schedule Trigger` (đặt lịch chạy mỗi 50 ngày) để tự động làm mới vòng đời token trước khi chúng hết hạn.
- **Cảnh báo qua Telegram/Slack:** Thêm một node Telegram hoặc Slack vào cuối chuỗi để nhận thông báo ngay khi workflow hoàn tất việc cập nhật token và webhook cho các Fanpage.
- **Kết hợp hệ thống Chatbot:** Sử dụng Page Access Token xuất ra từ workflow này để lắp vào các template Chatbot AI Gemini hoặc hệ thống chăm sóc khách hàng tự động.

### 📌 Kết luận
Workflow này là "vũ khí bí mật" giúp các lập trình viên no-code và doanh nghiệp tiết kiệm hàng giờ cấu hình thủ công mỗi khi triển khai dự án Facebook Marketing hay Chatbot Messenger. Hãy áp dụng ngay vào hệ thống của các sếp để tối ưu hóa vận hành ngay hôm nay!