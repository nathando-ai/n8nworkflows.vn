---
title: "🚀 Tự Động Hóa Quảng Bài YouTube Trên Reddit Với Bình Luận AI + Báo Cáo Email Tự Động - N8N"
description: "Workflow tự động hóa 100% không code giúp các sếp quảng bá video YouTube trên Reddit bằng bình luận AI tự động hóa, đồng thời gửi báo cáo email định kỳ. Tiết kiệm thời gian lên đến 80% so với cách làm thủ công."
slug: "tieu-dong-hoa-quang-bai-youtube-tren-reddit-voi-ai"
tags: [n8n, automation, marketing, ai, seo, youtube, reddit, email-automation, no-code]
keywords: [n8n workflow youtube reddit, tự động hóa quảng bá video, bình luận ai trên reddit, báo cáo email tự động, seo với n8n, tự động hóa marketing ai]
---

# 🚀 **Tự Động Hóa Quảng Bài YouTube Trên Reddit Với Bình Luận AI + Báo Cáo Email Tự Động**

### **Giải pháp hoàn hảo cho các sếp muốn quảng bá video YouTube trên Reddit mà không cần viết bình luận thủ công!**
Hiện nay, việc quảng bá video YouTube trên Reddit là một trong những chiến lược **SEO và marketing hiệu quả nhất**, nhưng lại tốn rất nhiều thời gian khi phải viết bình luận một cách thủ công. Workflow này sẽ **tự động hóa toàn bộ quy trình** bằng công nghệ AI, bao gồm:
- **Tạo bình luận AI tự nhiên** cho video trên Reddit.
- **Lọc và loại bỏ bình luận trùng lặp** để tránh bị Reddit flag.
- **Gửi báo cáo email định kỳ** với kết quả hoạt động.
- **Tích hợp Google Sheets** để theo dõi và quản lý dữ liệu.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động **24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên một VPS ổn định.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới **39%**)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian lên đến 80%** so với cách làm thủ công.
✅ **Bình luận AI tự nhiên**, không bị phát hiện là spam.
✅ **Lọc bỏ trùng lặp**, tránh bị Reddit cấm tài khoản.
✅ **Báo cáo email tự động** với thống kê chi tiết.
✅ **Tích hợp Google Sheets** để theo dõi hiệu suất.
✅ **Hoạt động liên tục 24/7**, không cần can thiệp thủ công.
:::

---

