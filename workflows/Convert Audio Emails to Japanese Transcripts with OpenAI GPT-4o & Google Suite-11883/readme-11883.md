---
title: "🎤 **Tự Động Chuyển Email Giọng Nhật Bản Sang Bản Tóm Tắt Nhật Văn Với OpenAI GPT-4o & Google Suite**"
description: "Workflow tự động hóa nhận email có file âm thanh, chuyển đổi thành bản phiên âm chính xác tiếng Nhật và tóm tắt AI theo định dạng Markdown, lưu trữ trên Google Drive, ghi log vào Google Sheets và thông báo qua Gmail/Slack - hoàn toàn không cần code!"
slug: "tich-hop-email-nhat-ban-sang-ban-tom-tat-nhat-van"
tags: [n8n, automation, no-code, ai-summarization, google-drive, openai, gmail, slack]
keywords: [tự động hóa email âm thanh, phiên âm tiếng Nhật, OpenAI GPT-4o, Google Drive tự động, tóm tắt AI, Google Sheets log, workflow n8n]
---

# 🚀 **Tự Động Chuyển Email Giọng Nhật Bản Sang Bản Tóm Tắt Nhật Văn Với AI**

### **Giải pháp hoàn hảo cho các sếp nhận email âm thanh, cuộc họp ghi âm, hoặc ghi chú giọng nói từ đồng nghiệp Nhật Bản!**
Hết phải nghe lại file âm thanh dài dòng, mất thời gian phiên âm thủ công, hoặc quên ghi chép nội dung quan trọng. **Workflow này tự động:**
- **Phiên âm chính xác** tất cả nội dung tiếng Nhật trong file âm thanh (MP3/WAV/M4A).
- **Tóm tắt AI** theo định dạng **Markdown** (có thể chuyển sang PDF, Word) với cấu trúc rõ ràng: **Tiêu đề, Điểm chính, Quyết định, và Nhiệm vụ hành động**.
- **Lưu trữ tự động** trên Google Drive với cấu trúc thư mục `Năm/Tháng` để dễ quản lý.
- **Ghi log** tất cả phiên âm và tóm tắt vào Google Sheets để theo dõi lịch sử.
- **Thông báo ngay** kết quả qua **Gmail** (gửi lại cho người gửi) và **Slack** (để toàn bộ team cập nhật).

---
## 🎯 **Kết quả các sếp nhận được**
:::tip[**3 Lợi ích Cốt Lõi**]
✅ **Tiết kiệm 10+ giờ/tuần** không phải nghe lại và phiên âm thủ công.
✅ **Chính xác 100%** với phiên âm AI (GPT-4o) và tóm tắt logic theo yêu cầu.
✅ **Cá nhân hóa & chuyên nghiệp** với định dạng Markdown sẵn sàng chia sẻ hoặc xuất bản.
:::

---
## 🔧 **Yêu cầu cần thiết**
:::info[**CHUẨN BỊ TRƯỚC KHI BẮT ĐẦU**]
- **Tài khoản Gmail** (có quyền truy cập vào hộp thư nhận email âm thanh).
- **Google Drive & Google Sheets** (để lưu trữ và ghi log).
- **Slack Workspace** (để thông báo kết quả).
- **OpenAI API Key** (để phiên âm và tóm tắt AI).
- **File âm thanh** (MP3, WAV, M4A, OGG) được gửi qua email.
:::

