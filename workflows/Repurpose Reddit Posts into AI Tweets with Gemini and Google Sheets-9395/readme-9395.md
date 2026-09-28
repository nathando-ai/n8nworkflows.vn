---
title: "🚀 Tự Động Hóa Chuyển Đổi Bài Đăng Reddit thành Tweet AI với Gemini & Google Sheets"
description: "Workflow tự động hóa lấy 10 bài đăng mới nhất từ subreddit ngẫu nhiên, sử dụng AI Gemini tạo tweet hấp dẫn, đăng lên Twitter và lưu log vào Google Sheets để tránh trùng lặp. Giúp các sếp tiết kiệm 10+ giờ/tháng làm thủ công."
slug: "tieu-dong-hoa-chuyen-doi-bai-dang-reddit-thanh-tweet-ai"
tags: [n8n, automation, no-code, ai-agent, google-sheets, twitter-automation, gemini-ai]
keywords: [n8n workflow reddit twitter, tự động hóa marketing, ai agent n8n, gemini api twitter, tự động đăng tweet từ reddit]
---

# 🚀 **Tự Động Hóa Chuyển Đổi Bài Đăng Reddit thành Tweet AI với Gemini & Google Sheets**

## **Nỗi Đau Của Các Sếp**
Các sếp marketing, content creator hay người quản lý cộng đồng thường phải:
- **Tìm kiếm nội dung** từ Reddit để chia sẻ trên Twitter (hoặc các nền tảng khác).
- **Chuyển đổi nội dung** từ bài đăng dài thành tweet ngắn gọn, hấp dẫn.
- **Tránh trùng lặp** để không làm mất uy tín với cộng đồng.
- **Làm thủ công** hàng ngày, tiêu tốn **10+ giờ/tháng** chỉ để tự động hóa một công việc đơn giản.

**Workflow này giải quyết tất cả!** Sử dụng **AI Gemini** để tự động viết tweet từ bài đăng Reddit, đăng lên Twitter và **lưu log vào Google Sheets** để tránh trùng lặp. **Không cần code, chỉ cần copy/paste và chạy!**

---
### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm 10+ giờ/tháng** làm thủ công tìm kiếm và viết tweet.
✅ **Nội dung cá nhân hóa** với AI Gemini tạo tweet hấp dẫn, ngắn gọn.
✅ **Tránh trùng lặp** bằng cách lưu ID bài đăng đã xử lý vào Google Sheets.
✅ **Hoạt động 24/7** với trigger lịch trình (Schedule Trigger).
✅ **Dễ dàng mở rộng** cho nhiều subreddit khác nhau.
:::

