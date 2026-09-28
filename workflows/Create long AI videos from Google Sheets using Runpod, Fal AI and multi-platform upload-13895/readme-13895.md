---
title: "🎬 Tự Động Hóa Sáng Tạo Video AI Dài Hạng & Phát Hành Multi-Platform (Google Sheets + Runpod + Fal AI)"
description: "Workflow này tự động chuyển đổi các prompt từ Google Sheets thành video AI dài hàng, ghép các đoạn clip thành video hoàn chỉnh, và phân phối lên YouTube, Google Drive, TikTok, Instagram, Facebook & X - hoàn toàn không cần code!"
slug: "tự-dộng-hoa-tao-video-ai-dai-hang-va-phat-hanh-multi-platform"
tags: [n8n, automation, content-creation, ai-multimodal, google-sheets, youtube-automation, social-media]
keywords: [n8n workflow video ai, tự động hóa video dài, Runpod Fal AI, phân phối video multi-platform, tự động hóa content marketing]
---

# 🚀 **Tự Động Hóa Sáng Tạo Video AI Dài Hạng & Phát Hành Multi-Platform**

### **Giải pháp hoàn hảo cho các sếp Content Creator, Marketing hoặc AI Enthusiast**
Bạn đã bao giờ mệt mỏi vì phải **tạo video AI dài hàng từ đầu đến cuối**, sau đó **ghép các đoạn clip thành video hoàn chỉnh**, rồi **phân phối lên nhiều nền tảng khác nhau** như YouTube, TikTok, Instagram, Facebook và X? Hay phải **cập nhật thủ công** mỗi khi có video mới? **Workflow này sẽ giải quyết tất cả những vấn đề đó trong một cú nhấp chuột!**

Dù bạn là **nhà sáng tạo nội dung**, **quản lý marketing**, hay **nhà đầu tư AI**, workflow này sẽ **tự động hóa toàn bộ quy trình** từ **tạo video AI dài** đến **phân phối multi-platform**, giúp bạn **tiết kiệm thời gian lên đến 90%** và **tăng cường hiệu quả content marketing** một cách hiệu quả.

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo **tốc độ và tính riêng tư**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tự động hóa toàn bộ quy trình tạo video AI dài** từ prompt đến video hoàn chỉnh.
✅ **Ghép các đoạn clip thành video dài** một cách tự động.
✅ **Phân phối video lên nhiều nền tảng** (YouTube, TikTok, Instagram, Facebook, X) chỉ với một workflow.
✅ **Cập nhật tự động** khi có video mới, không cần can thiệp thủ công.
✅ **Tiết kiệm thời gian lên đến 90%** so với cách làm thủ công.
✅ **Chỉnh sửa và mở rộng dễ dàng** bằng cách cập nhật Google Sheets.
:::

---

## 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
### **1. Tài khoản và API Keys**
- **Google Sheets** (để lưu trữ prompt, duration và thông tin video).
- **Google Drive** (để lưu trữ video cuối cùng).
- **Runpod API Key** (để tạo video AI từ prompt).
- **Fal AI API Key** (để ghép video và trích xuất frame cuối cùng).
- **Upload-Post API Key** (để upload video lên YouTube).
- **Postiz API Key** (để phân phối video lên TikTok, Instagram, Facebook, X).

