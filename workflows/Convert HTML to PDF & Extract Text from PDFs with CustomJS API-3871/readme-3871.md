---
title: "📄 Tự Động Hóa HTML to PDF & Trích Xuất Text với CustomJS API trên n8n"
description: "Hướng dẫn chi tiết cách chuyển đổi HTML sang PDF và trích xuất văn bản từ PDF một cách tự động, chính xác và không cần code nhờ CustomJS API trên n8n."
slug: "html-to-pdf-extract-text-customjs-n8n"
tags: [n8n, automation, no-code, pdf-processing, customjs]
keywords: [n8n workflow, tự động hóa PDF, html to pdf, trích xuất text, customjs api]
---

# 📄 Tự Động Hóa HTML to PDF & Trích Xuất Text với CustomJS API trên n8n

Trong môi trường doanh nghiệp hiện đại, việc xử lý tài liệu PDF là một phần không thể thiếu. Tuy nhiên, quy trình thủ công thường gặp nhiều "nỗi đau" khó chịu:
*   **Chuyển đổi HTML sang PDF:** Muốn tạo báo cáo đẹp mắt từ template HTML nhưng phải mở trình duyệt, in ra PDF thủ công, mất thời gian và dễ sai lệch định dạng.
*   **Trích xuất dữ liệu từ PDF:** Cần lấy nội dung văn bản từ hàng trăm file PDF để nhập vào cơ sở dữ liệu hoặc phân tích bằng AI, nhưng làm thủ công thì cực kỳ chậm và dễ sai sót.

