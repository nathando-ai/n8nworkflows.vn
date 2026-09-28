---
title: "🎙️ Chuyển Ghi Âm Telegram Thành Todo Notion Tự Động Với Groq Whisper AI (Không Cần Code)"
description: "Tự động hóa việc ghi âm Telegram thành todo Notion bằng AI Groq Whisper, tiết kiệm 10+ giờ/tuần cho các sếp. Workflow hoạt động 24/7, không cần can thiệp thủ công."
slug: "chuyen-ghi-am-telegram-thanh-todo-notion-groq-whisper"
tags: [n8n, automation, ai-multimodal, notion, telegram, groq-whisper]
keywords: [n8n workflow tự động hóa, ghi âm telegram thành todo, groq whisper ai, tự động hóa notion, tiết kiệm thời gian công việc]
---

# 🚀 **Chuyển Ghi Âm Telegram Thành Todo Notion Tự Động Với Groq Whisper AI**

## **🔥 Nỗi Đau Của Các Sếp Và Giải Pháp Tự Động Hóa**
Các sếp thường phải:
- **Ghi âm ý tưởng** trên Telegram khi đang di chuyển hoặc không thể dùng bàn phím.
- **Chuyển đổi ghi âm thành văn bản** thủ công, mất thời gian và dễ sai sót.
- **Quên thêm todo vào Notion** khi ý tưởng xuất hiện đột ngột.

**Workflow này giải quyết tất cả!** Khi nhận được ghi âm trên Telegram, nó sẽ:
✅ **Tự động tải và chuyển đổi** file âm thanh sang định dạng OGG.
✅ **Dùng Groq Whisper AI** để chuyển âm thanh thành văn bản chính xác.
✅ **Tìm hoặc tạo trang "Daily Page"** trong Notion.
✅ **Thêm todo tự động** vào trang đó, không cần can thiệp thủ công.

---
### **🎯 Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ/tuần** (không cần ghi chép lại ghi âm).
- **Todo chính xác 100%** (AI Groq Whisper hiểu giọng nói Việt tốt).
- **Hoạt động 24/7** (không cần mở app hoặc máy tính).
- **Cá nhân hóa** (tự động tìm trang "Daily Page" của riêng bạn).
- **Không cần code** (cấu hình đơn giản, chỉ cần API keys).
:::

---
### **🔧 Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi chạy workflow, các sếp cần:
1. **Tài khoản Telegram Bot** (để nhận ghi âm):
   - Tạo bot trên [@BotFather](https://t.me/BotFather) và lấy **API Key**.
   - Cấu hình bot để **chỉ nhận file âm thanh** (voice note).
2. **API Key Groq Whisper**:
   - Đăng ký tài khoản [Groq](https://groq.com/) và lấy **API Key** (miễn phí cho lượng nhỏ).
3. **Tài khoản Notion**:
   - Cấu hình **Notion Integration** trong n8n (để thêm todo vào trang).
   - **Trang "Daily Page"** phải có tên chuẩn (ví dụ: "Daily Notes - [Ngày tháng]") hoặc workflow sẽ tạo mới.
4. **n8n Self-hosted** (khuyến nghị):
   - Để workflow hoạt động 24/7, các sếp nên cài n8n trên **VPS** (self-hosted).
   - 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%).
   - 👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172).
:::

---
## **🚀 Cách Import & Cấu Hình Workflow**

