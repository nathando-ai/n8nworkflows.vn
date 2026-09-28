---
title: "🤖 **Tự Động Hóa Chat AI Tự Động Trả Lời Lịch Sự Kiện Từ Google Sheets Trên Telegram - Không Cần Code!**"
description: "Tự động hóa chatbot AI trả lời các câu hỏi về lịch sự kiện từ Google Sheets ngay trên Telegram, tiết kiệm thời gian và cải thiện trải nghiệm khách hàng. Workflow này hoạt động 24/7, không cần can thiệp thủ công."
slug: "tieu-dong-hoa-chatbot-ai-lich-su-kien-google-sheets-telegram"
tags: [n8n, automation, ai-chatbot, google-sheets, telegram-bot, no-code, langchain]
keywords: [n8n workflow tự động hóa, chatbot AI trả lời lịch sự kiện, tự động hóa Telegram với Google Sheets, tự động hóa không code, AI chatbot cho doanh nghiệp, tự động trả lời câu hỏi từ bảng tính]
---

# 🚀 **Tự Động Hóa Chatbot AI Trả Lời Lịch Sự Kiện Từ Google Sheets Trên Telegram**

## **💡 Giải Pháp Cho Nỗi Đau Của Các Sếp**
Bạn có bao giờ phải trả lời hàng trăm câu hỏi về lịch sự kiện như *"Lịch trình sự kiện ngày mai là gì?"* hay *"Sự kiện nào sắp diễn ra vào tháng này?"* từ khách hàng, đồng nghiệp hoặc team nội bộ? Thì đây là giải pháp **tự động hóa hoàn toàn** giúp bạn:
- **Tiết kiệm thời gian** lên đến 80% trong việc trả lời các câu hỏi liên quan đến lịch sự kiện.
- **Cải thiện trải nghiệm khách hàng** với phản hồi tức thời, chính xác và cá nhân hóa.
- **Hoạt động 24/7** mà không cần can thiệp thủ công.
- **Cập nhật tự động** khi lịch sự kiện thay đổi trên Google Sheets.

Không cần viết một dòng code nào, chỉ cần **import workflow này vào n8n** và kết nối với Telegram + Google Sheets là xong!

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động **ổn định 24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên một VPS chuyên dụng. Dưới đây là các gói VPS ưu đãi dành riêng cho n8n:

👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (Đảm bảo tốc độ cao, phù hợp cho AI)

Ngoài ra, các sếp cũng có thể **cài n8n trên máy chủ riêng** (AWS, DigitalOcean, Linode) nếu có nhu cầu cao.
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Trả lời tự động** tất cả các câu hỏi về lịch sự kiện từ Telegram (ví dụ: *"Sự kiện nào sắp diễn ra?"*, *"Lịch trình ngày 15/10 là gì?"*).
✅ **Cập nhật tức thời** khi lịch sự kiện thay đổi trên Google Sheets.
✅ **Trải nghiệm người dùng cao** với phản hồi nhanh chóng và chính xác.
✅ **Tiết kiệm chi phí** so với việc thuê nhân viên hỗ trợ 24/7.
✅ **Dễ dàng mở rộng** cho nhiều sự kiện khác nhau.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Telegram Bot**:
   - Tạo bot Telegram bằng cách gửi tin nhắn cho `@BotFather` và lấy **API Token**.
   - Cài đặt bot vào nhóm hoặc chat cá nhân để test.

2. **Google Sheets OAuth 2.0**:
   - Tạo một **Google Cloud Project** và bật **Google Sheets API**.
   - Tạo một **Service Account** và tải xuống **JSON Key File**.
   - Chia sẻ bảng Google Sheets với **Service Account** để bot có quyền đọc.

