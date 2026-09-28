---
title: "🚀 Tự động trích xuất lịch học Đại học từ Excel sang Google Calendar bằng n8n & AI"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa việc đọc file Excel lịch học, dùng AI trích xuất sự kiện và tạo file ICS gửi qua Gmail để đồng bộ lịch cực nhanh."
slug: "tu-dong-trich-xuat-lich-hoc-dai-hoc-tu-excel-bang-ai"
tags: [n8n, automation, ai, google-gemini, cloudflare, gmail]
keywords: [n8n workflow, tự động hóa n8n, trích xuất excel bằng ai, cloudflare markdown conversion, tạo file ics tự động, n8n gemini]
---

# 🚀 Tự động trích xuất lịch học Đại học từ Excel sang Google Calendar bằng n8n & AI

Các sếp có bao giờ cảm thấy phát nản khi phải ngồi thủ công copy từng mốc thời gian, ngày khai giảng, ngày thi từ file Excel dài dằng dặc của trường đại học vào Google Calendar hay Outlook chưa? Việc này vừa tốn thời gian, vừa dễ bỏ sót hoặc nhập sai ngày tháng.

Đừng làm việc đó bằng tay nữa! Bài viết này sẽ hướng dẫn các sếp cách "lên đồ" một workflow n8n cực kỳ thông minh, kết hợp giữa **Cloudflare Markdown Conversion**, **Google Gemini AI** và **n8n Code Node** để tự động hóa 100% quy trình này: Tải file Excel -> Chuyển đổi sang Markdown -> AI trích xuất sự kiện chuẩn cấu trúc -> Tạo file lịch chuẩn `.ics` và gửi thẳng qua Gmail!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 99% thời gian:** Thay vì mất hàng giờ nhập liệu thủ công, AI xử lý và phân tích toàn bộ file Excel lịch học chỉ trong vài giây.
- **Độ chính xác cao:** Trí tuệ nhân tạo hiểu được cấu trúc phức tạp của bảng dữ liệu (bảng biểu, gộp ô, nhiều dữ liệu trên một hàng) để trích xuất sự kiện chính xác.
- **Tương thích mọi ứng dụng lịch:** Tự động tạo tệp định dạng `.ics` chuẩn mực để import trực tiếp vào iCal, Google Calendar hay Outlook.
- **Chia sẻ liền mạch:** Tự động đính kèm file lịch vào email và gửi ngay cho bạn bè, học sinh hoặc giảng viên chỉ với 1 click.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow này chạy mượt mà, các sếp cần chuẩn bị sẵn các tài nguyên sau:
- **n8n Instance** (Self-hosted hoặc Cloud).
- **Tài khoản Cloudflare:** Cần thiết cho dịch vụ *Cloudflare Markdown Conversion* (hiện tại đang miễn phí) để chuyển đổi file Excel sang dạng văn bản Markdown mà LLM đọc được.
- **Google Gemini API Key:** Dùng cho node *Google Gemini Chat Model* kết hợp với *Information Extractor* để bóc tách dữ liệu thông minh.
- **Tài khoản Gmail (hoặc kết nối OAuth2):** Dùng cho node *Send Email with Attachment* để gửi file ICS.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể sử dụng file JSON mẫu của workflow (ID template gốc: `3505`) và import trực tiếp vào giao diện n8n của mình bằng cách chọn **Add workflow** -> **Import from File** (hoặc paste trực tiếp mã JSON).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import thành công, các sếp cần cấu hình chính xác các thành phần sau trong workflow:
- **Node `Get Term Dates Excel` (HTTP Request):** Thay đổi URL trỏ tới file Excel (`.xlsx`) chứa lịch học của trường đại học mà các sếp muốn lấy.
- **Node `Markdown Conversion Service` (HTTP Request):** 
  - Cần cấu hình **Credentials** cho Cloudflare API.
  - Điền đúng `{ACCOUNT_ID}` của Cloudflare vào đường dẫn URL của node để dịch vụ có thể chuyển đổi file Excel thành bảng Markdown.
- **Node `Google Gemini Chat Model` & `Extract Key Events and Dates` (AI Nodes):** 
  - Chọn credentials `googlePalmApi` bằng API Key của Google Gemini.
  - Tinh chỉnh Schema trong *Information Extractor* nếu cấu trúc sự kiện của trường các sếp cần thêm các trường thông tin đặc thù (ví dụ: tên môn học, giảng đường, ghi chú...).
- **Node `Send Email with Attachment` (Gmail):** 
  - Kết nối tài khoản Gmail qua OAuth2.
  - Cập nhật địa chỉ email nhận file ICS (của bản thân, học sinh, hoặc đồng nghiệp).

#### 3. Kích hoạt ⚡️
- Bấm nút **"Test workflow"** (`When clicking ‘Test workflow’`) để chạy thử nghiệm và kiểm tra kỹ dữ liệu ở từng node (đặc biệt là khâu chuyển đổi Markdown và bóc tách sự kiện của AI).
- Sau khi kiểm tra mọi thứ hoạt động trơn tru, hãy bật công tắc **Active** ở góc trên cùng bên phải để workflow sẵn sàng hoạt động tự động.

---

### ✍️ Mẹo & gợi ý nâng cao
Để tối ưu hóa workflow này cho các nhu cầu thực tế phức tạp hơn, các sếp có thể tham khảo các ý tưởng mở rộng:
1. **Tích hợp Chatbot (Telegram/Slack):** Thay vì gửi email, hãy gửi thông báo trực tiếp qua Telegram hoặc Slack bot khi file lịch `.ics` đã sẵn sàng.
2. **Lưu trữ đám mây tự động:** Kết nối thêm node Google Drive hoặc OneDrive để tự động lưu file `.ics` vào thư mục chung của lớp học/nhóm làm việc.
3. **Trigger định kỳ (Cron node):** Thay vì dùng `Manual Trigger`, hãy thay bằng node `Schedule Trigger` chạy mỗi quý/mỗi học kỳ để tự động quét lịch học mới nhất từ website nhà trường.

### 📌 Kết luận
Việc ứng dụng AI và các công cụ chuyển đổi như Cloudflare Markdown Conversion vào n8n giúp giải quyết triệt để bài toán nhập liệu thủ công nhàm chán. Hãy áp dụng ngay workflow này để tối ưu hóa thời gian quản lý thời gian biểu cá nhân và đội ngũ của các sếp nhé! Chúc các sếp thao tác thành công!