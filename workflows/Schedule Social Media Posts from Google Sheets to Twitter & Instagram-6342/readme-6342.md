---
title: "🚀 Tự Động Hóa Đăng Bài Social Media Từ Google Sheets Sang Twitter & Instagram (Không Cần Code)"
description: "Workflow tự động hóa hoàn toàn để lấy nội dung từ Google Sheets, tạo hình ảnh động từ HTML, đăng tweet trên Twitter và bài viết hình ảnh trên Instagram với thời gian chạy tự động hàng 5 giờ. Giúp tiết kiệm thời gian, tăng độ chính xác và tự động hóa toàn bộ quy trình content marketing."
slug: "tu-dong-hoa-dang-bai-social-media-google-sheets-twitter-instagram"
tags: [n8n, automation, social-media, google-sheets, instagram-twitter, no-code]
keywords: [n8n workflow social media, tự động hóa đăng bài instagram twitter, google sheets automation, tự động hóa content marketing, n8n schedule trigger]
---

# 🚀 **Tự Động Hóa Đăng Bài Social Media Từ Google Sheets Sang Twitter & Instagram**

## **🔥 Giới Thiệu: Giải Pháp Tự Động Hóa Content Marketing Cho Các Sếp Bận Rộn**

Chúng ta đã từng phải mất thời gian thủ công để:
- **Lên kế hoạch** các bài đăng trên Twitter và Instagram.
- **Tạo hình ảnh** cho bài viết (thường phải copy-paste từ Google Docs hoặc Canva).
- **Đăng bài** trên nhiều nền tảng khác nhau, dễ quên hoặc sai thời gian.
- **Theo dõi trạng thái** của bài đăng (đã đăng hay chưa) trong Google Sheets.

**Workflow này giải quyết tất cả những vấn đề trên!** Nó tự động:
✅ **Lấy dữ liệu** từ Google Sheets (dòng có trạng thái "Pending").
✅ **Tạo hình ảnh** từ HTML/CSS (không cần thiết kế thủ công).
✅ **Đăng tweet** trên Twitter và **bài viết hình ảnh** trên Instagram.
✅ **Cập nhật trạng thái** trong Google Sheets để tránh trùng lặp.

---
### **🎯 Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần đăng bài thủ công hàng ngày.
- **Chính xác 100%**: Không quên đăng hoặc đăng trùng.
- **Hình ảnh chuyên nghiệp**: Tự động tạo từ nội dung HTML.
- **Hoạt động liên tục**: Workflow chạy tự động hàng 5 giờ (cấu hình được).
- **Dễ dàng theo dõi**: Google Sheets luôn cập nhật trạng thái bài đăng.
:::

---
### **🔧 Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi chạy workflow, các sếp cần chuẩn bị:
1. **Tài khoản n8n Self-hosted** (để chạy 24/7).
2. **Google Sheets** với cấu trúc cột như sau:
   - **RowID** (ID dòng)
   - **Caption** (Nội dung tweet)
   - **Desc** (Mô tả cho Instagram)
   - **Hashtags** (Danh sách hashtag)
   - **Status** (Trạng thái: "Pending" để đăng, "Posted" nếu đã đăng)
3. **API Keys & Credentials**:
   - **Google Sheets OAuth2** (để đọc/viết dữ liệu).
   - **Twitter (X) OAuth1** (đăng tweet).
   - **Facebook Graph API** (đăng bài Instagram).
   - **HCTI.io API Key** (chuyển HTML → Hình ảnh).
4. **Tài khoản Instagram Business** (được kết nối với Facebook Page).
:::

---
## **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/6342](https://n8n.io/workflows/6342) hoặc copy toàn bộ JSON từ link trên.
- Mở **n8n Editor** → Nhấn **"Import"** → Dán JSON hoặc tải file `.json`.
- Workflow sẽ tự động hiển thị trên canvas.

### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
#### **🔹 Node 1: Schedule Trigger (Động cơ Khởi Động)**
- **Cấu hình thời gian chạy**: Mặc định là **5 giờ/lần** (có thể điều chỉnh).
- **Lưu ý**: Nếu muốn chạy thường xuyên hơn, giảm thời gian (ví dụ: 1 giờ/lần).

#### **🔹 Node 2: Get row(s) in sheet (Lấy Dòng Từ Google Sheets)**
- **Tham số cần điền**:
  - **Google Sheets ID**: ID của Google Sheet (tìm trong URL: `https://docs.google.com/spreadsheets/d/[ID]/edit`).
  - **Sheet Name**: Tên tab trong Google Sheet.
  - **Query**: `Status = "Pending"` (lấy chỉ những dòng chưa đăng).
  - **Range**: `Sheet1!A:E` (điều chỉnh theo cột của bạn).
- **Lưu ý**: Nếu Google Sheets không kết nối được, kiểm tra **credentials OAuth2** đã cấu hình chưa.

#### **🔹 Node 3: Insta post caption (Tạo Nội Dung Cho Instagram)**
- **Cấu hình**:
  - **Expression**: `{{ $json["Caption"] }} + "\n\n" + $json["Desc"] + "\n\n" + $json["Hashtags"]`
  - **HTML Structure**: Sử dụng `final_caption` để tạo hình ảnh sau này.

