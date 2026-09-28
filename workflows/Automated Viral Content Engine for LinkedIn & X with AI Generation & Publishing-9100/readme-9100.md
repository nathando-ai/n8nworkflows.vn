---
title: "🚀 **N8N Social Media Spark: Máy Tự Động Hóa Nội Dung Viral cho LinkedIn & X (Twitter) với AI Tự Động Sáng Tạo & Đăng Bài**"
description: "Workflow tự động hóa 100% không code giúp các sếp tự động phát hiện nội dung viral trong ngành, tạo bài viết LinkedIn/X chuyên nghiệp, sinh ảnh minh họa, và đăng bài tự động hàng ngày. Giúp tiết kiệm 20+ giờ/tuần cho công việc content marketing."
slug: "n8n-social-media-spark-ai-content-generation"
tags: [n8n, automation, content-marketing, ai-generative, linkedin-x-automation, google-sheets, telegram-bot]
keywords: [n8n workflow tự động hóa content, tạo bài viết LinkedIn với AI, đăng bài tự động X/Twitter, tự động hóa marketing xã hội, AI sinh ảnh cho bài viết, n8n + LangChain]
---

# 🚀 **N8N Social Media Spark: Hệ Thống Tự Động Hóa Nội Dung Viral Cho LinkedIn & X (Twitter)**

## **Giới Thiệu**
Các sếp đã từng phải mất **giờ đồng hồ** mỗi ngày để:
- Tìm kiếm nội dung viral trong ngành?
- Sáng tạo bài viết LinkedIn/X chuyên nghiệp?
- Tạo hình ảnh minh họa phù hợp?
- Đăng bài thủ công hàng ngày?

**Workflow này giải quyết tất cả!** Với **115 node** và tích hợp AI tiên tiến (Gemini, Deepseek, LangChain), **Social Media Spark** tự động:
✅ **Phát hiện** nội dung viral từ LinkedIn của đối thủ hàng tuần
✅ **Sáng tạo** bài viết LinkedIn/X với giọng điệu cá nhân hóa
✅ **Sinh ảnh** phù hợp với nội dung bài viết
✅ **Đăng bài tự động** vào thời điểm tối ưu
✅ **Gửi báo cáo** và thông báo qua Telegram

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 20+ giờ/tuần** cho công việc content marketing.
- **Nội dung viral tự động** từ đối thủ hàng tuần.
- **Bài viết LinkedIn/X chuyên nghiệp** với giọng điệu cá nhân hóa.
- **Ảnh minh họa AI** phù hợp với từng bài viết.
- **Đăng bài tự động** vào thời điểm tối ưu (LinkedIn 6h chiều, X 6h30 chiều).
- **Báo cáo và thông báo** qua Telegram cho quản lý dễ dàng.
- **Hệ thống mở rộng** dễ dàng cho Instagram, TikTok, hoặc các nền tảng khác.
:::

---

