---
title: "🚀 Tự động hóa Video: Transcript + Q&A với VLM Run, GPT-4 & Google Workspace"
description: "Hướng dẫn tự động hóa đầy đủ quy trình xử lý video: từ tải xuống, chuyển đổi transcript đến lưu trữ và trả lời câu hỏi thông minh bằng công nghệ AI tiên tiến."
slug: "tu-dong-hoa-video-transcript-va-q-a"
tags: [n8n, automation, no-code, google-workspace, ai, vlm-run, gpt-4]
keywords: [n8n workflow, tự động hóa video, transcript video, q&a video, vlm run, google sheets, openai]
---

# 🚀 Tự động hóa Video: Transcript + Q&A với VLM Run, GPT-4 & Google Workspace

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

Các sếp có bao giờ phải đối mặt với tình trạng:
- 📹 Phải xem lại hàng trăm video để tìm thông tin quan trọng?
- 📝 Tốn thời gian ghi chú tay từ nội dung video?
- 🤖 Cần trả lời hàng nghìn câu hỏi từ khách hàng về nội dung video?

Với workflow này, các sếp có thể tự động hóa hoàn toàn quy trình này chỉ trong vài bước đơn giản!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- 📝 **Tự động transcript video**: Chuyển đổi nội dung video thành văn bản đầy đủ trong vài phút
- 🔍 **Tìm kiếm thông minh**: Tìm kiếm thông tin trong video một cách nhanh chóng và chính xác
- 🤖 **Trả lời tự động**: Cung cấp câu trả lời chính xác từ nội dung video cho khách hàng
- 📊 **Lưu trữ tổ chức**: Lưu trữ transcript và thông tin liên quan trong Google Sheets
- ⏱️ **Tiết kiệm thời gian**: Giảm thiểu đến 80% thời gian xử lý video thủ công
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Workspace (Google Drive và Google Sheets)
- Tài khoản OpenAI (để sử dụng GPT-4)
- Tài khoản VLM Run (để xử lý video)
- URL webhook công khai (để nhận kết quả từ VLM Run)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/9325](https://n8n.io/workflows/9325)
2. Click vào nút "Import" ở góc trên bên phải
3. Chọn "Import from URL" và dán link workflow
4. Click "OK" để hoàn tất import

Hoặc có thể copy/paste JSON workflow vào n8n Editor:

```json
{
  "nodes": [
    {
      "parameters": {
        "folderId": "YOUR_FOLDER_ID",
        "triggerOn": "created"
      },
      "name": "Google Drive Trigger",
      "type": "googleDriveTrigger",
      "typeVersion": 1,
      "position": [
        250,
        300
      ]
    },
    {
      "parameters": {
        "operation": "download",
        "resource": "files",
        "options": {}
      },
      "name": "Download file",
      "type": "googleDrive",
      "typeVersion": 1,
      "position": [
        450,
        300
      ]
    },
    {
      "parameters": {
        "path": "transcript-video",
        "httpMethod": "POST"
      },
      "name": "Receives JSON Data",
      "type": "webhook",
      "typeVersion": 1,
      "position": [
        650,
        300
      ]
    },
    {
      "parameters": {
        "operation": "video",
        "options": {}
      },
      "name": "VLM Run for Video Processing",
      "type": "@vlm-run/n8n-nodes-vlmrun.vlmRun",
      "typeVersion": 1,
      "position": [
        850,
        300
      ]
    },
    {
      "parameters": {
        "operation": "append",
        "resource": "data",
        "options": {}
      },
      "name": "Append row in sheet",
      "type": "googleSheets",
      "typeVersion": 1,
      "position": [
        1050,
        300
      ]
    },
    {
      "parameters": {
        "resource": "data",
        "operation": "get"
      },
      "name": "Get row(s) in sheet in Google Sheets",
      "type": "googleSheetsTool",
      "typeVersion": 1,
      "position": [
        1250,
        300
      ]
    },
    {
      "parameters": {
        "model": "gpt-4.1",
        "temperature": 0.7,
        "maxTokens": 1000,
        "topP": 1,
        "frequencyPenalty": 0,
        "presencePenalty": 0,
        "stop": []
      },
      "name": "OpenAI Chat Model",
      "type": "lmChatOpenAi",
      "typeVersion": 1,
      "position": [
        1450,
        300
      ]
    },
    {
      "parameters": {
        "systemMessage": "You are a helpful assistant that answers questions based on the provided video transcript segments. Always cite your sources from the transcript. If you don't know the answer, say you don't know."
      },
      "name": "AI Agent",
      "type": "agent",
      "typeVersion": 1,
      "position": [
        1650,
        300
      ]
    },
    {
      "parameters": {
        "triggerOn": "message"
      },
      "name": "When chat message received",
      "type": "chatTrigger",
      "typeVersion": 1,
      "position": [
        1850,
        300
      ]
    }
  ],
  "connections": [
    {
      "node": "Google Drive Trigger",
      "type": "main",
      "index": 0,
      "target": "Download file"
    },
    {
      "node": "Download file",
      "type": "main",
      "index": 0,
      "target": "VLM Run for Video Processing"
    },
    {
      "node": "VLM Run for Video Processing",
      "type": "main",
      "index": 0,
      "target": "Append row in sheet"
    },
    {
      "node": "Receives JSON Data",
      "type": "main",
      "index": 0,
      "target": "Append row in sheet"
    },
    {
      "node": "When chat message received",
      "type": "main",
      "index": 0,
      "target": "AI Agent"
    },
    {
      "node": "AI Agent",
      "type": "main",
      "index": 0,
      "target": "Get row(s) in sheet in Google Sheets"
    },
    {
      "node": "Get row(s) in sheet in Google Sheets",
      "type": "main",
      "index": 0,
      "target": "OpenAI Chat Model"
    }
  ]
}
```

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Google Drive Trigger**:
   - Cần cấu hình credentials cho Google Drive OAuth2
   - Thay đổi `folderId` thành ID thư mục Google Drive bạn muốn theo dõi

2. **Download file**:
   - Đảm bảo credentials Google Drive đã được cấu hình
   - Kiểm tra quyền truy cập vào thư mục và file

3. **Receives JSON Data (Webhook)**:
   - Cần có URL webhook công khai để VLM Run có thể gửi kết quả
   - Thiết lập biến môi trường `N8N_WEBHOOK_URL` với giá trị là URL của webhook

4. **VLM Run for Video Processing**:
   - Cấu hình credentials cho VLM Run API
   - Đảm bảo domain `video.transcription` đã được kích hoạt trong tài khoản VLM Run

5. **Append row in sheet**:
   - Cấu hình credentials cho Google Sheets OAuth2
   - Thiết lập `spreadsheetId` và `range` cho sheet đích
   - Kiểm tra định dạng dữ liệu đầu vào phù hợp với sheet

6. **Get row(s) in sheet in Google Sheets**:
   - Cấu hình credentials cho Google Sheets OAuth2
   - Thiết lập `spreadsheetId` và `range` cho sheet nguồn
   - Kiểm tra truy vấn dữ liệu phù hợp với nhu cầu

7. **OpenAI Chat Model**:
   - Cấu hình credentials cho OpenAI API
   - Chọn model phù hợp (gpt-4.1 trong ví dụ)
   - Điều chỉnh các tham số như temperature, maxTokens...

8. **AI Agent**:
   - Thiết lập `systemMessage` phù hợp với mục đích sử dụng
   - Kiểm tra logic xử lý câu hỏi và trả lời

9. **When chat message received**:
   - Cấu hình kênh chat phù hợp (Slack, Telegram, Discord...)
   - Thiết lập các thông số kết nối cần thiết

#### 3. Kích hoạt ⚡️
1. Sau khi cấu hình xong tất cả các node, click vào nút "Activate" ở góc trên bên phải
2. Kiểm tra kết nối và xác nhận kích hoạt
3. Test workflow với dữ liệu mẫu để đảm bảo hoạt động đúng

### ✍️ Mẹo & gợi ý nâng cao
1. **Tối ưu hóa tìm kiếm**:
   - Thêm timestamp vào trường Data để cải thiện khả năng tìm kiếm
   - Sử dụng các kỹ thuật như vector embedding để tìm kiếm thông tin phức tạp

2. **Quản lý dữ liệu**:
   - Thiết lập lịch trình dọn dẹp dữ liệu cũ trong Google Sheets
   - Sử dụng các hàm xử lý dữ liệu trong Google Sheets để làm sạch và chuẩn hóa dữ liệu

3. **Tích hợp nâng cao**:
   - Kết nối với các nền tảng như Slack, Telegram để nhận thông báo khi có video mới
   - Tích hợp với các hệ thống CRM để tự động hóa các quy trình hỗ trợ khách hàng

4. **Bảo mật và quản lý**:
   - Thiết lập quyền truy cập phù hợp cho các tài nguyên Google
   - Sử dụng các tính năng bảo mật của OpenAI và VLM Run
   - Thiết lập logging và monitoring cho workflow

### 📌 Kết luận
Workflow này cung cấp giải pháp toàn diện cho việc tự động hóa quy trình xử lý video, từ transcript đến trả lời câu hỏi thông minh. Với công nghệ AI tiên tiến và tích hợp liền mạch với Google Workspace, các sếp có thể tiết kiệm thời gian đáng kể và nâng cao hiệu quả làm việc.

Hãy áp dụng ngay workflow này để tối ưu hóa quy trình xử lý video của các sếp và nâng cao trải nghiệm khách hàng!