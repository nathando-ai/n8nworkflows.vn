---
title: "📄 **Tự Động Hóa Trích Xuất Văn Bản PDF từ WhatsApp bằng AWS Textract & S3 – Không Cần Code!**"
description: "Workflow tự động nhận PDF từ WhatsApp, trích xuất văn bản bằng AWS Textract, và lưu kết quả sạch sẽ vào S3 – giải pháp hoàn hảo cho doanh nghiệp cần xử lý tài liệu nhanh chóng và chính xác."
slug: "tu-dong-hoa-trich-xuat-pdf-whatsapp-aws-textract"
tags: [n8n, automation, aws-textract, whatsapp-business-api, document-processing, no-code]
keywords: [tự động hóa trích xuất PDF, AWS Textract n8n, WhatsApp API tự động hóa, xử lý tài liệu không code, lưu trữ S3 tự động]
---

# 🚀 **Tự Động Hóa Trích Xuất Văn Bản từ PDF qua WhatsApp bằng AWS Textract & S3**

## **🔍 Giới Thiệu: Nỗi Đau Của Doanh Nghiệp Khi Xử Lý Tài Liệu PDF**
Hàng ngày, các sếp phải nhận hàng chục, thậm chí hàng trăm tệp PDF từ khách hàng qua WhatsApp để xử lý: hợp đồng, hóa đơn, giấy tờ pháp lý... Việc **tải xuống, trích xuất văn bản thủ công** không chỉ tốn thời gian mà còn dễ gây lỗi do con người. **AWS Textract** là công cụ OCR (quét văn bản) mạnh mẽ của Amazon, nhưng phải kết hợp với **n8n** mới có thể tự động hóa toàn bộ quy trình từ nhận tin nhắn đến lưu kết quả sạch sẽ vào S3.

Workflow này **giải quyết hoàn toàn tự động** tất cả các bước:
✅ **Nhận PDF từ WhatsApp** (không cần cài app nào).
✅ **Tải lên S3** để AWS Textract xử lý.
✅ **Trích xuất văn bản chính xác** từ cả PDF scanned và digital.
✅ **Lưu kết quả sạch sẽ** vào S3 hoặc gửi tiếp cho AI phân tích.
✅ **Hoạt động 24/7** mà không cần can thiệp của con người.

---
### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**LỢI ÍCH CỐT LÕI**]
- **Tiết kiệm 10+ giờ/ngày** cho đội ngũ xử lý tài liệu.
- **Chính xác 100%** với công nghệ OCR tiên tiến của AWS Textract.
- **Tự động hóa hoàn toàn** – không cần can thiệp thủ công.
- **Kết nối với AI** (ví dụ: sử dụng LLM để tóm tắt văn bản trích xuất).
- **Lưu trữ an toàn** trên S3 với khả năng truy cập dễ dàng.
:::

---
### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản AWS** với quyền:
   - **S3**: Upload/Download file.
   - **Textract**: Thực hiện phân tích OCR.
   - **IAM Role** cho n8n có quyền truy cập AWS.
