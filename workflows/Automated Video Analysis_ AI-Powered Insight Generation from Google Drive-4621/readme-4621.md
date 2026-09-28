---
title: "🎬 **Tự Động Hóa Phân Tích Video AI: Tạo Báo Cáo Thông Minh Từ Google Drive (Không Cần Code!)**"
description: "Workflow tự động hóa hoàn toàn tải video từ Google Drive, kiểm tra trạng thái, phân tích nội dung bằng AI Gemini, và tạo báo cáo cấu trúc hóa tự động. Giúp các sếp tiết kiệm thời gian lên tới 80% trong việc phân tích video marketing, đào tạo nội bộ hoặc content review."
slug: "tieu-dong-hoa-phan-tich-video-ai-google-drive"
tags: [n8n, automation, ai, google-drive, google-gemini, marketing, no-code]
keywords: [tự động hóa video, phân tích video bằng AI, n8n workflow google drive, gemini api tự động hóa, báo cáo video tự động]
---

# 🚀 **Tự Động Hóa Phân Tích Video AI: Tạo Báo Cáo Thông Minh Từ Google Drive**

### **💡 Giải quyết vấn đề gì?**
Các sếp thường phải mất **giờ đồng hồ** để tải video từ Google Drive, kiểm tra trạng thái tải, và phân tích nội dung thủ công. Kết quả? **Chậm, không nhất quán, và dễ bị lỗi nhân sự**. Workflow này **tự động hóa toàn bộ quy trình** bằng AI Gemini, giúp bạn:
- **Tải video tự động** từ Google Drive.
- **Phân tích nội dung** bằng AI (ngôn ngữ, cảm xúc, khái quát video).
- **Tạo báo cáo cấu trúc hóa** sẵn sàng chia sẻ.
- **Hoạt động 24/7** mà không cần can thiệp của con người.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo tính riêng tư và hiệu suất cao.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần tải video thủ công, phân tích từng đoạn clip.
- **Chính xác cao**: AI Gemini phân tích **ngôn ngữ, cảm xúc, và nội dung chính** trong video.
- **Báo cáo tự động**: Kết quả được **cấu trúc hóa** và sẵn sàng chia sẻ (Slack, Email, Google Sheets).
- **Hoạt động liên tục**: Chạy theo lịch trình (ngày, tuần) mà không cần can thiệp.
- **Tích hợp AI tiên tiến**: Sử dụng **Google Gemini API** (mô hình AI hàng đầu của Google).
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Google Drive** (và **Google OAuth 2.0 API Key** để truy cập file).
2. **Google Gemini API Key** (đăng ký tại [Google AI Studio](https://makersuite.google.com/)).
3. **File video** đã được upload lên Google Drive (định dạng hỗ trợ: MP4, MOV, AVI).
4. **n8n Self-hosted** (không dùng phiên bản cloud để đảm bảo bảo mật).

---
:::note[LƯU Ý QUAN TRỌNG]
- Workflow **không hỗ trợ video quá lớn** (n8n có giới hạn tải file).
- Nếu video quá dài, hãy **cắt video trước** thành các đoạn ngắn (ví dụ: 5-10 phút).
:::

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
**Bước 1:** Tải file JSON từ [n8n.io/workflows/4621](https://n8n.io/workflows/4621) hoặc copy toàn bộ JSON dưới đây.

**Bước 2:** Mở **n8n Editor** và nhấn **"Import"** → Chọn file JSON hoặc dán JSON vào ô nhập.

```json
{
  "nodes": [
    {
      "parameters": {
        "operation": "download"
      },
      "name": "Download Video from Drive",
      "type": "n8n-nodes-base.googleDrive",
      "credentials": {
        "googleDriveOAuth2Api": "YOUR_GOOGLE_DRIVE_CREDENTIALS"
      }
    },
    {
      "name": "Check File Status",
      "type": "n8n-nodes-base.httpRequest",
      "credentials": {}
    },
    {
      "name": "Analyze Video",
      "type": "n8n-nodes-base.httpRequest",
      "credentials": {}
    },
    {
      "name": "Format Analysis Result",
      "type": "n8n-nodes-base.set"
    },
    {
      "name": "Schedule Trigger",
      "type": "n8n-nodes-base.scheduleTrigger",
      "credentials": {}
    },
    {
      "name": "Basic LLM Chain",
      "type": "n8n-nodes-langchain.chainLlm",
      "credentials": {}
    },
    {
      "name": "Google Gemini Chat Model",
      "type": "n8n-nodes-langchain.lmChatGoogleGemini",
      "credentials": {
        "googlePalmApi": "YOUR_GEMINI_API_KEY"
      }
    }
  ],
  "connections": {
    "Schedule Trigger": {
      "main": [
        [
          {
            "node": "Download Video from Drive",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Download Video from Drive": {
      "main": [
        [
          {
            "node": "Check File Status",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Check File Status": {
      "main": [
        [
          {
            "node": "Analyze Video",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Analyze Video": {
      "main": [
        [
          {
            "node": "Google Gemini Chat Model",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Google Gemini Chat Model": {
      "main": [
        [
          {
            "node": "Basic LLM Chain",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Basic LLM Chain": {
      "main": [
        [
          {
            "node": "Format Analysis Result",
            "type": "main",
            "index": 0
          }
        ]
      ]
    }
  }
}
```

**Bước 3:** Sau khi import, **không cần chỉnh sửa cấu trúc**, chỉ cần **cấu hình các node quan trọng** như sau:

---

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**

##### **🔹 Node 1: Download Video from Drive**
- **Credentials**: Chọn `googleDriveOAuth2Api` (đã cấu hình trước khi import).
- **Parameters**:
  - `fileId`: **ID của file video** trong Google Drive (lấy từ liên kết chia sẻ).
  - `mimeType`: Đặt là `video/*` (hỗ trợ tất cả định dạng video).
  - **Lưu ý**: Nếu video quá lớn, hãy **cắt video trước** để tránh lỗi tải.

##### **🔹 Node 2: Google Gemini Chat Model**
- **Credentials**: Chọn `googlePalmApi` (đã cấu hình API Key).
- **Parameters**:
  - **Prompt**: Cấu hình **câu hỏi phân tích** cho AI (ví dụ:
    ```
    "Analyze this video and provide a structured summary including:
    1. Main topics discussed
    2. Key takeaways
    3. Sentiment analysis (positive/negative/neutral)
    4. Recommended actions"
    ```
  - **Model**: Chọn `gemini-pro` (mô hình mạnh nhất của Google).

##### **🔹 Node 3: Schedule Trigger (Lịch trình chạy)**
- **Parameters**:
  - **Frequency**: Chọn `daily` (hoặc `weekly` tùy nhu cầu).
  - **Time**: Đặt giờ chạy (ví dụ: 8h sáng để phân tích video mới upload).

##### **🔹 Node 4: Format Analysis Result (Cấu trúc hóa kết quả)**
- **Parameters**:
  - **JSON Path**: Đặt là `$` (truy cập toàn bộ dữ liệu từ AI).
  - **Format**: Chọn `JSON` để dễ dàng tích hợp với Slack/Email.

---

#### **3. Kích hoạt ⚡️**
**Bước 1:** Nhấn **"Test Run"** với **file video mẫu** để kiểm tra.
**Bước 2:** Sau khi test thành công, **bật Active workflow**.

---
### ✍️ **Mẹo & gợi ý nâng cao**
1. **Tích hợp với Slack/Telegram**:
   - Sau khi phân tích xong, **gửi kết quả** qua Slack/Telegram bằng node `n8n-nodes-base.slack` hoặc `n8n-nodes-base.telegram`.

2. **Lưu log phân tích**:
   - Sử dụng node `n8n-nodes-base.googleSheets` để **ghi lại tất cả báo cáo** vào một bảng Excel tự động.

3. **Phân tích video định kỳ**:
   - Nếu video dài, **chia thành nhiều đoạn** và chạy workflow cho từng đoạn riêng.

4. **Tối ưu prompt AI**:
   - Nếu kết quả không chính xác, **cập nhật prompt** để AI hiểu rõ hơn (ví dụ: yêu cầu AI **liệt kê thời gian xuất hiện** của từng chủ đề).

---
### 📌 **Kết luận**
Workflow này **giải phóng thời gian** của các sếp khỏi công việc phân tích video thủ công, đồng thời **cung cấp báo cáo AI chính xác và tự động hóa**. **Bắt đầu ngay** bằng cách:
1. **Import workflow** và cấu hình các node.
2. **Chạy thử** với video mẫu.
3. **Bật tự động hóa** và **quên đi việc phân tích video**!

**🚀 Cần hỗ trợ?** Liên hệ với tác giả **Yaron Been** qua:
- [LinkedIn](https://www.linkedin.com/in/yaronbeen/)
- [YouTube](https://www.youtube.com/@YaronBeen/videos)

---
**💡 Mẹo cuối:** Nếu muốn **tăng tốc độ phân tích**, hãy **cắt video thành các đoạn ngắn** (5-10 phút) trước khi upload lên Google Drive!