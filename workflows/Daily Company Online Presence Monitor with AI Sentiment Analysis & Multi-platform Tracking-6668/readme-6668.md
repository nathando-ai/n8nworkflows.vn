---
title: "🌐 **Tự Động Hóa Theo Dõi Xã Hội Mạng & Phân Tích Sentiment AI Cho Doanh Nghiệp Hàng Ngày - Không Cần Code!**"
description: "Workflow này tự động thu thập, phân tích và báo cáo tình hình xuất hiện của doanh nghiệp trên Google News, Reddit, YouTube hàng ngày với AI sentiment analysis. Giúp các sếp tiết kiệm 10+ giờ/tháng và đưa ra quyết định dựa trên dữ liệu chính xác."
slug: "tieu-dong-ho-tra-tracking-online-presence-ai-sentiment"
tags: [n8n, automation, market-research, ai-sentiment-analysis, no-code, google-news, reddit, youtube]
keywords: [tự động hóa theo dõi doanh nghiệp, phân tích sentiment AI, n8n workflow, thu thập tin tức tự động, báo cáo hàng ngày, tracking online presence]
---

# 🚀 **Tự Động Hóa Theo Dõi Xã Hội Mạng & Phân Tích Sentiment AI Cho Doanh Nghiệp Hàng Ngày**

### **Giải pháp hoàn hảo cho các sếp muốn:**
✅ **Biết ngay** doanh nghiệp của mình được nhắc đến như thế nào trên mạng hàng ngày
✅ **Hiểu rõ** cảm xúc (sentiment) của người dùng từ các bài viết, video, và bài đăng
✅ **Tiết kiệm 10+ giờ/tháng** thay vì phải tra cứu thủ công
✅ **Nhận báo cáo tự động** qua email với tóm tắt và phân tích chi tiết

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động **24/7** và không bị gián đoạn, các sếp nên **self-host** n8n trên VPS. Dưới đây là 2 lựa chọn uy tín với **mã giảm giá độc quyền** dành cho bạn:

👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (Đảm bảo tốc độ cao, ổn định)

*Lưu ý:* N8n **không** chạy được trên máy chủ shared hosting (như Hostinger, Bluehost) vì yêu cầu tài nguyên thấp nhưng cần **IP cố định** và **SSL**.
:::

---

## 🎯 **Kết quả các sếp nhận được**
Workflow này **tự động hóa toàn bộ quy trình** theo dõi và phân tích online presence của doanh nghiệp, giúp các sếp:
1. **Thu thập dữ liệu** từ **Google News, Reddit, và YouTube** hàng ngày (lúc 9h sáng).
2. **Phân tích sentiment** (tích cực, trung lập, tiêu cực) và **tóm tắt nội dung** bằng AI (GPT-3.5).
3. **Lọc bỏ trùng lặp** và **lưu lịch sử** trong cơ sở dữ liệu SQLite.
4. **Gửi báo cáo tự động** qua email với **các điểm nổi bật** và **phân tích chi tiết**.

:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian:** Không cần tra cứu thủ công trên Google, Reddit, YouTube.
- **Dữ liệu chính xác:** AI phân tích sentiment với độ chính xác cao.
- **Hoạt động liên tục:** Workflow chạy tự động hàng ngày, không cần can thiệp.
- **Báo cáo cá nhân hóa:** Nhận email tổng hợp với các thông tin quan trọng.
- **Lưu trữ dài hạn:** Dữ liệu được lưu trong SQLite, có thể truy xuất lại sau này.
:::

---

## 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
✔ **Tài khoản Google** (để sử dụng **Google News RSS** và **YouTube API**).
✔ **Tài khoản Reddit** (để lấy **OAuth2 API Key**).
✔ **Tài khoản OpenAI** (để phân tích **sentiment và tóm tắt** bằng AI).
✔ **Tài khoản Gmail** (để **gửi báo cáo tự động**).
✔ **VPS** (để self-host n8n, như đã gợi ý ở trên).

