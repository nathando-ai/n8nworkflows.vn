---
title: "🤖 **Tự Động Hóa Xét Lựa CV & Đặt Lịch Hồi Phỏng Vấn Với Gmail, AI & Airtable** – Giảm 90% Thời Gian HR"
description: "Workflow tự động hóa hoàn toàn quá trình nhận CV, đánh giá AI, lựa chọn ứng viên phù hợp và đặt lịch phỏng vấn tự động. Giúp HR tiết kiệm 10+ giờ/tuần, giảm sai sót và tăng hiệu quả tuyển dụng."
slug: "tuyen-dung-tu-dong-hoa-gmail-ai-airtable"
tags: [n8n, automation, hr, ai-chatbot, openai, airtable, google-workspace]
keywords: [tự động hóa tuyển dụng, xét lựa cv bằng ai, đặt lịch phỏng vấn tự động, n8n workflow hr, ai resume screening]
---

# 🚀 **Tự Động Hóa Xét Lựa CV & Đặt Lịch Hồi Phỏng Vấn Với Gmail, AI & Airtable**

### **Giải pháp cho HR: Từ "Đọc CV" đến "Đặt Lịch" chỉ trong vài giây**
Hiện nay, quá trình tuyển dụng tại các doanh nghiệp thường gặp phải **3 vấn đề lớn**:
1. **Tốn thời gian**: HR phải đọc hàng chục CV mỗi ngày, mất trung bình **10-15 phút/ứng viên**.
2. **Sai sót con người**: Đánh giá chủ quan, bỏ qua ứng viên tiềm năng hoặc nhầm lẫn thông tin.
3. **Khó quản lý**: Dữ liệu ứng viên phân tán trên email, Google Drive, và các bảng tính khác.

**Workflow này giải quyết tất cả!** Nó tự động:
✅ **Nhận CV** từ email (kèm file đính kèm).
✅ **Xét lựa CV** bằng AI (GPT-4) so sánh với các vị trí tuyển dụng.
✅ **Đặt lịch phỏng vấn** trên Google Calendar (nếu ứng viên đạt điểm ≥ 8/10).
✅ **Gửi email xác nhận** với thông tin chi tiết.
✅ **Lưu tất cả dữ liệu** vào Airtable để theo dõi dễ dàng.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS riêng.
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 Mã giảm giá: **VPSN8N** - giảm tới **39%**).
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (đủ sức mạnh cho workflow này).
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ/tuần** cho đội HR (không cần đọc CV thủ công).
- **Chọn ứng viên chính xác** với AI đánh giá khách quan (điểm, kỹ năng, trải nghiệm).
- **Đặt lịch tự động** trên Google Calendar (không cần can thiệp).
- **Quản lý ứng viên dễ dàng** với Airtable (theo dõi trạng thái, điểm số, lịch phỏng vấn).
- **Gửi email cá nhân hóa** với thông tin chi tiết (không cần copy-paste).
- **Hoạt động liên tục** (không cần người dùng mở ứng dụng).
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
✔ **Tài khoản Google Workspace** (Gmail + Google Drive + Google Calendar) với quyền:
   - Đọc email (nhận CV).
   - Tải lên và quản lý file trên Google Drive.
   - Tạo và quản lý sự kiện trên Google Calendar.
