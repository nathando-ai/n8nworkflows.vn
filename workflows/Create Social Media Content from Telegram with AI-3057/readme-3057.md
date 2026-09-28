---
title: "🤖 Tự Động Tạo Nội Dung Mạng Xã Hội Từ Telegram Với AI - Không Cần Code"
description: "Workflow này tự động chuyển đổi tin nhắn giọng nói hoặc văn bản từ Telegram thành nội dung mạng xã hội hoàn chỉnh, kèm theo hình ảnh AI sinh tạo - tiết kiệm thời gian cho các sếp lên đồ content 100%."
slug: "tieu-dong-tao-noidung-mang-xa-hoi-tu-telegram-voi-ai"
tags: [n8n, automation, ai, content-creation, telegram, openai]
keywords: [tự động hóa nội dung mạng xã hội, tạo bài viết AI từ Telegram, workflow n8n AI, tự động tạo hình ảnh AI, content marketing tự động]
---

# 🚀 **Tự Động Tạo Nội Dung Mạng Xã Hội Từ Telegram Với AI - Không Cần Code**

### **📌 Nỗi Đau Của Các Sếp Trong Lên Đồ Content**
Các sếp thường phải:
- **Ngồi chờ khách hàng gửi yêu cầu** qua Telegram, rồi phải **ghi chép thủ công** từng ý tưởng.
- **Tốn thời gian chuyển đổi giọng nói thành văn bản** nếu khách hàng gửi voice note.
- **Tìm kiếm thông tin** trên Google để viết bài, mất nhiều giờ cho mỗi post.
- **Không có hình ảnh đẹp** để kèm theo bài viết, phải tìm kiếm trên Freepik/Unsplash hay thuê designer.

