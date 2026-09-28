---
title: "🎬 Tự Động Chuyển RSS Tin Tức Sang Video Avatar AI với Heygen & GPT-4o – Giảm 90% Thời Gian Chế Biến Nội Dung"
description: "Workflow này tự động lấy tin tức từ RSS, tổng hợp nội dung bằng AI Agent, tạo video avatar động hình với giọng nói tự nhiên bằng Heygen, và lưu kết quả vào Google Sheets – hoàn toàn không cần code. Phù hợp cho các sếp marketing, content creator, và doanh nghiệp cần nội dung video tự động hóa."
slug: "tu-dong-chuyen-rss-sang-video-avatar-ai"
tags: [n8n, automation, ai, marketing, content-creation, heygen, gpt-4o, google-sheets, rss]
keywords: [n8n workflow tự động hóa, tạo video avatar AI, chuyển RSS thành video, Heygen API, GPT-4o tự động hóa nội dung, tự động hóa marketing]
---

# 🚀 **Tự Động Chuyển RSS Tin Tức Sang Video Avatar AI – Giải Pháp Marketing "Chỉ Cần Nhấn 1 Nút"**

### **Nỗi Đau Của Các Sếp Marketing & Content Creator**
Các sếp thường phải:
- **Lấy tin tức** từ nhiều nguồn RSS (Vnexpress, BBC, TechCrunch...) và **lọc nội dung** phù hợp.
- **Viết script** và **ghi âm** cho video – mất thời gian và không hiệu quả.
- **Tạo video** từ nội dung văn bản – đòi hỏi kỹ năng chỉnh sửa video và thiết kế.
- **Phân phối nội dung** trên mạng xã hội – mất công kiểm tra và điều chỉnh.

**Workflow này giải quyết tất cả!** Nó tự động:
✅ **Lấy tin tức** từ RSS.
✅ **Tổng hợp & viết script** bằng AI Agent.
✅ **Tạo video avatar động hình** với giọng nói tự nhiên bằng Heygen.
✅ **Lưu log & kết quả** vào Google Sheets.
✅ **Tải video xuống** để sử dụng.

---
### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**Lợi Ích Cốt Lõi**]
- **Tiết kiệm 90% thời gian** so với cách làm thủ công.
- **Nội dung video cá nhân hóa** với giọng nói tự nhiên, không cần diễn viên.
- **Hoạt động 24/7** – không cần can thiệp của con người.
- **Dễ dàng mở rộng** cho nhiều nguồn RSS và chủ đề.
- **Lưu trữ & theo dõi** tất cả video trong Google Sheets.
:::

