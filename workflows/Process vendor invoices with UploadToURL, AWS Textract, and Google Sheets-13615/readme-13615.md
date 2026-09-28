---
title: "💰 Tự Động Hóa Xử Lý Hóa Đơn Nhà Cung Cấp Với AWS Textract & Google Sheets (Không Cần Code)"
description: "Giải pháp tự động hóa hoàn toàn cho việc xử lý hóa đơn giấy/PDF sang Google Sheets, giảm 90% thời gian nhập liệu và loại bỏ sai sót do con người gây ra. Kết hợp UploadToURL, AWS Textract và Slack để báo cáo tự động."
slug: "tieu-dong-hoa-xu-ly-hoa-don-aws-textract-google-sheets"
tags: [n8n, automation, invoice processing, aws-textract, google-sheets, no-code, uploadtourl]
keywords: [tự động hóa hóa đơn, AWS Textract n8n, Google Sheets tự động, xử lý hóa đơn không code, UploadToURL, tự động hóa tài chính]
---

# 🚀 **Tự Động Hóa Xử Lý Hóa Đơn Nhà Cung Cấp Với AWS Textract & Google Sheets**

### **📌 Nỗi Đau Của Các Sếp**
Nhập liệu hóa đơn giấy hoặc PDF vào Google Sheets thủ công là một công việc **mệt mỏi, chậm chạp và dễ sai sót**. Mỗi hóa đơn mất từ **5-15 phút** để nhập, cộng dồn lên hàng trăm giờ/năm cho bộ phận tài chính. Kết quả? **Sai sót trong số tiền, ngày hạn thanh toán, hoặc mất hóa đơn** làm ảnh hưởng đến quyết định tài chính và mối quan hệ với nhà cung cấp.

**Giải pháp?** Một **workflow tự động hóa hoàn toàn** sử dụng:
✅ **UploadToURL** – Host hóa đơn từ URL hoặc file binary lên CDN.
✅ **AWS Textract** – Trích xuất dữ liệu (tên nhà cung cấp, số hóa đơn, số tiền, ngày hạn) từ hóa đơn giấy/PDF.
✅ **Google Sheets** – Lưu trữ và quản lý dữ liệu hóa đơn.
✅ **Slack** – Báo cáo tự động cho bộ phận tài chính.

---
### **🎯 Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian** nhập liệu (từ hàng giờ xuống chỉ vài giây/hoá đơn).
- **Giảm sai sót** đến 100% nhờ OCR (AWS Textract) và kiểm tra tự động.
- **Hoạt động 24/7** – Không cần can thiệp con người.
- **Báo cáo tự động** trên Slack với thông tin chi tiết và link truy cập.
- **Kiểm tra trùng lặp** – Ngăn chặn nhập liệu hóa đơn đã tồn tại.
:::

