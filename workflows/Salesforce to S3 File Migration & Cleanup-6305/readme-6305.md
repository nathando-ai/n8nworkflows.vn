---
title: "🚀 Tự Động Hóa Di Chuyển & Xóa File Từ Salesforce Sang S3: Giảm 90% Thời Gian Quản Lý File"
description: "Workflow tự động hóa hoàn toàn không cần code để di chuyển tất cả file từ Salesforce sang AWS S3, đồng thời tự động xóa file cũ hơn 1 năm trong Salesforce. Giúp doanh nghiệp tiết kiệm không gian lưu trữ, giảm rủi ro mất mát và tối ưu hóa hiệu suất CRM."
slug: "tieu-dong-hoa-di-chuyen-file-salesforce-sang-s3"
tags: [n8n, automation, salesforce, aws-s3, file-management, crm-integration]
keywords: [tự động hóa salesforce, di chuyển file salesforce sang s3, xóa file cũ salesforce, lưu trữ file cloud, n8n workflow salesforce, tối ưu hóa crm]
---

# 🚀 **Tự Động Hóa Di Chuyển File Từ Salesforce Sang S3: Giải Pháp Tiết Kiệm Không Gian & Giảm Rủi Ro**

### **Nỗi Đau Của Các Sếp Trong Quản Lý File Salesforce**
Hàng ngày, các sếp phải đối mặt với những vấn đề phiền phức khi quản lý file trong Salesforce:
- **Không gian lưu trữ Salesforce bị tràn**: File cũ, tạm thời hoặc không cần thiết chiếm dụng dung lượng, làm chậm hệ thống và tăng chi phí.
- **Rủi ro mất mát dữ liệu**: Khi xóa file thủ công, có thể vô tình xóa sai hoặc quên xóa file quan trọng.
- **Tốn thời gian thủ công**: Di chuyển hàng ngàn file từ Salesforce sang cloud storage như S3 là công việc mệt mỏi, dễ sai sót và không thể thực hiện liên tục 24/7.
- **Không có báo cáo tự động**: Không biết được tiến độ di chuyển hoặc thông báo khi có lỗi xảy ra.

