---
title: "🎙️ Tự Động Chuyển Bài Tiểu Đề Tin Tức Sang Tin Tức Audio Nhờ AI (Claude, GPT-4 & TTS OpenAI) - Không Cần Code!"
description: "Workflow tự động hóa hoàn chỉnh chuyển đổi tiêu đề tin tức hàng ngày thành tin tức audio cá nhân hóa, gửi qua email hàng ngày - tiết kiệm 10+ giờ công sức cho các sếp Content & Marketing mỗi tuần."
slug: "tuy-dong-chuyen-tieu-de-tin-tuc-sang-tin-tuc-audio"
tags: [n8n, automation, content-creation, ai-multimodal, email-automation, no-code]
keywords: [n8n workflow tin tức audio, tự động hóa tin tức hàng ngày, AI tạo tin tức audio, Claude 3.7 + GPT-4, OpenAI TTS, tự động hóa marketing]
---

# 🚀 **Tự Động Chuyển Bài Tiểu Đề Tin Tức Sang Tin Tức Audio Nhờ AI (Claude, GPT-4 & TTS OpenAI)**

### **🔥 Giải pháp cho các sếp Content & Marketing:**
Bạn đã bao giờ mệt mỏi vì phải:
- **Tìm kiếm** và **lọc** tin tức hàng ngày từ hàng trăm nguồn?
- **Viết** và **chỉnh sửa** tin tức thành định dạng email?
- **Tạo** và **chỉnh sửa** âm thanh cho tin tức audio?
- **Gửi** tin tức đến khách hàng hàng ngày mà không có sự hỗ trợ của AI?

**Workflow này tự động hóa toàn bộ quy trình trong 1 giờ/ngày** - chỉ cần **cài đặt 1 lần**, nó sẽ hoạt động **24/7** cho bạn!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ công sức** mỗi tuần: Không cần viết, chỉnh sửa hoặc gửi tin tức thủ công.
- **Tin tức cá nhân hóa**: AI Claude và GPT-4 tự động chuyển đổi tin tức thành định dạng dễ đọc và thu hút.
- **Audio chất lượng cao**: OpenAI TTS tạo ra giọng nói tự nhiên, chuyên nghiệp.
- **Gửi tự động hàng ngày**: Email với tin tức audio được gửi đến khách hàng **mỗi sáng** (hoặc thời gian bạn chọn).
- **Hoạt động liên tục**: Không cần can thiệp thủ công, workflow chạy tự động theo lịch.
:::

---