3. **OpenRouter API Key** (hoặc API LLM khác):
   - Đăng ký tài khoản trên [OpenRouter](https://openrouter.ai/) và lấy **API Key**.
   - *(Lưu ý: Nếu không muốn dùng OpenRouter, có thể thay thế bằng các API LLM khác như Mistral, Groq, hoặc Anthropic.)*

4. **Bảng Google Sheets chuẩn bị**:
   - Bảng phải có **cột tên sự kiện, ngày giờ, mô tả, và link** (cấu trúc mẫu sẽ được hướng dẫn sau).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ **file JSON** hoặc **copy/paste JSON** vào n8n Editor.

**Bước 1: Tải workflow từ n8n.io**
- Truy cập [link workflow gốc](https://n8n.io/workflows/2937) và nhấn **"Export"** để tải file JSON.

**Bước 2: Import vào n8n**
- Mở **n8n Editor** (trên web hoặc self-hosted).
- Nhấn **"Import"** và chọn file JSON vừa tải.
- Hoặc **copy toàn bộ JSON** và dán vào **"Import from JSON"** trong n8n.

---

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**

##### **A. Cấu Hình Telegram Bot**
1. **Node `telegramTrigger` (tên: `telegramInput`)**:
   - Điền **API Token** từ `@BotFather` vào `telegramApi`.
   - Chọn **chat ID** của bot (có thể lấy từ [@userinfobot](https://t.me/userinfobot)).

2. **Node `telegram` (tên: `SendTyping` và `telegramResponse`)**:
   - Sử dụng cùng **credentials `telegramApi`** như trên.

##### **B. Cấu Hình Google Sheets**
1. **Node `googleSheets` (tên: `Schedule`)**:
   - Chọn **credentials `googleSheetsOAuth2Api`** và tải lên **JSON Key File** từ Google Cloud.
   - Chọn **bảng Google Sheets** và **sheet name** (ví dụ: `"Lịch Sự Kiện"`).
   - Chọn **query** để lấy dữ liệu (mẫu query sẽ được hướng dẫn sau).

2. **Cấu trúc bảng Google Sheets**:
   Bảng phải có **các cột sau** (có thể thêm cột khác):
   | Tên Sự Kiện | Ngày Thời Gian | Mô Tả | Link | Loại Sự Kiện |
   |-------------|----------------|--------|------|--------------|
   | Học viện AI | 15/10/2024 | Khóa học AI cơ bản | [link] | Online |
   | Hội nghị Doanh nghiệp | 20/10/2024 | Hội nghị năm 2024 | [link] | Offline |

   *(Lưu ý: Cột `Ngày Thời Gian` nên định dạng là **ISO 8601** để LLM xử lý dễ dàng.)*

##### **C. Cấu Hình LLM (OpenRouter)**
1. **Node `lmChatOpenRouter` (tên: `LLM`)**:
   - Điền **API Key** từ OpenRouter vào `openRouterApi`.
   - Chọn **model** (ví dụ: `mistral-tiny`, `openrouter/mistral-7b-instruct-v0.1`).
   - Cấu hình **prompt** để LLM trả lời dựa trên lịch sự kiện:
     ```json
     {
       "model": "openrouter/mistral-7b-instruct-v0.1",
       "messages": [
         {
           "role": "system",
           "content": "Bạn là một trợ lý ảo chuyên trả lời về lịch sự kiện. Dữ liệu lịch sự kiện được cung cấp dưới dạng bảng Markdown. Hãy trả lời ngắn gọn, chính xác và thân thiện."
         },
         {
           "role": "user",
           "content": "{{ $node["ScheduleToMarkdown"].json["markdown"] }}"
         },
         {
           "role": "user",
           "content": "{{ $node["telegramInput"].json["message"]["text"] }}"
         }
       ],
       "temperature": 0.7,
       "max_tokens": 500
     }
     ```

##### **D. Cấu Hình Node `ScheduleToMarkdown` (Code)**
- Node này chuyển dữ liệu từ Google Sheets thành **bảng Markdown** để LLM dễ dàng xử lý.
- Mở node `ScheduleToMarkdown` và chỉnh sửa code như sau:
  ```javascript
  // Chuyển dữ liệu từ Google Sheets thành Markdown
  const rows = $input.all();
  let markdown = "| Tên Sự Kiện | Ngày Thời Gian | Mô Tả |\n|-------------|----------------|--------|\n";

  rows.forEach(row => {
    markdown += `| ${row["Tên Sự Kiện"]} | ${row["Ngày Thời Gian"]} | ${row["Mô Tả"]} |\n`;
  });

  return { markdown: markdown };
  ```

##### **E. Cấu Hình Node `Switch` (Chọn kênh trả lời)**
- Node này quyết định trả lời trên **Telegram** hay **n8n Editor** (dùng để debug).
- Chỉnh sửa điều kiện trong `Switch` để **luôn trả lời trên Telegram**:
  ```json
  {
    "condition": "true",
    "branch": "telegramResponse"
  }
  ```

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run với dữ liệu mẫu**:
   - Gửi tin nhắn từ Telegram đến bot (ví dụ: *"Lịch trình ngày mai là gì?"*).
   - Kiểm tra phản hồi của LLM và điều chỉnh **prompt** nếu cần.

2. **Bật Active workflow**:
   - Nhấn **"Active"** trên n8n Editor để workflow chạy liên tục.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**

#### **1. Cập Nhật Lịch Sự Kiện Tự Động**
- Sử dụng **Google Sheets Webhook** để cập nhật dữ liệu khi có thay đổi (ví dụ: sử dụng **Zapier** hoặc **Make** để gửi dữ liệu về Google Sheets).
- Hoặc **cài đặt cron job** để refresh dữ liệu định kỳ (ví dụ: mỗi 6 giờ).

#### **2. Gửi Báo Cáo Định Kỳ**
- Thêm **node `telegram`** để gửi **báo cáo tổng hợp** về lịch sự kiện hàng tuần/month.
- Ví dụ: *"Đây là danh sách sự kiện sắp diễn ra trong tháng 11/2024:"* + bảng Markdown.

#### **3. Kết Nối Với Slack**
- Thay thế node `telegramResponse` bằng **node `slack`** để chatbot hoạt động trên Slack.
- Cấu hình **credentials Slack API** và chọn **channel** để gửi tin nhắn.

#### **4. Lưu Log Cho Debug**
- Thêm **node `stickyNote`** để lưu lại **tất cả các câu hỏi và phản hồi** của chatbot.
- Dễ dàng theo dõi và cải thiện chất lượng trả lời.

#### **5. Sử Dụng Model LLM Khác**
- Nếu OpenRouter không phù hợp, thay thế bằng **Mistral, Groq, hoặc Anthropic** bằng cách chỉnh sửa node `lmChatOpenRouter`.

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** để tự động hóa việc trả lời các câu hỏi về lịch sự kiện trên Telegram, giúp các sếp **tiết kiệm thời gian, cải thiện trải nghiệm khách hàng** và **tăng cường hiệu suất công việc**.

**Hành động ngay hôm nay!**
1. **Import workflow** vào n8n.
2. **Cấu hình Telegram + Google Sheets + OpenRouter**.
3. **Test và bật Active** để chatbot hoạt động 24/7.

Nếu có bất kỳ vấn đề nào trong quá trình setup, các sếp có thể **đăng câu hỏi trên [Community n8n](https://community.n8n.io/)** hoặc liên hệ với tác giả **Daniel Nolde** qua [GitHub](https://github.com/daniel-nolde).

**🚀 Chúc các sếp thành công với tự động hóa AI này!**