Workflow **Convert HTML to PDF & Extract Text from PDFs with CustomJS API** chính là giải pháp "chữa cháy" hoàn hảo. Nó giúp các sếp tự động hóa 100% quy trình này trên nền tảng n8n, không cần viết một dòng code phức tạp nào, chỉ cần kết nối API là xong.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 và xử lý lượng lớn file PDF/HTML mà không lo bị gián đoạn, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian tối đa:** Tự động chuyển đổi hàng loạt HTML thành PDF chuyên nghiệp và trích xuất text tức thì.
- **Độ chính xác cao:** Loại bỏ hoàn toàn lỗi con người khi copy-paste hoặc in ấn thủ công.
- **Tích hợp linh hoạt:** Kết quả (file PDF hoặc text) có thể dễ dàng đẩy sang các hệ thống khác như Email, Google Drive, hoặc các mô hình AI.
- **Không cần code:** Chỉ cần cấu hình API Key là vận hành, phù hợp cho cả người không biết lập trình.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1.  **Tài khoản n8n:** Cloud hoặc Self-hosted.
2.  **Tài khoản CustomJS:** Đăng ký tại [CustomJS](https://customjs.com/) để lấy API Key.
3.  **Node CustomJS PDF Toolkit:** Cài đặt node cộng đồng `@custom-js/n8n-nodes-pdf-toolkit` vào n8n (nếu chưa có).
4.  **Dữ liệu đầu vào:**
    *   Chuỗi HTML hoặc URL trỏ đến trang HTML.
    *   File PDF hoặc URL trỏ đến file PDF cần trích xuất.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1.  Mở n8n Editor.
2.  Chọn **Import from URL** hoặc **Import from File** (nếu đã tải JSON).
3.  Dán link workflow gốc: `https://n8n.io/workflows/3871` hoặc chọn file JSON đã tải về.
4.  Workflow sẽ hiển thị với 5 nodes chính:
    *   `When clicking ‘Test workflow’` (Manual Trigger)
    *   `Code` (Xử lý dữ liệu trung gian)
    *   `HTML to PDF` (Chuyển đổi HTML sang PDF)
    *   `Convert PDF into Text` (Trích xuất text từ PDF - dạng file)
    *   `Convert PDF into Text1` (Trích xuất text từ PDF - dạng URL)

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

**Bước 1: Cấu hình Credentials CustomJS**
*   Click vào node `HTML to PDF` (hoặc bất kỳ node nào dùng CustomJS).
*   Chọn **CustomJS API** trong phần Credentials.
*   Nếu chưa có, tạo mới bằng cách nhập **API Key** lấy từ tài khoản CustomJS của các sếp.
*   *Lưu ý:* Đảm bảo API Key có quyền sử dụng các dịch vụ `html2pdf` và `pdftotext`.

**Bước 2: Cấu hình Node `Code` (Xử lý dữ liệu đầu vào)**
*   Node này đóng vai trò chuẩn bị dữ liệu cho các bước tiếp theo.
*   Các sếp cần chỉnh sửa mã JS trong node này để:
    *   **Cho luồng HTML to PDF:** Cung cấp chuỗi HTML hoặc URL. Ví dụ:
        ```javascript
        return [{
          json: {
            html: "<h1>Xin chào</h1><p>Nội dung báo cáo</p>",
            // hoặc url: "https://example.com/report.html"
          }
        }];
        ```
    *   **Cho luồng PDF to Text:** Cung cấp file PDF (base64) hoặc URL. Ví dụ:
        ```javascript
        return [{
          json: {
            // Nếu dùng URL:
            url: "https://example.com/document.pdf"
            // Hoặc nếu dùng file base64, cần cấu hình thêm trong node CustomJS
          }
        }];
        ```

**Bước 3: Cấu hình Node `HTML to PDF`**
*   Chọn **Resource**: `html2pdf`.
*   Chọn **Operation**: `Convert`.
*   **Input Data**: Chọn trường `html` hoặc `url` từ output của node `Code`.
*   **Output Format**: Chọn `pdf`.
*   **Filename**: Đặt tên file PDF (ví dụ: `bao-cao.pdf`).

**Bước 4: Cấu hình Node `Convert PDF into Text`**
*   Có 2 node trích xuất text, các sếp chọn 1 trong 2 tùy theo nguồn dữ liệu:
    *   **Node `Convert PDF into Text`**: Dùng khi đầu vào là **file PDF** (base64 hoặc binary).
    *   **Node `Convert PDF into Text1`**: Dùng khi đầu vào là **URL** trỏ đến file PDF.
*   Chọn **Resource**: `pdftotext`.
*   Chọn **Operation**: `Extract Text`.
*   **Input Data**: Kết nối với output của node `Code` (trường `url` hoặc `file`).

**Bước 5: Kiểm tra kết quả**
*   Output của các node CustomJS sẽ trả về:
    *   **HTML to PDF**: File PDF binary hoặc URL tải xuống.
    *   **PDF to Text**: Chuỗi văn bản trích xuất được.
*   Các sếp có thể thêm node `Debug` hoặc `Set` để xem trước kết quả.

#### 3. Kích hoạt ⚡️
1.  **Test Run:** Click nút **Test workflow** để chạy thử với dữ liệu mẫu.
2.  Kiểm tra output:
    *   File PDF có đúng định dạng không?
    *   Text trích xuất có đầy đủ và chính xác không?
3.  Nếu ổn, click **Active** để bật workflow.
4.  Thay thế `Manual Trigger` bằng trigger thực tế (ví dụ: `Webhook`, `Cron`, `Google Sheets Trigger`) để tự động hóa hoàn toàn.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp với Email:** Sau khi tạo PDF, dùng node `Gmail` hoặc `SMTP` để gửi báo cáo tự động cho khách hàng.
- **Lưu trữ trên Cloud:** Dùng node `Google Drive` hoặc `AWS S3` để lưu trữ file PDF và text trích xuất, tạo hồ sơ số hóa.
- **Phân tích bằng AI:** Đẩy text trích xuất từ PDF vào node `OpenAI` hoặc `Claude` để tóm tắt, phân tích cảm xúc, hoặc trả lời câu hỏi từ tài liệu.
- **Xử lý hàng loạt:** Kết hợp với `Google Sheets` để đọc danh sách URL HTML hoặc PDF, sau đó chạy vòng lặp (Loop) để xử lý từng file một cách tự động.

### 📌 Kết luận
Workflow **Convert HTML to PDF & Extract Text from PDFs with CustomJS API** là công cụ mạnh mẽ giúp các sếp tự động hóa quy trình xử lý tài liệu, tiết kiệm hàng giờ làm việc thủ công mỗi tuần. Với khả năng chuyển đổi HTML sang PDF chuyên nghiệp và trích xuất text chính xác, workflow này có thể tích hợp vào nhiều quy trình nghiệp vụ khác nhau, từ tạo báo cáo, số hóa tài liệu, đến phân tích dữ liệu bằng AI.

Hãy thử ngay hôm nay và trải nghiệm sự khác biệt mà tự động hóa mang lại! 🚀