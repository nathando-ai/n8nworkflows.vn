---
title: "🤖 **Tự Động Xử Lý Album Hình Telegram + AI NanoBanana: Tạo Nội Dung Chuyên Nghiệp Miễn Phí**"
description: "Workflow này tự động nhận album hình từ Telegram, lưu trữ dữ liệu, xử lý bằng AI NanoBanana (OpenRouter) và trả về bản tóm tắt + hình ảnh chuyên nghiệp. Giúp các sếp tiết kiệm 10+ giờ/tháng viết nội dung, đồng thời cá nhân hóa thông điệp cho từng khách hàng."
slug: "tu-dong-xu-ly-album-hinh-telegram-ai-nanobanana"
tags: [n8n, automation, content-creation, multimodal-ai, telegram-bot, data-tables, openrouter]
keywords: [n8n workflow telegram, tự động hóa xử lý hình ảnh, AI tạo nội dung, nano banana ai, openrouter api, data tables cache]
---

# 🚀 **Tự Động Xử Lý Album Hình Telegram + AI NanoBanana: Giải Pháp Tạo Nội Dung Chuyên Nghiệp**

### **Nỗi Đau Của Các Sếp**
Các sếp thường phải:
- **Làm thủ công** việc tóm tắt album hình từ Telegram (ví dụ: bài viết blog, báo cáo dự án, chia sẻ sản phẩm).
- **Tốn thời gian** để tìm kiếm hình ảnh, viết caption, và tổ chức lại thông tin.
- **Không cá nhân hóa** nội dung vì thiếu công cụ tự động hóa.
- **Mất trải nghiệm** khi phải xử lý hàng chục album mỗi ngày.