:::info[CHUẨN BỊ CREDENTIALS]
Các sếp cần **cấu hình các credentials** sau trong n8n:
- **redditOAuth2Api** (tạo từ [Reddit Developer Portal](https://www.reddit.com/prefs/apps)).
- **googleApi** (tạo từ [Google Cloud Console](https://console.cloud.google.com/)).
- **openAiApi** (tạo từ [OpenAI API Keys](https://platform.openai.com/account/api-keys)).
- **gmailApi** (tạo từ [Google Workspace API](https://developers.google.com/gmail/api/quickstart/python)).
:::

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
#### **Cách 1: Import từ file JSON**
1. **Tải workflow** từ [n8n.io/workflows/6668](https://n8n.io/workflows/6668).
2. **Đăng nhập** vào n8n Editor (self-hosted hoặc n8n.cloud).
3. Nhấn **Import** → Chọn file JSON vừa tải → **Import**.

#### **Cách 2: Copy/Paste JSON**
1. **Tải JSON** từ link trên.
2. Trong n8n Editor, nhấn **Import** → Chọn **Paste JSON** → Dán nội dung file → **Import**.

---

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**

#### **🔹 Node 1: "Daily Morning Trigger (9 AM)"**
- **Không cần chỉnh sửa**, workflow sẽ chạy tự động lúc 9h sáng hàng ngày.

#### **🔹 Node 2: "Set Company Details"**
- **Cấu hình tên công ty** và **keyword** để theo dõi.
  - Ví dụ:
    ```json
    {
      "companyName": "Công Ty ABC",
      "keywords": ["ABC", "sản phẩm ABC", "dịch vụ ABC"]
    }
    ```
- **Lưu ý:** Nếu không cấu hình, workflow sẽ không biết theo dõi công ty nào.

#### **🔹 Node 3: "Fetch Google News RSS"**
- **Không cần chỉnh sửa**, node này tự động lấy tin tức từ Google News dựa trên keyword.

#### **🔹 Node 5: "Search Reddit Posts"**
- **Sử dụng credentials `redditOAuth2Api`** đã tạo trước đó.
- **Không cần chỉnh sửa** các tham số mặc định (operation: search, resource: post).

#### **🔹 Node 7: "Search YouTube Videos"**
- **Sử dụng credentials `googleApi`** (API Key từ Google Cloud Console).
- **Không cần chỉnh sửa** các tham số mặc định (operation: list, resource: video).

#### **🔹 Node 11: "AI: Analyze Sentiment & Summarize"**
- **Sử dụng credentials `openAiApi`**.
- **Không cần chỉnh sửa model** (sử dụng `gpt-3.5-turbo` mặc định).
- **Lưu ý:** Nếu budget OpenAI không đủ, workflow có thể bị ngắt.

#### **🔹 Node 15: "Send Report Email"**
- **Sử dụng credentials `gmailApi`**.
- **Chỉnh sửa địa chỉ email nhận** trong node này:
  ```json
  {
    "to": "email-cua-ban@gmail.com",
    "subject": "Báo cáo Online Presence Hôm Nay"
  }
  ```

---

### **3. Kích hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Nhấn **Run Workflow** và kiểm tra các node có hoạt động không.
   - Nếu có lỗi, kiểm tra **credentials** và **cấu hình** của các node.
2. **Bật Active**:
   - Sau khi test thành công, nhấn **Active** để workflow chạy tự động hàng ngày.

---

## ✍️ **Mẹo & gợi ý nâng cao**

### **🔹 Kết hợp với Slack/Telegram**
- **Thêm node Slack/Telegram** để thông báo tức thời khi có tin tức mới.
- **Cách làm:**
  1. Thêm node **Slack Webhook** hoặc **Telegram Bot**.
  2. Chỉnh sửa node **"Format Report Email"** để gửi thông báo ngay khi có tin tức mới.

### **🔹 Lưu log vào Google Sheets/Notion**
- **Thêm node Google Sheets** để lưu tất cả dữ liệu theo dõi.
- **Cách làm:**
  1. Thêm node **Google Sheets** sau node **"SQLite: Record Processed Mentions"**.
  2. Cấu hình sheet và range muốn lưu.

### **🔹 Phân tích theo thời gian**
- **Tạo báo cáo tuần/tháng** bằng cách:
  - Thêm node **Cron** chạy hàng tuần/tháng.
  - Thêm node **Google Sheets** để tổng hợp dữ liệu.

### **🔹 Cải thiện prompt AI**
- Nếu muốn **tóm tắt chi tiết hơn**, chỉnh sửa node **"AI: Analyze Sentiment & Summarize"**:
  ```json
  {
    "prompt": "Tóm tắt bài viết này về công ty ABC trong 3 câu, phân tích sentiment (tích cực/tiêu cực/trung lập) và nêu ra điểm mạnh/điểm yếu của sản phẩm/dịch vụ."
  }
  ```

---

## 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** để các sếp **tự động hóa theo dõi online presence** và **phân tích sentiment** hàng ngày **không cần code**. Bằng cách **self-host n8n trên VPS** và cấu hình các credentials, các sếp sẽ **tiết kiệm thời gian, nhận dữ liệu chính xác và đưa ra quyết định thông minh**.

**🚀 Hãy áp dụng ngay hôm nay!**
1. **Self-host n8n** trên VPS (dùng mã giảm giá **VPSN8N**).
2. **Import workflow** và cấu hình credentials.
3. **Bật Active** và **nhận báo cáo tự động** hàng ngày!

*Có thắc mắc? Để lại comment dưới đây, tôi sẽ hỗ trợ!* 😊