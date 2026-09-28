---
title: "🎥 Tự Động Chuyển Pinterest Video Sang MP4 + Gửi Link Download qua Email (N8n + Google Drive)"
description: "Workflow tự động hóa hoàn chỉnh giúp các sếp content creator, marketer nhanh chóng chuyển đổi video từ Pinterest thành file MP4, lưu trữ trên Google Drive và gửi link download tự động qua email. Tiết kiệm thời gian lên đến 90% so với cách làm thủ công!"
slug: "tieu-dong-chuyen-pinterest-video-sang-mp4-voi-email"
tags: [n8n, automation, content-creation, google-drive, email-automation, rapidapi]
keywords: [n8n workflow pinterest, tự động hóa video pinterest, chuyển video pinterest sang mp4, tự động gửi link download, google drive automation, rapidapi n8n]
---

# 🚀 **Tự Động Chuyển Pinterest Video Sang MP4 + Gửi Link Download qua Email**

Hãy tưởng tượng một tình huống: Các sếp đang tìm kiếm video từ Pinterest để sử dụng trong nội dung marketing, nhưng phải mất **30-60 phút** để:
✅ Tải video từ Pinterest (thường là MP4 không rõ nguồn)
✅ Chuyển đổi sang định dạng MP4 chất lượng cao (nếu cần)
✅ Lưu trữ an toàn trên cloud
✅ Gửi link download cho đồng nghiệp hoặc khách hàng

