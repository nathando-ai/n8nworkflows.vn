---
title: "🚀 Tự động tạo chuỗi bài viết trên Bluesky mỗi ngày"
description: "Workflow n8n tự động đăng bài, trả lời và tạo các bài viết liên quan trên Bluesky, giúp bạn duy trì hoạt động mạng xã hội 24/7 mà không cần viết code."
slug: "tu-dong-tao-chuoi-bai-viet-bluesky"
tags: [n8n, automation, no-code, bluesky, marketing, social-media]
keywords: [n8n workflow, tự động hóa, Bluesky, social media automation, tạo thread]
---

# 🚀 Tự động tạo chuỗi bài viết trên Bluesky mỗi ngày

Bạn có bao giờ cảm thấy mệt mỏi vì phải **đăng bài, trả lời và tạo các bài viết liên quan** trên Bluesky một cách thủ công?  
Việc này không chỉ tốn thời gian mà còn dễ gây sai sót, khiến nội dung của bạn không đồng nhất và mất cơ hội tương tác.  

**Workflow “Create Threads on Bluesky”** chính là giải pháp **tự động 100%**, giúp bạn:

* Đăng **bài viết khởi đầu** (Initial Post) vào giờ cố định.  
* Tự động **đăng trả lời** (Reply) và **bài viết cùng luồng** (Sibling) dựa trên các ID (URI & CID) trả về.  
* Lặp lại quá trình tạo các **bài viết phụ** (Sibling Posts) thông qua node `splitInBatches`.  

Kết quả? Bạn có một **chuỗi thread chuyên nghiệp** trên Bluesky mà không cần viết một dòng code nào.

:::info[Gợi ý hạ tầng cho n8n]  
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]  
- **Tiết kiệm thời gian**: Không còn phải mở trình duyệt, copy‑paste nội dung.  
- **Độ chính xác cao**: URI & CID được lấy tự động, tránh lỗi “reply sai luồng”.  
- **Hoạt động liên tục**: Đặt lịch chạy hàng ngày, nội dung luôn tươi mới.  
- **Dễ mở rộng**: Thêm node Slack/Telegram để nhận thông báo ngay khi có bài mới.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]  
- **Tài khoản Bluesky** (handle) và **App Password** (được tạo trong mục Settings → App Passwords).  
- **n8n** đã được cài đặt và có quyền truy cập internet để gọi API Bluesky.  
- **API Endpoint**: `https://bsky.social/xrpc` (được n8n‑node `httpRequest` sử dụng mặc định).  
- **Cron** hoặc **Schedule Trigger** để chạy workflow vào 9 AM mỗi ngày.  
- (Tuỳ chọn) **Webhook** hoặc **Telegram Bot** nếu muốn nhận thông báo khi workflow hoàn thành.  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Tải file JSON của workflow từ trang gốc: <https://n8n.io/workflows/2798>.  
2. Vào **n8n → Workflows → Import** → Chọn file JSON → **Import**.  
3. Hoặc mở **n8n Editor**, nhấn **+** → **Import from Clipboard**, dán toàn bộ JSON và **Save**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Dưới đây là **các node quan trọng** và cách cấu hình chúng:

