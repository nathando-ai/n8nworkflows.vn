---
title: "🚀 Tự động lọc và gửi tin tức thời gian thực lên Telegram bằng Google Gemini AI & BrowserAct"
description: "Xây dựng hệ thống tự động cào tin tức, lọc nội dung thông minh bằng AI Agent và gửi thông báo trực quan lên kênh Telegram 24/7."
slug: "tu-dong-loc-tin-tuc-gemini-ai-browseract-telegram"
tags: [n8n, automation, no-code, gemini-ai, telegram, web-scraping]
keywords: [n8n workflow, lọc tin tức tự động, google gemini ai, browseract, telegram automation]
---

# 🚀 Tự động lọc và gửi tin tức thời gian thực lên Telegram bằng Google Gemini AI & BrowserAct

Các sếp có đang tốn hàng giờ mỗi ngày để lướt web, đọc báo, chọn lọc thông tin quan trọng rồi copy-paste thủ công lên kênh Telegram cộng đồng của mình không? Việc này vừa nhàm chán, vừa tốn thời gian mà lại dễ bỏ lỡ các tin nóng.

Đừng lo! Bài viết này sẽ hướng dẫn các sếp thiết lập một siêu workflow n8n tự động hóa 100%: Tự động cào tin tức mới nhất, dùng **Google Gemini AI** thông minh để phân tích và lọc theo từ khóa, sau đó tự động bắn tin tức trực quan kèm hình ảnh thẳng lên **Telegram Channel**. Không cần biết lập trình, chỉ cần kéo thả và cấu hình!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Không cần đụng tay vào việc cào dữ liệu hay lọc tin thủ công.
- **AI thông minh chọn lọc:** Google Gemini AI giúp lọc chính xác các bài viết có chứa hoặc liên quan đến từ khóa mục tiêu, bỏ qua tin rác.
- **Định dạng trực quan:** Tin nhắn gửi lên Telegram có đầy đủ hình ảnh, tiêu đề hấp dẫn và đường link gốc (Rich Media).
- **Hoạt động không nghỉ:** Chạy ngầm theo lịch trình (Schedule Trigger) đều đặn mỗi ngày.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **BrowserAct API Account** (Cùng Template "News Content Marketing Automation") để cào tin tức web.
- **Google Gemini API Key** cho AI Agent xử lý ngôn ngữ.
- **Telegram Bot Token & Channel ID** để gửi tin nhắn.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần tải file JSON của workflow này từ n8n.io (Link gốc: [Workflow #8915](https://n8n.io/workflows/8915)) hoặc copy toàn bộ JSON dán trực tiếp vào n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow gồm 12 nodes, các sếp cần chú ý cấu hình kỹ các điểm sau để hệ thống chạy mượt mà:

- **Schedule Trigger:** Thiết lập chu kỳ thời gian muốn workflow quét tin tức mới (ví dụ: mỗi 2 tiếng, mỗi ngày 3 lần...).
- **Run WorkFlow & Get WorkFlow Data (HTTP Request nodes):** 
  - Kết nối tài khoản **BrowserAct** qua `httpBearerAuth`.
  - Cập nhật đúng `workflow_id` ứng với template "News Content Marketing Automation" trong tài khoản BrowserAct của các sếp.
- **KeyWords filtering (AI Agent) & Google Gemini:** 
  - Kết nối tài khoản **Google Gemini** (`googlePalmApi`).
  - Định nghĩa danh sách từ khóa mục tiêu trong phần prompt của AI Agent để hệ thống biết cần lọc tin về lĩnh vực gì.
  - Đảm bảo node **Structured Output Parser** được gắn kết chặt chẽ để AI luôn trả về cấu trúc dữ liệu chuẩn xác.
- **Code - Clean Output:** Node code này giúp làm sạch và định dạng lại văn bản thô từ AI thành bố cục đẹp mắt, dễ đọc.
- **Send a News Photo To Telegram (Telegram node):** 
  - Cấu hình thông tin **Telegram API Credentials**.
  - Nhập **Chat ID** của kênh Telegram (Telegram Channel) nơi muốn xuất bản tin tức.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** chạy thử thủ công với dữ liệu mẫu để kiểm tra từ bước cào dữ liệu đến bước gửi Telegram.
- Nếu mọi thứ xanh mướt, gạt công tắc sang **Active** để hệ thống tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Đa kênh thông báo:** Ngoài Telegram, các sếp có thể nhân bản nhánh cuối để bắn thêm tin qua Discord, Slack hoặc Email.
- **Lưu trữ dữ liệu:** Thêm node **Google Sheets** hoặc **Airtable** trước bước gửi Telegram để lưu lại lịch sử các tin bài đã xuất bản, phục vụ việc phân tích content sau này.
- **Quản lý lỗi:** Tận dụng node **Check For Errors** để cài thêm thông báo phụ (gửi báo về chat riêng của admin) nếu quá trình cào dữ liệu từ BrowserAct gặp sự cố.

### 📌 Kết luận
Workflow này là trợ thủ đắc lực cho các nhà sáng tạo nội dung, Marketer hoặc các nhà quản trị cộng đồng muốn xây dựng kênh tin tức tự động cập nhật liên tục 24/7. Hãy "lên đồ" ngay hôm nay để tối ưu hóa hiệu suất công việc của các sếp!