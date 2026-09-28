---
title: "🚀 Tự Động Đặt Lịch Hẹn Giọng Nói Với VAPI & Cal.com (Không Code)"
description: "Hướng dẫn chi tiết cách tích hợp VAPI AI Voice Agent với Cal.com trên n8n để cho phép khách hàng đặt lịch hoặc kiểm tra lịch trống hoàn toàn bằng giọng nói, tự động hóa 100% quy trình."
slug: "tu-dong-dat-lich-hen-giong-noi-vapi-calcom"
tags: [n8n, vapi, cal.com, ai-voice-agent, appointment-scheduling]
keywords: [n8n workflow, vapi ai, cal.com api, tự động hóa đặt lịch, voice bot n8n]
---

# 🚀 Tự Động Đặt Lịch Hẹn Giọng Nói Với VAPI & Cal.com (Không Code)

Bạn có bao giờ cảm thấy phiền phức khi phải mở điện thoại, tìm ứng dụng đặt lịch, điền form, chọn ngày giờ và chờ xác nhận? Hoặc nếu bạn là chủ doanh nghiệp, việc đội ngũ hỗ trợ phải nghe điện thoại và nhập liệu thủ công vào hệ thống quản lý lịch (như Cal.com) gây ra bao nhiêu sai sót và lãng phí thời gian?

Workflow **Book Appointments with Voice Using VAPI & Cal.com** chính là giải pháp "vàng" cho bài toán này. Bằng cách kết hợp sức mạnh của **VAPI** (trợ lý giọng nói AI) và **Cal.com** (nền tảng đặt lịch chuyên nghiệp) thông qua **n8n**, các sếp có thể tạo ra một trợ lý ảo có khả năng nghe hiểu yêu cầu của khách hàng, kiểm tra lịch trống theo thời gian thực và xác nhận đặt lịch ngay lập tức – tất cả chỉ bằng một cuộc gọi hoặc tin nhắn thoại. Không cần code, không cần chờ đợi, trải nghiệm liền mạch và chuyên nghiệp.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, đặc biệt với các tác vụ liên quan đến API và Webhook, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100% quy trình đặt lịch:** Khách hàng chỉ cần nói, hệ thống tự động xử lý từ nhận diện ý định đến xác nhận lịch.
- **Giảm tải cho đội ngũ CSKH:** Loại bỏ hoàn toàn các cuộc gọi lặp đi lặp lại về việc "có lịch trống không?" hay "đặt lịch giúp tôi".
- **Trải nghiệm khách hàng hiện đại:** Sử dụng công nghệ AI Voice Agent tạo ấn tượng công nghệ cao, chuyên nghiệp.
- **Độ chính xác cao:** Loại bỏ lỗi nhập liệu thủ công, đảm bảo thông tin ngày giờ được chuyển đổi đúng định dạng API Cal.com.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản n8n:** Có quyền tạo và kích hoạt workflow.
2. **Tài khoản VAPI:** Tạo một Voice Agent (Bot giọng nói) và lấy **Webhook URL** hoặc cấu hình để gửi dữ liệu về n8n.
3. **Tài khoản Cal.com:**
   - Tạo một Event Type (ví dụ: "Họp tư vấn", "Cuộc gọi 15 phút").
   - Lấy **API Key** của Cal.com (thường nằm trong Settings > API Keys).
   - Ghi nhớ **Event Type ID** hoặc **Slug** của sự kiện.