---
### **🔧 Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi chạy workflow, các sếp cần chuẩn bị:
1. **Tài khoản AWS** với quyền sử dụng **AWS Textract** (đăng ký [tại đây](https://aws.amazon.com/textract/)).
2. **Google Sheets** với:
   - **Bảng tính** có cột: `Invoice Number`, `Vendor`, `Amount`, `Currency`, `Due Date`, `Status`.
   - **ID Spreadsheet** (tham khảo [hướng dẫn lấy ID](https://support.google.com/docs/answer/1052019?hl=vi)).
3. **Tài khoản Slack** và **channel** dành cho bộ phận tài chính.
4. **API Key UploadToURL** (cài đặt [n8n-nodes-uploadtourl](https://github.com/n8n-community/n8n-nodes-uploadtourl)).
5. **Môi trường n8n** (self-hosted trên VPS để hoạt động 24/7).
:::

---
### **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/13615](https://n8n.io/workflows/13615) hoặc copy toàn bộ JSON từ link trên.
- Mở **n8n Editor** → Nhấn **Import Workflow** → Dán JSON và nhấn **Import**.

#### **2. Các Lưu Ý Bắt Buộc Phải Chỉnh 📌**
Workflows này gồm **18 node**, nhưng các bước sau đây là **quan trọng nhất** cần cấu hình chính xác:

##### **A. Cấu Hình Webhook (Nhận Hóa Đơn)**
- **Node:** `Webhook - Receive Invoice`
  - **Path:** `invoice-processing` (không đổi).
  - **HTTP Method:** `POST`.
  - **Test:** Gửi request từ Postman với payload:
    ```json
    {
      "fileUrl": "https://example.com/invoice.pdf",
      "fileBinary": "base64_encoded_pdf_data"  // hoặc bỏ nếu dùng URL
    }
    ```

##### **B. Cấu Hình UploadToURL (Host Hóa Đơn)**
- **Node:** `Upload to URL - Remote` và `Upload to URL - Binary`
  - **Operation:** `uploadFile`.
  - **Credentials:** Chọn **UploadToURL** đã cấu hình trước.
  - **Lưu ý:**
    - Nếu hóa đơn từ **URL**, chọn `Upload to URL - Remote`.
    - Nếu hóa đơn từ **file binary**, chọn `Upload to URL - Binary`.
  - **Output:** Node `Extract CDN URL` (Code) sẽ lấy URL CDN để AWS Textract xử lý.

##### **C. Cấu Hình AWS Textract (Trích Xuất Dữ Liệu)**
- **Node:** `AWS Textract - Analyse Expense`
  - **URL:** `https://textract.amazonaws.com/`.
  - **Headers:**
    ```json
    {
      "Authorization": "AWS4-HMAC-SHA256 Credential=AKIAXXXXXXXXXXXXXXXX/20231015/us-east-1/textract/aws4_request",
      "X-Amz-Target": "textract.AnalyzeExpenseV1"
    }
    ```
  - **Body:**
    ```json
    {
      "Document": {
        "S3Object": {
          "Bucket": "your-bucket-name",
          "Name": "path/to/invoice.pdf"
        }
      },
      "FeatureTypes": ["TABLES", "FORMS"]
    }
    ```
  - **Lưu ý:**
    - Thay thế `AKIAXXXXX` bằng **Access Key** của AWS.
    - **Bucket S3** phải được chia sẻ với AWS Textract (cấu hình IAM).

##### **D. Cấu Hình Google Sheets (Lưu Trữ & Kiểm Tra Trùng Lặp)**
- **Node:** `Sheets - Search for Duplicate`
  - **Credentials:** Chọn **Google Sheets** đã kết nối.
  - **Spreadsheet ID:** Điền `dXXXXXXXXXXXXXXXXXXXXXXXXXXXX`.
  - **Range:** `Sheet1!A2:F` (đảm bảo cột `Invoice Number` ở cột A).
- **Node:** `Sheets - Append New Invoice` và `Sheets - Update Incomplete Row`
  - **Operation:** `append` hoặc `update`.
  - **Range:** `Sheet1!A2:F` (đảm bảo cột phù hợp với dữ liệu trích xuất).

##### **E. Cấu Hình Slack (Báo Cáo Tự Động)**
- **Node:** `Slack - Notify Finance`
  - **Credentials:** Chọn **Slack** đã kết nối.
  - **Channel:** `#finance-invoices` (hoặc channel của bạn).
  - **Message Template:**
    ```json
    {
      "blocks": [
        {
          "type": "section",
          "text": {
            "type": "mrkdwn",
            "text": "*Invoice:* <{{$json["invoiceNumber"]}}|{{$json["invoiceNumber"]}}> *from:* <{{$json["vendor"]}}|{{$json["vendor"]}}>"
          }
        },
        {
          "type": "section",
          "text": {
            "type": "mrkdwn",
            "text": "*Amount:* ${{$json["amount"]}} *Currency:* {{$json["currency"]}} *Due Date:* {{$json["dueDate"]}}"
          }
        },
        {
          "type": "actions",
          "elements": [
            {
              "type": "button",
              "text": {
                "type": "plain_text",
                "text": "View Invoice"
              },
              "url": "{{$json["cdnUrl"]}}"
            }
          ]
        }
      ]
    }
    ```

##### **F. Cấu Hình Môi Trường (Variables)**
- **GSHEET_SPREADSHEET_ID:** `dXXXXXXXXXXXXXXXXXXXXXXXXXXXX`.
- **SLACK_FINANCE_CHANNEL:** `#finance-invoices`.

---
#### **3. Kích Hoạt ⚡️**
1. **Test Run** với một hóa đơn mẫu:
   - Gửi request POST đến `https://your-n8n-domain/webhook/invoice-processing` với payload:
     ```json
     {
       "fileUrl": "https://example.com/test-invoice.pdf"
     }
     ```
2. **Kiểm tra:**
   - AWS Textract có trích xuất dữ liệu không?
   - Google Sheets có cập nhật mới không?
   - Slack có thông báo không?
3. **Bật Active** workflow.

---
### **✍️ Mẹo & Gợi Ý Nâng Cao**
:::tip[CẬP NHẬT & TỰ ĐỘNG HÓA NÊN]
1. **Lưu Log Hóa Đơn:**
   - Thêm node `n8n-nodes-base.fileSystem` để lưu file PDF và kết quả trích xuất vào thư mục `./invoices/{{$json["invoiceNumber"]}}`.

2. **Gửi Báo Cáo Định Kỳ:**
   - Sử dụng **n8n-nodes-base.schedule** để gửi báo cáo tổng hợp hóa đơn hàng tháng qua Email (n8n-nodes-base.email) hoặc Slack.

3. **Kết Nối với ERP:**
   - Nếu sử dụng **Zoho Books, QuickBooks, hoặc SAP**, thêm node `n8n-nodes-zohoBooks` hoặc `n8n-nodes-quickbooks` để tự động nhập hóa đơn vào hệ thống tài chính.

4. **Xử Lý Hóa Đơn Nhiều Trang:**
   - Cấu hình AWS Textract với `FeatureTypes: ["TABLES", "FORMS", "LAYOUT"]` để trích xuất dữ liệu từ nhiều trang.

5. **Báo Lỗi Tự Động:**
   - Thêm node `n8n-nodes-base.email` để gửi Email cảnh báo khi AWS Textract không trích xuất được dữ liệu.
:::

---
### **📌 Kết Luận**
Workflow này **giải phóng bộ phận tài chính** khỏi công việc mệt mỏi nhập liệu, đồng thời **tăng độ chính xác và hiệu quả** của quá trình xử lý hóa đơn. **Chỉ cần 3 bước đơn giản:**
1. **Upload hóa đơn** (URL hoặc file).
2. **AWS Textract** tự động trích xuất dữ liệu.
3. **Google Sheets & Slack** cập nhật tự động.

**🚀 Hãy áp dụng ngay và tiết kiệm hàng giờ/năm cho doanh nghiệp!**
Nếu gặp vấn đề, **hãy comment bên dưới** hoặc liên hệ với [n8n Community](https://community.n8n.io/) để hỗ trợ.

---
:::note[CHÚ Ý]
- **Self-hosted n8n** là yêu cầu bắt buộc để workflow hoạt động 24/7.
- **AWS Textract** có giới hạn free tier (5.000 trang/tháng), các sếp nên lên plan phù hợp.
- **Google Sheets** cần quyền chỉnh sửa tự động (cấu hình [OAuth](https://developers.google.com/sheets/api/quickstart/python)).
:::

---
👉 **🎁 Đăng ký VPS TinoHost để self-host n8n (Mã giảm giá: VPSN8N)**
👉 [TinoHost - VPS 4GB Xeon chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)