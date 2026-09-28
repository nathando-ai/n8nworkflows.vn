---
title: "🚀 Tự động tạo CV và Thư xin việc (Cover Letter) chuẩn chỉnh từ link tuyển dụng với AI"
description: "Hướng dẫn xây dựng workflow n8n tự động trích xuất thông tin từ link tuyển dụng, kết hợp AI OpenRouter và Google Docs/Sheets để tạo CV và Cover Letter cá nhân hóa."
slug: "tu-dong-tao-cv-va-cover-letter-tu-link-tuyen-dung-n8n"
tags: [n8n, automation, ai, google-sheets, google-docs, openrouter, hr]
keywords: [n8n workflow, tao cv tu dong, cover letter automation, openrouter ai, google sheets n8n, quan ly tuyen dung no-code]
---

# 🚀 Tự động hóa quy trình viết CV và Cover Letter chuẩn chỉnh với n8n và AI

Việc ứng tuyển hàng loạt công việc thường khiến các sếp tốn rất nhiều thời gian để "đo ni đóng giày" lại chiếc CV và viết một bức Cover Letter sao cho khớp với mô tả công việc (Job Description). Nếu làm thủ công, các sếp sẽ cực kỳ mệt mỏi và dễ nhàm chán.

Workflow n8n này sinh ra để giải quyết trọn vẹn nỗi đau đó! Hệ thống sẽ tự động theo dõi danh sách link tuyển dụng trong Google Sheets, cào dữ liệu công việc, đọc CV gốc của các sếp từ ổ cứng, sau đó dùng AI siêu thông minh qua OpenRouter để viết lại CV lẫn Cover Letter cực kỳ chuẩn xác rồi lưu thẳng lên Google Docs và Google Sheets. Hoàn toàn tự động 100%!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Không còn phải ngồi sửa từng câu chữ trong CV hay nghĩ cách viết thư xin việc cho từng công ty.
- **Cá nhân hóa tối đa:** AI sẽ phân tích kỹ JD (Job Description) và kết hợp với kinh nghiệm thực tế của các sếp để tạo ra bộ hồ sơ ứng tuyển có tỷ lệ trúng tuyển cao.
- **Đồng bộ tập trung:** Mọi dữ liệu, link CV và Cover Letter mới đều được lưu trữ gọn gàng trên Google Docs và Google Sheets để dễ dàng theo dõi.
- **Hoạt động tự động 24/7:** Chỉ cần ném link tuyển dụng vào Sheet, việc còn lại cứ để n8n lo.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản n8n (Cloud hoặc Self-hosted).
- Tài khoản Google Cloud (để cấu hình Google Sheets OAuth2 và Google Docs OAuth2).
- Tài khoản [OpenRouter](https://openrouter.ai/) (để lấy API Key sử dụng các mô hình AI miễn phí hoặc trả phí).
- File CV gốc (định dạng PDF) lưu sẵn trên ổ cứng hoặc môi trường chạy n8n.
- Một Google Sheet quản lý danh sách Link tuyển dụng (Job IDs).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy toàn bộ mã JSON của workflow này và paste trực tiếp vào giao diện n8n Editor của mình, hoặc import file JSON thông qua menu tuỳ chọn.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống mượt mà trơn tru, các sếp nhớ cấu hình kỹ các node sau:
- **Trigger by google sheet (Webhook):** Cấu hình Webhook URL kết nối từ Google Apps Script của Google Sheet để khi có dòng mới được thêm, nó sẽ ping thẳng vào n8n.
- **Get data from google sheet & Get Web Data from Job Site:** Kết nối credentials `googleSheetsOAuth2Api` và `linkedInOAuth2Api` (hoặc cấu hình HTTP Request tương ứng với trang tuyển dụng các sếp hay dùng).
- **Free AI Model, Free AI Model1, Free AI Model2 (lmChatOpenRouter):** Điền `openRouterApi` credentials và chọn model mong muốn (mặc định đang dùng model miễn phí `openai/gpt-oss-120b:free`).
- **Read CV from Disk & Extract Data From CV:** Trỏ đường dẫn tới file CV gốc (định dạng PDF) của các sếp trên ổ cứng.
- **Write Cover Letter & Write CV (Google Docs):** Kết nối `googleDocsOAuth2Api` và cấu hình template Google Docs để AI đổ dữ liệu vào đúng chỗ.
- **Append Cover Letter in sheet & Append CV in sheet (Google Sheets):** Kết nối `googleSheetsOAuth2Api` để ghi nhận lại kết quả ra bảng quản lý.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (**Test Run**) bằng một dòng dữ liệu mẫu trong Google Sheets để kiểm tra toàn bộ luồng chạy từ cào dữ liệu đến tạo Docs.
- Bật công tắc **Active** để workflow chính thức trực chiến 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Nối thêm một node Telegram hoặc Slack vào cuối chuỗi để bot bắn tin nhắn báo về máy ngay khi CV và Cover Letter được tạo xong.
- **Nâng cấp AI:** Nếu các sếp muốn chất lượng văn phong sắc sảo hơn, có thể chuyển sang các model trả phí như `GPT-4o` hoặc `Claude 3.5 Sonnet` thông qua OpenRouter.
- **Tạo bảng Log lỗi:** Thêm nhánh `Error Trigger` để bắt các trường hợp link tuyển dụng bị lỗi hoặc hỏng, giúp dễ dàng kiểm tra lại.

### 📌 Kết luận
Với workflow tự động hóa này, việc apply công việc mơ ước nay đã nhanh gọn và chuyên nghiệp hơn bao giờ hết. Hãy thiết lập ngay hôm nay để tối ưu hóa hành trình sự nghiệp của các sếp!