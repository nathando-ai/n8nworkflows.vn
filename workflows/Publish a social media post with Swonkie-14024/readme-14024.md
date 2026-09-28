---
title: "🚀 Tự Động Hóa Đăng Bài Social Media Trên Swonkie – Không Cần Code!"
description: "Workflow này giúp các sếp tự động hóa toàn bộ quy trình từ upload media đến đăng bài lên Swonkie (Facebook, Instagram, TikTok...) chỉ với 1 lần setup. Tiết kiệm thời gian lên đến 90% so với cách làm thủ công!"
slug: "tieu-dong-hoa-dang-bai-social-media-swonkie"
tags: [n8n, automation, social media, swonkie, no-code]
keywords: [n8n workflow social media, tự động hóa đăng bài Swonkie, API Swonkie, tự động hóa marketing digital, tự động hóa Facebook Instagram]
---

# 🚀 **Tự Động Hóa Đăng Bài Social Media Trên Swonkie – Không Cần Code!**

### **Giải pháp cho các sếp bị "đóng băng" vì đăng bài thủ công**
Hãy tưởng tượng: Bạn phải:
✅ **Tải hình ảnh/video lên** Swonkie (hoặc các nền tảng khác)
✅ **Kiểm tra lại caption** để đảm bảo không vi phạm quy định
✅ **Chờ media xử lý** (thường mất từ 5-30 phút)
✅ **Đăng bài ngay hoặc lịch trình** theo kế hoạch
✅ **Lặp lại quy trình này hàng ngày** cho nhiều tài khoản khác nhau

