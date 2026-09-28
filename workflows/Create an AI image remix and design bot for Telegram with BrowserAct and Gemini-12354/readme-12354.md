---
title: "🎨 **Tự Động Hóa Bot AI Remix Ảnh & Thiết Kế Telegram Với Gemini & BrowserAct - Không Cần Code**"
description: "Tạo bot Telegram thông minh tự động phân tích, remix ảnh từ input của người dùng hoặc lấy cảm hứng từ PromptHero, sinh ảnh cao cấp bằng Gemini và OpenRouter. Hoàn toàn tự động hóa từ đầu đến cuối, hoạt động 24/7 trên Telegram."
slug: "bot-ai-remix-anh-telegram-gemini-browseract"
tags: [n8n, automation, ai-chatbot, content-creation, browseract, google-gemini, telegram-bot]
keywords: [tự động hóa bot telegram ai, remix ảnh bằng gemini, browseract n8n, tạo bot thiết kế ảnh tự động, workflow n8n ai chatbot]
---

# 🚀 **Bot AI Remix Ảnh & Thiết Kế Telegram: Từ Input → Ảnh Cao Cấp Trong Vài Giây**

## 📌 **Nỗi Đau Của Các Sếp**
Bạn đã bao giờ phải:
- **Tốn thời gian** để tìm kiếm và chỉnh sửa ảnh từ đầu?
- **Không biết cách** biến một bức ảnh cũ thành một tác phẩm mới với phong cách riêng?
- **Mất nhiều công sức** để tạo ra những mô tả chi tiết cho AI sinh ảnh?
- **Không có bot** tự động hóa toàn bộ quy trình từ input đến output?

