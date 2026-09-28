---
title: "🎙️ Tự Động Chuyển Ghi Âm Cuộc Họp → Tóm Tắt & Nhiệm Vụ Hành Động với AI (AssemblyAI + GPT-4 + Google Sheets)"
description: "Workflow tự động hóa chuyển đổi ghi âm cuộc họp thành tóm tắt chuyên nghiệp và danh sách nhiệm vụ hành động, đồng thời ghi dữ liệu vào Google Sheets. Giúp tiết kiệm **100+ giờ/tháng** cho các sếp, giảm thiểu sai sót và tăng cường trách nhiệm trong quản lý dự án."
slug: "tieu-dong-chuyen-gi-am-cuoc-hop-den-tom-tat-nhiem-vu-hanh-dong"
tags: [n8n, automation, ai-summarization, assemblyai, gpt-4, google-sheets, no-code, workflow-ai]
keywords: [n8n workflow tự động hóa cuộc họp, chuyển ghi âm thành tóm tắt AI, AssemblyAI + GPT-4, tự động hóa quản lý dự án, lưu dữ liệu vào Google Sheets, tiết kiệm thời gian cuộc họp]
---

# 🚀 **Tự Động Chuyển Ghi Âm Cuộc Họp → Tóm Tắt & Nhiệm Vụ Hành Động với AI**

### **Nỗi Đau Của Các Sếp Hiện Nay**
Các sếp đã từng phải:
- **Lắng nghe lại hàng giờ ghi âm** để tóm tắt nội dung cuộc họp.
- **Mất thời gian viết tóm tắt thủ công**, dẫn đến thông tin không đầy đủ hoặc sai lệch.
- **Quên hoặc bỏ qua nhiệm vụ hành động** sau cuộc họp, gây trì hoãn dự án.
- **Không có hệ thống theo dõi** để biết ai chịu trách nhiệm và deadline của từng nhiệm vụ.

**Workflow này giải quyết tất cả vấn đề trên bằng AI + tự động hóa 100% không cần code!**

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow hoạt động **ổn định 24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS riêng.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (đủ sức mạnh cho workflow AI)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
✅ **Tiết kiệm 100+ giờ/tháng** bằng việc loại bỏ công việc tóm tắt thủ công.
✅ **Tóm tắt cuộc họp chính xác**, bao gồm:
   - **Agenda chính**
   - **Quyết định quan trọng**
   - **Điểm chính**
✅ **Trích xuất nhiệm vụ hành động** với:
   - **Người chịu trách nhiệm**
   - **Deadline cụ thể**
   - **Độ ưu tiên (cao/thấp)**
✅ **Lưu dữ liệu vào Google Sheets** để theo dõi và báo cáo dễ dàng.
✅ **Hoạt động liên tục** (không cần người dùng can thiệp).

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
✔ **Tài khoản AssemblyAI** (để chuyển đổi ghi âm thành văn bản).
✔ **API Key của AssemblyAI** (mã hóa trong workflow).
✔ **Tài khoản Google Cloud** (để kết nối với Google Sheets).
✔ **Google Sheets** (đã tạo sẵn bảng dữ liệu để lưu kết quả).
✔ **URL ghi âm cuộc họp** (cung cấp từ nhà cung cấp ghi âm như Zoom, Teams, etc.).
✔ **Mô hình AI GPT-4.1-mini** (đã tích hợp sẵn, không cần mua thêm).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/11409) hoặc copy/paste JSON vào **n8n Editor**.
- **Cách import nhanh**:
  1. Mở **n8n Workflow Editor**.
  2. Nhấn **Import** → **Paste JSON**.
  3. Dán nội dung JSON từ file và nhấn **Import**.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này gồm **15 node**, nhưng các bước **quan trọng nhất** cần điều chỉnh là:

##### **A. Cấu Hình Webhook (Recording Ready Webhook)**
- **Đường dẫn webhook**: `meeting-recording-ready` (không thay đổi).
- **Phương thức HTTP**: `POST` (không thay đổi).
- **Lưu ý**:
  - **Nhà cung cấp ghi âm** (Zoom, Teams, etc.) phải gọi đến URL này khi ghi âm hoàn tất.
  - **URL webhook** sẽ tự động tạo khi import xong. **Không thay đổi** URL này.

