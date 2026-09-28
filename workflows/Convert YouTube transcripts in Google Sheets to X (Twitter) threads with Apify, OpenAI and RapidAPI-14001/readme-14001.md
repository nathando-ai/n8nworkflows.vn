---
title: "🚀 Chuyển Transcript YouTube Sang Thread Twitter Tự Động - Khai Thác AI & API Miễn Phí"
description: "Workflow tự động hóa hoàn toàn chuyển transcript video YouTube thành thread Twitter hấp dẫn, cá nhân hóa, và phù hợp với người dùng Việt - tiết kiệm 100% thời gian soạn thảo thủ công."
slug: "chuyen-transcript-youtube-sang-thread-twitter-tu-dong"
tags: [n8n, automation, social-media, ai-chatbot, google-sheets, twitter-automation]
keywords: [n8n workflow youtube twitter, tự động hóa content twitter, convert transcript youtube, ai tạo thread twitter, apify openai rapidapi]
---

# 🚀 **Tự Động Hóa Chuyển Transcript YouTube → Thread Twitter Hấp Dẫn Với AI & API**

### **Nỗi Đau Của Các Sếp**
- **Thủ công chuyển transcript YouTube thành thread Twitter mất nhiều thời gian** (thường 30-60 phút/1 video).
- **Nội dung AI "cứng nhắc"** khi copy-paste transcript nguyên văn, mất tính hấp dẫn.
- **Không theo dõi được tiến trình xử lý** các video, dẫn đến trùng lặp công việc.
- **Không tối ưu hóa cho người dùng Việt**, dẫn đến tỷ lệ tương tác thấp.

**Workflow này giải quyết tất cả!** Sử dụng **Google Sheets + Apify + OpenAI + RapidAPI**, tự động:
✅ Chuyển transcript YouTube → Thread Twitter **một cách tự nhiên, hấp dẫn**.
✅ **Tối ưu hóa nội dung** với AI ChatGPT (gpt-5-mini) để tránh cảm giác "AI nói".
✅ **Tự động hóa hoàn toàn** từ lấy link video đến đăng thread, không cần can thiệp thủ công.
✅ **Lưu trạng thái xử lý** trong Google Sheets để tránh trùng lặp.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7**, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 5-10 giờ/Tháng** soạn thảo thread thủ công.
- **Tăng tỷ lệ tương tác** với thread tự nhiên, hấp dẫn (không giống AI).
- **Hoạt động liên tục** 24/7, không phụ thuộc vào thời gian làm việc.
- **Dễ dàng mở rộng** cho nhiều video, kênh YouTube khác.
- **Miễn phí** (sử dụng API miễn phí của Apify, OpenAI, và RapidAPI).
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Google Sheets** (để lưu danh sách video và trạng thái xử lý).
2. **Tài khoản Apify** (để lấy transcript YouTube).
3. **Tài khoản OpenAI** (để sử dụng mô hình `gpt-5-mini`).
4. **Tài khoản Twitter (X)** và **cookie** để đăng thread.
5. **API Key RapidAPI** (để đăng thread vào Twitter).

---
### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/14001](https://n8n.io/workflows/14001) hoặc copy/paste JSON vào **n8n Editor**.
- **Cách import**:
  ```bash
  # Nếu sử dụng CLI:
  n8n import workflow.json --name "Youtube-to-Twitter-Thread"
  ```
  - **Trong giao diện web**:
    1. Mở **n8n Editor** → Nhấn **"Import"** → Dán JSON → Chọn **"Import"**.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
##### **A. Cấu Hình Google Sheets**
- **Mẫu Sheet**:
  | Video                          | Processed |
  |---------------------------------|-----------|
  | `https://www.youtube.com/watch?v=abc123` | No       |
  | `https://www.youtube.com/watch?v=xyz456` | No       |

- **Node "Get YouTube Links from Sheet"**:
  - Chọn **credentials**: `googleSheetsOAuth2Api`.
  - **Range**: `Sheet1!A2:B` (đảm bảo không bao gồm header).
  - **Filter**: `Processed = "No"` (để lấy chỉ video chưa xử lý).

