---
title: "🚀 Tự Động Hoàn Chỉnh Upload Video YouTube Theo Lịch Trình 12h (JST) - Không Cần Code"
description: "Workflow tự động hóa upload video YouTube với khoảng cách 12h giữa các video, tự động hóa toàn bộ quy trình từ danh sách video đến lịch trình và playlist - tiết kiệm thời gian lên tới 80% cho các sếp content creator."
slug: "tuy-dong-hoa-upload-video-youtube-12h-jst"
tags: [n8n, automation, youtube, social-media, no-code]
keywords: [tự động hóa youtube, upload video tự động, lịch trình upload youtube, n8n workflow youtube, tự động hóa content creator]
---

# 🚀 **Tự Động Hoàn Chỉnh Upload Video YouTube Theo Lịch Trình 12h (JST) - Không Cần Code**

### **Giải pháp cho các sếp content creator muốn tự động hóa toàn bộ quy trình upload video YouTube**
Hãy tưởng tượng: **không cần phải nhớ thời gian upload, không cần phải lên lịch thủ công, và video của bạn được tự động phân bố đều nhau trên kênh** - với khoảng cách **12h giữa các video** (theo giờ JST). Workflow này sẽ **tự động hóa toàn bộ quy trình**, từ **danh sách video** đến **lịch trình upload** và **thêm vào playlist**, giúp bạn **tiết kiệm thời gian lên tới 80%** và **tăng cường sự nhất quán** cho kênh YouTube của mình.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn**: Không cần nhớ thời gian upload, không cần lên lịch thủ công.
- **Lịch trình 12h đều đặn**: Video được phân bố đều nhau trên kênh, tối ưu hóa SEO và engagement.
- **Tiết kiệm thời gian**: Giảm thiểu công việc thủ công lên tới **80%**.
- **Tự động thêm vào playlist**: Video mới được tự động thêm vào playlist đã chọn, giúp quản lý nội dung dễ dàng hơn.
- **Hoạt động liên tục**: Workflow chạy 24/7 trên VPS, không phụ thuộc vào thiết bị cá nhân.
:::

---

### 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
1. **Tài khoản YouTube** với quyền quản trị kênh.
2. **API Key OAuth2 của YouTube** (cấu hình trong n8n dưới tên `youTubeOAuth2Api`).
3. **Danh sách video** (file `.mp4` hoặc `.mov`) được lưu trong **một thư mục cụ thể** trên máy chủ VPS.
4. **Playlist YouTube** để video mới được tự động thêm vào.
5. **n8n Self-hosted** (cài đặt trên VPS để workflow hoạt động liên tục).
:::

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. **Tải file JSON** từ [đây](https://n8n.io/workflows/10098) (hoặc copy JSON từ link trên).
2. Trong **n8n Editor**, nhấn **Import Workflow** và dán JSON vào.
3. **Kích hoạt workflow** bằng cách bật nút **Active** ở góc trên bên phải.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này bao gồm **8 node chính**, các sếp cần **cấu hình kỹ lưỡng** các phần sau:

##### **A. Cấu hình OAuth2 YouTube (Quá trình này chỉ cần làm 1 lần)**
- Trong **n8n**, đi đến **Credentials** → **Add Credential** → Chọn **YouTube OAuth2**.
- Điền thông tin:
  - **Client ID** và **Client Secret** từ [Google Cloud Console](https://console.cloud.google.com/).
  - **Scopes**: Chọn `https://www.googleapis.com/auth/youtube.upload` và `https://www.googleapis.com/auth/youtube.force-ssl`.
  - **Name**: Giữ nguyên `youTubeOAuth2Api` (để khớp với workflow).
- Sau khi cấu hình, **lưu credential** và **test lại** bằng cách nhấn **Test Credential**.

##### **B. Cấu hình thư mục video**
- Node **"List Video Files"** sử dụng **Execute Command** để danh sách video trong thư mục.
- Các sếp cần **điền đường dẫn chính xác** đến thư mục chứa video (ví dụ: `/home/user/videos/`).
- **Lưu ý**:
  - Chỉ hỗ trợ file `.mp4` hoặc `.mov`.
  - Thư mục phải có **quyền đọc** cho n8n.

##### **C. Cấu hình playlist YouTube**
- Node **"Add to Playlist"** yêu cầu **ID playlist** của kênh.
- Các sếp cần **trích xuất ID playlist** từ URL playlist (ví dụ: `https://www.youtube.com/playlist?list=PLAYLIST_ID`).
- Trong **YouTube Node**, chọn **Playlist ID** và **Resource** là `playlistItem`.

##### **D. Thời gian JST (Japan Standard Time)**
- Workflow **tự động tính toán thời gian upload** với khoảng cách **12h** giữa các video.
- **Lưu ý**:
  - Các sếp cần **đảm bảo máy chủ VPS** của mình **đang sử dụng múi giờ JST** (hoặc điều chỉnh trong node **"Calculate Publish Schedule"** bằng mã JavaScript).

##### **E. Node Code (Sửa nếu cần)**
- Node **"Sort and Generate Items"** và **"Calculate Publish Schedule"** sử dụng **JavaScript**.
- **Không cần chỉnh sửa** nếu các sếp muốn sử dụng logic mặc định (12h JST).
- Nếu muốn **đổi khoảng cách thời gian**, các sếp có thể mở node **Code** và sửa:
  ```javascript
  // Ví dụ: Đổi thành 6h thay vì 12h
  const intervalHours = 6; // Thay đổi giá trị này
  ```

#### **3. Kích hoạt ⚡️**
1. **Test Run** với **dữ liệu mẫu**:
   - Chọn **Manual Trigger** → Nhấn **Execute Workflow**.
   - Kiểm tra **log** để đảm bảo workflow hoạt động.
2. **Bật Active**:
   - Sau khi test thành công, **bật nút Active** để workflow chạy tự động.

---

### ✍️ **Mẹo & gợi ý nâng cao**
:::tip[CÁCH LÀM NÀY ĐỂ TIẾT KIỆM THÊM THỜI GIAN]
- **Tự động thêm thẻ & mô tả**:
  - Sử dụng **node `code`** để thêm **thẻ (tags)** và **mô tả (description)** tự động từ metadata file (ví dụ: tên file).
- **Gửi thông báo khi upload xong**:
  - Kết nối với **Slack/Telegram** bằng node `webhook` để nhận thông báo khi video được upload thành công.
- **Lưu log upload**:
  - Sử dụng **node `stickyNote`** để ghi lại lịch sử upload (thời gian, video, trạng thái).
- **Tự động chia sẻ trên mạng xã hội**:
  - Kết hợp với **node `twitter`** hoặc **`facebook`** để tự động chia sẻ video mới.
- **Chỉnh sửa tiêu đề video**:
  - Sử dụng **node `code`** để **tự động thêm số thứ tự** vào tiêu đề (ví dụ: "Video #1 - Tên Video").
:::

---

### 📌 **Kết luận**
Workflow này **giải phóng hoàn toàn thời gian** của các sếp content creator, giúp **tự động hóa toàn bộ quy trình upload video YouTube** với **lịch trình 12h đều đặn** và **tự động thêm vào playlist**. **Không cần code**, chỉ cần **cấu hình OAuth2 và đường dẫn video**, workflow sẽ **chạy tự động 24/7** trên VPS.

**Hãy áp dụng ngay để tiết kiệm thời gian và tăng cường hiệu quả cho kênh YouTube của mình!** 🚀

---
**🔗 [Tải workflow nguyên bản](https://n8n.io/workflows/10098) | 📌 [Cài đặt n8n Self-hosted](https://docs.n8n.io/)**