**Workflow này giải quyết tất cả những vấn đề trên bằng cách:**
✅ **Tự động di chuyển tất cả file từ Salesforce sang S3** (không giới hạn dung lượng).
✅ **Xóa tự động file cũ hơn 365 ngày** trong Salesforce, giải phóng không gian.
✅ **Báo cáo ngay lập tức trên Slack** khi có lỗi hoặc hoàn thành.
✅ **Hoạt động liên tục 24/7** mà không cần can thiệp thủ công.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian** quản lý file: Không cần phải copy/paste hoặc sử dụng công cụ thứ ba.
- **Giảm chi phí lưu trữ Salesforce**: Xóa file cũ tự động, tránh bị phạt dung lượng quá hạn.
- **An toàn tuyệt đối**: File được sao lưu trên S3 trước khi xóa trong Salesforce.
- **Báo cáo thực thời**: Nhận thông báo Slack khi có lỗi hoặc hoàn thành, không phải kiểm tra thủ công.
- **Scalable**: Hoạt động với bất kỳ số lượng file nào, từ hàng chục đến hàng nghìn.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Salesforce**:
   - **Credentials API**: Username, Password, Security Token (tạo tại [Salesforce Security Token](https://help.salesforce.com/s/articleView?id=sf.bc_manage_security_tokens.htm&type=5)).
   - **Permissions**: Trình duyệt file (`ContentVersion`, `ContentDocumentLink`), quyền đọc/xóa (`ContentDocument`).

2. **Tài khoản AWS S3**:
   - **Access Key & Secret Key**: Tạo tại [AWS IAM](https://console.aws.amazon.com/iam/).
   - **Bucket S3**: Bucket đã tồn tại và có quyền `putObject`, `deleteObject`.

3. **Tài khoản Slack** (không bắt buộc nhưng khuyến nghị):
   - **Token Slack**: Tạo tại [Slack API Tokens](https://api.slack.com/apps) (chọn `Bot Token`).

4. **n8n Self-hosted**:
   - Cài đặt n8n trên VPS để workflow hoạt động liên tục (không dùng phiên bản miễn phí trên cloud).
   - 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%).
   - 👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Truy cập [n8n Editor](https://n8n.io/editor).
2. Nhấp vào **"Import"** và chọn file JSON từ [link gốc](https://n8n.io/workflows/6305).
   *Hoặc* copy toàn bộ JSON từ link trên và paste vào ô **"Import from JSON"**.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow gồm **11 node** quan trọng, các sếp cần cấu hình như sau:

##### **A. Cấu Hình Salesforce**
- **Node "Get All ContentDocuments older than 365 days ago"**:
  - **Credentials**: Chọn tài khoản Salesforce đã cấu hình.
  - **Query**: Đảm bảo đã chọn `ContentDocument` và lọc theo `LastModifiedDate < 365 days ago`.
  - **Fields**: Chọn `Id`, `Title`, `ContentDocumentId`, `ContentDocumentLink` (để lấy liên kết file).

- **Node "Get LinkedEntityId from ContentDocumentLink"**:
  - **Operation**: Chọn `GET`.
  - **Endpoint**: `https://{instance}.salesforce.com/services/data/v56.0/sobjects/ContentDocumentLink/{ContentDocumentLinkId}`.
  - **Headers**: Thêm `Authorization: Bearer {JWT_TOKEN}` (tự động tạo khi sử dụng credentials Salesforce).

- **Node "Delete Original File in Salesforce"**:
  - **Method**: `DELETE`.
  - **Endpoint**: `https://{instance}.salesforce.com/services/data/v56.0/sobjects/ContentVersion/{ContentVersionId}`.
  - **Headers**: Giống như node trên.

##### **B. Cấu Hình AWS S3**
- **Node "Upload to S3"**:
  - **Bucket Name**: Điền tên bucket S3 đã tạo.
  - **File Key**: Sử dụng `{json["Title"]}` để đặt tên file theo tiêu đề trong Salesforce (ví dụ: `Contract_2024.pdf`).
  - **Permissions**: Chọn `public-read` (nếu cần chia sẻ) hoặc `private` (mặc định).

- **Node "Prepare ContentDocumentId for Deletion"**:
  - **Code Script** (sử dụng JavaScript):
    ```javascript
    // Lấy ContentDocumentId từ ContentDocumentLink
    const contentDocumentId = $input.all()[0].json.ContentDocumentId;
    return { json: { ContentDocumentId: contentDocumentId } };
    ```

##### **C. Cấu Hình Slack (Nếu Có)**
- **Node "Send Slack Notification"**:
  - **Channel**: Chọn #general hoặc channel riêng.
  - **Message Template**:
    ```json
    {
      "blocks": [
        {
          "type": "section",
          "text": {
            "type": "mrkdwn",
            "text": "*File Migration Status:* :white_check_mark:"
          }
        },
        {
          "type": "section",
          "text": {
            "type": "mrkdwn",
            "text": "File *{{ $node["Get LinkedEntityId from ContentDocumentLink"].json["Title"] }}* đã được di chuyển sang S3 và xóa khỏi Salesforce."
          }
        }
      ]
    }
    ```

##### **D. Cấu Hình Schedule Trigger**
- **Node "Schedule Trigger"**:
  - **Frequency**: Chọn `daily` (hoặc `weekly` tùy chọn).
  - **Time**: Đặt giờ chạy vào ban đêm (ví dụ: 2 AM) để tránh ảnh hưởng đến hoạt động của Salesforce.

##### **E. Cấu Hình Filter Out User Attachments**
- **Node "Filter Out User Attachments"**:
  - **Code Script** (lọc bỏ file liên quan đến người dùng):
    ```javascript
    // Lọc bỏ file là attachment của người dùng (ContentDocumentLink.RelatedEntityId = User)
    const isUserAttachment = $input.all()[0].json.ContentDocumentLink.RelatedEntityId.startsWith('005');
    return !isUserAttachment;
    ```

#### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Chọn node **"Get All ContentDocuments older than 365 days ago"** và nhấp **"Run Workflow"**.
   - Kiểm tra log để đảm bảo file được tải xuống, upload lên S3 và xóa trong Salesforce.

2. **Bật Active**:
   - Sau khi test thành công, nhấp **"Active"** trên tab **"Workflow"** để chạy tự động theo lịch.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Lưu Log Tự Động**:
   - Thêm node **`n8n-nodes-base.stickyNote`** sau node **"Delete Original File in Salesforce"** để ghi log lỗi:
     ```json
     {
       "name": "Log Deletion Status",
       "type": "stickyNote",
       "operation": "append",
       "fileName": "salesforce_file_migration.log",
       "text": "Xóa file {{ $node["Delete Original File in Salesforce"].json["Title"] }} thành công."
     }
     ```

2. **Gửi Báo Cáo Định Kỳ**:
   - Sử dụng node **`n8n-nodes-base.email`** để gửi báo cáo hàng tháng cho team:
     ```json
     {
       "name": "Send Monthly Report",
       "type": "email",
       "operation": "send",
       "to": ["team@example.com"],
       "subject": "Báo cáo di chuyển file Salesforce - Tháng {{ $date.now("MMMM YYYY") }}",
       "text": "Tổng số file đã di chuyển: {{ $node["Loop Over Each File Record"].json.length }}."
     }
     ```

3. **Kết Hợp Với Slack Alert**:
   - Thêm node **`n8n-nodes-base.slack`** để báo lỗi nếu file không tải được:
     ```json
     {
       "name": "Slack Error Alert",
       "type": "slack",
       "operation": "postMessage",
       "channel": "#errors",
       "text": "Lỗi tải file: {{ $node["Download File Content"].json.error }}",
       "blocks": [
         {
           "type": "section",
           "text": {
             "type": "mrkdwn",
             "text": "*Lỗi tải file:* {{ $node["Download File Content"].json.error }}"
           }
         }
       ]
     }
     ```

4. **Tối Ưu Hóa Dung Lượng S3**:
   - Sử dụng **`n8n-nodes-base.awsS3`** với tùy chọn **`StorageClass: STANDARD_IA`** để giảm chi phí cho file ít truy cập.

---

### 📌 **Kết Luận**
Workflow **Salesforce to S3 File Migration & Cleanup** là giải pháp **tự động hóa hoàn toàn** để:
✔ **Giải phóng không gian Salesforce** bằng cách xóa file cũ tự động.
✔ **Sao lưu an toàn** tất cả file lên S3 trước khi xóa.
✔ **Tiết kiệm thời gian** và giảm rủi ro sai sót.
✔ **Báo cáo thực thời** qua Slack hoặc email.

**Hành động ngay hôm nay!**
1. **Cài đặt n8n trên VPS** (để workflow chạy liên tục).
2. **Import workflow** và cấu hình theo hướng dẫn.
3. **Bật Active** và để nó làm việc cho bạn!

👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) với mã **VPSN8N** để tiết kiệm chi phí.
👉 [Xem hướng dẫn cài n8n trên VPS](https://docs.n8n.io/hosting/self-hosting-on-vps/) (nếu cần hỗ trợ).

**Chúc các sếp thành công với việc tự động hóa file Salesforce!** 🚀