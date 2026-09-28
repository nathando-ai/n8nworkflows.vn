---
title: "🚀 Tự Động Hóa Báo Cáo Email & Lịch Trên Slack Với Gemini AI & Google Workspace (Không Cần Code)"
description: "Workflow tự động hóa tổng hợp email chưa đọc trong 7 ngày và sự kiện lịch hàng ngày, sau đó tóm tắt bằng AI Gemini và gửi báo cáo định kỳ lên Slack. Giúp các sếp tiết kiệm thời gian, tập trung vào công việc quan trọng hơn."
slug: "tieu-dong-hoa-bao-cao-email-lich-slack-gemini-ai"
tags: [n8n, automation, no-code, ai-summarization, google-workspace, slack-integration]
keywords: [n8n workflow tự động hóa, tổng hợp email với AI, báo cáo lịch Google, Gemini AI, tự động hóa Slack, Google Sheets API]
---

# 🚀 **Tự Động Hóa Báo Cáo Email & Lịch Trên Slack Với Gemini AI & Google Workspace**

### **Giải Pháp Cho Các Sếp Bận Rộn**
Hàng ngày, các sếp phải mất thời gian quét qua hàng chục email chưa đọc và kiểm tra lịch để cập nhật công việc. **Workflow này tự động hóa toàn bộ quy trình** bằng cách:
- Lấy tất cả email chưa đọc trong **7 ngày qua**.
- Lấy tất cả sự kiện lịch trong ngày hôm nay.
- **Lọc email** theo danh sách người liên quan (từ Google Sheets).
- **Tóm tắt email và lịch** bằng AI Gemini (Google’s AI model).
- **Gửi báo cáo định kỳ** lên Slack để các sếp cập nhật nhanh chóng.

