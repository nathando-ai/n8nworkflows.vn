---
title: "📅 Tự Động Hẹn Lịch Phỏng Vấn Với Xác Nhận Thủ Công - Google Calendar + Gmail (N8n)"
description: "Workflow tự động hóa hoàn toàn không cần code giúp các sếp nhận và xử lý yêu cầu hẹn lịch phỏng vấn, kiểm tra sẵn sàng trên Google Calendar, yêu cầu xác nhận từ HR, và gửi thông báo tự động. Giảm thiểu thời gian thủ công lên đến 80% và tránh lỗi lịch trùng lặp."
slug: "tu-dong-hoan-lich-phong-van-google-calendar-gmail"
tags: [n8n, automation, google-calendar, gmail, hr-process, no-code, workflow-tieng-viet]
keywords: [tự động hóa hẹn lịch, google calendar api, gmail automation, workflow n8n, xác nhận thủ công, tự động hóa nhân sự]
---

# 🚀 **Tự Động Hẹn Lịch Phỏng Vấn Với Xác Nhận Thủ Công - Google Calendar + Gmail (N8n)**

## **💡 Giải quyết vấn đề gì?**
Các sếp HR hay quản lý nhân sự thường phải làm thủ công:
- **Nhận yêu cầu hẹn lịch** từ ứng viên qua email hoặc form.
- **Kiểm tra sẵn sàng** trên Google Calendar để tránh lịch trùng.
- **Yêu cầu xác nhận** từ đồng nghiệp hoặc HR trước khi đặt lịch.
- **Gửi thông báo** xác nhận hoặc từ chối cho ứng viên.

Workflow này **tự động hóa toàn bộ quy trình**, giảm thiểu thời gian thủ công, tránh lỗi lịch trùng, và đảm bảo quy trình phỏng vấn chuyên nghiệp.

---
### **🎯 Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Xử lý hàng trăm yêu cầu hẹn lịch chỉ trong vài giây.
- **Tránh lịch trùng**: Kiểm tra tự động sẵn sàng trên Google Calendar.
- **Xác nhận thủ công**: Yêu cầu đồng nghiệp/HR phê duyệt trước khi đặt lịch.
- **Thông báo tự động**: Gửi email xác nhận hoặc từ chối cho ứng viên.
- **Hoạt động 24/7**: Không cần can thiệp người dùng sau khi setup.
:::

---
## **🔧 Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi sử dụng workflow, các sếp cần:
✅ **Tài khoản Google** (để kết nối Google Calendar và Gmail).
✅ **API Key và OAuth2 Credentials**:
   - [Cấu hình Google Calendar API](https://developers.google.com/calendar/api/quickstart/python) (đăng ký dự án và tạo OAuth2 Client ID).
   - [Cấu hình Gmail API](https://developers.google.com/gmail/api/quickstart/python) (bật quyền API trong Google Cloud Console).
✅ **VPS Self-hosted n8n** (để workflow chạy 24/7):
   👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%).
   👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172).
:::

---
## **🚀 Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. Tải workflow từ [đây](https://n8n.io/workflows/12419) (nút "Export").
2. Trên n8n Editor, nhấn **"Import"** và chọn file JSON vừa tải.
3. Chọn **"Import"** để hoàn tất.

