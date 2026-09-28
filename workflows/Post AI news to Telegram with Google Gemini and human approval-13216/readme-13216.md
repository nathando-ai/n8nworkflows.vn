---
title: "🤖 Tự Động Hóa Báo Tin AI Trên Telegram Với Gemini + Xác Nhận Người Dùng (N8n)"
description: "Workflow tự động thu thập tin tức AI từ RSS, tóm tắt bằng Google Gemini, và yêu cầu xác nhận người dùng trước khi đăng trên Telegram. Giúp tiết kiệm thời gian 80% trong công việc quản lý tin tức, đồng thời đảm bảo chất lượng nội dung."
slug: "tu-dong-hoa-bao-tin-ai-telegram-gemini-xac-nhan-nguoi-dung"
tags: [n8n, automation, no-code, google-gemini, telegram-bot, ai-summarization, rss-feed]
keywords: [n8n workflow telegram, tự động hóa tin tức AI, google gemini n8n, xác nhận người dùng tự động, rss feed n8n, chatbot telegram tự động]
---

# 🚀 **Tự Động Hóa Báo Tin AI Trên Telegram Với Gemini + Xác Nhận Người Dùng**

## **🔍 Nỗi Đau Của Các Sếp Trong Quản Lý Tin Tức AI**
Hàng ngày, các sếp phải:
- **Tìm kiếm và lọc** tin tức AI từ hàng trăm nguồn RSS khác nhau (VentureBeat, TechCrunch, AI Blog...).
- **Tóm tắt nội dung** dài dòng thành đoạn ngắn gọn, phù hợp với Telegram.
- **Xác nhận chất lượng** trước khi đăng, tránh tin sai lệch hoặc nội dung không phù hợp.
- **Đăng tải thủ công**, mất thời gian và dễ quên.

