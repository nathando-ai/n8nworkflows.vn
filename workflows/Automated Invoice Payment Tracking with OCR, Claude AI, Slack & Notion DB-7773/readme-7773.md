---
title: "💰 **Tự Động Hóa Theo Dõi Thanh Toán Hóa Đơn Với OCR, AI Claude, Slack & Notion – Giảm 90% Thời Gian Kiểm Tra**"
description: "Workflow tự động hóa hoàn toàn không cần code để quét, phân tích, xác minh và cập nhật trạng thái thanh toán hóa đơn từ file ảnh/vid, tự động phân loại và báo cáo lên Slack/Notion. Giúp các sếp tiết kiệm hàng giờ mỗi tuần và giảm thiểu lỗi nhân sự."
slug: "tieu-dong-hoa-theo-doi-thanh-toan-hoa-don-ocr-ai-claude-notion"
tags: [n8n, automation, no-code, ai-summarization, multimodal-ai, notion-api, slack-integration, ocr-automation, claudie-ai]
keywords: [tự động hóa hóa đơn, n8n workflow hóa đơn, ai phân tích hóa đơn, quét hóa đơn tự động, notion database hóa đơn, slack báo cáo hóa đơn, claudie-3-5 haiku]
---

# 🚀 **Tự Động Hóa Theo Dõi Thanh Toán Hóa Đơn: Từ File Ảnh → AI Phân Tích → Notion Cập Nhật → Slack Báo Cáo**

## **😩 Nỗi Đau Của Các Sếp Khi Theo Dõi Hóa Đơn Thủ Công**
Hàng tuần, các sếp và nhân viên tài chính phải:
- **Quét và nhập liệu hóa đơn** từ hàng chục file ảnh/vid (PDF, JPG, PNG) vào hệ thống.
- **Phân tích nội dung** để xác định số tiền, ngày hạn, người nhận, và trạng thái thanh toán.
- **So sánh với cơ sở dữ liệu** để tránh trùng lặp hoặc bỏ sót hóa đơn cũ.
- **Cập nhật trạng thái** (chưa thanh toán, đã thanh toán, phần mềm) vào Notion/Excel.
- **Gửi báo cáo** lên Slack/Teams cho các bộ phận liên quan, dẫn đến **lỗi thông tin và mất thời gian**.

