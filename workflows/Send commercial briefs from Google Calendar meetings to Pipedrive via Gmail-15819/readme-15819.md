---
title: "🚀 Tự Động Gửi Tóm Tắt Thương Mại Từ Cuộc Hẹn Google Calendar Sang Pipedrive Vía Email - Giảm 90% Công Việc Lặp Lại"
description: "Workflow tự động hóa hoàn toàn không cần code giúp các sếp lấy thông tin cuộc họp từ Google Calendar, tìm kiếm lead tương ứng trên Pipedrive, gửi tóm tắt thương mại qua email Gmail và cập nhật trạng thái lead tự động. Giúp tiết kiệm 5-10 giờ/tuần cho bộ phận bán hàng."
slug: "tu-dong-gui-tom-tat-thuong-mai-tu-google-calendar-sang-pipedrive"
tags: [n8n, automation, lead-nurturing, pipedrive, gmail, google-calendar, no-code]
keywords: [tự động hóa pipedrive, gửi email từ google calendar, workflow n8n lead nurturing, tự động hóa bán hàng, giảm công việc lặp lại]
---

# 🚀 **Tự Động Gửi Tóm Tắt Thương Mại Từ Cuộc Hẹn Google Calendar Sang Pipedrive Vía Email**

## **🔥 Nỗi Đau Của Các Sếp Bán Hàng**
Hàng ngày, các sếp phải:
- **Lặp đi lặp lại** ghi chép tóm tắt cuộc họp từ Google Calendar vào Pipedrive.
- **Quên gửi email tóm tắt** cho khách hàng sau cuộc họp, dẫn đến mất cơ hội chuyển đổi.
- **Tốn thời gian** tra cứu lead trong Pipedrive để cập nhật trạng thái sau khi gửi email.
- **Rủi ro nhân sự** khi nhân viên nghỉ ốm hoặc thay đổi, làm mất dữ liệu quan trọng.

**Workflow này giải quyết tất cả!** Nó tự động:
✅ **Lấy cuộc họp** từ Google Calendar.
✅ **Tìm lead tương ứng** trên Pipedrive.
✅ **Gửi email tóm tắt** qua Gmail.
✅ **Cập nhật trạng thái lead** trong Pipedrive.
✅ **Chạy 24/7** mà không cần can thiệp của con người.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 5-10 giờ/tuần** cho bộ phận bán hàng (tương đương 200 giờ/năm).
- **Tăng tỷ lệ chuyển đổi** do không quên gửi email tóm tắt sau cuộc họp.
- **Dữ liệu chính xác** vì tự động đồng bộ giữa Google Calendar và Pipedrive.
- **Hoạt động liên tục** ngay cả khi nhân viên nghỉ hoặc thay đổi.
- **GDPR-compliant** (phù hợp với luật bảo vệ dữ liệu châu Âu).
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
✔ **Tài khoản Google Calendar** (đã cấp quyền API).
✔ **Tài khoản Pipedrive** (API Key đã tạo).
✔ **Tài khoản Gmail** (đã cấp quyền OAuth2).
✔ **Danh sách lead** trong Pipedrive (để workflow tìm kiếm).
✔ **Mẫu email tóm tắt** (cần chỉnh sửa trong node Gmail).

---
### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/15819](https://n8n.io/workflows/15819).
- **Mở n8n Editor** → Nhấn **Import** → Chọn file JSON vừa tải.
- **Hoặc copy/paste** JSON từ file vào n8n Editor.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow gồm **10 node** quan trọng, các sếp cần chú ý:

##### **🔹 Node 1: Schedule Trigger (Lên lịch chạy)**
- **Thiết lập thời gian chạy**: Ví dụ, **mỗi 30 phút** (hoặc mỗi sáng 7h).
- **Lưu ý**: Chọn **Active** để workflow bắt đầu chạy.

##### **🔹 Node 2: Fetch Calendar Appointments (Lấy cuộc họp từ Google Calendar)**
- **Credentials**: Chọn `googleCalendarOAuth2Api` (đã cấu hình trước).
- **Key Parameters**:
  - `operation`: `getAll` (lấy tất cả cuộc họp).
  - **Lưu ý**: Nếu chỉ lấy cuộc họp trong ngày, cần thêm điều kiện lọc trong **Code Node** sau.

##### **🔹 Node 3: Parse Calendar Events (Xử lý dữ liệu cuộc họp)**
- **Mở node Code** → Chỉnh sửa mã JavaScript để:
  - **Trích xuất email của khách hàng** từ `attendees` trong cuộc họp.
  - **Định dạng dữ liệu** phù hợp với Pipedrive API.
  **Mẫu mã JavaScript tham khảo**:
  ```javascript
  return {
    data: {
      email: event.attendees[0].email, // Giả sử khách hàng là người tham gia đầu tiên
      subject: event.summary,
      startTime: event.start.dateTime,
      endTime: event.end.dateTime
    }
  };
  ```

