---
title: "🤖 Bot Telegram Tự Động Tóm Tắt Bài Viết & Tạo Ảnh Bằng AI (OpenAI) - Cách Sử Dụng & Cài Đặt Chi Tiết"
description: "Tự động hóa hoàn toàn việc tóm tắt bài viết từ URL và tạo ảnh từ mô tả bằng AI (ChatGPT/DALL·E) thông qua Telegram Bot. Giúp các sếp tiết kiệm thời gian nghiên cứu, tăng hiệu suất làm việc và cá nhân hóa nội dung."
slug: "bot-telegram-tom-tat-bai-viet-tao-anh-ai-openai"
tags: [n8n, automation, ai, telegram-bot, openai, no-code, marketing, content-creation]
keywords: [tự động hóa telegram bot, tóm tắt bài viết bằng ai, tạo ảnh bằng ai, n8n workflow telegram, chatgpt tự động hóa, bot marketing ai]
---

# 🚀 **Bot Telegram Tự Động Tóm Tắt Bài Viết & Tạo Ảnh Bằng AI (ChatGPT/DALL·E) - Hướng Dẫn Cài Đặt & Sử Dụng**

### **🎯 Giải quyết vấn đề gì?**
Các sếp thường phải mất **thời gian quý báu** để:
- **Tìm kiếm và đọc** nhiều bài viết từ các nguồn khác nhau (blog, báo, website chuyên ngành).
- **Tóm tắt nội dung** dài để chia sẻ với đồng nghiệp hoặc chuẩn bị báo cáo.
- **Tạo hình ảnh minh họa** cho nội dung marketing, bài viết, hoặc dự án mà không có kỹ năng thiết kế.

**Workflow này tự động hóa toàn bộ quá trình bằng AI!** Chỉ cần gửi **URL bài viết** hoặc **mô tả ảnh** qua Telegram, bot sẽ:
✅ **Tóm tắt bài viết** thành văn bản ngắn gọn (sử dụng ChatGPT).
✅ **Tạo ảnh từ mô tả** (sử dụng DALL·E) và gửi kết quả ngay.
✅ **Hỗ trợ menu hướng dẫn** (`/help`) để các sếp biết cách sử dụng.

---
### **🎯 Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 50% thời gian** nghiên cứu và tóm tắt nội dung.
- **Cá nhân hóa nội dung** với tóm tắt ngắn gọn và ảnh minh họa chuyên nghiệp.
- **Hoạt động 24/7** mà không cần can thiệp thủ công.
- **Tích hợp AI** để nâng cao chất lượng nội dung.
- **Dễ dàng mở rộng** cho các chức năng khác (ví dụ: tổng hợp tin tức, tạo video script).
:::

---
### **🔧 Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Telegram** và **chatbot Telegram** (đã tạo và có **Webhook URL**).
2. **API Key OpenAI** (để sử dụng ChatGPT và DALL·E):
   - Mua tại [OpenAI Platform](https://platform.openai.com/) (gói miễn phí có giới hạn).
   - **Lưu ý**: API Key phải có **tiền nạp** (tối thiểu ~$5 USD) để hoạt động.
3. **n8n Self-hosted** (không dùng phiên bản cloud để đảm bảo bảo mật và ổn định):
   - 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%).
   - 👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172).

---
### **🚀 Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n.io/workflows/4392](https://n8n.io/workflows/4392) và import vào **n8n Editor**.
- **Cách 2**: Copy toàn bộ JSON từ link trên và dán vào **Import Workflow** trong n8n.

#### **2. Các bước cấu hình BẮT BUỘC phải chỉnh 📌**
Sau khi import, các sếp cần **cấu hình chi tiết** các node quan trọng:

##### **A. Cấu hình Telegram Webhook**
- Node: **"Trigger: Telegram Webhook"**
  - **Webhook URL**: Điền **URL Webhook** của bot Telegram (đã tạo trước).
  - **Token**: Điền **Token API** của bot (tìm trong `@BotFather` Telegram).
  - **Update**: Chọn **All Updates**.