**Kết quả?** Tốn **3-5 giờ/ngày** cho mỗi nhân viên, và **rủi ro sai sót cao** do con người.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow này **chạy 24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS chuyên dụng:
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 **[VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (đủ sức mạnh cho workflow 85 nodes này)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
Sau khi triển khai workflow này, các sếp sẽ:
✅ **Tiết kiệm 90% thời gian** trong việc theo dõi hóa đơn (từ 5h/ngày xuống còn **30 phút**).
✅ **Giảm thiểu lỗi 100%** nhờ AI Claude phân tích chính xác thông tin từ hóa đơn.
✅ **Cập nhật tự động** trạng thái thanh toán lên Notion (chưa thanh toán, đã thanh toán, phần mềm).
✅ **Báo cáo ngay lập tức** lên Slack với thông tin chi tiết (số hóa đơn, ngày hạn, người nhận).
✅ **Phân loại và lưu trữ** hóa đơn theo trạng thái (chưa thanh toán → đã thanh toán → đã lưu trữ).
✅ **Xử lý trùng lặp tự động** (hóa đơn cũ bị quét lại).

---

## 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
### **1. Tài Khoản & API Keys**
| **Dịch Vụ**       | **Thông Tin Cần Thiết**                          | **Lưu Ý** |
|-------------------|------------------------------------------------|-----------|
| **Slack**         | - API Token (Slack App)                         | Tạo từ [Slack API](https://api.slack.com/apps) |
|                   | - Channel ID (để gửi thông báo)               | Chọn channel muốn nhận báo cáo |
| **Notion**        | - API Key (Notion Integration)                 | Tạo từ [Notion API](https://www.notion.so/my-integrations) |
|                   | - Database ID (các bảng: Hóa Đơn, Dòng Chi Tiết, Dòng Thu Chi) | Chọn database đã tạo sẵn |
| **OCR Space**     | - API Key (để quét và phân tích văn bản)       | Đăng ký tại [OCR Space](https://ocr.space/ocrapi) |
| **Anthropic (Claude AI)** | - API Key (để sử dụng model Claude 3.5) | Đăng ký tại [Anthropic](https://www.anthropic.com/) |

### **2. Cấu Trúc Notion (Nên Chuẩn Bị Trước)**
Workflow này **yêu cầu các bảng Notion sau**:
1. **Hóa Đơn (Invoice Database)**
   - Trạng thái: Chưa thanh toán / Đã thanh toán / Phần mềm
   - Ngày hạn
   - Số hóa đơn
   - Người nhận
   - Tổng tiền
   - File đính kèm (liên kết đến hóa đơn gốc)

2. **Dòng Chi Tiết Hóa Đơn (Line Items Database)**
   - Mô tả dịch vụ
   - Số lượng
   - Đơn giá
   - Thành tiền

3. **Dòng Thu Chi (Cashflow Database)**
   - Ngày thanh toán
   - Số tiền
   - Trạng thái (Chưa thanh toán / Đã thanh toán)
   - Liên kết đến hóa đơn

---
## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. **Tải workflow** từ [n8n.io/workflows/7773](https://n8n.io/workflows/7773) (chọn **Export as JSON**).
2. **Mở n8n Editor** (trên VPS hoặc n8n.cloud).
3. **Nhấp vào "Import"** → Chọn file JSON vừa tải.
4. **Chọn "Import"** → Workflow sẽ xuất hiện trên canvas.

#### **Phương pháp 2: Copy/Paste JSON**
1. **Copy toàn bộ JSON** từ file export.
2. **Tạo workflow mới** trong n8n Editor.
3. **Nhấp vào "Import"** → Chọn **Paste JSON** → Đóng cửa sổ.

---
### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này **phức tạp** (85 nodes) và cần **cấu hình cẩn thận** các phần sau:

#### **🔹 1. Cấu Hình Slack Trigger (Bắt Đầu Workflow)**
- **Node: "Slack Trigger"**
  - **Action:** Chọn **"File shared"** (để bắt đầu khi file hóa đơn được gửi lên Slack).
  - **Channel:** Chọn channel muốn kích hoạt workflow.
  - **Credentials:** Chọn **"slackApi"** (đã cấu hình trước).

#### **🔹 2. Cấu Hình OCR Space (Quét Văn Bản)**
- **Node: "OCR Space Parse1" & "OCR Space Parse"**
  - **API Key:** Điền vào **credentials "httpHeaderAuth"** (tạo từ OCR Space).
  - **URL:** Sử dụng URL API của OCR Space (ví dụ: `https://api.ocr.space/parse/image`).
  - **Headers:**
    ```json
    {
      "apikey": "{{$credentials.httpHeaderAuth.apiKey}}",
      "Content-Type": "application/json"
    }
    ```
  - **Body:**
    ```json
    {
      "language": "eng",
      "OCREngine": 1,
      "FileContentBase64": "{{$json.file.content}}"
    }
    ```
  - **Lưu ý:** Nếu file quá lớn, cần **nén trước** hoặc chia nhỏ.

#### **🔹 3. Cấu Hình Claude AI (Phân Tích Hóa Đơn)**
- **Node: "Anthropic Chat Model4"**
  - **Model:** Chọn **"claude-3-5-haiku-20241022"** (đã cấu hình trong workflow).
  - **API Key:** Điền vào **credentials "anthropicApi"** (tạo từ Anthropic).
  - **Prompt mẫu (cần chỉnh sửa theo yêu cầu):**
    ```json
    {
      "prompt": "Analyze the following invoice details extracted from OCR:\n\n{{$json.invoiceData}}\n\nExtract the following information in JSON format:\n1. Invoice Number\n2. Date\n3. Due Date\n4. Vendor Name\n5. Total Amount\n6. Line Items (Description, Quantity, Unit Price, Amount)\n\nIf any field is missing, return 'N/A'.",
      "max_tokens": 1000,
      "temperature": 0.7
    }
    ```
  - **Lưu ý:** Nếu AI trả về sai, cần **cập nhật prompt** trong node **"Basic LLM Chain"**.

#### **🔹 4. Cấu Hình Notion (Cập Nhật Dữ Liệu)**
- **Node: "Send to Source File Invoice 1", "Update Invoice to Paid Fully", ...**
  - **Database ID:** Điền **ID của database Notion** (tìm trong URL Notion).
  - **Properties:**
    - **Trạng thái:** Chọn từ dropdown (Chưa thanh toán / Đã thanh toán).
    - **File đính kèm:** Liên kết đến file gốc (nếu có).
    - **Liên kết đến dòng chi tiết:** ID của dòng chi tiết trong database.
  - **Lưu ý:**
    - **Kiểm tra lại tên database** trong Notion (workflow sử dụng tên mặc định).
    - **Cập nhật lại ID** nếu database được tạo mới.

#### **🔹 5. Cấu Hình Slack Notification (Báo Cáo)**
- **Node: "Send a message", "Notify New Invoice", ...**
  - **Channel:** Chọn channel muốn gửi thông báo.
  - **Message Template:** Sử dụng **JSON Path** để trích xuất dữ liệu từ workflow:
    ```json
    {
      "blocks": [
        {
          "type": "section",
          "text": {
            "type": "mrkdwn",
            "text": "*Hóa Đơn Mới:* <{{$json.invoiceNumber}}|{{$json.invoiceNumber}}>\n*Người Nhận:* {{$json.vendorName}}\n*Ngày Hạn:* {{$json.dueDate}}\n*Tổng Tiền:* ${{$json.totalAmount}} VND"
          }
        },
        {
          "type": "actions",
          "elements": [
            {
              "type": "button",
              "text": {
                "type": "plain_text",
                "text": "Xem Chi Tiết"
              },
              "url": "{{$json.notionUrl}}",
              "style": "primary"
            }
          ]
        }
      ]
    }
    ```
  - **Lưu ý:** Nếu Slack không hiển thị đúng, **kiểm tra lại JSON Path**.

#### **🔹 6. Xử Lý Trùng Lặp (Duplicate Invoice)**
- **Node: "Internal Check Duplicate Invoice"**
  - **Logic:** So sánh **số hóa đơn** với database Notion.
  - **Nếu trùng lặp:**
    - Workflow sẽ **tạo bản sao** và **gửi thông báo "Duplicate Found"** lên Slack.
    - **Node: "Send Duplicate Notification"** sẽ hoạt động.
  - **Nếu không trùng lặp:**
    - Workflow tiếp tục **tạo hóa đơn mới** và cập nhật trạng thái.

#### **🔹 7. Cập Nhật Trạng Thái Thanh Toán**
- **Node: "Update Invoice to Paid Fully", "Update Invoice to Paid Partial"**
  - **Điều kiện:**
    - Nếu **file thanh toán được gửi lên**, workflow sẽ **cập nhật trạng thái** từ "Chưa thanh toán" → "Đã thanh toán".
    - Nếu **chỉ thanh toán một phần**, sẽ cập nhật thành "Đã thanh toán phần mềm".
  - **Lưu ý:** Cần **kiểm tra lại logic trong node "Decide Fate"** (Switch node).

---
### **3. Kích Hoạt ⚡️ Workflow**
1. **Test Run với dữ liệu mẫu:**
   - Gửi **1 file hóa đơn mẫu** (PDF/JPG) lên Slack channel đã cấu hình.
   - **Kiểm tra các bước:**
     - OCR có phân tích đúng không?
     - Claude AI có trích xuất thông tin chính xác không?
     - Notion có cập nhật trạng thái không?
     - Slack có nhận được thông báo không?
   - **Nếu có lỗi:** Sử dụng **node "Stop and Error"** để debug.

2. **Bật Active Workflow:**
   - Sau khi test thành công, **nhấp vào "Active"** trên workflow.

---
## ✍️ **Mẹo & Gợi Ý Nâng Cao**
### **1. Tối Ưu Hóa AI Claude**
- **Cập nhật Prompt** để AI phân tích chính xác hơn:
  ```json
  {
    "prompt": "You are an expert invoice parser. Extract ONLY the following fields from this invoice:\n\n- Invoice Number: [EXACT NUMBER]\n- Date: [DD/MM/YYYY]\n- Due Date: [DD/MM/YYYY]\n- Vendor Name: [FULL NAME]\n- Total Amount: [NUMBER WITH CURRENCY]\n- Line Items: [ARRAY OF OBJECTS WITH DESCRIPTION, QUANTITY, UNIT PRICE, AMOUNT]\n\nIf any field is missing, return 'N/A'. Do NOT add extra information."
  }
  ```
- **Sử dụng LangChain** để **cải thiện độ chính xác** của AI.

### **2. Lưu Log Lỗi & Báo Cáo Hàng Ngày**
- **Thêm node "Error Trigger"** để **gửi email/Slack** khi workflow lỗi.
- **Sử dụng node "StickyNote"** để ghi lại **log lỗi** (ví dụ: OCR không đọc được file nào).
- **Tạo báo cáo hàng ngày** bằng **node "Aggregate"** + **Slack Notification**.

### **3. Kết Nối Với Google Sheets/Excel**
- **Thay thế Notion bằng Google Sheets** (nếu ưa dùng Excel):
  - Thay **node Notion** bằng **node Google Sheets**.
  - Cấu hình **API Google Sheets** và **database tương ứng**.

### **4. Tự Động Gửi Hóa Đơn Đến Email**
- **Thêm node "Email"** (n8n-nodes-base.email) để:
  - Gửi **hóa đơn mới** đến bộ phận kế