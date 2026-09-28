---
title: "🍽️ **Hệ Thống Theo Dõi Calorie & Ghi Chép Bữa Ăn Tự Động với Telegram + Gemini AI (N8N)**"
description: "Tự động hóa ghi chép bữa ăn, phân tích calorie và tạo báo cáo sức khỏe thông minh chỉ với Telegram và Gemini AI. Giúp các sếp tiết kiệm thời gian, theo dõi chế độ ăn uống hiệu quả và nhận phân tích cá nhân hóa 24/7."
slug: "calorie-tracker-telegram-gemini-ai-n8n"
tags: [n8n, automation, no-code, ai-automation, google-gemini, telegram-bot, data-tracking]
keywords: [n8n workflow calorie tracker, tự động hóa ghi chép bữa ăn, Gemini AI với Telegram, phân tích calorie tự động, n8n self-hosted]
---

# 🚀 **Hệ Thống Theo Dõi Calorie & Ghi Chép Bữa Ăn Tự Động với Telegram + Gemini AI**

### **Giải pháp cho các sếp muốn sống khỏe mà không mất thời gian ghi chép bữa ăn thủ công**
Ghi chép bữa ăn, tính calorie và theo dõi chế độ ăn uống là một việc làm tẻ nhạt, dễ quên và tốn thời gian. Nhưng với **workflow này**, các sếp có thể:
- **Ghi chép bữa ăn chỉ bằng Telegram** (thông qua tin nhắn, ảnh, hoặc ghi âm).
- **Được Gemini AI phân tích calorie, dinh dưỡng và đưa ra gợi ý** ngay lập tức.
- **Tự động lưu dữ liệu vào bảng Excel/Google Sheets** để theo dõi xu hướng ăn uống dài hạn.
- **Nhận báo cáo sức khỏe cá nhân hóa** định kỳ (ví dụ: tuần hoặc tháng).

Không cần code, không cần kỹ sư AI – chỉ cần **n8n self-hosted** và một chút cấu hình, các sếp đã có một **hệ thống tự động hóa hoàn chỉnh** để quản lý sức khỏe ăn uống một cách thông minh.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo tính riêng tư và hiệu suất cao.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (Đảm bảo tốc độ xử lý nhanh cho AI)
:::

---

## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần ghi chép thủ công, chỉ cần gửi tin nhắn hoặc ảnh bữa ăn qua Telegram.
- **Phân tích calorie & dinh dưỡng tự động**: Gemini AI phân tích thành phần dinh dưỡng của mỗi bữa ăn và tính toán calorie.
- **Báo cáo sức khỏe cá nhân hóa**: Nhận tổng hợp dữ liệu ăn uống hàng tuần/tháng để điều chỉnh chế độ ăn.
- **Hỗ trợ đa dạng đầu vào**: Ghi âm, ảnh bữa ăn, hoặc tin nhắn văn bản đều được xử lý.
- **Lưu trữ dữ liệu dài hạn**: Dữ liệu được tự động lưu vào **Google Sheets/DataTable** để theo dõi xu hướng.
- **Tương tác 24/7**: Hệ thống hoạt động liên tục, không phụ thuộc vào thời gian làm việc của các sếp.
:::

---