Không cần viết một dòng code nào! Chỉ cần **cấu hình và chạy**, workflow sẽ hoạt động **24/7** như một trợ lý ảo thông minh.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian**: Không phải quét email hoặc lịch thủ công.
✅ **Tóm tắt thông minh**: AI Gemini tự động rút gọn nội dung email và sự kiện.
✅ **Lọc email chính xác**: Chỉ lấy email liên quan đến danh sách người trong Google Sheets.
✅ **Báo cáo tự động**: Gửi lên Slack hàng ngày, giúp các sếp cập nhật nhanh chóng.
✅ **Hoạt động liên tục**: Workflow chạy tự động mỗi sáng, không cần can thiệp.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
✔ **Google Sheets** với **3 cột**: `Name`, `Email`, `Subject` (dùng để lọc email).
✔ **Tài khoản Gmail** (để lấy email chưa đọc).
✔ **Google Calendar** (để lấy sự kiện).
✔ **Slack Workspace** (để nhận báo cáo).
✔ **API Key Gemini AI** (để tóm tắt nội dung).
✔ **Credentials cho các dịch vụ**:
   - Google Sheets (Service Account JSON).
   - Gmail (OAuth 2.0).
   - Slack (Bot Token).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/8109](https://n8n.io/workflows/8109) hoặc copy toàn bộ JSON từ trang này.
- Mở **n8n Editor** → Nhấn `Import` → Dán JSON và nhấn `Import`.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Dưới đây là **các node quan trọng** cần cấu hình cẩn thận:

##### **📌 Node 1: Cron (Đặt lịch chạy hàng ngày)**
- **Cấu hình**: `0 7 * * *` (chạy lúc 7h sáng hàng ngày).
- **Lưu ý**: Đảm bảo **n8n đang chạy 24/7** trên VPS.

##### **📌 Node 2: Google Sheets (Lấy danh sách lọc email)**
- **Credentials**: Chọn **Service Account** (tạo từ Google Cloud Console).
- **Sheet Name**: Điền tên file Google Sheets của bạn.
- **Range**: `Sheet1!A:D` (giả sử dữ liệu ở Sheet1, cột A-D).
- **Lưu ý**: Đảm bảo **cột đầu tiên là "Name"**, thứ hai là "Email", thứ ba là "Subject"**.

##### **📌 Node 3: Gmail (Lấy email chưa đọc)**
- **Credentials**: Chọn **OAuth 2.0** (cấu hình từ [Google Cloud Console](https://console.cloud.google.com/)).
- **Operation**: `getAll` (lấy tất cả email chưa đọc trong 7 ngày).
- **Lưu ý**: Đảm bảo **tài khoản Gmail đã cho phép ứng dụng không an toàn** (nếu cần).

##### **📌 Node 4: Google Calendar (Lấy sự kiện)**
- **Credentials**: Chọn **OAuth 2.0** (cấu hình từ Google Cloud Console).
- **Operation**: `getAll` (lấy tất cả sự kiện trong ngày hôm nay).
- **Lưu ý**: Đảm bảo **tài khoản Calendar đã được kết nối**.

##### **📌 Node 5: AI Agent (Tóm tắt email & lịch)**
- **Model**: Chọn **Google Gemini** (đã được cấu hình sẵn trong workflow).
- **Prompt**: Workflow đã tự động cấu hình, **không cần chỉnh sửa** (nếu muốn thay đổi, mở node `Google Gemini Chat Model` và sửa `prompt`).
- **Lưu ý**: Đảm bảo **API Key Gemini** đã được điền vào `n8n-nodes-langchain.lmChatGoogleGemini`.

##### **📌 Node 6: Merge (Kết hợp dữ liệu)**
- **Lưu ý**: Node này tự động kết hợp email đã tóm tắt và sự kiện lịch.
- **Không cần chỉnh sửa** nếu muốn giữ nguyên logic.

##### **📌 Node 7: Slack (Gửi báo cáo)**
- **Credentials**: Chọn **Slack Bot Token** (tạo từ [Slack API](https://api.slack.com/apps)).
- **Channel**: Điền `#channel-bao-cao` (hoặc channel của bạn).
- **Lưu ý**: Đảm bảo **bot Slack đã được thêm vào channel**.

##### **📌 Node 8: Code (Restructure dữ liệu)**
- **Lưu ý**: Các node `Restructure` (Code) đã được cấu hình sẵn để chuyển đổi dữ liệu thành định dạng Slack Block Kit.
- **Không cần chỉnh sửa** trừ khi muốn thay đổi cách hiển thị.

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run** (nút `Run Workflow` ở góc trên phải) với dữ liệu mẫu để kiểm tra.
2. **Active Workflow** (bật nút `Active` ở góc trên phải).
3. **Kiểm tra Slack** vào sáng hôm sau để xem báo cáo đã được gửi không.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Thêm Logs cho Debug**:
   - Thêm node **Sticky Note** sau `Google Gemini Chat Model` để lưu kết quả tóm tắt.
   - Cách thêm: `+ Add Node` → Tìm `Sticky Note` → Kết nối sau node AI.

2. **Gửi Báo Cáo Định Kỳ**:
   - Nếu muốn gửi báo cáo **mỗi sáng 8h**, thay đổi Cron thành `0 8 * * *`.

3. **Tích Hợp Email Báo Cáo**:
   - Thêm node **Gmail Send Email** sau `Slack` để gửi báo cáo qua email nếu cần.

4. **Cập Nhật Danh Sách Email Lọc**:
   - Mở Google Sheets và **cập nhật danh sách Name, Email, Subject** để lọc email mới.

5. **Sử Dụng AI Gemini Pro**:
   - Nếu muốn tóm tắt chất lượng cao hơn, thay đổi model từ `Gemini` sang `Gemini Pro` (cần API Key mới).

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp bằng cách tự động hóa việc tổng hợp email và lịch, sau đó gửi báo cáo lên Slack. **Không cần code, không cần kỹ thuật**, chỉ cần **cấu hình và chạy** là xong!

**🚀 Hãy áp dụng ngay để bắt đầu ngày mới với thông tin cập nhật nhanh chóng!**

---
**💡 Cần hỗ trợ?**
- Trên [n8n Community](https://community.n8n.io/) hoặc liên hệ [SayOne Technologies](https://sayone.tech/) (tác giả của workflow).
- Nếu gặp vấn đề với VPS, liên hệ [TinoHost](https://tino.vn) hoặc [BNIX](https://my.bnix.one/).