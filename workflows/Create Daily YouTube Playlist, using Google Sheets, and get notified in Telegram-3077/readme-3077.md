---
title: "🎵 **Tự Động Hoàn Chỉnh Danh Sách YouTube Hàng Ngày Với Google Sheets & Telegram - Không Cần Code!**"
description: "Workflow này tự động tạo danh sách YouTube mới hàng ngày từ các kênh được theo dõi, xóa danh sách cũ, và gửi thông báo hoàn thành qua Telegram. Giúp tiết kiệm thời gian và tối ưu hóa quản lý nội dung video."
slug: "tay-dong-hoan-chinh-danh-sach-youtube-hang-ngay"
tags: [n8n, automation, youtube, google-sheets, telegram, no-code, self-hosted]
keywords: [tự động hóa youtube, danh sách video hàng ngày, google sheets api, telegram notification, n8n workflow youtube]
---

# 🎵 **Tự Động Hoàn Chỉnh Danh Sách YouTube Hàng Ngày Với Google Sheets & Telegram**

## **Giới Thiệu**
Bạn có bao giờ phải **tìm kiếm, chọn lọc và thêm video mới** vào danh sách YouTube hàng ngày một cách thủ công? Hoặc phải **quan sát nhiều kênh** để cập nhật nội dung mới nhất? Với **workflow này**, các sếp có thể **tự động hóa toàn bộ quá trình** chỉ trong vài phút mỗi ngày, mà không cần viết một dòng code nào!

Workflow này sẽ:
✅ **Tự động lấy video mới nhất** từ các kênh YouTube được theo dõi (trong vòng 24h).
✅ **Xóa danh sách cũ** (ngày hôm qua) để tránh trùng lặp.
✅ **Tạo danh sách mới** với tên theo định dạng `YYMMDD_DanhSáchTên`.
✅ **Gửi thông báo hoàn thành** qua Telegram để các sếp không bỏ lỡ bất kỳ cập nhật nào.

---
### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần phải thủ công tìm video và thêm vào danh sách hàng ngày.
- **Chính xác & tự động**: Chỉ lấy video mới nhất trong 24h, tránh trùng lặp.
- **Cá nhân hóa**: Thêm tên kênh và định dạng ngày để dễ quản lý.
- **Hoạt động liên tục**: Chạy tự động hàng ngày (hoặc theo lịch) mà không cần can thiệp.
- **Thông báo tức thời**: Nhận tin nhắn Telegram khi danh sách mới được tạo.
:::