## 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi chạy workflow, các sếp cần chuẩn bị:
### **1. API Keys & Credentials**
| Dịch vụ               | Loại Credential          | Ghi chú                                                                 |
|-----------------------|--------------------------|--------------------------------------------------------------------------|
| **Google Sheets**     | OAuth 2.0                | [Tạo credential](https://developers.google.com/sheets/api/quickstart/js) |
| **Google Drive**      | OAuth 2.0                | Cho phép lưu ảnh sinh ra từ AI.                                         |
| **Google Gemini**     | API Key (Google Palm)    | [Cài đặt API](https://makersuite.google.com/)                           |
| **OpenRouter**        | API Key                  | [Đăng ký](https://openrouter.ai/) (dùng cho Deepseek)                   |
| **LinkedIn API**      | OAuth 2.0                | [Hướng dẫn](https://developer.linkedin.com/)                            |
| **X (Twitter) API**   | OAuth 1.0a & OAuth 2.0    | [Hướng dẫn OAuth 1.0a](https://developer.twitter.com/en/docs/authentication/oauth-1-0a) |
| **Telegram Bot**      | Bot Token + Chat ID      | [Tạo bot](https://core.telegram.org/bots/api)                          |
| **Apify/Browseract**  | API Key                  | [Browseract](https://browseract.com/) (miễn phí)                        |

### **2. Google Sheets Template**
- [Tải template](https://docs.google.com/spreadsheets/d/14yeNCC9M7SHN0XG8hgXxCSh9rDkzg_ywIlu_GcZgUu8/edit?usp=sharing)
  - **Bảng "Competitors"**: Lưu danh sách đối thủ.
  - **Bảng "Viral Ideas"**: Lưu ý tưởng viral đã phát hiện.
  - **Bảng "Content Gen (LinkedIn)"**: Lưu bài viết đã tạo.
  - **Bảng "Other handles"**: Lưu bài viết cho X.

### **3. Google Drive**
- Tạo một folder để lưu ảnh sinh ra từ AI.

### **4. Telegram Bot**
- Tạo bot Telegram và lấy **Chat ID** của mình (dùng để nhận thông báo).
- **Cách lấy Chat ID**:
  ```bash
  https://api.telegram.org/bot<BOT_TOKEN>/getUpdates
  ```
  (Thay `<BOT_TOKEN>` bằng token bot của bạn).

---
## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Tải file JSON từ [đây](https://n8n.io/workflows/9100).
2. Trong n8n Editor, nhấn **Import** → Chọn file JSON.
3. Hoặc copy toàn bộ JSON và dán vào **Import Workflow** trong Editor.

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này được chia thành **5 hệ thống** (System 1-5). Dưới đây là hướng dẫn chi tiết cho từng phần quan trọng:

---

#### **🔹 System 1: Scrape Competitor Profiles (Tìm kiếm đối thủ)**
- **Node quan trọng**:
  - **Find competitors** (HTTP Request): Cấu hình URL API của Apify/Browseract để scrape LinkedIn.
  - **Add competitors** (Google Sheets): Điền **Sheet Name = "Competitors"** và cấu hình cột cần append.
- **Lưu ý**:
  - Thay đổi **keywords** trong node **Find competitors** để phù hợp với ngành của các sếp.
  - Ví dụ: `"AI, Automation, No-Code, SaaS, Productivity"`.

---

#### **🔹 System 2: Content Discovery (Phát hiện nội dung viral)**
- **Node quan trọng**:
  - **Scrape viral posts** (HTTP Request): Cấu hình URL API để scrape bài viết từ đối thủ.
  - **Text Classifier** (LangChain): **BẮT BUỘC** chỉnh **system prompt** để phù hợp với ngành.
    - Ví dụ:
      ```json
      "prompt": "Classify the following LinkedIn post as either 'EvergreenAI' (if it's about AI, Automation, or No-Code) or 'Personal/Other'. Return only the category."
      ```
  - **Gemini flash** (Google Gemini): Đảm bảo **API Key** đã được cấu hình trong credentials.
- **Lưu ý**:
  - **Filter >100 likes**: Chỉ giữ bài viết có >100 like để đảm bảo chất lượng.
  - **Remove Duplicates**: Loại bỏ trùng lặp để tránh nội dung giống nhau.

---

#### **🔹 System 3: Generate LinkedIn Posts (Sáng tạo bài viết LinkedIn)**
- **Node quan trọng**:
  - **Post repurpose** (LangChain Agent): **BẮT BUỘC** chỉnh **system prompt** để phù hợp với giọng điệu cá nhân.
    - Ví dụ:
      ```json
      "prompt": "Rewrite this viral LinkedIn post in a professional yet engaging tone for [Tên Công Ty]. Keep it under 1000 characters. Also, generate a unique image description that matches the content."
      ```
  - **Gemini Image Generation**: Nếu muốn sử dụng **OpenAI DALL·E**, thay thế node này bằng **OpenAI Image** (HTTP Request).
  - **Save Post** (Google Sheets): Điền **Sheet Name = "Content Gen (LinkedIn)"**.
- **Lưu ý**:
  - **Reference Image (Minimalistic)**: Tải một ảnh tham khảo lên Google Drive và cấu hình trong node **Minimalistic**.
  - **ScheduleTrigger**: Đặt lịch chạy vào **Chủ nhật 1h sáng** để tránh ảnh hưởng đến hoạt động hàng ngày.

---

#### **🔹 System 4: Repurpose for X (Chuyển đổi bài viết LinkedIn sang X)**
- **Node quan trọng**:
  - **Content repurpose** (LangChain Chain): Chỉnh **system prompt** để phù hợp với định dạng tweet (<280 ký tự).
    - Ví dụ:
      ```json
      "prompt": "Convert this LinkedIn post into a concise, engaging tweet under 280 characters. Keep the key message intact."
      ```
  - **Create Tweet** (Twitter): Đảm bảo **OAuth 1.0a** và **OAuth 2.0** đã được cấu hình.
- **Lưu ý**:
  - **Image valid?** (IF Node): Kiểm tra xem ảnh có tồn tại trước khi đăng.
  - **ScheduleTrigger**: Đặt lịch chạy vào **Chủ nhật 7h sáng**.

---

#### **🔹 System 5: Auto-Post to LinkedIn & X (Đăng bài tự động)**
- **Node quan trọng**:
  - **Create a post** (LinkedIn): Đảm bảo **OAuth 2.0** đã được cấu hình.
  - **Create Tweet** (Twitter): Đảm bảo **OAuth 1.0a** và **OAuth 2.0** đã được cấu hình.
  - **Upload image to X** (HTTP Request): Cấu hình URL API của Twitter để upload ảnh.
- **Lưu ý**:
  - **ScheduleTrigger**:
    - **LinkedIn**: 6h chiều.
    - **X**: 6h30 chiều.
  - **Notify user** (Telegram): Thông báo khi bài viết đã đăng thành công.

---

#### **🔹 System 6: Telegram Helper (Triggers on-demand)**
- **Node quan trọng**:
  - **Telegram Trigger**: Điền **Chat ID** của mình vào node này.
  - **Switch**: Cấu hình các lệnh như `/sms.linkedin`, `/sms.x`, `/sms.scrape`.
  - **Browseract/Perplexity Research**: Nếu muốn sử dụng **Perplexity**, kích hoạt node này và cấu hình API Key.
- **Lưu ý**:
  - **Configure Me!**: Điền **Task ID** của agent Browseract vào node **Perplexity Research**.

---

### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Chạy **Manual Trigger** để kiểm tra workflow.
   - Kiểm tra **Google Sheets** và **Telegram** để xác nhận dữ liệu đã được lưu và thông báo.
2. **Bật Active**:
   - Sau khi kiểm tra xong, bật **Active** cho tất cả các **ScheduleTrigger**.

---

## ✍️ **Mẹo & gợi ý nâng cao**
:::tip[CÁCH LÀM NÂNG CAO]
1. **Tích hợp với Buffer/Hootsuite**:
   - Thay thế node **Create a post** và **Create Tweet** bằng API của Buffer để quản lý nhiều nền tảng.

2. **A/B Testing Prompts**:
   - Tạo **2-3 phiên bản khác nhau** của system prompt trong **LangChain Agent** và so sánh kết quả.

3. **Analytics & Logging**:
   - Thêm node **Google Analytics** hoặc **Google Sheets** để theo dõi engagement (like, comment, share).

4. **Sinh ảnh từ DALL·E**:
   - Thay thế node **Gemini Image Generation** bằng **OpenAI Image** (HTTP Request) nếu muốn sử dụng DALL·E.

5. **Tự động đáp ứng bình luận**:
   - Thêm node **Twitter/LinkedIn Comments** để tự động trả lời bình luận với câu trả lời AI.

6. **Báo cáo tuần/Tháng**:
   - Tạo một **Google Sheet** mới để lưu trữ báo cáo thống kê (bài viết đã đăng, engagement, traffic).

7. **Tích hợp với Notion**:
   - Lưu bài viết và ý tưởng vào **Notion** thay vì Google Sheets.

8. **Sử dụng nhiều mô hình AI**:
   - Thay đổi mô hình trong **Deepseek** hoặc **Gemini** để tối ưu chi phí và chất lượng.
:::

---

## 📌 **Kết luận**
**Social Media Spark** là **hệ thống tự động hóa nội dung hoàn chỉnh** cho LinkedIn và X, giúp các sếp:
✔ **Tiết kiệm thời gian** cho công việc content marketing.
✔ **Tăng cường engagement** với nội dung viral tự động.
✔ **Đăng bài tự động** vào thời điểm tối ưu.
✔ **Cá nhân hóa giọng điệu** với AI.

**Bắt đầu ngay hôm nay!**
1. **Import workflow** và cấu hình credentials.
2. **Chỉnh system prompt** để phù hợp với ngành và giọng điệu cá nhân.
3. **Bật tự động hóa** và theo dõi kết quả!

---
**💬 Có thắc mắc?** Hãy để lại comment bên dưới hoặc liên hệ với tác giả **Diptamoy Barman** qua [LinkedIn](https://www.linkedin.com/in/diptamoy/) để được hỗ trợ chi tiết! 🚀