##### **B. Cấu Hình Apify Transcript Scraper**
- **Node "Apify YouTube Transcript Scraper"**:
  - **URL**: `https://api.apify.com/v2/actors/your-actor-id/runs`
  - **Headers**:
    ```json
    {
      "Authorization": "Bearer YOUR_APIFY_API_TOKEN",
      "Content-Type": "application/json"
    }
    ```
  - **Body**:
    ```json
    {
      "input": {
        "startUrls": ["{{$json["videoUrl"]}}"]
      }
    }
    ```
  - **Lưu ý**: Thay `your-actor-id` bằng ID của [Apify YouTube Transcript Scraper](https://apify.com/supreme_coder/youtube-transcript-scraper).

##### **C. Cấu Hình OpenAI (ChatGPT)**
- **Node "OpenAI Chat Model"**:
  - **Credentials**: `openAiApi`.
  - **Model**: `gpt-5-mini` (được cấu hình sẵn).
  - **Prompt**:
    ```json
    {
      "system": "Bạn là chuyên gia tạo thread Twitter. Chuyển transcript YouTube thành thread hấp dẫn, dưới 280 ký tự/tweet, với hook và CTA. Tránh cảm giác AI nói.",
      "user": "Video Title: {{Title}}\n\nTranscript: {{Transcript}}"
    }
    ```
  - **Output Format**: JSON structured (được xử lý bởi node `Structured Output Parser`).

##### **D. Cấu Hình Twitter (X) Cookies**
- **Node "Publish Thread with RapidAPI/X API"**:
  - **URL**: `https://x.com/i/api/graphql/...` (mã API từ RapidAPI).
  - **Headers**:
    ```json
    {
      "Cookie": "YOUR_TWITTER_COOKIES",
      "X-RapidAPI-Key": "YOUR_RAPIDAPI_KEY",
      "Content-Type": "application/json"
    }
    ```
  - **Body**:
    ```json
    {
      "variables": {
        "tweet_text": "{{$json.thread[0].text}}",
        "include_media": false
      }
    }
    ```
  - **Lấy cookie Twitter**:
    1. Cài **Cookie-Editor** (Chrome Extension).
    2. Đăng nhập Twitter → Mở Cookie-Editor → Copy **Header string** → Dán vào node.

##### **E. Cấu Hình Schedule Trigger (Nếu Muốn Chạy Định Kỳ)**
- **Node "Schedule Trigger"**:
  - Chọn **cron job** (ví dụ: `0 0 * * *` để chạy hàng ngày 00:00).

##### **F. Cập Nhật Trạng Thái Xử Lý**
- **Node "Mark Link as Processed"**:
  - **Credentials**: `googleSheetsOAuth2Api`.
  - **Range**: `Sheet1!A2:B`.
  - **Value**: `Processed = "Yes"` (để đánh dấu video đã xử lý).

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Nhấn **"Execute"** với 1 video mẫu để kiểm tra.
   - Kiểm tra **Apify Console** và **Twitter** để xác nhận thread được đăng thành công.
2. **Bật Active**:
   - Chuyển trạng thái workflow sang **"Active"**.
   - **Lưu ý**: Nếu dùng **Schedule Trigger**, workflow sẽ tự chạy theo lịch.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tối Ưu Hóa Prompt**:
   - Thay đổi **prompt** để phù hợp với **ngôn ngữ Việt** (ví dụ: thêm ví dụ cụ thể về thị trường Việt).
   - Thử mô hình **gpt-4** (nếu có API key) để nội dung chất lượng hơn.

2. **Lưu Log & Theo Dõi**:
   - Sử dụng **n8n Webhook** để nhận thông báo khi thread được đăng thành công.
   - Lưu **link thread** vào Google Sheets để theo dõi hiệu quả.

3. **Kết Hợp Slack/Telegram**:
   - Thêm node **Slack/Telegram** để thông báo khi workflow hoàn thành.

4. **Xử Lý Video Nhiều Chương**:
   - Nếu video có nhiều chương, thêm **filter** để lấy transcript của chương cụ thể.

5. **Tăng Tốc Độ**:
   - Sử dụng **Apify Batch** để xử lý nhiều video cùng lúc (nếu có API token premium).

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp để tập trung vào **strategy content** thay vì soạn thảo thread thủ công. Với **AI + API miễn phí**, nội dung trở nên **hấp dẫn, tự nhiên**, và **tương tác cao**.

**Hành động ngay!**
1. **Import workflow** và cấu hình theo hướng dẫn.
2. **Test với 1 video** để đảm bảo hoạt động.
3. **Bật Schedule Trigger** để tự động hóa hàng ngày.

👉 **Cần hỗ trợ?** Đăng ký **VPS n8n** từ [TinoHost](https://tino.vn/vps-n8n?affid=388) để workflow chạy **ổn định 24/7**!

---