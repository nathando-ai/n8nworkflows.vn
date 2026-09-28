---
title: "🚀 Tự Động Hóa Nhận Dữ Liệu Reddit + Tóm Tắt AI + Lưu Trữ Google Sheets: Giải Pháp Nghiên Cứu Thị Trường 24/7"
description: "Workflow tự động hóa hoàn toàn không cần code để theo dõi xu hướng trên Reddit bằng công nghệ BrowserAct, tóm tắt nội dung với Gemini AI, và lưu kết quả vào Google Sheets. Giúp các sếp tiết kiệm thời gian nghiên cứu thị trường và cạnh tranh với đối thủ hàng ngày."
slug: "tieu-dong-hoa-reddit-ai-google-sheets"
tags: [n8n, automation, market-research, ai-summarization, browseract, google-sheets, reddit-scraping]
keywords: [tự động hóa nghiên cứu thị trường, scrape Reddit với n8n, tóm tắt AI Gemini, lưu dữ liệu Google Sheets, công cụ tự động hóa không code]
---

# 🚀 **Tự Động Hóa Nhận Dữ Liệu Reddit + Tóm Tắt AI + Lưu Trữ Google Sheets: Giải Pháp Nghiên Cứu Thị Trường 24/7**

## **🔍 Nỗi Đau Của Các Sếp Trong Nghiên Cứu Thị Trường**
Bạn có bao giờ phải:
- **Tốn hàng giờ** để theo dõi xu hướng trên Reddit, tìm kiếm từ khóa liên quan đến ngành nghề?
- **Mất thời gian** đọc hàng chục bài viết dài để rút ra thông tin quan trọng?
- **Không biết đối thủ đang nói gì** trên các subreddit liên quan?
- **Không có hệ thống lưu trữ** để theo dõi sự thay đổi của thị trường theo thời gian?

**Workflow này giải quyết tất cả!** Với công nghệ **BrowserAct** (scrape stealthy không bị chặn), **Gemini AI** (tóm tắt thông minh), và **Google Sheets** (lưu trữ tự động), bạn sẽ có một **báo cáo hàng ngày** về xu hướng, đối thủ cạnh tranh, và ý kiến của cộng đồng – **không cần làm thủ công một lần nào nữa!**

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian**: Không cần theo dõi Reddit thủ công hàng ngày.
✅ **Tóm tắt thông minh**: AI Gemini tổng hợp **top 3 bài viết** thành một báo cáo ngắn gọn.
✅ **Lưu trữ tự động**: Dữ liệu được ghi vào Google Sheets với **ngày tháng, liên kết, và tóm tắt**.
✅ **Theo dõi đối thủ**: Bạn có thể theo dõi **các subreddit của đối thủ** và biết họ đang nói gì.
✅ **Hoạt động 24/7**: Dữ liệu cập nhật **mỗi ngày** khi bạn ngủ.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Google** (để kết nối với Google Sheets và Gemini API).
2. **Tài khoản BrowserAct** (để scrape Reddit mà không bị chặn).
3. **Google Sheet** với **2 tab**:
   - **Tab "Config"**: Cột `keywords` (dành cho từ khóa tìm kiếm) và cột `competitor` (dành cho tên subreddit).
   - **Tab "Report"**: Cột `Date`, `Competitor/Keyword`, `Summary`, `Link` (để lưu kết quả).
4. **API Key Google Gemini** (hoặc sử dụng OpenAI nếu muốn thay thế).

---
### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Bước 1**: Tải workflow từ [n8n.io/workflows/13685](https://n8n.io/workflows/13685) hoặc copy JSON từ trang này.
- **Bước 2**: Mở **n8n Editor**, nhấn **"Import"** và dán JSON vào.
- **Bước 3**: Chọn **"Create Workflow"** để lưu.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này có **2 đường dẫn chính**:
- **Đường dẫn 1**: Theo dõi **từ khóa** (ví dụ: "sản phẩm của bạn").
- **Đường dẫn 2**: Theo dõi **subreddit của đối thủ** (ví dụ: r/oppo, r/xiaomi).

##### **A. Cấu Hình Google Sheets**
- **Node "GSheets: Read Config"**:
  - Chọn **credentials**: `googleApi`.
  - Điền **Sheet ID** và **Range**: `Config!A1` (nếu dữ liệu bắt đầu từ ô A1).
  - **Tab "Report"**: Đảm bảo cột `Date` (ngày tháng), `Competitor/Keyword`, `Summary`, `Link` đã được định nghĩa.

##### **B. Cấu Hình BrowserAct**
- **Node "BrowserAct: Scrape Keywords" & "BrowserAct: Scrape Subreddit"**:
  - Chọn **credentials**: `browserActApi`.
  - Điền **Task ID** từ tài khoản BrowserAct của bạn (để nó biết scrape gì).
  - **Lưu ý**:
    - Nếu không có Task ID, tạo một **task mới** trên BrowserAct với:
      - **URL**: `https://reddit.com/search/?q=<keyword>` (đối với từ khóa).
      - **URL**: `https://reddit.com/r/<subreddit>/` (đối với subreddit).
    - **Selector**: Sử dụng CSS selector để lấy bài viết (ví dụ: `.post` hoặc `.title`).

