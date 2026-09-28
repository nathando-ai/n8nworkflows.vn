---
title: "🤖 Tự Động Hoá Lịch Google Từ Email Nhờ AI Gemini: Giảm 90% Thời Gian Sắp Lịch"
description: "Workflow tự động hóa chuyển đổi email có nhãn thành sự kiện lịch Google thông qua trí tuệ nhân tạo Google Gemini, tiết kiệm thời gian và tránh sai sót trong quản lý lịch. Phù hợp với doanh nghiệp, freelancer và người làm việc nhiều email hàng ngày."
slug: "tu-dong-hoa-lich-google-tu-email-nhung-ai-gemini"
tags: [n8n, automation, google-calendar, google-gmail, ai-gemini, no-code, productivity]
keywords: [tự động hóa lịch google, ai gemini n8n, chuyển email thành lịch google, tự động hóa email, công cụ quản lý lịch hiệu quả]
---

# 🚀 **Tự Động Hoá Lịch Google Từ Email Nhờ AI Gemini: Giải Pháp Cho Người Bận Rộn**

### **Nỗi Đau Của Các Sếp**
Các sếp và chuyên viên thường phải mất **30-60 phút/ngày** để:
- Lọc email có thông tin lịch (hẹn, cuộc họp, sự kiện).
- Chuyển đổi nội dung email thành sự kiện trên Google Calendar.
- Đảm bảo không bỏ sót thời gian, địa điểm hoặc chi tiết quan trọng.

Kết quả? **Sai sót, quên lịch, và mất thời gian quý giá** trong công việc chính. **Workflow này giải quyết tất cả bằng trí tuệ nhân tạo!**

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow hoạt động **24/7** mà không gián đoạn, các sếp nên **self-host n8n** trên VPS chuyên dụng:
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới 39%)
👉 [VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (đảm bảo tốc độ cao cho AI)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm 90% thời gian** trong việc sắp xếp lịch.
✅ **Tránh sai sót** nhờ AIGemini tự động trích xuất thời gian, địa điểm, mô tả.
✅ **Hoạt động tự động 24/7** mà không cần can thiệp thủ công.
✅ **Gửi email xác nhận** với link chỉnh sửa sự kiện trên Google Calendar.
✅ **Cá nhân hóa** với các nhãn email riêng (ví dụ: `Scheduled`, `Meeting`, `Event`).
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Google** (Gmail + Google Calendar).
2. **API Key Google Gemini** (đăng ký tại [Google AI Studio](https://aistudio.google.com/)).
3. **n8n Instance** (self-hosted hoặc dùng n8n.cloud).
4. **Nhãn email đặc biệt** (ví dụ: `Scheduled`) để kích hoạt workflow.
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/7340](https://n8n.io/workflows/7340).
- **Nhấn "Import"** trong n8n Editor và chọn file.
- **Hoặc copy/paste** JSON từ file vào Editor.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow gồm **6 node chính**, các sếp cần cấu hình như sau:

##### **🔹 Node 1: Gmail Trigger (Gmail Trigger)**
- **Chọn nhãn email** (ví dụ: `Scheduled`) để workflow kích hoạt khi email có nhãn này.
- **Kiểm tra credentials Gmail** đã được cấu hình trong n8n.

##### **🔹 Node 2: Google Gemini Chat Model (lmChatGoogleGemini)**
- **Điền API Key Google Gemini** vào `apiKey` (từ Google AI Studio).
- **Prompt mặc định** đã tối ưu để trích xuất:
  - **Tiêu đề sự kiện** (`title`).
  - **Thời gian bắt đầu/ket thúc** (`startTime`, `endTime`).
  - **Địa điểm** (`location`).
  - **Mô tả** (`description`).
- **Lưu ý**: Nếu muốn thay đổi prompt, chỉnh sửa ở **node "Parse Event with AI"** (node 4).

##### **🔹 Node 3: Structured Output Parser (outputParserStructured)**
- **Không cần chỉnh sửa** (n8n tự động phân tích kết quả từ Gemini).

##### **🔹 Node 4: Parse Event with AI (agent)**
- **Prompt mặc định** đã được tối ưu, nhưng các sếp có thể **cải thiện** bằng cách:
  - Thêm **múi giờ** (ví dụ: `UTC+7` thay vì `JST`).
  - Thêm **quy tắc cho sự kiện lặp lại** (nếu cần).

##### **🔹 Node 5: Create Google Calendar Event (googleCalendar)**
- **Chọn tài khoản Google Calendar** liên kết.
- **Kiểm tra quyền** để tạo sự kiện tự động.
- **Thêm chi tiết tùy chọn** (như người tham gia, nhắc nhở).

##### **🔹 Node 6: Send Confirmation Email (gmail)**
- **Điền email nhận** (ví dụ: `sếp@example.com`).
- **Chỉnh sửa nội dung email** (tiêu đề, nội dung) nếu muốn cá nhân hóa.

#### **3. Kích Hoạt ⚡️**
- **Test Run** với email mẫu có nhãn `Scheduled`.
- **Bật Active** workflow sau khi kiểm tra thành công.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết hợp với Slack/Telegram**
   - Thêm node **Slack Webhook** để thông báo sự kiện mới trên kênh công việc.

2. **Lưu Log Tự Động**
   - Sử dụng node **StickyNote** để ghi lại lịch sử sự kiện đã tạo.

3. **Gửi Báo Cáo Định Kỳ**
   - Tạo workflow phụ để **tổng hợp và gửi báo cáo** về số lượng sự kiện đã tự động hóa hàng tháng.

4. **Thêm Nhiều Nhãn Email**
   - Mỗi loại sự kiện (cuộc họp, sự kiện cá nhân) có thể có **nhãn riêng** để workflow xử lý khác nhau.

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp để tập trung vào công việc chiến lược hơn. **Chỉ cần nhãn email, AIGemini sẽ tự động chuyển đổi thành lịch Google**, gửi email xác nhận và lưu trữ log.

**🚀 Hãy áp dụng ngay và trải nghiệm sự tự động hóa hoàn hảo!**
Nếu có vấn đề, các sếp có thể **liên hệ tác giả** qua [profile của nobu](https://n8n.io/profile/nobu) để hỗ trợ thêm.

---
**#TựĐộngHóa #GoogleCalendar #AIGemini #N8N #Productivity**