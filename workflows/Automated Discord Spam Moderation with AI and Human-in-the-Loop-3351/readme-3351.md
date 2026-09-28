---
title: "🛡️ Tự Động Hóa Phân Loại & Xử Lý Spam Trên Discord Với AI + Con Người (Human-in-the-Loop)"
description: "Workflow tự động hóa 100% không code để phát hiện và xử lý spam trên Discord bằng AI + hệ thống phản hồi từ người quản trị, giảm thiểu thời gian và tối ưu hóa trải nghiệm cộng đồng."
slug: "tieu-dong-hoa-phan-loai-spam-discord-ai-human-loop"
tags: [n8n, automation, discord, ai, human-in-the-loop, spam-filtering]
keywords: [n8n workflow discord, tự động hóa quản trị discord, phân loại spam bằng AI, human-in-the-loop n8n, tự động xóa tin nhắn spam]
---

# 🚀 **Tự Động Hóa Phân Loại & Xử Lý Spam Trên Discord Với AI + Con Người (Human-in-the-Loop)**

### **Giải pháp hoàn hảo cho cộng đồng Discord bị spam quấy rối**
Các sếp đang gặp phải tình trạng **spam, tin nhắn quảng cáo không mong muốn** làm xáo trộn trải nghiệm người dùng trên Discord? Hay phải **tốn thời gian kiểm tra thủ công** hàng trăm tin nhắn mỗi ngày? Workflow này sẽ **tự động phát hiện, cảnh báo và xử lý spam** bằng AI + sự can thiệp của người quản trị, giúp **giảm thiểu 90% công việc thủ công** và duy trì môi trường cộng đồng sạch sẽ.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động phát hiện spam** bằng AI (OpenAI GPT-3.5) với độ chính xác cao.
- **Cảnh báo người quản trị** thông qua Discord với **form dropdown** để chọn hành động xử lý (xóa, cảnh báo, bỏ qua...).
- **Xử lý bulk** tin nhắn spam trên nhiều kênh đồng thời.
- **Không bị chặn** bởi Discord (do sử dụng bot API chính thức).
- **Tiết kiệm thời gian** từ 5-10 giờ/ngày cho đội ngũ quản trị.
- **Cá nhân hóa phản hồi** cho từng người dùng (tránh cảnh báo sai).
:::

---

