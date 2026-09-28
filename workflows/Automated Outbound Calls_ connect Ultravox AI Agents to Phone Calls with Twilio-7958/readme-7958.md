---
title: "📞 🤖 Tự Động Hoá Gọi Điện Thoại AI: Kết Nối Ultravox AI Agents Với Twilio (Không Cần Code)"
description: "Workflow này biến n8n thành hệ thống tự động gọi điện AI, cho phép các agent AI Ultravox trò chuyện trực tiếp với người dùng qua điện thoại thông qua Twilio. Giảm thiểu chi phí nhân sự, tăng cường trải nghiệm khách hàng 24/7."
slug: "tự-dộng-hoá-gọi-điện-thoại-ai-ultravox-twilio"
tags: [n8n, automation, ai-chatbot, twilio, ultravox, no-code, outbound-calls]
keywords: [tự động hóa gọi điện AI, twilio n8n, ultravox ai agents, gọi điện tự động không code, chatbot điện thoại, tự động hóa marketing]
---

# 🚀 **Tự Động Hoá Gọi Điện Thoại AI: Kết Nối Ultravox Agents Với Twilio**

### **Giải pháp cho các sếp muốn:**
- **Tiết kiệm chi phí nhân sự** với gọi điện tự động AI 24/7.
- **Tăng trải nghiệm khách hàng** với cuộc gọi tự động hóa, cá nhân hóa.
- **Kết nối AI với điện thoại thực tế** mà không cần viết một dòng code.

---
## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần gọi điện thủ công, tự động hóa toàn bộ quy trình.
- **Chính xác & cá nhân hóa**: AI Ultravox xử lý cuộc gọi với giọng nói tự nhiên và logic chatbot.
- **Hoạt động liên tục**: Gọi điện bất kỳ lúc nào, không giới hạn giờ làm việc.
- **Tích hợp AI đa phương thức**: Kết hợp giọng nói, công cụ và logic AI để tối ưu hóa cuộc gọi.
:::

---
## 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần:
1. **Tài khoản Twilio** (để mua số điện thoại và cấu hình API):
   - [Twilio Console](https://www.twilio.com/)
   - **Account SID** và **Auth Token** (tìm trong **Project Settings**).
   - **Số điện thoại Twilio** (mua trong **Phone Numbers**).

2. **Tài khoản Ultravox AI** (để tạo agent AI):
   - [Ultravox App](https://app.ultravox.ai/)
   - **Agent ID** (tạo từ **Agents > New Agent**).

3. **n8n Workflow Editor** (cài đặt [n8n Cloud](https://n8n.io/) hoặc [Self-hosted](https://docs.n8n.io/)).
:::

---
## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/7958) hoặc copy/paste JSON từ trang này.
- Mở **n8n Editor** → **Import Workflow** → Chọn file JSON hoặc dán JSON vào ô nhập liệu.

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này gồm **4 node chính**, các sếp cần cấu hình như sau:

#### **Node 1: "Start Manually" (manualTrigger)**
- **Chức năng**: Khởi động workflow thủ công.
- **Cách sử dụng**: Click vào nút **Execute Workflow** khi muốn gọi điện.

#### **Node 2: "Set Params" (set)**
- **Cấu hình bắt buộc**:
  - **`agent_id`**: ID của agent Ultravox (đã tạo ở **STEP 2**).
  - **`twilio_number`**: Số điện thoại Twilio (ví dụ: `+1234567890`).
  - **`phone_number`**: Số điện thoại người dùng (ví dụ: `+84123456789`).

#### **Node 3: "Twilio Call" (twilio)**
- **Cấu hình bắt buộc**:
  - **Credentials**: Chọn **twilioApi** (đã cấu hình trong **n8n Credentials**).
  - **Resource**: Chọn **call**.
  - **Tham số cần điền**:
    - **`to`**: Số điện thoại người dùng (từ `phone_number` ở node `Set Params`).
    - **`from`**: Số điện thoại Twilio (từ `twilio_number` ở node `Set Params`).
    - **`url`**: URL của API Ultravox (cấu hình trong **httpHeaderAuth** ở node tiếp theo).

#### **Node 4: "Create Ultravox Call" (httpRequest)**
- **Cấu hình bắt buộc**:
  - **Credentials**: Chọn **httpHeaderAuth** (nếu Ultravox yêu cầu).
  - **Method**: POST.
  - **URL**: URL API của Ultravox (thường là `https://api.ultravox.ai/voice/calls`).
  - **Headers**:
    - `Authorization`: `Bearer YOUR_ULTRAVOX_API_KEY` (nếu có).
    - `Content-Type`: `application/json`.
  - **Body (JSON)**:
    ```json
    {
      "agent_id": "{{ $node["Set Params"].json["agent_id"] }}",
      "caller_id": "{{ $node["Set Params"].json["twilio_number"] }}",
      "recipient_number": "{{ $node["Set Params"].json["phone_number"] }}"
    }
    ```

### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Điền số điện thoại mẫu vào `phone_number` và chạy workflow.
   - Kiểm tra liệu cuộc gọi có được kết nối thành công không.
2. **Bật Active**:
   - Sau khi test thành công, chuyển workflow sang **Active**.

---
## ✍️ **Mẹo & gợi ý nâng cao**
:::note[CÁC Ý TƯỞNG MỞ RỘNG]
- **Gửi thông báo trước khi gọi**: Kết hợp với **Slack/Telegram** để thông báo cho nhân viên khi có cuộc gọi mới.
- **Lưu log cuộc gọi**: Sử dụng **Google Sheets** hoặc **Airtable** để ghi lại lịch sử cuộc gọi.
- **Gửi báo cáo định kỳ**: Tích hợp **Google Calendar** để gửi báo cáo tổng hợp hàng tuần.
- **Tối ưu AI**: Cập nhật **System Prompt** của Ultravox để cải thiện chất lượng cuộc gọi.
:::

---
## 📌 **Kết luận**
Workflow này giúp các sếp **tự động hóa gọi điện AI một cách đơn giản**, tiết kiệm thời gian và chi phí. **Không cần code**, chỉ cần cấu hình vài bước là có thể kết nối Ultravox AI với Twilio để gọi điện tự động hóa.

**👉 Bắt đầu ngay!**
1. Mua số điện thoại Twilio.
2. Tạo agent Ultravox.
3. Import workflow và cấu hình.
4. Chạy và tự động hóa gọi điện!

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::