**Workflow này giải quyết tất cả!** Nó tự động:
✅ **Thu thập tin tức AI** từ RSS feeds.
✅ **Tóm tắt bằng Google Gemini** (AI mạnh nhất hiện nay).
✅ **Yêu cầu xác nhận người dùng** trước khi đăng.
✅ **Đăng tải tự động** chỉ khi được chấp thuận.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80% thời gian** trong việc quản lý tin tức AI.
- **Chất lượng nội dung cao** nhờ Gemini tóm tắt chính xác.
- **Kiểm soát toàn bộ quy trình** với xác nhận người dùng.
- **Hoạt động 24/7** mà không cần can thiệp thủ công.
- **Tích hợp hoàn hảo** với Telegram, không cần code.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Telegram Bot** (để đăng tải tin tức):
   - Tạo bot trên [@BotFather](https://t.me/BotFather) và lấy **API Token**.
   - Chọn **Channel/Group Telegram** để đăng tải.
2. **API Key Google Gemini** (để tóm tắt tin tức):
   - Đăng ký tại [Google AI Studio](https://makersuite.google.com/app/apikey) và lấy **API Key**.
3. **URL RSS Feed** của các nguồn tin AI (ví dụ:
   - [VentureBeat AI](https://venturebeat.com/rss/)
   - [AI Blog RSS](https://example.com/rss-ai)
4. **VPS Self-hosted n8n** (để workflow chạy 24/7):
   - 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
   - 👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

## **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Từ File JSON**
1. Tải workflow từ [n8n.io/workflows/13216](https://n8n.io/workflows/13216) (chọn **Export as JSON**).
2. Trên **n8n Editor**, nhấn **Import** → Chọn file JSON vừa tải.
3. Chọn **Workflow Name** (ví dụ: **"AI News Telegram Bot"**).

#### **Phương pháp 2: Copy/Paste JSON**
1. Copy toàn bộ mã JSON từ [n8n.io/workflows/13216](https://n8n.io/workflows/13216).
2. Trên **n8n Editor**, nhấn **Import** → Chọn **Paste JSON**.
3. Đặt tên workflow và nhấn **Import**.

---

### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**

#### **🔹 Node "Fetch VentureBeat AI feed" & "Fetch AI Blog feed"**
- **Cấu hình RSS Feed**:
  - Điền **URL RSS** của nguồn tin (ví dụ: `https://venturebeat.com/rss/`).
  - Thiết lập **Limit** (số bài viết lấy về, ví dụ: `5`).

#### **🔹 Node "Prepare Gemini Prompt" (Code Node)**
- **Mở Code Editor** và chỉnh sửa template prompt:
  ```javascript
  // Ví dụ template prompt cho Gemini:
  `Tóm tắt bài viết sau thành một đoạn Telegram post ngắn gọn (dưới 300 ký tự), bao gồm:
  - Tiêu đề chính (bold)
  - 2-3 điểm chính (danh sách)
  - Link nguồn
  - Từ khóa: AI, Machine Learning, Deep Learning

  Bài viết:
  {{ $json["title"] }}
  {{ $json["description"] }}
  {{ $json["content"] }}`
  ```
  - **Lưu ý**: Đảm bảo biến `$json` chứa dữ liệu từ RSS feed.

#### **🔹 Node "Keep Top 1 Article" (Code Node)**
- **Chỉnh sửa logic lọc bài viết**:
  ```javascript
  // Chọn bài viết có "views" hoặc "date" mới nhất
  return $input.all()[0]; // Lấy bài viết đầu tiên (cần tùy chỉnh theo logic)
  ```
  - **Lưu ý**: Nếu muốn lọc bài viết mới nhất, sử dụng:
    ```javascript
    const latestArticle = $input.all().sort((a, b) => new Date(b.date) - new Date(a.date))[0];
    return latestArticle;
    ```

#### **🔹 Node "Request approval via Telegram"**
- **Cấu hình Telegram Bot**:
  - **Credentials**: Chọn `telegramApi` (đã cấu hình trước).
  - **Message Template**:
    ```
    📢 **Xác nhận bài viết AI mới!**
    **Tiêu đề:** {{ $json["title"] }}
    **Tóm tắt:** {{ $json["summary"] }}
    **Link:** {{ $json["link"] }}

    ⚠️ **Phím /approve** để đăng tải
    ❌ **Phím /reject** để bỏ qua
    ```
  - **Operation**: Chọn `sendAndWait` (đợi phản hồi người dùng).

#### **🔹 Node "Check approval result" (If Node)**
- **Cấu hình điều kiện**:
  - **If**: Kiểm tra phản hồi Telegram có chứa `/approve` hay không.
  - **Else**: Bỏ qua bài viết (không đăng tải).

#### **🔹 Node "Generate Telegram post (Gemini)"**
- **Credentials**: Chọn `googlePalmApi` (API Key Gemini).
- **Prompt**: Sử dụng template đã chuẩn bị ở **Node "Prepare Gemini Prompt"**.

#### **🔹 Node "Publish approved post to Telegram"**
- **Credentials**: Chọn `telegramApi`.
- **Message Format**:
  ```
  📢 **Bài viết AI mới đã được đăng tải!**
  **Tiêu đề:** {{ $json["title"] }}
  **Nội dung:** {{ $json["summary"] }}
  **Link:** {{ $json["link"] }}
  ```

#### **🔹 Node "Schedule trigger"**
- **Chọn lịch chạy**:
  - Ví dụ: **Lịch chạy hàng ngày lúc 8h sáng** (để cập nhật tin tức mới nhất).
  - Cấu hình tại **Schedule Trigger** → **Recurrence**: `0 8 * * *` (UTC).

---

### **3. Kích Hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Nhấn **Execute Workflow** và kiểm tra từng node.
   - Đảm bảo Telegram bot nhận được tin nhắn yêu cầu xác nhận.
2. **Bật Active**:
   - Chuyển trạng thái workflow từ **Inactive** → **Active**.

---

## **✍️ Mẹo & Gợi Ý Nâng Cao**

### **🔹 Kết hợp với Slack/Email Báo Cáo**
- **Thêm Node Slack/Email** để thông báo khi bài viết được đăng tải.
- **Ví dụ**:
  ```javascript
  // Node Code thêm vào sau "Publish approved post"
  return {
    "message": `🚀 Bài viết "${$json["title"]}" đã được đăng tải trên Telegram!`,
    "channel": "#ai-news"
  };
  ```

### **🔹 Lưu Log Lịch Sử Bài Viêt**
- **Thêm Node Database (n8n-nodes-base.database)** để lưu tất cả bài viết đã xử lý.
- **Cấu hình**:
  - Database: SQLite (đã tích hợp sẵn).
  - Query: `INSERT INTO posts (title, summary, link, status) VALUES (?, ?, ?, ?)`.

### **🔹 Tự Động Chọn Top 3 Bài Viêt**
- **Sửa Node "Keep Top 1 Article"** thành:
  ```javascript
  // Lấy 3 bài viết mới nhất
  const topArticles = $input.all().sort((a, b) => new Date(b.date) - new Date(a.date)).slice(0, 3);
  return topArticles;
  ```
- **Sau đó**, sử dụng **Node Merge** để xử lý song song.

### **🔹 Cập Nhật Tin Tức Theo Thời Gian**
- **Thêm Node "If"** để kiểm tra thời gian đăng tải:
  ```javascript
  // Chỉ đăng bài viết sau 12h trưa
  const now = new Date();
  const isAfterNoon = now.getHours() >= 12;
  return { "isAfterNoon": isAfterNoon };
  ```

---

## **📌 Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc lặp lại trong quản lý tin tức AI, đồng thời **đảm bảo chất lượng** nhờ xác nhận người dùng và tóm tắt bằng Gemini.

**🚀 Hành động ngay!**
1. **Import workflow** và cấu hình theo hướng dẫn.
2. **Test với dữ liệu mẫu** trước khi bật chế độ tự động.
3. **Tích hợp thêm Slack/Email** để báo cáo hiệu quả.

**💡 Gợi ý cuối cùng**: Nếu muốn **tăng tính chuyên nghiệp**, các sếp có thể thêm **thẻ nhãn** cho bài viết (AI, Machine Learning, Robotics...) và **xếp hạng** dựa trên độ quan trọng.

---
**Chia sẻ & phản hồi**: Nếu có vấn đề trong quá trình setup, hãy để lại comment bên dưới hoặc liên hệ với tác giả [Natnail Getachew](https://n8n.io/workflows/13216) để hỗ trợ! 🚀