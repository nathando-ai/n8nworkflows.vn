---
title: "🎵 Chuyển Spotify URL → MP3 & Chia Sẻ Trực Tuyến Với Google Drive (Không Cần Code)"
description: "Workflow tự động hóa hoàn toàn chuyển Spotify track thành file MP3, tải lên Google Drive và chia sẻ công khai chỉ trong vài giây - giải pháp tiết kiệm thời gian cho các sếp quản lý nội dung âm nhạc."
slug: "chuyen-spotify-url-sang-mp3-va-chia-se-google-drive"
tags: [n8n, automation, no-code, google-drive, spotify, file-management]
keywords: [n8n workflow spotify mp3, tự động hóa âm nhạc, chia sẻ file mp3 google drive, convert spotify url to mp3, tự động hóa không code]
---

# 🚀 Chuyển Spotify URL → MP3 & Chia Sẻ Trực Tuyến Với Google Drive (Không Cần Code)

### 🎧 **Nỗi đau của các sếp khi làm thủ công:**
- **Tốn thời gian:** Phải copy URL Spotify → tìm công cụ chuyển đổi → tải xuống → tổ chức file → chia sẻ link.
- **Rủi ro lỗi:** File bị mất, chất lượng âm thanh kém, hoặc không chia sẻ được với người dùng.
- **Không chuyên nghiệp:** Quá trình thủ công dễ gây ra sai sót, đặc biệt khi phải xử lý hàng loạt track.

