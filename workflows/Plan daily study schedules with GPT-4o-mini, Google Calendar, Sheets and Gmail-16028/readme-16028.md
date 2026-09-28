---
title: "🎯 Tự Động Hoàn Thành Lịch Học Hàng Ngày với GPT-4o-mini, Google Calendar & Gmail - Không Cần Code!"
description: "Workflow tự động hóa sinh lịch học cá nhân hóa từ ngày thi, môn học và thời gian sẵn sàng hàng ngày, đồng thời tự động thêm vào Google Calendar và Google Sheets. Giúp học sinh tiết kiệm 8+ giờ/tháng và giảm stress chuẩn bị thi."
slug: "tieu-dong-hoan-thanh-lich-hoc-hang-ngay"
tags: [n8n, automation, ai, google-calendar, google-sheets, gmail, personal-productivity]
keywords: [tự động hóa lịch học, n8n workflow, GPT-4o-mini, lịch học cá nhân hóa, google calendar tự động, google sheets tự động]
---

# 🚀 **Tự Động Hoàn Thành Lịch Học Hàng Ngày với AI - Không Cần Code!**

### **Giải pháp cho học sinh/ sinh viên:**
Bạn đã bao giờ cảm thấy **mệt mỏi** khi phải tự tay xây dựng lịch học hàng ngày, phân bổ thời gian cho từng môn học, và lo lắng liệu mình có học đủ không? Hay **chưa biết cách** phân bổ thời gian học hiệu quả, đặc biệt là khi có nhiều môn học và ngày thi sắp đến?

**Workflow này sẽ:**
✅ **Tự động sinh lịch học cá nhân hóa** dựa trên ngày thi, môn học và thời gian sẵn sàng hàng ngày.
✅ **Tự động thêm lịch vào Google Calendar** với thời gian, chủ đề và loại buổi học (học mới, ôn tập, thực hành).
✅ **Ghi lại lịch học vào Google Sheets** để theo dõi tiến độ.
✅ **Gửi email xác nhận lịch học** với định dạng HTML đẹp mắt và lời khuyên học tập.

---
### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 8+ giờ/tháng** so với cách làm thủ công.
- **Lịch học được tối ưu hóa** với phân bổ thời gian hợp lý, đặc biệt là ôn tập gần ngày thi.
- **Không lo quên** vì lịch được tự động thêm vào Google Calendar.
- **Theo dõi tiến độ dễ dàng** với Google Sheets.
- **Không cần code** - chỉ cần nhập thông tin và AI sẽ làm hết!
:::

---
### 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
1. **Tài khoản OpenAI** (để sử dụng GPT-4o-mini) và **API Key**.
2. **Tài khoản Google** (để kết nối Google Calendar, Google Sheets và Gmail).
3. **Google Sheet** có tên tab là **"Study Planner"** với các cột sau:
   - Student Name, Exam Date, Subject, Topic, Date, Day, Start Time, End Time, Duration (hrs), Session Type, Priority, Status.
4. **Email** để nhận lịch học sau khi hoàn thành.
:::

