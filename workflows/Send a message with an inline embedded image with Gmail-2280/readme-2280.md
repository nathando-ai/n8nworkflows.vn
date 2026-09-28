---
title: "📧 Gửi Email Gmail Với Ảnh Trực Tuyến (Inline Embedded) - Tự Động Hóa 100% Không Code"
description: "Tự động gửi email Gmail chứa ảnh trực tuyến (inline embedded) chỉ với 6 bước đơn giản, tiết kiệm thời gian và nâng cao hiệu quả giao tiếp. Phù hợp cho doanh nghiệp, marketing, hoặc cá nhân cần gửi thông báo hình ảnh định kỳ."
slug: "gui-email-gmail-voi-anh-truc-tuyen"
tags: [n8n, automation, gmail, email-marketing, no-code, inline-image]
keywords: [n8n workflow gmail, tự động hóa email, gửi ảnh trong email, inline embedded image, tự động hóa marketing]
---

# 🚀 Gửi Email Gmail Với Ảnh Trực Tuyến (Inline Embedded) - Không Cần Code

### 💡 **Giải quyết vấn đề gì?**
Các sếp thường phải mất thời gian thủ công để:
- Tạo email chứa ảnh từ các nguồn trực tuyến (Google Images, website, hoặc URL tùy chỉnh).
- Chuyển đổi ảnh thành định dạng inline embedded để tránh liên kết bị đứt gãy.
- Gửi email định kỳ hoặc theo yêu cầu, dễ bị quên hoặc trễ hạn.