**Workflow này giải quyết tất cả!** Chỉ cần khách hàng gửi tin nhắn (giọng nói hoặc văn bản) qua Telegram, hệ thống sẽ:
✅ **Chuyển đổi giọng nói thành văn bản** tự động.
✅ **Tạo nội dung mạng xã hội hoàn chỉnh** (bài viết + mô tả hình ảnh).
✅ **Sinh ra hình ảnh AI** phù hợp với chủ đề.
✅ **Gửi kết quả về Telegram** ngay lập tức.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80% thời gian** lên đồ content so với làm thủ công.
- **Nội dung cá nhân hóa** dựa trên yêu cầu thực tế của khách hàng.
- **Hình ảnh AI sinh tạo** luôn mới mẻ, không cần thiết kế.
- **Hoạt động 24/7** - không cần phải ngồi chờ khách hàng.
- **Giảm thiểu lỗi** so với viết bài thủ công.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi chạy workflow, các sếp cần chuẩn bị:
1. **Tài khoản Telegram Bot**:
   - Tạo bot trên [@BotFather](https://t.me/BotFather) và lấy **API Token**.
   - Cấu hình bot để nhận tin nhắn từ người dùng (cần quyền admin trong group/channel nếu muốn test).
2. **API Key OpenAI**:
   - Đăng ký tài khoản [OpenAI](https://platform.openai.com/) và lấy **API Key**.
   - Chọn mô hình `gpt-4o-mini` (miễn phí) hoặc nâng cấp nếu cần.
3. **API Key SerpAPI** (tùy chọn, để AI tìm kiếm thông tin):
   - Đăng ký [SerpAPI](https://serpapi.com/) và lấy **API Key**.
4. **API Key Hugging Face** (để sinh hình ảnh AI):
   - Đăng ký [Hugging Face](https://huggingface.co/) và lấy **API Key**.
   - **Lưu ý**: Một số mô hình sinh ảnh yêu cầu tài khoản Pro (tùy chọn node `httpRequest` này).
5. **VPS Self-hosted n8n** (khuyến nghị):
   - Workflow này hoạt động liên tục, nên **không nên chạy trên n8n Cloud** (có giới hạn thời gian chạy).
   - 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%).
   - 👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n.io/workflows/3057](https://n8n.io/workflows/3057) và import vào n8n Editor.
- **Cách 2**: Copy toàn bộ JSON từ link trên và paste vào **Import Workflow** trong n8n.
- **Cách 3**: Sử dụng **n8n CLI** để import:
  ```bash
  n8n import workflow.json --workspace "Your Workspace Name"
  ```

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow gồm **12 node**, các sếp cần chú ý cấu hình sau:

##### **🔹 Node 1: Receive Telegram Messages (telegramTrigger)**
- **Cấu hình**:
  - **Credentials**: Chọn `telegramApi` (đã cấu hình trước khi import).
  - **Chat ID**: Nếu muốn test riêng, lấy **Chat ID** của bot bằng cách gửi `/get_id` cho bot.
  - **Trigger**: Chọn `message` để bắt tất cả tin nhắn mới.

##### **🔹 Node 2 & 3: Voice or Text? + Fetch Voice Message (switch + telegram)**
- **Cấu hình**:
  - Node `switch` sẽ phân loại tin nhắn là **text** hoặc **voice**.
  - Nếu là **voice**, node `telegram` sẽ lấy file audio bằng `resource: file`.

##### **🔹 Node 4: Transcribe Voice to Text (openAi)**
- **Cấu hình**:
  - **Credentials**: Chọn `openAiApi`.
  - **Operation**: Đảm bảo chọn `translate` và `resource: audio`.
  - **Lưu ý**: Nếu OpenAI không hỗ trợ transcribe audio, có thể thay thế bằng **Whisper API** của OpenAI (cần cấu hình lại).

##### **🔹 Node 5-6: AI Agent + OpenAI Chat Model (agent + lmChatOpenAi)**
- **Cấu hình**:
  - **Prompt Template**: Workflow đã sẵn sàng, nhưng các sếp có thể **cập nhật prompt** để phù hợp với phong cách content của mình.
    - Ví dụ: Thêm yêu cầu về **tone (chuyên nghiệp, thân thiện, hài hước)**.
    - Thêm **keyword** cần bao gồm trong bài viết.
  - **Model**: Đã chọn `gpt-4o-mini` (rẻ và hiệu quả), có thể thay bằng `gpt-4` nếu cần chất lượng cao hơn.

##### **🔹 Node 7: SerpAPI (toolSerpApi)**
- **Cấu hình**:
  - **Credentials**: Chọn `serpApi`.
  - **Lưu ý**: Nếu không muốn AI tìm kiếm, có thể **bỏ qua node này** bằng cách cấu hình `skip` trong node `switch` trước đó.

##### **🔹 Node 8-9: Structured Output Parser + Extract from File (outputParserStructured + extractFromFile)**
- **Cấu hình**:
  - Node này **tách nội dung** thành:
    - **Bài viết mạng xã hội** (text).
    - **Mô tả hình ảnh** (prompt).
  - **Không cần chỉnh** nếu import đúng file.

##### **🔹 Node 10: Prepare Final Output (set)**
- **Cấu hình**:
  - Node này **sắp xếp dữ liệu** để chuẩn bị gửi về Telegram.
  - **Không cần chỉnh** trừ khi muốn thay đổi định dạng output.

##### **🔹 Node 11: Generate Image (httpRequest)**
- **Cấu hình**:
  - **Credentials**: Chọn `huggingFaceApi` (nếu có) hoặc thay bằng API khác như **Stable Diffusion API**.
  - **API Endpoint**: Workflow sử dụng **Hugging Face Inference API**, nhưng có thể thay bằng:
    - [Replicate](https://replicate.com/) (mô hình Stable Diffusion).
    - [Leonardo.AI](https://leonardo.ai/) (API sinh ảnh dễ dùng).
  - **Lưu ý**:
    - Nếu không muốn sinh ảnh, có thể **bỏ node này** và chỉ giữ text.
    - Nếu sinh ảnh, **kiểm tra mô tả prompt** để hình ảnh phù hợp với nội dung.

---

#### **3. Kích Hoạt ⚡️ Workflow**
1. **Test Run** với dữ liệu mẫu:
   - Gửi **tin nhắn văn bản** hoặc **giọng nói** cho bot Telegram.
   - Kiểm tra output trong **Execution View** của n8n.
2. **Bật Active**:
   - Chuyển trạng thái workflow từ `Inactive` sang `Active`.
   - **Lưu ý**: Nếu chạy trên VPS, đảm bảo **n8n đang chạy 24/7** (sử dụng `systemd` hoặc `pm2`).

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[CÁCH LÀM THÊM]
1. **Gửi kết quả về Slack/Email**:
   - Thêm node `slack` hoặc `email` sau node `Prepare Final Output` để báo cáo tự động.
2. **Lưu log vào Google Sheets**:
   - Sử dụng node `googleSheets` để ghi lại lịch sử yêu cầu và kết quả.
3. **Tự động đăng bài lên Instagram/Facebook**:
   - Kết nối với API của Meta hoặc sử dụng **n8n node Instagram Business**.
4. **Cập nhật prompt cho nhiều loại nội dung**:
   - Tạo **nhiều workflow riêng** cho:
     - **Bài viết Blog**.
     - **Caption Instagram**.
     - **Tin tức ngắn**.
5. **Sử dụng AI khác nhau**:
   - Thay thế OpenAI bằng **Mistral AI** (rẻ hơn) hoặc **Google Vertex AI**.
6. **Tự động chia sẻ kết quả**:
   - Thêm node `telegram` cuối cùng để **gửi kết quả về group khách hàng**.
:::

---

### 📌 **Kết Luận**
Workflow **"Tự Động Tạo Nội Dung Mạng Xã Hội Từ Telegram Với AI"** là **giải pháp hoàn hảo** cho các sếp:
✔ **Không cần code**.
✔ **Hoạt động 24/7**.
✔ **Tiết kiệm thời gian lên đồ content**.
✔ **Nội dung cá nhân hóa, hình ảnh AI sinh tạo**.

**Hành động ngay!**
1. **Chuẩn bị tài khoản** (Telegram, OpenAI, SerpAPI, Hugging Face).
2. **Import workflow** và cấu hình API.
3. **Test với tin nhắn mẫu** và bật chạy!

**Nếu gặp vấn đề**, liên hệ với tác giả **Onur** qua [LinkedIn](https://www.linkedin.com/in/onurdev/) hoặc comment dưới bài viết này.

---
**🚀 Cảm ơn các sếp đã đọc đến cuối!** Chúc các sếp **tự động hóa content** một cách hiệu quả! 🎉