---
title: "🚀 Tự Động Hóa Email Chúc Mừng Sinh Nhật Hàng Ngày Với NASA, GPT-4 & Slack – Chúc Mừng Đặc Biệt Cho Người Yêu"
description: "Workflow tự động hóa gửi email chúc mừng sinh nhật hàng ngày với chủ đề không gian, kết hợp hình ảnh NASA, AI GPT-4 và thông báo Slack – tiết kiệm thời gian, cá nhân hóa và mang lại trải nghiệm độc đáo cho người nhận."
slug: "tieu-dong-hoa-email-chuc-mung-sinh-nhat-nasa-gpt4-slack"
tags: [n8n, automation, no-code, ai-chatbot, google-sheets, slack-integration, email-automation]
keywords: [n8n workflow sinh nhật, tự động hóa email chúc mừng, GPT-4 sinh nhật, NASA API, Slack notification, tự động hóa không gian]
---

# 🚀 **Tự Động Hóa Email Chúc Mừng Sinh Nhật Hàng Ngày Với NASA, GPT-4 & Slack**

## **🌌 Giải Pháp Cho Những Người Quên Làm Chúc Mừng Sinh Nhật**
Bạn có bao giờ cảm thấy **quên chúc mừng sinh nhật** cho đồng nghiệp, bạn bè hoặc thành viên trong nhóm? Hay lại phải **ghi nhớ hàng loạt email** để không quên ngày đặc biệt của họ? Với workflow này, **các sếp** sẽ không còn lo lắng nữa! Hàng ngày lúc **7h sáng**, hệ thống sẽ tự động:
✅ **Lấy danh sách sinh nhật** từ Google Sheets.
✅ **Lấy hình ảnh NASA** về Trái Đất từ API NASA EPIC.
✅ **Sử dụng GPT-4** để tạo **bài chúc mừng độc đáo** với chủ đề không gian.
✅ **Gửi email cá nhân hóa** với hình ảnh và lời chúc.
✅ **Thông báo trên Slack** để toàn bộ team cùng chúc mừng.