---
## 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
### **1. Tài Khoản & API Keys**
| **Dịch Vụ**       | **Thông Tin Cần Thiết**                          | **Liên Hệ Đăng Ký**                          |
|-------------------|------------------------------------------------|-----------------------------------------------|
| **Reddit**        | OAuth2 API Key (Client ID & Secret)            | [Reddit API](https://www.reddit.com/prefs/apps) |
| **Twitter (X)**   | OAuth2 API Key (Bearer Token)                  | [Twitter Developer Portal](https://developer.x.com/) |
| **Google Sheets** | OAuth2 API Key (Service Account)               | [Google Cloud Console](https://console.cloud.google.com/) |
| **Google Gemini** | API Key (Palm API)                            | [Google AI Studio](https://aistudio.google/) |

### **2. Google Sheets**
- **Tạo 1 bảng mới** với 2 cột:
  - `Post ID` (lưu ID bài đăng Reddit đã xử lý)
  - `Timestamp` (thời gian xử lý)
- **Chia sẻ bảng** với quyền **Editor** cho n8n.

---
## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. **Tải workflow** từ [n8n.io/workflows/9395](https://n8n.io/workflows/9395) (chọn **Export as JSON**).
2. **Mở n8n Editor** và nhấn **Import** → **Paste JSON**.
3. **Chọn "Create new workflow"** và nhấn **Import**.

#### **Phương pháp 2: Copy/Paste JSON**
1. **Copy toàn bộ JSON** từ [n8n.io/workflows/9395](https://n8n.io/workflows/9395).
2. **Mở n8n Editor** → **Create new workflow** → **Paste JSON** → **Import**.

---
### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**

#### **🔹 Node 1: Schedule Trigger1 (Trigger Lịch Trình)**
- **Cấu hình:**
  - **Frequency:** Chọn **Daily** (hoặc **Every 6 hours** để tăng tần suất).
  - **Time:** Đặt giờ phù hợp (ví dụ: **8h sáng** để tweet vào buổi sáng).

#### **🔹 Node 2: Get many posts in Reddit1 (Lấy Bài Đăng Reddit)**
- **Cấu hình:**
  - **Subreddits:** Điền danh sách subreddit muốn lấy bài đăng (ví dụ: `["n8n", "microsaas", "SaaS", "automation", "n8n_ai_agents"]`).
  - **Limit:** Đặt **10** (lấy 10 bài đăng mới nhất).
  - **Credentials:** Chọn `redditOAuth2Api` (đã cấu hình trước).

#### **🔹 Node 3: Structured Output Parser2 (Xử Lý Dữ Liệu)**
- **Lưu ý:** Node này **không cần chỉnh sửa**, n8n sẽ tự động phân tích dữ liệu từ Reddit.

#### **🔹 Node 4: Tweet maker1 (AI Agent Gemini)**
- **Cấu hình:**
  - **Prompt:** AI sẽ tự động tạo tweet từ bài đăng Reddit. **Không cần chỉnh sửa** (nếu muốn tùy chỉnh, chỉnh ở **Code1** sau).
  - **Model:** Chọn **Gemini Pro** (hoặc **Gemini Flash** nếu muốn tiết kiệm chi phí).
  - **Credentials:** Chọn `googlePalmApi` (API Key đã đăng ký).

#### **🔹 Node 5: Code1 (Tùy Chỉnh Prompt AI)**
- **Mã mặc định:**
  ```javascript
  // Chỉnh sửa prompt để AI viết tweet ngắn gọn hơn
  const redditPost = $input.all()[0].json;
  const prompt = `
    You are a Twitter content creator. Convert this Reddit post into a short, engaging tweet (max 280 characters).
    Post: ${redditPost.body}
    Rules:
    1. Keep it concise and to the point.
    2. Add a relevant hashtag.
    3. Use emojis if appropriate.
    4. Avoid replying to comments.
    Tweet:
  `;
  return { tweet: prompt };
  ```
- **Lưu ý:**
  - Nếu muốn **AI thêm hashtag tự động**, chỉnh sửa mã trên.
  - Nếu muốn **AI viết tweet dài hơn**, giảm yêu cầu "max 280 characters".

#### **🔹 Node 6: Creates the tweet1 (Đăng Tweet lên Twitter)**
- **Cấu hình:**
  - **Status:** Chọn **$node["Tweet maker1"].json.tweet** (tweet đã tạo bởi AI).
  - **Credentials:** Chọn `twitterOAuth2Api` (Bearer Token đã đăng ký).

#### **🔹 Node 7: Append row in sheet1 (Lưu Log vào Google Sheets)**
- **Cấu hình:**
  - **Sheet Name:** Điền tên bảng Google Sheets (ví dụ: `Reddit_Tweets_Log`).
  - **Range:** Điền `Post ID!A2` (cột `Post ID` bắt đầu từ hàng 2).
  - **Values:** Chọn **$node["Get many posts in Reddit1"].json.data[0].id** (ID bài đăng Reddit).
  - **Credentials:** Chọn `googleSheetsOAuth2Api`.

#### **🔹 Node 8: Edit Fields1 (Chỉnh Sửa Dữ Liệu Trước Khi Lưu)**
- **Lưu ý:** Node này **không cần chỉnh sửa**, n8n tự động chuẩn hóa dữ liệu.

---
### **3. Kích Hoạt ⚡️ Workflow**
1. **Test Run** với dữ liệu mẫu:
   - Nhấn **Execute Workflow** và kiểm tra:
     - AI có tạo tweet không?
     - Tweet có đăng lên Twitter không?
     - Dữ liệu có được lưu vào Google Sheets không?
2. **Bật Active** nếu test thành công.

---
## ✍️ **Mẹo & Gợi Ý Nâng Cao**
### **1. Thêm Nhiều Subreddit**
- Mở rộng danh sách subreddit trong **Node "Get many posts in Reddit1"** để lấy bài đăng từ nhiều topic khác nhau.

### **2. Gửi Báo Cáo Định Kỳ**
- **Thêm Node "Email"** (n8n-nodes-base.email) sau **Node "Append row in sheet1"** để gửi báo cáo hàng tuần về email.

### **3. Lưu Log vào Slack/Telegram**
- Thay thế **Google Sheets** bằng **Slack Webhook** hoặc **Telegram Bot** để thông báo khi tweet được đăng.

### **4. Tùy Chỉnh AI Gemini**
- Nếu muốn **AI viết tweet theo phong cách riêng**, chỉnh sửa **Code1** để thay đổi prompt:
  ```javascript
  const prompt = `
    You are a Vietnamese Twitter content creator. Write a tweet in Vietnamese style (short, engaging, and local-friendly).
    Post: ${redditPost.body}
    Rules:
    1. Max 280 characters.
    2. Use Vietnamese slang if appropriate.
    3. Add a trending hashtag in Vietnam.
    Tweet:
  `;
  ```

### **5. Dùng AI Agent Cho Nhiều Nền Tảng**
- **Mở rộng workflow** để tweet cũng được đăng lên **Facebook, LinkedIn** bằng cách thêm **Node "Facebook"** hoặc **Node "LinkedIn API"**.

---
## 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp để tập trung vào chiến lược marketing hơn. **Chỉ cần 5 phút setup**, workflow sẽ tự động:
✔ **Lấy bài đăng Reddit mới nhất.**
✔ **Viết tweet hấp dẫn với AI Gemini.**
✔ **Đăng tweet lên Twitter.**
✔ **Lưu log để tránh trùng lặp.**

**Hãy áp dụng ngay và tự động hóa công việc marketing của mình!** 🚀

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**Bạn có thắc mắc gì?** Hãy để lại comment dưới đây, chúng tôi sẽ hỗ trợ! 😊