---
title: "🚀 Tự Động Hóa Phân Tích Sentiment Reddit cho WWDC25 Apple bằng AI Gemini + Google Sheets"
description: "Workflow tự động hóa 100% không code để scrap và phân tích tình cảm (sentiment) của cộng đồng Reddit về sự kiện WWDC25 Apple, kết hợp AI Gemini và Google Sheets để báo cáo tự động. Giúp các sếp nhanh chóng hiểu xu hướng, phản ứng và cảm xúc của người dùng, tối ưu chiến lược marketing."
slug: "tieu-dong-hoa-phan-tich-sentiment-reddit-wwdc25-apple-gemini-google-sheets"
tags: [n8n, automation, ai, marketing, google-sheets]
keywords: [n8n workflow, tự động hóa sentiment analysis, reddit api, gemini ai, phân tích marketing apple, tự động hóa no-code]
---

# 🚀 **Tự Động Hóa Phân Tích Sentiment Reddit cho WWDC25 Apple bằng AI Gemini + Google Sheets**

### **📌 Nỗi Đau Của Các Sếp**
Hàng năm, sự kiện **WWDC (Worldwide Developers Conference) của Apple** thu hút hàng triệu nhà phát triển và fan hâm mộ trên toàn cầu. Tuy nhiên, để **hiểu rõ phản ứng, xu hướng và tình cảm (sentiment) của cộng đồng** về các tin tức mới nhất, các sếp phải:
- **Scrap thủ công** hàng ngàn bài đăng trên Reddit (r/apple, r/iOS, r/macOS, ...).
- **Phân tích từng comment** để xác định xu hướng tích cực/tiêu cực.
- **Tập hợp dữ liệu** vào bảng tính Google Sheets để báo cáo cho ban lãnh đạo.
- **Tốn thời gian** và dễ bị lỗi do thủ công.

**Workflow này giải quyết tất cả vấn đề trên bằng cách tự động hóa toàn bộ quy trình với AI Gemini và Google Sheets!**

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS chuyên dụng.
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (đảm bảo tốc độ cao cho AI)
:::

---

## 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian** – Không cần scrap thủ công, phân tích từng comment.
✅ **Dữ liệu chính xác** – AI Gemini phân tích **tình cảm (sentiment) chi tiết** (tích cực, tiêu cực, trung lập).
✅ **Báo cáo tự động** – Kết quả được ghi vào **Google Sheets** với định dạng sẵn sàng cho báo cáo.
✅ **Hoạt động liên tục** – Workflow chạy **24/7** mà không cần can thiệp.
✅ **Cá nhân hóa** – Có thể **lọc theo chủ đề** (chỉ lấy comment liên quan đến WWDC25).
:::

---

## 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
✔ **API Key Google Gemini** (để phân tích sentiment)
✔ **Google Sheets OAuth 2.0** (để ghi kết quả)
✔ **Tài khoản Reddit API** (để scrap dữ liệu)
✔ **Thời gian chờ** (do API Reddit có giới hạn request)

---

## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. Tải workflow từ [n8n.io/workflows/4980](https://n8n.io/workflows/4980) (chọn **Export as JSON**).
2. Trên **n8n Editor**, nhấn **Import** → Chọn file JSON vừa tải.
3. Chọn **Create new workflow** và nhấn **Import**.