---
### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### 1. **Import Workflow 📥**
- **Cách 1:** Tải file JSON từ [n8n.io/workflows/16028](https://n8n.io/workflows/16028) và import vào n8n Editor.
- **Cách 2:** Copy toàn bộ JSON từ link trên và dán vào **Import Workflow** trong n8n Editor.

#### 2. **Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow gồm **9 node** chính, các sếp cần chú ý cấu hình các node sau:

##### **A. Node 1: Form — Study Planner Input**
- **Không cần chỉnh** (form đã được thiết kế sẵn với các trường: Name, Exam Date, Subjects, Daily Hours, Email).

##### **B. Node 2 & 3: AI Agent — Generate Study Schedule + OpenAI — GPT-4o-mini Model**
- **Cấu hình OpenAI API Key:**
  - Vào node **OpenAI — GPT-4o-mini Model** → Chọn **Credentials** → Thêm **OpenAI API Key** (mua tại [OpenAI](https://platform.openai.com/)).
  - **Model:** Đảm bảo chọn **gpt-4o-mini** (đã được thiết lập sẵn).

##### **C. Node 5: Google Calendar — Create Study Event**
- **Kết nối Google Calendar:**
  - Vào node → Chọn **Credentials** → Thêm **Google OAuth2** (cách kết nối: [Google Calendar OAuth](https://developers.google.com/calendar/api/guides/overview)).
  - **Thay đổi `YOUR_CALENDAR_ID`** (thường là email của bạn hoặc tìm trong **Cài đặt → Calendars** trên Google Calendar).

##### **D. Node 7: Google Sheets — Log Study Plan**
- **Kết nối Google Sheets:**
  - Vào node → Chọn **Credentials** → Thêm **Google OAuth2** (cách kết nối: [Google Sheets OAuth](https://developers.google.com/sheets/api/guides/overview)).
  - **Thay đổi `YOUR_GOOGLE_SHEET_ID`** (tìm ID Sheet trong URL: `https://docs.google.com/spreadsheets/d/[ID]/edit`).
  - **Đảm bảo Sheet có tab "Study Planner"** với các cột như mô tả ở trên.

##### **E. Node 8: Gmail — Send Confirmation Email**
- **Kết nối Gmail:**
  - Vào node → Chọn **Credentials** → Thêm **Gmail OAuth2** (cách kết nối: [Gmail OAuth](https://developers.google.com/gmail/api/quickstart/python)).
  - **Không cần chỉnh thêm** (email sẽ tự động gửi từ tài khoản đã kết nối).

#### 3. **Kích hoạt ⚡️**
- **Test Run:**
  - Nhập dữ liệu mẫu vào **Form — Study Planner Input** (ví dụ: Name = "John", Exam Date = "2024-12-15", Subjects = "Toán, Lý, Hóa", Daily Hours = "4", Email = "john@example.com").
  - Chạy **Test Run** để kiểm tra workflow hoạt động như thế nào.
- **Bật Active:**
  - Sau khi test thành công, chuyển workflow sang **Active**.

---
### ✍️ **Mẹo & gợi ý nâng cao**
:::info[TIPS THỰC TIỆN]
1. **Tự động gửi lịch hàng tuần:**
   - Sử dụng **n8n Trigger** (Webhook hoặc Schedule Node) để chạy workflow hàng tuần thay vì chỉ khi cần.
2. **Thêm Slack/Telegram Notification:**
   - Sau khi lịch được tạo, thêm node **Slack** hoặc **Telegram** để thông báo kết quả ngay khi hoàn thành.
3. **Lưu log hoạt động:**
   - Sử dụng node **StickyNote** để ghi lại lịch sử chạy workflow (ví dụ: ngày chạy, người dùng, kết quả).
4. **Cập nhật lịch học theo thời gian thực:**
   - Nếu có thay đổi trong lịch (ví dụ: thêm môn học mới), chỉ cần chạy lại workflow với dữ liệu mới.
5. **Tối ưu hóa GPT-4o-mini:**
   - Nếu muốn lịch học được sinh nhanh hơn, thử sử dụng **GPT-3.5-turbo** (rẻ hơn) thay vì **gpt-4o-mini** (tùy thuộc vào yêu cầu chất lượng).
:::

---
### 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho học sinh/sinh viên muốn **tự động hóa lịch học**, tiết kiệm thời gian và giảm stress chuẩn bị thi. **Không cần code**, chỉ cần nhập thông tin và AI sẽ làm hết!

**Hãy thử ngay và bắt đầu học tập hiệu quả hơn!** 🚀

---
:::note[CHÚ Ý]
- **N8n Self-hosted** (cài trên VPS) sẽ giúp workflow **chạy 24/7** mà không bị giới hạn.
- **Nếu cần hỗ trợ**, các sếp có thể liên hệ với [Incrementors](https://incrementors.com/) (tác giả của workflow).
:::

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::