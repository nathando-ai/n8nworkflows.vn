---
title: "🤖 **Tự Động Hóa Chatbot AI Multi-Mô Hình Telegram: GPT-4o + Custom Models + Google Sheets**"
description: "Workflow tự động hóa hoàn toàn không cần code giúp các sếp xây dựng chatbot Telegram thông minh hỗ trợ nhiều mô hình AI khác nhau (GPT-4o, mô hình tùy chỉnh) với giới hạn sử dụng hằng ngày và logging chi tiết trên Google Sheets. Giúp tiết kiệm thời gian, tăng trải nghiệm người dùng và quản lý hiệu quả API."
slug: "tay-dong-hoa-chatbot-ai-multi-model-telegram"
tags: [n8n, automation, ai-chatbot, telegram-bot, google-sheets, aimlapi, no-code]
keywords: [n8n workflow chatbot telegram, tự động hóa chatbot ai, multi-model ai, giới hạn sử dụng telegram, logging google sheets, ai/aimlapi]
---

# 🚀 **Chatbot AI Multi-Mô Hình Telegram: Từ Thông Tin Sang Trải Nghiệm**

Hiện nay, các sếp và doanh nghiệp thường phải mất nhiều thời gian để quản lý các yêu cầu từ khách hàng qua Telegram, đồng thời phải theo dõi sử dụng API và đảm bảo trải nghiệm người dùng ổn định. **Workflow này giải quyết tất cả những vấn đề đó bằng cách tự động hóa hoàn toàn một chatbot Telegram thông minh, hỗ trợ nhiều mô hình AI khác nhau (GPT-4o, mô hình tùy chỉnh) với giới hạn sử dụng hằng ngày và logging chi tiết.**

:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động 24/7 với hiệu suất tối ưu, các sếp nên cài đặt n8n trên **VPS riêng** (Self-hosted) với cấu hình ổn định. N8n chạy trên VPS sẽ đảm bảo tính liên tục và bảo mật cao hơn so với phiên bản cloud.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động trả lời hàng ngàn yêu cầu Telegram mà không cần can thiệp thủ công.
- **Hỗ trợ nhiều mô hình AI**: Người dùng có thể chọn giữa GPT-4o, mô hình tùy chỉnh hoặc các mô hình khác thông qua hashtag (#model_id).
- **Giới hạn sử dụng hằng ngày**: Đảm bảo không bị vượt quá ngân sách API và tránh bị chặn bởi nhà cung cấp.
- **Logging chi tiết**: Tất cả hoạt động được ghi lại trên Google Sheets, giúp theo dõi và phân tích hiệu suất.
- **Trải nghiệm người dùng cá nhân hóa**: Hỗ trợ lệnh `/models` để người dùng xem danh sách mô hình sẵn có và tương tác dễ dàng.
- **Hoạt động liên tục**: Workflow hoạt động 24/7 trên VPS, không phụ thuộc vào phiên bản cloud.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị các tài khoản và thông tin sau:

1. **Tài khoản Telegram Bot**:
   - Tạo bot qua [@BotFather](https://t.me/BotFather) và lấy **API Token**.
   - Bot cần quyền gửi tin nhắn và phản hồi trong chat.

2. **Google Sheets**:
   - Tạo một Google Sheet mới với tên **Sheet1** và các cột sau:
     ```
     user_id | date | query | result
     ```
   - Cung cấp quyền truy cập cho **Google Service Account** hoặc **OAuth email** trong n8n.

3. **API Key AI/ML API**:
   - Đăng ký tài khoản tại [AI/ML API](https://aimlapi.com/app) và lấy **API Key**.
   - Thông tin cấu hình:
     - Base URL: `https://api.aimlapi.com/v1`
     - API Key: `your_key_here`

4. **N8n Credentials**:
   - **Telegram API**: Thêm credential với API Token từ BotFather.
   - **Google Sheets OAuth2**: Thêm credential với quyền truy cập vào Google Sheet.
   - **AI/ML API**: Thêm credential với Base URL và API Key.

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### 1. **Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
- **Tải file JSON** từ [n8n.io/workflows/7045](https://n8n.io/workflows/7045) và nhấn **Import Workflow** trong n8n.
- **Hoặc copy/paste** JSON từ file vào **Create Workflow** > **Import JSON**.

#### 2. **Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflows này bao gồm **17 node** với các chức năng chính sau. Các sếp cần chú ý cấu hình các node sau:

##### **📩 Receive Telegram Message**
- **Credentials**: Chọn `telegramApi` đã tạo trước đó.
- **Lưu ý**: Đảm bảo bot Telegram đã được kích hoạt và có quyền gửi tin nhắn trong chat.

##### **📊 Fetch Usage Logs**
- **Credentials**: Chọn `googleSheetsOAuth2Api`.
- **Sheet Name**: Đảm bảo chọn **Sheet1** và tab chính là `Sheet1!A1:D`.
- **Lưu ý**: Nếu Google Sheet có nhiều tab, chọn tab chứa dữ liệu logging.

##### **🔢 Set Daily Limit**
- **Giá trị mặc định**: 5 (số lần sử dụng hằng ngày cho mỗi người dùng).
- **Lưu ý**: Các sếp có thể điều chỉnh giá trị này theo nhu cầu.

##### **🚦 Check Limit Exceeded?**
- Node này kiểm tra xem người dùng đã vượt quá giới hạn sử dụng hằng ngày hay chưa.
- **Lưu ý**: Nếu vượt quá, node sẽ chuyển sang **🚫 Notify: Limit Exceeded**.

##### **🧠 Generate Msg (AI/ML API | GPT-4o)**
- **Credentials**: Chọn `aimlApi`.
- **Model**: `openai/gpt-4o` (mặc định).
- **Prompt**: `={{ $('📩 Receive Telegram Message').item.json.message.text }}`
- **Lưu ý**: Đảm bảo API Key của AI/ML API được cấu hình chính xác.

##### **🧠 Generate Msg (AI/ML API | Custom Model)**
- **Credentials**: Chọn `aimlApi`.
- **Model**: `={{ $json.model_id }}` (tự động lấy từ hashtag `#model_id` trong tin nhắn).
- **Prompt**: `={{ $json.message }}`
- **Lưu ý**: Node này sẽ được kích hoạt khi người dùng chọn mô hình tùy chỉnh.

##### **📝 Log Successful Generation1**
- **Credentials**: Chọn `googleSheetsOAuth2Api`.
- **Operation**: `append` (thêm dữ liệu mới vào sheet).
- **Lưu ý**: Đảm bảo cột `user_id`, `date`, `query`, và `result` được định nghĩa chính xác.

##### **🔄 Get Models List**
- **Credentials**: Không cần (lấy danh sách mô hình từ API).
- **Lưu ý**: Node này sẽ trả về danh sách mô hình sẵn có từ AI/ML API.

##### **📝 Group Models By Providers**
- **Node Code**: Các sếp có thể xem và chỉnh sửa mã nguồn trong node này để nhóm mô hình theo nhà cung cấp (OpenAI, Groq, etc.).
- **Lưu ý**: Nếu cần thay đổi cách nhóm, mở node và chỉnh sửa mã.

##### **🔄 Set Custom Model?**
- Node này kiểm tra xem người dùng đã chọn mô hình tùy chỉnh hay không.
- **Lưu ý**: Nếu không chọn mô hình, workflow sẽ sử dụng mô hình mặc định (GPT-4o).

#### 3. **Kích hoạt ⚡️**
- **Test Run**: Nhấn **Execute Node** trên node **📩 Receive Telegram Message** và gửi tin nhắn mẫu như:
  ```
  #openai/gpt-4o Giải thích về blockchain.
  ```
  hoặc
  ```
  /models
  ```
  để kiểm tra tính năng.
- **Bật Active**: Sau khi test thành công, nhấn **Active** để workflow hoạt động liên tục.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Thêm lệnh hỗ trợ**:
   - Thêm lệnh `/help` để hướng dẫn người dùng cách sử dụng chatbot.
   - Thêm lệnh `/usage` để hiển thị số lần sử dụng còn lại trong ngày.

2. **Cá nhân hóa trải nghiệm**:
   - Thêm tính năng **inline buttons** để người dùng chọn mô hình một cách dễ dàng.
   - Hỗ trợ **shortcuts** (ví dụ: `#fast` = Groq model).

3. **Lọc nội dung NSFW**:
   - Thêm node **Code** để lọc và chặn nội dung không phù hợp.

4. **Báo cáo sử dụng định kỳ**:
   - Thêm node **Google Sheets** để tạo báo cáo tổng hợp sử dụng hàng tháng.

5. **Caching danh sách mô hình**:
   - Sử dụng node **Sticky Note** để lưu trữ danh sách mô hình và tránh gọi API liên tục.

---

### 📌 **Kết luận**
Workflow này là giải pháp hoàn hảo cho các sếp muốn tự động hóa chatbot Telegram với **hỗ trợ nhiều mô hình AI**, **giới hạn sử dụng hằng ngày** và **logging chi tiết**. Bằng cách sử dụng n8n trên VPS, các sếp có thể đảm bảo tính liên tục và bảo mật cao, đồng thời tiết kiệm thời gian và tăng trải nghiệm người dùng.

**Hãy áp dụng ngay workflow này và nâng cao hiệu suất công việc của mình!** 🚀

---
**📌 Lưu ý cuối cùng**:
- Đảm bảo **API Key** của AI/ML API không bị rò rỉ.
- Theo dõi **Google Sheets** để kiểm tra logging và điều chỉnh giới hạn sử dụng nếu cần.
- Nếu gặp vấn đề, hãy kiểm tra **n8n Logs** và **Google Sheets** để tìm nguyên nhân.