**Workflow này giải quyết tất cả!** Nó tự động:
✅ **Nhận album hình** từ Telegram (bao gồm caption và tất cả hình ảnh).
✅ **Lưu trữ dữ liệu** trong Data Tables (cache) để theo dõi trạng thái xử lý.
✅ **Xử lý bằng AI NanoBanana** (OpenRouter) để tạo caption chuyên nghiệp.
✅ **Trả về kết quả** dưới dạng hình ảnh + văn bản, gửi trực tiếp về Telegram.
✅ **Hoạt động 24/7** mà không cần can thiệp của con người.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Xử lý hàng trăm album hình chỉ trong vài giây.
- **Nội dung chuyên nghiệp**: AI NanoBanana tự động viết caption, tóm tắt, và tối ưu hình ảnh.
- **Hoạt động liên tục**: Workflow chạy tự động khi có album mới, không cần can thiệp.
- **Cá nhân hóa**: Gửi kết quả trực tiếp về Telegram với hình ảnh + văn bản sẵn sàng chia sẻ.
- **Dữ liệu được cache**: Tất cả album đã xử lý được lưu trong Data Tables để theo dõi.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi chạy workflow, các sếp cần chuẩn bị:
1. **Tài khoản Telegram Bot**:
   - Tạo bot mới tại [@BotFather](https://t.me/BotFather) và sao chép **API Token**.
   - Thêm **Telegram Credentials** trong n8n với token này.
   - Cập nhật URL trong node **"prepare user messages"** (nếu sử dụng liên kết tải hình trực tiếp từ Telegram).

2. **Data Table**:
   - Tạo một bảng mới trong n8n với các cột sau:
     - `chat_id` (ID chat của người dùng)
     - `message_id` (ID tin nhắn gốc)
     - `media_group` (ID nhóm media của album)
     - `message` (Caption của album)
     - `status` (Trạng thái: `processing`, `done`, hoặc `failed`).

3. **API Key OpenRouter**:
   - Đăng ký tài khoản [OpenRouter](https://openrouter.ai/) và lấy **API Key**.
   - Thêm **OpenRouter Credentials** trong n8n với key này (dùng cho node **"Call NanoBanana via OpenRouter"**).

4. **NanoBanana AI**:
   - Workflow sử dụng NanoBanana (giao diện của OpenRouter) để xử lý hình ảnh + văn bản. Đảm bảo API Key đã được cấu hình đúng.
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/9288) hoặc copy toàn bộ JSON từ trang này.
- Trong **n8n Editor**, nhấn **"Import"** > **"From JSON"** và dán nội dung JSON.
- **Hoặc** copy/paste JSON vào ô **"Import Workflow"** và nhấn **"Import"**.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflows này có **28 node**, nhưng chỉ cần chú ý đến các node quan trọng sau:

##### **A. Cấu Hình Telegram Bot**
- **Node "Telegram Trigger"**:
  - Đảm bảo **credentials** `"telegramApi"` đã được cấu hình với **API Token** của bot.
  - Cập nhật **chat_id** trong node **"Send initial notification"** nếu cần gửi thông báo cho chat cụ thể.

- **Node "Get a file"**:
  - Kiểm tra **resource** là `"file"` (đã mặc định).
  - Nếu sử dụng **liên kết tải hình trực tiếp** từ Telegram, cập nhật URL trong node **"prepare user messages"** theo mẫu:
    ```
    https://api.telegram.org/file/bot<TOKEN>/<FILE_PATH>
    ```

##### **B. Cấu Hình Data Tables**
- **Node "Upsert row(s)"**:
  - Đảm bảo **Data Table** đã được tạo với các cột (`chat_id`, `message_id`, `media_group`, `message`, `status`).
  - Node này sẽ **thêm hoặc cập nhật** tin nhắn vào bảng khi có album mới.

- **Node "Get new requests"**:
  - Cập nhật **thời gian kiểm tra mới** trong **Schedule Trigger** (ví dụ: 10 giây) để workflow nhanh chóng phát hiện album mới.

##### **C. Cấu Hình AI NanoBanana (OpenRouter)**
- **Node "Call NanoBanana via OpenRouter"**:
  - Đảm bảo **credentials** `"openRouterApi"` đã được thêm với **API Key** của OpenRouter.
  - Cập nhật **URL API** trong node này (mặc định là `https://openrouter.ai/api/v1/chat/completions`).
  - **Prompt mẫu** (có thể chỉnh sửa trong node **"Summarize"**):
    ```
    Tóm tắt album hình này thành một bài viết ngắn (5-7 câu) với tiêu đề hấp dẫn. Đảm bảo bao gồm tất cả hình ảnh và caption. Tránh lặp lại thông tin.
    ```

##### **D. Node Quan Trọng Khác**
- **Node "Is media group with images?"**:
  - Kiểm tra **điều kiện** để chỉ xử lý album **chứa hình ảnh** (loại bỏ tin nhắn văn bản hoặc video).

- **Node "Convert to File"**:
  - Chuyển dữ liệu từ **Base64** sang **binary** để AI NanoBanana xử lý hình ảnh.

- **Node "status:processing" và "status:done"**:
  - Cập nhật trạng thái trong Data Tables để theo dõi tiến trình xử lý.

##### **E. Test Run Trước Khi Bật Active**
- Nhấn **"Run Workflow"** với một **album hình mẫu** để kiểm tra:
  - AI có tạo caption không?
  - Hình ảnh có được gửi lại Telegram không?
  - Trạng thái trong Data Tables có được cập nhật không?

---

#### **3. Kích Hoạt ⚡️**
- Sau khi kiểm tra thành công, chuyển **status** của workflow từ **"Inactive"** sang **"Active"**.
- **Lưu ý**: Workflow sẽ chạy tự động khi có tin nhắn mới từ Telegram (do **Telegram Trigger**).

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Gửi kết quả về Slack/Email**:
   - Thêm node **Slack** hoặc **Email** sau **"Send result message"** để gửi báo cáo định kỳ cho team.

2. **Lưu log xử lý**:
   - Thêm node **StickyNote** hoặc **Google Sheets** để ghi lại lịch sử xử lý (chat_id, thời gian, kết quả).

3. **Tối ưu AI với Prompt cá nhân hóa**:
   - Chỉnh sửa **prompt** trong node **"Summarize"** để phù hợp với ngành nghề (ví dụ: marketing, giáo dục, y tế).

4. **Xử lý lỗi tự động**:
   - Thêm node **Error Handling** (ví dụ: **If Error**) để gửi thông báo lỗi về Telegram nếu AI không xử lý được.

5. **Dùng cho nhiều bot**:
   - Tạo **credentials Telegram** riêng cho từng bot và cập nhật trong node **"Telegram Trigger"**.

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp cần tự động hóa việc xử lý album hình Telegram và tạo nội dung chuyên nghiệp bằng AI. Bằng cách kết hợp **Telegram, Data Tables, và NanoBanana**, các sếp sẽ:
✔ **Tiết kiệm thời gian** viết nội dung.
✔ **Cải thiện chất lượng** thông điệp với AI.
✔ **Hoạt động 24/7** mà không cần can thiệp.

**Hành động ngay!**
1. Import workflow vào n8n.
2. Cấu hình Telegram Bot và Data Tables.
3. Bật **Active** và bắt đầu tự động hóa!

---
**💡 Mẹo cuối**: Nếu gặp khó khăn, tham khảo [hướng dẫn chi tiết của Eduard](https://www.linkedin.com/in/parsadanyan/) hoặc liên hệ hỗ trợ n8n. Chúc các sếp thành công! 🚀