✔ **Tài khoản Airtable** (một base mới hoặc table đã tồn tại để lưu dữ liệu ứng viên).
✔ **API Key OpenAI** (đăng ký tại [OpenAI](https://platform.openai.com/)).
✔ **Danh sách vị trí tuyển dụng** (các role mà công ty đang cần, sẽ được cấu hình trong node **"Available Positions"**).

---
### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n.io/workflows/11912](https://n8n.io/workflows/11912) và import vào **n8n Editor**.
- **Cách 2**: Copy toàn bộ JSON từ link trên và paste vào **Create Workflow** → **Import JSON** trong n8n.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này gồm **20 node**, nhưng có **5 node quan trọng nhất** cần cấu hình cẩn thận:

##### **A. Cấu hình Gmail (Nhận & Gửi Email)**
- **Node**: `Gmail Trigger1` (nhận email), `Send a message1` (gửi email xác nhận).
- **Lưu ý**:
  - Chọn **credentials**: `gmailOAuth2` (đã cấu hình trước khi import).
  - **Filter**: Đặt điều kiện nhận email có chủ đề chứa từ khóa như **"CV"**, **"Application"**, **"Job Application"**.
  - **Test**: Gửi một email mẫu (kèm file CV PDF) để kiểm tra.

##### **B. Cấu hình OpenAI (AI Xét Lựa CV)**
- **Node**: `Message a model2`, `Message a model3`, `OpenAI Chat Model2`, `OpenAI Chat Model3`.
- **Lưu ý**:
  - Chọn **credentials**: `openai` (đã cấu hình API Key).
  - **Model**: Sử dụng `gpt-4.1-mini` (nhỏ gọn, tiết kiệm chi phí).
  - **Prompt**: Các sếp **không cần chỉnh sửa** (đã tối ưu sẵn), nhưng có thể cập nhật danh sách vị trí tuyển dụng trong node **"Available Positions"** (xem phần sau).

##### **C. Cấu hình Airtable (Lưu Dữ liệu Ứng Viên)**
- **Node**: `Create a record2`, `Create a record3`.
- **Lưu ý**:
  - Chọn **credentials**: `airtable` (đã cấu hình trước).
  - **Table Name**: Đặt tên table mới (ví dụ: **"Candidate Database"**).
  - **Fields**: Cần có các trường như:
    - `Email` (email ứng viên).
    - `Resume` (link file trên Google Drive).
    - `Best Fit Role` (vị trí phù hợp).
    - `Score` (điểm đánh giá).
    - `Strengths` (điểm mạnh).
    - `Gaps` (nhược điểm).
    - `Interview Scheduled` (trạng thái đã đặt lịch chưa).

##### **D. Cấu hình Google Calendar (Đặt Lịch Phỏng Vấn)**
- **Node**: `Get Next Business Day1`, `Check Availability1`, `Create an event1`.
- **Lưu ý**:
  - Chọn **credentials**: `googleCalendar`.
  - **Thời gian mặc định**: Cài đặt khoảng giờ phỏng vấn (ví dụ: **9 AM - 6 PM**).
  - **Người tham gia**: Thêm email của người phỏng vấn và ứng viên vào node `Create an event1`.

##### **E. Cấu hình "Available Positions" (Danh sách Vị Trí Tuyển Dụng)**
- **Node**: `Available Positions1` (type: **Set**).
- **Lưu ý**:
  - Đây là **danh sách vị trí** mà AI sẽ so sánh với CV ứng viên.
  - **Cách cấu hình**:
    1. Nhấp chuột phải vào node → **Edit**.
    2. Thêm các role như:
       ```json
       [
         { "role": "Full Stack Developer", "description": "Chuyên viên phát triển ứng dụng web" },
         { "role": "Marketing Specialist", "description": "Chuyên viên tiếp thị" },
         { "role": "Data Analyst", "description": "Kỹ sư phân tích dữ liệu" }
       ]
       ```
    3. Lưu lại.

#### **3. Kích hoạt ⚡️**
- **Bước 1**: **Test Run** với email mẫu (kèm file CV PDF).
- **Bước 2**: Kiểm tra:
  - AI có phân loại email là CV không?
  - AI có đánh giá điểm số và gợi ý vị trí phù hợp không?
  - Lịch phỏng vấn có được đặt thành công không?
  - Email xác nhận có được gửi không?
- **Bước 3**: Nếu tất cả hoạt động bình thường → **Bật Active workflow**.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Tự động lưu log**: Thêm node **StickyNote** để ghi lại quá trình xử lý (giúp debug dễ dàng).
   ```json
   {
     "name": "Log Candidate Data",
     "type": "stickyNote",
     "keyParameters": {
       "message": "📌 Candidate: {{ $json["email"] }} | Role: {{ $json["bestFitRole"] }} | Score: {{ $json["score"] }}"
     }
   }
   ```

2. **Gửi báo cáo định kỳ**: Sử dụng node **Google Sheets** hoặc **Airtable API** để tự động tạo báo cáo số liệu ứng viên hàng tuần.

3. **Kết hợp với Slack/Telegram**: Thêm node **Slack Webhook** hoặc **Telegram Bot** để thông báo khi có ứng viên mới hoặc lịch phỏng vấn được đặt.

4. **Cập nhật AI prompt**: Nếu cần, các sếp có thể chỉnh sửa **prompt** trong node `OpenAI Chat Model2` để AI đánh giá theo tiêu chí riêng của công ty.

5. **Tối ưu chi phí OpenAI**: Sử dụng **gpt-3.5-turbo** thay vì `gpt-4.1-mini` nếu không cần độ chính xác cao (giảm chi phí ~50%).

---

### 📌 **Kết luận**
Workflow này **giải phóng HR khỏi công việc lặp lại**, giúp **tuyển dụng nhanh chóng và chính xác hơn**. Bằng cách tự động hóa từ **nhận CV** đến **đặt lịch phỏng vấn**, các sếp sẽ:
✔ **Tiết kiệm thời gian** (không cần đọc CV thủ công).
✔ **Tăng chất lượng tuyển dụng** (AI đánh giá khách quan).
✔ **Quản lý ứng viên hiệu quả** (dữ liệu tập trung trên Airtable).

**Hành động ngay!**
1. **Import workflow** theo hướng dẫn trên.
2. **Cấu hình các node quan trọng** (Gmail, OpenAI, Airtable, Google Calendar).
3. **Test với email mẫu** và bật workflow.
4. **Theo dõi kết quả** và mở rộng tính năng nếu cần!

💡 **Lưu ý cuối cùng**: Nếu gặp khó khăn trong quá trình cấu hình, các sếp có thể liên hệ với **Avkash Kakdiya** (tác giả workflow) qua [iTechNotion](https://itechnotion.com/) để hỗ trợ.

---
**Chúc các sếp thành công với quy trình tuyển dụng tự động hóa!** 🚀