**Workflow này giải quyết tất cả trong vòng 5-10 giây!** Dựa trên **API Pinterest Video Downloader** của RapidAPI, n8n sẽ tự động:
1. Nhận URL video từ Pinterest
2. Chuyển đổi sang MP4 chất lượng cao
3. Lưu trữ trên **Google Drive**
4. Cài đặt quyền **chia sẻ công khai**
5. Gửi **link download tự động** qua email

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow hoạt động **24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS. Dưới đây là 2 lựa chọn ổn định và giá cả phải chăng:
👉 **[VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** - giảm tới 39%)
👉 **[VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (Đảm bảo tốc độ cao cho API)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần tải thủ công, chuyển đổi hoặc chia sẻ file.
- **Chất lượng ổn định**: Video được chuyển đổi qua API chuyên nghiệp.
- **Lưu trữ an toàn**: Tất cả file được lưu trên Google Drive với quyền quản lý.
- **Chia sẻ dễ dàng**: Link download được gửi tự động qua email, không cần gửi file lớn.
- **Hoạt động liên tục**: Workflow chạy 24/7, không phụ thuộc vào thời gian làm việc.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Google Drive** (để lưu trữ file MP4).
2. **API Key của RapidAPI** (để sử dụng [Pinterest Video Downloader API](https://rapidapi.com/skdeveloper/api/pinterest-video-downloader6)).
   - **Mua API Key**: [Đăng ký tại RapidAPI](https://rapidapi.com/skdeveloper/api/pinterest-video-downloader6) (giá từ **$10/month**).
3. **Credentials SMTP** (để gửi email tự động):
   - Dịch vụ email như **Gmail, Outlook, hoặc SendGrid**.
   - **Thiết lập OAuth 2.0** (không dùng mật khẩu thường).
4. **Form nhận URL** (cần một trang web hoặc công cụ như **Google Form, Typeform, hoặc Carrd** để người dùng nhập URL và email).

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ **file JSON** hoặc **copy/paste JSON** vào **n8n Editor**:
- **Tải file JSON**: [Tải workflow từ n8n.io](https://n8n.io/workflows/6839) (ấn "Export").
- **Import vào n8n**:
  1. Mở **n8n Editor** (trang chủ của workflow).
  2. Nhấn **"Import"** và chọn file JSON.
  3. Hoặc **copy toàn bộ JSON** và dán vào **"Import from JSON"** (tab bên phải).

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow gồm **7 node chính**, các sếp cần cấu hình **cẩn thận** các node sau:

##### **🔹 Node 1: n8n Form Trigger**
- **Mục đích**: Nhận URL video từ Pinterest và email người dùng.
- **Cấu hình**:
  - **Trigger Type**: Chọn **"Form"** (nếu sử dụng Google Form) hoặc **"HTTP Request"** (nếu sử dụng API).
  - **Fields**:
    - `pinterestVideoUrl` (type: `string`, required: `true`).
    - `userEmail` (type: `string`, required: `true`).
  - **Lưu ý**:
    - Nếu sử dụng **Google Form**, các sếp cần **mapping field** giữa Form và node này.
    - Nếu sử dụng **API**, cấu hình **HTTP Request** để nhận dữ liệu JSON.

##### **🔹 Node 2 & 4: HTTP Request (Gửi & Lấy dữ liệu từ API)**
- **Mục đích**: Gửi URL video đến API và lấy kết quả MP4.
- **Cấu hình**:
  - **URL**: `https://pinterest-video-downloader6.p.rapidapi.com/download`
  - **Headers**:
    - `x-rapidapi-key`: Điền **API Key** từ RapidAPI.
    - `x-rapidapi-host`: `pinterest-video-downloader6.p.rapidapi.com`.
  - **Body (Request)**:
    ```json
    {
      "url": "${{ $json.pinterestVideoUrl }}"
    }
    ```
  - **Response Handling**:
    - API trả về **link download MP4** (node HTTP Downloader sẽ lấy file từ đây).

##### **🔹 Node 3: Wait (Đợi API hoàn thành)**
- **Mục đích**: API cần thời gian xử lý (thường **5-30 giây**).
- **Cấu hình**:
  - **Time**: Đặt **10-30 giây** (thử nghiệm để điều chỉnh).

##### **🔹 Node 5: Upload To Google Drive**
- **Mục đích**: Lưu file MP4 lên Google Drive.
- **Cấu hình**:
  - **Credentials**: Chọn **googleApi** (cần thiết lập trước).
  - **File Path**: `${{ $json.fileUrl }}` (link từ API).
  - **Folder**: Chọn **folder cụ thể** trong Google Drive (ví dụ: "Pinterest Videos").
  - **File Name**: `${{ $json.filename }}` (tên file từ API).

##### **🔹 Node 6: Set Permissions Google Drive (Chia sẻ công khai)**
- **Mục đích**: Cho phép người dùng tải file qua link.
- **Cấu hình**:
  - **Credentials**: Chọn **googleApi**.
  - **File ID**: `${{ $json.fileId }}` (ID file từ Google Drive).
  - **Permission**:
    - **Role**: `reader`.
    - **Type**: `anyone` (cho phép ai đó với link cũng có thể xem/tải).

##### **🔹 Node 7: Send Email (Gửi link download)**
- **Mục đích**: Gửi email chứa link download đến người dùng.
- **Cấu hình**:
  - **Credentials**: Chọn **smtp** (cần thiết lập trước).
  - **To**: `${{ $json.userEmail }}`.
  - **Subject**: `"Video của bạn đã sẵn sàng! Tải tại đây"`.
  - **Body (HTML)**:
    ```html
    <p>Xin chào,</p>
    <p>Video từ Pinterest đã được chuyển đổi thành MP4 và lưu trên Google Drive.</p>
    <p><a href="${{ $json.fileUrl }}">Tải video tại đây</a></p>
    <p>Trân trọng,</p>
    <p>Dự án tự động hóa của bạn</p>
    ```
  - **Lưu ý**:
    - Nếu dùng **Gmail**, cần **bật "Mật khẩu ứng dụng"** (2FA).
    - Để tránh spam, các sếp có thể **thêm header** như `Reply-To`.

---

#### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Nhập **URL video mẫu** và **email test** vào Form.
   - Chạy workflow và kiểm tra:
     - File có được tải xuống từ API không?
     - File có được upload lên Google Drive không?
     - Email có được gửi không?
2. **Bật Active**:
   - Sau khi test thành công, **bật workflow** để hoạt động liên tục.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Tự động hóa Form**:
   - Sử dụng **Google Form** hoặc **Typeform** để người dùng nhập URL và email.
   - **Mapping field** giữa Form và node `n8n Form Trigger`.

2. **Lưu log hoạt động**:
   - Thêm **node `Set`** sau `Send Email` để lưu dữ liệu vào **Google Sheets** hoặc **Database** (ví dụ: danh sách video đã xử lý).

3. **Gửi báo cáo định kỳ**:
   - Sử dụng **node `Schedule`** để gửi email tổng hợp (ví dụ: "Báo cáo video đã chuyển đổi trong tuần").

4. **Cài đặt quyền an toàn**:
   - Thay vì `anyone`, các sếp có thể **chia sẻ với người dùng cụ thể** (ví dụ: `user` với email `${{ $json.userEmail }}`).

5. **Optimize API**:
   - Nếu API trả về lỗi, thêm **node `If`** để xử lý trường hợp:
     - Video không tồn tại.
     - URL không hợp lệ.
     - Email không đúng định dạng.

---

### 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp content creator, marketer và team marketing để tập trung vào **strategy** thay vì **chuyển đổi file thủ công**. Với **Google Drive + Email tự động**, việc chia sẻ video trở nên **nhanh chóng, an toàn và chuyên nghiệp**.

**Bắt đầu ngay!**
1. **Import workflow** vào n8n.
2. **Cấu hình API Key, Google Drive và SMTP**.
3. **Test và bật workflow**.
4. **Chia sẻ link Form** với đồng nghiệp hoặc khách hàng.

**🚀 Cài đặt n8n trên VPS ngay hôm nay** và tự động hóa công việc của mình! 🚀