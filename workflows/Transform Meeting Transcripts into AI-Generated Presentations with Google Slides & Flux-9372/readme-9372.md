---
title: "🚀 Tự động hóa chuyển đổi bản ghi cuộc họp thành slide trình chiếu AI với Google Slides & Flux"
description: "Hướng dẫn chi tiết cách tự động hóa chuyển đổi bản ghi cuộc họp thành slide trình chiếu chuyên nghiệp bằng công nghệ AI, tiết kiệm thời gian và nâng cao hiệu quả truyền thông"
slug: "tu-dong-hoa-chuyen-doi-ban-ghi-cuoc-hop-thanh-slide-trinh-chieu-ai"
tags: [n8n, automation, no-code, google-slides, ai-content-creation]
keywords: [n8n workflow, tự động hóa nội dung, tạo slide trình chiếu, AI tạo hình ảnh, google slides]
---

# 🚀 Tự động hóa chuyển đổi bản ghi cuộc họp thành slide trình chiếu AI với Google Slides & Flux

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

Các sếp thường phải đối mặt với tình trạng tốn thời gian và công sức lớn khi phải chuyển đổi thủ công bản ghi cuộc họp thành slide trình chiếu chuyên nghiệp. Quá trình này không chỉ mất thời gian mà còn dễ gây ra sai sót và không nhất quán. Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình từ bản ghi cuộc họp đến slide trình chiếu hoàn chỉnh chỉ trong vài phút, giúp tiết kiệm thời gian quý giá và nâng cao hiệu quả truyền thông.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Tự động hóa toàn bộ quy trình từ 30-60 phút xuống còn vài phút
- Tăng tính chuyên nghiệp: Tạo slide trình chiếu chuyên nghiệp với nội dung chính xác và hình ảnh phù hợp
- Tăng tính nhất quán: Đảm bảo nội dung và hình ảnh luôn đồng bộ và chuyên nghiệp
- Tăng hiệu quả truyền thông: Nâng cao khả năng thuyết phục của slide trình chiếu
- Tăng tính cá nhân hóa: Tạo slide trình chiếu phù hợp với từng khách hàng và tình huống cụ thể
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Workspace với quyền truy cập vào Google Slides, Google Docs, Google Sheets và Google Drive
- API key từ OpenRouter (để sử dụng mô hình nanobanana cho tạo hình ảnh)
- API key từ ImgBB (dịch vụ lưu trữ hình ảnh miễn phí)
- API key từ OpenAI (để sử dụng mô hình AI tạo văn bản)
- API key từ Google AI Studio (để sử dụng mô hình Gemini)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Để import workflow này vào n8n của bạn, các sếp có thể làm theo các bước sau:

