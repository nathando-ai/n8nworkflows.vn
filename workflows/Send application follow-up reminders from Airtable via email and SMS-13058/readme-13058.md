---
title: "📩 Tự Động Gửi Lại Lời Nhắc Nhở Ứng Tuyển từ Airtable qua Email & SMS – Giảm 10+ giờ/năm cho Doanh Nghiệp"
description: "Workflow tự động hóa gửi email và SMS nhắc nhở ứng viên theo dõi tiến độ ứng tuyển từ Airtable, giảm thiểu công việc thủ công và tăng cường trải nghiệm ứng viên. Giúp các sếp tiết kiệm thời gian, giảm lỗi và tự động hóa quy trình tuyển dụng."
slug: "tu-dong-ho-gui-lai-loi-nhac-nhom-ung-tuyen"
tags: ["n8n", "automation", "lead-nurturing", "airtable", "sendinblue", "sms-automation", "tuyen-dung"]
keywords: ["tự động hóa tuyển dụng n8n", "gửi email nhắc nhở ứng viên", "sms tự động từ airtable", "tự động hóa nhắc nhở ứng tuyển", "airtable + email + sms"]
---

# 🚀 **Tự Động Gửi Lại Lời Nhắc Nhở Ứng Tuyển từ Airtable qua Email & SMS**

### **Giải quyết vấn đề gì?**
Các sếp đã từng gặp tình huống này chưa?
- Ứng viên đã nộp hồ sơ nhưng không nhận được phản hồi kịp thời → **tỷ lệ chuyển đổi thấp**.
- Các sếp phải **gõ tay** gửi email/SMS nhắc nhở → **tốn thời gian, dễ quên, và không chuyên nghiệp**.
- Không theo dõi được tiến độ ứng viên → **trải nghiệm ứng viên xấu, mất cơ hội tuyển dụng chất lượng**.

**Workflow này tự động hóa toàn bộ quy trình nhắc nhở ứng viên qua email và SMS từ Airtable**, giúp các sếp:
✅ **Tiết kiệm 10+ giờ/năm** (không phải làm thủ công).
✅ **Tăng tỷ lệ phản hồi** từ ứng viên (do nhắc nhở tự động).
✅ **Cải thiện trải nghiệm ứng viên** (nhắc nhở chuyên nghiệp, không quên).
✅ **Tự động hóa tuyển dụng** (không phụ thuộc vào người).

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động nhắc nhở ứng viên** qua email và SMS khi hồ sơ chưa được xử lý.
- **Tiết kiệm thời gian** so với việc gõ tay gửi email/SMS.
- **Tăng tỷ lệ phản hồi** từ ứng viên (do nhắc nhở kịp thời).
- **Cải thiện trải nghiệm ứng viên** (nhắc nhở chuyên nghiệp, không quên).
- **Dễ dàng mở rộng** cho nhiều vòng tuyển dụng khác nhau.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi chạy workflow, các sếp cần chuẩn bị:
✔ **Tài khoản Airtable** (để lấy dữ liệu ứng viên).
✔ **Tài khoản SendinBlue** (để gửi email tự động).
✔ **API Key SendinBlue** (để kết nối với SendinBlue).
✔ **Số điện thoại ứng viên** (để gửi SMS, có thể lấy từ Airtable hoặc nhập thủ công).
✔ **Mô hình nhắc nhở** (ví dụ: "Chúng tôi đang xem xét hồ sơ của bạn. Vui lòng cho biết tiến độ.").

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Workflow này được xây dựng trên nền tảng **n8n**, các sếp có thể:
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/13058) và import vào n8n Editor.
- **Copy/Paste JSON** từ file vào n8n Editor (đảm bảo không có lỗi cú pháp).

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này sử dụng các **node chính** sau (các sếp cần cấu hình kỹ lưỡng):

