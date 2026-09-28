---
title: "🎁 Hệ Thống Tặng Phần Thưởng Khuyến Mãi Tự Động Hóa Với Email Xác Minh & Coupon Hình Ảnh - N8n"
description: "Tự động hóa hoàn toàn hệ thống khuyến mãi giới thiệu bằng email với xác minh địa chỉ email và tạo coupon hình ảnh cá nhân hóa, giúp doanh nghiệp tiết kiệm thời gian và tăng tỷ lệ chuyển đổi. Workflow này tự động gửi phần thưởng, theo dõi tất cả hoạt động và phân loại thành công/thất bại."
slug: "automated-referral-reward-system-n8n"
tags: [n8n, automation, no-code, email-marketing, google-sheets, social-media]
keywords: [n8n workflow tự động hóa khuyến mãi, hệ thống phần thưởng giới thiệu, coupon tự động hóa, xác minh email tự động, n8n google sheets]
---

# 🚀 **Hệ Thống Tặng Phần Thưởng Khuyến Mãi Tự Động Hóa Với Email Xác Minh & Coupon Hình Ảnh**

## **💡 Giới Thiệu: Tự Động Hóa Khuyến Mãi Giới Thiệu Cho Doanh Nghiệp**
Bạn có bao giờ phải mất thời gian thủ công xác minh email, tạo coupon cá nhân hóa và gửi phần thưởng cho khách hàng giới thiệu? Hay phải lo lắng về những đơn đăng ký giả mạo từ email tạm thời? **Workflow này giải quyết tất cả những vấn đề đó!**

Với **Automated Referral Reward System**, các sếp có thể:
✅ **Xác minh email tự động** để loại bỏ những đơn đăng ký không hợp lệ.
✅ **Tạo coupon hình ảnh cá nhân hóa** với tên người giới thiệu, mã khuyến mãi và thông tin chiến dịch.
✅ **Gửi phần thưởng qua email** với coupon hình ảnh đẹp mắt, không cần viết code.
✅ **Theo dõi tất cả hoạt động** trên Google Sheets để phân tích hiệu quả chiến dịch.

