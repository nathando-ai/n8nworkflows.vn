---
title: "🚀 Tự Động Chuyển YouTube Shorts Sang TikTok Miễn Phí - Không Cần Code!"
description: "Workflow tự động hóa hoàn chỉnh giúp các sếp tự động chuyển tất cả YouTube Shorts mới nhất sang TikTok trong vòng 1 giờ, tiết kiệm thời gian và tăng cơ hội viral. Dùng API TikTok và RSS Feed, không cần kỹ năng code."
slug: "tu-dong-chuyen-youtube-shorts-sang-tiktok"
tags: [n8n, automation, social-media, tiktok-api, youtube-shorts, no-code]
keywords: [tự động hóa tiktok youtube, chuyển shorts tiktok tự động, api tiktok, workflow n8n, tự động hóa mạng xã hội, tiết kiệm thời gian content]
---

# 🚀 **Tự Động Chuyển YouTube Shorts Sang TikTok - Giải Pháp Miễn Phí Cho Creator & Agency**

### **Nỗi Đau Của Các Sếp**
Các sếp đang mất **giờ đồng hồ** mỗi ngày để:
- **Tải xuống** YouTube Shorts thủ công.
- **Chỉnh sửa** để phù hợp với TikTok (thời lượng, định dạng, caption).
- **Tải lên** TikTok một cách lặp đi lặp lại.
- **Lo lắng** về việc bỏ lỡ Shorts mới nhất của đối thủ.

**Kết quả?** Content không được tối ưu, mất thời gian, và cơ hội viral bị giảm thiểu.

---
### **🎯 Kết Quả Các Sếp Nhận Được**
✅ **Tiết kiệm 10+ giờ/tuần** - Workflow chạy tự động mỗi giờ.
✅ **Tối ưu hóa nội dung** - Chuyển Shorts sang định dạng phù hợp với TikTok (360p với âm thanh).
✅ **Tăng cơ hội viral** - Đăng lên TikTok ngay khi Shorts mới ra, không bỏ lỡ thời cơ.
✅ **Chế độ Draft/Publish linh hoạt** - Chọn đăng trực tiếp hoặc lưu nháp để chỉnh sửa sau.
✅ **Không cần kỹ năng code** - Cấu hình đơn giản, chỉ cần API keys và một chút cấu hình.

