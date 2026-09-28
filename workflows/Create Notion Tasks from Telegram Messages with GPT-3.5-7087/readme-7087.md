---
title: "🚀 Tự Động Hóa: Biến Tin Nhắn Telegram & Voice Note Thành Task Notion bằng AI"
description: "Hướng dẫn cài đặt workflow n8n giúp chuyển đổi tin nhắn văn bản hoặc ghi âm giọng nói từ Telegram thành các tác vụ chi tiết trong Notion Database nhờ sức mạnh của GPT-3.5."
slug: "telegram-notion-tasks-ai"
tags: [n8n, automation, no-code, notion, telegram, ai]
keywords: [n8n workflow, tự động hóa notion, telegram bot, ai summarization, voice to text]
---

# 🚀 Tự Động Hóa: Biến Tin Nhắn Telegram & Voice Note Thành Task Notion bằng AI

Bạn có bao giờ đang di chuyển, họp hành hoặc bận rộn mà nảy ra một ý tưởng công việc quan trọng? Thay vì phải mở điện thoại, tìm ứng dụng Notion, nhập liệu thủ công và loay hoay với định dạng, bạn chỉ cần **gửi một tin nhắn nhanh** hoặc **ghi âm giọng nói** cho một bot Telegram.

Workflow này chính là "trợ lý ảo" của bạn. Nó lắng nghe mọi tin nhắn (cả text lẫn voice note), sử dụng AI (GPT-3.5) để phân tích nội dung, trích xuất ngày tháng, mô tả công việc và tự động tạo một Task hoàn chỉnh trong Notion Database của bạn. Không cần code, không cần thao tác phức tạp, chỉ cần "nói là xong".

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian cực đại:** Biến quá trình nhập liệu 2-3 phút xuống còn 5 giây (chỉ cần gửi tin nhắn).
- **Hỗ trợ đa phương thức:** Nhận cả tin nhắn văn bản lẫn **Voice Note** (AI sẽ tự chuyển giọng nói thành chữ - Transcribe).
- **Trí tuệ nhân tạo thông minh:** GPT-3.5 sẽ tự động hiểu ngữ cảnh, xác định ngày deadline, mô tả chi tiết công việc thay vì chỉ lưu một dòng chữ thô.
- **Tích hợp liền mạch:** Dữ liệu được đẩy thẳng vào Notion Database, sẵn sàng cho việc quản lý dự án.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Telegram:** Tạo một Bot mới qua @BotFather và lấy `Bot Token`.
2. **Tài khoản OpenAI:** Cần `API Key` để sử dụng GPT-3.5 (cho việc phân tích text và transcribe audio).
3. **Tài khoản Notion:**
   - Tạo một Database (ví dụ: "Tasks").
   - Lấy `Internal ID` của Database đó.
   - Tạo `Integration Token` trong Notion Settings.
4. **Tài khoản n8n:** Nơi để chạy workflow.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow từ link gốc hoặc copy toàn bộ cấu hình.
1. Mở n8n Editor.
2. Chọn **Import from URL** hoặc **Import from File**.
3. Dán JSON hoặc chọn file đã tải về.
4. Workflow sẽ hiện ra với 8 nodes chính.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Đây là phần quan trọng nhất. Các sếp cần click vào từng node và cấu hình credentials cũng như tham số:

**A. Nhóm Telegram (3 Nodes)**
1. **Telegram Trigger**:
   - Chọn credentials `telegramApi` (tạo mới nếu chưa có, điền Bot Token).
   - **Quan trọng:** Ở phần `Chat ID`, các sếp cần điền ID chat của mình. *Mẹo: Gửi tin "start" cho bot, sau đó xem log trong n8n để lấy Chat ID chính xác.*
2. **Download recording**:
   - Chọn cùng credentials `telegramApi`.
   - Node này tự động tải file audio khi nhận được voice note.
3. **Confirmation message**:
   - Chọn cùng credentials `telegramApi`.
   - Node này gửi tin nhắn xác nhận "Đã tạo task thành công" lại cho bạn trên Telegram.

