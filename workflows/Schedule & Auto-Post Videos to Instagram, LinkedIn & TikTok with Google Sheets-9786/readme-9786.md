---
title: "🚀 Tự Động Hóa Đăng Video Trên Instagram, LinkedIn & TikTok Từ Google Sheets - Không Cần Code!"
description: "Workflow tự động hóa hoàn chỉnh giúp các sếp lên kế hoạch và đăng video lên 3 nền tảng lớn (Instagram, LinkedIn, TikTok) chỉ với 1 bảng Google Sheets. Tiết kiệm thời gian lên đến 20h/tuần, tránh lỡ thời điểm đăng tối ưu, và theo dõi trạng thái công việc một cách chuyên nghiệp."
slug: "tu-dong-hoa-dang-video-instagram-linkedin-tiktok"
tags: [n8n, automation, social-media, google-sheets, upload-post]
keywords: [n8n workflow tự động hóa, đăng video tự động, Instagram LinkedIn TikTok, Google Sheets tự động hóa, tự động hóa mạng xã hội]
---

# 🚀 **Tự Động Hóa Đăng Video Trên Instagram, LinkedIn & TikTok - Không Cần Code!**

## **🔥 Nỗi Đau Của Các Sếp Trong Quá Trình Đăng Video**
Các sếp thường phải:
- **Lên lịch đăng video thủ công** trên từng nền tảng (Instagram, LinkedIn, TikTok) với thời gian khác nhau.
- **Quên hoặc đăng sai thời điểm**, khiến nội dung không đạt hiệu quả tối đa.
- **Phải theo dõi nhiều bảng Google Sheets** để quản lý trạng thái của từng video.
- **Tốn thời gian** lên đến **20h/tuần** chỉ để đăng video, thay vì tập trung vào nội dung chất lượng.

**Workflow này giải quyết tất cả!** Với **n8n**, các sếp có thể **tự động hóa toàn bộ quy trình**, chỉ cần **1 bảng Google Sheets** và **UploadPost API**, mà không cần viết một dòng code nào.

---
### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Đăng video chỉ với **1 nhấp chuột**, không cần làm thủ công.
- **Đăng đúng thời điểm**: Workflow kiểm tra và đăng video **chỉ khi thời gian phù hợp** (không đăng sai giờ).
- **Theo dõi trạng thái chuyên nghiệp**: Google Sheets tự động cập nhật trạng thái từ **"Đã sẵn sàng đăng"** → **"Đã đăng"** để tránh trùng lặp.
- **Báo cáo tức thời**: Nhận **tin nhắn Telegram** với kết quả đăng video trên tất cả nền tảng.
- **Hoạt động 24/7**: Workflow chạy tự động **2 lần/ngày** (9h sáng và 9h tối) theo múi giờ Chile (có thể điều chỉnh).
:::

---
## 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản n8n Self-hosted** (để workflow chạy 24/7 ổn định).
   👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
   👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)

