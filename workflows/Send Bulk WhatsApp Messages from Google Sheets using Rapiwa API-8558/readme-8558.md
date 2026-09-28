---
title: "📱 Tự Động Hóa Gửi Tin Nhắn WhatsApp Bulk Từ Google Sheets Với Rapiwa API (Không Cần Code)"
description: "Giải pháp hoàn toàn tự động hóa gửi tin nhắn WhatsApp bulk từ Google Sheets, sử dụng API Rapiwa để tiết kiệm chi phí và thời gian. Workflow hoạt động 24/7, kiểm tra và gửi tin nhắn tự động mỗi 5 phút, đồng thời cập nhật trạng thái trong bảng tính."
slug: "tieu-dong-hoa-gui-tin-nhan-whatsapp-bulk-tu-google-sheets"
tags: [n8n, automation, no-code, whatsapp-bulk, rapiwa-api, google-sheets, marketing-automation]
keywords: [tự động hóa whatsapp bulk, gửi tin nhắn whatsapp tự động, n8n workflow whatsapp, rapiwa api, tự động hóa marketing, google sheets automation]
---

# 🚀 **Tự Động Hóa Gửi Tin Nhắn WhatsApp Bulk Từ Google Sheets Với Rapiwa API**

## **🔥 Giải Pháp Cho Những Ai Đang Mệt Mỏi Với Công Việc Gửi Tin Nhắn WhatsApp Thủ Công**
Bạn có bao giờ phải mất hàng giờ để gửi tin nhắn WhatsApp cho hàng trăm khách hàng, đồng nghiệp hoặc thành viên trong nhóm? Hay phải lo lắng rằng tin nhắn sẽ bị gửi trùng lặp, hoặc số điện thoại không hợp lệ khiến tin nhắn bị từ chối? **Workflow này sẽ giải quyết tất cả những vấn đề đó!**

