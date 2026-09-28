---
title: "🚀 Tự Động Hóa Theo Dõi Lead Tích Hợp Email, SMS & WhatsApp - Giảm Thiểu 80% Thời Gian Làm Thủ Công"
description: "Workflow tự động hóa theo dõi lead từ FollowUpBoss sang Email (Gmail), SMS (Twilio) và WhatsApp, với logic phân loại thông minh và cá nhân hóa tin nhắn. Giúp doanh nghiệp giảm thiểu 80% công việc thủ công, tăng tỷ lệ chuyển đổi và tối ưu hóa thời gian cho đội ngũ bán hàng."
slug: "tieu-dong-hoa-theo-doi-lead-email-sms-whatsapp"
tags: [n8n, automation, no-code, CRM, sales-automation, follow-up-boss, twilio, gmail]
keywords: [tự động hóa lead follow-up, n8n workflow, tự động hóa bán hàng, CRM tự động, gửi email và sms tự động, theo dõi lead tự động]
---

# 🚀 **Tự Động Hóa Theo Dõi Lead Tích Hợp Email, SMS & WhatsApp - Giải Pháp Tối Ưu Cho Đội Ngũ Bán Hàng**

---

## **📌 Nỗi Đau Của Các Sếp Trong Quá Trình Theo Dõi Lead**
Hàng ngày, đội ngũ bán hàng phải:
- **Làm thủ công** việc theo dõi lead từ CRM (FollowUpBoss) sang Email, SMS và WhatsApp.
- **Phân loại từng lead** để gửi tin nhắn phù hợp (Email chỉ, SMS chỉ, hoặc cả hai).
- **Lo lắng về tính chính xác** của thông tin (email sai, số điện thoại không hợp lệ) dẫn đến tin nhắn bị phản hồi hoặc thất bại.
- **Mất thời gian** để cá nhân hóa nội dung tin nhắn cho từng lead, khiến quá trình trở nên chậm chạp và không hiệu quả.

**Kết quả?** Lead bị bỏ qua, tỷ lệ chuyển đổi giảm, và đội ngũ bán hàng phải làm việc thêm giờ để hoàn thành công việc.

---
### **🎯 Kết Quả Các Sếp Nhận Được**
Sau khi triển khai workflow này, các sếp sẽ:
✅ **Tiết kiệm 80% thời gian** làm thủ công theo dõi lead.
✅ **Tăng tỷ lệ chuyển đổi** nhờ tin nhắn cá nhân hóa và logic phân loại thông minh.
✅ **Tránh mất tin nhắn** do email hoặc số điện thoại không hợp lệ.
✅ **Hoạt động 24/7** mà không cần can thiệp của con người.
✅ **Tối ưu hóa nguồn lực** cho đội ngũ bán hàng, giúp họ tập trung vào việc bán hàng chứ không phải làm thủ công.

---

## **🔧 Yêu Cầu Cần Thiết**
Để workflow này hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản FollowUpBoss** (API Key để lấy dữ liệu lead).
2. **Tài khoản Gmail** (đã kích hoạt OAuth 2.0 cho n8n).
3. **Tài khoản Twilio** (để gửi SMS và WhatsApp):
   - **Twilio Account SID** và **Auth Token**.
   - **Số điện thoại Twilio** (để gửi tin nhắn).
   - **Số điện thoại WhatsApp** (nếu muốn gửi qua WhatsApp, cần số WhatsApp Business).
4. **n8n Self-hosted** (để workflow chạy 24/7 ổn định).

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