2. **Tài khoản Google Sheets** với **bảng mẫu** (có thể sao chép từ [đây](https://docs.google.com/spreadsheets/d/1ZKbnD7GM6eAHKzyDY98cvz9jMUib1HLU7d9gohYkR3s/edit?usp=sharing)).
   - **Cột bắt buộc**:
     - `Title` (tiêu đề video)
     - `Copy` (mô tả/caption)
     - `Video Link` (đường dẫn video từ Google Drive)
     - `Status` (phải là **"Listo para postear"** để workflow xử lý)
     - `Fecha.Hora` (thời gian đăng, định dạng: `16 de Octubre a las 9 am` - có thể thay đổi sang tiếng Việt)
     - `row_number` (dùng để theo dõi)

3. **Tài khoản UploadPost API** (để đăng video lên Instagram, LinkedIn, TikTok).
   - [Đăng ký UploadPost](https://uploadpost.io/) và **cấu hình kết nối** với các tài khoản mạng xã hội.

4. **Tài khoản Telegram** (để nhận báo cáo kết quả).
   - Tạo **bot Telegram** và lấy **API Key** từ [@BotFather](https://t.me/BotFather).

5. **N8n Credentials**:
   - `googleSheetsOAuth2Api` (để kết nối với Google Sheets).
   - `telegramApi` (để gửi tin nhắn Telegram).
   - `uploadPostApi` (để đăng video lên các nền tảng).
:::

---
## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
Các sếp có thể **import workflow** từ file JSON hoặc **copy/paste JSON** vào **n8n Editor**:
1. Tải file JSON từ [đây](https://n8n.io/workflows/9786) (hoặc sao chép từ link gốc).
2. Trong **n8n Editor**, nhấn **Import Workflow** và chọn file JSON.
3. Hoặc **copy toàn bộ JSON** và dán vào **Import Workflow** từ menu.

---
### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**

#### **🔹 Node "Schedule Trigger" (Lên Lịch)**
- **Thời gian chạy**: Mặc định là **9h sáng và 9h tối** (múi giờ Chile: `America/Santiago`).
- **Cách thay đổi**:
  - Mở node **Schedule Trigger** → Chọn **Edit**.
  - Thay đổi **timezone** thành múi giờ của các sếp (ví dụ: `Asia/Ho_Chi_Minh` cho Việt Nam).
  - Thêm hoặc xóa thời gian đăng theo nhu cầu.

#### **🔹 Node "Google Sheets" (Lấy Dữ liệu)**
- **Credentials**: Chọn `googleSheetsOAuth2Api` (đã cấu hình trước).
- **Operation**: Đặt là **"Read"** (đọc dữ liệu).
- **Filter**: Workflow sẽ **lấy chỉ 1 bản ghi đầu tiên** có `Status = "Listo para postear"`.
- **Lưu ý**:
  - Nếu muốn **đăng nhiều video cùng lúc**, cần **sửa code** trong node **Code** (xem phần **Mẹo & Gợi Ý Nâng Cao**).

#### **🔹 Node "Code" (Định dạng thời gian)**
- **Mục đích**: Chuyển đổi **thời gian hiện tại** thành định dạng **tiếng Tây Ban Nha** (ví dụ: `"16 de Octubre a las 9 am"`).
- **Cách thay đổi sang tiếng Việt**:
  - Mở node **Code** → Chọn **Edit**.
  - Thay đổi **các biến** trong code để phù hợp với tiếng Việt:
    ```javascript
    const dayNames = ["Chủ nhật", "Thứ 2", "Thứ 3", "Thứ 4", "Thứ 5", "Thứ 6", "Thứ 7"];
    const monthNames = ["Tháng 1", "Tháng 2", "Tháng 3", "Tháng 4", "Tháng 5", "Tháng 6", "Tháng 7", "Tháng 8", "Tháng 9", "Tháng 10", "Tháng 11", "Tháng 12"];
    ```
  - **Kết quả**: Thời gian sẽ hiển thị như `"16 Tháng 10 lúc 9 giờ sáng"`.

#### **🔹 Node "If" (Kiểm tra thời gian)**
- **Mục đích**: So sánh **thời gian hiện tại** với **thời gian trong Google Sheets**.
- **Nếu trùng khớp**: Workflow tiếp tục đăng video.
- **Nếu không trùng khớp**: Workflow **dừng lại** (tránh đăng sai giờ).

#### **🔹 Node "Upload a video" (Đăng video)**
- **Credentials**: Chọn `uploadPostApi` (đã cấu hình trước).
- **Operation**: Đặt là **"uploadVideo"**.
- **Lưu ý**:
  - **Video phải ở định dạng MP4** và **được upload lên Google Drive**.
  - **Tên tài khoản** (Facebook ID, Pinterest Board ID,...) cần được điền chính xác trong node **"Social Media Account IDs"**.

#### **🔹 Node "Telegram" (Gửi báo cáo)**
- **Credentials**: Chọn `telegramApi`.
- **Message**: Workflow sẽ gửi **tin nhắn Telegram** với kết quả đăng video, bao gồm:
  - **Tên nền tảng** (Instagram, LinkedIn, TikTok).
  - **Link video** (clickable).
  - **Trạng thái thành công/thất bại**.

---
### **3. Kích Hoạt ⚡️**
1. **Test Run** (kiểm tra dữ liệu mẫu):
   - Nhấn **Run Workflow** và chọn **1 bản ghi** từ Google Sheets.
   - Kiểm tra **các node** có hoạt động đúng không (đặc biệt là **If** và **Upload a video**).
2. **Bật Active**:
   - Sau khi test thành công, **bật Active** cho workflow.

---
## ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[CẬP NHẬT & TỰ ĐỘNG HÓA NÂNG CAO]
1. **Đăng nhiều video cùng lúc**:
   - Mở node **Google Sheets** → Thay đổi **filter** để lấy **nhiều bản ghi** (ví dụ: `Status = "Listo para postear"`).
   - Sửa node **Code** để **lặp qua tất cả bản ghi** và đăng video.

2. **Thêm nền tảng khác**:
   - Workflow hiện hỗ trợ **Instagram, LinkedIn, TikTok**.
   - Nếu muốn thêm **Facebook, YouTube**, chỉ cần **cấu hình thêm tài khoản** trong **UploadPost API**.

3. **Lưu log hoạt động**:
   - Thêm node **Google Sheets (Update)** để **ghi lại lịch sử** của từng video (thời gian đăng, trạng thái, link).
   - Ví dụ:
     ```json
     {
       "action": "appendRow",
       "sheetName": "Log",
       "values": [
         $node["Google Sheets"].json["Fecha.Hora"],
         $node["Google Sheets"].json["Title"],
         "Đã đăng thành công",
         $node["Upload a video"].json["url"]
       ]
     }
     ```

4. **Gửi báo cáo định kỳ**:
   - Thêm node **Email** (n8n-nodes-base.email) để gửi **báo cáo tuần/Tháng** về hiệu quả đăng video.
   - Ví dụ:
     ```json
     {
       "to": "email@cua-ban.com",
       "subject": "Báo cáo đăng video tuần này",
       "html": "Tổng số video đăng: {{ $node["Google Sheets"].json.length }}"
     }
     ```

5. **Sử dụng AI để tự động tạo caption**:
   - Thêm node **LLM (n8n-nodes-base.llm)** để **tự động viết mô tả** cho video.
   - Ví dụ:
     ```json
     {
       "prompt": "Tạo một mô tả hấp dẫn cho video có tiêu đề: {{ $node["Google Sheets"].json["Title"] }}. Đảm bảo ngắn gọn và có từ khóa SEO."
     }
     ```
     - Sau đó, **ghi lại mô tả** vào Google Sheets trước khi đăng.
:::

---
## 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp để tập trung vào **nội dung chất lượng** thay vì làm thủ công. Với **n8n**, các sếp có thể:
✅ **Đăng video tự động** vào thời điểm tối ưu.
✅ **Theo dõi trạng thái** một cách chuyên nghiệp.
✅ **Nhận báo cáo tức thời** qua Telegram.
✅ **Hoạt động 24/7** mà không cần can thiệp.

**Hãy thử ngay!** Import workflow, cấu hình và **đăng video chỉ với 1 nhấp chuột** từ bây giờ!

---
### **🔗 Tài Liệu Tham Khảo**
- [UploadPost API](https://uploadpost.io/)
- [Google Sheets Mẫu](https://docs.google.com/spreadsheets/d/1ZKbnD7GM6eAHKzyDY98cvz9jMUib1HLU7d9gohYkR3s/edit?usp=sharing)
- [n8n Self-hosted](https://docs.n8n.io/hosting/self-hosting/)