##### **B. Workflow Configuration (Workflow Configuration)**
- **Tham số cần điền**:
  - `assemblyaiApiKey`: API Key của AssemblyAI.
  - `sheetId`: ID của Google Sheets (tìm trong URL của sheet).
  - `tabName`: Tên tab trong Google Sheets (ví dụ: "Meeting Logs").
  - `defaultDueDate`: Ngày mặc định cho nhiệm vụ (ví dụ: `7 days from now`).
  - `recordingUrl`: URL mẫu của ghi âm (ví dụ: `https://example.com/meetings/{id}.mp3`).

##### **C. AssemblyAI Transcription (AssemblyAI Transcription)**
- **Tham số cần điền**:
  - **Headers**:
    - `Authorization`: `Bearer {assemblyaiApiKey}`.
  - **Body**:
    - `audio_url`: URL ghi âm từ webhook.
    - `format`: `mp3` (hoặc `wav` nếu ghi âm là định dạng này).

##### **D. AI Notes & Action Items (Generate Meeting Notes & Extract Action Items)**
- **Mô hình AI**: Sử dụng **GPT-4.1-mini** (đã cấu hình sẵn).
- **Lưu ý**:
  - **Prompt AI** đã được tối ưu hóa, nhưng các sếp có thể **tùy chỉnh** trong node `Prepare Meeting Notes Input` và `OpenAI Model - Meeting Notes`.
  - **Schema JSON** cho nhiệm vụ hành động cũng đã được định nghĩa sẵn, nhưng có thể **sửa đổi** trong node `Action Items Schema`.

##### **E. Log Meeting to Sheets (Log Meeting to Sheets)**
- **Tham số cần điền**:
  - **Credentials**: Chọn `googleApi` (đã cấu hình trước khi import).
  - **Sheet ID**: Điền ID của Google Sheets (tìm trong URL).
  - **Tab Name**: Điền tên tab (ví dụ: "Meeting Logs").
  - **Range**: `A1` (để ghi từ ô A1).

##### **F. Parse and Validate Action Items (Parse and Validate Action Items)**
- **Lưu ý**:
  - Node này **kiểm tra và sửa lỗi** trong danh sách nhiệm vụ.
  - **Mã JavaScript** đã được viết sẵn, nhưng các sếp có thể **sửa đổi** nếu cần.

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run** với một ghi âm mẫu:
   - Gửi một ghi âm thử đến webhook.
   - Kiểm tra kết quả trong **Google Sheets** và **node Log Meeting to Sheets**.
2. **Bật Active workflow**:
   - Nhấn **Active** trên tab workflow.
   - **Xem log** để đảm bảo không có lỗi.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết nối với Slack/Telegram**:
   - Thêm node **Slack/Telegram** sau `Log Meeting to Sheets` để thông báo kết quả cuộc họp.
2. **Lưu log chi tiết**:
   - Sử dụng node **Google Drive** để lưu toàn bộ ghi âm và transcript.
3. **Gửi báo cáo định kỳ**:
   - Tạo một workflow mới để **tổng hợp và gửi báo cáo** về nhiệm vụ hành động qua email.
4. **Tùy chỉnh AI**:
   - **Điều chỉnh prompt** trong node `Prepare Meeting Notes Input` để phù hợp với ngành nghề của công ty.
   - **Thêm hoặc loại bỏ schema** trong `Action Items Schema` nếu cần.

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc tóm tắt cuộc họp thủ công, đồng thời **tăng cường trách nhiệm** bằng cách tự động trích xuất nhiệm vụ hành động. **Không cần code**, chỉ cần **cấu hình và kích hoạt** là xong!

**Hành động ngay hôm nay**:
1. **Import workflow** và **cấu hình** theo hướng dẫn.
2. **Test với một ghi âm mẫu**.
3. **Bật Active** và **theo dõi kết quả** trong Google Sheets.

**🚀 Cùng tự động hóa cuộc họp của mình ngay bây giờ!** 🚀