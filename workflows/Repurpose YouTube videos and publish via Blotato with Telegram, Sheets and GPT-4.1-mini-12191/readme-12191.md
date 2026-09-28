---
title: "🎥 Tự Động Hóa Chuyển Đổi Video YouTube → Blog + Telegram + GPT-4.1-mini (Không Cần Code)"
description: "Workflow tự động hóa chuyển đổi video YouTube thành bài viết blog trên Blotato, đồng thời gửi thông báo Telegram và lưu log vào Google Sheets - tiết kiệm 80% thời gian biên tập nội dung."
slug: "tieu-dong-hoa-chuyen-doi-video-youtube-den-blog"
tags: [n8n, automation, content-creation, multimodal-ai, youtube, blotato, telegram, google-sheets, openai]
keywords: [n8n workflow youtube, tự động hóa nội dung, chuyển đổi video thành bài viết, blotato api, gpt-4.1-mini, google sheets tự động]
---

# 🚀 **Tự Động Hóa Chuyển Đổi Video YouTube → Blog + Telegram + GPT-4.1-mini (Không Cần Code)**

## **💡 Giải Pháp Cho Người Sáng Tạo Nội Dung & Doanh Nghiệp**
Bạn đã bao giờ phải **chuyển đổi video YouTube thành bài viết blog** để tối ưu SEO, chia sẻ trên mạng xã hội hoặc lưu trữ nội dung? Hoặc phải **quét hàng chục video** để tạo script, mô tả SEO và bài viết chi tiết? Với workflow này, **các sếp** có thể:
✅ **Tự động hóa 100% quá trình** từ video YouTube → bài viết blog (Blotato) → thông báo Telegram → lưu log vào Google Sheets.
✅ **Tiết kiệm 8+ giờ/ngày** so với cách làm thủ công.
✅ **Cải thiện SEO** với mô tả tự động sinh bởi GPT-4.1-mini.
✅ **Hoạt động 24/7** mà không cần can thiệp của con người.

---
### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không phải viết script, mô tả hoặc biên tập bài viết thủ công.
- **Chất lượng cao**: GPT-4.1-mini tự động tạo **script chi tiết** và **mô tả SEO** phù hợp với video.
- **Hoạt động liên tục**: Workflow chạy tự động khi có video mới trên Google Sheets.
- **Dữ liệu theo dõi**: Tất cả thông tin được lưu vào Google Sheets để quản lý dễ dàng.
- **Tích hợp đa nền tảng**: Từ Telegram (thông báo) đến Blotato (blog) và YouTube (video).
:::