| Node | Loại | Mô tả | Tham số / Credentials cần điền |
|------|------|------|--------------------------------|
| **Run Daily at 9 AM** | `scheduleTrigger` | Kích hoạt workflow mỗi ngày lúc 09:00. | Đảm bảo múi giờ (Timezone) phù hợp với khu vực của bạn. |
| **Set Bluesky Credentials** | `set` | Lưu `handle` và `appPassword` vào biến tạm. | - `handle` (ví dụ: `sếp@example.com`) <br> - `appPassword` (chuỗi 32 ký tự). |
| **Create Bluesky Session** | `httpRequest` | Đăng nhập, lấy **access token**. | - **Method**: POST <br> - **URL**: `https://bsky.social/xrpc/com.atproto.server.createSession` <br> - **Body (JSON)**: `{ "identifier": {{$json["handle"]}}, "password": {{$json["appPassword"]}} }` <br> - **Response**: Lưu `accessJwt` vào biến `sessionToken`. |
| **Create Initial Post** | `httpRequest` | Đăng bài viết đầu tiên (A). | - **Method**: POST <br> - **URL**: `https://bsky.social/xrpc/com.atproto.repo.createRecord` <br> - **Headers**: `Authorization: Bearer {{$node["Create Bluesky Session"].json.accessJwt}}` <br> - **Body**: Dùng output của node **Create Post Text** (xem dưới). |
| **Create Post Text** | `code` | Tạo nội dung cho bài viết đầu (A). | ```javascript\nreturn { text: `🚀 Bắt đầu chuỗi thread tự động!\n#Bluesky #Automation` };\n``` |
| **Create Reply Text** | `code` | Tạo nội dung cho **bài trả lời đầu** (B). | ```javascript\nreturn { text: `💬 Đây là trả lời đầu tiên, tự động tạo bởi n8n.` };\n``` |
| **Create Reply** | `httpRequest` | Đăng trả lời (B) dựa trên URI/CID của A. | - **ROOT** & **PARENT**: Lấy từ output của **Create Initial Post** (`uri` & `cid`). |
| **Create Sibling** | `httpRequest` | Đăng **bài sibling đầu tiên** (C). | - **ROOT**: URI/CID của A. <br> - **PARENT**: URI/CID trả về từ **Create Reply**. |
| **Create Sibling Text** | `code` | Nội dung cho sibling đầu (C). | ```javascript\nreturn { text: `🔗 Bài sibling 1, nối tiếp thread.` };\n``` |
| **Loop Posts** | `splitInBatches` | Lặp qua danh sách nội dung (có thể tùy chỉnh). | - **Batch Size**: 1 (để tạo từng bài một). |
| **Create Sibling Text (Loop)** | `code` | Nội dung cho các sibling tiếp theo (D). | ```javascript\nreturn { text: `🔁 Sibling ${$itemIndex + 2}: nội dung tự động.` };\n``` |
| **Create Sibling Array** | `code` | Tạo mảng dữ liệu cho node **Loop Posts**. | ```javascript\nreturn [{}, {}, {}]; // số phần tử = số sibling muốn tạo\n``` |
| **Wait** | `wait` | Đặt thời gian chờ giữa các lần tạo (để tránh rate‑limit). | - **Delay**: 5 giây (có thể tăng/giảm). |
| **Create Post** | `httpRequest` | Đăng các sibling tiếp theo (D) trong vòng lặp. | - **ROOT**: URI/CID của A. <br> - **PARENT**: URI/CID của bài trước (lấy từ output của node **Create Sibling** hoặc **Create Post** của vòng lặp trước). |

> **Lưu ý:**  
> - Mọi node `httpRequest` đều cần **Header** `Authorization: Bearer {{$node["Create Bluesky Session"].json.accessJwt}}`.  
> - Khi copy/paste **JSON body**, hãy chắc chắn các trường `repo`, `collection`, `record` (định dạng ATProto) đúng theo tài liệu Bluesky.  
> - Kiểm tra lại **URI** và **CID** được trả về ở mỗi bước; chúng là chìa khóa để duy trì cấu trúc thread.

#### 3. Kích hoạt ⚡️
1. **Test run**: Nhấn nút **Execute Workflow** → Kiểm tra log của mỗi node, đặc biệt là `Create Bluesky Session` và `Create Initial Post`.  
2. Nếu mọi thứ trả về `200 OK` và bạn thấy bài viết trên Bluesky, **bật** chế độ **Active** (nút toggle ở góc phải).  
3. Đợi đến 09:00 hôm sau để xác nhận lịch chạy tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Thông báo Slack/Telegram**: Thêm node `Slack` hoặc `Telegram` sau node `Create Post` để gửi tin nhắn “Thread đã được tạo xong”.  
- **Lưu log vào Google Sheets**: Dùng node `Google Sheets` để ghi lại `timestamp`, `URI`, `CID` của mỗi bài, giúp bạn theo dõi hiệu suất.  
- **Dynamic content**: Thay đổi nội dung trong node `Create Sibling Text (Loop)` bằng cách đọc dữ liệu từ một API tin tức hoặc RSS feed, tạo thread “tin nóng” mỗi ngày.  
- **Quản lý rate‑limit**: Nếu gặp lỗi 429, tăng thời gian `Wait` lên 10–15 giây hoặc giảm batch size.

### 📌 Kết luận
Với **workflow “Create Threads on Bluesky”**, các sếp có thể **tự động duy trì hoạt động nội dung** trên nền tảng xã hội mới nổi, giảm thiểu công sức thủ công và tăng tính nhất quán.  
Hãy **import**, **cấu hình** nhanh chóng, **kích hoạt** và để n8n lo phần còn lại. Đừng quên thử các gợi ý nâng cao để biến workflow thành một trung tâm tự động hoá marketing đa kênh! 🚀