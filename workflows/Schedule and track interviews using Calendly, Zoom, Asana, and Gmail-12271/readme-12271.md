---
title: "🚀 Tự Động Hóa Quá Trình Phỏng Vấn HR & Kỹ Thuật Với Calendly, Zoom, Asana & Gmail - Không Cần Code"
description: "Workflow này tự động hóa toàn bộ quy trình phỏng vấn từ đặt lịch đến thông báo, kết hợp Calendly, Zoom, Asana và Gmail để tiết kiệm thời gian cho các sếp HR và kỹ thuật, giảm thiểu lỗi lịch và tối ưu hóa quy trình phỏng vấn cho đội ngũ mở rộng."
slug: "tu-dong-hoa-qua-trinh-phong-van-calendly-zoom-asana-gmail"
tags: [n8n, automation, hr, zoom, asana, calendly, gmail, no-code, workflow]
keywords: [tự động hóa phỏng vấn, calendly n8n, zoom automation, asana task automation, gmail notification, workflow hr]
---

# 🚀 **Tự Động Hóa Quá Trình Phỏng Vấn HR & Kỹ Thuật Với Calendly, Zoom, Asana & Gmail**

### **Giải pháp cho các sếp HR và kỹ thuật:**
Hiện nay, việc quản lý lịch phỏng vấn thủ công không chỉ tốn thời gian mà còn dễ gây ra lỗi lịch, mất thông tin quan trọng và làm gián đoạn quy trình tuyển dụng. **Workflow này tự động hóa toàn bộ quy trình phỏng vấn**, từ khi ứng viên đặt lịch trên Calendly đến việc tạo phòng Zoom, lập nhiệm vụ trên Asana và gửi thông báo tự động đến các bên liên quan. **Không cần viết một dòng code nào!**

:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động 24/7 mà không gặp sự cố, các sếp nên **self-host n8n trên VPS** để đảm bảo tính riêng tư và ổn định.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian:** Không cần phải quản lý lịch phỏng vấn thủ công trên nhiều nền tảng.
- **Chính xác 100%:** Không có lỗi lịch hoặc mất thông tin do con người gây ra.
- **Tự động phân loại phỏng vấn:** Hệ thống tự nhận diện và phân loại phỏng vấn HR hoặc kỹ thuật.
- **Thông báo tự động:** Gửi email thông báo đến cả ban HR và người phỏng vấn ngay khi lịch được đặt.
- **Dữ liệu tập trung:** Tất cả thông tin phỏng vấn được lưu trên Asana với liên kết Zoom sẵn sàng.
- **Hoạt động liên tục:** Workflow chạy 24/7, không phụ thuộc vào giờ làm việc của nhân viên.
:::

---

## 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản và API Key:**
   - **Calendly:** Tài khoản Calendly và OAuth2 API Key (để nhận sự kiện đặt lịch).
   - **Zoom:** Tài khoản Zoom và OAuth2 API Key (để tạo phòng họp).
   - **Asana:** Tài khoản Asana và OAuth2 API Key (để tạo nhiệm vụ).
   - **Gmail:** Tài khoản Gmail và OAuth2 API Key (để gửi email thông báo).