##### **A. Node Airtable (n8n-nodes-base.airtable)**
- **Tham số cần điền:**
  - **API Key**: API Key của Airtable (tạo tại [Airtable API](https://airtable.com/api)).
  - **Base ID**: ID của bảng dữ liệu ứng viên (thường là một chuỗi dài ở URL của bảng).
  - **View Name**: Tên của view (lọc dữ liệu ứng viên cần nhắc nhở).
  - **Filter**: Lọc ứng viên chưa được phản hồi (ví dụ: `Status = "Chưa phản hồi"`).

##### **B. Node Schedule Trigger (n8n-nodes-base.scheduleTrigger)**
- **Tham số cần điền:**
  - **Schedule**: Thời gian nhắc nhở (ví dụ: **mỗi ngày 9h** để nhắc nhở ứng viên sáng sớm).
  - **Time Zone**: Chọn múi giờ phù hợp (ví dụ: `Asia/Ho_Chi_Minh`).

##### **C. Node Set (n8n-nodes-base.set)**
- **Tham số cần điền:**
  - **Variable**: Đặt tên biến để lưu trữ dữ liệu ứng viên (ví dụ: `{{ $json["fields"]["Email"] }}`).
  - **Value**: Lấy email/SĐT từ Airtable (ví dụ: `{{ $json["fields"]["Phone"] }}`).

##### **D. Node SendinBlue Email (n8n-nodes-base.sendInBlue)**
- **Tham số cần điền:**
  - **API Key**: API Key của SendinBlue (tạo tại [SendinBlue Dashboard](https://app.sendinblue.com/)).
  - **From Email**: Email gửi (ví dụ: `noreply@công-ty.com`).
  - **To Email**: Email ứng viên (lấy từ Airtable).
  - **Subject**: Tiêu đề email (ví dụ: **"Lời nhắc nhở: Tiến độ ứng tuyển của bạn"**).
  - **HTML Content**: Nội dung email (có thể sử dụng **template động** từ Airtable).

##### **E. Node HTTP Request (n8n-nodes-base.httpRequest)**
- **Tham số cần điền:**
  - **Method**: `POST` (để gửi SMS).
  - **URL**: API của dịch vụ SMS (ví dụ: **Twilio, Plivo, hoặc API SMS của SendinBlue**).
  - **Headers**: Thêm `Content-Type: application/json`.
  - **Body**: JSON chứa số điện thoại và nội dung SMS (ví dụ: `{"to": "{{ $json["fields"]["Phone"] }}", "message": "Xin chào, chúng tôi đang xem xét hồ sơ của bạn. Vui lòng cho biết tiến độ."}`).

##### **F. Node Sticky Note (n8n-nodes-base.stickyNote)**
- **Tham số cần điền:**
  - **Content**: Ghi chú cho các sếp (ví dụ: **"Workflow này sẽ gửi nhắc nhở tự động cho ứng viên chưa được phản hồi."**).

---

#### **3. Kích hoạt ⚡️**
- **Test Run**: Chạy thử với **1-2 ứng viên mẫu** để kiểm tra email/SMS có được gửi đúng không.
- **Bật Active**: Sau khi kiểm tra thành công, **bật workflow** để hoạt động 24/7.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Kết hợp với Slack/Telegram**:
   - Thêm **node Slack/Telegram** để thông báo khi workflow gửi nhắc nhở thành công.
   - Ví dụ: `{{ $json["fields"]["Name"] }} đã được gửi nhắc nhở qua email và SMS!`.

2. **Lưu log hoạt động**:
   - Sử dụng **node Code** để ghi log vào Airtable (ví dụ: `Status = "Đã nhắc nhở"`).

3. **Gửi báo cáo định kỳ**:
   - Tạo **workflow riêng** để tổng hợp số lượng ứng viên đã được nhắc nhở và gửi báo cáo cho team HR.

4. **Tùy chỉnh nội dung nhắc nhở**:
   - Sử dụng **node Code** để thay đổi nội dung email/SMS dựa trên **trạng thái ứng viên** (ví dụ: "Chúng tôi đang xem xét hồ sơ của bạn" vs. "Hồ sơ của bạn đã được lựa chọn!").

---

### 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc nhắc nhở ứng viên thủ công, đồng thời **tăng tỷ lệ phản hồi** và **cải thiện trải nghiệm ứng viên**. **Hãy áp dụng ngay** và tự động hóa quy trình tuyển dụng của mình!

👉 **Bắt đầu tự động hóa tuyển dụng ngay hôm nay!** [Tải workflow từ n8n](https://n8n.io/workflows/13058) và cài đặt trên VPS của mình. 🚀