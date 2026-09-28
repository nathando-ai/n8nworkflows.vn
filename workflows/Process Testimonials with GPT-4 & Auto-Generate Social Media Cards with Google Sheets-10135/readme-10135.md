---
title: "🚀 Tự Động Xử Lý Đánh Giá Khách Hàng (Testimonials) Với GPT-4 + Tạo Thẻ Social Media Tự Động (Google Sheets)"
description: "Workflow tự động hóa hoàn toàn không cần code để thu thập, cải tiến nội dung đánh giá khách hàng bằng GPT-4, tạo thẻ hình ảnh chuyên nghiệp từ HTML/CSS, và tự động hóa việc đăng tải lên Google Drive và Google Sheets. Giúp các sếp tiết kiệm 10+ giờ/tháng và nâng cao chất lượng nội dung marketing."
slug: "tieu-ly-danh-gia-khach-hang-voi-gpt-4-tao-the-social-media"
tags: [n8n, automation, no-code, ai-gpt-4, google-sheets, social-media, html-css-to-image, slack-notification]
keywords: [n8n workflow testimonials, tự động hóa đánh giá khách hàng, GPT-4 cải tiến nội dung, tạo thẻ social media tự động, Google Drive + Google Sheets, tự động hóa marketing]
---

# 🚀 **Tự Động Xử Lý Đánh Giá Khách Hàng (Testimonials) Với GPT-4 + Tạo Thẻ Social Media Tự Động**

---

## **🔥 Nỗi Đau Của Các Sếp Khi Làm Thủ Công**
Hàng ngày, các sếp phải:
- **Thu thập** hàng chục đánh giá khách hàng từ email, form, hoặc mạng xã hội.
- **Chỉnh sửa thủ công** nội dung để grammar, tone và nội dung chuyên nghiệp hơn.
- **Tạo thẻ hình ảnh** cho mỗi testimonial bằng Photoshop hoặc Canva (tốn thời gian và không nhất quán).
- **Quản lý** danh sách testimonials trên Google Sheets và theo dõi trạng thái (Approved/Posted).
- **Gửi thông báo** cho team marketing khi có testimonial sẵn sàng đăng tải.

**Kết quả?** Tốn **10+ giờ/tháng**, dễ sai sót, và không thể hoạt động 24/7. **Workflow này giải quyết tất cả!**

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ/tháng** với tự động hóa hoàn toàn từ thu thập đến đăng tải.
- **Nội dung testimonial chuyên nghiệp** với GPT-4 sửa chữa grammar, tone và giữ nguyên ý nghĩa gốc.
- **Thẻ hình ảnh tự động** từ HTML/CSS → PNG, không cần kỹ năng thiết kế.
- **Quản lý trung tâm hóa** trên Google Sheets với trạng thái Approved/Posted.
- **Thông báo Slack tự động** khi có testimonial sẵn sàng đăng tải.
- **Hoạt động 24/7** với trigger định kỳ (5 phút/lần) để kiểm tra và thông báo.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi chạy workflow, các sếp cần chuẩn bị:
1. **Tài khoản OpenAI** (API Key) để sử dụng GPT-4 Turbo Preview.
2. **Tài khoản HTML/CSS to Image** (API Key) để chuyển HTML → PNG.
3. **Google Cloud Project** với:
   - **Google Drive API** (OAuth2) để upload ảnh.
   - **Google Sheets API** (OAuth2) để quản lý dữ liệu.
4. **Slack Workspace** và **Slack App** (API Token) để gửi thông báo.
5. **Google Sheet** đã chuẩn bị sẵn với các cột:
   - `Name`, `Designation`, `Email`, `Original Testimonial`, `Enhanced Testimonial`, `Image Link`, `Status` (Approved/Pending/Rejected), `Posted to Social`.
6. **Webhook URL** từ n8n để khách hàng gửi testimonial (ví dụ: `https://tên-domain-n8n.com/webhook/testimonial-webhook`).
:::

---

## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
Các sếp có thể:
- **Tải file JSON** từ [n8n.io/workflows/10135](https://n8n.io/workflows/10135) và import vào n8n Editor.
- **Copy/Paste JSON** từ file vào n8n Editor (đảm bảo không có lỗi syntax).

**Cách import:**
1. Mở **n8n Editor** → Nhấn `+` → Chọn `Import Workflow`.
2. Chọn file JSON hoặc dán JSON vào ô `Paste JSON`.
3. Nhấn `Import`.

---

### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow gồm **16 node** với các bước quan trọng sau. Các sếp **phải** cấu hình chính xác:

#### **🔹 Node 1: Webhook Trigger**
- **Path:** `testimonial-webhook` (không thay đổi).
- **HTTP Method:** `POST`.
- **Lưu ý:**
  - Cung cấp **URL webhook** này cho khách hàng hoặc form thu thập testimonial.
  - Ví dụ: `https://tên-domain-n8n.com/webhook/testimonial-webhook`.

#### **🔹 Node 2: Data Validation (Code)**
- **Mục đích:** Kiểm tra và chuẩn hóa dữ liệu đầu vào.
- **Lưu ý:**
  - Các trường bắt buộc: `name`, `testimonial_text`.
  - Trường `photo_url` và `email` là tùy chọn.
  - Nếu thiếu `photo_url`, hệ thống sẽ tự động tạo avatar từ tên (sử dụng UI Avatars API).

#### **🔹 Node 3: Set AI Prompt**
- **Mục đích:** Cấu hình prompt cho GPT-4.
- **Lưu ý:**
  - Đảm bảo prompt trong node `Set` là:
    ```json
    {
      "instruction": "Fix grammar and spelling. Keep it natural and conversational. Maintain enthusiasm. No fake details. Similar length to original."
    }
    ```

#### **🔹 Node 4: OpenAI Enhancement**
- **Model:** `gpt-4-1106-preview` (GPT-4 Turbo Preview).
- **Credentials:** Chọn `openAiApi` (đã cấu hình trước).
- **Lưu ý:**
  - Đảm bảo **API Key OpenAI** được cập nhật trong `Credentials` của n8n.
  - Ngân sách: GPT-4 có chi phí cao, nên **test với dữ liệu mẫu** trước khi chạy toàn bộ.

#### **🔹 Node 5: Extract AI Response (Code)**
- **Mục đích:** Lấy nội dung testimonial đã chỉnh sửa từ OpenAI.
- **Lưu ý:**
  - Code trong node này **không cần chỉnh sửa** (n8n tự động trích xuất).

#### **🔹 Node 6: Generate HTML Template (Code)**
- **Mục đích:** Tạo mẫu thẻ testimonial với HTML/CSS.
- **Lưu ý:**
  - Code đã tối ưu, **không cần chỉnh sửa** trừ khi muốn thay đổi design.
  - Thẻ bao gồm:
    - Hình ảnh khách hàng (hoặc avatar tự động).
    - Tên, chức vụ.
    - Nội dung testimonial.
    - Rating 5 sao.
    - Background gradient.

#### **🔹 Node 7: HTML/CSS to Image**
- **Service:** [htmlcsstoimg.com](https://htmlcsstoimg.com).
- **Credentials:** Chọn `htmlcsstoimgApi`.
- **Lưu ý:**
  - **API Key** phải được cập nhật trong `Credentials` của n8n.
  - Kích thước mặc định: `800x600px`.

#### **🔹 Node 8: Download Image (HTTP Request)**
- **Method:** `GET`.
- **URL:** Lấy từ node `HTML/CSS to Image`.
- **Lưu ý:**
  - Đảm bảo `Response Format` là `Binary`.

#### **🔹 Node 9: Upload to Google Drive**
- **Credentials:** Chọn `googleDriveOAuth2Api`.
- **Folder:** Chọn `testimonial data` (hoặc tạo mới).
- **File Name Format:**
  ```
  {Name}_Testimonial_{Timestamp}.png
  ```
  (Ví dụ: `Sarah_Johnson_Testimonial_20240520.png`).

#### **🔹 Node 10: Update Google Sheet**
- **Credentials:** Chọn `googleSheetsOAuth2Api`.
- **Operation:** `appendOrUpdate`.
- **Lưu ý:**
  - Đảm bảo **Google Sheet** có cấu trúc đúng với các cột đã đề cập ở trên.
  - Nếu cột `Status` chưa có, hệ thống sẽ tự động tạo.

#### **🔹 Node 11: Send Slack Notification**
- **Credentials:** Chọn `slackApi`.
- **Lưu ý:**
  - Chọn **channel** muốn gửi thông báo (ví dụ: `#marketing`).
  - Nội dung thông báo bao gồm:
    - Tên, chức vụ, email khách hàng.
    - So sánh giữa `Original Testimonial` và `Enhanced Testimonial`.
    - Link preview ảnh.
    - Trạng thái (`Approved/Pending`).

#### **🔹 Node 12: Every 5 Minutes (Schedule Trigger)**
- **Lưu ý:**
  - Thiết lập **lịch trình** chạy mỗi **5 phút** để kiểm tra Google Sheet.
  - Đảm bảo node này **active** để workflow hoạt động liên tục.

#### **🔹 Node 13: IF Approved & Not Posted**
- **Logic:**
  - **TRUE path:** Chỉ chạy nếu `Status = Approved` **và** `Posted to Social = false`.
  - **FALSE path:** Bỏ qua nếu chưa được Approved hoặc đã Posted.

#### **🔹 Node 14: Notify Ready to Post**
- **Nội dung thông báo:**
  - Thông báo Slack khi testimonial **sẵn sàng đăng tải**.
  - Kèm **text social media ready** và hashtags.

#### **🔹 Node 15: Mark as Posted**
- **Operation:** `update`.
- **Lưu ý:**
  - Cập nhật cột `Posted to Social` thành `true` khi đã đăng tải.

---

### **3. Kích Hoạt ⚡️ Workflow**
1. **Test Run với Dữ Liệu Mẫu:**
   - Gửi **payload JSON** dưới đây đến webhook:
     ```json
     {
         "name": "Sarah Johnson",
         "designation": "Marketing Director",
         "photo_url": "https://i.pravatar.cc/400?img=5",
         "testimonial_text": "Working with this team was amazing!",
         "email": "sample@gmail.com"
     }
     ```
   - **Kết quả dự kiến:**
     - Testimonial được cải tiến trong **15-30 giây**.
     - Ảnh được upload lên Google Drive.
     - Dữ liệu được thêm vào Google Sheet.
     - Thông báo Slack được gửi.

2. **Bật Active Workflow:**
   - Nhấn `Active` trên tab `Workflow` trong n8n Editor.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::tip[CÁCH LÀM THÊM]
1. **Kết hợp với Slack/Telegram Bot:**
   - Thay vì chỉ Slack, các sếp có thể **gửi thông báo qua Telegram** bằng node `telegram`.
   - Cài đặt bot Telegram và thêm node `telegram` vào workflow.

2. **Lưu Log Dữ Liệu:**
   - Thêm node `set` hoặc `code` để lưu **log hoạt động** (ví dụ: thời gian xử lý, lỗi nếu có) vào Google Sheets hoặc Google Drive.

3. **Gửi Báo Cáo Định Kỳ:**
   - Sử dụng **schedule trigger** (ví dụ: hàng tuần) để gửi **báo cáo tổng hợp** tất cả testimonials đã Approved/Pending.

4. **Tích Hợp với CRM (HubSpot/Zoho):**
   - Thêm node `hubspot` hoặc `zoho` để tự động thêm testimonial vào hồ sơ khách hàng.

5. **Tối Ưu Chi Phí OpenAI:**
   - Sử dụng **GPT-3.5 Turbo** thay vì GPT-4 nếu ngân sách hạn chế (nhưng chất lượng sẽ thấp hơn).
   - **Cache response** của OpenAI để tránh trùng lặp (sử dụng node `set` + `code`).
:::

---

## 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc thủ công, đồng thời **nâng cao chất lượng** của nội dung marketing. Bằng cách kết hợp **AI (GPT-4), tự động hóa (n8n), và quản lý dữ liệu (Google Sheets)**, các sếp có thể:
✅ **Tự động thu thập và cải tiến** tất cả testimonials.
✅ **Tạo thẻ hình ảnh chuyên nghiệp** mà không cần kỹ năng thiết kế.
✅ **Quản lý trung tâm hóa** trên Google Sheets.
✅ **Hoạt động 24/7** với thông báo tự động.

**Hành động ngay hôm nay:**
1. **Cài đặt n8n trên VPS** (Self-hosted) để workflow chạy ổn định.
2. **Import workflow** và cấu hình credentials.
3. **Test với dữ liệu mẫu** và bật Active.
4. **Chia sẻ với team** để bắt đầu tự động hóa!

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**Chia sẻ và hỏi đáp:**
💬 Có thắc mắc về workflow? Để lại comment bên dưới hoặc liên hệ qua [n8n Community](https://community.n8n.io/).