**B. Nhóm AI - OpenAI (2 Nodes)**
1. **Transcribe recording**:
   - Chọn credentials `openAiApi`.
   - Đảm bảo model được chọn là `whisper-1` (hoặc model transcribe tương đương) để chuyển giọng nói thành văn bản.
2. **Interpret Request**:
   - Chọn credentials `openAiApi`.
   - Model: `gpt-3.5-turbo` (hoặc `gpt-4` nếu muốn chính xác hơn).
   - **System Prompt:** Mặc định đã khá tốt, nhưng các sếp có thể chỉnh sửa prompt để AI hiểu rõ hơn về cách phân loại task, ví dụ: *"Hãy phân tích tin nhắn, trích xuất tiêu đề, mô tả, và ngày hoàn thành. Nếu không có ngày, để trống."*

**C. Nhóm Logic & Notion (2 Nodes)**
1. **Switch text vs audio**:
   - Node này tự động phân luồng: Nếu là text thì đi thẳng sang AI phân tích, nếu là audio thì đi qua bước Transcribe trước. Thường không cần chỉnh sửa gì nhiều, chỉ cần đảm bảo mapping output đúng.
2. **Create new Task in Notion**:
   - Chọn credentials `notionApi`.
   - **Database ID:** Dán Internal ID của Notion Database.
   - **Properties:** Map các trường dữ liệu từ output của node "Interpret Request" (ví dụ: `title`, `description`, `due_date`) vào các cột tương ứng trong Notion.
   - **Timezone:** ⚠️ **Rất quan trọng:** Đảm bảo Timezone trong node này khớp với Timezone trong cài đặt chung của n8n (Settings > Timezone) để tránh lệch giờ deadline.

**D. Node Code (Handle Text Message)**
- Node này xử lý text thô trước khi đưa vào AI. Thường không cần chỉnh sửa code nếu không muốn thay đổi logic xử lý chuỗi.

#### 3. Kích hoạt ⚡️
1. **Test Run:**
   - Bật nút **Execute Workflow** (hoặc dùng Webhook URL nếu chạy local).
   - Gửi một tin nhắn text đơn giản cho Bot Telegram: *"Họp với khách hàng A lúc 10h sáng mai về dự án X"*.
   - Kiểm tra xem Notion có xuất hiện task mới không và Telegram có nhận được tin xác nhận không.
   - Gửi một **Voice Note** thử nghiệm để kiểm tra tính năng Transcribe.
2. **Bật Active:**
   - Khi mọi thứ hoạt động ổn, bật công tắc **Active** ở góc trên bên phải n8n.
   - Workflow sẽ bắt đầu lắng nghe mọi tin nhắn gửi đến Bot.

### ✍️ Mẹo & gợi ý nâng cao
- **Cá nhân hóa Prompt:** Trong node `Interpret Request`, hãy thêm các quy tắc cụ thể. Ví dụ: *"Nếu tin nhắn chứa từ 'khẩn cấp', hãy thêm tag 'Urgent' vào Notion."*
- **Phân loại theo dự án:** Nếu Notion Database của bạn có cột "Project", hãy yêu cầu AI trong prompt nhận diện dự án và map vào cột đó.
- **Gửi báo cáo tổng hợp:** Kết nối thêm một node Telegram khác để gửi tổng hợp các task đã tạo trong ngày vào cuối giờ.
- **Hỗ trợ nhiều ngôn ngữ:** GPT-3.5 hỗ trợ đa ngôn ngữ. Các sếp có thể ghi âm bằng tiếng Việt, AI sẽ tự động chuyển thành text và tạo task (có thể yêu cầu AI dịch sang tiếng Anh nếu Notion dùng tiếng Anh).

### 📌 Kết luận
Workflow **Create Notion Tasks from Telegram Messages with GPT-3.5** là một công cụ "vũ khí bí mật" cho những ai cần ghi chú nhanh và quản lý công việc hiệu quả. Thay vì để ý tưởng trôi đi trong đầu, hãy biến chúng thành hành động cụ thể trong Notion chỉ với một thao tác gửi tin nhắn.

Các sếp hãy thử ngay hôm nay để trải nghiệm sự tiện lợi của việc "nói là có" trong quản lý công việc! 🚀