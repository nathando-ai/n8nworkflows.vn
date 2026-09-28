---
title: "🚀 Tự Động Hóa Chăm Sóc Khách Hàng WhatsApp với Gallabox API + Drip Campaign Supabase (N8n)"
description: "Workflow tự động hóa chăm sóc khách hàng (lead nurturing) trên WhatsApp bằng Gallabox API và Supabase, giúp các sếp gửi tin nhắn tự động theo dõi, phân loại và chuyển đổi khách hàng hiệu quả 24/7."
slug: "tự-dộng-hoa-chăm-sóc-whatsapp-gallabox-supabase"
tags: [n8n, automation, lead-nurturing, gallabox-api, supabase, no-code]
keywords: [n8n workflow tự động hóa WhatsApp, Gallabox API tự động, drip campaign Supabase, tự động hóa chăm sóc khách hàng, tự động hóa marketing]
---

# 🚀 **Tự Động Hóa Chăm Sóc Khách Hàng WhatsApp với Gallabox API + Drip Campaign Supabase**

### **💡 Giải pháp cho các sếp: Tiết kiệm thời gian, tăng tỷ lệ chuyển đổi khách hàng mà không cần code!**
Hiện nay, việc chăm sóc khách hàng (lead nurturing) thủ công trên WhatsApp không chỉ tốn thời gian mà còn dễ gây mất mát do quên gửi tin nhắn hoặc gửi sai thời điểm. **Workflow này tự động hóa toàn bộ quy trình**, từ nhận lead đến gửi tin nhắn theo dõi, phân loại và chuyển đổi khách hàng một cách chính xác và cá nhân hóa.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow hoạt động ổn định 24/7, các sếp nên **self-host n8n** trên VPS riêng:
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### **🎯 Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động gửi tin nhắn WhatsApp cho khách hàng theo lịch trình đã thiết lập.
- **Tăng tỷ lệ chuyển đổi**: Drip campaign cá nhân hóa giúp khách hàng được chăm sóc một cách liên tục và hiệu quả.
- **Quản lý lead chuyên nghiệp**: Phân loại khách hàng theo trạng thái (disposition) và gửi tin nhắn phù hợp.
- **Hoạt động 24/7**: Không cần can thiệp thủ công, workflow chạy tự động theo lịch trình.
- **Lưu trữ dữ liệu an toàn**: Dữ liệu lead được lưu trữ trên **Supabase** (database cloud), dễ dàng theo dõi và phân tích.
:::

---

