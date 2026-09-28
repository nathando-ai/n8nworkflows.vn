---
title: "🚀 Tự Động Hóa Xét Lựa CV & Đặt Lịch Hồi Phỏng Vấn Với Gmail, AI & Google Calendar (N8n)"
description: "Workflow này tự động hóa toàn bộ quy trình tuyển dụng: từ nhận CV qua Gmail, phân tích AI, lưu trữ Airtable, đặt lịch phỏng vấn và gửi thông báo tự động. Giúp tiết kiệm 80% thời gian của bộ phận HR và giảm thiểu sai sót con người."
slug: "tuyen-dung-ai-gmail-google-calendar"
tags: [n8n, automation, hr, ai-chatbot, google-calendar, openai, airtable, no-code]
keywords: [tự động hóa tuyển dụng n8n, phân tích cv bằng ai, đặt lịch phỏng vấn tự động, workflow hr no-code, ai chatbot tuyển dụng]
---

# 🚀 **Tự Động Hóa Xét Lựa CV & Đặt Lịch Phỏng Vấn Với Gmail, AI & Google Calendar**

### **Giải pháp AI hoàn toàn tự động hóa quy trình tuyển dụng**
Bạn đã bao giờ phải mất **3-5 tiếng/ngày** để xem xét hàng chục CV, liên hệ với ứng viên, và đặt lịch phỏng vấn? Hay phải lo lắng **sai sót trong quá trình đánh giá** do con người mệt mỏi? Workflow này sẽ **giải phóng bộ phận HR** khỏi công việc lặp lại, giúp bạn:
✅ **Phân tích CV bằng AI** trong giây lát (đánh giá phù hợp với vị trí, điểm mạnh/nhược điểm, kỹ năng)
✅ **Lưu trữ tất cả thông tin ứng viên** vào Airtable (dễ dàng theo dõi và báo cáo)
✅ **Đặt lịch phỏng vấn tự động** trên Google Calendar (không cần can thiệp thủ công)
✅ **Gửi email xác nhận cá nhân hóa** cho ứng viên và người phỏng vấn
✅ **Tiết kiệm 80% thời gian** so với cách làm thủ công

---
## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Từ 5 tiếng/ngày xuống còn **15-30 phút** để quản lý ứng viên.
- **Đánh giá khách quan**: AI phân tích CV theo tiêu chí **cố định** (không bị ảnh hưởng cảm xúc).
- **Lịch phỏng vấn tự động**: Không cần gọi điện để đặt lịch, giảm thiểu **trùng lịch** và **quên lịch**.
- **Dữ liệu tập trung**: Tất cả thông tin ứng viên được lưu vào **Airtable**, dễ dàng báo cáo và phân tích.
- **Trải nghiệm ứng viên tốt**: Email xác nhận **cá nhân hóa** tăng tỷ lệ tham gia phỏng vấn.
- **Hoạt động 24/7**: Workflow chạy liên tục, không phụ thuộc vào giờ làm việc của HR.
:::

---
## 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Gmail** (để nhận CV và gửi email xác nhận)
   - Cần **OAuth 2.0** cho n8n truy cập.
2. **Tài khoản Google Drive** (để lưu trữ CV tạm thời)
3. **Tài khoản Google Calendar** (để kiểm tra và đặt lịch phỏng vấn)
4. **Tài khoản Airtable** (để lưu trữ thông tin ứng viên)
   - **Base** và **Table** đã tạo sẵn (cần cấu hình tên cột phù hợp).
5. **Tài khoản OpenAI** (để sử dụng AI phân tích CV và đặt lịch)
   - **API Key** của OpenAI (mô hình `gpt-4.1-mini` được sử dụng).
6. **Danh sách vị trí tuyển dụng** (được lưu trong node `Available Positions1`)
   - Ví dụ: "DevOps Engineer", "Product Manager", "Data Analyst".
7. **Email mẫu** (để gửi xác nhận phỏng vấn)
   - Có thể sử dụng **template** trong node `Send a message1`.
:::

---
## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n.io/workflows/11657](https://n8n.io/workflows/11657) và import vào n8n Editor.
- **Cách 2**: Copy toàn bộ JSON từ link trên và **paste** vào n8n Editor (tab `Import`).
- **Cách 3**: Tạo mới workflow và **copy/paste** từng node theo danh sách dưới đây.

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflows này gồm **20 node**, nhưng có **5 node quan trọng** cần cấu hình kỹ lưỡng:

#### **A. Cấu hình Gmail (Nhận CV & Gửi Email)**
- **Node `Gmail Trigger1`**:
  - Chọn **credentials**: `gmailOAuth2` (đã cấu hình trước).
  - **Filter**: Cần thiết lập **rule** để chỉ nhận email có **đính kèm file PDF** (CV).
    - Ví dụ: `has:attachment` và `subject` chứa từ khóa như "CV", "Application", "Job Application".
- **Node `Get a message1`**:
  - Chọn **credentials**: `gmailOAuth2`.
  - **ID của email**: Sử dụng `$node["Gmail Trigger1"].json["$.id"]` (đường dẫn từ node trước).
- **Node `Send a message1`** (gửi email xác nhận):
  - **Credentials**: `gmailOAuth2`.
  - **Template email**: Sử dụng **HTML template** hoặc văn bản động (điền `$node["Structured Output Parser1"].json["interviewDetails"]` vào email).