1. Truy cập vào trang [n8n.io/workflows/9372](https://n8n.io/workflows/9372)
2. Nhấp vào nút "Download" để tải xuống file JSON của workflow
3. Trong n8n Editor, nhấp vào nút "Import" và chọn file JSON đã tải xuống
4. Hoàn tất quá trình import và kiểm tra các node trong workflow

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

- **On form submission**: Node này sẽ bắt đầu workflow khi có dữ liệu được gửi từ form. Các sếp cần đảm bảo rằng form đã được cấu hình đúng và các trường dữ liệu cần thiết đã được điền đầy đủ.
- **Create Presentation**: Node này sẽ tạo một slide trình chiếu mới từ một template đã được cấu hình trước. Các sếp cần thay thế ID của template trong URL POST bằng ID của template mà họ muốn sử dụng.
- **Append in Main Sheet, Append in Images Sheet, Append in Client Sheet**: Các node này sẽ lưu trữ thông tin về slide trình chiếu, hình ảnh và khách hàng vào Google Sheets. Các sếp cần cấu hình đúng ID của Google Sheets và tên của các sheet tương ứng.
- **OpenAI Chat Model, Google Gemini Chat Model**: Các node này sẽ sử dụng mô hình AI để tạo nội dung và hình ảnh cho slide trình chiếu. Các sếp cần cấu hình đúng API key và mô hình AI mà họ muốn sử dụng.
- **Get Pending Row, Get Transcript**: Các node này sẽ lấy thông tin về slide trình chiếu đang chờ xử lý và bản ghi cuộc họp từ Google Sheets và Google Docs. Các sếp cần cấu hình đúng ID của Google Sheets và Google Docs.
- **Generate Presentation Plan**: Node này sẽ tạo kế hoạch trình chiếu từ bản ghi cuộc họp. Các sếp cần đảm bảo rằng bản ghi cuộc họp đã được cấu trúc đúng và chứa thông tin cần thiết.
- **Update PPT Plan Doc, Create PPT Plan Doc**: Các node này sẽ cập nhật hoặc tạo tài liệu kế hoạch trình chiếu trong Google Docs. Các sếp cần cấu hình đúng ID của Google Docs.
- **Update row in Main Sheet + Trigger Image Gen**: Node này sẽ cập nhật thông tin về slide trình chiếu trong Google Sheets và kích hoạt quá trình tạo hình ảnh.
- **Get a document, Convert to File**: Các node này sẽ lấy tài liệu từ Google Docs và chuyển đổi nó thành định dạng có thể sử dụng được trong workflow.
- **Edit Fields**: Node này sẽ chỉnh sửa các trường dữ liệu trong workflow. Các sếp cần đảm bảo rằng các trường dữ liệu đã được cấu hình đúng.
- **HTTP Request**: Các node này sẽ gửi yêu cầu HTTP đến các dịch vụ khác nhau. Các sếp cần cấu hình đúng URL và tham số của yêu cầu.
- **Upload file**: Các node này sẽ tải lên các file vào Google Drive. Các sếp cần cấu hình đúng ID của Google Drive.
- **Structured Output Parser**: Node này sẽ phân tích cú pháp đầu ra có cấu trúc từ các mô hình AI. Các sếp cần đảm bảo rằng đầu ra của mô hình AI đã được cấu hình đúng.
- **Get row(s) in sheet, Update row in sheet**: Các node này sẽ lấy và cập nhật thông tin về các hàng trong Google Sheets. Các sếp cần cấu hình đúng ID của Google Sheets và tên của các sheet tương ứng.
- **Convert to File, Edit Fields, HTTP Request, Upload file**: Các node này sẽ chuyển đổi file, chỉnh sửa các trường dữ liệu, gửi yêu cầu HTTP và tải lên các file vào Google Drive. Các sếp cần cấu hình đúng các tham số của các node này.
- **Merge**: Node này sẽ hợp nhất các dữ liệu từ các node khác nhau trong workflow. Các sếp cần đảm bảo rằng các dữ liệu đã được cấu hình đúng.
- **Update row Presentation Details, Update row in Images Sheet**: Các node này sẽ cập nhật thông tin về slide trình chiếu và hình ảnh trong Google Sheets. Các sếp cần cấu hình đúng ID của Google Sheets và tên của các sheet tương ứng.
- **Get row(s) in sheet, Get a presentation, Get a document**: Các node này sẽ lấy thông tin về các hàng trong Google Sheets, slide trình chiếu và tài liệu từ Google Slides và Google Docs. Các sếp cần cấu hình đúng ID của Google Sheets, Google Slides và Google Docs.
- **OpenAI Chat Model, Code, Replace text in a presentation**: Các node này sẽ sử dụng mô hình AI để tạo nội dung và thay thế văn bản trong slide trình chiếu. Các sếp cần cấu hình đúng API key và mô hình AI mà họ muốn sử dụng.
- **Update row in sheet, Upload to Imgbb, Replace Image**: Các node này sẽ cập nhật thông tin về các hàng trong Google Sheets, tải lên hình ảnh vào ImgBB và thay thế hình ảnh trong slide trình chiếu. Các sếp cần cấu hình đúng ID của Google Sheets và API key của ImgBB.
- **Download file, Convert to Base64**: Các node này sẽ tải xuống các file từ Google Drive và chuyển đổi chúng thành định dạng base64. Các sếp cần cấu hình đúng ID của Google Drive.
- **Get row(s) in sheet, Get a presentation, Get a document**: Các node này sẽ lấy thông tin về các hàng trong Google Sheets, slide trình chiếu và tài liệu từ Google Slides và Google Docs. Các sếp cần cấu hình đúng ID của Google Sheets, Google Slides và Google Docs.
- **Update row in sheet, Merge**: Các node này sẽ cập nhật thông tin về các hàng trong Google Sheets và hợp nhất các dữ liệu từ các node khác nhau trong workflow. Các sếp cần cấu hình đúng ID của Google Sheets.
- **Wait**: Các node này sẽ tạm dừng workflow trong một khoảng thời gian nhất định. Các sếp cần cấu hình đúng thời gian chờ.
- **Final Text Content Formatting, Illustrations & Image Prompt Agent**: Các node này sẽ định dạng nội dung văn bản cuối cùng và tạo các gợi ý hình ảnh cho slide trình chiếu. Các sếp cần đảm bảo rằng các mô hình AI đã được cấu hình đúng.
- **Google Gemini Chat Model, OpenAI Chat Model**: Các node này sẽ sử dụng mô hình AI để tạo nội dung và hình ảnh cho slide trình chiếu. Các sếp cần cấu hình đúng API key và mô hình AI mà họ muốn sử dụng.

#### 3. Kích hoạt ⚡️
Sau khi đã cấu hình các node quan trọng trong workflow, các sếp có thể kích hoạt workflow bằng cách thực hiện các bước sau:

1. Trong n8n Editor, nhấp vào nút "Activate" để kích hoạt workflow
2. Kiểm tra các node trong workflow để đảm bảo rằng chúng đã được cấu hình đúng
3. Thực hiện một số dữ liệu mẫu để kiểm tra workflow
4. Kiểm tra kết quả của workflow để đảm bảo rằng nó hoạt động như mong đợi

### ✍️ Mẹo & gợi ý nâng cao
- **Tùy chỉnh template**: Các sếp có thể tùy chỉnh template slide trình chiếu để phù hợp với nhu cầu của mình.
- **Tùy chỉnh mô hình AI**: Các sếp có thể thay đổi mô hình AI được sử dụng trong workflow để phù hợp với nhu cầu của mình.
- **Tích hợp với các dịch vụ khác**: Các sếp có thể tích hợp workflow với các dịch vụ khác nhau để mở rộng tính năng của nó.
- **Tạo báo cáo tự động**: Các sếp có thể tạo báo cáo tự động từ dữ liệu được thu thập từ workflow để theo dõi hiệu suất của nó.

### 📌 Kết luận
Workflow này cung cấp một giải pháp tự động hóa toàn diện để chuyển đổi bản ghi cuộc họp thành slide trình chiếu chuyên nghiệp. Với workflow này, các sếp có thể tiết kiệm thời gian và công sức lớn, đồng thời nâng cao hiệu quả truyền thông và tăng tính chuyên nghiệp của slide trình chiếu. Các sếp nên đảm bảo rằng đã cấu hình đúng các node quan trọng trong workflow và kích hoạt nó để bắt đầu sử dụng.