## 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
✔ **Tài khoản Reddit** (API Key và OAuth2 credentials).
✔ **Tài khoản YouTube** (API Key để lấy video).
✔ **Tài khoản Gmail** (để gửi báo cáo email).
✔ **Google Sheets** (để lưu trữ dữ liệu bình luận và báo cáo).
✔ **API Key OpenRouter** (hoặc mô hình AI khác hỗ trợ `lmChatOpenRouter`).
✔ **Tài khoản n8n** (cài đặt self-hosted hoặc dùng phiên bản cloud).

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
Các sếp có thể **import từ file JSON** hoặc **copy/paste JSON** vào **n8n Editor**:
1. Tải file JSON từ [link gốc](https://n8n.io/workflows/4433).
2. Mở **n8n Editor** → **Import Workflow** → Chọn file JSON.
3. Hoặc **copy toàn bộ JSON** và dán vào **Import Workflow** trong n8n.

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**

#### **A. Cấu hình Reddit Node**
- **Node: "Reddit"**
  - **Credentials**: Thiết lập **OAuth2** từ Reddit API.
  - **Subreddit**: Chọn subreddit mục tiêu (ví dụ: `seo`, `marketing`, `ai`).
  - **API Key**: Điền vào **Client ID** và **Client Secret**.

#### **B. Cấu hình YouTube Node**
- **Node: "YouTube"**
  - **API Key**: Điền **API Key YouTube** từ [Google Cloud Console](https://console.cloud.google.com/).
  - **Channel ID**: Chọn kênh YouTube cần quảng bá.

#### **C. Cấu hình AI (OpenRouter)**
- **Node: "AI Brain" (lmChatOpenRouter) & "Brain", "Brain1"**
  - **API Key**: Điền **API Key OpenRouter** (hoặc mô hình AI khác hỗ trợ).
  - **Prompt Template**: Các sếp có thể **tùy chỉnh prompt** để AI tạo bình luận phù hợp với nội dung video.
  - **Dữ liệu đầu vào**: Đảm bảo **tên video, mô tả, và link** được truyền vào AI.

#### **D. Cấu hình Gmail Node**
- **Node: "Send to your email"**
  - **Credentials**: Thiết lập **OAuth2** từ Gmail.
  - **Email Template**: Sử dụng **HTML template** trong node **"Generate Email HTML"** để tạo báo cáo chuyên nghiệp.

#### **E. Cấu hình Google Sheets**
- **Node: "Append Data" & "Store Humanized Comment"**
  - **Credentials**: Thiết lập **OAuth2** từ Google Sheets.
  - **Sheet Name**: Chọn **tên sheet** để lưu trữ dữ liệu.
  - **Range**: Điền **A1** (hoặc tùy chỉnh) để ghi dữ liệu.

#### **F. Cấu hình Filter & Remove Duplicates**
- **Node: "Filter Posts by Criteria" (If)**
  - **Điều kiện lọc**: Các sếp có thể **tùy chỉnh** để lọc video mới nhất hoặc video có engagement cao.
- **Node: "Remove Duplicates"**
  - **Field**: Chọn **trường duy nhất** (ví dụ: `videoId`) để loại bỏ trùng lặp.

#### **G. Cấu hình Agent AI (Social Post Comment)**
- **Node: "Social Post Comment" (Agent)**
  - **Prompt**: Tùy chỉnh **câu hỏi AI** để tạo bình luận phù hợp với từng video.
  - **Output Parser**: Đảm bảo **Structured Output** được cấu hình đúng để AI trả về bình luận có cấu trúc.

#### **H. Cấu hình Wait & Batch Processing**
- **Node: "Wait 5 sec"**
  - **Thời gian chờ**: Để tránh bị Reddit detect bot, **cài đặt 5 giây** giữa các bình luận.
- **Node: "Loop Over Items" (Split In Batches)**
  - **Batch Size**: Đặt **10-20 video/lần** để tránh quá tải.

---

### **3. Kích hoạt ⚡️**
1. **Test Run** với **dữ liệu mẫu** (ví dụ: 1-2 video YouTube).
2. **Kiểm tra email** để xác nhận báo cáo được gửi đúng.
3. **Bật Active** workflow và **monitor** trong **n8n Dashboard**.

---

## ✍️ **Mẹo & gợi ý nâng cao**
### **1. Tùy chỉnh AI để tạo bình luận chuyên nghiệp hơn**
- **Sử dụng prompt nâng cao** để AI tạo bình luận **cá nhân hóa** hơn:
  ```plaintext
  "Tôi là một người dùng YouTube chuyên về [chủ đề]. Viết một bình luận tự nhiên, có giá trị và không spam cho video này:
  - Video: [Tên Video]
  - Link: [Link Video]
  - Mô tả: [Mô tả video]
  - Yêu cầu: Bình luận phải dài 3-5 câu, có cảm xúc tích cực và đề cập đến 1-2 điểm mạnh của video."
  ```

### **2. Tích hợp Slack/Telegram để báo cáo thực thời**
- **Thêm node Slack/Telegram** sau **"Send to your email"** để **báo cáo ngay khi workflow chạy**.
- **Cấu hình webhook** từ Slack/Telegram và gửi thông báo khi có bình luận mới.

### **3. Lưu log hoạt động vào Google Sheets**
- **Thêm node "Sticky Note"** để lưu **log error** và **thông tin debug**.
- **Tích hợp với Google Sheets** để theo dõi **tất cả hoạt động** của workflow.

### **4. Chạy workflow định kỳ với n8n Cloud Scheduler**
- Nếu dùng **n8n Cloud**, các sếp có thể **cài đặt lịch chạy** (ví dụ: **mỗi ngày 8h sáng**) để tự động quảng bá video mới nhất.

### **5. Tăng hiệu suất với API Key miễn phí (nếu cần)**
- Nếu **API Key OpenRouter** quá đắt, các sếp có thể thử **mô hình AI miễn phí** như:
  - **Replicate** (AI Studio)
  - **Hugging Face Inference API**
  - **Google Vertex AI**

---

## 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp để tập trung vào **strategy marketing** thay vì làm việc thủ công. Với **AI tự động tạo bình luận**, **lọc trùng lặp**, và **báo cáo email tự động**, việc quảng bá video YouTube trên Reddit trở nên **dễ dàng và hiệu quả hơn bao giờ hết**.

🚀 **Hãy import workflow ngay hôm nay và bắt đầu tự động hóa marketing của mình!**
👉 [Tải workflow từ n8n.io](https://n8n.io/workflows/4433)

---
**Cần hỗ trợ?** Đăng ký **VPS n8n** từ [TinoHost](https://tino.vn/vps-n8n?affid=388) và liên hệ **support** để được hướng dẫn chi tiết! 💡