## **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
- **Tải file JSON** từ [đây](https://n8n.io/workflows/9738) (hoặc sử dụng link gốc).
- **Mở n8n Editor** → Nhấn **Import** → Chọn file JSON hoặc dán JSON vào ô **Import Workflow**.

### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này có **3 logic chính** để phân loại lead và gửi tin nhắn phù hợp:

#### **🔹 Bước 1: Lấy Dữ Liệu Lead Từ FollowUpBoss**
- **Node: "Get Last Lead (FUB)"** (HTTP Request)
  - **Credentials**: Chọn `httpBasicAuth` (đã cấu hình trước khi import).
  - **URL**: `https://api.followupboss.com/api/v1/leads` (hoặc URL API của FollowUpBoss).
  - **Headers**:
    ```
    Authorization: Basic {API_KEY}
    Content-Type: application/json
    ```
  - **Query Parameters**:
    ```
    since={last_run_time}  // Tham số này sẽ được lấy từ node "Get Last time run"
    ```

#### **🔹 Bước 2: Lọc Lead Hợp Lệ (Email & Số Điện Thoại)**
- **Node: "False Email or False Phone" (IF)**
  - **Condition**: Kiểm tra nếu `email` hoặc `phone` là `null` hoặc không hợp lệ.
- **Node: "Invalid Number and Email" (Filter)**
  - **Condition**: Loại bỏ lead có email hoặc số điện thoại không hợp lệ.

#### **🔹 Bước 3: Phân Loại Lead & Gửi Tin Nhắn**
Workflow chia lead thành **3 trường hợp**:
1. **Full data → Send both Email + SMS/WhatsApp** (nếu email và số điện thoại đều hợp lệ).
2. **Missing/Invalid phone → Email only** (nếu số điện thoại không hợp lệ).
3. **Missing/Invalid email → SMS/WhatsApp only** (nếu email không hợp lệ).

##### **Cấu Hình Node "Send Email" (Gmail)**
- **Credentials**: Chọn `gmailOAuth2` (đã cấu hình trước).
- **To**: `{{$json["email"]}}`
- **Subject**: `Cá nhân hóa theo lead` (ví dụ: `Xin chào {{$json["first_name"]}}, đây là tin nhắn theo dõi từ chúng tôi...`).
- **Body**: Nội dung tin nhắn cá nhân hóa (sử dụng `{{$json["custom_field"]}}` nếu có).

##### **Cấu Hình Node "Send SMS/Whatsapp" (Twilio)**
- **Credentials**: Chọn `twilioApi`.
- **To**: `whatsapp:+{{$json["phone"]}}` (nếu gửi WhatsApp) hoặc `sms:+{{$json["phone"]}}` (nếu gửi SMS).
- **Body**: Nội dung tin nhắn (ví dụ: `Xin chào {{$json["first_name"]}}, chúng tôi đang theo dõi lead của bạn...`).

#### **🔹 Bước 4: Cập Nhật Thời Gian Cuối Cùng**
- **Node: "Get Last time run" & "Last Time Run" (Code)**
  - **Mục đích**: Lưu thời gian cuối cùng workflow chạy để tránh lấy lại lead cũ.
  - **Code mẫu** (nếu cần chỉnh sửa):
    ```javascript
    // Get current time
    const currentTime = new Date().toISOString();
    // Set sticky note for next run
    $node.set("lastRunTime", currentTime);
    ```

#### **🔹 Bước 5: Kích Hoạt Workflow ⚡️**
- **Test Run**: Nhấn **Run Workflow** với dữ liệu mẫu để kiểm tra.
- **Bật Active**: Sau khi kiểm tra thành công, nhấn **Active** để workflow chạy tự động theo lịch.

---

## **✍️ Mẹo & Gợi Ý Nâng Cao**
1. **Kết Nối Với Slack/Telegram**
   - Thêm node **Slack/Telegram** để thông báo khi workflow chạy thành công hoặc gặp lỗi.
   - Ví dụ: Gửi tin nhắn "Workflow đã hoàn tất, có {{count}} lead mới được xử lý".

2. **Lưu Log & Báo Cáo**
   - Sử dụng node **Google Sheets** hoặc **Airtable** để lưu lịch sử gửi tin nhắn.
   - Tạo báo cáo định kỳ (hàng tuần) về số lead được theo dõi và tỷ lệ phản hồi.

3. **Cá Nhân Hóa Tin Nhắn**
   - Sử dụng **LLM (n8n-nodes-ai.assistant)** để tự động viết tin nhắn cá nhân hóa dựa trên dữ liệu lead.
   - Ví dụ: Nếu lead có `custom_field = "interested_in_product_X"`, tin nhắn sẽ đề cập đến sản phẩm đó.

4. **Tối Ưu Hóa Lịch Scheduling**
   - Đặt lịch chạy workflow vào giờ làm việc (ví dụ: 9h sáng) để tránh gửi tin nhắn vào ban đêm.

---

## **📌 Kết Luận**
Workflow này là **giải pháp hoàn hảo** để tự động hóa quá trình theo dõi lead, giúp đội ngũ bán hàng **tiết kiệm thời gian, tăng tỷ lệ chuyển đổi và tối ưu hóa hiệu suất**. Với logic phân loại thông minh và tích hợp Email, SMS & WhatsApp, các sếp không cần lo lắng về việc bỏ qua lead nào.

**Hành động ngay hôm nay!**
1. **Import workflow** và cấu hình các credentials.
2. **Test run** với dữ liệu mẫu.
3. **Bật Active** và để n8n làm việc cho bạn!

---
**💬 Có thắc mắc?** Để lại bình luận bên dưới hoặc liên hệ với tác giả [Fabian Perez](https://n8n.io/workflows/9738) để được hỗ trợ chi tiết! 🚀