Không cần viết một dòng code nào, workflow này hoạt động **24/7** và giúp doanh nghiệp **tăng tỷ lệ chuyển đổi, giảm chi phí thủ công và tối ưu hóa chiến dịch marketing**.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần thủ công xác minh email hoặc tạo coupon.
- **Tăng tỷ lệ chuyển đổi**: Coupon hình ảnh cá nhân hóa làm tăng sự hấp dẫn.
- **Giảm chi phí**: Loại bỏ đơn đăng ký giả mạo từ email tạm thời.
- **Theo dõi hiệu quả**: Dữ liệu chi tiết trên Google Sheets giúp phân tích chiến dịch.
- **Hoạt động liên tục**: Workflow tự động hóa 24/7, không cần can thiệp.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản VerifiEmail API** (để xác minh email):
   - Đăng ký tại: [https://verifi.email](https://verifi.email)
   - Lấy **API Key** từ dashboard.

2. **Tài khoản HTMLCSStoImage API** (để chuyển đổi HTML thành hình ảnh):
   - Đăng ký tại: [https://htmlcsstoimg.com](https://htmlcsstoimg.com)
   - Lấy **User ID** và **API Key**.

3. **Tài khoản Gmail** (để gửi email phần thưởng và thông báo lỗi):
   - **Bật 2FA** để bảo mật.

4. **Google Sheets** (để theo dõi hoạt động):
   - Tạo bảng **Referral_Reward_Tracker** với các cột:
     - `Timestamp`
     - `Referrer Name` (Tên người giới thiệu)
     - `Referrer Email` (Email người giới thiệu)
     - `Status` (Thành công/Thất bại)
     - `Coupon Code` (Mã khuyến mãi)
     - `Coupon Image URL` (Link hình ảnh coupon)
     - `Campaign` (Chiến dịch)

5. **Webhook từ Jotform** (để nhận dữ liệu đăng ký):
   - Cấu hình **Webhook Trigger** với đường dẫn `referral-reward` và phương thức `POST`.
   - Dữ liệu đầu vào dự kiến:
     ```json
     {
       "referrer_name": "John Doe",
       "referrer_email": "john@example.com",
       "referred_friend": "jane@example.com",
       "campaign": "Holiday Referral 2025"
     }
     ```
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Mở **n8n Workflow Editor**.
2. Nhấp vào **Import** và chọn file JSON hoặc dán JSON vào ô nhập liệu.
3. Nhấp **Import** để tải workflow vào.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Sau khi import, các sếp cần **cấu hình chi tiết** các node quan trọng:

##### **🔐 Cấu Hình Credentials**
- **VerifiEmail**:
  - Điền **API Key** từ dashboard VerifiEmail vào `verifiEmailApi`.
- **HTMLCSStoImage**:
  - Điền **User ID** và **API Key** vào `htmlcsstoimgApi`.
- **Gmail**:
  - Chọn **gmailOAuth2** và bật **2FA** để bảo mật.
- **Google Sheets**:
  - Chọn **googleSheetsOAuth2Api** và chọn bảng **Referral_Reward_Tracker**.

##### **📝 Cấu Hình Node "Set Coupon Template"**
- **HTML Template**: Sử dụng mã HTML/CSS mẫu để tạo coupon cá nhân hóa.
  ```html
  <div style="width: 500px; height: 300px; background: #f4f4f4; border-radius: 10px; padding: 20px; text-align: center;">
      <h2 style="color: #333;">🎁 PHẦN THƯỞNG GIỚI THIỆU</h2>
      <p style="font-size: 18px;">Chúc mừng {{referrer_name}}!</p>
      <p style="font-size: 24px; font-weight: bold;">MÃ KHUYẾN MÃI: <span style="color: #e74c3c;">{{coupon_code}}</span></p>
      <p>Áp dụng cho chiến dịch: {{campaign}}</p>
      <p>Hiệu lực: 30 ngày</p>
  </div>
  ```
- **Dynamic Data**:
  - `{{referrer_name}}`: Tên người giới thiệu (từ webhook).
  - `{{coupon_code}}`: Mã khuyến mãi tự động sinh (ví dụ: `REF-JOHN1234`).
  - `{{campaign}}`: Tên chiến dịch (từ webhook).

##### **⚠️ Lưu Ý Quá Trình Xác Minh Email**
- Node **IF Email Valid?** sẽ kiểm tra kết quả từ **VerifiEmail**:
  - **Nếu email hợp lệ** → Tạo coupon và gửi email phần thưởng.
  - **Nếu email không hợp lệ** → Gửi email thông báo lỗi.

##### **🖼️ Cấu Hình Node "HTML/CSS to Image"**
- Chọn **htmlcsstoimgApi** và đảm bảo **User ID** và **API Key** đã điền đúng.
- Node này sẽ chuyển đổi HTML coupon thành **hình ảnh PNG** để embed vào email.

##### **📧 Cấu Hình Node "Send Reward Email"**
- Chọn **gmailOAuth2** và cấu hình nội dung email:
  - **Tiêu đề**: `🎁 Phần thưởng của bạn đã sẵn sàng!`
  - **Nội dung HTML**:
    ```html
    <h2>Chúc mừng, {{referrer_name}}!</h2>
    <p>Bạn đã thành công giới thiệu thành viên mới và nhận được phần thưởng!</p>
    <p>Dưới đây là coupon của bạn:</p>
    <img src="{{coupon_image_url}}" alt="Coupon" style="width: 100%;">
    <p><strong>Mã khuyến mãi:</strong> {{coupon_code}}</p>
    <p><strong>Hiệu lực:</strong> 30 ngày</p>
    <p><strong>Chiến dịch:</strong> {{campaign}}</p>
    ```
  - **Nội dung văn bản** (plain text) cũng cần được cấu hình để đảm bảo email không bị đánh dấu là spam.

##### **📊 Cấu Hình Node "Log to Google Sheets"**
- Chọn **googleSheetsOAuth2Api** và bảng **Referral_Reward_Tracker**.
- **Operation**: `appendOrUpdate` (thêm hoặc cập nhật hàng).
- **Headers** phải khớp với bảng:
  ```
  Timestamp | Referrer Name | Referrer Email | Status | Coupon Code | Coupon Image URL | Campaign
  ```

#### **3. Kích Hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Gửi một request POST đến webhook với dữ liệu mẫu:
     ```json
     {
       "referrer_name": "John Doe",
       "referrer_email": "john@example.com",
       "referred_friend": "jane@example.com",
       "campaign": "Holiday Referral 2025"
     }
     ```
   - Kiểm tra email và Google Sheets để xác nhận workflow hoạt động.
2. **Bật Active workflow** khi đã kiểm tra xong.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết Nối Với Slack/Telegram**:
   - Thêm node **Slack** hoặc **Telegram Bot** để thông báo khi có đơn đăng ký mới hoặc lỗi xác minh email.
   - Ví dụ: Khi email không hợp lệ, gửi thông báo đến Slack với nội dung:
     ```
     ❌ Email không hợp lệ: {{referrer_email}}
     Lý do: {{verification_status}}
     ```

2. **Lưu Log Chi Tiết**:
   - Thêm node **Set** trước khi log vào Google Sheets để lưu thêm thông tin như:
     - `verification_status` (Hợp lệ/Không hợp lệ).
     - `timestamp` (Thời gian xử lý).

3. **Gửi Báo Cáo Định Kỳ**:
   - Sử dụng **n8n Scheduler** để chạy workflow hàng tuần và gửi báo cáo tổng hợp về hiệu quả chiến dịch qua email.

4. **Tùy Chỉnh Coupon**:
   - Sử dụng **n8n Code Node** để sinh mã khuyến mãi phức tạp hơn (ví dụ: kết hợp ngày tháng, tên người giới thiệu).

5. **Bảo Mật Email**:
   - Sử dụng **n8n Node "Email Validation"** để thêm bước kiểm tra email trước khi xác minh.

---

### 📌 **Kết Luận**
Workflow **Automated Referral Reward System** là giải pháp **tự động hóa hoàn toàn** cho hệ thống khuyến mãi giới thiệu, giúp doanh nghiệp:
✔ **Tiết kiệm thời gian** và chi phí thủ công.
✔ **Tăng tỷ lệ chuyển đổi** với coupon cá nhân hóa.
✔ **Theo dõi hiệu quả chiến dịch** trên Google Sheets.
✔ **Giảm rủi ro** từ email giả mạo.

**Hãy áp dụng ngay workflow này và nâng cao hiệu quả marketing của doanh nghiệp!** 🚀

---
**🔗 [Tải workflow JSON](https://n8n.io/workflows/10161)** (nếu cần) hoặc import trực tiếp từ n8n Editor.