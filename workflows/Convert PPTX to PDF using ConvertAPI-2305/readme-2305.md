---
title: "📄 Tự Động Chuyển File PPTX Sang PDF Trong 1 Click Với n8n & ConvertAPI"
description: "Hướng dẫn chi tiết cách xây dựng workflow n8n để tự động tải và chuyển đổi file PowerPoint (PPTX) sang định dạng PDF chuyên nghiệp, không cần code."
slug: "chuyen-pptx-sang-pdf-n8n-convertapi"
tags: [n8n, automation, no-code, convertapi, file-conversion, pdf]
keywords: [n8n workflow, chuyển đổi file, pptx to pdf, tự động hóa văn bản, convertapi n8n]
---

# 📄 Tự Động Chuyển File PPTX Sang PDF Trong 1 Click Với n8n & ConvertAPI

Trong môi trường làm việc hiện đại, việc chuyển đổi định dạng file là một thao tác cực kỳ phổ biến nhưng lại tốn thời gian và dễ gây lỗi nếu làm thủ công. Đặc biệt, khi bạn cần gửi báo cáo, slide thuyết trình cho đối tác hoặc khách hàng, việc đảm bảo file PDF hiển thị đúng font chữ, layout và chất lượng là điều bắt buộc.

Làm thủ công bằng cách mở PowerPoint, Save As PDF, rồi gửi đi lặp đi lặp lại hàng chục lần mỗi ngày? Đó là sự lãng phí năng lượng sáng tạo. Workflow n8n dưới đây sẽ giúp các sếp **tự động hóa 100%** quy trình này: chỉ cần có link file PPTX, hệ thống sẽ tự động tải về, chuyển đổi sang PDF thông qua dịch vụ ConvertAPI và lưu trữ kết quả. Không cần cài đặt phần mềm nặng, không cần lo lắng về tương thích hệ điều hành, tất cả đều diễn ra mượt mà trên nền tảng n8n.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, đặc biệt khi xử lý file dung lượng lớn, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian tuyệt đối:** Loại bỏ hoàn toàn thao tác thủ công, chuyển đổi hàng loạt file chỉ trong vài giây.
- **Độ chính xác cao:** Sử dụng ConvertAPI - dịch vụ chuyển đổi file hàng đầu, đảm bảo layout PDF giống hệt file gốc, không bị lỗi font hay vỡ hình.
- **Tích hợp linh hoạt:** Dễ dàng kết nối với Email, Slack, hoặc Google Drive để tự động gửi file PDF sau khi chuyển đổi xong.
- **Vận hành liên tục:** Workflow hoạt động 24/7, sẵn sàng xử lý yêu cầu bất kể giờ nào.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản n8n:** Đã cài đặt và chạy n8n (Cloud hoặc Self-hosted).
2. **Tài khoản ConvertAPI:** Đăng ký tại [ConvertAPI](https://www.convertapi.com/a/signin) để lấy **Secret Key** (Authentication Secret).
   - *Lưu ý:* ConvertAPI có gói miễn phí với hạn mức nhất định, phù hợp để test.
3. **Link file PPTX:** Một URL công khai (Public URL) trỏ đến file PowerPoint cần chuyển đổi.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Mở n8n Editor của bạn.
2. Chọn **Import from URL** và dán link workflow gốc: `https://n8n.io/workflows/2305` HOẶC copy toàn bộ JSON của workflow và dán vào n8n.
3. Sau khi import, các sếp sẽ thấy 4 nodes chính được kết nối sẵn.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Đây là phần quan trọng nhất. Các sếp cần cấu hình lại các node sau để workflow chạy đúng với dữ liệu của mình:

**Node 1: `Download PPTX File` (HTTP Request)**
- **URL:** Thay thế URL mẫu bằng **link thực tế** trỏ đến file PPTX cần chuyển đổi.
- **Options:** Đảm bảo option `Response Format` được đặt là `File` (hoặc Binary) để n8n có thể xử lý dữ liệu nhị phân của file.

**Node 2: `File conversion to PDF` (HTTP Request)**
- **Credentials:** Chọn hoặc tạo mới credentials loại **Query Auth** (hoặc Header Auth tùy cấu hình ConvertAPI, nhưng workflow gốc dùng Query Auth).
  - *Cách tạo:* Vào Credentials > Add New Credential > Query Auth.
  - Điền **Key:** `secret`
  - Điền **Value:** [Secret Key của bạn từ ConvertAPI]
- **URL:** Giữ nguyên URL API của ConvertAPI (thường là `https://v2.convertapi.com/convert/pptx/to/pdf`).
- **Body:** Đảm bảo tham số `File` được map từ output của node `Download PPTX File`.

**Node 3: `Write Result File to Disk` (Read/Write File)**
- **Operation:** Chọn `Write`.
- **File Path:** Chỉ định đường dẫn thư mục trên máy chủ n8n nơi bạn muốn lưu file PDF sau khi chuyển đổi (ví dụ: `/data/converted_pdfs/result.pdf`).
- **Data:** Map dữ liệu binary từ node `File conversion to PDF`.

:::note[Lưu ý quan trọng về ConvertAPI]
ConvertAPI yêu cầu xác thực cho mọi yêu cầu chuyển đổi. Nếu các sếp chưa có tài khoản, hãy đăng ký miễn phí ngay. Secret Key là chìa khóa để workflow "nói chuyện" với API của họ. Đừng chia sẻ key này cho người khác.
:::

#### 3. Kích hoạt ⚡️
1. **Test Run:** Nhấn nút **Test workflow**.
   - Kiểm tra xem node `Download PPTX File` có tải được file không (kích thước file > 0).
   - Kiểm tra node `File conversion to PDF` có trả về mã 200 OK và dữ liệu binary không.
   - Kiểm tra file PDF có xuất hiện đúng thư mục đã chỉ định trong Node 3 không.
2. **Active Workflow:** Nếu test thành công, bật công tắc **Active** ở góc trên bên phải để workflow sẵn sàng nhận dữ liệu từ các nguồn khác (Webhook, Cron, v.v.).

### ✍️ Mẹo & gợi ý nâng cao
- **Tự động gửi Email:** Thêm node **Gmail** hoặc **SMTP** sau node `Write Result File to Disk` để tự động đính kèm file PDF vừa tạo và gửi cho khách hàng hoặc đồng nghiệp.
- **Lưu lên Cloud:** Thay vì lưu vào disk, các sếp có thể thay node `Read/Write File` bằng node **Google Drive** hoặc **AWS S3** để lưu trữ file PDF trực tiếp lên cloud, dễ dàng chia sẻ link.
- **Xử lý hàng loạt:** Thay đổi trigger từ Manual sang **Cron** hoặc **Webhook** để nhận danh sách link PPTX từ Google Sheets và xử lý hàng loạt file mỗi ngày.
- **Báo cáo lỗi:** Thêm node **Slack** hoặc **Telegram** để gửi thông báo ngay lập tức nếu quá trình chuyển đổi thất bại (ví dụ: file hỏng, hết hạn mức ConvertAPI).

### 📌 Kết luận
Việc chuyển đổi PPTX sang PDF tưởng chừng đơn giản nhưng khi đặt trong quy trình làm việc tự động hóa, nó trở thành một mắt xích quan trọng giúp tăng hiệu suất và độ chuyên nghiệp. Với workflow n8n kết hợp ConvertAPI này, các sếp có thể loại bỏ hoàn toàn công việc lặp lại, tập trung vào những giá trị cốt lõi hơn. Hãy import, cấu hình Secret Key và bắt đầu trải nghiệm sự mượt mà của tự động hóa ngay hôm nay!