## 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Discord Bot**:
   - Bot phải có quyền `View Channels`, `Send Messages`, và `Manage Messages` trong các kênh cần giám sát.
   - [Hướng dẫn tạo bot Discord](https://support.discord.com/hc/en-us/articles/228383668-Intro-to-Bots).
   - **Credentials**: `discordBotApi` (điền `Token` của bot vào n8n).

2. **API Key OpenAI**:
   - Đăng ký tại [OpenAI](https://platform.openai.com/) và lấy `API Key`.
   - **Credentials**: `openAiApi` (điền `API Key` vào n8n).

3. **Kênh Discord dành cho quản trị**:
   - Tạo 1 kênh riêng để nhận thông báo từ bot (ví dụ: `#spam-reports`).

4. **Mô hình AI (LLM) OpenAI**:
   - Workflow sử dụng mô hình `o3-mini` (miễn phí). Nếu muốn nâng cao độ chính xác, có thể thay thế bằng `gpt-4` (có phí).

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/3351) hoặc copy toàn bộ JSON từ đây.
- Mở **n8n Editor** → Nhấn `Import` → Dán JSON → Chọn `Import`.

:::note[Lưu ý]
- **Không chỉnh sửa cấu trúc** của workflow trừ khi hiểu rõ logic.
- **Không xóa node** `Schedule Trigger` (nút bấm đỏ) nếu muốn chạy tự động hàng giờ.
:::

---

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**

#### **A. Cấu hình Discord Bot**
1. **Node `Get Recent Messages`**:
   - Điền `Channel ID` của kênh cần giám sát (tìm ID kênh bằng cách mở URL kênh và lấy số sau `channels/`).
   - Thiết lập `Limit` (số tin nhắn lấy mỗi lần chạy, ví dụ: `50`).

2. **Node `Warn User` và `Warn User Only`**:
   - Chọn `Channel ID` để gửi cảnh báo (có thể là kênh riêng hoặc kênh chung).
   - **Thêm biến động态**:
     ```json
     "content": "Tin nhắn của bạn đã bị nghi ngờ là spam. Vui lòng kiểm tra lại nội dung!"
     ```

3. **Node `Notify Moderators with Send & Wait`**:
   - Chọn kênh quản trị (ví dụ: `#spam-reports`).
   - **Tạo form dropdown** cho người quản trị chọn hành động:
     ```json
     "components": [
       {
         "type": "action_row",
         "components": [
           {
             "type": "select_menu",
             "placeholder": "Chọn hành động",
             "options": [
               {"value": "delete", "label": "Xóa tin nhắn"},
               {"value": "warn", "label": "Cảnh báo người dùng"},
               {"value": "ignore", "label": "Bỏ qua"}
             ]
           }
         ]
       }
     ]
     ```

#### **B. Cấu hình AI Spam Detection**
1. **Node `Spam Detection` (Text Classifier)**:
   - **Prompt mẫu** (có thể tùy chỉnh):
     ```plaintext
     Bạn là một chuyên gia phân loại spam. Hãy đánh giá tin nhắn sau và trả lời YES/NOT_SPAM:
     Tin nhắn: "{{$json.message.content}}"
     ```
   - **Mô hình**: Chọn `o3-mini` (miễn phí) hoặc `gpt-4` (nâng cao độ chính xác).

2. **Node `Model` (OpenAI Chat)**:
   - Đảm bảo `openAiApi` được cấu hình đúng trong `Credentials`.

#### **C. Cấu hình Subworkflow (Human-in-the-Loop)**
1. **Node `Moderation Subworkflow`**:
   - **Không cần chỉnh sửa** trừ khi muốn thêm logic mới.
   - **Lưu ý**: Nếu tắt `Wait for Subworkflow Completion`, workflow sẽ không bị chặn khi chờ phản hồi từ người quản trị.

#### **D. Cấu hình Lọc & Xóa Spam**
1. **Node `Spam Messages Only` (Filter)**:
   - Chọn `Flagged as Spam` (đã được AI phân loại).

2. **Node `Delete Messages`**:
   - Điền `Message IDs` từ node `Get Message IDs` (sử dụng biến động态 `$json.messageIds`).

---

### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Nhấn `Execute Workflow` → Chọn `Test` → Chọn `Run Once`.
   - Kiểm tra kết quả trên Discord (cảnh báo spam và phản hồi từ người quản trị).

2. **Bật Active**:
   - Sau khi kiểm tra thành công, nhấn `Active` để workflow chạy tự động.

---

## ✍️ **Mẹo & gợi ý nâng cao**

### **1. Tăng độ chính xác AI**
- **Tùy chỉnh prompt** cho node `Spam Detection` để phù hợp với cộng đồng của bạn:
  ```plaintext
  Nếu tin nhắn chứa từ khóa "đăng ký", "mua hàng", "click link" hoặc có nhiều liên kết, trả lời YES.
  ```
- **Sử dụng mô hình GPT-4** (nếu có ngân sách) để giảm sai sót.

### **2. Log & Báo cáo tự động**
- Thêm node **Google Sheets** hoặc **Notion** để lưu lịch sử spam:
  ```json
  {
    "name": "Log to Google Sheets",
    "type": "googleSheets",
    "credentials": ["googleSheetsApi"],
    "keyParameters": {
      "operation": "createRow",
      "sheetName": "Spam_Logs",
      "data": {
        "User": "{{$json.user.id}}",
        "Message": "{{$json.message.content}}",
        "Action": "{{$json.action}}",
        "Timestamp": "{{$json.timestamp}}"
      }
    }
  }
  ```

### **3. Gửi báo cáo định kỳ cho admin**
- Sử dụng **node `Schedule Trigger`** để chạy hàng ngày và gửi tổng hợp spam qua Discord:
  ```json
  {
    "name": "Daily Spam Report",
    "type": "discord",
    "keyParameters": {
      "operation": "sendAndWait",
      "resource": "message",
      "content": "Tổng hợp spam trong ngày: {{$json.totalSpam}} tin nhắn",
      "channelId": "CHANNEL_ID_ADMIN"
    }
  }
  ```

### **4. Kết hợp với Telegram/Email**
- Thay thế node Discord bằng **Telegram Bot** hoặc **Email** để cảnh báo quản trị:
  ```json
  {
    "name": "Notify via Email",
    "type": "email",
    "credentials": ["emailApi"],
    "keyParameters": {
      "to": "admin@example.com",
      "subject": "Spam Detected in Discord",
      "html": "<p>Tin nhắn spam từ: <b>{{$json.user.username}}</b></p>"
    }
  }
  ```

---

## 📌 **Kết luận**
Workflow này **giải phóng đội ngũ quản trị** khỏi công việc lặp lại, đồng thời **giảm thiểu spam** bằng AI + sự can thiệp của con người. **Áp dụng ngay** để:
✅ **Tiết kiệm 5-10 giờ/ngày** cho quản trị viên.
✅ **Tăng trải nghiệm người dùng** với môi trường Discord sạch sẽ.
✅ **Tự động hóa 100%** không cần viết code.

**Bắt đầu ngay** bằng cách import workflow và cấu hình theo hướng dẫn trên! Nếu gặp vấn đề, tham gia **community n8n** để hỗ trợ:
🔗 [Discord n8n](https://discord.com/invite/XPKeKXeB7d) | [Forum n8n](https://community.n8n.io/)

---
**🚀 Cần hỗ trợ cài đặt VPS cho n8n?** Liên hệ ngay với TinoHost qua [đây](https://tino.vn/vps-n8n?affid=388) để được tư vấn miễn phí!