**Kết quả?** Một **trải nghiệm sinh nhật độc đáo**, **tiết kiệm thời gian** và **không bao giờ quên**!

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7**, các sếp nên cài **n8n trên VPS riêng (Self-hosted)** để tránh giới hạn của phiên bản Cloud.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không phải ghi nhớ hoặc gửi email thủ công.
- **Cá nhân hóa cao**: Mỗi email đều có **lời chúc độc đáo** từ AI + hình ảnh NASA.
- **Hoạt động liên tục**: Chỉ cần **cấu hình 1 lần**, hệ thống tự động chạy hàng ngày.
- **Tăng tính chuyên nghiệp**: Thông báo Slack giúp **toàn bộ team** cùng tham gia chúc mừng.
- **Trải nghiệm độc đáo**: Không chỉ là email thông thường, mà còn có **chủ đề không gian** mang tính thú vị.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
✔ **Tài khoản Google Sheets** (để lưu danh sách sinh nhật).
✔ **Tài khoản Gmail** (để gửi email chúc mừng).
✔ **Tài khoản Slack** (để thông báo nhóm).
✔ **API Key OpenAI** (để sử dụng GPT-4).
✔ **Google Sheets** với **cấu trúc dữ liệu chuẩn**:
   - Cột `Name` (Tên người)
   - Cột `Email` (Email của họ)
   - Cột `Birthday` (Ngày sinh, định dạng `DD/MM`)

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/10645](https://n8n.io/workflows/10645).
- **Mở n8n Editor** → Nhấn **Import** → Chọn file JSON → **Import**.
- **Hoặc copy/paste** JSON vào **Import Workflow** trong n8n.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow gồm **12 node**, các sếp cần **cấu hình chính xác** các phần sau:

##### **📌 Node 1: Every Morning at 7:00 (Schedule Trigger)**
- **Không cần chỉnh sửa**, workflow đã được **cấu hình chạy hàng ngày lúc 7h sáng**.

##### **📌 Node 2: Get Birthday Roster (Google Sheets)**
- **Credentials**: Chọn **Google Sheets credentials** đã tạo trước.
- **Document ID**: Lấy từ **URL Google Sheets** (phần giữa `docs.google.com/spreadsheets/d/`).
- **Sheet Name**: Tên của **tab** chứa dữ liệu sinh nhật.

##### **📌 Node 3 & 4: Filter Today's Birthdays & Any Birthdays Today? (Code + If)**
- **Không cần chỉnh**, workflow tự động **lọc ngày sinh ngày hôm nay**.

##### **📌 Node 5: Prepare Birthday Data (Code)**
- **Không cần chỉnh**, node này **định dạng dữ liệu** cho bước tiếp theo.

##### **📌 Node 6: Generate Space Birthday Message (Agent)**
- **Credentials**: Chọn **OpenAI credentials**.
- **Prompt**: Workflow đã **sẵn sàng**, chỉ cần **không xóa** phần này.
- **Model**: Đã chọn **gpt-4.1-mini** (tiết kiệm chi phí).

##### **📌 Node 7: OpenAI Chat Model (lmChatOpenAi)**
- **Model**: Đã chọn **gpt-4.1-mini** (tốt nhất cho việc tạo nội dung cá nhân hóa).
- **API Key**: Đảm bảo **API Key OpenAI** được cập nhật trong credentials.

##### **📌 Node 8: Count Birthdays (Code)**
- **Không cần chỉnh**, node này **đếm số lượng sinh nhật** để thông báo Slack.

##### **📌 Node 9: Post Slack Notification (Slack)**
- **Credentials**: Chọn **Slack credentials**.
- **Channel ID**: Lấy từ **URL Slack channel** (phần cuối `channels/CHANNEL_ID`).
- **Message**: Workflow tự động **điền thông tin** về số lượng sinh nhật.

##### **📌 Node 10: Fetch NASA EPIC Images (HTTP Request)**
- **Không cần chỉnh**, node này **tự động lấy hình ảnh NASA** mới nhất.

##### **📌 Node 11: Format for Gmail (Code)**
- **Không cần chỉnh**, node này **định dạng email** với hình ảnh và lời chúc.

##### **📌 Node 12: Send Birthday Email (Gmail)**
- **Credentials**: Chọn **Gmail credentials**.
- **From Email**: Đảm bảo **email này có quyền gửi** (không bị block).
- **HTML Content**: Workflow tự động **điền nội dung** từ bước trước.

---

#### **3. Kích hoạt ⚡️**
- **Test Run**: Nhấn **Run Workflow** với **dữ liệu mẫu** để kiểm tra.
- **Active Workflow**: Sau khi **không có lỗi**, chuyển **Active** để chạy hàng ngày.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Thêm hình ảnh cá nhân hóa**:
   - Sử dụng **node `httpRequest`** để lấy ảnh từ **API NASA** khác (ví dụ: `Mars`, `Jupiter`).
   - Cấu hình **ngẫu nhiên** hình ảnh để mỗi email có **một chủ đề không gian khác nhau**.

2. **Gửi báo cáo định kỳ**:
   - Thêm **node `scheduleTrigger`** để gửi **tổng hợp sinh nhật trong tháng** vào cuối tháng.

3. **Kết hợp với Zoom/Teams**:
   - Sử dụng **node `zoom`** để tự động **tạo cuộc họp chúc mừng** cho người có sinh nhật.

4. **Lưu log hoạt động**:
   - Thêm **node `stickyNote`** để ghi lại **lịch sử gửi email** (giúp theo dõi và debug).

5. **Tăng tính cá nhân hóa**:
   - Sử dụng **node `code`** để thêm **một câu chuyện ngắn** về người đó (ví dụ: "Năm nay, bạn đã hoàn thành dự án XYZ – thật tuyệt!").

---

### 📌 **Kết luận**
Workflow này không chỉ **giúp các sếp không bao giờ quên chúc mừng sinh nhật**, mà còn **tạo ra những trải nghiệm độc đáo** với **hình ảnh NASA + lời chúc từ AI**. **Chỉ cần cấu hình 1 lần**, hệ thống sẽ tự động hoạt động hàng ngày!

**🚀 Hãy áp dụng ngay và làm cho sinh nhật của mọi người trở nên đặc biệt hơn!**

---
**💡 Cần hỗ trợ?** Đăng ký **VPS n8n** từ [TinoHost](https://tino.vn/vps-n8n?affid=388) để workflow chạy **ổn định 24/7**!