##### **C. Cấu Hình AI Gemini**
- **Node "Google Gemini Chat Model" & "Google Gemini Chat Model1"**:
  - Chọn **credentials**: `googlePalmApi`.
  - **Prompt mẫu** (đã được định sẵn trong workflow):
    ```json
    "You are a market research analyst. Summarize the top 3 Reddit posts about [KEYWORD] into a single concise bullet-point report. Include key insights, trends, and any negative/positive feedback. Do not exceed 3 sentences per point."
    ```
  - **Lưu ý**:
    - Nếu muốn thay đổi AI model, thay thế `lmChatGoogleGemini` bằng `lmChatOpenAI` và cập nhật credentials.

##### **D. Cấu Hình Schedule Trigger**
- **Node "Schedule Trigger"**:
  - Chọn **lịch trình** (ví dụ: **mỗi ngày lúc 8h sáng**).
  - **Lưu ý**: Đảm bảo workflow được **Active** và **Schedule Trigger** được bật.

##### **E. Cấu Hình Node Code (Clean & Format)**
- **Node "Clean Keyword Data" & "Clean Competitor Data"**:
  - Mở **Code Editor** và kiểm tra logic:
    ```javascript
    // Ví dụ: Lọc ra bài viết mới nhất và loại bỏ dữ liệu thừa
    return $input.all();
    ```
  - **Lưu ý**: Nếu dữ liệu không đúng, chỉnh sửa để phù hợp với cấu trúc Reddit.

- **Node "Format Keyword Digest" & "Format Competitor Digest"**:
  - Chỉnh sửa để đảm bảo **AI nhận được dữ liệu đúng định dạng**:
    ```json
    {
      "posts": [
        { "title": "...", "link": "...", "content": "..." },
        { "title": "...", "link": "...", "content": "..." }
      ]
    }
    ```

##### **F. Cấu Hình Archive (Lưu vào Google Sheets)**
- **Node "Archive Keywords" & "Archive Competitors"**:
  - Chọn **credentials**: `googleApi`.
  - **Range**: `Report!A2:A` (để append dữ liệu mới vào dưới dòng 2).
  - **Lưu ý**: Đảm bảo cột `Date` tự động lấy ngày hiện tại (nếu không, thêm một node **Set** trước khi lưu).

---

#### **3. Kích Hoạt ⚡️**
- **Bước 1**: Nhấn **"Test Run"** để chạy thử với dữ liệu mẫu.
- **Bước 2**: Kiểm tra **Google Sheets** xem có dữ liệu mới được append không.
- **Bước 3**: Nếu thành công, **bật Active** và **bật Schedule Trigger**.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Thêm Slack/Telegram Notification**:
   - Sử dụng **node `n8n-nodes-slack`** hoặc **`n8n-nodes-telegram`** để gửi báo cáo hàng ngày.
   - **Cách làm**:
     - Thêm node **`Set`** sau khi AI tóm tắt.
     - Thêm node **`Slack Webhook`** và cấu hình message:
       ```json
       {
         "text": `📊 Daily Reddit Report: ${summary}`,
         "attachments": [
           {
             "title": "Link",
             "title_link": `${link}`,
             "text": "🔗 Click to view"
           }
         ]
       }
       ```

2. **Lưu Log Dữ Liệu**:
   - Thêm **node `n8n-nodes-base.httpRequest`** để gửi dữ liệu đến **Google Drive** hoặc **AWS S3** làm backup.

3. **Tăng Cường Tính Cá Nhân Hóa**:
   - Sử dụng **node `n8n-nodes-base.if`** để lọc bài viết có từ khóa cụ thể (ví dụ: "giá cả", "sản phẩm mới").
   - **Ví dụ**:
     ```javascript
     // Trong node "If: Is Keyword?"
     return $input.all().some(item => item.content.includes("giá cả"));
     ```

4. **Thay Đổi AI Model**:
   - Nếu muốn sử dụng **OpenAI** thay vì Gemini:
     - Thay thế `lmChatGoogleGemini` bằng `lmChatOpenAI`.
     - Cập nhật **credentials** với API Key OpenAI.

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn:
✔ **Tiết kiệm thời gian** trong nghiên cứu thị trường.
✔ **Hiểu rõ xu hướng** từ Reddit mà không cần đọc hàng chục bài viết.
✔ **Theo dõi đối thủ** một cách tự động hóa.
✔ **Lưu trữ dữ liệu** để so sánh theo thời gian.

**Hành động ngay!**
1. **Import workflow** và cấu hình theo hướng dẫn.
2. **Bật Schedule Trigger** để nhận báo cáo hàng ngày.
3. **Tích hợp Slack/Telegram** để không bỏ lỡ bất kỳ thông tin quan trọng nào!

**🚀 Cùng tự động hóa nghiên cứu thị trường của bạn ngay hôm nay!** 🚀