## 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
### **1. Tài khoản & API Keys**
- **Tài khoản Telegram Bot**:
  - Tạo bot trên [@BotFather](https://t.me/BotFather) và lấy **API Token**.
  - Thêm bot vào nhóm Telegram cá nhân để test.
- **Google Gemini API**:
  - Đăng ký [Google AI Studio](https://aistudio.google/) và lấy **API Key**.
  - Chọn mô hình **Gemini Pro** (hoặc Gemini 1.5).
- **Google Sheets (tùy chọn)**:
  - Tạo một bảng Google Sheets để lưu dữ liệu bữa ăn.
  - Chia sẻ bảng với quyền **Editor** cho n8n.

### **2. Cấu hình n8n**
- **Self-hosted n8n** (không dùng phiên bản cloud để đảm bảo dữ liệu riêng tư).
- **Node LangChain** (đã được tích hợp trong workflow, cần cài đặt từ [n8n Community Nodes](https://n8n.io/community/)).

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. Tải workflow từ [n8n.io/workflows/9294](https://n8n.io/workflows/9294) (chọn **Download JSON**).
2. Mở **n8n Editor** (trang chủ của n8n self-hosted).
3. Nhấn **Import** và chọn file JSON vừa tải.
4. Chọn **Create Workflow** để bắt đầu cấu hình.

#### **Phương pháp 2: Copy/Paste JSON**
1. Mở **n8n Editor** và nhấn **Create Workflow**.
2. Chọn **Import** > **Paste JSON**.
3. Dán nội dung JSON từ [n8n.io/workflows/9294](https://n8n.io/workflows/9294) (chọn **Copy JSON**).
4. Nhấn **Import** và bắt đầu cấu hình.

---

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflows này **phức tạp** với 65 node, nhưng các sếp chỉ cần chú ý đến các phần quan trọng sau:

#### **A. Cấu hình Telegram Bot**
1. **Node "Telegram Trigger"**:
   - Điền **API Token** của bot Telegram vào **Credentials**.
   - Chọn **Chat ID** của nhóm/private chat để nhận tin nhắn.
   - **Lưu ý**: Nếu chưa có Chat ID, các sếp có thể gửi tin nhắn `/get_id` cho bot và lấy giá trị trả về.

2. **Node "Send a text message"**:
   - Chọn **Credentials** của Telegram Bot.
   - Thay đổi **Chat ID** thành Chat ID của nhóm cá nhân.

#### **B. Cấu hình Google Gemini AI**
1. **Tất cả node có tiền tố "Google Gemini"** (ví dụ: `Google Gemini Chat Model1`, `Analyze Text Message`):
   - Điền **API Key** của Google Gemini vào **Credentials**.
   - Chọn mô hình **Gemini Pro** (hoặc Gemini 1.5) trong **Configuration**.
   - **Lưu ý**: Nếu API Key hết hạn, workflow sẽ báo lỗi. Các sếp cần **kiểm tra lại API Key** định kỳ.

#### **C. Cấu hình DataTable (Google Sheets)**
1. **Node "Is User Registered?"** và **"Register User"**:
   - Chọn **Credentials** của Google Sheets.
   - Điền **Sheet Name** là `UserData` (hoặc tên sheet các sếp muốn sử dụng).
   - **Lưu ý**: Sheet phải có **cột: `user_id`, `name`, `email`** (nếu chưa có, các sếp cần tạo trước).

2. **Node "Append Meal Data"**:
   - Chọn **Credentials** của Google Sheets.
   - Điền **Sheet Name** là `MealData` (hoặc tên sheet các sếp muốn lưu dữ liệu bữa ăn).
   - **Lưu ý**: Sheet phải có **cột: `user_id`, `meal_name`, `calories`, `description`, `timestamp`**.

#### **D. Cấu hình Agent AI**
Workflows này sử dụng **LangChain Agent** để xử lý logic phức tạp. Các sếp **không cần chỉnh sửa mã**, nhưng cần:
1. **Node "Register Agent"**:
   - Đảm bảo **Credentials** của Google Gemini đã được cài đặt.
2. **Node "Cal AI Router Agent"**:
   - Đây là **cơ chế phân loại** tin nhắn của người dùng (ghi bữa ăn, cập nhật thông tin, yêu cầu báo cáo...).
   - **Không cần chỉnh sửa**, nhưng nếu gặp lỗi, các sếp có thể **test run** với dữ liệu mẫu.

#### **E. Cấu hình Webhook (tùy chọn)**
- **Node "Webhook"**:
  - Nếu các sếp muốn **kích hoạt workflow từ bên ngoài** (ví dụ: từ website), cần:
    - Chọn **Credentials** mới (nếu cần).
    - Điền **URL Webhook** (ví dụ: `https://domain.com/webhook`).
    - **Lưu ý**: Nếu không dùng webhook, có thể **xóa node này** để tiết kiệm tài nguyên.

---

### **3. Kích hoạt ⚡️**
1. **Test Run với dữ liệu mẫu**:
   - Gửi tin nhắn **/start** đến bot Telegram để đăng ký tài khoản.
   - Gửi **ảnh bữa ăn** hoặc **ghi âm** để test phân tích calorie.
   - Gửi **tin nhắn văn bản** như:
     - *"Ghi bữa ăn: Phở bò, 500 calorie"*
     - *"Báo cáo tuần này"*
     - *"Cập nhật thông tin: Tên: [Tên], Tuổi: 30"*

2. **Bật Active workflow**:
   - Sau khi test thành công, nhấn **Active** trên n8n Editor.

---

## ✍️ **Mẹo & gợi ý nâng cao**
### **1. Tích hợp với Slack/Email (nâng cao)**
- **Node "Send a text message"** có thể thay thế bằng **Slack** hoặc **Email** để nhận báo cáo.
- **Cách làm**:
  1. Cài **n8n-nodes-slack** hoặc **n8n-nodes-email**.
  2. Thay thế **Credentials** của Telegram bằng Slack/Email.
  3. Cấu hình **Webhook Slack** hoặc **SMTP Email**.

### **2. Lưu log hoạt động**
- **Node "StickyNote"** (nếu có) có thể được sử dụng để lưu **log lỗi** hoặc **dữ liệu debug**.
- **Cách làm**:
  - Thêm **StickyNote** sau node có lỗi (ví dụ: sau `Google Gemini Chat Model`).
  - Lưu **JSON output** để phân tích sau.

### **3. Tự động gửi báo cáo định kỳ**
- Sử dụng **n8n Cron Trigger** để gửi báo cáo hàng tuần/tháng.
- **Cách làm**:
  1. Thêm **Cron Trigger** vào workflow.
  2. Cấu hình **lịch chạy** (ví dụ: `0 0 * * 0` để chạy Chủ Nhật hàng tuần).
  3. Gửi báo cáo qua **Telegram/Email** bằng node `Send a text message`.

### **4. Phân tích ảnh bữa ăn tự động**
- **Node "Analyze image"** sử dụng **Gemini AI** để phân tích thành phần dinh dưỡng từ ảnh.
- **Mẹo**:
  - Chụp ảnh bữa ăn **đầy đủ** (không chỉ một món).
  - Đảm bảo **ánh sáng tốt** để AI nhận diện chính xác.

### **5. Cập nhật thông tin cá nhân**
- Các sếp có thể **cập nhật thông tin** (tuổi, chiều cao, cân nặng) để AI tính toán **BMR (Metabolic Rate)** và gợi ý calorie phù hợp.
- **Cách làm**:
  - Gửi tin nhắn: *"Cập nhật thông tin: Tuổi: 30, Cân nặng: 70kg, Chiều cao: 175cm"*.

---

## 📌 **Kết luận**
### **Bắt đầu tự động hóa chế độ ăn uống ngay hôm nay!**
Workflows này là **giải pháp hoàn chỉnh** để các sếp:
✅ **Ghi chép bữa ăn một cách dễ dàng** chỉ với Telegram.
✅ **Phân tích calorie & dinh dưỡng tự động** bằng Gemini AI.
✅ **Theo dõi xu hướng ăn uống dài hạn** trên Google Sheets.
✅ **Nhận báo cáo sức khỏe cá nhân hóa** định kỳ.

**Không cần là kỹ sư AI**, các sếp chỉ cần:
1. **Import workflow** từ [n8n.io/workflows/9294](https://n8n.io/workflows/9294).
2. **Cấu hình Telegram + Google Gemini** theo hướng dẫn.
3. **Test run** và **bật Active**.

**Hãy thử ngay và bắt đầu sống khỏe hơn!** 💪🍏

---
### **🔗 Tài liệu tham khảo**
- [Tutorial n8n Self-hosted](https://docs.n8n.io/)
- [Google Gemini API Docs](https://ai.google.dev/gemini-api/docs)
- [LangChain Agents in n8n](https://n8n.io/community/nodes/n8n-nodes-langchain)