## 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản NewsAPI** (miễn phí hoặc trả phí):
   - [Đăng ký NewsAPI](https://newsapi.org/) và lấy **API Key**.
   - Mục tiêu: Lấy tin tức từ các nguồn tin tức lớn như BBC, Reuters, CNN...
2. **Tài khoản OpenRouter** (để sử dụng Claude 3.7):
   - [Đăng ký OpenRouter](https://openrouter.ai/) và lấy **API Key**.
   - **Model**: `anthropic/claude-3.7-sonnet` (được sử dụng trong workflow).
3. **Tài khoản OpenAI** (để sử dụng GPT-4 và TTS):
   - [Đăng ký OpenAI](https://platform.openai.com/) và lấy **API Key**.
   - **Model**: `gpt-4o` (để tạo script) và **TTS** (để chuyển văn bản thành âm thanh).
4. **Tài khoản Gmail** (để gửi email tự động):
   - **OAuth 2.0** (cần thiết để n8n gửi email thay mặt bạn).
   - Hướng dẫn [cài đặt OAuth 2.0 cho Gmail](https://developers.google.com/gmail/api/quickstart/python).
5. **Email của khách hàng** (để nhận tin tức audio hàng ngày).
6. **Thời gian chạy** (cấu hình trong **Schedule Trigger**).
:::

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
Các sếp có thể **import** workflow từ file JSON hoặc **copy/paste** JSON vào **n8n Editor**:
- **Tải file JSON** từ [n8n.io/workflows/8121](https://n8n.io/workflows/8121).
- **Mở n8n Editor** → **Import Workflow** → **Chọn file JSON** → **Import**.

:::note[Lưu ý]
Nếu copy/paste JSON, **không quên** thay thế các giá trị mặc định như:
- `YOUR_NEWSAPI_KEY`
- `YOUR_OPENROUTER_API_KEY`
- `YOUR_OPENAI_API_KEY`
- `YOUR_GMAIL_OAUTH2_CREDENTIALS`
:::

---

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**

#### **🔹 Node 1: Schedule Trigger (Lịch chạy hàng ngày)**
- **Cấu hình thời gian chạy**:
  - Ví dụ: **7h sáng** (để gửi tin tức hàng ngày).
  - **Format**: `0 7 * * *` (7h00 hàng ngày).

#### **🔹 Node 2: Get Latest News (Lấy tin tức từ NewsAPI)**
- **Tham số cần chỉnh**:
  - `url`: `https://newsapi.org/v2/top-headlines?country=us&apiKey=YOUR_NEWSAPI_KEY`
  - **Thay thế `YOUR_NEWSAPI_KEY`** bằng API Key của bạn.
  - **Lựa chọn nguồn tin tức**: `country=us` (Mỹ), có thể thay bằng `country=vn` (Việt Nam) hoặc `sources=bbc-news` (nhiều nguồn khác).

#### **🔹 Node 3: Model (Claude AI - Chuyển đổi tin tức)**
- **Credentials**: `openRouterApi` (đã cấu hình trước khi import).
- **Model**: `anthropic/claude-3.7-sonnet` (được sử dụng mặc định).
- **Prompt**: AI sẽ tự động **chuyển đổi tin tức thành định dạng email** (không cần chỉnh sửa).

#### **🔹 Node 4: Newsletter Agent (GPT-4 - Tạo script audio)**
- **Credentials**: `openAiApi` (đã cấu hình trước).
- **Model**: `gpt-4o` (để tạo script 2 phút).
- **Prompt**: AI sẽ **tạo script tự nhiên** từ tin tức, phù hợp với âm thanh.

#### **🔹 Node 5: Transcribe Newsletter (OpenAI TTS - Chuyển văn bản thành âm thanh)**
- **Credentials**: `openAiApi` (đã cấu hình trước).
- **Resource**: `audio` (chuyển văn bản thành âm thanh).
- **Lưu ý**:
  - **Chất lượng âm thanh**: OpenAI TTS tạo ra giọng nói **như người thật**, nhưng có thể **thử nghiệm** với các model khác như `tts-1` hoặc `tts-1-hd`.
  - **Kích thước file**: Nếu file âm thanh quá lớn, có thể **cắt ngắn** hoặc **chuyển đổi định dạng**.

#### **🔹 Node 6: Notify Subscriber (Gửi email với tin tức audio)**
- **Credentials**: `gmailOAuth2` (đã cấu hình trước).
- **Email của bạn**: Điền địa chỉ email **để nhận tin tức** (để test).
- **Email của khách hàng**: Điền địa chỉ email **của người nhận** (ví dụ: `khachhang@example.com`).
- **Tiêu đề email**: `📰 Tin tức hàng ngày [Ngày tháng]` (có thể chỉnh sửa).
- **Nội dung email**:
  - **Thêm link download**: Nếu muốn, có thể **đính kèm file audio** hoặc **gửi link nghe trực tiếp**.
  - **Thêm logo/định dạng**: Sử dụng **HTML email** để làm đẹp hơn.

---

### **3. Kích hoạt ⚡️**
1. **Test run** với **dữ liệu mẫu**:
   - Chạy workflow **1 lần** để kiểm tra:
     - Tin tức có được lấy đúng không?
     - AI có chuyển đổi thành tin tức email không?
     - Audio có được tạo thành công không?
     - Email có được gửi đúng không?
2. **Bật Active workflow**:
   - Sau khi **test thành công**, **bật Active** để workflow chạy tự động hàng ngày.

---

## ✍️ **Mẹo & gợi ý nâng cao**

### **🔹 1. Tăng tính cá nhân hóa cho tin tức**
- **Sử dụng biến thể prompt**:
  - Thay vì sử dụng prompt mặc định, **cấu hình lại** để AI:
    - **Chỉ lấy tin tức liên quan** đến ngành nghề của bạn (ví dụ: **tech, finance, health**).
    - **Bổ sung bình luận cá nhân** (ví dụ: "Đây là tin tức quan trọng cho doanh nghiệp của bạn").
- **Ví dụ prompt nâng cao**:
  ```plaintext
  "Viết tin tức hàng ngày cho [Tên Doanh Nghiệp] với nội dung ngắn gọn, tập trung vào [ngành nghề]. Đảm bảo:
  - Mở đầu bằng tin tức quan trọng nhất.
  - Sử dụng ngôn ngữ chuyên nghiệp nhưng dễ đọc.
  - Kết thúc bằng 1 câu khuyến nghị hành động."
  ```

### **🔹 2. Lưu log và theo dõi hiệu suất**
- **Thêm node `stickyNote`** để ghi lại:
  - **Số lượng tin tức được lấy**.
  - **Thời gian chạy**.
  - **Lỗi nếu có**.
- **Sử dụng node `httpRequest`** để gửi log đến **Google Sheets** hoặc **Notion** để theo dõi.

### **🔹 3. Gửi tin tức qua Slack/Telegram**
- **Thêm node `slack`** hoặc `telegram`** để thông báo tin tức:
  - Khi tin tức được tạo, **gửi tin nhắn** đến nhóm Slack/Telegram.
  - **Đính kèm link nghe audio** hoặc **file âm thanh**.

### **🔹 4. Tự động chia sẻ trên mạng xã hội**
- **Thêm node `twitter`** hoặc `facebook`** để tự động chia sẻ tin tức:
  - Khi tin tức được tạo, **post lên Twitter/Facebook** với link nghe audio.

### **🔹 5. Tối ưu hóa chất lượng âm thanh**
- **Thử nghiệm các model TTS**:
  - `tts-1` (chất lượng cao, giọng nam/nữ).
  - `tts-1-hd` (chất lượng siêu cao, giọng tự nhiên).
- **Cắt ngắn audio**:
  - Nếu audio quá dài, **cắt bỏ phần giới thiệu** hoặc **tóm tắt lại**.

---

## 📌 **Kết luận**
Workflow này **giải phóng bạn khỏi công việc lặp lại** khi tạo tin tức hàng ngày. Bằng cách **tự động hóa toàn bộ quy trình** từ lấy tin tức đến gửi email, các sếp có thể:
✅ **Tiết kiệm thời gian** (không cần viết email hàng ngày).
✅ **Tăng tính chuyên nghiệp** (tin tức được AI chuyển đổi thành định dạng tốt).
✅ **Mở rộng đến nhiều khách hàng** (gửi tin tức tự động hàng ngày).

**Bắt đầu ngay hôm nay!**
1. **Import workflow** và **cấu hình các API key**.
2. **Test run** và **bật Active**.
3. **Nhận tin tức audio hàng ngày** mà không cần làm gì!

**🚀 Cần hỗ trợ thêm?** Liên hệ với [Abideen Bello](https://www.linkedin.com/in/abideenbello/) (tác giả workflow) để **cấu hình custom** cho doanh nghiệp của bạn!

---
**#n8n #Automation #AIContent #TinTứcAudio #NoCode**