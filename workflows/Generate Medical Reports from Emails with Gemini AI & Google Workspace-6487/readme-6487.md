---
title: "🚀 Tự động hóa tạo báo cáo y tế từ Email với Gemini AI & Google Workspace trong n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động đọc email từ bác sĩ, trích xuất dữ liệu bằng Gemini AI, cập nhật Google Sheets và tạo/gửi báo cáo PDF qua Gmail."
slug: "tu-dong-hoa-tao-bao-cao-y-te-tu-email-gemini-ai-google-workspace"
tags: [n8n, automation, no-code, google-workspace, gemini-ai, healthcare]
keywords: [n8n workflow, tự động hóa y tế, gemini ai, google docs, google sheets, gmail automation]
---

# 🚀 Tự động hóa tạo báo cáo y tế từ Email với Gemini AI & Google Workspace

Trong ngành y tế hoặc các phòng khám, việc tiếp nhận thông tin chẩn đoán từ email của bác sĩ và chuyển đổi chúng thành các báo cáo y tế định dạng chuẩn (PDF) thường tốn rất nhiều thời gian thủ công. Việc này không chỉ dễ xảy ra sai sót mà còn làm chậm quá trình trả kết quả cho bệnh nhân.

Workflow n8n này chính là giải pháp tự động hóa 100% không cần code (No-code), giúp các sếp xử lý toàn bộ quy trình: Tự động bắt email đến $\rightarrow$ Đọc và trích xuất dữ liệu bằng AI (Gemini) $\rightarrow$ Lưu log vào Google Sheets $\rightarrow$ Tạo file Google Docs theo mẫu $\rightarrow$ Xuất ra PDF và tự động gửi email trả kết quả.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Loại bỏ hoàn toàn thao tác copy-paste thủ công dữ liệu từ email sang file báo cáo.
- **Độ chính xác cao:** Ứng dụng sức mạnh của Gemini AI để trích xuất chính xác tên bệnh nhân, tên bác sĩ, chẩn đoán và phác đồ điều trị.
- **Đồng bộ toàn diện:** Tự động ghi nhận thông tin vào Google Sheets để quản lý và lưu trữ bản sao báo cáo trên Google Docs/Drive.
- **Hoạt động 24/7:** Tự động phản hồi và gửi báo cáo PDF hoàn chỉnh qua Gmail ngay khi có email mới từ bác sĩ gửi đến.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động trơn tru, các sếp cần chuẩn bị sẵn các tài nguyên sau:
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Tài khoản Google Workspace** kết nối với n8n (qua OAuth2) bao gồm:
  - Gmail (để nhận email đầu vào và gửi báo cáo đầu ra).
  - Google Sheets (để lưu dữ liệu bệnh nhân).
  - Google Docs (tạo sẵn một template báo cáo mẫu).
  - Google Drive (để lưu trữ và chuyển đổi file).
- **Google Gemini API Key** (Google Palm/Gemini API credentials) để AI xử lý ngôn ngữ tự nhiên.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow này và dán trực tiếp vào n8n Editor (hoặc Import file JSON thông qua giao diện n8n).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, các sếp cần cấu hình chính xác các node sau:

- **Gmail Trigger:** 
  - Chọn Credentials tài khoản Gmail của các sếp.
  - Cấu hình bộ lọc (Filters) để chỉ bắt email đến từ các bác sĩ hoặc có tiêu đề/nhãn (Label) phù hợp nhằm tránh xử lý nhầm email rác.
- **Edit Fields (Set) & Code / Code1:** 
  - Kiểm tra lại các trường dữ liệu (`content`) được trích xuất từ nội dung email thô để chuyển sang cho AI.
- **AI Agent & Google Gemini Chat Model:** 
  - Chọn Credentials cho `Google Gemini Chat Model` bằng Google Palm/Gemini API Key của các sếp.
  - Cấu hình prompt trong AI Agent yêu cầu trích xuất cấu trúc JSON rõ ràng (Tên bệnh nhân, Bác sĩ, Ngày khám, Chẩn đoán...).
- **Append row in sheet (Google Sheets):** 
  - Chọn Credentials Google Sheets.
  - Trỏ đến file Spreadsheet quản lý bệnh nhân và chọn đúng Sheet Name để lưu thông tin đã trích xuất từ AI.
- **Copy file (Google Drive) & Update a document1 (Google Docs):** 
  - Trỏ `Copy file` đến ID của file Google Docs Template mẫu.
  - Cấu hình node `Update a document1` để thay thế các placeholder (ví dụ: `{{PatientName}}`, `{{Diagnosis}}`...) bằng dữ liệu thực tế từ các bước trước.
- **HTTP Request & Send a message (Gmail):** 
  - Cấu hình node HTTP Request để tải file Google Doc dưới dạng PDF thông qua Google Drive API.
  - Cấu hình node `Send a message` để đính kèm file PDF vừa tạo và gửi email tự động về cho người nhận.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và gửi một email thử nghiệm (Test email) chứa thông tin bệnh án mẫu để kiểm tra toàn bộ luồng chạy.
- Sau khi test thành công không báo lỗi, các sếp bật công tắc **Active** ở góc trên cùng bên phải để workflow tự động hoạt động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo lỗi qua Telegram/Slack:** Thêm một nhánh Error Trigger để nếu AI hoặc Google Docs gặp lỗi, hệ thống sẽ bắn tin nhắn cảnh báo ngay vào nhóm chat nội bộ của phòng khám.
- **Lưu trữ file khoa học:** Tự động tạo thư mục trên Google Drive theo tên tháng/năm để lưu trữ các báo cáo PDF của bệnh nhân một cách ngăn nắp.
- **Xác thực dữ liệu (Human-in-the-loop):** Thêm node Wait trước khi gửi email, yêu cầu nhân viên y tế duyệt lại bản PDF trên Google Docs trước khi hệ thống tự động gửi đi.

### 📌 Kết luận
Workflow **Generate Medical Reports from Emails with Gemini AI & Google Workspace** là một "vũ khí" tối ưu hóa cực kỳ mạnh mẽ cho các cơ sở y tế hoặc các bộ phận cần tự động hóa quy trình xử lý văn bản từ email. Hãy triển khai ngay hôm nay để giải phóng sức lao động thủ công và nâng cao chất lượng dịch vụ của các sếp!