#### **Phương pháp 2: Copy/Paste JSON**
1. Mở **n8n Editor** → Nhấn **Create new workflow**.
2. Chọn **Import** → **Paste JSON** và dán nội dung từ [n8n.io/workflows/4980](https://n8n.io/workflows/4980).
3. Nhấn **Import**.

---

### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**

#### **🔹 Node "scrap reddit" (HTTP Request)**
- **URL:** `https://api.pushshift.io/reddit/search/comment/?subreddit=apple&size=100&fields=body,score,created_utc`
  - **Lưu ý:** Thay đổi `subreddit` để lấy dữ liệu từ các subreddit khác (ví dụ: `iOS`, `macOS`).
  - **Tham số quan trọng:**
    - `size=100` (số lượng comment scrap mỗi lần).
    - `fields=body,score,created_utc` (chỉ lấy nội dung, điểm số và thời gian).

#### **🔹 Node "Google Gemini Chat Model" (Sentiment Analysis)**
- **Credentials:** Chọn `googlePalmApi` (đã cấu hình trước).
- **Prompt mẫu:**
  ```plaintext
  Analyze the sentiment of this Reddit comment: "{comment_body}"
  Return in JSON format: {"sentiment": "positive/negative/neutral", "confidence": 0-1}
  ```
- **Lưu ý:**
  - Nếu API Gemini trả về lỗi, kiểm tra **API Key** và **quota** (Google Gemini có giới hạn request/month).

#### **🔹 Node "Append Sentiments" (Google Sheets)**
- **Credentials:** Chọn `googleSheetsOAuth2Api`.
- **Sheet Name:** Đặt tên bảng tính (ví dụ: `WWDC25_Sentiment_Analysis`).
- **Headers:** Đảm bảo cột `comment`, `sentiment`, `confidence` được định nghĩa.
- **Operation:** Chọn `appendOrUpdate` để ghi dữ liệu mới.

#### **🔹 Node "Text Classifier" (Lọc comment liên quan WWDC25)**
- **Model:** Chọn `text-classification` (n8n LangChain).
- **Prompt:**
  ```plaintext
  Classify this Reddit comment as "WWDC25" or "No category".
  Only return "WWDC25" if the comment mentions WWDC25, Apple Silicon, new iOS features, or WWDC keynote.
  ```
- **Lưu ý:** Nếu comment không liên quan, nó sẽ được **loop lại** để phân loại chính xác.

#### **🔹 Node "Wait" (Thời gian chờ)**
- **Thời gian:** Đặt **5-10 giây** để API Reddit trả về kết quả đầy đủ.

---

### **3. Kích Hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Nhấn **Execute Workflow** và kiểm tra kết quả trong **Google Sheets**.
   - Đảm bảo **sentiment** được phân tích chính xác.
2. **Bật Active Workflow**:
   - Chuyển trạng thái từ **Inactive** sang **Active**.
   - **Lưu ý:** Workflow sẽ chạy **mỗi khi kích hoạt thủ công** (do sử dụng `manualTrigger`).

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**

### **🔹 Kết hợp với Slack/Telegram để báo cáo tự động**
- Thêm **node `n8n-nodes-base.slack`** sau `Append Sentiments` để gửi **tin nhắn báo cáo** khi có dữ liệu mới.
- **Prompt Slack:**
  ```plaintext
  🚀 **WWDC25 Sentiment Update**
  - Tổng comment: {total_comments}
  - Tích cực: {positive_count} ({positive_percentage}%)
  - Tiêu cực: {negative_count} ({negative_percentage}%)
  - Link: {google_sheets_link}
  ```

### **🔹 Lưu log vào Google Drive**
- Thêm **node `n8n-nodes-base.googleDrive`** để lưu **log hoạt động** của workflow.
- **Tiện ích:** Giúp theo dõi lỗi và lịch sử chạy.

### **🔹 Chạy định kỳ với n8n Cron**
- Cấu hình **n8n Cron** để workflow chạy **mỗi ngày** (ví dụ: 8h sáng) để cập nhật sentiment mới nhất.
- **Cú pháp Cron:** `0 8 * * *` (8h hàng ngày).

### **🔹 Phân tích chi tiết hơn với nuanced emotions**
- Thay vì chỉ **tích cực/tiêu cực/trung lập**, có thể yêu cầu AI phân tích **cảm xúc cụ thể** như:
  ```plaintext
  Analyze nuanced emotions: excitement, frustration, curiosity, disappointment.
  ```

---

## 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc scrap và phân tích thủ công, đồng thời cung cấp **dữ liệu sentiment chính xác** để tối ưu chiến lược marketing cho WWDC25.

**🚀 Hãy áp dụng ngay và hiểu rõ hơn phản ứng của cộng đồng Apple!**

---
**🔗 [Xem workflow gốc](https://n8n.io/workflows/4980) | 📌 [Cài đặt n8n trên VPS](https://docs.n8n.io/hosting/installation/installation-on-a-vps/)**