2. **Thông tin cấu hình:**
   - **Danh sách email của các người phỏng vấn** (HR và kỹ thuật).
   - **ID dự án Asana** nơi lưu nhiệm vụ phỏng vấn.
   - **Từ khóa phân loại phỏng vấn** (ví dụ: "HR" hoặc "Technical" trong tiêu đề sự kiện Calendly).
   - **Mẫu nội dung email thông báo** (có thể chỉnh sửa trong node Gmail).

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Mở **n8n Workflow Editor**.
2. Nhấn **Import** và chọn file JSON (hoặc paste JSON từ link gốc: [Workflow Calendly-Zoom-Asana-Gmail](https://n8n.io/workflows/12271)).
3. Chọn **Create Workflow** để tạo workflow mới.

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này có **11 node** quan trọng, các sếp cần chú ý cấu hình như sau:

#### **🔹 Node "Receive interview booking" (Calendly Trigger)**
- **Chức năng:** Nhận sự kiện đặt lịch từ Calendly.
- **Cấu hình:**
  - Chọn **credentials** là `calendlyOAuth2Api`.
  - Chọn **Event Type** là `Event Created` (hoặc tương tự).
  - **Lưu ý:** Nếu Calendly không gửi sự kiện, kiểm tra lại OAuth2 Key và quyền API.

#### **🔹 Node "Prepare interview data" (Code)**
- **Chức năng:** Chuẩn bị dữ liệu phỏng vấn (tách loại phỏng vấn, thời gian, người phỏng vấn).
- **Cấu hình:**
  - Mở node **Code** và chỉnh sửa script để:
    - Trích xuất **loại phỏng vấn** từ tiêu đề sự kiện (ví dụ: nếu tiêu đề chứa "HR" → loại phỏng vấn là HR).
    - Lấy **thời gian và liên kết Zoom** từ sự kiện.
  - **Mẫu script cơ bản:**
    ```javascript
    // Trích xuất loại phỏng vấn
    const interviewType = $input.all()[0].event.title.includes("HR") ? "HR" : "Technical";

    // Lấy thời gian và người phỏng vấn
    const startTime = $input.all()[0].event.start_time;
    const interviewerEmail = $input.all()[0].event.attendee_email; // Nếu có

    return {
      json: {
        interviewType,
        startTime,
        interviewerEmail,
        // Thêm dữ liệu khác từ Calendly
        ...$input.all()[0].event
      }
    };
    ```

#### **🔹 Node "Route by interview type" (If)**
- **Chức năng:** Phân loại phỏng vấn HR và kỹ thuật.
- **Cấu hình:**
  - Thêm **2 nhánh** (branch) dựa trên `interviewType`:
    - **Nếu `interviewType === "HR"`** → Chạy nhánh tạo nhiệm vụ HR trên Asana.
    - **Nếu `interviewType === "Technical"`** → Chạy nhánh tạo nhiệm vụ kỹ thuật trên Asana.

#### **🔹 Node "Create HR Interview Task" & "Create Technical Interview Task" (Asana)**
- **Chức năng:** Tạo nhiệm vụ phỏng vấn trên Asana với thông tin chi tiết.
- **Cấu hình:**
  - Chọn **credentials** là `asanaOAuth2Api`.
  - Điền **Project ID** (tìm trên Asana: `Settings > Workspace > Project ID`).
  - **Mẫu nội dung nhiệm vụ:**
    ```
    TITLE: Phỏng vấn [HR/Kỹ thuật] - {Candidate Name}
    DESCRIPTION:
    - Thời gian: {Start Time}
    - Liên kết Zoom: {Zoom Meeting URL}
    - Người phỏng vấn: {Interviewer Email}
    - Ghi chú: {Additional Notes}
    ```
  - **Lưu ý:** Sử dụng **Dynamic Content** để trích xuất dữ liệu từ node `Prepare interview data`.

#### **🔹 Node "Create Zoom meeting" (Zoom)**
- **Chức năng:** Tạo phòng Zoom tự động.
- **Cấu hình:**
  - Chọn **credentials** là `zoomOAuth2Api`.
  - **Tham số cần điền:**
    - **Topic:** `{Candidate Name} - Phỏng vấn {HR/Kỹ thuật}`
    - **Start Time:** `{Start Time}` (định dạng `YYYY-MM-DDTHH:MM:SSZ`).
    - **Duration:** 60 (phút).
    - **Settings:** Bật **Join Before Host**, **Enable Waiting Room** (tùy chọn).
  - **Lưu ý:** Sau khi tạo, Zoom sẽ trả về **liên kết tham gia** (`join_url`), cần lưu vào Asana.

#### **🔹 Node "Notify HR team" & "Notify interviewer" (Gmail)**
- **Chức năng:** Gửi email thông báo đến ban HR và người phỏng vấn.
- **Cấu hình:**
  - Chọn **credentials** là `gmailOAuth2`.
  - **Mẫu email:**
    ```
    SUBJECT: Thông báo lịch phỏng vấn - {Candidate Name}
    BODY:
    Xin chào {Recipient Name},

    Lịch phỏng vấn đã được đặt thành công:
    - Loại phỏng vấn: {HR/Kỹ thuật}
    - Thời gian: {Start Time}
    - Liên kết Zoom: {Zoom Meeting URL}
    - Người phỏng vấn: {Interviewer Email}

    Xin vui lòng chuẩn bị trước nội dung phỏng vấn.

    Trân trọng,
    Đội ngũ HR
    ```
  - **Lưu ý:**
    - Đối với **Notify HR team**, gửi đến email nhóm (ví dụ: `hr-team@example.com`).
    - Đối với **Notify interviewer**, sử dụng `interviewerEmail` từ node `Prepare interview data`.

#### **🔹 Node "Error Handler Trigger" & "Error Email Notification" (Gmail)**
- **Chức năng:** Báo lỗi nếu workflow gặp sự cố.
- **Cấu hình:**
  - Node **Error Trigger** sẽ bắt tất cả lỗi và chuyển sang node **Error Email Notification**.
  - **Email báo lỗi** nên gửi đến email hỗ trợ (ví dụ: `support@example.com`) với nội dung:
    ```
    TÊN WORKFLOW: Tự động hóa phỏng vấn
    LỖI: {Error Message}
    THỜI GIAN: {Timestamp}
    DỮ LIỆU: {Input Data}
    ```

---

### **3. Kích hoạt ⚡️**
1. **Test Run:** Chạy workflow với **dữ liệu mẫu** từ Calendly (ví dụ: tạo một sự kiện test trên Calendly).
2. **Kiểm tra:**
   - Nhiệm vụ đã được tạo trên Asana chưa?
   - Phòng Zoom đã được tạo và có liên kết chưa?
   - Email thông báo đã được gửi đến HR và người phỏng vấn chưa?
3. **Bật Active:** Nếu test thành công, chuyển workflow sang **Active**.

---

## ✍️ **Mẹo & gợi ý nâng cao**
1. **Thêm Slack/Telegram Notifications:**
   - Sử dụng node **Slack** hoặc **Telegram Bot** để gửi thông báo nhanh chóng khi lịch được đặt.
   - **Cách làm:**
     - Import node **Slack** hoặc **Telegram** vào workflow.
     - Thêm node sau **Notify HR team** và **Notify interviewer** để gửi tin nhắn Slack/Telegram cùng nội dung.

2. **Lưu Log Dữ liệu:**
   - Sử dụng node **StickyNote** hoặc **Database** (ví dụ: **Google Sheets**) để lưu lịch sử phỏng vấn.
   - **Cách làm:**
     - Thêm node **Google Sheets** sau node **Prepare interview data**.
     - Lưu dữ liệu vào sheet với cột: `Candidate Name`, `Interview Type`, `Start Time`, `Zoom Link`, `Status`.

3. **Gửi Báo cáo Định Kỳ:**
   - Sử dụng **n8n Scheduler** để gửi báo cáo tổng hợp phỏng vấn hàng tuần.
   - **Cách làm:**
     - Tạo một workflow mới với **Trigger: Schedule**.
     - Sử dụng node **Google Sheets** hoặc **Gmail** để tổng hợp và gửi báo cáo.

4. **Tích Hợp với CRM (Salesforce, HubSpot):**
   - Nếu công ty sử dụng CRM, có thể tích hợp để cập nhật thông tin ứng viên sau phỏng vấn.
   - **Cách làm:**
     - Import node **Salesforce** hoặc **HubSpot**.
     - Sau khi phỏng vấn kết thúc, cập nhật trạng thái ứng viên trên CRM.

---

## 📌 **Kết luận**
Workflow này **giải phóng thời gian cho các sếp HR và kỹ thuật**, loại bỏ việc quản lý lịch phỏng vấn thủ công và giảm thiểu lỗi. **Với chỉ một lần cấu hình, workflow sẽ tự động hóa toàn bộ quy trình**, từ đặt lịch đến thông báo và lưu trữ dữ liệu.

**Hành động ngay hôm nay:**
1. **Import workflow** và cấu hình theo hướng dẫn trên.
2. **Test với dữ liệu mẫu** trước khi chuyển sang chế độ hoạt động thực tế.
3. **Tích hợp thêm Slack/Telegram** để nhận thông báo nhanh chóng.

**🚀 Khởi động tự động hóa phỏng vấn của công ty bạn ngay bây giờ!** Nếu có bất kỳ vấn đề nào, hãy để lại comment bên dưới hoặc liên hệ với cộng đồng n8n để hỗ trợ.