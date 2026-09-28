---
title: "🎵 Tự Động Hoàn Thành 20 Bài Hát YouTube Playlist Với Suno AI, Claude & Telegram Bot (N8N)"
description: "Workflow tự động hóa 100% không code để tạo ra 20 bài hát độc quyền cho playlist YouTube, kết hợp AI Suno (sáng tạo nhạc), Claude (tạo lời), và Telegram Bot (cập nhật tự động). Giúp các content creator tiết kiệm 100+ giờ/tháng và tăng cường nội dung cá nhân hóa."
slug: "tay-dong-hoan-thanh-20-bai-hat-youtube-playlist"
tags: [n8n, automation, content-creation, ai-multimodal, suno-ai, claude-ai, telegram-bot, google-sheets, google-drive]
keywords: [n8n workflow tự động hóa, tạo playlist youtube bằng ai, suno api tự động, claude ai tạo lời bài hát, telegram bot cập nhật playlist, tự động hóa content creator]
---

# 🚀 **Tự Động Hoàn Thành 20 Bài Hát Playlist YouTube Với AI & Telegram Bot**

### **Giải pháp cho những content creator mệt mỏi vì phải tạo nhạc và lời bài hát thủ công**
Hãy tưởng tượng một ngày bạn chỉ cần **nhấp một nút** trên Telegram, và trong vòng 24 giờ, một **playlist YouTube hoàn chỉnh với 20 bài hát độc quyền** đã được tạo ra tự động:
- **Nhạc** được sinh ra từ AI Suno (chất lượng cao, phù hợp với mọi thể loại).
- **Lời bài hát** được viết bởi Claude AI (cá nhân hóa theo chủ đề, cảm xúc, hoặc keyword bạn chỉ định).
- **Playlists** được tổ chức trên Google Sheets và Google Drive, với trạng thái cập nhật tự động.
- **Báo cáo tiến độ** được gửi qua Telegram mỗi khi một bài hát hoàn thành.

**Workflow này không chỉ tiết kiệm 100+ giờ/tháng mà còn giúp bạn:**
✅ **Tăng sản lượng nội dung** lên 10x mà không cần viết nhạc thủ công.
✅ **Cá nhân hóa từng playlist** theo nhu cầu của khán giả (ví dụ: playlist "Bài hát về tình yêu mùa thu" hoặc "Nhạc game indie").
✅ **Hoạt động 24/7** mà không cần can thiệp của con người.
✅ **Tối ưu chi phí** so với việc thuê nhạc sĩ hoặc mua bản quyền nhạc.

---
## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Từ 10+ giờ/tuần xuống còn **5 phút/playlist**.
- **Nội dung độc quyền**: Playlist không trùng lặp với bất kỳ kênh nào khác.
- **Cập nhật tự động**: Telegram Bot thông báo tiến độ và kết quả cuối cùng.
- **Quản lý dễ dàng**: Tất cả dữ liệu tập trung trên Google Sheets và Drive.
- **Khả năng mở rộng**: Dễ dàng tạo ra nhiều playlist song song với các chủ đề khác nhau.
:::