Với **n8n**, bạn có thể tự động hóa hoàn toàn quá trình gửi tin nhắn WhatsApp bulk từ **Google Sheets**, sử dụng **API Rapiwa** (không cần WhatsApp Business API chính thức). Workflow sẽ:
✅ **Tự động lấy dữ liệu** từ Google Sheets (chỉ các tin nhắn có trạng thái "pending").
✅ **Lọc và kiểm tra số điện thoại** trước khi gửi (tránh số không hợp lệ).
✅ **Gửi tin nhắn theo batch** (tối đa 60 tin nhắn/lần) để tránh bị chặn.
✅ **Cập nhật trạng thái** trong Google Sheets (verified/unverified/sent).
✅ **Hoạt động 24/7** mỗi 5 phút, không cần can thiệp thủ công.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần gửi tin nhắn thủ công hàng ngày.
- **Tăng hiệu quả**: Gửi tin nhắn bulk trong thời gian ngắn (mỗi 5 phút).
- **Tránh bị chặn**: Sử dụng batch và kiểm tra số điện thoại trước khi gửi.
- **Dữ liệu chính xác**: Cập nhật trạng thái tự động trong Google Sheets.
- **Không cần WhatsApp Business API**: Sử dụng Rapiwa API (rẻ hơn và dễ sử dụng).
- **Hoạt động liên tục**: Workflow tự động chạy mỗi 5 phút, không cần can thiệp.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
✔ **Tài khoản WhatsApp** (cả cá nhân và doanh nghiệp đều được).
✔ **Google Sheet** với cấu trúc như [mẫu này](https://docs.google.com/spreadsheets/d/1Ui4TzzI-Gq-bsEsrZELwW1Kyddw0IU9L1wxlHikktqw/edit?usp=sharing).
✔ **Google Sheets OAuth2 credentials** (đã cấu hình trong n8n).
✔ **Tài khoản Rapiwa** và **Bearer Token** (mua trên [rapiwa.com](https://rapiwa.com/)).
✔ **Số điện thoại WhatsApp** đã kết nối và xác thực trên Rapiwa.

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
```bash
# Nếu import từ file:
1. Tải file JSON từ [n8n.io/workflows/8558](https://n8n.io/workflows/8558).
2. Trong n8n Editor, nhấn **Import** và chọn file.
# Nếu copy/paste:
1. Mở n8n Editor, tạo workflow mới.
2. Nhấn **Import** → **Paste JSON** và dán toàn bộ JSON từ workflow.
```

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Dưới đây là các node quan trọng cần cấu hình chính xác:

##### **🔹 Node "Trigger Every 5 Minute"**
- **Đã cấu hình sẵn** để workflow chạy tự động mỗi 5 phút.
- **Không cần chỉnh sửa**, trừ khi muốn thay đổi thời gian chạy (ví dụ: 10 phút).

##### **🔹 Node "Fetch All Pending Queries for Messaging" (Google Sheets)**
- **Credentials**: Chọn `googleSheetsOAuth2Api` (đã cấu hình trước).
- **Query**: `Status = "pending"` (lấy chỉ các tin nhắn chưa gửi).
- **Lưu ý**:
  - Đảm bảo Google Sheet đã chia sẻ cho tài khoản OAuth2.
  - Cột `Status` phải có giá trị "pending" cho các tin nhắn chưa gửi.

##### **🔹 Node "Clean WhatsApp Number" (Code)**
- **Mã JavaScript**:
  ```javascript
  // Loại bỏ ký tự không hợp lệ (khoảng trắng, dấu gạch, dấu ngoặc)
  const cleanedNumber = $input.all().number.replace(/\D/g, '');
  return [{ number: cleanedNumber }];
  ```
- **Lưu ý**:
  - WhatsApp chỉ chấp nhận số điện thoại **số nguyên** (ví dụ: `880123456789` thay vì `+84 123 456 789`).

##### **🔹 Node "Check valid whatsapp number Using Rapiwa" (HTTP Request)**
- **URL**: `https://app.rapiwa.com/api/check-number`
- **Method**: `POST`
- **Headers**:
  - `Authorization: Bearer {API_KEY_RAPIWA}`
  - `Content-Type: application/json`
- **Body**:
  ```json
  {
    "number": "{{ $json['number'] }}"
  }
  ```
- **Lưu ý**:
  - Thay `{API_KEY_RAPIWA}` bằng **Bearer Token** từ Rapiwa.
  - Nếu trả về `exists: true`, số điện thoại hợp lệ.

##### **🔹 Node "Send Message Using Rapiwa" (HTTP Request)**
- **URL**: `https://app.rapiwa.com/api/send-message`
- **Method**: `POST`
- **Headers**:
  - `Authorization: Bearer {API_KEY_RAPIWA}`
  - `Content-Type: application/json`
- **Body**:
  ```json
  {
    "number": "{{ $json['number'] }}",
    "message": "{{ $json['message'] }}",
    "message_type": "text"
  }
  ```
- **Lưu ý**:
  - Thay `{{ $json['number'] }}` và `{{ $json['message'] }}` bằng dữ liệu từ Google Sheets.
  - Nếu muốn gửi **tin nhắn hình ảnh**, thêm `imageUrl` vào body.

##### **🔹 Node "Change State of Rows in Verified & Sent" (Google Sheets)**
- **Credentials**: `googleSheetsOAuth2Api`.
- **Operation**: `update`.
- **Lưu ý**:
  - Cập nhật cột `Status` thành `"sent"` và `Verification` thành `"verified"`.
  - Sử dụng `rowNumber` để xác định hàng cần cập nhật.

##### **🔹 Node "Change State of Rows in Unverified & Not Sent" (Google Sheets)**
- **Credentials**: `googleSheetsOAuth2Api`.
- **Operation**: `update`.
- **Lưu ý**:
  - Cập nhật cột `Status` thành `"not_sent"` và `Verification` thành `"unverified"`.

##### **🔹 Node "Wait"**
- **Thời gian chờ**: 5 giây (có thể điều chỉnh để tránh bị chặn).
- **Lưu ý**:
  - Nếu gửi quá nhiều tin nhắn cùng lúc, Rapiwa có thể chặn số điện thoại.
  - Thời gian chờ giúp phân tán tải.

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Nhấn **Run Workflow** và kiểm tra:
     - Các tin nhắn có được gửi không?
     - Trạng thái trong Google Sheets có được cập nhật không?
2. **Bật Active**:
   - Sau khi test thành công, chuyển workflow sang **Active**.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Gửi Tin Nhắn Hình Ảnh**:
   - Thêm cột `Image URL` vào Google Sheets và cập nhật body HTTP Request:
     ```json
     {
       "number": "{{ $json['number'] }}",
       "message": "{{ $json['message'] }}",
       "imageUrl": "{{ $json['Image URL'] }}",
       "message_type": "image"
     }
     ```

2. **Gửi Báo Cáo Định Kỳ**:
   - Thêm node **Slack/Telegram** để thông báo khi workflow hoàn thành.
   - Ví dụ: Gửi tin nhắn `"Đã gửi {{count}} tin nhắn WhatsApp thành công!"`.

3. **Lưu Log**:
   - Thêm node **Code** để log tất cả hoạt động vào Google Sheets hoặc một file JSON.

4. **Tăng Batch Size**:
   - Nếu không bị chặn, có thể tăng số tin nhắn trong `Limit` node (ví dụ: 100 tin nhắn/lần).

5. **Kết Hợp Với CRM**:
   - Nếu đang sử dụng **HubSpot, Zoho CRM** hoặc **Salesforce**, có thể lấy dữ liệu từ đó thay vì Google Sheets.

---

### 📌 **Kết Luận**
**Workflow này là giải pháp hoàn hảo** cho các doanh nghiệp, marketer hoặc team cần gửi tin nhắn WhatsApp bulk một cách **tự động, chính xác và tiết kiệm chi phí**. Bằng cách kết hợp **n8n, Google Sheets và Rapiwa API**, bạn không chỉ tiết kiệm thời gian mà còn tránh được những rủi ro như bị chặn số điện thoại hoặc gửi tin nhắn trùng lặp.

**Hãy áp dụng ngay và tự động hóa công việc của mình!** 🚀

---
**🔗 Tài Liệu Tham Khảo:**
- [Rapiwa API Documentation](https://docs.rapiwa.com)
- [Mẫu Google Sheets](https://docs.google.com/spreadsheets/d/1Ui4TzzI-Gq-bsEsrZELwW1Kyddw0IU9L1wxlHikktqw/edit?usp=sharing)
- [n8n Workflow Gốc](https://n8n.io/workflows/8558)