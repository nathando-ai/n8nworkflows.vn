---
title: "📅 Tự Động Hóa Lịch Hẹn Online với Google Calendar & Gmail - Không Cần Code"
description: "Workflow này tự động hóa việc nhận đơn đặt lịch từ form, đồng bộ lịch Google Calendar và gửi email xác nhận - tiết kiệm thời gian cho các sếp lên tới 8h/tuần. Hoàn toàn tự động, hoạt động 24/7."
slug: "tu-dong-hoa-lich-hen-online-google-calendar-gmail"
tags: [n8n, automation, no-code, google-calendar, gmail, booking-system]
keywords: [tự động hóa lịch hẹn, n8n workflow google calendar, tự động hóa email xác nhận, booking system no-code, tự động hóa lịch hẹn online]
---

# 🚀 **Tự Động Hóa Lịch Hẹn Online với Google Calendar & Gmail - Không Cần Code**

Hãy tưởng tượng một tình huống: Các sếp phải trả lời hàng chục email, tin nhắn hoặc gọi điện để xác nhận lịch hẹn hàng ngày. Thời gian và sự chán nản của nhân viên không chỉ làm giảm hiệu suất mà còn gây mất mát kinh tế lớn. **Workflow này giải quyết vấn đề này hoàn toàn tự động hóa** bằng cách:
1. **Hiển thị form đặt lịch** trên trang web của doanh nghiệp.
2. **Tự động đồng bộ lịch** vào Google Calendar khi khách hàng đặt lịch.
3. **Gửi email xác nhận** tự động đến khách hàng và các sếp.
4. **Hoạt động 24/7** mà không cần can thiệp thủ công.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần phải trả lời email hoặc gọi điện để xác nhận lịch (tiết kiệm **8h/tuần**).
- **Tăng trải nghiệm khách hàng**: Khách hàng nhận được email xác nhận ngay lập tức và không phải chờ đợi.
- **Lịch đồng bộ chính xác**: Không có xung đột lịch vì lịch được tự động cập nhật vào Google Calendar.
- **Hoạt động liên tục**: Workflow hoạt động 24/7, ngay cả khi các sếp nghỉ ngơi.
- **Dễ dàng mở rộng**: Có thể kết nối với Slack/Telegram để thông báo thêm hoặc lưu log lịch.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Google Calendar** và **API Key OAuth2** (để đồng bộ lịch).
2. **Tài khoản Gmail** và **API Key OAuth2** (để gửi email xác nhận).
3. **URL của n8n** (để khách hàng truy cập form đặt lịch).
4. **Thiết bị VPS** (để chạy workflow 24/7, khuyến nghị dùng VPS từ [TinoHost](https://tino.vn/vps-n8n?affid=388)).

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Truy cập [n8n Editor](https://n8n.io/editor) và tạo một workflow mới.
2. Nhấp vào **Import** và chọn file JSON (hoặc copy/paste JSON vào ô nhập liệu).
3. Nhấp **Import** để hoàn tất.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này có **hai đường dẫn chính**:
- **Đường dẫn GET (hiển thị form)**: Webhook → Get Calendar Events → Calculate Available Slots → Build HTML Form → Respond.
- **Đường dẫn POST (xử lý đặt lịch)**: Webhook → Calculate End Time → Create Calendar Event → Format Email Data → Send Confirmation → Show Success Page.

##### **Cấu hình chi tiết các node quan trọng:**
| **Node**                     | **Lưu ý cấu hình**                                                                                                                                                                                                 |
|------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Webhook - Submit Form**    | Đảm bảo **path** là `/booking` và **httpMethod** là `POST`.                                                                                                                                                     |
| **Webhook - Show Form**      | Đảm bảo **path** là `/booking` và **httpMethod** là `GET`.                                                                                                                                                     |
| **Get Calendar Events**      | Chọn **credentials** là `googleCalendarOAuth2Api` và **operation** là `getAll`.                                                                                                                              |
| **Calculate Available Slots**| Các sếp cần **cập nhật logic** trong node Code này để phù hợp với thời gian làm việc của mình (ví dụ: 9h-17h, chỉ cho phép đặt lịch trong khoảng thời gian này).                          |
| **Create Calendar Event**    | Chọn **credentials** là `googleCalendarOAuth2Api`. Các sếp cần **cập nhật tiêu đề và mô tả** của sự kiện để phù hợp với doanh nghiệp.                                                               |
| **Send Confirmation Email**  | Chọn **credentials** là `gmailOAuth2`. Các sếp cần **cập nhật nội dung email** (tiêu đề, nội dung) và **địa chỉ email gửi** (ví dụ: `no-reply@doanhnghiep.com`).                                       |
| **Build HTML Form**          | Các sếp có thể **cập nhật form** để phù hợp với yêu cầu đặt lịch của doanh nghiệp (ví dụ: thêm trường "Số điện thoại", "Dự án", "Ghi chú").                                                          |

##### **Cập nhật logic trong node Code (Calculate Available Slots)**
Các sếp cần mở node **Calculate Available Slots** và chỉnh sửa mã JavaScript để phù hợp với:
- **Thời gian làm việc** (ví dụ: chỉ cho phép đặt lịch từ 9h-17h).
- **Thời gian slot** (ví dụ: 30 phút, 1 giờ).
- **Người dùng có thể chọn** (ví dụ: chỉ cho phép chọn ngày trong tuần).

Mẫu mã JavaScript cơ bản:
```javascript
// Ví dụ: Chỉ cho phép đặt lịch từ 9h-17h, slot 30 phút
const availableSlots = [];
const startTime = new Date();
startTime.setHours(9, 0, 0, 0);

const endTime = new Date();
endTime.setHours(17, 0, 0, 0);

while (startTime <= endTime) {
    availableSlots.push({
        time: startTime.toISOString(),
        displayTime: startTime.toLocaleTimeString([], { hour: '2-digit', minute: '2-digit' })
    });
    startTime.setMinutes(startTime.getMinutes() + 30);
}

return { json: { availableSlots } };
```

##### **Cập nhật nội dung email (Send Confirmation Email)**
Các sếp cần mở node **Format Email Data** và chỉnh sửa mã JavaScript để phù hợp với:
- **Tiêu đề email** (ví dụ: "Xác nhận lịch hẹn thành công").
- **Nội dung email** (ví dụ: bao gồm thông tin lịch, địa điểm, và link hủy lịch).

Mẫu mã JavaScript cơ bản:
```javascript
// Ví dụ: Tạo email xác nhận
return {
    json: {
        to: "khachhang@example.com", // Địa chỉ email khách hàng
        subject: "Xác nhận lịch hẹn với " + $input.all().name,
        html: `
            <h2>Xác nhận lịch hẹn</h2>
            <p>Xin chào <strong>${$input.all().name}</strong>,</p>
            <p>Lịch hẹn của bạn đã được xác nhận:</p>
            <ul>
                <li>Ngày: <strong>${$input.all().date}</strong></li>
                <li>Thời gian: <strong>${$input.all().time}</strong></li>
                <li>Địa điểm: <strong>${$input.all().location}</strong></li>
            </ul>
            <p>Nếu cần hủy lịch, vui lòng liên hệ qua email.</p>
            <p>Trân trọng,</p>
            <p>Đội ngũ hỗ trợ</p>
        `
    }
};
```

#### **3. Kích hoạt ⚡️**
1. **Test run dữ liệu mẫu**:
   - Mở node **Webhook - Submit Form** và gửi một request POST với dữ liệu mẫu (ví dụ: `{"name": "John Doe", "date": "2024-05-20", "time": "10:00", "location": "Văn phòng"}`).
   - Kiểm tra workflow có chạy đúng không bằng cách theo dõi log trong n8n Editor.

2. **Bật Active workflow**:
   - Sau khi test thành công, nhấp vào **Active** để kích hoạt workflow.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Kết nối với Slack/Telegram**:
   - Thêm node **Slack** hoặc **Telegram** để thông báo khi có lịch mới được đặt.
   - Ví dụ: Gửi tin nhắn Slack với thông tin lịch mới cho team.

2. **Lưu log lịch**:
   - Thêm node **Google Sheets** hoặc **Airtable** để lưu lịch vào bảng dữ liệu.
   - Có thể sử dụng để báo cáo hoặc phân tích lịch sử đặt lịch.

3. **Gửi báo cáo định kỳ**:
   - Sử dụng node **Google Calendar** để lấy danh sách lịch trong tuần và gửi báo cáo email tự động cho các sếp.

4. **Tùy chỉnh form đặt lịch**:
   - Sử dụng node **Code** trong **Build HTML Form** để thêm trường tùy chỉnh (ví dụ: "Dự án", "Người liên hệ").

5. **Xử lý lỗi**:
   - Thêm node **Code** để xử lý lỗi (ví dụ: nếu lịch đã bị đặt trùng, hiển thị thông báo cho khách hàng).

---

### 📌 **Kết luận**
Workflow này giúp các sếp **tự động hóa hoàn toàn quá trình đặt lịch**, tiết kiệm thời gian và tăng trải nghiệm khách hàng. Bằng cách kết nối với **Google Calendar** và **Gmail**, workflow này hoạt động 24/7 mà không cần can thiệp thủ công.

**Hãy áp dụng ngay và tự động hóa lịch hẹn của doanh nghiệp!**
👉 [Tải workflow JSON](https://n8n.io/workflows/13923) và bắt đầu "lên đồ" ngay!

---
**Chú ý**: Nếu các sếp gặp khó khăn trong quá trình cấu hình, hãy liên hệ với cộng đồng n8n trên [Discord](https://n8n.io/community) để được hỗ trợ!