---
title: "🎧 Tự Động Hoá Sáng Tạo & Đăng Video ASMR AI lên YouTube Shorts - Không Cần Code!"
description: "Workflow này tự động sinh ra nội dung ASMR độc đáo, tạo âm thanh & video bằng AI, sau đó đăng lên YouTube Shorts 24/7. Giúp các sếp tiết kiệm 100+ giờ/tháng và mở rộng kênh YouTube một cách tự động hóa hoàn toàn."
slug: "tieu-dong-hoa-sang-tao-asmr-ai-len-youtube-shorts"
tags: [n8n, automation, ai-content-creation, youtube-automation, asmr, no-code]
keywords: [n8n workflow asmr, tự động hóa video youtube, ai tạo video, seedance fal ai, gpt-4 youtube shorts]
---

# 🚀 **Tự Động Hoá Sáng Tạo & Đăng Video ASMR AI lên YouTube Shorts - Không Cần Code!**

### **Giải pháp cho các sếp muốn:**
- **Tạo nội dung ASMR 24/7** mà không cần viết script, quay video hay chỉnh sửa?
- **Tiết kiệm 100+ giờ/tháng** mà vẫn giữ chất lượng cao?
- **Mở rộng kênh YouTube** với hàng ngàn video Shorts tự động, mỗi ngày?
- **Không cần kỹ năng code** nhưng vẫn muốn tự động hóa toàn bộ quy trình từ ý tưởng đến đăng tải?

Workflow này **chỉ cần cài đặt 1 lần**, sau đó **chạy tự động** mỗi khi bạn muốn (hoặc theo lịch trình) để sinh ra video ASMR độc đáo, tải lên YouTube Shorts, và gửi thông báo ngay khi video được đăng tải. **Không cần can thiệp thủ công!**

---
## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động sinh ra **10+ video/ngày** mà không cần viết script hay quay video.
- **Nội dung độc đáo**: Sử dụng AI GPT-4 + Seedance (ByteDance) + Fal AI để tạo **âm thanh & video ASMR** theo xu hướng mới nhất.
- **Tự động đăng tải**: Video được tự động **tải lên YouTube Shorts** và cập nhật vào Google Sheet theo dõi.
- **Quản lý dễ dàng**: **Google Sheet** làm "hệ thống quản lý nội dung" (CMS), giúp theo dõi tất cả video từ ý tưởng đến đăng tải.
- **Thông báo tức thời**: Nhận **tin nhắn Telegram/Gmail** khi video mới được đăng tải.
- **Không giới hạn sáng tạo**: AI tự động **tạo ý tưởng mới**, **tạo âm thanh**, **chỉnh video**, và **đăng tải** một cách hoàn toàn tự động.
:::

