---
title: "🔒 Tự Động Xóa Chứng Nhận AWS ACM Hết Hạn Với Phê Chuẩn Trên Slack (Không Code)"
description: "Giải pháp tự động hóa 100% không cần code để phát hiện và xóa chứng nhận SSL AWS ACM hết hạn chỉ sau 1 lần phê duyệt trên Slack, giúp bảo mật môi trường AWS của các sếp một cách an toàn và minh bạch."
slug: "tu-dong-xoa-chung-nhan-aws-acm-het-han-voi-phe-chuan-tren-slack"
tags: [n8n, automation, devops, aws-acm, slack-integration, no-code]
keywords: [tự động hóa aws acm, xóa chứng nhận ssl hết hạn, slack approval workflow, devops no-code, quản lý ssl aws]
---

# 🚀 **Tự Động Xóa Chứng Nhận AWS ACM Hết Hạn Với Phê Chuẩn Trên Slack**

### **Nỗi Đau Của Các Sếp**
Các sếp đã từng phải:
- **Quét thủ công** danh sách chứng nhận SSL trên AWS ACM để tìm những cái đã hết hạn?
- **Lo lắng** về chứng nhận SSL cũ vẫn tồn tại trong hệ thống, gây rủi ro bảo mật?
- **Phải nhớ nhắc** mình xóa chúng sau khi hết hạn, dẫn đến quên lãng và lãng phí tài nguyên?
- **Không có cách nào** để kiểm soát và phê duyệt xóa chứng nhận một cách minh bạch?

**Workflow này giải quyết tất cả!** Nó tự động phát hiện, thông báo và xóa chứng nhận AWS ACM hết hạn **chỉ sau 1 lần phê duyệt trên Slack**, giúp các sếp **tiết kiệm thời gian, giảm rủi ro và duy trì môi trường AWS sạch sẽ**.

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%**: Không cần can thiệp thủ công, workflow chạy hàng ngày theo lịch trình.
- **Bảo mật tối ưu**: Chỉ xóa chứng nhận **sau khi được phê duyệt** trên Slack, tránh xóa sai hoặc mất dữ liệu.
- **Minh bạch toàn diện**: Tất cả hành động (thông báo, phê duyệt, xóa) đều được ghi lại trên Slack.
- **Tiết kiệm thời gian**: Giảm thiểu công việc thủ công, tập trung vào những nhiệm vụ chiến lược.
- **Dễ dàng mở rộng**: Thêm logging, báo cáo hoặc tích hợp với các công cụ khác như Google Sheets/Notion.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản AWS** với quyền IAM cho:
   - `acm:ListCertificates`
   - `acm:DescribeCertificate`
   - `acm:DeleteCertificate`
2. **Bot Slack** với quyền:
   - `chat:write` (để gửi thông báo)
   - `reactions:read` (để đọc phản hồi phê duyệt)