##### **B. Cấu hình OpenAI API**
- Node: **"AI: Generate Article Summary"** và **"AI: Process Image Generation Request"**
  - **Credentials**: Chọn **"openAiApi"** (đã tạo trước trong n8n).
  - **API Key**: Điền **API Key OpenAI** (từ OpenAI Platform).
  - **Model**:
    - **Tóm tắt bài viết**: Chọn `gpt-3.5-turbo` (hoặc `gpt-4` nếu có).
    - **Tạo ảnh**: Chọn `dall-e-3` (hoặc `dall-e-2`).

##### **C. Cấu hình Command Routing**
- Node: **"Route: Check for Help Command"**, **"Route: Check for Summary Command"**, **"Route: Check for Image Command"**
  - **Condition**:
    - `/help` → Gửi menu hướng dẫn.
    - `/summary <URL>` → Tóm tắt bài viết.
    - `/img <prompt>` → Tạo ảnh từ mô tả.

##### **D. Cấu hình Fetch & Parse Article**
- Node: **"Fetch: Download Article Content"** và **"Parse: Extract Text from HTML"**
  - **URL**: Điền vào **URL** của bài viết (được truyền từ Telegram).
  - **Operation**: Chọn `extractHtmlContent` để trích xuất văn bản.

##### **E. Cấu hình AI Prompt (Tùy chọn nâng cao)**
- **Tóm tắt bài viết**: Các sếp có thể **cập nhật prompt** trong node OpenAI để điều chỉnh độ dài hoặc phong cách tóm tắt.
  - Ví dụ:
    ```json
    "prompt": "Tóm tắt bài viết này thành 3 câu ngắn gọn, tập trung vào điểm chính. Không bao gồm thông tin không liên quan."
    ```
- **Tạo ảnh**: Đảm bảo mô tả (`prompt`) trong `/img <prompt>` rõ ràng và cụ thể.

---
#### **3. Kích hoạt ⚡️**
- **Test Run**:
  - Gửi tin nhắn `/help` đến bot Telegram để kiểm tra menu.
  - Gửi `/summary https://example.com` để test tóm tắt.
  - Gửi `/img "a futuristic city with neon lights"` để test tạo ảnh.
- **Bật Active**: Sau khi test thành công, **bật workflow** trong n8n.

---
### **✍️ Mẹo & gợi ý nâng cao**
1. **Tích hợp Slack/Email**:
   - Thêm node **Slack** hoặc **Email** để gửi kết quả tóm tắt/ảnh đến nhóm hoặc cá nhân.
2. **Lưu log hoạt động**:
   - Sử dụng node **Sticky Note** hoặc **Google Sheets** để ghi lại lịch sử yêu cầu và kết quả.
3. **Cập nhật prompt AI**:
   - Tùy chỉnh prompt để phù hợp với ngành nghề (ví dụ: tóm tắt bài viết về marketing khác với y học).
4. **Tạo bot riêng cho từng nhóm**:
   - Mỗi nhóm có thể có **bot riêng** với các command khác nhau (ví dụ: `/report` để tổng hợp tin tức).
5. **Sử dụng Stability AI cho ảnh thực tế**:
   - Thay thế DALL·E bằng **Stability AI** (nếu muốn ảnh chất lượng cao hơn).

---
### **📌 Kết luận**
Workflow này là **công cụ mạnh mẽ** giúp các sếp tự động hóa việc **tóm tắt bài viết và tạo ảnh** chỉ bằng Telegram, tiết kiệm thời gian và nâng cao hiệu suất làm việc. **Không cần code**, chỉ cần **cấu hình vài bước** là có thể sử dụng ngay!

**🚀 Hành động ngay:**
1. **Cài đặt n8n Self-hosted** trên VPS (để đảm bảo bảo mật và ổn định).
2. **Import workflow** và cấu hình API Key.
3. **Test và bật hoạt động** để bắt đầu tự động hóa!

**Có thắc mắc?** Để lại comment bên dưới hoặc liên hệ với cộng đồng n8n tại [n8n Community](https://community.n8n.io/). 😊