---
## **🎯 Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
🔹 **Tài khoản TikTok Developer** (đăng ký tại [developers.tiktok.com](https://developers.tiktok.com/))
🔹 **API Keys TikTok**:
   - `client_key`
   - `client_secret`
   - `refresh_token` (có hiệu lực 1 năm)
🔹 **API Key RapidAPI** (dùng để tải video từ YouTube)
🔹 **Playlist ID YouTube** (để lấy RSS Feed của Shorts)
🔹 **Tài khoản TikTok** (đã thêm vào sandbox tester trong TikTok Developer)

---
## **🚀 Cách Import & Cấu Hình Workflow**

### **1. Import Workflow 📥**
Các sếp có thể:
- **Tải file JSON** từ [n8n.io/workflows/16171](https://n8n.io/workflows/16171) và import vào n8n Editor.
- **Copy/Paste JSON** từ file này vào n8n Editor (đảm bảo đã chọn **Create Workflow** trước).

### **2. Các Bước Cấu Hình Bắt Buộc 📌**
#### **🔹 Node 1: RSS Feed Trigger (Lấy Shorts mới)**
- **Thay đổi URL RSS Feed**:
  ```
  https://www.youtube.com/feeds/videos.xml?playlist_id=YOUR_PLAYLIST_ID
  ```
  (Thay `YOUR_PLAYLIST_ID` bằng ID playlist Shorts của kênh YouTube).

#### **🔹 Node 2: Deduplication (Tránh trùng lặp)**
- Workflow tự động kiểm tra và bỏ qua Shorts đã được chuyển trước đó.

#### **🔹 Node 3: Get Download Link (Tải video từ YouTube)**
- **Thêm API Key RapidAPI**:
  - Mở node **Get Download Link** → **Headers** → Thêm `x-rapidapi-key: YOUR_RAPIDAPI_KEY`.

#### **🔹 Node 4: TikTok Authentication (Lấy Token TikTok)**
- **Cấu hình 3 trường bắt buộc**:
  - `client_key`: API Key TikTok của bạn.
  - `client_secret`: API Secret TikTok.
  - `refresh_token`: Token refresh (có hiệu lực 1 năm).
- **Lưu ý**: Nếu chưa có `refresh_token`, các sếp phải chạy **Get Refresh Token (One Time Setup)** trước (xem phần sau).

#### **🔹 Node 5: Config (Chọn chế độ Draft/Publish)**
- **Thiết lập `mode`**:
  - `"draft"` → Video được gửi vào hộp nháp TikTok (các sếp phải đăng thủ công sau).
  - `"publish"` → Video được đăng trực tiếp (yêu cầu tài khoản TikTok **private**).
- **Thiết lập `privacy_level`**:
  - `"SELF_ONLY"` (mặc định, không cần audit).
  - Các cấp độ khác (`MUTUAL_FOLLOW_FRIENDS`, `PUBLIC_TO_EVERYONE`) yêu cầu **audit app**.

#### **🔹 Node 6: TikTok Init Draft/Publish (Chọn chế độ)**
- **Chế độ Draft**:
  - Video được gửi vào hộp nháp TikTok.
- **Chế độ Publish**:
  - Video được đăng trực tiếp với **caption** từ mô tả YouTube (có thể thêm hashtag).

#### **🔹 Node 7: Upload Video to TikTok (Tải lên TikTok)**
- Workflow tự động tải video binary lên TikTok theo URL được trả về từ node trước.

---
### **3. Kích Hoạt Workflow ⚡️**
1. **Test Run** với một Shorts mẫu để kiểm tra cấu hình.
2. **Bật Active** workflow.
3. **Monitor Logs** trong n8n để đảm bảo không có lỗi.

---
## **🔑 Get Refresh Token (One-Time Setup)**
**Lưu ý**: Các sếp chỉ cần chạy node này **một lần** để lấy `refresh_token`.

### **Bước Cấu Hình**
1. **Mở URL OAuth TikTok**:
   ```
   https://www.tiktok.com/v2/auth/authorize?
   client_key=YOUR_CLIENT_KEY
   &response_type=code
   &scope=video.publish,video.upload,user.info.basic
   &redirect_uri=YOUR_REDIRECT_URI
   &state=abc123
   ```
   (Thay `YOUR_CLIENT_KEY` và `YOUR_REDIRECT_URI` theo cấu hình TikTok Developer).

2. **Xác nhận quyền** trên TikTok.

3. **Copy `auth_code`** từ URL redirect (phần sau `code=`).

4. **Điền vào node**:
   - `client_key`: API Key TikTok.
   - `client_secret`: API Secret TikTok.
   - `code`: `auth_code` vừa copy.
   - `grant_type`: `authorization_code` (không thay đổi).
   - `redirect_uri`: Cùng với URL OAuth.

5. **Chạy node** và **copy `refresh_token`** từ output để dán vào node **Get TikTok Token**.

---
## **✍️ Mẹo & Gợi Ý Nâng Cao**
🔹 **Tăng tần suất poll RSS Feed**:
   - Thay đổi từ `everyHour` sang `every30minutes` để cập nhật nhanh hơn (nếu cần).

🔹 **Thêm hashtag tự động**:
   - Trong node **TikTok Init Publish**, chỉnh sửa **caption expression** để thêm hashtag:
     ```json
     "{{$json.youtube.description || $json.youtube.title}}#shorts #trending #viral"
     ```

🔹 **Lưu log hoạt động**:
   - Thêm node **Slack/Telegram** để thông báo khi workflow hoàn thành thành công/lỗi.

🔹 **Chuyển nhiều kênh YouTube**:
   - Sử dụng **Multi-RSS Trigger** bằng cách tạo nhiều workflow hoặc sử dụng node **Set** để quản lý nhiều playlist.

---
## **📌 Kết Luận**
Workflow này giúp các sếp **tự động hóa hoàn toàn** quá trình chuyển YouTube Shorts sang TikTok, tiết kiệm **thời gian và công sức** đáng kể. Với cấu hình đơn giản và không cần code, các sếp có thể **tăng cơ hội viral** cho nội dung của mình mà không lo bỏ lỡ bất kỳ Shorts nào.

**🚀 Hành động ngay!**
1. **Import workflow** và cấu hình theo hướng dẫn.
2. **Kích hoạt** và theo dõi kết quả.
3. **Tối ưu hóa** bằng cách thêm hashtag hoặc thay đổi tần suất poll.

**🎁 Đăng ký VPS TinoHost để chạy workflow 24/7**:
👉 [Đăng ký VPS N8N](https://tino.vn/vps-n8n?affid=388) (Mã giảm giá: **VPSN8N** - giảm tới 39%)

---
**💡 Chia sẻ & phản hồi**:
Các sếp có thể chia sẻ kết quả hoặc gặp vấn đề khi cấu hình, hãy để lại comment bên dưới! 👇