#### **🔹 Node 4: HCTI Image (Tạo Hình Ảnh Từ HTML)**
- **Tham số cần điền**:
  - **URL**: `https://hcti.io/api/v1/image`
  - **Headers**:
    - `Authorization`: `Bearer [API_KEY_HCTI]` (mua trên [hcti.io](https://hcti.io/)).
    - `Content-Type`: `application/json`.
  - **Body**:
    ```json
    {
      "html": "{{ $json["final_caption"] }}",
      "width": 1080,
      "height": 1080,
      "backgroundColor": "#FFFFFF"
    }
    ```
- **Lưu ý**:
  - Nếu không có API Key, đăng ký tài khoản **HCTI.io** (có phiên bản miễn phí với giới hạn).
  - Nếu hình ảnh không tạo được, kiểm tra **HTML** có đúng định dạng không.

#### **🔹 Node 5: Post on Twitter (Đăng Tweet)**
- **Tham số cần điền**:
  - **URL**: `https://api.twitter.com/1.1/statuses/update.json`
  - **Headers**:
    - `Authorization`: `OAuth oauth_consumer_key="[CONSUMER_KEY]", oauth_token="[ACCESS_TOKEN]", oauth_signature_method="HMAC-SHA1", oauth_timestamp="[TIMESTAMP]", oauth_nonce="[NONCE]", oauth_version="1.0"`.
  - **Body**:
    ```json
    {
      "status": "{{ $json["Caption"] }}"
    }
    ```
- **Lưu ý**:
  - **Twitter OAuth1** phải được cấu hình trong **n8n Credentials**.
  - Nếu tweet không đăng được, kiểm tra **credentials** có đúng không.

#### **🔹 Node 6 & 7: Create Insta post & Post On Instagram (Đăng Bài Instagram)**
- **Tham số cần điền**:
  - **Access Token**: Token **Facebook Graph API** (của tài khoản Instagram Business).
  - **URL**:
    - **Create Insta post**: `https://graph.facebook.com/v18.0/[PAGE_ID]/media`
    - **Post On Instagram**: `https://graph.facebook.com/v18.0/[PAGE_ID]/media_publish`
  - **Body**:
    ```json
    {
      "message": "{{ $json["final_caption"] }}",
      "caption": "{{ $json["final_caption"] }}",
      "image_url": "{{ $json["image_url"] }}"
    }
    ```
- **Lưu ý**:
  - **Facebook Graph API** phải được kết nối với **Instagram Business Account**.
  - Nếu token hết hạn, tạo **Long-lived Token** mới trên [Facebook Developer](https://developers.facebook.com/).

#### **🔹 Node 8: Update Status Posted (Cập Nhật Trạng Thái)**
- **Tham số cần điền**:
  - **Google Sheets ID & Sheet Name**: Như Node 2.
  - **Range**: `Sheet1!A:E`.
  - **Expression**:
    ```json
    {
      "Status": "Posted on " + new Date().toLocaleString()
    }
    ```
- **Lưu ý**: Đảm bảo **credentials OAuth2** đã được cấu hình.

---
### **3. Kích Hoạt ⚡️**
1. **Test Run** với một dòng mẫu:
   - Chọn **Run Workflow** và kiểm tra từng node có hoạt động không.
   - Nếu gặp lỗi, xem **Logs** để sửa.
2. **Bật Active**:
   - Sau khi test thành công, chuyển **Schedule Trigger** sang **Active**.

---
## **✍️ Mẹo & Gợi Ý Nâng Cao**
:::info[TIPS THỰC TIỆN]
- **Kết hợp với Slack/Telegram**: Thêm node **Slack Webhook** hoặc **Telegram Bot** để thông báo khi bài đăng thành công.
- **Lưu Log**: Sử dụng **n8n-nodes-base.stickyNote** để ghi lại lỗi hoặc thành công.
- **Báo Cáo Định Kỳ**: Tạo một **Google Sheet** mới để thống kê số lượng bài đăng mỗi tháng.
- **Sử dụng AI Tạo Hình**: Thay vì HCTI.io, có thể kết nối với **MidJourney API** hoặc **DALL·E** để tạo hình ảnh động.
- **Chỉnh Thời Gian**: Nếu muốn đăng vào giờ vàng (ví dụ: 8h sáng), điều chỉnh **Schedule Trigger** thành **08:00**.
:::

---
## **📌 Kết Luận: Tự Động Hóa Content Marketing Bằng n8n**
Workflow này **giải phóng thời gian** cho các sếp để tập trung vào chiến lược content chứ không phải việc đăng bài thủ công. Với **cấu hình đơn giản** và **không cần code**, bạn có thể:
✔ **Tiết kiệm 10+ giờ/tuần** cho việc đăng bài.
✔ **Tăng độ chính xác** với hệ thống tự động.
✔ **Tạo hình ảnh chuyên nghiệp** từ HTML.
✔ **Theo dõi toàn bộ quá trình** trên Google Sheets.

**🚀 Hãy import workflow ngay hôm nay và bắt đầu tự động hóa content marketing của mình!**

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**💡 Cần hỗ trợ thêm?** Đăng ký **hỗ trợ kỹ thuật n8n** tại [n8n Community](https://community.n8n.io/) hoặc liên hệ với tác giả [Parag Javale](https://twitter.com/paragjavale) để tối ưu workflow!**