#### **B. Cấu hình AI Phân Tích CV**
- **Node `Message a model2` & `Message a model3`**:
  - **Credentials**: OpenAI API Key (đã cấu hình trong n8n).
  - **Prompt**:
    - **Node `Message a model2`** (phân loại email là CV hay không):
      ```json
      "Analyze the email content and determine if it's a job application. Return 'true' if it is, otherwise 'false'."
      ```
    - **Node `Message a model3`** (phân tích CV):
      ```json
      "Analyze the resume text and compare it against the available positions: {{$node["Available Positions1"].json["positions"]}}. Return a structured JSON with:
      - best_fit_role: string
      - fit_score: number (1-10)
      - strengths: array
      - gaps: array
      - skills: array
      - experience: string"
      ```
  - **Model**: `gpt-4.1-mini` (đã cấu hình trong `keyParameters`).

#### **C. Cấu hình Airtable (Lưu Trữ Dữ Liệu)**
- **Node `Create a record2` & `Create a record3`**:
  - **Credentials**: Airtable OAuth (đã cấu hình).
  - **Base & Table**: Chọn **base** và **table** đã tạo sẵn.
  - **Fields**:
    - Cần **định nghĩa cột** trong Airtable phù hợp với dữ liệu từ AI:
      - `best_fit_role` (string)
      - `fit_score` (number)
      - `strengths` (text, format JSON)
      - `gaps` (text, format JSON)
      - `email` (string)
      - `name` (string, trích từ email)
      - `phone` (string, nếu có trong email)
      - `linkedin` (string, nếu có).

#### **D. Cấu hình Google Calendar (Đặt Lịch)**
- **Node `Get Next Business Day1`** (Code Node):
  - **Mã JavaScript**:
    ```javascript
    const today = new Date();
    const nextDay = new Date(today);
    nextDay.setDate(today.getDate() + 1);

    // Find next business day (Monday-Friday)
    while (nextDay.getDay() === 0 || nextDay.getDay() === 6) { // Sunday or Saturday
      nextDay.setDate(nextDay.getDate() + 1);
    }

    return { nextBusinessDay: nextDay.toISOString().split('T')[0] };
    ```
- **Node `Check Availability1`**:
  - **Credentials**: Google Calendar OAuth.
  - **Time Range**: Từ `9:00 AM` đến `6:00 PM` ngày tiếp theo.
  - **Duration**: `1 hour`.
- **Node `Create an event1`**:
  - **Credentials**: Google Calendar OAuth.
  - **Title**: `$node["Structured Output Parser1"].json["interviewDetails"].title`.
  - **Description**: `$node["Structured Output Parser1"].json["interviewDetails"].description`.
  - **Guests**: Email ứng viên và người phỏng vấn (trích từ Airtable).

#### **E. Cấu hình "Available Positions"**
- **Node `Available Positions1` (Set Node)**:
  - **Value**:
    ```json
    {
      "positions": [
        "DevOps Engineer",
        "Product Manager",
        "Data Analyst",
        "Frontend Developer"
      ]
    }
    ```
  - **Cần cập nhật** danh sách vị trí tuyển dụng theo thực tế của công ty.

---
### **3. Kích hoạt ⚡️**
1. **Test Run** với email mẫu:
   - Gửi **email có đính kèm CV PDF** đến địa chỉ Gmail đã cấu hình.
   - Kiểm tra **Airtable** xem dữ liệu có được lưu không.
   - Kiểm tra **Google Calendar** xem lịch có được đặt không.
2. **Bật Active**:
   - Chuyển trạng thái workflow từ `Inactive` sang `Active`.

---
## ✍️ **Mẹo & gợi ý nâng cao**
:::info[CẬP NHẬT & TỐT HÓA]
- **Cập nhật danh sách vị trí tuyển dụng**:
  - Khi có vị trí mới, chỉ cần **sửa node `Available Positions1`** mà không cần thay đổi workflow.
- **Lưu log hoạt động**:
  - Thêm **node `StickyNote`** để ghi lại lịch sử phỏng vấn (ví dụ: ngày, vị trí, ứng viên).
- **Gửi báo cáo định kỳ**:
  - Sử dụng **node `googleDrive`** để lưu **báo cáo tổng hợp** (từ Airtable) vào Google Drive.
- **Tích hợp Slack/Telegram**:
  - Thêm **node `slack`** hoặc `telegram` để thông báo khi có ứng viên mới phù hợp.
- **Tối ưu AI Prompt**:
  - Nếu AI phân tích không chính xác, **cập nhật prompt** trong node `Message a model3` để phù hợp với tiêu chí tuyển dụng của công ty.
- **Xử lý lỗi tự động**:
  - Thêm **node `Set`** sau `Create an event1` để lưu **status** của lịch (thành công/thất bại) vào Airtable.
:::

---
## 📌 **Kết luận**
Workflow này **giải phóng bộ phận HR** khỏi công việc lặp lại, giúp bạn:
✔ **Tiết kiệm thời gian** để tập trung vào việc **phỏng vấn và tuyển dụng chất lượng**.
✔ **Giảm thiểu sai sót** nhờ AI phân tích khách quan.
✔ **Tự động hóa toàn bộ quy trình** từ nhận CV đến đặt lịch phỏng vấn.

**Hành động ngay!**
1. **Cài đặt n8n Self-hosted** trên VPS để workflow chạy 24/7 (không phụ thuộc vào cloud miễn phí).
   👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
   👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
2. **Import workflow** và **cấu hình theo hướng dẫn**.
3. **Gửi email test** và **bật workflow** để tự động hóa tuyển dụng!

**Chia sẻ kết quả** của bạn sau khi áp dụng nhé! 🚀