**Workflow này tự động hóa toàn bộ quá trình chỉ với 6 node**, giúp tiết kiệm **30 phút/ngày** và đảm bảo hình ảnh luôn hiển thị chính xác trong email.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow hoạt động 24/7 mà không gián đoạn, các sếp nên **self-host n8n** trên VPS. Dưới đây là 2 lựa chọn ưu tiên:
👉 [VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [VPS Xeon 4GB](https://my.bnix.one/aff.php?aff=172) (Chỉ **50k/tháng**, ổn định cao)
:::

---

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Gửi email + ảnh chỉ với 1 cú nhấp chuột.
- **Chất lượng cao**: Ảnh được embed trực tiếp (inline), không phụ thuộc vào liên kết ngoài.
- **Tự động hóa hoàn toàn**: Hoạt động 24/7, không cần can thiệp thủ công.
- **Dễ mở rộng**: Thêm nhiều email nhận hoặc thay đổi nội dung một cách linh hoạt.
:::

---

### 🔧 Yêu cầu cần thiết
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Gmail** (đã kích hoạt OAuth 2.0):
   - Cài đặt **OAuth 2.0 Credential** trong n8n:
     - Mở **Settings > Credentials > Add Credential > Gmail OAuth2**.
     - Theo hướng dẫn để kết nối tài khoản Gmail.
2. **URL ảnh trực tuyến** (để workflow lấy ảnh tự động):
   - Ví dụ: `https://example.com/image.jpg` (hoặc sử dụng URL ảnh ngẫu nhiên như trong workflow mẫu).
3. **Thông tin email**:
   - **Người gửi (From)**: Địa chỉ email Gmail đã kết nối.
   - **Người nhận (To)**: Địa chỉ email của khách hàng/đội ngũ (có thể thêm nhiều địa chỉ).

---

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. **Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [link gốc](https://n8n.io/workflows/2280) và import vào n8n Editor.
- **Cách 2**: Copy toàn bộ JSON từ [đây](https://n8n.io/workflows/2280) và paste vào **Import Workflow** trong n8n.

#### 2. **Các lưu ý BẮT BUỘC phải chỉnh 📌**
Workflow gồm **6 node chính**, các sếp cần điều chỉnh như sau:

##### **Node 1: Manual Trigger (Kích hoạt thủ công)**
- **Không cần chỉnh**: Sử dụng để test workflow trước khi tự động hóa.

##### **Node 2: Get Image (Lấy ảnh từ URL)**
- **Chỉnh sửa**:
  - Thay đổi **URL** trong `Method: GET` từ:
    ```json
    "url": "https://picsum.photos/200/300"
    ```
    thành URL ảnh **của các sếp** (ví dụ: `https://tinodata.vn/logo.png`).
  - **Lưu ý**: Ảnh phải có định dạng **JPEG/PNG** và có thể truy cập trực tuyến.

##### **Node 3: Convert Image to Base64 (Chuyển ảnh thành Base64)**
- **Không cần chỉnh**: Node này tự động chuyển ảnh thành định dạng embedable.

##### **Node 4: Message Settings (Cấu hình email)**
- **Chỉnh sửa**:
  - **From**: Địa chỉ email Gmail đã kết nối (ví dụ: `tinodata@example.com`).
  - **To**: Địa chỉ email người nhận (ví dụ: `nhanvien1@example.com`).
  - **Subject**: Tiêu đề email (ví dụ: `Thông báo mới từ TinoData`).
  - **Body**: Nội dung email, **không cần chỉnh** (workflow sẽ tự động thêm `<img src='cid:image1'>`).
  - **HTML**: **Không cần chỉnh** (n8n sẽ tự động render ảnh inline).

##### **Node 5: Compose Message (Tạo email hoàn chỉnh)**
- **Không cần chỉnh**: Node này kết hợp nội dung và ảnh thành email cuối cùng.

##### **Node 6: Send Message (Gửi email)**
- **Chỉnh sửa**:
  - **Credentials**: Chọn **gmailOAuth2** (đã cài đặt ở bước 1).
  - **Method**: Đảm bảo là `POST`.
  - **Headers**:
    - `Content-Type`: `application/json`.
  - **Body**:
    - Thay đổi `to` và `subject` nếu cần (hoặc giữ nguyên từ Node 4).
    - **Không cần chỉnh** phần `html` (n8n sẽ tự động thêm ảnh).

#### 3. **Kích hoạt ⚡️**
- **Bước 1**: Click **Test Workflow** để chạy thử với dữ liệu mẫu.
- **Bước 2**: Kiểm tra email nhận được có chứa ảnh inline không.
- **Bước 3**: Nếu thành công, **bật Active** để workflow hoạt động tự động.

---

### ✍️ Mẹo & gợi ý nâng cao
1. **Tự động hóa theo lịch**:
   - Sử dụng **n8n Trigger Node (Schedule)** để gửi email định kỳ (ví dụ: hàng ngày/lần/tuần).
   - Cài đặt trong **Settings > Workflow > Schedule**.

2. **Gửi nhiều email cùng lúc**:
   - Thay đổi Node **Message Settings** để loop qua danh sách email (ví dụ: từ Google Sheets).
   - Sử dụng **n8n-nodes-base.iterate** để xử lý nhiều người nhận.

3. **Lưu log và báo cáo**:
   - Thêm **n8n-nodes-base.slack** hoặc **n8n-nodes-base.email** để thông báo khi gửi thành công/thất bại.
   - Ví dụ: Gửi báo cáo hàng tuần về số email đã gửi qua Slack.

4. **Thay đổi ảnh động**:
   - Sử dụng **n8n-nodes-base.if** để thay đổi URL ảnh theo điều kiện (ví dụ: ảnh khác nhau cho từng ngày).

---

### 📌 Kết luận
Workflow này giúp các sếp **gửi email Gmail chứa ảnh inline chỉ trong vài phút**, tiết kiệm thời gian và đảm bảo tính chuyên nghiệp. **Áp dụng ngay** để tự động hóa quá trình giao tiếp hình ảnh trong doanh nghiệp!

👉 **Bắt đầu tự động hóa ngay**:
1. Import workflow từ [đây](https://n8n.io/workflows/2280).
2. Chỉnh sửa URL ảnh và thông tin email.
3. Test và bật **Active**!

**Cần hỗ trợ?** Đăng ký [VPS n8n](https://tino.vn/vps-n8n?affid=388) và liên hệ team TinoHost để được tư vấn chi tiết! 🚀