---
## 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị:
### **1. Tài Khoản & API Keys**
| Dịch Vụ | Link Đăng Ký | API Key/Credential trong n8n |
|---------|-------------|-----------------------------|
| **Telegram Bot** | [@BotFather](https://t.me/botfather) | `Telegram API` (Credential name: `Telegram - youtube`) |
| **Google Sheets API** | [Google Cloud Console](https://console.cloud.google.com/) | `Google Sheets OAuth2 API` (Credential name: `Google Sheets account`) |
| **Google Drive API** | [Google Cloud Console](https://console.cloud.google.com/) | `Google Drive OAuth2 API` (Credential name: `Google Drive account`) |
| **OpenAI (GPT-4.1-mini)** | [OpenAI Platform](https://platform.openai.com/) | `OpenAI API` (Credential name: `n8n free OpenAI API credits`) |
| **Blotato** | [Blotato](https://blotato.com/?ref=firas) | `Blotato API` (Credential name: `Blotato account`) |
| **RapidAPI (YouTube Transcript)** | [RapidAPI](https://rapidapi.com/) | **Không cần API key riêng** (được cấu hình trong node `RapidAPI Summarizer`) |

### **2. File & Template**
- **Google Sheets mẫu**: [Tải bản sao](https://docs.google.com/spreadsheets/d/1A-LpZ8OGn8FP692Hx50j3sEuPgIhlyMOrJ1jUNGwHr8/copy)
  - Cột cần thiết: `Video URL`, `Status` (đặt thành `"ready"` để kích hoạt workflow).
- **Video YouTube**: Các sếp cần **nạp video lên Google Drive** (để workflow lấy ID file).

---
## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
Các sếp có thể:
- **Tải file JSON** từ [n8n.io/workflows/12191](https://n8n.io/workflows/12191) và import vào n8n Editor.
- **Copy/paste JSON** từ file vào n8n Editor (đảm bảo không có lỗi syntax).

:::note[LƯU Ý]
- **Không xóa node nào** trong workflow, chỉ chỉnh sửa cấu hình.
- **Không sử dụng phiên bản n8n cũ** (cần n8n **v4.0+** để hỗ trợ node Blotato).
:::

---

### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**

#### **🔹 Node `Workflow Configuration` (Set)**
- **Cấu hình API RapidAPI**:
  - Mở node `RapidAPI Summarizer` → Tab `Advanced` → Điền:
    ```json
    {
      "url": "https://youtube-video-summarizer-gpt-ai.p.rapidapi.com/summarize",
      "method": "POST",
      "headers": {
        "content-type": "application/json",
        "X-RapidAPI-Key": "{{$node["Workflow Configuration"].json["rapidApiKey"]}}",
        "X-RapidAPI-Host": "youtube-video-summarizer-gpt-ai.p.rapidapi.com"
      },
      "body": {
        "videoUrl": "{{$json.videoUrl}}"
      }
    }
    ```
  - **Lưu ý**: API key RapidAPI **không cần điền** vào n8n, chỉ cần đặt trong `Workflow Configuration` như trên.

#### **🔹 Node `Generate Script` & `Generate SEO` (OpenAI)**
- **Model**: Chọn **`gpt-4-1106-preview`** (GPT-4.1-mini).
- **Prompt**:
  - **Generate Script**:
    ```plaintext
    Tạo một script chi tiết cho video YouTube có URL: {{$json.videoUrl}}. Script phải:
    1. Giới thiệu ngắn gọn về chủ đề.
    2. Phân tích chi tiết từng phần trong video.
    3. Kết luận và gọi hành động (CTA).
    Đảm bảo ngôn ngữ thân thiện và phù hợp với độc giả.
    ```
  - **Generate SEO**:
    ```plaintext
    Tạo mô tả SEO cho video YouTube có URL: {{$json.videoUrl}}. Mô tả phải:
    1. Có từ khóa chính (keyword) từ tiêu đề video.
    2. Gồm 150-200 ký tự.
    3. Kết hợp hashtag phù hợp.
    4. Được viết bằng tiếng Việt chuẩn.
    ```

#### **🔹 Node `Upload Video to BLOTATO`**
- **Cấu hình**:
  - **Resource**: `media` (đã mặc định).
  - **File**: Chọn `$node["Download file"].file` (file video đã tải từ Google Drive).
  - **Metadata**:
    ```json
    {
      "title": "{{$json.title}}",
      "description": "{{$json.seoDescription}}",
      "tags": ["youtube", "automation", "n8n"]
    }
    ```

#### **🔹 Node `Check Google Sheets`**
- **Cấu hình**:
  - **Sheet Name**: `Sheet1` (hoặc tên sheet của các sếp).
  - **Query**: `SELECT * WHERE Status = "ready"`.
  - **Output**: Chỉ lấy cột `Video URL`.

#### **🔹 Node `Get Google Drive ID` (Set)**
- **Cấu hình**:
  - **File ID**: Lấy từ URL Google Drive của video (ví dụ: `https://drive.google.com/file/d/FILE_ID/view` → `FILE_ID`).
  - **Output**:
    ```json
    {
      "fileId": "{{$json.fileId}}"
    }
    ```

---
### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Chọn một hàng trong Google Sheets có `Status = "ready"`.
   - Chạy **Manual Execution** trong n8n để kiểm tra workflow.
2. **Bật Active**:
   - Sau khi test thành công, **bật Active** cho workflow.

---
## ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::tip[CÁCH LÀM TIẾP]
- **Tích hợp Slack/Telegram thông báo lỗi**:
  - Thêm node `telegram` hoặc `slack` sau node `Generate Script` để gửi thông báo khi có lỗi.
- **Lưu log chi tiết**:
  - Thêm node `stickyNote` để ghi lại lỗi hoặc tiến trình.
- **Tự động chia sẻ trên mạng xã hội**:
  - Sau khi publish trên Blotato, thêm node `twitter` hoặc `facebook` để tự động share.
- **Tạo báo cáo định kỳ**:
  - Sử dụng node `googleSheets` để tổng hợp thống kê video đã publish.
:::

---
## 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp để tập trung vào **strategy content** thay vì làm thủ công. Với **GPT-4.1-mini**, **Blotato** và **Google Sheets**, nội dung của các sếp sẽ **chất lượng cao, SEO friendly** và **hoạt động tự động**.

**🚀 Hãy áp dụng ngay và tự động hóa nội dung của mình!**

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**📚 [Tài liệu chi tiết](https://automatisation.notion.site/YOUTUBE-2d53d6550fd980d0ba16fa054ecb1f95)** (Notion) | **🎥 Demo video setup** ([Youtube](https://youtu.be/szKueQ7Aen8))