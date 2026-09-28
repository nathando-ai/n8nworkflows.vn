---
title: "🚀 Tự động hóa tuyển dụng: Tóm tắt CV trong Slack với easybits Extractor"
description: "Giải pháp tự động hóa tuyển dụng 100% không cần code. Tóm tắt CV trong Slack chỉ trong vài giây, tiết kiệm thời gian và nâng cao hiệu quả tuyển dụng."
slug: "tu-dong-hoa-tuyen-dung-tom-tat-cv-slack"
tags: [n8n, automation, no-code, hr, ai]
keywords: [n8n workflow, tự động hóa tuyển dụng, tóm tắt cv, easybits, slack]
---

# 🚀 Tự động hóa tuyển dụng: Tóm tắt CV trong Slack với easybits Extractor

[Các sếp tuyển dụng] có biết không? Với mỗi ứng viên nộp CV, các sếp thường phải mất hàng giờ để đọc và phân tích từng hồ sơ. Đặc biệt khi nhận hàng loạt CV từ các kênh tuyển dụng khác nhau, việc này trở nên cực kỳ tốn thời gian và dễ gây lỗi.

Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình tóm tắt CV chỉ trong vài giây, ngay khi ứng viên upload CV lên Slack. Không cần phải đọc từng dòng, các sếp sẽ nhận được thông tin tóm tắt về ứng viên ngay trong kênh Slack, giúp tăng tốc quy trình tuyển dụng đáng kể.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tóm tắt CV chỉ trong vài giây thay vì phải đọc từng dòng.
- **Chính xác**: Sử dụng công nghệ AI của easybits để trích xuất thông tin chính xác từ CV.
- **Tích hợp liền mạch**: Tóm tắt CV được gửi ngay trong kênh Slack, giúp các sếp quản lý tuyển dụng hiệu quả hơn.
- **Tự động hóa hoàn toàn**: Không cần can thiệp thủ công, workflow hoạt động liên tục 24/7.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Slack với quyền quản trị để tạo ứng dụng bot.
- API key từ dịch vụ easybits Extractor (đăng ký tại [https://go.easybits.tech/cn](https://go.easybits.tech/cn)).
- Kênh Slack dành riêng cho việc nhận CV từ ứng viên.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Để import workflow này vào n8n của bạn, các sếp có thể làm theo các bước sau:

1. Truy cập vào trang workflow gốc tại [https://n8n.io/workflows/16098](https://n8n.io/workflows/16098).
2. Nhấp vào nút "Download" để tải file JSON của workflow.
3. Trong n8n Editor, nhấp vào nút "Import from File" và chọn file JSON vừa tải về.
4. Hoặc, các sếp có thể copy toàn bộ nội dung JSON từ trang workflow và paste vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này bao gồm các node quan trọng sau:

- **Watch Channel for Messages**: Node này lắng nghe các tin nhắn mới trong kênh Slack được cấu hình. Các sếp cần thay đổi tên kênh Slack trong node này để phù hợp với kênh nhận CV của công ty.

- **Guard: Ignore Self & No-File Filter**: Node này lọc bỏ các tin nhắn từ bot của chính nó và các tin nhắn không có file đính kèm. Các sếp cần thay đổi `UYOURBOTID` trong node này bằng ID của bot Slack của công ty. ID này có thể tìm thấy trong phần **Bot User** của ứng dụng Slack.

- **Guard: Supported MIME**: Node này chỉ cho phép các file có định dạng PDF, PNG hoặc JPG. Các sếp cần đảm bảo rằng các ứng viên gửi CV dưới các định dạng này.

- **Download File from Slack**: Node này tải file CV từ Slack. Các sếp cần cấu hình credential **Header Auth** với tên `Authorization` và giá trị `Bearer <your-bot-token>` để tải file thành công.

- **easybits: Extract CV Fields**: Node này sử dụng công nghệ AI của easybits để trích xuất thông tin từ CV. Các sếp cần cấu hình credential **easybits Extractor API** với API key đã đăng ký từ dịch vụ easybits.

- **Build Summary & Action Card**: Node này định dạng thông tin tóm tắt và tạo card hành động cho Slack. Các sếp có thể tùy chỉnh thông tin được hiển thị trong node này.

- **Post Summary to Thread**: Node này gửi thông tin tóm tắt CV vào luồng tin nhắn của ứng viên. Các sếp cần đảm bảo rằng bot có quyền gửi tin nhắn vào kênh Slack.

- **Post Action Card to Slack**: Node này gửi card hành động với các nút **💾 Save to Sheet** và **Dismiss**. Các sếp cần cấu hình credential **httpBearerAuth** và **httpHeaderAuth** để gửi card hành động thành công.

- **Reply: Unsupported File Type**: Node này gửi thông báo lỗi khi ứng viên gửi file không được hỗ trợ. Các sếp có thể tùy chỉnh thông báo lỗi trong node này.

#### 3. Kích hoạt ⚡️
Sau khi đã cấu hình các node quan trọng, các sếp cần thực hiện các bước sau để kích hoạt workflow:

1. **Test run dữ liệu mẫu**: Các sếp có thể thử chạy workflow với một file CV mẫu để đảm bảo rằng các node hoạt động đúng cách.
2. **Bật Active workflow**: Sau khi đã kiểm tra và đảm bảo rằng workflow hoạt động đúng, các sếp có thể bật workflow để hoạt động liên tục 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp với Google Sheets**: Các sếp có thể kết nối workflow với Google Sheets để lưu trữ thông tin ứng viên sau khi đã được tóm tắt. Điều này giúp các sếp quản lý danh sách ứng viên một cách hiệu quả hơn.
- **Gửi báo cáo định kỳ**: Các sếp có thể cấu hình workflow để gửi báo cáo định kỳ về số lượng ứng viên đã nhận và thông tin tóm tắt của họ qua email hoặc Slack.
- **Tích hợp với các công cụ khác**: Các sếp có thể kết nối workflow với các công cụ khác như LinkedIn, Indeed, hoặc các công cụ tuyển dụng khác để tự động hóa toàn bộ quy trình tuyển dụng.

### 📌 Kết luận
Workflow "Summarize candidate CVs in Slack with easybits Extractor" là giải pháp tự động hóa tuyển dụng hoàn hảo cho các sếp. Với workflow này, các sếp có thể tiết kiệm thời gian, nâng cao hiệu quả tuyển dụng và quản lý danh sách ứng viên một cách hiệu quả hơn. Hãy áp dụng ngay workflow này để tối ưu hóa quy trình tuyển dụng của công ty!