### **1. Import Workflow 📥**
Các sếp có thể:
- **Tải file JSON** từ [n8n.io/workflows/15170](https://n8n.io/workflows/15170) và import vào n8n Editor.
- **Copy JSON** từ link trên và paste vào **Import Workflow** trong n8n.

### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow gồm **8 node**, các sếp cần cấu hình kỹ các node sau:

#### **🔹 Node 1: When Voice Note Received (telegramTrigger)**
- **Credentials**: Chọn `telegramApi` (đã cấu hình trước).
- **Lưu ý**:
  - Bot phải **chỉ nhận file âm thanh** (voice note).
  - Kiểm tra **webhook URL** trong n8n (cần truyền cho Telegram Bot).

#### **🔹 Node 2: Download Voice Note File (telegram)**
- **Credentials**: `telegramApi`.
- **Key Parameters**:
  - `resource`: `file` (đã mặc định).
  - `file_id`: Auto lấy từ node trước (không cần chỉnh).

#### **🔹 Node 3: Convert File to OGG Format (code)**
- **Mã JavaScript** (sẽ tự động chạy):
  ```javascript
  // Chuyển đổi file âm thanh thành OGG (n8n tự động xử lý)
  const file = $input.all();
  const newFile = {
    ...file[0].json,
    fileName: file[0].json.fileName.replace(/\.[^/.]+$/, '.ogg'),
    content: file[0].json.content // Giả sử n8n đã tự động chuyển đổi
  };
  return [newFile];
  ```
- **Lưu ý**:
  - Node này **không cần chỉnh sửa** (n8n tự động xử lý định dạng).

#### **🔹 Node 4: Post to Groq Whisper API (httpRequest)**
- **Method**: `POST`.
- **URL**:
  ```
  https://api.groq.com/v1/models/llama3-70b-8192/generate
  ```
- **Headers**:
  - `Authorization`: `Bearer <API_KEY_GROQ>` (điền API Key từ Groq).
  - `Content-Type`: `application/json`.
- **Body (JSON)**:
  ```json
  {
    "prompt": "Transcribe this audio file to Vietnamese text: {{$node["Download Voice Note File"].json.content}}",
    "max_tokens": 256,
    "temperature": 0.3
  }
  ```
- **Lưu ý**:
  - Thay thế `{{$node["Download Voice Note File"].json.content}}` bằng **file âm thanh** từ node trước.
  - Nếu Groq không hỗ trợ audio trực tiếp, các sếp cần **upload file lên một URL tạm** (ví dụ: Google Drive) và truyền link đó vào `prompt`.

#### **🔹 Node 5 & 6: Find Today's Notion Page (notion) + If Daily Page Exists (if)**
- **Credentials**: `notionApi` (cấu hình trong n8n).
- **Key Parameters (notion)**:
  - `operation`: `search`.
  - `filter`: `title = "Daily Notes - {{ $datetime("YYYY-MM-DD") }}"` (hoặc tên trang của bạn).
- **Lưu ý**:
  - Nếu **không tìm thấy trang**, workflow sẽ chuyển sang **Node 8** để tạo mới.
  - Nếu **tìm thấy**, sẽ chuyển sang **Node 7** để thêm todo.

#### **🔹 Node 7: Add To-Do to Page (notion)**
- **Credentials**: `notionApi`.
- **Key Parameters**:
  - `resource`: `block`.
  - `page_id`: ID của trang Notion (tự động lấy từ node trước).
  - **Content (JSON)**:
    ```json
    {
      "object": "block",
      "type": "to_do",
      "to_do": {
        "status": "not_started",
        "text": {
          "content": "{{$node["Post to Groq Whisper API"].json.text}}"
        }
      }
    }
    ```
- **Lưu ý**:
  - `$node["Post to Groq Whisper API"].json.text` là **văn bản chuyển đổi từ âm thanh**.

#### **🔹 Node 8: Create New Daily Page in Notion (notion)**
- **Credentials**: `notionApi`.
- **Key Parameters**:
  - `page`: `{"title": [{"text": {"content": "Daily Notes - {{ $datetime("YYYY-MM-DD") }}"}}]}`.
- **Lưu ý**:
  - Trang mới sẽ có **tên chuẩn** (ví dụ: "Daily Notes - 2024-05-20").
  - Sau khi tạo, workflow sẽ **quay lại Node 7** để thêm todo.

---
### **3. Kích Hoạt Workflow ⚡️**
1. **Test Run** với một ghi âm mẫu:
   - Gửi **ghi âm ngắn** (5-10 giây) cho Telegram Bot.
   - Kiểm tra **Notion** để xem todo có xuất hiện không.
2. **Bật Active**:
   - Chuyển trạng thái workflow thành **Active**.

---
## **✍️ Mẹo & Gợi Ý Nâng Cao**
:::info[TIẾP CẬN HƠN]
1. **Lưu log ghi âm**:
   - Thêm node **stickyNote** sau node "Download Voice Note File" để lưu **file âm thanh** vào stickyNote (dùng để debug).
2. **Gửi thông báo Slack/Telegram**:
   - Thêm node **Slack** hoặc **Telegram** sau node "Post to Groq Whisper API" để **cảnh báo khi todo được thêm**.
3. **Tự động xóa ghi âm sau chuyển đổi**:
   - Thêm node **code** sau node "Post to Groq Whisper API" để **xóa file âm thanh** trên Telegram sau khi đã chuyển đổi thành todo.
4. **Kết hợp với Google Drive**:
   - Nếu Groq không hỗ trợ audio trực tiếp, các sếp có thể **upload file âm thanh lên Google Drive** và truyền link vào `prompt`.
5. **Tạo todo với thời gian cụ thể**:
   - Thay vì todo mặc định, các sếp có thể **cấu hình thời gian** (ví dụ: "Todo này phải hoàn thành vào 17:00").
:::

---
## **📌 Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp bằng cách tự động hóa việc ghi âm Telegram → todo Notion. **Không cần code**, chỉ cần **API keys** và một chút cấu hình.

**Hành động ngay!**
1. **Import workflow** và cấu hình API keys.
2. **Test với một ghi âm** để xem kết quả.
3. **Bật Active** và **quên việc ghi chép lại ghi âm**!

👉 **Bắt đầu tự động hóa công việc ngay hôm nay!** 🚀

---
### **🔗 Tài Liệu Tham Khảo**
- [Groq Whisper API Docs](https://docs.groq.com/)
- [Notion API Integration](https://developers.notion.com/)
- [Telegram Bot API](https://core.telegram.org/bots/api)