3. **Slack Channel** để workflow gửi thông báo và chờ phê duyệt.
4. **n8n Self-hosted** (khuyến nghị) hoặc n8n Cloud.
5. **API Key AWS** và **Token OAuth2 Slack** đã cấu hình trong n8n.
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/7626](https://n8n.io/workflows/7626) hoặc copy/paste JSON vào **n8n Editor**.
- **Cách import**:
  1. Mở **n8n Editor** → Nhấn **"Import"** → Dán JSON hoặc tải file `.json`.
  2. Chọn **"Import"** để workflow xuất hiện trên canvas.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow gồm **6 node chính**, các sếp cần chú ý cấu hình như sau:

##### **🔹 Node 1: Daily Schedule Trigger**
- **Cấu hình**:
  - Chọn **"Daily"** và thời gian phù hợp (ví dụ: **09:00 AM** để tránh giờ cao điểm).
  - Nếu muốn chạy tuần hoặc theo cron, chỉnh sửa ở **"Schedule"** → **"Custom"** và nhập biểu thức cron (ví dụ: `0 9 * * *` cho 9h hàng ngày).

##### **🔹 Node 2: Get Many Certificates (AWS ACM)**
- **Credentials**: Chọn **"aws"** (đã cấu hình trước trong n8n).
- **Không cần chỉnh sửa thêm** vì node này tự lấy tất cả chứng nhận từ AWS.

##### **🔹 Node 3: Filter (Lọc Chỉ Chứng Nhận Hết Hạn)**
- **Cấu hình**:
  - Trong tab **"Filter"**, chọn **"Status"** → **"INACTIVE"** (chứng nhận hết hạn).
  - Hoặc sử dụng **JSONPath** để lọc theo ngày hết hạn (ví dụ: `$.ExpirationDate < "2024-01-01T00:00:00Z"`).
  - **Lưu ý**: Nếu không có node **Filter**, workflow sẽ gửi tất cả chứng nhận cho Slack, gây nhầm lẫn.

##### **🔹 Node 4: Send Message & Wait for Reaction (Slack)**
- **Credentials**: Chọn **"slackOAuth2Api"**.
- **Cấu hình thông báo**:
  - **Message**: Tùy chỉnh nội dung thông báo (ví dụ:
    ```json
    {
      "text": "🚨 Chứng nhận SSL hết hạn cần phê duyệt:\nDomain: {{$node["Get many certificates"].jsonpath("$.DomainName")}}\nARN: {{$node["Get many certificates"].jsonpath("$.CertificateArn")}}\nNgày hết hạn: {{$node["Get many certificates"].jsonpath("$.ExpirationDate")}}",
      "blocks": [
        {
          "type": "section",
          "text": {
            "type": "mrkdwn",
            "text": "*Chứng nhận SSL hết hạn* 🚨"
          }
        },
        {
          "type": "divider"
        },
        {
          "type": "section",
          "text": {
            "type": "mrkdwn",
            "text": "Domain: `{{$node["Get many certificates"].jsonpath("$.DomainName")}}`\nARN: `{{$node["Get many certificates"].jsonpath("$.CertificateArn")}}`\nNgày hết hạn: `{{$node["Get many certificates"].jsonpath("$.ExpirationDate")}}`"
          }
        },
        {
          "type": "actions",
          "elements": [
            {
              "type": "button",
              "text": {
                "type": "plain_text",
                "text": "Phê duyệt xóa"
              },
              "value": "approve",
              "style": "primary"
            },
            {
              "type": "button",
              "text": {
                "type": "plain_text",
                "text": "Từ chối"
              },
              "value": "reject"
            }
          ]
        }
      ]
    }
    ```
  - **Channel**: Chọn **Slack Channel** muốn gửi thông báo (ví dụ: `#aws-certificates`).
  - **Wait for Reaction**: Chọn **"Yes"** và thời gian chờ (mặc định **1 giờ**). Nếu muốn nhanh hơn, giảm xuống **30 phút**.

##### **🔹 Node 5: Delete a Certificate (AWS ACM)**
- **Credentials**: Chọn **"aws"** (cùng với node lấy chứng nhận).
- **Không cần chỉnh sửa thêm** vì node này tự lấy **ARN** từ node trước để xóa.

##### **🔹 Node 6: Inform IT Admin (Slack)**
- **Credentials**: Chọn **"slackOAuth2Api"**.
- **Cấu hình thông báo kết quả**:
  - **Message**: Tùy chỉnh thông báo sau khi xóa (ví dụ:
    ```json
    {
      "text": "✅ Chứng nhận SSL đã được xóa thành công:\nDomain: {{$node["Get many certificates"].jsonpath("$.DomainName")}}\nARN: {{$node["Get many certificates"].jsonpath("$.CertificateArn")}}\nNgày xóa: {{$node["Get many certificates"].jsonpath("$.ExpirationDate")}}",
      "blocks": [
        {
          "type": "section",
          "text": {
            "type": "mrkdwn",
            "text": "*Chứng nhận đã được xóa thành công* ✅"
          }
        },
        {
          "type": "divider"
        },
        {
          "type": "section",
          "text": {
            "type": "mrkdwn",
            "text": "Domain: `{{$node["Get many certificates"].jsonpath("$.DomainName")}}`\nARN: `{{$node["Get many certificates"].jsonpath("$.CertificateArn")}}`"
          }
        }
      ]
    }
    ```
  - **Channel**: Chọn cùng **Slack Channel** như node thông báo.

#### **3. Kích Hoạt ⚡️**
- **Test Run**: Nhấn **"Run Workflow"** và chọn **1 chứng nhận mẫu** để kiểm tra.
- **Bật Active**: Sau khi kiểm tra thành công, chuyển **switch Active** sang **"ON"**.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Thêm Logging (Ghi Log)**
   - Sử dụng **Google Sheets** hoặc **Notion** để lưu lịch sử chứng nhận hết hạn và hành động phê duyệt.
   - **Cách làm**:
     - Thêm node **Google Sheets** sau node **Delete a Certificate**.
     - Cấu hình để ghi dữ liệu như:
       ```json
       {
         "sheetName": "AWS_Certificates_Log",
         "values": [
           ["Domain", "ARN", "ExpirationDate", "Action", "Timestamp"],
           [
             "{{$node["Get many certificates"].jsonpath("$.DomainName")}}",
             "{{$node["Get many certificates"].jsonpath("$.CertificateArn")}}",
             "{{$node["Get many certificates"].jsonpath("$.ExpirationDate")}}",
             "{{$node["Send message and wait for response"].jsonpath("$.reaction")}}",
             "{{$node["Daily Schedule Trigger"].jsonpath("$.date")}}"
           ]
         ]
       }
       ```

2. **Thêm Mode Dry-Run (Test Trước Khi Xóa)**
   - Thêm **IF Node** trước node **Delete a Certificate** để kiểm tra môi trường.
   - **Cấu hình**:
     - Nếu `ENV === "dry-run"`, **bỏ qua** node xóa.
     - Nếu `ENV === "prod"`, tiến hành xóa.
   - **Cách thiết lập**:
     - Thêm node **Set** trước node **Delete a Certificate**.
     - Cấu hình:
       ```json
       {
         "operation": "set",
         "key": "ENV",
         "value": "prod"
       }
       ```
     - Thêm node **IF** sau đó:
       - **Condition**: `{{$node["Set"].jsonpath("$.ENV")}} === "prod"`
       - Nếu **true**, tiếp tục node xóa.

3. **Tích Hợp với Email (Báo Cáo Định Kỳ)**
   - Thêm node **Email** để gửi báo cáo hàng tuần cho team.
   - **Cấu hình**:
     - Sử dụng **Gmail SMTP** hoặc **SendGrid**.
     - Nội dung email bao gồm:
       - Danh sách chứng nhận hết hạn trong tuần.
       - Số lượng đã xóa.
       - Link Slack để xem chi tiết.

4. **Tự Động Xóa Chứng Nhận Cũ (Old Certificates)**
   - Thêm điều kiện lọc để xóa chứng nhận **trước 30 ngày** (thay vì chỉ hết hạn).
   - **Cách làm**:
     - Trong node **Filter**, thêm điều kiện:
       ```json
       {
         "path": "ExpirationDate",
         "operator": "lt",
         "value": "{{$now - 30 * 24 * 60 * 60 * 1000}}"
       }
       ```

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** để các sếp tự động hóa quản lý chứng nhận SSL trên AWS ACM một cách **an toàn, minh bạch và không cần code**. Bằng cách kết hợp **Slack cho phê duyệt** và **AWS ACM cho xóa tự động**, các sếp không chỉ tiết kiệm thời gian mà còn **giảm thiểu rủi ro bảo mật** do chứng nhận cũ còn tồn tại.

**Hành động ngay!**
1. **Import workflow** và cấu hình theo hướng dẫn.
2. **Test Run** với 1-2 chứng nhận mẫu.
3. **Bật Active** và để workflow chạy tự động hàng ngày.

**Nếu có thắc mắc**, các sếp có thể comment bên dưới hoặc liên hệ với tác giả [Trung Tran](https://n8n.io/workflows/7626) để hỗ trợ!

---
**💡 Mở rộng khả năng**: Nếu muốn, các sếp có thể tích hợp thêm **AWS CloudWatch** để cảnh báo khi có chứng nhận sắp hết hạn (trong vòng 7 ngày). Hãy thử nghiệm và tối ưu hóa workflow theo nhu cầu của team!