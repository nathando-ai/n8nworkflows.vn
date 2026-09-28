---
title: "📞 Tự Động Hoàn Tất Cả Lời Nhắc Nhở Đặt Chỗ Nhà Hàng Với Grok-4 & Twilio - Không Cần Code!"
description: "Workflow tự động gọi điện nhắc nhở khách hàng về lịch đặt chỗ nhà hàng bằng AI Grok-4 và Twilio, tiết kiệm thời gian quản lý và tăng trải nghiệm khách hàng. Hoàn toàn tự động hóa từ việc lấy dữ liệu Google Sheets đến gọi điện cá nhân hóa."
slug: "tieu-dong-hoan-tat-loi-nhac-nhom-dat-cho-nhan-hang-grok-4-twilio"
tags: [n8n, automation, no-code, ai-chatbot, twilio, google-sheets, grok-4, marketing]
keywords: [tự động hóa gọi điện nhắc nhở đặt chỗ, n8n workflow, grok-4, twilio api, tự động hóa nhà hàng, nhắc nhở khách hàng, ai-powered automation]
---

# 🚀 **Tự Động Hoàn Tất Cả Lời Nhắc Nhở Đặt Chỗ Nhà Hàng Với Grok-4 & Twilio**

### **Giải Phẫu Nỗi Đau Của Quản Lý Nhà Hàng**
Các sếp nhà hàng đã từng phải:
- **Gọi điện thủ công** để nhắc nhở khách hàng về lịch đặt chỗ, tốn thời gian và dễ quên.
- **Sử dụng tin nhắn SMS** nhưng nội dung nhắc nhở thiếu cá nhân hóa, không thể tương tác.
- **Lo lắng khách hàng quên đặt chỗ**, dẫn đến tỷ lệ hủy booking cao.
- **Không có cách nào tự động** để gửi lời nhắc nhở **cá nhân hóa** với giọng nói tự nhiên và thông tin chính xác.

**Workflow này giải quyết tất cả!** Dùng **AI Grok-4** để tạo nội dung gọi điện tự nhiên, **Twilio** để thực hiện cuộc gọi tự động, và **Google Sheets** để quản lý dữ liệu khách hàng. **Không cần viết một dòng code nào!**

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7** và **không bị gián đoạn**, các sếp nên cài **n8n trên VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới **39%**)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (đảm bảo tốc độ cao, không lag)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian** – Không cần gọi điện thủ công, tự động nhắc nhở khách hàng.
✅ **Nội dung gọi điện cá nhân hóa** – Grok-4 tạo ra lời nhắc nhở **tự nhiên, thân thiện** như người thật.
✅ **Tỷ lệ thành công cao** – Khách hàng ít quên đặt chỗ hơn, giảm tỷ lệ hủy booking.
✅ **Hoạt động 24/7** – Workflow chạy tự động theo lịch trình, không phụ thuộc vào giờ làm việc.
✅ **Dễ dàng mở rộng** – Thêm thông tin bổ sung (ví dụ: menu đặc biệt, sự kiện) vào lời nhắc nhở.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Twilio** (để gọi điện):
   - Mua một **số điện thoại Twilio** (để gọi khách hàng).
   - Cấu hình **Text-to-Speech (TTS)** với ngôn ngữ Việt (hoặc ngôn ngữ khách hàng).
   - Cấu hình **geo permissions** (nếu gọi quốc tế).
   - **API Key Twilio** (để kết nối với n8n).

2. **Tài khoản Google Sheets**:
   - **Clone Google Sheet mẫu** từ [đây](https://docs.google.com/spreadsheets/d/1lQh-199bQe-HKwmVI_6cS-Xv1OiGo1B4-OpR6kbNg7E/edit?usp=sharing).
   - **Cột Phone** phải chứa **số điện thoại quốc tế** (không có dấu `+`).
   - Cấu hình **OAuth 2.0** cho Google Sheets trong n8n.

3. **Tài khoản OpenRouter (để sử dụng Grok-4)**:
   - Đăng ký tại [OpenRouter](https://openrouter.ai/) và lấy **API Key**.
   - Cấu hình **credentials** trong n8n với tên `openRouterApi`.

4. **n8n Self-hosted** (để chạy workflow 24/7):
   - Cài đặt trên **VPS** (khuyến nghị sử dụng [TinoHost](https://tino.vn/vps-n8n?affid=388) hoặc [BNIX](https://my.bnix.one/aff.php?aff=172)).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [workflow gốc](https://n8n.io/workflows/6135) và import vào **n8n Editor**.
- **Cách 2**: Copy toàn bộ JSON từ [đây](https://n8n.io/workflows/6135) và paste vào **Create Workflow** → **Import JSON**.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
##### **A. Cấu Hình Twilio (Node "Make a call")**
- **Credentials**:
  - Chọn `twilioApi` (đã cấu hình trước khi import).
- **Key Parameters**:
  - **From**: Điền **số Twilio** của bạn (ví dụ: `+1234567890`).
  - **To**: Sử dụng **dữ liệu từ Google Sheets** (cột `Phone`).
  - **Url**: Điền URL của **Twilio Voice Response** (cấu hình TTS).
  - **Method**: Chọn `POST`.
  - **Body**:
    ```json
    {
      "To": "{{$node["Loop Over Items"].json["phone"]}}",
      "From": "{{$credentials["twilioApi"].accountSid}}",
      "Url": "https://handler.twilio.com/twiml/EYxXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX