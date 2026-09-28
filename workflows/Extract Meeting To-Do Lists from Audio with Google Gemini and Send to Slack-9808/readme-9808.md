---
title: "🚀 Tự động trích xuất biên bản & To-Do List từ file ghi âm cuộc họp bằng Google Gemini và Slack"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa quy trình nghe file ghi âm họp từ Google Drive, dùng AI Gemini chuyển đổi thành văn bản, trích xuất công việc và gửi thẳng vào Slack."
slug: "tu-dong-trich-xuat-to-do-list-tu-audio-gemini-slack"
tags: [n8n, automation, google-drive, google-gemini, slack, ai-workflow]
keywords: [n8n workflow, trích xuất to-do list từ audio, google gemini n8n, tự động hóa họp slack, google drive trigger n8n]
---

# 🚀 Tự động trích xuất biên bản & To-Do List từ file ghi âm cuộc họp bằng Google Gemini và Slack

Các sếp có thường xuyên tốn hàng giờ nghe lại các file ghi âm cuộc họp dài dằng dặc, sau đó hì hục gõ lại từng đầu việc (To-Do List) rồi phân công cho team không? Công việc thủ công này cực kỳ nhàm chán và rất dễ bỏ sót các action items quan trọng.

Giải pháp ở đây là gì? Workflow n8n này sẽ tự động hóa **100%** quy trình đó cho các sếp: Chỉ cần ném file ghi âm lên Google Drive, AI sẽ tự nghe, tự tóm tắt, trích xuất danh sách công việc và bắn thẳng vào kênh Slack của team. Không cần code, hoạt động mượt mà 24/7!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 mà không sợ sập nguồn hay mất kết nối, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không cần nghe lại băng ghi âm hay tự tổng hợp biên bản họp thủ công.
- **Không bỏ sót việc:** AI thông minh tự động bóc tách danh sách đầu việc (Task), người phụ trách (Assignee), hạn chót (Deadline) và mức độ ưu tiên (Priority).
- **Cập nhật tức thì:** Báo cáo được gửi thẳng vào Slack ngay khi file ghi âm được tải lên thư mục định sẵn.
- **Chuyên nghiệp hóa:** Quy trình làm việc của team trở nên minh bạch và tự động hóa hoàn toàn.
:::

### 📦 Các Nodes chính trong Workflow
Workflow bao gồm tổng cộng 7 nodes phối hợp nhịp nhàng với nhau:
1. **Looking for uploading file (`googleDriveTrigger`):** Theo dõi thư mục Google Drive, kích hoạt ngay khi có file ghi âm mới (MP3, M4A, WAV...).
2. **Download file (`googleDrive`):** Tải file ghi âm từ Google Drive về hệ thống n8n để xử lý.
3. **Get date & Format date (`dateTime`):** Lấy thời gian thực và định dạng lại để gắn timestamp cho báo cáo.
4. **Transcribe a recording1 (`googleGemini`):** Sử dụng sức mạnh AI của Google Gemini để chuyển đổi file âm thanh thành văn bản (Transcript).
5. **Analyze document (`googleGemini`):** Đọc bản transcript và dùng Prompt chuyên sâu để trích xuất các đầu việc ra định dạng JSON sạch sẽ.
6. **Send a message (`slack`):** Gửi bản danh sách To-Do List đã định dạng đến kênh Slack của team.

---

### 🔧 Yêu cầu cần thiết
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản và API Keys sau:
- **Tài khoản n8n** (Cloud hoặc Self-hosted trên VPS).
- **Google Drive Credentials** (OAuth2) để theo dõi và tải file.
- **Google Gemini / Google AI Studio API Key** (dùng cho 2 node AI xử lý audio và văn bản).
- **Slack App / Bot Token** có quyền gửi tin nhắn vào kênh (Channel) chỉ định.

---

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Copy mã JSON của workflow (hoặc tải file JSON từ nguồn gốc).
- Vào giao diện n8n Editor, chọn **Add workflow** -> Dán (Paste) trực tiếp vào canvas.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình chính xác các thông số sau để workflow không bị lỗi:

- **Node `Looking for uploading file` (Google Drive Trigger):**
  - Chọn Credentials Google Drive của sếp.
  - Chọn thư mục cụ thể trên Google Drive (Folder ID) nơi sếp sẽ upload các file ghi âm cuộc họp.
- **Node `Download file` (Google Drive):**
  - Chọn lại Credentials Google Drive tương ứng và ánh xạ file ID từ node Trigger.
- **Node `Transcribe a recording1` & `Analyze document` (Google Gemini):**
  - Kết nối tài khoản Google Gemini (Google Palm API Key).
  - Tại node phân tích tài liệu (`Analyze document`), kiểm tra kỹ Prompt để đảm bảo AI trả về kết quả đúng cấu trúc JSON mong muốn (Mô tả, Người phụ trách, Deadline, Mức độ ưu tiên).
- **Node `Send a message` (Slack):**
  - Cấu hình Slack OAuth2.
  - Chọn kênh Slack (Slack Channel) mà bot sẽ gửi thông báo To-Do List tới.

#### 3. Kích hoạt ⚡️
- Nhấn **Test step** hoặc **Execute Workflow** bằng cách upload thử một file ghi âm ngắn lên thư mục Google Drive đã chọn để kiểm tra dòng dữ liệu.
- Nếu mọi thứ chạy xanh mướt (success), hãy bật công tắc **Active** ở góc trên bên phải để workflow tự động chạy 24/7.

---

### ✍️ Mẹo & gợi ý nâng cao
Để hệ thống xịn xò hơn nữa, các sếp có thể mở rộng workflow với các ý tưởng sau:
- **Lưu trữ lịch sử:** Thêm node Google Sheets, Notion hoặc Airtable ngay sau node AI phân tích để lưu lại toàn bộ biên bản cuộc họp làm kho tri thức công ty.
- **Đa dạng hóa kênh thông báo:** Thay vì chỉ gửi Slack, có thể đồng thời bắn tin nhắn sang nhóm Telegram hoặc tạo task tự động trên Trello/Jira/Asana.
- **Tùy biến Prompt AI:** Yêu cầu Gemini viết thêm phần tóm tắt nội dung chính (Meeting Summary) bên cạnh danh sách To-Do List.

---

### 📌 Kết luận
Tự động hóa biên bản cuộc họp chưa bao giờ dễ dàng và tiết kiệm chi phí đến thế nhờ sự kết hợp giữa Google Drive, AI Gemini và n8n. Hãy thiết lập ngay hôm nay để giải phóng thời gian cho bản thân và giúp team làm việc năng suất hơn, các sếp nhé!