---
## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
- **Cách 1:** Tải file JSON từ [n8n.io/workflows/11883](https://n8n.io/workflows/11883) và import vào **n8n Editor**.
- **Cách 2:** Copy toàn bộ JSON từ link trên và dán vào **Import Workflow** trong n8n.

### **2. Các lưu ý BẮT BUỘC phải chỉnh 📌**
Workflow gồm **20 node** với các bước logic rõ ràng. Dưới đây là **các node quan trọng cần cấu hình**:

#### **📌 Node 1: New Gmail with Audio (gmailTrigger)**
- **Cấu hình:**
  - Chọn **Gmail account** (nếu có nhiều tài khoản, chọn tài khoản chính).
  - **Label:** Đặt tên cho label mới (ví dụ: `email-am-thanh`).
  - **Attachments:** Chọn **Only files** và **Audio files** (MP3, WAV, M4A, OGG).
  - **Polling Interval:** 60 giây (để kịp thời nhận email mới).

#### **📌 Node 2: Filter (filter)**
- **Cấu hình:**
  - **Regex:** `mp3|wav|m4a|ogg` (đảm bảo chỉ giữ lại file âm thanh).
  - **Nếu muốn chỉ lấy email từ người gửi cụ thể**, thêm điều kiện trong **New Gmail with Audio** (ví dụ: `from:team@company.com`).

#### **📌 Node 3: Generate Year-Month Folder Path (code)**
- **Cấu hình:**
  - **Script JavaScript:** Đã sẵn sàng, không cần chỉnh (tạo thư mục theo định dạng `Năm/Tháng`).
  - **Nếu muốn thay đổi cấu trúc**, mở node này và chỉnh `YYYY/MM` thành `YYYY/MM/DD` hoặc `Tháng/Năm`.

#### **📌 Node 4: HTTP Request (httpRequest) → OpenAI Audio Transcription**
- **Cấu hình:**
  - **URL:** `https://api.openai.com/v1/audio/transcriptions`
  - **Headers:**
    - `Authorization: Bearer {API_KEY}` (điền API Key OpenAI của bạn).
    - `Content-Type: multipart/form-data`.
  - **Body:**
    - `file`: Chọn file âm thanh từ node trước.
    - `model`: `gpt-4o` (hoặc `whisper-1` nếu muốn phiên âm miễn phí).
    - `response_format`: `text` (để trả về văn bản).
    - `language`: `ja` (tiếng Nhật).
  - **Lưu ý:** Nếu không có API Key, [đăng ký tại OpenAI](https://platform.openai.com/account/api-keys) và cài đặt.

#### **📌 Node 5: Generate AI Summary (openAi)**
- **Cấu hình:**
  - **Model:** `gpt-4o` (hoặc `gpt-4`).
  - **Prompt:** Đã sẵn sàng, nhưng bạn có thể chỉnh sửa để phù hợp với yêu cầu tóm tắt của công ty (ví dụ: thêm yêu cầu về định dạng JSON cụ thể).
  - **Example:**
    ```json
    {
      "title": "Tóm tắt cuộc họp ngày {date}",
      "points": ["Điểm 1", "Điểm 2"],
      "decisions": ["Quyết định 1", "Quyết định 2"],
      "actionItems": ["Nhiệm vụ 1", "Nhiệm vụ 2"]
    }
    ```

#### **📌 Node 6: Edit Fields (set)**
- **Cấu hình:**
  - **Chuyển JSON thành Markdown:** Sử dụng hàm `JSON.stringify()` và thêm syntax Markdown (ví dụ: `# Tiêu đề`, `- Điểm 1`).
  - **Example:**
    ```javascript
    {
      summaryContent: `# Tóm tắt cuộc họp\n\n**Tiêu đề:** ${json.title}\n\n**Điểm chính:**\n${json.points.map(p => `- ${p}`).join('\n')}\n\n**Quyết định:**\n${json.decisions.map(d => `- ${d}`).join('\n')}\n\n**Nhiệm vụ:**\n${json.actionItems.map(a => `- ${a}`).join('\n')}`
    }
    ```

#### **📌 Node 7: Google Drive (googleDrive)**
- **Cấu hình:**
  - **Parent Folder:** Chọn **thư mục cha** trên Google Drive (ví dụ: `Tự động hóa Email`).
  - **File Name:** Sử dụng `{{ $node["Generate Year-Month Folder Path"].json["folderPath"] }}/{{ $node["New Gmail with Audio"].json["subject"] }}_transcript.txt` (để tự động đặt tên theo email).
  - **Mime Type:** `text/plain` (cho file TXT) và `text/markdown` (cho file MD).

#### **📌 Node 8: Share Transcript File (googleDrive)**
- **Cấu hình:**
  - **Share Type:** `anyone` (hoặc `user` nếu chỉ muốn chia sẻ cho người dùng cụ thể).
  - **Permission:** `viewer` (để người khác xem mà không chỉnh sửa).

#### **📌 Node 9: Log to Google Sheets (googleSheets)**
- **Cấu hình:**
  - **Sheet Name:** Chọn bảng Google Sheets cần ghi log.
  - **Range:** `A1` (để ghi từ ô A1).
  - **Data:** Đảm bảo node **Prepare Sheets Data** (code) đã chuẩn bị dữ liệu dưới dạng JSON:
    ```json
    {
      "subject": "{{ $node["New Gmail with Audio"].json["subject"] }}",
      "fileName": "{{ $node["Upload Transcript to Drive"].json["name"] }}",
      "transcript": "{{ $node["Convert Transcript to TXT"].json["text"] }}",
      "summary": "{{ $node["Convert Summary to MD"].json["text"] }}",
      "driveLink": "{{ $node["Share Transcript File"].json["webViewLink"] }}"
    }
    ```

#### **📌 Node 10: Send Slack Notification (slack)**
- **Cấu hình:**
  - **Workspace URL:** `https://slack.com/api/chat.postMessage` (đăng nhập Slack và lấy URL từ **Apps > Custom Integrations**).
  - **Channel:** `#tự-động-hoá` (hoặc channel khác).
  - **Message:** Sử dụng template:
    ```json
    {
      "text": `📤 **Tóm tắt email âm thanh mới**\n\n**Tiêu đề:** ${json.subject}\n**Link file:** ${json.driveLink}\n**Tóm tắt:** ${json.summary}`,
      "blocks": [
        {
          "type": "section",
          "text": {
            "type": "mrkdwn",
            "text": `*Tóm tắt email âm thanh:* ${json.subject}`
          }
        },
        {
          "type": "actions",
          "elements": [
            {
              "type": "button",
              "text": {
                "type": "plain_text",
                "text": "Xem file"
              },
              "url": "${json.driveLink}"
            }
          ]
        }
      ]
    }
    ```

---
### **3. Kích hoạt ⚡️**
- **Test Run:** Chọn **Run Once** và gửi một email âm thanh mẫu để kiểm tra.
- **Active Workflow:** Sau khi kiểm tra thành công, bật **Active** để workflow chạy 24/7.

---
## ✍️ **Mẹo & gợi ý nâng cao**
:::info[**CÁCH LÀM NÀY ĐỂ TIẾP CẬN HƠN**]
- **Kết hợp với Google Calendar:** Sử dụng node **HTTP Request** để tự động tạo sự kiện từ tóm tắt (ví dụ: nhắc nhở nhiệm vụ hành động).
- **Lưu log vào BigQuery:** Nếu công ty dùng BigQuery, thay thế node **googleSheets** bằng **HTTP Request** để đẩy dữ liệu vào BigQuery.
- **Thông báo qua Email Template:** Sử dụng **gmail** với **HTML template** để gửi email có định dạng chuyên nghiệp hơn.
- **Phân loại email:** Thêm node **filter** sau **New Gmail with Audio** để chỉ xử lý email từ người gửi cụ thể (ví dụ: `team@company.com`).
- **Tự động xóa email sau xử lý:** Thêm node **gmail** với action `delete` để xóa email sau khi đã xử lý.
:::

---
## 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc thủ công, đồng thời **tăng cường hiệu quả** với phiên âm và tóm tắt AI chính xác. **Đừng bỏ lỡ cơ hội tự động hóa quá trình này ngay hôm nay!**

### **🔥 BƯỚC TIẾP THEO:**
1. **Cài đặt n8n Self-hosted** trên VPS để workflow chạy ổn định 24/7.
   👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%).
2. **Import workflow** và cấu hình các node theo hướng dẫn trên.
3. **Test với email mẫu** và bật **Active** để bắt đầu tự động hóa!

**Chia sẻ workflow này với đồng nghiệp nếu bạn thấy hữu ích!** 🚀