4. **Credentials trong n8n:** Tạo một credential loại `Header Auth` chứa API Key của Cal.com.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể import workflow này từ file JSON hoặc copy toàn bộ cấu trúc node vào n8n Editor.
- **Cách 1:** Tải file JSON từ link gốc [n8n.io/workflows/6895](https://n8n.io/workflows/6895) và chọn *Import from File*.
- **Cách 2:** Copy cấu trúc node và dán vào canvas n8n.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này sử dụng 9 nodes chính. Dưới đây là các điểm cần cấu hình kỹ:

**1. Node `Webhook` (Điểm vào)**
- Đây là nơi VAPI gửi dữ liệu về.
- **Path:** Giữ nguyên hoặc đổi path tùy ý, nhưng phải khớp với cấu hình trong VAPI.
- **Method:** POST.
- **Lưu ý:** Trong VAPI, các sếp cần cấu hình Agent để khi nhận được ý định (intent) là `book` hoặc `check`, nó sẽ gọi Webhook này với payload chứa các entity như `date`, `time`, `action`.

**2. Node `Switch` (Phân luồng)**
- Node này kiểm tra trường `action` trong payload từ VAPI.
- **Rule 1:** Nếu `action` = "check" -> Đi sang luồng kiểm tra lịch.
- **Rule 2:** Nếu `action` = "book" -> Đi sang luồng đặt lịch.
- *Mẹo:* Đảm bảo giá trị string khớp chính xác với những gì VAPI trả về (thường là lowercase).

**3. Node `Set Variables` & `Extract Start & End Time`**
- Các node `Set` này có nhiệm vụ làm sạch và định dạng dữ liệu thô từ giọng nói.
- **Quan trọng:** VAPI thường trả về ngày giờ dưới dạng text (ví dụ: "Tuesday 3 PM"). Các node này sẽ parse và chuyển đổi thành định dạng ISO 8601 hoặc timestamp mà Cal.com API yêu cầu.
- Các sếp cần kiểm tra logic trong node `Extract Start & End Time` để đảm bảo nó xử lý đúng múi giờ (Timezone) của doanh nghiệp.

**4. Node `Check Availability` (HTTP Request)**
- **Method:** GET
- **URL:** `https://api.cal.com/v1/bookings/availability` (hoặc endpoint tương ứng của Cal.com).
- **Query Parameters:** Cần điền các tham số như `event_type_id`, `start`, `end`.
- **Credentials:** Chọn credential `Header Auth` đã tạo chứa API Key của Cal.com.
- **Headers:** Đảm bảo có header `Authorization: Bearer [YOUR_API_KEY]` (hoặc theo chuẩn Cal.com yêu cầu).

**5. Node `Book Appointment` (HTTP Request)**
- **Method:** POST
- **URL:** `https://api.cal.com/v1/bookings`
- **Body:** JSON chứa thông tin khách hàng (name, email) và thời gian đã được parse từ trước đó.
- **Credentials:** Dùng chung credential `Header Auth` của Cal.com.

**6. Nodes `Respond To Webhook`**
- **`Check Availability successful`:** Trả về danh sách các slot trống về cho VAPI. VAPI sẽ đọc to cho khách hàng nghe (ví dụ: "Có lịch trống lúc 3 giờ chiều và 4 giờ chiều").
- **`Booking SuccessFul`:** Trả về thông báo xác nhận đặt lịch thành công. VAPI sẽ đọc: "Lịch hẹn của bạn đã được xác nhận lúc 3 giờ chiều thứ Ba".

#### 3. Kích hoạt ⚡️
1. **Test Run:**
   - Sử dụng tính năng *Test* trong n8n hoặc gửi một payload mẫu từ Postman/Insomnia đến Webhook URL.
   - Payload mẫu cho kiểm tra lịch:
     ```json
     {
       "action": "check",
       "date": "2023-10-25",
       "time": "15:00"
     }
     ```
   - Payload mẫu cho đặt lịch:
     ```json
     {
       "action": "book",
       "date": "2023-10-25",
       "time": "15:00",
       "customer_name": "John Doe",
       "customer_email": "john@example.com"
     }
     ```
2. **Cấu hình VAPI:**
   - Trong dashboard VAPI, chỉ định Webhook URL của n8n cho các intent `check_availability` và `book_appointment`.
   - Cấu hình prompt cho VAPI để nó biết cách trích xuất ngày giờ từ giọng nói của người dùng và gửi về n8n.
3. **Bật Active:**
   - Sau khi test thành công, bật nút **Active** trên workflow n8n.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp CRM:** Sau khi đặt lịch thành công, thêm một node HTTP Request hoặc node CRM (HubSpot, Salesforce) để tạo lead mới hoặc cập nhật trạng thái khách hàng.
- **Gửi Email/Xác nhận:** Thêm node `Send Email` (Gmail/SMTP) để gửi email xác nhận lịch hẹn chi tiết kèm link hủy lịch cho khách hàng ngay sau khi VAPI đọc xong.
- **Lưu Log vào Google Sheets:** Thêm node `Google Sheets` để ghi lại lịch sử các cuộc gọi, thời gian đặt lịch và kết quả (thành công/thất bại) để dễ dàng theo dõi và phân tích.
- **Xử lý ngoại lệ:** Thêm một nhánh `Error` hoặc `Default` trong node `Switch` để xử lý các trường hợp khách hàng nói không rõ hoặc yêu cầu ngoài phạm vi (ví dụ: hỏi giá cả), trả về thông báo lịch sự từ VAPI.

### 📌 Kết luận
Việc tích hợp **VAPI** và **Cal.com** thông qua **n8n** không chỉ là một tính năng "cool" mà là một công cụ thực chiến giúp doanh nghiệp nâng cao trải nghiệm khách hàng và tối ưu hóa vận hành. Với workflow này, các sếp có thể biến mọi cuộc gọi vào thành một lịch hẹn tiềm năng, tự động và chính xác. Hãy bắt đầu triển khai ngay hôm nay để không bỏ lỡ cơ hội nâng tầm dịch vụ của mình!