#### **Phương pháp 2: Copy/Paste JSON**
1. Copy toàn bộ mã JSON từ [đây](https://n8n.io/workflows/12419) (nút "Export").
2. Trên n8n Editor, nhấn **"Import"** → **"Paste JSON"** và dán mã.
3. Chọn **"Import"** để hoàn tất.

---
### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này bao gồm **10 node** chính, mỗi node đều cần cấu hình kỹ lưỡng. Dưới đây là hướng dẫn chi tiết:

#### **🔹 Node 1: Receive appointment request (Webhook)**
- **Cấu hình**:
  - **Path**: `appointment-request` (không thay đổi).
  - **HTTP Method**: `POST` (không thay đổi).
  - **Credentials**: Không cần (webhook mặc định).
- **Lưu ý**:
  - Sau khi import, **không cần thay đổi** cấu hình này.
  - Để test, các sếp có thể gửi yêu cầu từ **Postman** hoặc **cURL**:
    ```bash
    curl -X POST https://[Tên-Domain-N8N]/webhook/appointment-request \
    -H "Content-Type: application/json" \
    -d '{"name":"John Doe","email":"john@example.com","timezone":"Asia/Ho Chi Minh","preferredTime":"2024-06-15T10:00:00"}'
    ```

#### **🔹 Node 2: Format appointment data (Set)**
- **Cấu hình**:
  - **Format JSON** để chuẩn hóa dữ liệu đầu vào (không cần thay đổi).
  - Ví dụ: Chuyển đổi `preferredTime` thành format `YYYY-MM-DDTHH:MM:SS`.

#### **🔹 Node 3: Check Availability (Google Calendar)**
- **Cấu hình**:
  - **Credentials**: Chọn `googleCalendarOAuth2Api` (đã cấu hình trước).
  - **Resource**: `calendar` (không thay đổi).
  - **Timezone**: **CẦN THAY ĐỔI** thành múi giờ của công ty (ví dụ: `Asia/Ho Chi Minh`).
- **Lưu ý**:
  - Nếu không chọn múi giờ chính xác, workflow sẽ trả về kết quả sai.

#### **🔹 Node 4: Is approved? (If)**
- **Cấu hình**:
  - **Condition**: Kiểm tra nếu `isApproved` = `true` (mặc định).
  - **Lưu ý**: Node này sẽ **chuyển hướng** sang node **"Book Appointment"** nếu `isApproved` = `true`, ngược lại sẽ chuyển sang **"Appointment Failed"**.

#### **🔹 Node 5: Appointment Failed (Gmail)**
- **Cấu hình**:
  - **Credentials**: Chọn `gmailOAuth2` (đã cấu hình trước).
  - **Template Email**: Cần **cập nhật nội dung email** để thông báo cho ứng viên:
    ```html
    <p>Xin lỗi, lịch hẹn của bạn không thể được đặt do lịch trùng hoặc chưa được phê duyệt.</p>
    <p>Nếu có thắc mắc, vui lòng liên hệ qua email: support@example.com</p>
    ```
  - **To**: Điền `{{$json.email}}` (để tự động lấy email từ yêu cầu).

#### **🔹 Node 6: Book Appointment (Google Calendar)**
- **Cấu hình**:
  - **Credentials**: Chọn `googleCalendarOAuth2Api`.
  - **Event Details**: Cần điền thông tin chi tiết:
    - **Summary**: `Phỏng vấn với {{$json.name}}`.
    - **Start Time**: `{{$json.preferredTime}}`.
    - **End Time**: `{{$json.preferredTime}} + 30 minutes` (hoặc tùy chỉnh).
    - **Description**: `Lịch hẹn tự động từ hệ thống HR`.

#### **🔹 Node 7: Respond to Webhook (RespondToWebhook)**
- **Cấu hình**:
  - **Response**: Trả về kết quả ngay lập tức cho yêu cầu webhook:
    ```json
    {
      "status": "{{$node["Check Availability"].json["status"]}}",
      "message": "{{$node["Check Availability"].json["message"]}}"
    }
    ```
  - **Lưu ý**: Node này **không cần thay đổi** nếu muốn trả về kết quả tức thời.

#### **🔹 Node 8: Is Slot Available? (If)**
- **Cấu hình**:
  - **Condition**: Kiểm tra nếu `isAvailable` = `true` (trả về từ node **"Check Availability"**).
  - **Lưu ý**: Nếu `isAvailable` = `false`, workflow sẽ chuyển sang **"End - Slot Busy"**.

#### **🔹 Node 9: Get Approval (HR) [1 hour wait] (Gmail)**
- **Cấu hình**:
  - **Credentials**: Chọn `gmailOAuth2`.
  - **Template Email**: Cần **cập nhật nội dung email** để yêu cầu phê duyệt:
    ```html
    <p>Xin vui lòng phê duyệt lịch hẹn với ứng viên {{$json.name}}:</p>
    <p>Thời gian: {{$json.preferredTime}}</p>
    <p>Liên kết phê duyệt: [Liên kết n8n Webhook](https://[Tên-Domain-N8N]/webhook/approval)</p>
    ```
  - **Operation**: `sendAndWait` (đợi phản hồi trong **1 giờ**).
  - **Lưu ý**:
    - Sau khi gửi email, workflow sẽ **đợi 1 giờ** để HR trả lời.
    - Nếu HR không phản hồi, workflow sẽ tự động chuyển sang **"Appointment Failed"**.

#### **🔹 Node 10: End - Slot Busy (NoOp)**
- **Cấu hình**:
  - **Lưu ý**: Node này **không cần cấu hình**, chỉ dùng để kết thúc workflow nếu lịch đã bận.

---
### **3. Kích hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Gửi yêu cầu từ Postman (như hướng dẫn ở trên).
   - Kiểm tra email và Google Calendar để xác nhận.
2. **Bật Active workflow**:
   - Trên n8n Editor, nhấn **"Active"** ở góc trên bên phải.

---
## **✍️ Mẹo & gợi ý nâng cao**
:::info[CẢI TIẾN TRONG QUY TRÌNH]
- **Kết hợp với Slack/Telegram**:
  - Thêm node **Slack** hoặc **Telegram** để thông báo ngay khi có yêu cầu mới.
- **Lưu log hoạt động**:
  - Sử dụng node **Google Sheets** hoặc **Airtable** để ghi lại tất cả lịch hẹn và trạng thái.
- **Gửi báo cáo định kỳ**:
  - Tạo một workflow riêng để tổng hợp và gửi báo cáo số lượng lịch hẹn, tỷ lệ phê duyệt.
- **Cập nhật múi giờ tự động**:
  - Sử dụng node **Set** để lấy múi giờ từ `user.timezone` trong yêu cầu.
:::

---
## **📌 Kết luận**
Workflow này **giải phóng thời gian** cho các sếp HR khỏi việc xử lý thủ công hàng trăm yêu cầu hẹn lịch. Với **xác nhận thủ công**, quy trình trở nên chuyên nghiệp và an toàn, đồng thời **tránh lịch trùng** nhờ kiểm tra tự động trên Google Calendar.

**🚀 Hãy setup ngay và tự động hóa quy trình phỏng vấn của công ty!**
Nếu có vấn đề, hãy để lại comment bên dưới hoặc liên hệ với cộng đồng n8n tại [Discord](https://discord.gg/n8n).

---
**🔗 Tài liệu tham khảo:**
- [Cấu hình Google Calendar API](https://developers.google.com/calendar/api/quickstart/python)
- [Cấu hình Gmail API](https://developers.google.com/gmail/api/quickstart/python)
- [Hướng dẫn Webhook trong n8n](https://docs.n8n.io/integrations/builtins/webhook/)