### **2. File Google Sheets mẫu**
- **Clone file mẫu** từ [đây](https://docs.google.com/spreadsheets/d/1MisBkHc1RmsYit1ndaPS7oOvSQV1VBMW7nyehTuiRQs/edit?usp=sharing).
- **Cập nhật thông tin** như:
  - **START** (URL hình ảnh khởi đầu cho đoạn clip).
  - **PROMPT** (prompt AI để tạo video).
  - **DURATION** (thời lượng đoạn clip).
  - **MERGE** (đánh dấu "x" nếu muốn ghép đoạn clip này vào video cuối cùng).

### **3. Các dịch vụ cần đăng ký**
- **Runpod** ([Đăng ký](https://get.runpod.io/n3witalia)) để tạo video AI.
- **Fal AI** ([Đăng ký](https://fal.ai/)) để ghép video và trích xuất frame.
- **Upload-Post** ([Đăng ký](https://www.upload-post.com/?linkId=lp_144414&sourceId=n3witalia&tenantId=upload-post-app)) để upload YouTube.
- **Postiz** ([Đăng ký](https://affiliate.postiz.com/n3witalia)) để phân phối multi-platform.

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/13895](https://n8n.io/workflows/13895).
- **Import vào n8n Editor** bằng cách:
  - Nhấn **Import** trên giao diện n8n.
  - Chọn file JSON vừa tải.
  - **Hoặc** copy toàn bộ JSON và dán vào **Import Workflow** trong n8n.

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này gồm **28 node**, các sếp cần chú ý cấu hình các node sau:

#### **🔹 Node "Get new video" (Google Sheets)**
- **Cấu hình:**
  - Chọn **Google Sheets OAuth2Api** đã thiết lập trước đó.
  - **Sheet ID** phải khớp với file Google Sheets mẫu đã clone.
  - **Range** đặt là `"Sheet1"` (hoặc tên sheet của bạn).

#### **🔹 Node "Generate video" (HTTP Request)**
- **Cấu hình:**
  - **URL:** `https://api.runpod.ai/v2/<YOUR_RUNPOD_PROJECT_ID>/run`
  - **Headers:**
    - `Authorization: Bearer <YOUR_RUNPOD_API_KEY>`
    - `Content-Type: application/json`
  - **Body (JSON):**
    ```json
    {
      "input": {
        "prompt": "${{ $node["Get new video"].json["PROMPT"] }}",
        "duration": ${{ $node["Get new video"].json["DURATION"] }},
        "start_image": ${{ $node["Get new video"].json["START"] }}
      }
    }
    ```

#### **🔹 Node "Merge videos" (HTTP Request)**
- **Cấu hình:**
  - **URL:** `https://api.fal.ai/v1/merge`
  - **Headers:**
    - `Authorization: Bearer <YOUR_FAL_AI_API_KEY>`
    - `Content-Type: application/json`
  - **Body (JSON):**
    ```json
    {
      "videos": ${{ $json["videoUrls"] }},
      "output_format": "mp4"
    }
    ```

#### **🔹 Node "Upload to YouTube" (HTTP Request)**
- **Cấu hình:**
  - **URL:** `https://www.googleapis.com/upload/youtube/v3/videos?part=snippet,status&uploadType=resumable`
  - **Headers:**
    - `Authorization: Bearer <YOUR_UPLOAD_POST_API_KEY>`
    - `Content-Type: application/json`
  - **Body (JSON):**
    ```json
    {
      "snippet": {
        "title": ${{ $node["Get new video"].json["TITLE"] }},
        "description": ${{ $node["Get new video"].json["DESCRIPTION"] }},
        "tags": ["AI", "Video", "Automation"]
      },
      "status": {
        "privacyStatus": "private"
      }
    }
    ```

#### **🔹 Node "Upload to Postiz" (Postiz Node)**
- **Cấu hình:**
  - **API Key:** Điền `postizApi` đã thiết lập trước đó.
  - **Platforms:** Chọn tất cả nền tảng (TikTok, Instagram, Facebook, X).
  - **Caption:** `${{ $node["Get new video"].json["CAPTION"] }}`
  - **Video URL:** `${{ $node["Get final video"].json["url"] }}`

#### **🔹 Node "Update video" (Google Sheets)**
- **Cấu hình:**
  - **Range:** `"Sheet1!A2:A"` (hoặc range tương ứng).
  - **Value:** `${{ $json["videoUrl"] }}` (để cập nhật URL video mới vào Google Sheets).

---

### **3. Kích hoạt ⚡️**
- **Test Run:** Chạy workflow với **dữ liệu mẫu** để kiểm tra tính năng.
- **Bật Active:** Sau khi kiểm tra thành công, **bật workflow** để tự động hóa.

---

## ✍️ **Mẹo & gợi ý nâng cao**
### **1. Tự động hóa định kỳ**
- Sử dụng **n8n Cron Trigger** để chạy workflow **mỗi ngày/lần một tuần** thay vì nhấn thủ công.

### **2. Log & Monitoring**
- Thêm **Slack/Telegram Notification** để nhận thông báo khi workflow **bắt đầu, hoàn thành hoặc gặp lỗi**.

### **3. Tối ưu hóa chất lượng video**
- **Cập nhật prompt** trong Google Sheets để **tăng chất lượng video AI**.
- **Thử nghiệm duration** khác nhau để tìm ra thời lượng tối ưu.

### **4. Phân phối video lên nhiều nền tảng khác**
- Nếu muốn **phân phối lên Pinterest hoặc LinkedIn**, thêm **Postiz Node** mới và cấu hình tương tự.

### **5. Tự động tạo thumbnail**
- Sử dụng **Fal AI API** để **trích xuất frame đầu tiên** của video và tự động tạo thumbnail.

---

## 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn **tự động hóa toàn bộ quy trình tạo và phân phối video AI dài hàng** mà **không cần code**. Bằng cách **cập nhật Google Sheets**, bạn có thể **tạo video mới, ghép chúng thành video dài, và phân phối lên nhiều nền tảng** chỉ với một cú nhấp chuột!

**Hãy áp dụng ngay và tiết kiệm thời gian cho công việc sáng tạo nội dung của mình!** 🚀

---
**🔗 [Xem video hướng dẫn chi tiết trên YouTube](https://youtube.com/@n3witalia)** (nếu các sếp muốn xem cách thiết lập cụ thể).