---
## 🎯 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
### **1. Tài khoản & API Keys**
| **Dịch vụ**       | **Thao tác cần thực hiện**                                                                 |
|-------------------|--------------------------------------------------------------------------------------------|
| **Google Sheets**  | - Tạo một bảng Google Sheets với **4 cột**: `Channel User Name`, `Channel Name`, `Channel Link`, `Channel ID`. <br> - Cài đặt **OAuth 2.0** trong n8n (tạo `googleSheetsOAuth2Api`). |
| **YouTube API**    | - Tạo **API Key** và **OAuth 2.0 Client ID** trên [Google Cloud Console](https://console.cloud.google.com/). <br> - Cài đặt trong n8n với tên `youTubeOAuth2Api`. |
| **Telegram Bot**   | - Tạo một bot Telegram mới và lấy **API Token** từ [@BotFather](https://t.me/BotFather). <br> - Cài đặt trong n8n với tên `telegramApi`. |
| **VPS (Self-hosted)** | - Cài đặt n8n trên máy chủ riêng để workflow chạy 24/7. <br> 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%). |

### **2. Bảng Google Sheets chuẩn bị**
Các sếp cần tạo một bảng với **4 cột đầu tiên** như sau:
| **Channel User Name** | **Channel Name**       | **Channel Link**                     | **Channel ID**       |
|----------------------|------------------------|-------------------------------------|----------------------|
| @CorporalStock       | Recruit Training Videos | [https://www.youtube.com/@CorporalStock](https://www.youtube.com/@CorporalStock) | UC... (ID kênh) |

:::note[LƯU Ý]
- **Cột `Channel User Name`** phải chứa **@ + tên kênh** (ví dụ: `@TechMaster`).
- **Cột `Channel ID`** có thể lấy từ URL kênh YouTube (ví dụ: `UC...` trong `https://www.youtube.com/@TechMaster`).
- **Workflow này sẽ tự động điền `Channel Link` và `Channel ID`** sau khi chạy workflow **"Create your Channel List"** (xem phần **Cách import & Lưu ý**).
:::

---
## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
Các sếp có thể:
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/3077) và import vào n8n Editor.
- **Copy & Paste JSON** từ file vào n8n (đảm bảo không có lỗi syntax).

:::info[LINK TẢI FILE JSON]
👉 [Tải workflow này](https://n8n.io/workflows/3077) (chọn **Export as JSON**).
:::

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này được chia thành **5 phần chính**. Các sếp cần **cấu hình kỹ lưỡng** các node sau:

#### **🔹 Phần 1: Khởi động & Lấy danh sách kênh**
- **Node `0715 Trigger` (ScheduleTrigger)**:
  - Đặt lịch chạy hàng ngày (ví dụ: **8h sáng**).
  - **Lưu ý**: Nếu muốn chạy thủ công, có thể sử dụng **`When clicking ‘Test workflow’` (ManualTrigger)**.

- **Node `Read Channel Names` & `Read Channel Names1` (Google Sheets)**:
  - **Chọn sheet** và **range** là `Sheet1!A1:D` (hoặc tên sheet của các sếp).
  - **Credentials**: Chọn `googleSheetsOAuth2Api` (đã cài đặt trước).

#### **🔹 Phần 2: Lấy video mới từ kênh**
- **Node `Get Videos` (HTTP Request)**:
  - **Method**: `GET`
  - **URL**: `https://www.googleapis.com/youtube/v3/search?part=snippet&channelId={channelId}&maxResults=8&order=date&type=video`
  - **Headers**:
    ```json
    {
      "Authorization": "Bearer {{ $json["access_token"] }}",
      "Content-Type": "application/json"
    }
    ```
    (Lấy `access_token` từ `youTubeOAuth2Api`).
  - **Dynamic Data**: Chọn `Channel ID` từ Google Sheets.

- **Node `Filter Out Upcoming` (Filter)**:
  - **Condition**: Lọc video **có ngày upload trong 24h** (sử dụng `{{ $node["Get Videos"].json["items"][0]["snippet"]["publishedAt"] }}`).

#### **🔹 Phần 3: Xóa danh sách cũ (ngày hôm qua)**
- **Node `Delete Old Playlist` (YouTube)**:
  - **Lưu ý quan trọng**: **Không kích hoạt node này lần đầu tiên** (nếu không, workflow sẽ lỗi vì không có danh sách cũ).
  - **Credentials**: `youTubeOAuth2Api`.
  - **Key Parameters**:
    ```json
    {
      "operation": "delete",
      "resource": "playlist",
      "id": "{{ $json["id"] }}" (lấy từ Google Sheets, cột Playlist ID ngày hôm qua)
    }
    ```

#### **🔹 Phần 4: Tạo danh sách mới**
- **Node `Create Playlist` (YouTube)**:
  - **Credentials**: `youTubeOAuth2Api`.
  - **Key Parameters**:
    ```json
    {
      "operation": "create",
      "resource": "playlist",
      "snippet": {
        "title": "{{ $json["date"] }}_DanhSáchVideoHômNay",
        "description": "Danh sách video mới nhất từ các kênh được theo dõi"
      }
    }
    ```
    (Thay `{{ $json["date"] }}` bằng định dạng `YYMMDD`).

- **Node `YouTube` (Add to Playlist)**:
  - **Credentials**: `youTubeOAuth2Api`.
  - **Key Parameters**:
    ```json
    {
      "resource": "playlistItem",
      "snippet": {
        "playlistId": "{{ $json["playlistId"] }}",
        "resourceId": {
          "kind": "youtube#video",
          "videoId": "{{ $node["Get Videos"].json["items"][0]["id"]["videoId"] }}"
        }
      }
    }
    ```

#### **🔹 Phần 5: Lưu Playlist ID & Gửi thông báo Telegram**
- **Node `Save Playlist ID` (Google Sheets)**:
  - **Operation**: `update`
  - **Range**: `Sheet1!E1` (cột Playlist ID).
  - **Value**: `{{ $json["id"] }}` (ID danh sách mới).

- **Node `Telegram` (Telegram Bot)**:
  - **Credentials**: `telegramApi`.
  - **Message**:
    ```
    🚀 Danh sách YouTube mới đã được tạo thành công!
    Ngày: {{ $json["date"] }}
    Link danh sách: https://www.youtube.com/playlist?list={{ $json["playlistId"] }}
    ```

---
### **3. Kích hoạt ⚡️**
1. **Test run** với dữ liệu mẫu:
   - Chạy **ManualTrigger** để kiểm tra logic.
   - Kiểm tra **Google Sheets** và **Telegram** để xác nhận kết quả.
2. **Bật Active workflow**:
   - Đảm bảo **ScheduleTrigger** được kích hoạt và lịch chạy đúng giờ.

---
## ✍️ **Mẹo & gợi ý nâng cao**
### **1. Tạo workflow riêng để cập nhật danh sách kênh**
- **Workflow "Create your Channel List"** (nêu trong hướng dẫn gốc) cần được **tách riêng** và chạy khi thêm kênh mới.
- **Cách làm**:
  - Tạo một workflow mới với **Google Sheets** và **HTTP Request** để lấy `Channel ID` từ `@username`.
  - **Lưu ý**: Cần **tham khảo API YouTube** để lấy `Channel ID` từ tên kênh.

### **2. Lưu log hoạt động**
- Thêm **node `StickyNote`** để ghi lại lịch sử hoạt động (ví dụ: ngày tạo, số video, lỗi nếu có).

### **3. Gửi báo cáo định kỳ**
- Sử dụng **node `Telegram`** để gửi **báo cáo tuần/month** về số video được thêm vào danh sách.

### **4. Kết hợp với Slack**
- Thay vì Telegram, các sếp có thể **gửi thông báo qua Slack** bằng node `slack`.

---
## 📌 **Kết luận**
Với **workflow này**, các sếp đã **tự động hóa hoàn toàn quá trình quản lý danh sách YouTube**, tiết kiệm **gần 1 giờ mỗi ngày** và tránh sai sót thủ công. **Không cần code**, chỉ cần **cấu hình và chạy** là xong!

👉 **Bắt đầu ngay**:
1. **Chuẩn bị tài khoản** (Google Sheets, YouTube API, Telegram).
2. **Import workflow** và **cấu hình các node**.
3. **Kích hoạt lịch chạy hàng ngày**.
4. **Nhận danh sách mới mỗi sáng** cùng với thông báo Telegram!

---
**💡 Cần hỗ trợ?** Hãy để lại comment bên dưới hoặc liên hệ với cộng đồng n8n tại [n8n Community](https://community.n8n.io/). Chúc các sếp thành công! 🚀