**Workflow này giải quyết tất cả đó!** Với chỉ một form đơn giản, các sếp có thể:
✅ **Tự động hóa toàn bộ quy trình** từ Spotify URL → MP3 → Google Drive → Chia sẻ công khai.
✅ **Tiết kiệm 100% thời gian** so với cách làm thủ công.
✅ **Chất lượng ổn định** nhờ API Spotify RapidAPI và Google Drive.
✅ **Chia sẻ dễ dàng** với link công khai, không cần đăng nhập.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow hoạt động 24/7 mà không gián đoạn, các sếp nên **self-host n8n** trên VPS riêng:
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian:** Chỉ cần 5 giây để chuyển đổi và chia sẻ một track.
- **Chất lượng cao:** File MP3 được tải từ nguồn chính thức Spotify.
- **Chia sẻ công khai:** File luôn sẵn sàng chia sẻ với bất kỳ ai qua link Google Drive.
- **Dễ dàng mở rộng:** Có thể tích hợp với Slack/Telegram để thông báo kết quả.
- **An toàn:** Không cần lưu trữ file trên máy chủ của bạn.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Spotify Premium** (để sử dụng API Spotify).
2. **API Key của Spotify RapidAPI**:
   - Đăng ký tại [Spotify RapidAPI](https://rapidapi.com/apidojo/api/spotify-downloader-mp3) và lấy `x-rapidapi-key`.
3. **Tài khoản Google Drive** và **Service Account Key**:
   - Tạo **Service Account** trong Google Cloud Console và cấp quyền cho Google Drive.
   - Cấu hình **credentials** trong n8n với tên `googleApi` (hướng dẫn chi tiết ở phần sau).
4. **Folder Google Drive** để lưu trữ file MP3 (có thể là folder mặc định hoặc folder mới).

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
- **Tải file JSON** từ [liên kết gốc](https://n8n.io/workflows/6218) hoặc sử dụng mã JSON dưới đây:
  ```json
  {
    "nodes": [
      {
        "parameters": {},
        "name": "On form submission",
        "type": "formTrigger",
        "typeOptions": {
          "fields": [
            {
              "key": "url",
              "label": "Spotify Track URL",
              "type": "text"
            }
          ]
        }
      },
      {
        "parameters": {
          "waitTime": 5000
        },
        "name": "Wait",
        "type": "wait"
      },
      {
        "parameters": {
          "method": "post",
          "url": "https://spotify-downloader-mp3.p.rapidapi.com/download",
          "headers": {
            "x-rapidapi-host": "spotify-downloader-mp3.p.rapidapi.com",
            "x-rapidapi-key": "{{ $json.x_rapidapi_key }}",
            "content-type": "multipart/form-data"
          },
          "body": {
            "url": "{{ $json.url }}"
          }
        },
        "name": "Spotify Rapid Api",
        "type": "httpRequest"
      },
      {
        "parameters": {
          "method": "get",
          "url": "{{ $json.download_url }}",
          "responseFormat": "binary"
        },
        "name": "Downloader",
        "type": "httpRequest"
      },
      {
        "parameters": {
          "operation": "createFile",
          "file": "{{ $node["Downloader"].json }}",
          "name": "{{ $json.track_name }}.mp3",
          "folderId": "{{ $json.folder_id }}"
        },
        "name": "Upload Mp3 To Google Drive",
        "type": "googleDrive",
        "credentials": {
          "googleApi": {}
        }
      },
      {
        "parameters": {
          "operation": "share",
          "fileId": "{{ $node["Upload Mp3 To Google Drive"].json.body.id }}",
          "role": "writer",
          "type": "anyone"
        },
        "name": "Update Permission",
        "type": "googleDrive",
        "credentials": {
          "googleApi": {}
        }
      }
    ],
    "connections": {
      "formTrigger": {
        "main": ["Wait"]
      },
      "Wait": {
        "main": ["Spotify Rapid Api"]
      },
      "Spotify Rapid Api": {
        "main": ["Downloader"]
      },
      "Downloader": {
        "main": ["Upload Mp3 To Google Drive"]
      },
      "Upload Mp3 To Google Drive": {
        "main": ["Update Permission"]
      }
    }
  }
  ```
- **Cách import**:
  1. Mở **n8n Editor** → Nhấn **"Import"** → Chọn file JSON hoặc dán JSON vào ô **"Paste JSON"**.
  2. Nhấn **"Import"** để hoàn tất.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Các sếp cần **cấu hình kỹ lưỡng** các node sau để workflow hoạt động:

##### **Node 1: On form submission (`formTrigger`)**
- **Không cần chỉnh sửa** (form mặc định đã có field `url` để nhập Spotify URL).
- **Gợi ý**: Thêm mô tả cho field `url` như *"Nhập URL Spotify của track bạn muốn chuyển đổi"*.

##### **Node 2: Spotify Rapid Api (`httpRequest`)**
- **Tham số cần điền**:
  - **`x-rapidapi-key`**: Điền **API Key** của bạn từ RapidAPI (lấy từ [đây](https://rapidapi.com/apidojo/api/spotify-downloader-mp3)).
  - **Body**: Đảm bảo `url` được truyền từ node `formTrigger` (`{{ $json.url }}`).

##### **Node 3: Wait (`wait`)**
- **Thời gian chờ mặc định**: 5 giây (`waitTime: 5000`).
- **Lưu ý**: Nếu API phản hồi nhanh hơn, có thể giảm thời gian chờ (ví dụ: 3 giây).

##### **Node 4: Downloader (`httpRequest`)**
- **Không cần chỉnh sửa** (node này tự động lấy `download_url` từ API và tải file).

##### **Node 5: Upload Mp3 To Google Drive (`googleDrive`)**
- **Cấu hình credentials**:
  1. Trong **n8n Editor**, nhấn **"Add"** → **"Google Drive"** → **"Add"** với tên `googleApi`.
  2. Chọn **Service Account Key** (JSON) từ Google Cloud Console và cấp quyền cho Google Drive.
  3. **Folder ID**: Điền ID của folder Google Drive bạn muốn lưu file (có thể là folder mặc định).
     - **Lấy Folder ID**:
       - Mở Google Drive → Chọn folder → URL sẽ có dạng `https://drive.google.com/drive/folders/{{FOLDER_ID}}`.
       - Copy `FOLDER_ID` và điền vào `folderId` trong node.
  4. **Tên file**: Đảm bảo `track_name` được lấy từ API Spotify (thường là tên track).

##### **Node 6: Update Permission (`googleDrive`)**
- **Cấu hình quyền chia sẻ**:
  - **Role**: `writer` (người dùng có thể tải xuống và chia sẻ lại).
  - **Type**: `anyone` (không cần đăng nhập).
  - **Lưu ý**: Nếu muốn hạn chế quyền, thay `writer` thành `reader`.

---

#### **3. Kích hoạt ⚡️**
1. **Test run dữ liệu mẫu**:
   - Nhập một **Spotify URL** vào form (ví dụ: `https://open.spotify.com/track/...`).
   - Nhấn **"Execute"** để kiểm tra workflow.
   - Kiểm tra Google Drive để xác nhận file đã được tải lên và chia sẻ.
2. **Bật Active workflow**:
   - Sau khi test thành công, nhấn **"Active"** để workflow chạy tự động khi có form submission.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Tích hợp với Slack/Telegram**:
   - Sau khi file được chia sẻ, gửi thông báo qua Slack/Telegram với link download.
   - **Cách làm**:
     - Thêm node `slack` hoặc `telegram` sau node `Update Permission`.
     - Gửi thông điệp: `"File MP3 đã sẵn sàng! Link: {{ $node["Update Permission"].json.shareableUrl }}"`.

2. **Lưu log hoạt động**:
   - Thêm node `stickyNote` để ghi lại thông tin track đã xử lý (ví dụ: tên track, URL Spotify, thời gian upload).
   - **Cách làm**:
     ```json
     {
       "parameters": {
         "text": "Track: {{ $json.track_name }} đã được chuyển đổi và chia sẻ tại: {{ $node["Update Permission"].json.shareableUrl }}"
       },
       "name": "Log",
       "type": "stickyNote"
     }
     ```

3. **Tự động chia sẻ với nhóm**:
   - Sau khi file được chia sẻ, gửi email thông báo cho nhóm (ví dụ: bộ phận marketing).
   - **Cách làm**:
     - Thêm node `email` (ví dụ: Gmail) sau node `Update Permission`.
     - Gửi email với nội dung: `"Xin chào, file MP3 của track {{ $json.track_name }} đã sẵn sàng tại: {{ $node["Update Permission"].json.shareableUrl }}"`.

4. **Tạo dashboard theo dõi**:
   - Sử dụng node `googleSheets` để ghi lại tất cả các track đã chuyển đổi vào bảng tính.
   - **Cách làm**:
     - Thêm node `googleSheets` sau node `Update Permission`.
     - Cấu hình để ghi dữ liệu vào cột: `Track Name`, `Spotify URL`, `Download Link`, `Time`.

---

### 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp cần tự động hóa quy trình chuyển đổi Spotify URL → MP3 và chia sẻ file một cách nhanh chóng, không cần code. Với chỉ vài bước cấu hình, các sếp có thể **tiết kiệm thời gian, tránh sai sót và nâng cao hiệu suất công việc**.

**Hành động ngay!**
1. **Import workflow** và cấu hình credentials.
2. **Test với một track** để đảm bảo hoạt động.
3. **Bật Active** và chia sẻ với đội nhóm!

**Cần hỗ trợ?** Đừng ngần ngại comment bên dưới hoặc liên hệ với cộng đồng n8n tại [n8n Community](https://community.n8n.io/). 🚀