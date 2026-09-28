---
title: "🚀 Tự Động Hoà AI Tạo Video YouTube Shorts Hàng Ngày Với Groq, VoiceRSS & Pexels - Không Cần Code"
description: "Workflow tự động hóa 100% miễn phí tạo video YouTube Shorts hàng ngày từ tin tức AI, với giọng nói tự động, video stock chất lượng cao và render cloud. Giúp các sếp tiết kiệm 10+ giờ/tháng và xây dựng nội dung liên tục cho kênh."
slug: "tieu-dong-hoa-tao-video-youtube-shorts-ai"
tags: [n8n, automation, youtube-shorts, ai-content, groq, voice-rss, pexels, shotstack]
keywords: [tự động hóa youtube shorts, tạo video ai, groq llama 3, voiceover tự động, pexels video stock, shotstack render cloud, workflow n8n youtube]
---

# 🚀 **Tự Động Hoà AI Tạo Video YouTube Shorts Hàng Ngày - Không Cần Code**

### **Giải pháp cho các sếp muốn:**
- **Tạo video YouTube Shorts hàng ngày** mà không cần quay phim hoặc chỉnh sửa.
- **Tiết kiệm 10+ giờ/tháng** cho việc viết script, ghi âm và edit video.
- **Xây dựng nội dung liên tục** từ tin tức AI mới nhất với giọng nói tự động và video stock chất lượng cao.
- **Tối ưu SEO** cho kênh với nội dung mới mỗi ngày, thu hút người xem tự động.

---

## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn**: Chỉ cần bật workflow, hệ thống sẽ tự lấy tin tức AI, tạo script, ghi âm, render video và upload lên YouTube.
- **Chất lượng chuyên nghiệp**: Video 9:16 MP4 với âm thanh giọng nói tự động (VoiceRSS) và video stock từ Pexels (1080x1920).
- **Tiết kiệm chi phí**: Sử dụng các API miễn phí (Groq, VoiceRSS, Pexels) và sandbox Shotstack (200 render/tháng).
- **Tối ưu SEO**: Nội dung mới mỗi ngày từ tin tức AI, giúp kênh được YouTube ưu tiên hiển thị.
- **Hoạt động 24/7**: Workflow chạy tự động hàng ngày theo lịch trình (cấu hình được).
:::

---