---
### 🔧 **Yêu Cầu Cần Thiết**
:::info[**CHUẨN BỊ TRƯỚC KHI BẮT ĐẦU**]
Để workflow hoạt động, các sếp cần:
1. **Tài khoản Heygen** (đăng ký tại [heygen.com](https://heygen.com/)) và **API Key**.
2. **Tài khoản OpenAI** (để sử dụng GPT-4o) và **API Key**.
3. **Tài khoản Google Drive & Google Sheets** (để lưu log và kết quả).
4. **Danh sách URL RSS** của các nguồn tin tức muốn theo dõi (ví dụ: Vnexpress, BBC, TechCrunch).
5. **VPS n8n** (để chạy workflow 24/7 – **không thể chạy trên n8n.cloud miễn phí**).

:::info[**Gợi ý hạ tầng cho n8n**]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Cách 1:** Tải file JSON từ [n8n.io/workflows/4288](https://n8n.io/workflows/4288) và import vào n8n Editor.
- **Cách 2:** Copy toàn bộ JSON từ link trên và paste vào **Import Workflow** trong n8n.
- **Cách 3:** Sử dụng **n8n CLI** để import:
  ```bash
  n8n import workflow.json --nodeInputs
  ```

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này có **15 node**, nhưng các node quan trọng nhất cần cấu hình kỹ lưỡng:

##### **A. Cấu Hình Heygen (Setup Heygen)**
- **Node:** `Setup Heygen` (type: `set`)
- **Cách làm:**
  1. Mở node `Setup Heygen`.
  2. Thêm biến môi trường:
     ```json
     {
       "HEYGEN_API_KEY": "your_heygen_api_key_here",
       "HEYGEN_PROJECT_ID": "your_project_id_here"
     }
     ```
  3. **Lấy `HEYGEN_API_KEY` và `PROJECT_ID`:**
     - Đăng nhập Heygen → **API Settings** → Copy `API Key`.
     - Tạo một **Project** mới → Copy `Project ID`.

##### **B. Cấu Hình OpenAI (GPT-4o)**
- **Node:** `write script` (type: `lmChatOpenAi`)
- **Cách làm:**
  1. Mở node `write script`.
  2. Thêm **API Key** của OpenAI vào **Credentials**.
  3. **Cấu hình Prompt:**
     - Sử dụng **template mặc định** trong workflow, nhưng có thể tùy chỉnh để phù hợp với nội dung RSS của bạn.
     - Ví dụ:
       ```json
       "prompt": "Tóm tắt tin tức này thành một script ngắn (30-60 giây) phù hợp cho video avatar. Đảm bảo có tiêu đề hấp dẫn và kết thúc bằng một câu hỏi để kích thích tương tác. Tin tức: {{$json.rssItem.content}}"
       ```

##### **C. Cấu Hình RSS Feed**
- **Node:** `RSS Read` (type: `rssFeedRead`)
- **Cách làm:**
  1. Mở node `RSS Read`.
  2. Thêm **URL RSS** của các nguồn tin tức bạn muốn theo dõi (ví dụ: `https://vnexpress.net/rss/tin-tuc.rss`).
  3. **Lọc tin tức** bằng cách sử dụng **filter** trong node `Limit` (node `Limit` sẽ giới hạn số lượng tin tức được xử lý).

##### **D. Cấu Hình Google Sheets**
- **Node:** `log news to sheets` và `Log video url and title to sheets` (type: `googleSheets`)
- **Cách làm:**
  1. Tạo một **Google Sheet** mới với 2 sheet:
     - **Sheet 1:** `News Log` (để lưu tin tức đã xử lý).
     - **Sheet 2:** `Video Log` (để lưu URL và tiêu đề video).
  2. Trong node `googleSheets`, chọn:
     - **Credentials:** Tài khoản Google của bạn.
     - **Sheet Name:** `News Log` (cho node `log news to sheets`) và `Video Log` (cho node `Log video url and title to sheets`).
     - **Range:** `A1` (để ghi dữ liệu từ ô A cột 1).

##### **E. Cấu Hình Heygen API Requests**
- **Node:** `Get Avatar Video`, `Create Avatar Video`, `Download video` (type: `httpRequest`)
- **Cách làm:**
  1. Trong node `Get Avatar Video`:
     - **Method:** `GET`
     - **URL:** `https://api.heygen.com/v1/avatars`
     - **Headers:**
       ```json
       {
         "Authorization": "Bearer {{$node["Setup Heygen"]["json"]["HEYGEN_API_KEY"]}}",
         "Content-Type": "application/json"
       }
       ```
  2. Trong node `Create Avatar Video`:
     - **Method:** `POST`
     - **URL:** `https://api.heygen.com/v1/avatars/{{$json.avatarId}}/videos`
     - **Body:**
       ```json
       {
         "script": "{{$json.script}}",
         "avatarId": "{{$json.avatarId}}",
         "settings": {
           "voice": "neutral",
           "speed": 1.0
         }
       }
       ```
  3. Trong node `Download video`:
     - **Method:** `GET`
     - **URL:** `{{$json.videoUrl}}` (URL video từ Heygen).

##### **F. Cấu Hình AI Agent (parse caption)**
- **Node:** `parse caption` (type: `code`)
- **Cách làm:**
  - Mở node `parse caption` và chỉnh sửa code để **tách tiêu đề và nội dung** từ tin tức RSS.
  - **Ví dụ code:**
    ```javascript
    return {
      json: {
        title: item.title,
        content: item.content
      }
    };
    ```
  - **Lưu ý:** Đảm bảo biến `item` được truyền từ node `RSS Read`.

#### **3. Kích Hoạt ⚡️ Workflow**
1. **Test Run** với một tin tức mẫu:
   - Nhấn **Test Workflow** và chọn một tin tức từ RSS.
   - Kiểm tra từng node để đảm bảo không có lỗi.
2. **Bật Active Workflow:**
   - Sau khi test thành công, chuyển trạng thái từ **Inactive** sang **Active**.
   - **Lưu ý:** Workflow sẽ chạy liên tục theo lịch trình của node `Wait` (thời gian chờ giữa các lần lấy tin tức).

---
### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tự động gửi video đến Slack/Telegram:**
   - Thêm node `slack` hoặc `telegramBot` sau node `Download video` để thông báo khi video được tạo thành công.
   - **Cách làm:**
     - Mở node `slack` → Chọn **Credentials** → Thêm token Slack.
     - Gửi thông báo với nội dung:
       ```json
       "text": "🎬 Video mới được tạo: {{$json.title}} - {{$json.videoUrl}}"
       ```

2. **Lưu video vào Google Drive tự động:**
   - Thêm node `googleDrive` sau node `Download video` để lưu video vào một folder cụ thể.
   - **Cách làm:**
     - Chọn **Credentials** → Tài khoản Google Drive.
     - **Folder ID** → Chọn folder muốn lưu.
     - **File Name:** `{{$json.title}}.mp4`

3. **Tùy chỉnh giọng nói và avatar Heygen:**
   - Trong node `Create Avatar Video`, bạn có thể thay đổi **giọng nói** (`voice`) và **tốc độ** (`speed`) để phù hợp với nội dung.
   - **Ví dụ:**
     ```json
     "settings": {
       "voice": "female_neutral", // Thay đổi giọng nữ hoặc nam
       "speed": 1.2 // Tăng tốc độ
     }
     ```

4. **Lọc tin tức theo chủ đề:**
   - Sử dụng node `code` để **lọc tin tức** trước khi gửi vào Heygen.
   - **Ví dụ:**
     ```javascript
     if (item.title.includes("AI") || item.title.includes("Marketing")) {
       return { json: item };
     }
     return null;
     ```

5. **Gửi báo cáo định kỳ:**
   - Thêm node `googleSheets` để **tổng hợp thống kê** số lượng video được tạo trong một ngày.
   - **Cách làm:**
     - Tạo một sheet mới `Daily Report`.
     - Gửi dữ liệu từ node `Log video url and title to sheets` vào sheet này với ngày tháng.

---
### 📌 **Kết Luận: Bắt Đầu Tự Động Hóa Nội Dung Video Hôm Nay!**
Workflow này là **giải pháp hoàn hảo** cho các sếp marketing, content creator và doanh nghiệp muốn:
✔ **Tiết kiệm thời gian** trong việc tạo nội dung video.
✔ **Cải thiện chất lượng nội dung** với giọng nói tự nhiên và thiết kế chuyên nghiệp.
✔ **Hoạt động 24/7** mà không cần can thiệp của con người.

**Hành động ngay:**
1. **Cài đặt n8n trên VPS** (để workflow chạy liên tục).
2. **Import workflow** và cấu hình theo hướng dẫn trên.
3. **Test và bật workflow** để bắt đầu tự động hóa!

**Nếu có vấn đề:** Đừng ngại comment bên dưới hoặc liên hệ với tác giả [David Olusola](https://n8n.io/workflows/4288) để hỗ trợ!

---
**🚀 Chúc các sếp thành công với việc tự động hóa nội dung video!** 🎥✨