### **🔧 Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Gallabox API**:
   - API Key của Gallabox để gửi tin nhắn WhatsApp.
   - [Đăng ký Gallabox](https://gallabox.com/) và lấy API Key từ Dashboard.
2. **Tài khoản Supabase**:
   - Database Supabase để lưu trữ và quản lý lead.
   - [Đăng ký Supabase](https://supabase.com/) và lấy `supabaseApi` credentials (URL, Public Key, Private Key).
3. **Credentials trong n8n**:
   - Thiết lập **`supabaseApi`** trong n8n để kết nối với Supabase.
   - Thiết lập **`Gallabox API Key`** trong node `httpRequest` để gửi tin nhắn.

---

### **🚀 Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n.io/workflows/7064](https://n8n.io/workflows/7064) và import vào n8n Editor.
- **Cách 2**: Copy toàn bộ JSON từ link trên và paste vào **Import Workflow** trong n8n.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này bao gồm **31 node** và được cấu trúc theo logic sau:
- **Lấy lead từ Supabase** (`Get many rows1`) → **Phân loại lead** (`Switch2`, `Switch3`, `Switch4`, `Switch5`) → **Gửi tin nhắn WhatsApp** (`httpRequest`) → **Cập nhật trạng thái lead** (`Update a row1`, `Update a row2`, ...).

##### **🔹 Cấu hình quan trọng trong workflow:**
1. **Node `httpRequest` (Gallabox API)**:
   - **URL**: `https://api.gallabox.com/v1/messages` (hoặc URL chính thức của Gallabox).
   - **Headers**:
     - `Authorization: Bearer <API_KEY_GALLABOX>`
     - `Content-Type: application/json`
   - **Body**:
     ```json
     {
       "to": "{{$json.path('phone_number')}}",
       "message": "{{$json.path('message_content')}}",
       "type": "text"
     }
     ```
   - **Lưu ý**: Thay thế `{{$json.path('phone_number')}}` và `{{$json.path('message_content')}}` bằng dữ liệu từ Supabase.

2. **Node `Supabase` (Get many rows, Update a row)**:
   - **Credentials**: Chọn `supabaseApi` đã thiết lập trước đó.
   - **Table Name**: Đặt tên bảng trong Supabase (ví dụ: `leads`).
   - **Filter**: Cần thiết lập điều kiện lấy lead (ví dụ: `status = 'new'`).

3. **Node `Switch` (Phân loại lead)**:
   - **Condition**: Xác định điều kiện phân loại lead (ví dụ: `status = 'pending'`, `status = 'converted'`).
   - **Action**: Chọn drip campaign tương ứng (ví dụ: gửi tin nhắn nhắc nhở, tin nhắn cảm ơn, ...).

4. **Node `If` (Kiểm tra trạng thái HTTP)**:
   - **Status Code 202/203/204**: Kiểm tra phản hồi từ Gallabox API.
   - **If Interval**: Đặt thời gian chờ giữa các tin nhắn (ví dụ: 1 ngày).

5. **Node `Create Logs`**:
   - Lưu lịch sử hoạt động (ví dụ: khi gửi tin nhắn thành công/bất thành công).

##### **🔹 Ví dụ cấu hình node `httpRequest` (Gallabox):**
```json
{
  "name": "new_lead_0",
  "type": "httpRequest",
  "method": "POST",
  "url": "https://api.gallabox.com/v1/messages",
  "headers": {
    "Authorization": "Bearer YOUR_GALLABOX_API_KEY",
    "Content-Type": "application/json"
  },
  "body": {
    "to": "{{$json.path('phone_number')}}",
    "message": "Xin chào {{$json.path('name')}}, cảm ơn bạn đã liên hệ! Chúng tôi sẽ liên hệ lại trong 24h.",
    "type": "text"
  }
}
```

#### **3. Kích hoạt ⚡️**
- **Test run**: Chạy workflow với dữ liệu mẫu để kiểm tra logic.
- **Bật Active**: Sau khi kiểm tra thành công, bật workflow để chạy tự động.

---

### **✍️ Mẹo & gợi ý nâng cao**
1. **Kết hợp với Slack/Telegram**:
   - Thêm node `slack` hoặc `telegram` để thông báo khi lead được chuyển đổi thành công.
2. **Lưu log hoạt động**:
   - Sử dụng node `stickyNote` để ghi chú hoặc lưu log vào Supabase.
3. **Gửi báo cáo định kỳ**:
   - Sử dụng node `scheduleTrigger` để gửi báo cáo tổng hợp về lead đã chăm sóc.
4. **Tối ưu drip campaign**:
   - Thiết lập các drip campaign khác nhau cho từng nhóm lead (ví dụ: lead mới, lead tiềm năng, lead đã chuyển đổi).

---

### **📌 Kết luận**
Workflow này giúp các sếp **tự động hóa chăm sóc khách hàng trên WhatsApp một cách chuyên nghiệp**, tiết kiệm thời gian và tăng tỷ lệ chuyển đổi. **Hãy import ngay và bắt đầu sử dụng!** Nếu có vấn đề, các sếp có thể tham khảo [hướng dẫn chi tiết của Gallabox](https://docs.gallabox.com/) hoặc [Supabase](https://supabase.com/docs).

👉 **Bắt đầu tự động hóa ngay hôm nay!** 🚀