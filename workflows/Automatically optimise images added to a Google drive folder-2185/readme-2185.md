---
title: "🚀 Tự Động Nén Ảnh Google Drive Với TinyPNG - Giảm Dung Lượng 80% Miễn Code"
description: "Workflow tự động hóa nén tất cả ảnh mới được upload vào Google Drive, giảm dung lượng lên đến 80% bằng TinyPNG và lưu lại tự động. Giúp tiết kiệm không gian lưu trữ và tăng tốc độ tải trang web."
slug: "tu-dong-nen-anh-google-drive-tinypng"
tags: [n8n, automation, google-drive, image-optimization, tinypng]
keywords: [tự động hóa n8n, nén ảnh google drive, giảm dung lượng ảnh, tinypng api, lưu trữ đám mây hiệu quả]
---

# 🚀 Tự Động Nén Ảnh Google Drive Với TinyPNG - Giảm Dung Lượng 80% Miễn Code

### 🔍 Nỗi Đau Của Các Sếp
Các sếp đang phải vật lộn với vấn đề **dung lượng ảnh quá lớn** trong Google Drive? Ảnh chất lượng cao chiếm trống không gian lưu trữ, làm chậm tốc độ tải trang web, và tăng chi phí lưu trữ đám mây? **Workflow này giải quyết tất cả!** Nó tự động **nén ảnh mới được upload** vào Google Drive bằng công nghệ TinyPNG (giảm dung lượng lên đến **80%**), sau đó lưu lại kết quả vào một thư mục riêng biệt - **không cần viết một dòng code nào!**

---

### 🎯 Kết Quả Các Sếp Nhận Được
:::tip[LỢI ÍCH CỐT LÕI]
- **Giảm dung lượng ảnh 80%** → Tiết kiệm không gian lưu trữ đám mây.
- **Tự động hóa hoàn toàn** → Không cần can thiệp thủ công.
- **Tốc độ tải trang web tăng** → Ảnh nhẹ hơn làm trang web hoạt động nhanh hơn.
- **Lưu trữ có tổ chức** → Ảnh nén được lưu vào thư mục riêng biệt, dễ quản lý.
- **Hoạt động 24/7** → Không cần phải nhớ bấm nút nào.
:::

---

### 🔧 Yêu Cầu Cần Thiết
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Google Drive** (đã kết nối với n8n).
2. **API Key TinyPNG** (miễn phí, cấp từ [tinypng.com](https://tinypng.com/developers)).
3. **Thư mục Google Drive** để lưu ảnh mới (để n8n theo dõi).
4. **Thư mục Google Drive khác** để lưu ảnh đã nén (cần tạo trước).
:::

---

### 🚀 Cách Import & Lưu Ý Khi "Lên Đồ"

#### 1. **Import Workflow 📥**
- **Cách 1:** Tải file JSON từ [n8n.io/workflows/2185](https://n8n.io/workflows/2185) và import vào n8n Editor.
- **Cách 2:** Copy toàn bộ JSON từ link trên và dán vào **Import Workflow** trong n8n.

#### 2. **Cấu Hình Cần Thiết (BẮT BUỘC Chỉnh)**
Workflow gồm **5 node** chính, các sếp cần chú ý cấu hình như sau:

##### **Node 1: "Check GDrive for new images" (Google Drive Trigger)**
- **Chọn credential:** `googleDriveOAuth2Api` (đã cấu hình trước).
- **Thiết lập folder theo dõi:**
  - Vào Google Drive, tạo **thư mục mới** (ví dụ: `Ảnh-Nguyên-Thù`).
  - Trong node này, chọn **folder đó** trong trường `Folder ID` (có thể copy từ liên kết Google Drive của folder).

##### **Node 2 & 3: "Download image" & "Optimise - Send image to TinyPNG" (Google Drive + HTTP Request)**
- **Node 2 (Download):**
  - Sử dụng credential `googleDriveOAuth2Api` như node 1.
  - **Không cần chỉnh sửa** ngoài credential.
- **Node 3 (Optimise):**
  - **Thêm API Key TinyPNG:**
    - Vào [TinyPNG Developers](https://tinypng.com/developers), tạo API Key.
    - Trong node này, vào tab **Headers**, thêm:
      ```
      Authorization: Basic YOUR_API_KEY_IN_BASE64
      ```
      (Chuyển API Key thành Base64 bằng công cụ như [Base64Encode.org](https://www.base64encode.org/)).
    - **Method:** POST.
    - **URL:** `https://api.tinypng.com/v1/shrink`.
    - **Body (JSON):**
      ```json
      {
        "key": "YOUR_API_KEY",
        "url": "{{$node["Download image"].json["downloadUrl"]}}"
      }
      ```

##### **Node 4: "Get optimised image from tinyPNG" (HTTP Request)**
- **Không cần chỉnh sửa** ngoài credential API Key đã cấu hình ở node 3.
- **URL:** `https://api.tinypng.com/v1/shrink`.
- **Method:** POST (giống node 3).

##### **Node 5: "Google Drive" (Upload ảnh nén)**
- **Chọn credential:** `googleDriveOAuth2Api`.
- **Thiết lập folder lưu ảnh nén:**
  - Tạo **thư mục mới** trong Google Drive (ví dụ: `Ảnh-Nén-TinyPNG`).
  - Trong node này, chọn folder đó trong trường `Folder ID`.
- **Tùy chọn: Đổi tên file:**
  - Mặc định, file sẽ được đặt tên là `original_name-optimised.ext`.
  - Các sếp có thể chỉnh sửa trường `File Name` để tự động thêm/loại bỏ ký tự (ví dụ: `{{$node["Get optimised image from tinyPNG"].json["filename"]}}`).

---

#### 3. **Kích Hoạt ⚡️**
1. **Test Run:**
   - Upload một ảnh vào **thư mục theo dõi** (node 1).
   - Chạy **Manual Test** cho workflow để kiểm tra kết quả.
   - Kiểm tra ảnh đã nén có xuất hiện trong **thư mục lưu** (node 5) không.
2. **Bật Active:**
   - Sau khi test thành công, bật **Active** để workflow chạy tự động mỗi khi có ảnh mới.

---

### ✍️ Mẹo & Gợi Ý Nâng Cao
:::info[TIPS THỰC TẾ]
- **Lưu log tự động:** Sử dụng node **Sticky Note** (node đầu tiên) để ghi lại lịch sử nén ảnh, giúp theo dõi dễ dàng.
- **Kết hợp Slack/Telegram:** Thêm node **Slack** hoặc **Telegram Bot** để thông báo khi ảnh đã nén thành công.
- **Báo cáo định kỳ:** Sử dụng node **Google Sheets** để tự động ghi dữ liệu dung lượng trước/khi nén vào bảng tính.
- **Nén nhiều loại hình ảnh:** TinyPNG hỗ trợ PNG, JPEG, WebP. Các sếp có thể mở rộng để nén tất cả loại hình ảnh.
- **Tự động xóa ảnh cũ:** Sử dụng node **Google Drive** với operation `delete` để xóa ảnh nguyên bản sau khi đã nén (nếu không cần).
:::

---

### 📌 Kết Luận
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn **tự động hóa nén ảnh Google Drive** mà không cần viết code. Với chỉ **5 node**, nó giúp tiết kiệm **80% dung lượng**, tăng tốc độ trang web và **tự động hóa hoàn toàn** quy trình. **Hãy thử ngay và cảm nhận sự khác biệt!**

👉 **Bắt đầu với n8n Self-hosted** để workflow chạy 24/7:
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::