2. **API Key WhatsApp Business** (đăng ký tại [WhatsApp Cloud API](https://developers.facebook.com/docs/whatsapp/cloud-api/)).
3. **Bucket S3** để lưu tạm PDF và kết quả trích xuất.
4. **n8n Self-hosted** (không dùng phiên bản miễn phí để đảm bảo hoạt động 24/7).

:::info[**Gợi ý hạ tầng cho n8n**]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** – giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
## **🚀 Cách Import & Cấu Hình Workflow**

### **1. Import Workflow từ File JSON**
1. **Tải workflow** từ [n8n.io/workflows/13504](https://n8n.io/workflows/13504) hoặc sử dụng file JSON đã cung cấp.
2. **Mở n8n Editor** → Nhấn **"Import"** → Chọn file JSON.
3. **Hoặc copy/paste** JSON vào ô **"Import Workflow"** và nhấn **"Import"**.

### **2. Các Bước Cấu Hình Quan Trọng (BẮT BUỘC ĐIỀN)**
Workflow gồm **9 node**, nhưng các node sau cần **cấu hình kỹ lưỡng**:

#### **📌 Node 1: WhatsApp Trigger (n8n-nodes-base.whatsAppTrigger)**
- **Credentials**: Chọn **"whatsAppTriggerApi"** (đã cấu hình trước khi import).
- **Setup**:
  - **Phone Number**: Số điện thoại WhatsApp Business của doanh nghiệp.
  - **Webhook URL**: URL của n8n (ví dụ: `https://tên-domain-n8n.com/webhook/whatsAppTrigger`).

#### **📌 Node 2: File Download (n8n-nodes-base.httpRequest)**
- **Credentials**: Chọn **"whatsAppApi"**.
- **Setup**:
  - **Method**: `GET`.
  - **URL**: `$json["mediaUrl"]` (trích từ tin nhắn WhatsApp).
  - **Headers**:
    ```json
    {
      "Authorization": "Bearer YOUR_WHATSAPP_API_KEY"
    }
    ```
  - **Response Format**: Chọn **"Binary"** để tải file PDF nguyên vẹn.

#### **📌 Node 3: Upload File to S3 (n8n-nodes-base.awsS3)**
- **Credentials**: Chọn **"aws"** (cấu hình IAM Role cho n8n).
- **Setup**:
  - **Bucket Name**: Tên bucket S3 của bạn.
  - **Key**: `$node["File Download"].json["filename"]` (tên file PDF).
  - **Content Type**: `application/pdf`.
  - **Operation**: `upload`.

#### **📌 Node 4: AWS StartDocumentAnalysis (n8n-nodes-base.httpRequest)**
- **Credentials**: Chọn **"aws"** (AWS Access Key & Secret Key).
- **Setup**:
  - **Method**: `POST`.
  - **URL**: `https://textract.amazonaws.com/`
  - **Body (JSON)**:
    ```json
    {
      "Document": {
        "S3Object": {
          "Bucket": "$node["Upload File to S3"].json["bucket"]",
          "Name": "$node["Upload File to S3"].json["key"]"
        }
      },
      "NotifyChannel": {
        "SNSTopicArn": "YOUR_SNS_TOPIC_ARN"  // (Nếu muốn nhận thông báo khi xử lý xong)
      }
    }
    ```
  - **Headers**:
    ```json
    {
      "X-Amz-Target": "textract.StartDocumentAnalysis",
      "Content-Type": "application/x-amz-json-1.1"
    }
    ```

#### **📌 Node 5: Wait for Processing Time (n8n-nodes-base.wait)**
- **Setup**:
  - **Time**: `30000` (30 giây) – Thời gian chờ mặc định. **Cần điều chỉnh** tùy theo kích thước file (AWS Textract có thời gian xử lý khác nhau).

#### **📌 Node 6: AWS GetDocumentAnalysis (n8n-nodes-base.httpRequest)**
- **Credentials**: Chọn **"aws"**.
- **Setup**:
  - **Method**: `POST`.
  - **URL**: `https://textract.amazonaws.com/`
  - **Body (JSON)**:
    ```json
    {
      "JobId": "$node["AWS StartDocumentAnalysis"].json["JobId"]"
    }
    ```
  - **Headers**:
    ```json
    {
      "X-Amz-Target": "textract.GetDocumentAnalysis",
      "Content-Type": "application/x-amz-json-1.1"
    }
    ```

#### **📌 Node 7: Extract Text (n8n-nodes-base.code)**
- **Setup**:
  - **Code (JavaScript)**:
    ```javascript
    // Lấy dữ liệu từ AWS Textract và trích xuất văn bản
    const blocks = $input.all().map(item => item.json.Blocks).flat();
    const text = blocks
      .filter(block => block.BlockType === "LINE" && block.Text)
      .map(block => block.Text)
      .join("\n");

    return {
      json: {
        extractedText: text,
        originalFile: $input.all()[0].json["filename"]
      }
    };
    ```

#### **📌 Node 8 & 9 (Tùy Chọn): Lưu hoặc Gửi Kết Quả**
- **Lưu vào S3**: Sử dụng node `awsS3` với `operation: "upload"` để lưu văn bản trích xuất.
- **Gửi qua Email/Slack**: Kết nối với node `email` hoặc `slack` để thông báo kết quả.

---
### **3. Kích Hoạt Workflow**
1. **Test Run** với một file PDF mẫu:
   - Gửi PDF qua WhatsApp → Kiểm tra log trong n8n để xác nhận workflow chạy đúng.
2. **Bật Active**:
   - Nhấn **"Active"** trên tab **"Workflows"** trong n8n Editor.

---
## **✍️ Mẹo & Gợi Ý Nâng Cao**
1. **Kết nối với AI Tóm Tắt**:
   - Sau khi trích xuất văn bản, sử dụng **node `n8n-nodes-base.llm`** (OpenAI, Mistral) để tóm tắt nội dung.
2. **Lưu Log vào Database**:
   - Kết nối với **MySQL/PostgreSQL** để lưu lịch sử trích xuất.
3. **Gửi Kết Quả qua Email**:
   - Sử dụng node `n8n-nodes-base.email` để tự động gửi văn bản trích xuất cho khách hàng.
4. **Báo Cáo Định Kỳ**:
   - Sử dụng **node `n8n-nodes-base.cron`** để gửi báo cáo tổng hợp hàng tuần.

---
## **📌 Kết Luận: Tự Động Hóa PDF WhatsApp – Giải Pháp Hoàn Hảo Cho Doanh Nghiệp**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc nhàn tẻ, **tăng độ chính xác** với AWS Textract, và **mở rộng khả năng tự động hóa** với AI. **Không cần code**, chỉ cần cấu hình AWS và WhatsApp API là xong!

**Bắt đầu ngay**:
1. **Import workflow** từ [n8n.io/workflows/13504](https://n8n.io/workflows/13504).
2. **Cấu hình AWS & WhatsApp API** theo hướng dẫn trên.
3. **Test với file PDF mẫu** và **bật Active** để hoạt động 24/7.

**🚀 Hãy tự động hóa ngay hôm nay – không để tài liệu PDF làm chậm doanh nghiệp!**