**Thời gian tiêu tốn?** **Tối thiểu 30 phút/ngày** cho mỗi bài đăng! Với **n8n**, bạn có thể **tự động hóa toàn bộ quy trình này chỉ trong vài phút** – **không cần viết một dòng code nào!**

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động **ổn định 24/7** (đặc biệt khi đăng bài theo lịch), các sếp nên **self-host n8n** trên VPS riêng:
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** – giảm tới **39%**)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (đủ sức mạnh cho workflow này)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: **Tự động hóa 100% quy trình** từ upload media đến đăng bài.
- **Chính xác 100%**: Không còn lo lắng về **vi phạm quy định caption**, **media không hợp lệ**, hoặc **bài đăng bị treo**.
- **Hoạt động liên tục**: **Đăng bài tự động** theo lịch (ví dụ: 8h sáng, 12h trưa, 6h chiều) **mặc dù bạn đang ngủ**.
- **Dễ dàng mở rộng**: **Kết hợp với Slack/Telegram** để thông báo khi bài đăng thành công/thất bại.
- **Lưu log toàn bộ quá trình**: **Theo dõi được trạng thái media**, **lịch sử đăng bài**, và **sửa lỗi nhanh chóng**.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
✅ **Tài khoản Swonkie** (đăng ký tại [app.swonkie.com](https://app.swonkie.com/))
✅ **API Key & App ID** của Swonkie:
   - Mở [Cài đặt công việc](https://app.swonkie.com/settings/workspace/public-api) → **Public API**
   - Lấy **App ID** và **API Key** (sẽ dùng trong **node Configure**)
✅ **Profile ID** của tài khoản social muốn đăng bài:
   - Gửi **GET /profiles** (API endpoint) để lấy danh sách profile.
   - Chọn **Profile ID** của tài khoản cần đăng bài.
✅ **Media URL** (hình ảnh/video công khai):
   - **Không được là file private** (n8n sẽ tải xuống và upload lên Swonkie).
   - **Định dạng hỗ trợ**: JPG, PNG, MP4, GIF (kiểu file lớn hơn 50MB cần kiểm tra lại).
✅ **Caption** (nội dung bài đăng):
   - **Kiểm tra độ dài** (mỗi nền tảng có giới hạn khác nhau).
   - **Không chứa link** (nếu muốn thêm link, cần xử lý thêm trong workflow).

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
**Cách 1: Import từ file JSON**
1. Tải workflow từ [n8n.io/workflows/14024](https://n8n.io/workflows/14024) (chọn **Download JSON**).
2. Mở **n8n Editor** → Nhấn **Import** → Chọn file JSON vừa tải.
3. **Hoặc** copy toàn bộ JSON từ [đây](https://n8n.io/workflows/14024) (chọn **Copy JSON**) và **paste** vào **Import Workflow** trong n8n.

**Cách 2: Copy/paste JSON trực tiếp**
- Mở **n8n Editor** → Nhấn **Import** → Chọn **Paste JSON** → Dán toàn bộ mã từ [n8n.io/workflows/14024](https://n8n.io/workflows/14024).

---

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này **phức tạp** vì phải **upload media trước khi đăng bài**, nhưng **không lo** – chỉ cần làm theo hướng dẫn dưới đây:

##### **A. Cấu hình node "Configure" (QUAN TRỌNG NHẤT!)**
Mở node **"Configure"** (type: **Set**) và điền thông tin:
| Tham số | Giá trị | Ghi chú |
|---------|---------|---------|
| **apiId** | `YOUR_APP_ID` | Lấy từ [Cài đặt Swonkie](https://app.swonkie.com/settings/workspace/public-api) |
| **apiKey** | `YOUR_API_KEY` | Lấy từ [Cài đặt Swonkie](https://app.swonkie.com/settings/workspace/public-api) |
| **profileId** | `123456789` | Lấy từ API endpoint `GET /profiles` |
| **caption** | `Bài đăng của tôi` | Nội dung bài đăng (không quá giới hạn của nền tảng) |
| **stage** | `publishNow` (mặc định) hoặc `schedule` | - `publishNow`: Đăng tức thì <br> - `schedule`: Cần thiết lập `publishAt` (thời gian đăng) |
| **mediaUrl** | `https://tudonghoa.vn/image.jpg` | Link hình ảnh/video **công khai** |
| **mediaName** | `photo.jpg` | Tên file (không ảnh hưởng nhiều, nhưng nên điền chính xác) |

##### **B. Cấu hình an toàn cho API Key (Nên làm!)**
:::warning[LƯU Ý AN TOÀN]
**Không nên để API Key trong plain text** trong workflow (n8n sẽ lưu log). **Làm theo cách này để an toàn:**
1. Mở **Credentials** trong n8n (nhấn **⚙️ Settings** → **Credentials**).
2. Tạo **Generic Credential** mới:
   - **Name**: `Swonkie_API`
   - **Type**: `Header Auth`
   - **Headers**:
     - `X-API-ID`: `YOUR_APP_ID`
     - `X-API-KEY`: `YOUR_API_KEY`
3. **Thay thế** tất cả các node `httpRequest` bằng cách:
   - Mở node `httpRequest` → Tab **Credentials** → Chọn `Swonkie_API` vừa tạo.
   - **Xóa** các tham số `apiId` và `apiKey` trong **Headers** của node.

---
##### **C. Cấu hình node "Create Post" (Nếu muốn lịch trình)**
Nếu chọn **`stage: schedule`**, cần thêm **`publishAt`** (thời gian đăng bài):
- Mở node **"Create Post"** (type: `httpRequest`).
- Trong **Body**, thêm:
  ```json
  {
    "caption": "{{ $json.caption }}",
    "mediaId": "{{ $json.mediaId }}",
    "profileId": "{{ $json.profileId }}",
    "stage": "schedule",
    "publishAt": "2024-12-31T12:00:00Z"  // Thay đổi thành thời gian muốn đăng
  }
  ```

##### **D. Test Run & Kích hoạt**
1. **Nhấn "Run"** để test với dữ liệu mẫu.
2. **Kiểm tra các node quan trọng**:
   - **"Media Ready?"** (nếu media không xử lý thành công, workflow sẽ **dừng và báo lỗi**).
   - **"Post Valid?"** (nếu bài đăng không hợp lệ, workflow sẽ **dừng và báo lỗi**).
3. **Bật "Active"** để workflow chạy tự động khi được **manual trigger**.

---

### ✍️ **Mẹo & gợi ý nâng cao**
#### **1. Kết hợp với Slack/Telegram để thông báo**
- Thêm **node Slack/Telegram** sau **"Post Published"** để nhận thông báo khi bài đăng thành công.
- **Cách làm**:
  1. Tạo **Generic Credential** cho Slack/Telegram.
  2. Thêm node **`n8n-nodes-base.slack`** hoặc **`n8n-nodes-base.telegram`**.
  3. Gửi tin nhắn:
     ```json
     {
       "text": `📢 Bài đăng thành công!\nPost ID: {{ $json.postId }}\nTrạng thái: {{ $json.stage }}`
     }
     ```

#### **2. Lưu log vào Google Sheets/Notion**
- Thêm **node `n8n-nodes-base.googleSheets`** sau **"Post Published"** để lưu log:
  - **Sheet Name**: `Social Media Logs`
  - **Range**: `A1` (để ghi dữ liệu mới vào hàng mới)
  - **Data**:
    ```json
    {
      "postId": "{{ $json.postId }}",
      "caption": "{{ $json.caption }}",
      "mediaName": "{{ $json.mediaName }}",
      "status": "Published",
      "timestamp": "{{ $json.timestamp }}"
    }
    ```

#### **3. Xử lý lỗi media tự động**
- Nếu media bị lỗi (ví dụ: quá lớn), workflow sẽ **dừng và báo lỗi**.
- **Cách khắc phục**:
  - Thêm **node `n8n-nodes-base.if`** sau **"Media Processing Failed"** để gửi **email thông báo** (sử dụng **node `n8n-nodes-base.email`**).
  - **Cấu hình email**:
    ```json
    {
      "to": "email@cua-ban.com",
      "subject": "Lỗi upload media: {{ $json.error }}",
      "text": `File: {{ $json.mediaName }} không được xử lý thành công. Lỗi: {{ $json.error }}`
    }
    ```

#### **4. Đăng bài cho nhiều profile cùng lúc**
- Sử dụng **node `n8n-nodes-base.set`** trước **"Create Post"** để **lặp qua nhiều profile**:
  ```json
  {
    "profileIds": ["123456789", "987654321"],  // Danh sách Profile ID
    "caption": "{{ $json.caption }}",
    "mediaUrl": "{{ $json.mediaUrl }}"
  }
  ```
- Sau đó, sử dụng **node `n8n-nodes-base.loop`** để chạy workflow cho từng profile.

---

### 📌 **Kết luận**
Workflow này **giải phóng thời gian** của các sếp để tập trung vào **strategy marketing** thay vì **quản lý bài đăng thủ công**. Với **n8n**, bạn có thể:
✅ **Đăng bài tự động** theo lịch.
✅ **Tự động xử lý lỗi** media và caption.
✅ **Lưu log toàn bộ quá trình** để theo dõi hiệu quả.
✅ **Kết hợp với Slack/Email** để thông báo kết quả.

**Hành động ngay!**
1. **Import workflow** theo hướng dẫn trên.
2. **Cấu hình API Key** và **Profile ID**.
3. **Test run** và **bật Active**.
4. **Thêm Slack/Google Sheets** để theo dõi.

**🚀 Bắt đầu tự động hóa ngay hôm nay – không cần code!** 🚀