**Bot AI Remix & Design này giải quyết tất cả!** Với công nghệ **Gemini AI, BrowserAct, và OpenRouter**, bot sẽ:
✅ **Phân tích** bức ảnh của bạn (độ sáng, màu sắc, chủ đề)
✅ **Tạo mô tả chi tiết** để sinh ảnh mới với phong cách cao cấp
✅ **Lấy cảm hứng** từ PromptHero (trending prompts trên mạng)
✅ **Sinh ảnh mới** trong vài giây và cho phép bạn chỉnh sửa liên tục
✅ **Hoạt động 24/7** trên Telegram, không cần can thiệp thủ công

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần thiết kế ảnh từ đầu, chỉ cần upload hoặc nhắn tin.
- **Chất lượng cao**: Ảnh sinh ra với mô tả chi tiết, phong cách chuyên nghiệp.
- **Tương tác linh hoạt**: Chỉnh sửa, tái sinh ảnh theo ý muốn với các nút "Regenerate" và "Next".
- **Hoạt động liên tục**: Bot hoạt động 24/7, không cần người quản lý.
- **Cá nhân hóa**: Mỗi người dùng có trải nghiệm riêng với trạng thái lưu trữ trên Google Sheets.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Để workflow này hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Telegram Bot**:
   - [Tạo Bot Telegram](https://core.telegram.org/bots#botfather) và lấy **Token API**.
   - Cài đặt bot vào nhóm hoặc chat cá nhân để test.

2. **Google Sheets (Bảng Excel)**:
   - Tạo một file Google Sheets với **5 tab** sau (đặt tên chính xác):
     - `PromptHero` (lưu trending prompts từ BrowserAct)
     - `Current State` (lưu trạng thái của người dùng)
     - `UserImage` (lưu ảnh upload từ người dùng)
     - `Current Image` (lưu ảnh đang được xử lý)
     - `PromptHero Database` (lưu dữ liệu PromptHero)
   - **Chia sẻ quyền** cho n8n với quyền **Editor**.
   - **Lấy ID của file** (đường link chia sẻ → sao chép phần sau `d/` và trước `/edit`).

3. **BrowserAct API**:
   - Đăng ký tài khoản [BrowserAct](https://www.browseract.com/) và lấy **API Key**.
   - Tải template **"Image Remix & Design Bot"** từ [đây](https://www.browseract.com/templates) và lưu vào tài khoản BrowserAct.
   - **Lấy Workflow ID** của template này (thông tin trong tài khoản BrowserAct).

4. **Google Gemini API**:
   - [Đăng ký API Key Google Gemini](https://makersuite.google.com/app/apikey) (miễn phí 1 triệu credit/tháng).
   - Thêm **credentials** trong n8n với tên `googlePalmApi`.

5. **OpenRouter API** (tùy chọn):
   - [Đăng ký OpenRouter](https://openrouter.ai/) và lấy **API Key**.
   - Thêm **credentials** trong n8n với tên `openRouterApi`.

6. **n8n Self-Hosted**:
   :::info[Gợi ý hạ tầng cho n8n]
   Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
   👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
   👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
   :::
---

---

## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/12354](https://n8n.io/workflows/12354) (hoặc copy/paste JSON từ link này).
- Trong **n8n Editor**, chọn **Import Workflow** → Chọn file JSON hoặc dán JSON vào ô nhập.
- **Kích hoạt workflow** bằng cách bật nút **Active** ở góc trên bên phải.

### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này **phức tạp** và có **52 node**, nhưng chỉ cần chú ý đến các bước sau:

#### **A. Cấu Hình Credentials (Tài Khoản)**
- **Telegram**:
  - Node: `Telegram Trigger`, `Notify User`, `Get Picture from User`, `Send Photo`, `Chat With User`, `Ask for changes`, `Send Finishing Alert`.
  - **Điền**:
    - **Credentials**: `telegramApi` (tên trong n8n).
    - **Token**: Token bot Telegram (lấy từ BotFather).
    - **Chat ID**: ID của chat cá nhân hoặc nhóm (lấy bằng cách gửi `/get_id` cho bot).

- **Google Sheets**:
  - Node: Tất cả node có `googleSheetsOAuth2Api` (ví dụ: `Set user State`, `Get Prompt`, `Save Images To Database`).
  - **Điền**:
    - **Credentials**: `googleSheetsOAuth2Api`.
    - **File ID**: ID của Google Sheets (lấy từ bước chuẩn bị).
    - **Sheet Name**: Đặt tên tab chính xác theo yêu cầu (ví dụ: `PromptHero`, `Current State`).
    - **Range**: Để trống hoặc điền `A1:Z` (n8n sẽ tự động điều chỉnh).

- **BrowserAct**:
  - Node: `Extract Top AI-Generated Images`.
  - **Điền**:
    - **Credentials**: `browserActApi`.
    - **API Key**: API Key từ BrowserAct.
    - **Workflow ID**: Workflow ID của template "Image Remix & Design Bot".

- **Google Gemini**:
  - Node: `Google Gemini`, `Google Gemini2`, `Google Gemini1`, `Fix Output`, `Generate Thumbnail`.
  - **Điền**:
    - **Credentials**: `googlePalmApi`.
    - **API Key**: API Key từ Google Cloud.

- **OpenRouter** (nếu sử dụng):
  - Node: `OpenRouter`, `OpenRouter1`.
  - **Điền**:
    - **Credentials**: `openRouterApi`.
    - **API Key**: API Key từ OpenRouter.
    - **Model**: `openai/gpt-4o` (đã đặt sẵn trong workflow).

#### **B. Cấu Hình Node Quan Trọng**
1. **`Telegram Trigger`**:
   - Chọn **Event**: `message` (để bot phản ứng với mọi tin nhắn).
   - **Filter**: Để trống hoặc chỉ định `text` hoặc `photo` nếu muốn lọc input.

2. **`Switch Query` và `Switch User State`**:
   - Các node này **quan trọng** để điều khiển logic workflow.
   - **Không cần chỉnh sửa** nếu đã import file JSON chính xác.

3. **`Agent` Nodes** (ví dụ: `Validate user input`, `Analyze the Chosen image`):
   - Các node này sử dụng **LangChain Agent** để phân tích text hoặc ảnh.
   - **Không cần chỉnh sửa** trừ khi muốn thay đổi logic AI.

4. **`Google Sheets` Nodes** (ví dụ: `Set user State1`, `Get Description`):
   - **Range**: Đặt theo cột cần update (ví dụ: `UserState!A1`).
   - **Header**: Chọn `Yes` nếu sheet có header.

5. **`BrowserAct` Node**:
   - **Template ID**: Điền ID của template "Image Remix & Design Bot".
   - **Limit**: Đặt số lượng prompts muốn lấy (ví dụ: `10`).

6. **`Generate Thumbnail`**:
   - Node này tự động lấy **prompt** từ `Generate Image From PromptHero` hoặc `Generate Image From UserData`.
   - **Không cần chỉnh sửa** trừ khi muốn thay đổi mô tả mặc định.

---

### **3. Kích Hoạt ⚡️**
- **Test Run**:
  - Gửi tin nhắn `/start` cho bot Telegram để kích hoạt workflow.
  - Bot sẽ phản hồi và bắt đầu quá trình:
    1. Nếu gửi **text**: Bot phân loại và trả lời hoặc lấy cảm hứng từ PromptHero.
    2. Nếu gửi **ảnh**: Bot phân tích và sinh ảnh remix.
- **Bật Active**:
  - Sau khi test thành công, bật nút **Active** để workflow chạy liên tục.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tích Hợp Slack/Telegram Log**:
   - Thêm node **Slack** hoặc **Telegram** để log tất cả hoạt động của bot.
   - Ví dụ: Sau khi sinh ảnh thành công, gửi thông báo đến Slack với link preview.

2. **Lưu Lịch Sử Ảnh**:
   - Sử dụng **Google Drive** hoặc **AWS S3** để lưu ảnh sinh ra thay vì chỉ Google Sheets.
   - Node `Save Images To Database` có thể được thay thế bằng node **Google Drive** hoặc **HTTP Request**.

3. **Báo Cáo Định Kỳ**:
   - Thêm node **Google Sheets** hoặc **Email** để gửi báo cáo hàng ngày về số lượng ảnh sinh ra, chủ đề phổ biến.

4. **Cập Nhật PromptHero**:
   - Thêm node **HTTP Request** để tự động cập nhật trending prompts từ PromptHero mỗi ngày.

5. **Chỉnh Sửa Logic AI**:
   - Nếu muốn bot **tương tác hơn**, chỉnh sửa **prompt** trong node `Google Gemini` hoặc `OpenRouter` để cải thiện chất lượng output.

---

## 📌 **Kết Luận**
Bot **AI Remix & Design** này là **giải pháp hoàn hảo** cho các sếp muốn tự động hóa quy trình tạo ảnh, thiết kế và lấy cảm hứng một cách **tiện lợi, nhanh chóng và chuyên nghiệp**. Với công nghệ **Gemini AI, BrowserAct và OpenRouter**, bot không chỉ sinh ảnh mà còn **phân tích, remix và cải tiến** theo ý muốn của người dùng.

**Hành động ngay!**
1. Chuẩn bị tài khoản và credentials theo hướng dẫn.
2. Import workflow và cấu hình các node quan trọng.
3. Kích hoạt và test với `/start` trên Telegram.
4. **Tận hưởng** bot AI hoạt động 24/7 cho bạn!

---
**💡 Cần hỗ trợ?** Hãy tham gia [Discord n8n](https://discord.gg/n8n) hoặc xem [tutorial video](https://www.youtube.com/watch?v=GqeKd9aYjW4) để hiểu rõ hơn về cách cấu hình BrowserAct và n8n!