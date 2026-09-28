---
title: "🚀 Tự động hóa tạo bản mô tả công việc (JD) từ Briefing Notes bằng OpenAI & Google Docs"
description: "Biến bản ghi chú phỏng vấn tuyển dụng trên Google Docs thành bản mô tả công việc (JD) hoàn chỉnh dưới dạng HTML và PDF, tích hợp AI Agent và quy trình phê duyệt qua Microsoft Teams."
slug: "tu-dong-hoa-tao-jd-tu-briefing-notes-openai-google-docs"
tags: [n8n, automation, ai-agent, openai, google-docs, microsoft-teams, hr-automation]
keywords: [n8n workflow, tạo JD tự động, AI HR automation, OpenAI GPT, Google Docs to PDF, Microsoft Teams approval]
---

# 🚀 Tự động hóa tạo bản mô tả công việc (JD) từ Briefing Notes bằng OpenAI & Google Docs

Các sếp làm trong ngành Nhân sự (HR) hay Tuyển dụng chắc hẳn đều quen thuộc với cảnh "đau đầu" mỗi khi nhận briefing từ Hiring Manager: ghi chú lộn xộn, mất thời gian cấu trúc lại ý chính, rồi lại loay hoay viết từng câu chữ cho bản Mô tả công việc (JD), sau đó lại xin sếp lớn duyệt đi duyệt lại. Quá trình này ngốn rất nhiều thời gian và công sức thủ công!

Đừng lo, workflow n8n này sẽ giải quyết trọn gói bài toán trên bằng cách tự động hóa **100% không cần code**: đọc bản ghi chú phỏng vấn trên Google Docs, dùng AI Agent trích xuất dữ liệu, tự động viết JD chuyên nghiệp, gửi qua Microsoft Teams để phê duyệt, và xuất ra file PDF lưu trữ gọn gàng.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted) do workflow này có sử dụng community node chuyển đổi PDF.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Biến ghi chú thô sơ thành bản JD chuẩn chỉnh chỉ trong vài phút.
- **AI thông minh & Chính xác:** Sử dụng OpenAI Agent để bóc tách dữ liệu (chức vụ, trách nhiệm, kỹ năng, quyền lợi...) thành JSON schema mạch lạc.
- **Human-in-the-loop chuyên nghiệp:** Gửi yêu cầu duyệt JD trực tiếp qua Microsoft Teams với nút bấm Phê duyệt/Từ chối trực quan.
- **Tự động hóa lưu trữ:** Tự động tạo thư mục theo mốc thời gian trên Google Drive, lưu trữ tài liệu gốc, log Google Sheets và xuất file PDF bản JD đã được duyệt.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản và API keys sau:
- **Tài khoản n8n** (bản Self-hosted để hỗ trợ community node).
- **Google Drive & Google Docs Credentials** (OAuth2).
- **Google Sheets** (tạo sẵn file bảng tính theo dõi dữ liệu tuyển dụng).
- **OpenAI API Key** (dành cho AI Agent trích xuất dữ liệu và viết JD).
- **Microsoft Teams Credentials** (OAuth2 để gửi thông báo chờ duyệt).
- **Community Node:** Cài đặt node `n8n-nodes-htmlcsstopdf` để chuyển đổi HTML sang PDF.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy toàn bộ mã JSON của workflow này, sau đó dán trực tiếp vào giao diện n8n Editor (hoặc import file JSON thông qua menu tuỳ chọn).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Google Drive Trigger:** Kết nối tài khoản Google Drive và chọn thư mục cần theo dõi (Watched Folder ID) nơi các Hiring Manager sẽ tải file ghi chú briefing lên.
- **Create timestamped subfolder & Move briefing doc:** Cấu hình thư mục gốc để hệ thống tự động tạo thư mục con kèm dấu thời gian nhằm quản lý tài liệu ngăn nắp.
- **Extract job data from transcript & JD-Writer (Agent):** Chọn credential OpenAI và kiểm tra lại model đang sử dụng (mặc định là `gpt-5.1` hoặc các dòng GPT-4o mới nhất).
- **Log job data in Google Sheets:** Trỏ tới file Google Sheets quản lý tuyển dụng của công ty và map đúng các cột dữ liệu (`job_title`, `department`, `responsibilities`,...).
- **Send JD to Teams for approval:** Kết nối tài khoản Microsoft Teams, thiết lập Chat ID hoặc Channel ID để gửi bản nháp JD kèm form phê duyệt (Approve/Reject).
- **Convert approved JD to PDF:** Đảm bảo community node `n8n-nodes-htmlcsstopdf` đã được cài đặt thành công trên hệ thống self-hosted của các sếp.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và tải lên một file Google Doc mẫu vào thư mục được theo dõi để test chạy thử.
- Sau khi kiểm tra toàn bộ luồng chạy mượt mà, các sếp gạt công tắc sang **Active** để bật chế độ tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thêm thông báo:** Có thể mở rộng kết nối thêm node Slack hoặc Telegram để thông báo ngay lập tức cho đội ngũ nhân sự khi có một JD mới được duyệt và xuất file PDF thành công.
- **Lưu log chi tiết:** Tích hợp thêm bước gửi email tổng kết hàng tuần về các vị trí tuyển dụng đã được xử lý qua Google Sheets.
- **Tinh chỉnh Prompt AI:** Các sếp có thể điều chỉnh system prompt trong OpenAI Agent để phong cách viết JD phù hợp với văn hóa riêng của công ty (trang trọng, trẻ trung, sáng tạo...).

### 📌 Kết luận
Với workflow tự động hóa này, quy trình tuyển dụng từ khâu nhận briefing đến khi ra mắt bản JD hoàn chỉnh sẽ trở nên chuyên nghiệp, nhanh chóng và loại bỏ hoàn toàn các bước thủ công nhàm chán. Hãy cài đặt ngay hôm nay để tối ưu hóa hiệu suất cho đội ngũ HR của các sếp nhé!