## 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản YouTube** (đã kết nối OAuth2).
2. **API Keys miễn phí**:
   - [Groq API Key](https://console.groq.com/) (dùng model `llama-3.1-8b-instant`).
   - [VoiceRSS API Key](https://voicerss.org/) (dùng giọng nói như `Linda` hoặc `Amy`).
   - [Pexels API Key](https://www.pexels.com/api/) (tìm video portrait cho video Shorts).
   - [Shotstack API Key](https://shotstack.io/) (sandbox miễn phí 200 render/tháng).
3. **Tài khoản n8n** (cài đặt trên VPS hoặc dùng phiên bản cloud miễn phí).
4. **Kênh YouTube** đã kích hoạt tính năng upload video (không bị giới hạn).
:::

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/16201](https://n8n.io/workflows/16201) hoặc copy toàn bộ JSON từ trang này.
- **Mở n8n Editor** và chọn **Import Workflow** → Dán JSON hoặc tải file `.json`.
- **Kích hoạt chế độ "Active"** sau khi import xong.

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflows này gồm **16 node** quan trọng, các sếp cần cấu hình như sau:

#### **🔹 Node "Daily Schedule" (n8n-nodes-base.scheduleTrigger)**
- **Cấu hình lịch trình**:
  - Chọn **Daily** (hàng ngày).
  - Thời gian chạy: **Sáng sớm (6h-8h)** để video được upload khi người xem nhiều nhất.
  - **Lưu ý**: Nếu kênh của các sếp ở khu vực khác (Việt Nam), điều chỉnh giờ theo múi giờ địa phương.

#### **🔹 Node "Groq Chat Model" (n8n-nodes-langchain.lmChatGroq)**
- **Tham số cần thiết**:
  - **API Key**: Điền `YOUR_GROQ_API_KEY` (từ [Groq Console](https://console.groq.com/)).
  - **Model**: Để mặc định là `llama-3.1-8b-instant`.
  - **Prompt tùy chỉnh** (nếu muốn thay đổi giọng điệu):
    ```json
    "prompt": "Tôi là một nhà sản xuất nội dung YouTube Shorts. Viết một script 45 giây về tin tức AI mới nhất với tiêu đề: {headline}. Giọng nói tự nhiên, không có chỉ dẫn sân khấu. Đảm bảo nội dung phù hợp với kênh {channelName} và thu hút người xem trong 3 giây đầu tiên."
    ```
  - **Lưu ý**: Điền `{channelName}` là tên kênh của các sếp (ví dụ: "TechAI Việt Nam").

#### **🔹 Node "VoiceRSS" (n8n-nodes-base.httpRequest)**
- **Tham số cần thiết**:
  - **API Key**: Điền `YOUR_VOICERSS_API_KEY`.
  - **Voice**: Chọn giọng nói phù hợp (ví dụ: `&v=Linda`).
  - **Script**: Auto-trích từ node "Groq Chat Model".
  - **Lưu ý**: Nếu giọng nói không phù hợp, thử các giọng khác như `Amy`, `Emma`, hoặc `Brian`.

#### **🔹 Node "Pexels" (n8n-nodes-base.httpRequest)**
- **Tham số cần thiết**:
  - **API Key**: Điền `YOUR_PEXELS_API_KEY`.
  - **Keyword**: Auto-extract từ tiêu đề tin tức (2 từ đầu).
    - Ví dụ: Nếu tiêu đề là *"Groq ra mắt model Llama 3.1"*, keyword sẽ là `Groq Llama`.
  - **Lọc video**:
    - **Orientation**: `portrait`.
    - **Resolution**: `1920` (1080x1920).
  - **Lưu ý**: Nếu không tìm thấy video phù hợp, chỉnh sửa keyword thủ công trong node **"Parse Script & Keyword"**.

#### **🔹 Node "Shotstack – Start Render" (n8n-nodes-base.httpRequest)**
- **Tham số cần thiết**:
  - **API Key**: Điền `YOUR_SHOTSTACK_API_KEY`.
  - **Input**:
    - **Video URL**: Từ node Pexels.
    - **Audio URL**: Từ node VoiceRSS.
  - **Output**:
    - **Render ID**: Lưu vào node **"Save Render ID"** để theo dõi tiến độ.
  - **Lưu ý**:
    - Nếu video render chậm, tăng thời gian **Wait node** từ 30s → 60s.
    - Kiểm tra sandbox Shotstack có đủ credit (200 render/tháng).

#### **🔹 Node "Upload a video" (n8n-nodes-base.youtube)**
- **Tham số cần thiết**:
  - **Credentials**: Kết nối tài khoản YouTube OAuth2 (cấu hình trong **n8n Credentials**).
  - **Key Parameters**:
    - `operation`: `upload`.
    - `resource`: `video`.
    - **Thông tin video**:
      ```json
      {
        "snippet": {
          "title": "{headline}",
          "description": "Tin tức AI mới nhất được tự động hóa với Groq và VoiceRSS. Đăng ký kênh để theo dõi nội dung mới hàng ngày!",
          "tags": ["AI", "Tin tức", "YouTube Shorts", "Groq", "VoiceRSS"]
        },
        "status": {
          "privacyStatus": "public", // Thay đổi thành "private" nếu muốn review trước
          "categoryId": "28" // Science & Technology
        }
      }
      ```
  - **Lưu ý**:
    - Nếu kênh của các sếp ở Việt Nam, thay `region` thành `VN`.
    - Để `privacyStatus` là `private` nếu muốn kiểm tra video trước khi upload.

---

### **3. Kích hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Chạy workflow một lần với **Manual Trigger** để kiểm tra từng node.
   - Kiểm tra:
     - Script Groq có logic không?
     - VoiceRSS có phát âm rõ không?
     - Video Pexels có phù hợp không?
     - Shotstack có render thành công không?
     - Video YouTube có upload thành công không?
2. **Bật Active** sau khi kiểm tra xong.

---

## ✍️ **Mẹo & gợi ý nâng cao**
:::info[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Tối ưu SEO cho kênh**:
   - Thêm **thẻ hashtag** trong mô tả video (ví dụ: `#AI #Tin tức #YouTubeShorts`).
   - Sử dụng **keyword từ tin tức** trong tiêu đề và mô tả để tăng khả năng xếp hạng.

2. **Lưu log hoạt động**:
   - Thêm node **Sticky Note** hoặc **Google Sheets** để ghi lại:
     - Tiêu đề tin tức.
     - Thời gian upload.
     - Link video.
     - Trạng thái (thành công/thất bại).

3. **Gửi báo cáo định kỳ**:
   - Kết hợp với **Slack/Telegram Bot** để thông báo khi video upload thành công.
   - Ví dụ: *"🚀 Video mới đã upload: [Tên tin tức] - Link: [URL]"*.

4. **Tùy chỉnh giọng nói**:
   - Thử các giọng VoiceRSS khác (ví dụ: `Joey` hoặc `Matthew`) để phù hợp với âm thanh kênh.

5. **Xử lý lỗi tự động**:
   - Thêm node **Set** sau node **Shotstack – Get Render URL** để kiểm tra:
     - Nếu render thất bại, gửi thông báo lỗi qua Slack/Email.
     - Thay đổi keyword Pexels hoặc script Groq.

6. **Tăng tương tác**:
   - Thêm **câu hỏi trong mô tả** để khuyến khích người xem comment (ví dụ: *"Bạn nghĩ tin tức này sẽ ảnh hưởng như thế nào đến ngành AI?"*).
   - Sử dụng **các template script** khác nhau cho từng loại tin tức (ví dụ: tin tức công nghệ vs. tin tức nghiên cứu).
:::

---

## 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn xây dựng kênh YouTube Shorts chuyên về tin tức AI **mà không cần code**. Với **tự động hóa hoàn toàn**, các sếp sẽ tiết kiệm thời gian, tạo nội dung liên tục và thu hút người xem tự động.

### **Hành động ngay hôm nay:**
1. **Đăng ký VPS** để chạy n8n 24/7 (không bị giới hạn như phiên bản cloud).
   👉 [VPS TinoHost (Mã giảm giá: **VPSN8N**)](https://tino.vn/vps-n8n?affid=388)
   👉 [VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)

2. **Import workflow** và cấu hình API keys theo hướng dẫn trên.

3. **Bật Active** và theo dõi kênh của mình **nở rộ** với nội dung AI mới mỗi ngày!

---
**💡 Chia sẻ workflow này với đồng nghiệp nếu bạn thấy hữu ích!** 🚀