---
title: "🚀 Tự động trích xuất bảng chấm công (Timesheet) với Mistral OCR và Gmail Human Verification"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa xử lý bảng chấm công từ Google Drive, sử dụng Mistral AI OCR và cơ chế phê duyệt qua Gmail một cách chuyên nghiệp."
slug: "trich-xuat-timesheet-mistral-ocr-gmail-n8n"
tags: [n8n, automation, no-code, mistral-ai, ocr, google-drive, gmail]
keywords: [n8n workflow, mistral ocr, trích xuất timesheet, tự động hóa chấm công, ai agent n8n, gmail human verification]
---

# 🚀 Tự động trích xuất bảng chấm công với Mistral OCR & Gmail Human Verification

Các sếp có đang đau đầu mỗi khi cuối tháng phải thu thập, đọc hiểu và nhập liệu hàng tá bảng chấm công (timesheet) từ nhân viên dưới dạng file PDF, hình ảnh hay Excel không? Quá trình thủ công này vừa tốn thời gian, dễ xảy ra sai sót lại vừa nhàm chán. 

Giải pháp là đây! Workflow n8n này sẽ tự động hóa toàn bộ quy trình: quét tệp từ **Google Drive**, sử dụng sức mạnh thị giác máy tính **Mistral OCR** để đọc dữ liệu, dùng **AI Agent** để làm sạch, sau đó gửi email xin phê duyệt qua **Gmail** trước khi lưu kết quả chính thức. Tất cả diễn ra tự động 100% không cần viết code phức tạp!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Tự động hóa hoàn toàn từ khâu đọc file, trích xuất dữ liệu tới tổng hợp báo cáo.
- **Độ chính xác cao:** Kết hợp Mistral OCR tiên tiến và AI Agent để làm sạch, chuẩn hóa định dạng dữ liệu đầu ra.
- **Kiểm soát chặt chẽ:** Tích hợp tính năng xác thực con người (`Send and Wait`) qua Gmail trước khi lưu dữ liệu vào hệ thống.
- **Vận hành linh hoạt:** Hỗ trợ đa định dạng tệp (PDF, hình ảnh, Excel) được lưu trữ sẵn trên Google Drive.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance** (Self-hosted hoặc Cloud).
- **Google Drive Account & Credentials** (OAuth2 API) để đọc/ghi file timesheet.
- **Mistral Cloud API Key** (Dùng cho Model Mistral Cloud Chat và các HTTP Request OCR).
- **Gmail Account & Credentials** (OAuth2) để gửi thông báo và nhận phản hồi xác thực.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow (hoặc tải file từ trang chủ n8n workflow ID `8767`), sau đó paste trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình chính xác các node quan trọng sau:
- **Search files and folders & Download File (Google Drive):** Kết nối tài khoản Google Drive của sếp và chỉ định thư mục chứa các bảng chấm công cần xử lý.
- **Mistral Cloud Chat Model2 & Mistral OCR nodes:** Nhập `Mistral Cloud API Key` của sếp. Đảm bảo model `mistral-small-latest` được chọn đúng ở phần cấu hình LLM.
- **AI Agent to clean and format extracted data:** Kiểm tra lại Prompt của AI Agent để đảm bảo nó trích xuất đúng các trường thông tin cần thiết từ bảng chấm công (như: Tên nhân viên, Số giờ làm việc, Ngày, Dự án...).
- **Send a message (Gmail):** Cấu hình credentials Gmail, thiết lập người nhận (nhân sự hoặc quản lý) để hệ thống gửi bảng tóm tắt dữ liệu chờ duyệt (`sendAndWait`).

#### 3. Kích hoạt ⚡️
- Nhấn **Test workflow** trên node `When clicking ‘Test workflow’` để chạy thử với một vài file mẫu trên Google Drive và kiểm tra kết quả trả về ở từng bước.
- Sau khi test thành công, bật nút **Active** để workflow tự động hoạt động theo lịch trình hoặc sự kiện mong muốn.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng lưu trữ:** Thay vì chỉ lưu lại trên Google Drive ở node `Upload file`, các sếp có thể kết nối thêm node Google Sheets để đồng bộ trực tiếp dữ liệu chấm công vào một bảng tính chung theo dõi hàng tháng.
- **Tích hợp kênh chat:** Kết hợp thêm node Telegram hoặc Slack để gửi thông báo ngay lập tức cho quản lý khi có bản timesheet mới cần phê duyệt.
- **Ghi log lỗi:** Thêm node Error Trigger để bắt các trường hợp file bị lỗi định dạng hoặc OCR không đọc được, tự động gửi cảnh báo về email cho kỹ thuật viên xử lý.

### 📌 Kết luận
Workflow **Extract Timesheet Data with Mistral OCR & Gmail Human Verification** là một giải pháp tự động hóa toàn diện giúp các doanh nghiệp tối ưu hóa quy trình hành chính nhân sự. Hãy triển khai ngay hôm nay để giải phóng thời gian cho đội ngũ của bạn!