---
## 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Để workflow này hoạt động, các sếp cần chuẩn bị:
### **1. Tài khoản & API Keys**
| Dịch vụ/API | Mô tả | Làm thế nào để lấy? |
|-------------|--------|---------------------|
| **OpenAI API** | Dùng cho AI GPT-4 tạo ý tưởng và kế hoạch sản xuất | [Đăng ký tại OpenAI](https://platform.openai.com/account/api-keys) |
| **Seedance (Wavespeed AI)** | Tạo video từ mô tả bằng AI | [Đăng ký tại Wavespeed](https://wavespeed.ai/) |
| **Fal AI** | Tạo âm thanh & hiệu ứng âm thanh cho video | [Đăng ký tại Fal AI](https://fal.ai/) |
| **Google Cloud** | Dùng cho Google Sheets & YouTube API | [Tạo dự án Google Cloud](https://console.cloud.google.com/) và kích hoạt: <br> - **Google Sheets API** <br> - **YouTube Data API v3** |
| **YouTube OAuth 2.0** | Đăng tải video lên kênh YouTube | [Tạo OAuth 2.0 cho YouTube](https://developers.google.com/youtube/v3/getting-started) |
| **Telegram Bot** | Gửi thông báo khi video mới được đăng tải | [Tạo Bot Telegram](https://core.telegram.org/bots) |
| **Gmail OAuth 2.0** (Tùy chọn) | Gửi email thông báo | [Tạo OAuth 2.0 cho Gmail](https://developers.google.com/gmail/api/quickstart/python) |

### **2. Google Sheet quản lý nội dung**
- Tạo **1 bảng Google Sheets** với các cột sau:
  - `id` (ID duy nhất cho mỗi video)
  - `idea` (ý tưởng ASMR ban đầu)
  - `caption` (tiêu đề video)
  - `production_status` (trạng thái: "Đang xử lý", "Hoàn thành", "Lỗi")
  - `environment_prompt` (mô tả môi trường video)
  - `sound_prompt` (mô tả âm thanh)
  - `final_output` (link video sau khi hoàn thành)
  - `youtube_url` (link YouTube Shorts)

  **Mẫu Google Sheet**:
  ![Mẫu Google Sheet](https://i.imgur.com/xyz1234.png) *(Hình ảnh tham khảo)*

### **3. Kênh YouTube**
- **Kênh YouTube** cần được kết nối với OAuth 2.0 để tự động đăng tải video.
- **Chế độ "Unlisted"** hoặc **"Public"** tùy chọn (khuyến nghị **Shorts** để tối ưu SEO).

---
## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. **Tải workflow** từ [n8n.io/workflows/5110](https://n8n.io/workflows/5110) (ấn nút "Download").
2. **Mở n8n Editor** trên máy chủ tự host của bạn.
3. **Nhấn "Import"** và chọn file JSON vừa tải.
4. **Chọn "Create Workflow"** để lưu vào hệ thống.

#### **Phương pháp 2: Copy/Paste JSON**
1. **Mở n8n Editor** và tạo **workflow mới**.
2. **Nhấn "Import"** → Chọn "Paste JSON".
3. **Dán toàn bộ JSON** từ [n8n.io/workflows/5110](https://n8n.io/workflows/5110) (ấn "View Source" trên trang workflow).
4. **Nhấn "Import"** để hoàn tất.

---
### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này **phức tạp** và cần **cấu hình cẩn thận** các node sau:

#### **🔹 Node "Schedule Trigger" (Động cơ kích hoạt theo lịch)**
- **Cấu hình**:
  - **Time Zone**: Chọn múi giờ phù hợp (ví dụ: `Asia/HoChiMinh`).
  - **Frequency**: Thiết lập thời gian chạy (ví dụ: **mỗi 6 giờ** để tránh bị chặn API).
  - **Example**: `0 0 */6 * *` (chạy lúc 00:00, 06:00, 12:00, 18:00 hàng ngày).

#### **🔹 Node "OpenAI Chat Model" (GPT-4 tạo ý tưởng)**
- **Cấu hình**:
  - **Credentials**: Chọn `openAiApi` (đã tạo trước đó).
  - **Model**: Đảm bảo chọn `gpt-4.1` (hoặc `gpt-4-turbo` nếu có).
  - **System Message**: **Không chỉnh sửa** (nếu muốn giữ phong cách mặc định). Nếu muốn **tạo phong cách riêng**, chỉnh sửa ở:
    ```json
    {
      "role": "system",
      "content": "Bạn là một AI chuyên tạo nội dung ASMR. Hãy sinh ra ý tưởng video ngắn, thú vị và có khả năng viral. Mô tả chi tiết về môi trường, âm thanh, và kịch bản."
    }
    ```

#### **🔹 Node "Seedance (Create Sounds)" & "Fal AI (Create Clips)"**
- **Cấu hình**:
  - **Headers**: Thêm `Authorization: Bearer {API_KEY}` (thay `{API_KEY}` bằng API Key của Seedance/Fal AI).
  - **Body (JSON)**:
    ```json
    {
      "prompt": "${{ $json['environment_prompt'] }}",
      "style": "ASMR",
      "duration": 10
    }
    ```
  - **Lưu ý**:
    - **Seedance** có giới hạn **1000 credit/ngày**. Nếu vượt quá, API sẽ trả về lỗi `429 Too Many Requests`.
    - **Fal AI** cũng có giới hạn. **Không chạy quá 10 lần/phút** để tránh bị chặn.

#### **🔹 Node "YouTube Upload"**
- **Cấu hình**:
  - **Credentials**: Chọn `youTubeOAuth2Api`.
  - **File Video**: Chọn `Download Final Video` (node trước đó).
  - **Title**: `${{ $json['caption'] }}` (tự động lấy từ Google Sheet).
  - **Description**: `${{ $json['idea'] }}` (mô tả chi tiết).
  - **Tags**: `ASMR, Shorts, Relaxing, [thêm tags phù hợp]`.
  - **Privacy Status**: `public` (để tối ưu SEO).

#### **🔹 Node "Google Sheets" (Log & Update)**
- **Cấu hình**:
  - **Credentials**: Chọn `googleSheetsOAuth2Api`.
  - **Sheet Name**: Tên bảng Google Sheets của bạn.
  - **Range**: `${{ $json['id'] }}` (để cập nhật hàng tương ứng).
  - **Values**: Cập nhật các cột như `final_output`, `youtube_url`, `production_status`.

---
### **3. Kích hoạt ⚡️**
1. **Test Run** (để kiểm tra lỗi):
   - Nhấn **Run Workflow** và chọn **1 hàng mẫu** trong Google Sheet.
   - Kiểm tra:
     - AI có tạo ý tưởng không?
     - Video có tạo thành công không?
     - Video có upload lên YouTube không?
     - Thông báo Telegram/Gmail có hoạt động không?

2. **Bật Active**:
   - Sau khi test thành công, **bật "Active"** cho **Schedule Trigger**.
   - **Kiểm tra log** trong n8n để đảm bảo không có lỗi.

---
## ✍️ **Mẹo & gợi ý nâng cao**
### **🔹 Tối ưu hóa API để tránh bị chặn**
- **Thêm delay** giữa các API call:
  ```json
  {
    "operation": "wait",
    "time": 30000 // 30 giây
  }
  ```
- **Sử dụng `batchInterval`** trong HTTP Request:
  ```json
  {
    "batchInterval": 60000 // 1 phút giữa các request
  }
  ```

### **🔹 Tăng tính cá nhân hóa**
- **Chỉnh sửa Prompts** trong node `Prompts AI Agent` để:
  - **Tạo phong cách riêng** (ví dụ: ASMR "ngủ ngon", "ăn ngon", "chăm sóc da").
  - **Thêm keyword xu hướng** (ví dụ: "ASMR 2024", "ASMR sleep", "ASMR eating").
- **Ví dụ Prompt cá nhân hóa**:
  ```json
  {
    "role": "system",
    "content": "Tạo nội dung ASMR theo phong cách **relaxing + food** (ăn ngon). Mô tả chi tiết về âm thanh cắn, nhai, và môi trường ấm áp."
  }
  ```

### **🔹 Lưu log & theo dõi hiệu suất**
- **Thêm node `Sticky Note`** để ghi lại lỗi:
  ```json
  {
    "name": "Log Error",
    "type": "stickyNote",
    "options": {
      "content": "Lỗi tại node: ${{ $node.error.name }} - Lỗi: ${{ $node.error.message }}"
    }
  }
  ```
- **Sử dụng Google Analytics** để theo dõi lượt xem video.

### **🔹 Tích hợp với Slack/Telegram**
- **Thay thế Gmail bằng Slack**:
  - Sử dụng node `slack` với webhook Slack.
  - **Thông báo mẫu**:
    ```json
    {
      "text": "🎉 Video mới được đăng tải!\nTên: ${{ $json['caption'] }}\nLink: ${{ $json['youtube_url'] }}"
    }
    ```

### **🔹 Tự động xóa video lỗi**
- **Thêm node `if`** để kiểm tra `production_status`:
  - Nếu `production_status = "Lỗi"`, **xóa video** từ YouTube:
    ```json
    {
      "operation": "delete",
      "resource": "video",
      "id": "${{ $json['youtube_video_id'] }}"
    }
    ```

---
## 📌 **Kết luận**
Workflow này là **công cụ tự động hóa hoàn chỉnh** để các sếp:
✅ **Tạo video ASMR AI** mà không cần viết script.
✅ **Tải lên YouTube Shorts** 24/7.
✅ **Quản lý toàn bộ quy trình** trên Google Sheet.
✅ **Nhận thông báo tức thời** khi video mới được đăng tải.

**Không cần là nhà phát triển**, chỉ cần **cài đặt và chạy** là xong! **Hãy tự động hóa kênh YouTube của mình ngay hôm nay!**

---
### **🎁 Bonus: Đăng ký VPS để chạy workflow 24/7**
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7**, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**🚀 Bắt đầu tự động hóa ngay!** Nếu có vấn đề, hãy liên hệ với tác giả tại **bilsimaging@gmail.com**.