##### **🔹 Node 4 & 5: Fetch Lead & Person from Pipedrive (Tìm lead và khách hàng)**
- **Credentials**: Chọn `pipedriveApi` (đã cấu hình trước).
- **Key Parameters**:
  - `operation`: `search` (tìm kiếm lead/person).
  - **Lưu ý**:
    - **Node Fetch Lead**: Tìm kiếm bằng `email` từ cuộc họp.
    - **Node Fetch Person**: Tìm kiếm bằng `email` hoặc `phone` của khách hàng.

##### **🔹 Node 6 & 7: Filter Lead Exists & Filter Note Exists (Lọc lead hợp lệ)**
- **Node Filter Lead Exists**:
  - **Condition**: `$.json.data.id !== null` (loại bỏ lead không tồn tại).
- **Node Filter Note Exists**:
  - **Condition**: `$.json.data.notes.length === 0` (loại bỏ lead đã có ghi chú).

##### **🔹 Node 8: Send Commercial Brief Email (Gửi email tóm tắt)**
- **Credentials**: Chọn `gmailOAuth2` (đã cấu hình trước).
- **Tham số cần chỉnh**:
  - **Subject**: `"Tóm tắt cuộc họp với [Tên Khách Hàng]"`.
  - **Body**: Nội dung email tóm tắt (có thể sử dụng **LLM** như n8n-nodes-base.llm để tự động tạo).
  - **Recipient**: `$.json.data.email` (email từ cuộc họp).
  - **Lưu ý**: Nếu muốn thêm **đính kèm file**, sử dụng node `n8n-nodes-base.googleDrive` để lấy file từ Google Drive.

##### **🔹 Node 9: Update Lead Label in Pipedrive (Cập nhật trạng thái lead)**
- **Credentials**: `pipedriveApi`.
- **Key Parameters**:
  - `operation`: `update`.
  - **Field**: `labels` (cập nhật nhãn "Đã gửi tóm tắt").
  - **Mẫu JSON**:
    ```json
    {
      "labels": ["Brief Sent"]
    }
    ```

#### **3. Kích Hoạt ⚡️**
- **Test Run**:
  - Nhấn **Run Workflow** với dữ liệu mẫu (ví dụ: một cuộc họp giả).
  - Kiểm tra **email đã gửi** và **trạng thái lead** trong Pipedrive.
- **Bật Active**:
  - Sau khi test thành công, chuyển **Active** sang `true`.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tự động tạo email tóm tắt bằng AI**:
   - Thêm node **LLM** (n8n-nodes-base.llm) để tự động tổng hợp nội dung từ cuộc họp.
   - **Prompt tham khảo**:
     ```
     Tóm tắt cuộc họp giữa [Tên Doanh Nghiệp] và [Tên Khách Hàng] vào ngày [Ngày].
     Nội dung chính: [Nội dung từ cuộc họp].
     Yêu cầu: Trích xuất 3 điểm quan trọng và đề xuất hành động tiếp theo.
     ```

2. **Gửi báo cáo định kỳ cho quản lý**:
   - Thêm node **Slack/Telegram** để báo cáo số lượng lead đã gửi email.
   - **Mẫu thông báo**:
     ```
     📊 **Báo cáo tự động hóa bán hàng**
     - Ngày: [Ngày]
     - Số lead đã gửi email: [Số lượng]
     - Tỷ lệ thành công: [Tỷ lệ %]
     ```

3. **Lưu log hoạt động**:
   - Thêm node **Google Sheets** hoặc **Notion** để ghi lại lịch sử hoạt động.
   - **Cột cần lưu**: Ngày, Email khách hàng, Trạng thái, Nội dung email.

4. **Kết hợp với CRM khác**:
   - Thay thế Pipedrive bằng **HubSpot** hoặc **Salesforce** bằng cách thay đổi node `pipedrive` thành `hubspot` hoặc `salesforce`.

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp bán hàng, giúp họ tập trung vào **quan hệ khách hàng** thay vì công việc lặp lại. Với **n8n**, không cần code, không cần kỹ sư IT, các sếp có thể tự xây dựng và chạy tự động hóa **24/7**.

**🚀 Hành động ngay!**
1. **Import workflow** từ [n8n.io/workflows/15819](https://n8n.io/workflows/15819).
2. **Cấu hình credentials** (Google Calendar, Pipedrive, Gmail).
3. **Chỉnh sửa email tóm tắt** phù hợp với doanh nghiệp.
4. **Bật Active** và **xem kết quả** trong vài phút!

**💡 Cần hỗ trợ thêm?**
- Liên hệ **Allan Vaccarizi** (n8n automation expert) qua:
  - [LinkedIn](https://www.linkedin.com/in/allanvaccarizi/)
  - [Growth-AI.fr](https://www.growth-ai.fr/)

**🎁 Bonus**: Các sếp có thể **mở rộng workflow** này để tự động:
- Gửi **follow-up email** sau 3 ngày.
- **Tạo deal** trong Pipedrive từ cuộc họp.
- **Gửi báo cáo hàng tháng** cho CEO.

**Hãy tự động hóa ngay hôm nay!** 🚀