---
## 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
### **1. Tài khoản và API Keys**
| Dịch vụ/API | Yêu cầu |
|-------------|----------|
| **Suno API** | [Đăng ký API Key](https://suno.com/api) (để tạo nhạc từ prompt). |
| **Anthropic (Claude AI)** | [Đăng ký API Key](https://www.anthropic.com/api) (để viết lời bài hát). |
| **Google Workspace** | Tài khoản Google với quyền chỉnh sửa **Google Sheets** và **Google Drive**. |
| **Telegram Bot** | Bot Telegram được tạo và có **Token API** (hướng dẫn [tại đây](https://core.telegram.org/bots/api#creating-a-new-bot)). |
| **n8n Self-hosted** | [Cài đặt n8n trên VPS](https://docs.n8n.io/hosting/installation/) (không dùng phiên bản cloud để đảm bảo ổn định). |

### **2. File và cấu trúc Google Sheets**
Workflow yêu cầu **4 bảng Google Sheets** với cấu trúc cụ thể:
1. **Playlist Details Sheet** (danh sách các playlist cần tạo).
2. **Generated Songs Sheet** (lưu trữ thông tin bài hát đã tạo).
3. **Suno Task ID Sheet** (quản lý ID của các nhiệm vụ tạo nhạc).
4. **Drive Details Sheet** (thông tin về folder trên Google Drive).

:::note[LƯU Ý]
Các sếp **phải tạo sẵn 4 bảng này** trước khi import workflow. Dưới đây là **mẫu cấu trúc** cho từng bảng:
#### **Playlist Details Sheet**
| Column Name | Data Type | Mô tả |
|-------------|-----------|-------|
| `playlist_id` | Text | ID duy nhất cho playlist (cần tự tạo hoặc sử dụng node `Generate Unique Playlist ID`). |
| `playlist_name` | Text | Tên playlist (ví dụ: "Bài hát về tình yêu mùa thu"). |
| `playlist_description` | Text | Mô tả playlist (tự động lấy từ Claude AI). |
| `playlist_theme` | Text | Chủ đề chính (ví dụ: "Tình yêu", "Du lịch", "Game"). |
| `status` | Text | Trạng thái: `pending`, `in_progress`, `completed`. |
| `created_at` | DateTime | Thời gian tạo playlist. |

#### **Generated Songs Sheet**
| Column Name | Data Type | Mô tả |
|-------------|-----------|-------|
| `song_title` | Text | Tiêu đề bài hát (tự động tạo). |
| `song_summary` | Text | Tóm tắt nội dung (tự động tạo). |
| `suno_task_id` | Text | ID nhiệm vụ từ Suno API. |
| `song_url` | Text | Link tải nhạc (sau khi hoàn thành). |
| `lyrics` | Text | Lời bài hát (tự động tạo). |
| `status` | Text | Trạng thái: `pending`, `generating`, `completed`. |
| `playlist_id` | Text | ID playlist thuộc về bài hát này. |

#### **Suno Task ID Sheet**
| Column Name | Data Type | Mô tả |
|-------------|-----------|-------|
| `task_id` | Text | ID nhiệm vụ từ Suno API. |
| `song_id` | Text | ID bài hát tương ứng trong `Generated Songs Sheet`. |
| `status` | Text | Trạng thái: `pending`, `processing`, `completed`. |

#### **Drive Details Sheet**
| Column Name | Data Type | Mô tả |
|-------------|-----------|-------|
| `folder_id` | Text | ID folder trên Google Drive. |
| `playlist_id` | Text | ID playlist liên quan. |
| `status` | Text | Trạng thái: `pending`, `created`, `shared`. |
:::

---
## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
#### **Bước 1: Tải file JSON**
- Tải workflow từ [n8n.io/workflows/6021](https://n8n.io/workflows/6021) hoặc sử dụng file JSON đã cung cấp.
- **Lưu ý**: File này có **128 node**, nên **không nên import trực tiếp từ giao diện web** của n8n.io (do giới hạn kích thước). Thay vào đó:
  - **Tải file JSON** và mở bằng trình soạn thảo như **VS Code**.
  - **Copy toàn bộ nội dung JSON** và dán vào **n8n Editor** (trang `Create Workflow` → `Import Workflow` → `Paste JSON`).

#### **Bước 2: Chọn template và import**
- Trong n8n Editor, chọn **`Import Workflow`** và chọn **`Paste JSON`**.
- Nhấn **`Import`** và chờ workflow được tải hoàn toàn.

---
### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này **phức tạp** và yêu cầu cấu hình cẩn thận. Dưới đây là **các node quan trọng** cần chỉnh sửa:

#### **🔹 Node `Playlist Telegram Bot` (Telegram Trigger)**
- **Cấu hình**:
  - **Update Token**: Điền **Token API** của bot Telegram (tìm trong `@username:bot` trên Telegram).
  - **Command**: Đặt là `/create_playlist` (người dùng sẽ gửi lệnh này để kích hoạt workflow).
  - **Chat ID**: Điền **ID chat** của bot (lấy từ [@userinfobot](https://t.me/userinfobot)).

#### **🔹 Node `AI Music Agent` (Agent)**
- **Cấu hình**:
  - **Tools**: Đảm bảo các tool liên quan (`Anthropic Chat Model`, `Suno API Request`) được kết nối.
  - **Prompt**: Workflow đã định sẵn prompt cho Claude AI và Suno API, **không cần chỉnh sửa** trừ khi muốn thay đổi logic.

#### **🔹 Node `Anthropic Chat Model` (lmChatAnthropic)**
- **Cấu hình**:
  - **API Key**: Điền **API Key** của Anthropic (Claude AI).
  - **Model**: Chọn `claude-2` (hoặc phiên bản mới nhất).
  - **Prompt Template**: Workflow đã cấu hình sẵn để tạo **tên bài hát và tóm tắt** từ chủ đề playlist.

#### **🔹 Node `Music Generation API Request` (httpRequest)**
- **Cấu hình**:
  - **URL**: `https://api.suno.com/v1/tasks` (API của Suno).
  - **Headers**:
    ```json
    {
      "Authorization": "Bearer YOUR_SUNO_API_KEY",
      "Content-Type": "application/json"
    }
    ```
  - **Body**:
    ```json
    {
      "prompt": "${{ $json["prompt"] }}",
      "duration": 30,
      "temperature": 0.7
    }
    ```
  - **Lưu ý**: Thay `YOUR_SUNO_API_KEY` bằng API Key của bạn.

#### **🔹 Node `Google Sheets` (get_playlist_rows_tool, append_playlist_tool, ...)**
- **Cấu hình chung**:
  - **Credentials**: Chọn **credentials** đã tạo trước đó trong n8n (ví dụ: `google-sheets-credentials`).
  - **Spreadsheet ID**: Điền **ID của Google Sheet** (lấy từ liên kết share: `https://docs.google.com/spreadsheets/d/[ID]/edit`).
  - **Sheet Name**: Điền tên bảng tương ứng (`Playlist Details`, `Generated Songs`, `Suno Task ID`, `Drive Details`).

#### **🔹 Node `Google Drive` (create_songs_drive_folder, make_drive_folder_public)**
- **Cấu hình**:
  - **Credentials**: Chọn credentials Google Drive đã cấu hình.
  - **Folder Name**: Đặt tên folder theo mẫu: `Playlist_{{$json["playlist_id"]}}_Songs`.

#### **🔹 Node `Wait` (wait 10 minutes, wait 2 minutes)**
- **Cấu hình**:
  - Thời gian chờ **không cần chỉnh sửa** (workflow đã tối ưu thời gian chờ giữa các bước).

#### **🔹 Node `Structured Output Parser` (outputParserStructured)**
- **Cấu hình**:
  - **Schema**: Workflow đã định sẵn schema để phân tích kết quả từ Claude AI và Suno API. **Không cần chỉnh sửa** trừ khi muốn thay đổi cấu trúc dữ liệu.

---
### **3. Kích hoạt ⚡️**
#### **Bước 1: Test Run với dữ liệu mẫu**
1. **Tạo một hàng mẫu** trong `Playlist Details Sheet` với:
   - `playlist_id`: `test_playlist_1`
   - `playlist_name`: "Bài hát về tình yêu mùa thu"
   - `playlist_theme`: "Tình yêu, mùa thu"
   - `status`: `pending`
2. **Gửi lệnh `/create_playlist`** đến bot Telegram.
3. **Kiểm tra tiến độ**:
   - Telegram Bot sẽ gửi **cập nhật tiến độ** (ví dụ: "Đang tạo nhạc cho bài hát 1/20").
   - Kiểm tra **Google Sheets** và **Google Drive** để xác nhận bài hát đã được tạo.

#### **Bước 2: Bật Active workflow**
- Sau khi test thành công, **bật chế độ `Active`** của workflow.
- **Lưu ý**: Workflow này **sử dụng nhiều schedule trigger**, nên **không nên chạy liên tục** nếu không có yêu cầu. Thay vào đó, kích hoạt bằng Telegram Bot hoặc sử dụng **schedule trigger** định kỳ (ví dụ: 1 lần/ngày).

---
## ✍️ **Mẹo & gợi ý nâng cao**
### **1. Tối ưu hóa cho nhiều playlist song song**
- **Sử dụng `Split Out`** để chia nhỏ các nhiệm vụ (ví dụ: tạo 5 playlist cùng lúc).
- **Cấu hình `Schedule Trigger`** để chạy workflow vào giờ rảnh (ví dụ: 3h sáng).

### **2. Kết hợp với YouTube API**
- Sau khi có **song URL**, tự động **upload lên YouTube** bằng node `YouTube API` (n8n có plugin hỗ trợ).
- **Mẫu prompt cho Claude AI** để tạo **thumbnails và mô tả video**:
  ```plaintext
  Tạo một mô tả video YouTube cho bài hát "{{$json["song_title"]}}" với chủ đề "{{$json["playlist_theme"]}}". Mô tả phải:
  1. Giới thiệu ngắn về bài hát.
  2. Nêu cảm xúc hoặc chủ đề chính.
  3. Kêu gọi người xem like và subscribe.
  ```

### **3. Lưu log và báo cáo**
- **Thêm node `Set`** để lưu **log hoạt động** vào một bảng Google Sheets riêng.
- **Tạo báo cáo tuần/Tháng** bằng **Google Data Studio** hoặc **Power BI** từ dữ liệu trong Sheets.

### **4. Cập nhật tự động trên Telegram**
- **Tạo một bot Telegram mới** chỉ để **báo cáo kết quả** (không cần tương tác).
- **Cấu hình node `Telegram`** để gửi **tin nhắn định kỳ** (ví dụ: "Playlist 'Bài hát về du lịch' đã hoàn thành!").

### **5. Mở rộng với các AI khác**
- Thay thế **Claude AI** bằng **Gemini (Google AI)** hoặc **Mistral AI** nếu có API Key.
- **Sử dụng MidJourney API** để tạo **thumbnails** cho playlist.

---
## 📌 **Kết luận**
Workflow này là **giải pháp hoàn chỉnh** cho những content creator muốn **tự động hóa toàn bộ quy trình tạo playlist YouTube**, từ **tạo nhạc** đến **viết lời** và **quản lý nội dung**. Với **n8n**, các sếp không cần viết một dòng code nào cả, mà vẫn có thể:
✔ **Tiết kiệm 100+ giờ/tháng**.
✔ **Tạo nội dung độc