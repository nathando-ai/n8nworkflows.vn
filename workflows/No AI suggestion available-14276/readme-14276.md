---
title: "🤖 **Tự Động Hóa Khớp Lại Tài Chính 100% AI: Khớp Hóa Đơn, Bảng Cân Đối & ERP Với GPT-4.1 Mini - Không Cần Code!**"
description: "Workflow này tự động khớp lại dữ liệu tài chính từ nhiều nguồn (bảng cân đối, hóa đơn, ERP, CSV) bằng logic xác định và AI fuzzy matching. Kết quả: tiết kiệm 20h/tháng, giảm sai sót 90%, và báo cáo tự động lên Google Sheets + Slack. Phù hợp cho doanh nghiệp vừa và lớn."
slug: "tu-dong-hoa-khop-lai-tai-chinh-ai"
tags: [n8n, automation, no-code, tài chính, AI, OpenAI, Google Sheets, Slack, ERP, hóa đơn, bảng cân đối]
keywords: [tự động hóa khớp lại tài chính, n8n workflow tài chính, AI khớp hóa đơn, khớp lại ERP và bank statement, tự động hóa báo cáo tài chính, GPT-4.1 Mini trong n8n]
---

# 🚀 **Tự Động Hóa Khớp Lại Tài Chính: Khớp Hóa Đơn, Bảng Cân Đối & ERP Với AI (Không Cần Code!)**

### **Nỗi Đau Của Các Sếp Tài Chính Hàng Ngày**
Các sếp tài chính thường phải:
- **Tốn thời gian vô cùng** để so sánh thủ công hóa đơn, bảng cân đối, và dữ liệu từ ERP (SAP, Odoo, QuickBooks...).
- **Mắc sai sót** do con người quên hoặc nhầm lẫn trong quá trình khớp lại.
- **Không biết dữ liệu nào đã được khớp** và cần review thêm.
- **Báo cáo chậm trễ** vì phải tổng hợp thủ công sau khi khớp xong.

**Workflow này giải quyết tất cả!** Nó tự động:
✅ **Khớp lại hóa đơn, bảng cân đối, và dữ liệu ERP** với độ chính xác cao.
✅ **Sử dụng AI (GPT-4.1 Mini)** để khớp dữ liệu không chính xác (fuzzy matching).
✅ **Tính điểm tin cậy** và tự động phân loại giao dịch đã khớp vs. cần review.
✅ **Gửi báo cáo tự động** lên Google Sheets và thông báo trên Slack.
✅ **Hoạt động 24/7** mà không cần can thiệp của con người.

---

## 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**Lợi Ích Cốt Lõi**]
- **Tiết kiệm 20h/tháng** cho bộ phận tài chính (giá trị ~10-15 triệu/tháng).
- **Giảm sai sót 90%** nhờ logic xác định + AI fuzzy matching.
- **Báo cáo tự động** lên Google Sheets với lịch sử khớp lại chi tiết.
- **Thông báo ngay lập tức** trên Slack khi có giao dịch cần review.
- **Hoạt động liên tục** mà không cần can thiệp thủ công.
:::

---

## 🔧 **Yêu Cầu Cần Thiết**
Để workflow này hoạt động, các sếp cần chuẩn bị:
### **1. Tài Khoản & API Keys**
| **Dịch Vụ**          | **Thông Tin Cần Thiết**                          | **Lưu Ý**                                  |
|----------------------|--------------------------------------------------|--------------------------------------------|
| **n8n Self-hosted**  | VPS với 4GB RAM trở lên (gợi ý [TinoHost](https://tino.vn/vps-n8n?affid=388) hoặc [BNIX](https://my.bnix.one/aff.php?aff=172)) | Sử dụng mã giảm giá **VPSN8N** (39% off). |
| **OpenAI**           | API Key (trong [OpenAI Dashboard](https://platform.openai.com/account/api-keys)) | Chọn model **gpt-4.1-mini** (rẻ hơn gpt-4). |
| **Google Sheets**     | File Google Sheets có quyền chỉnh sửa (để lưu báo cáo). | Chia sẻ file với email `@n8n-workflow.com`. |
| **Slack**            | Webhook URL từ Slack (tạo tại [API Settings](https://api.slack.com/apps)). | Chọn channel muốn nhận thông báo. |

### **2. Dữ Liệu Input**
Workflow nhận dữ liệu tài chính qua **Webhook POST** với đường dẫn:
```
https://[your-n8n-domain]/financial-data-reconciliation
```
**Dạng dữ liệu hỗ trợ:**
- **CSV** (bảng cân đối, hóa đơn)
- **JSON/XML** (dữ liệu từ ERP)
- **Bảng Excel** (có thể convert sang CSV trước khi gửi)

---

## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Cách 1: Từ File JSON**
1. **Tải workflow** từ [n8n.io/workflows/14276](https://n8n.io/workflows/14276) (chọn **Export as JSON**).
2. **Mở n8n Editor** trên VPS của bạn.
3. Nhấn **Import** và chọn file JSON vừa tải.
4. **Xác nhận** và workflow sẽ xuất hiện trên canvas.

#### **Cách 2: Copy/Paste JSON**
1. **Copy toàn bộ JSON** từ [n8n.io/workflows/14276](https://n8n.io/workflows/14276).
2. Trong n8n Editor, nhấn **Import** → **Paste JSON** → **Import**.

---

### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này **phức tạp** vì sử dụng **AI + logic xác định**, nên cần cấu hình cẩn thận các node sau:

#### **🔹 Node 1: Webhook - Receive Financial Data**
- **Đường dẫn (Path):** `financial-data-reconciliation` (không đổi).
- **Phương thức HTTP:** `POST` (không đổi).
- **Lưu ý:**
  - Cần **bảo mật Webhook** bằng cách:
    - Sử dụng **Authentication** (Basic Auth hoặc Bearer Token).
    - Kiểm tra **IP nguồn** (chỉ cho phép IP của ERP hoặc hệ thống nội bộ).
  - **Test Webhook** bằng cách gửi dữ liệu mẫu từ Postman:
    ```json
    {
      "data": [
        {
          "source": "bank_statement",
          "transaction_id": "TXN123",
          "amount": 1000000,
          "date": "2024-05-20",
          "description": "Thanh toán hóa đơn điện"
        }
      ]
    }
    ```

#### **🔹 Node 2: OpenAI Chat Model (AI Fuzzy Matching)**
- **Model:** `gpt-4.1-mini` (đã cấu hình sẵn, không cần đổi).
- **API Key:**
  - Đi đến **Credentials** trong n8n Editor → **Add Credential** → **OpenAI**.
  - Nhập **API Key** từ OpenAI Dashboard.
- **Prompt Template:**
  Workflow đã cấu hình sẵn **prompt** để AI khớp dữ liệu không chính xác. **Không cần chỉnh sửa** trừ khi:
  - Dữ liệu của bạn có **đặc điểm riêng** (ví dụ: định dạng ngày khác).
  - Thêm **các rule khớp bổ sung** (ví dụ: tolerable difference cho amount).

#### **🔹 Node 3: Google Sheets (Log to Reconciliation Report)**
- **File Google Sheets:**
  - Tạo **một file mới** và chia sẻ với `@n8n-workflow.com`.
  - **Cấu trúc sheet** phải có các cột:
    | Column Name       | Type      |
    |--------------------|-----------|
    | `transaction_id`   | Text      |
    | `amount`           | Number    |
    | `date`             | Date      |
    | `source`           | Text      |
    | `match_status`     | Text      |
    | `confidence_score` | Number    |
    | `review_needed`    | Boolean   |
- **Operation:** `appendOrUpdate` (đã cấu hình sẵn).

#### **🔹 Node 4: Slack (Notify Finance Team)**
- **Webhook URL:**
  - Tạo **Incoming Webhook** trong Slack App:
    1. Vào [API Settings](https://api.slack.com/apps) → Tạo app mới.
    2. Chọn **Incoming Webhooks** → Add New Webhook to Workspace.
    3. Chọn **channel** muốn nhận thông báo.
  - **Copy URL** và dán vào **Credentials** của node Slack trong n8n.
- **Message Template:**
  Workflow sẽ tự động gửi **các thông báo** như:
  - `✅ Auto-reconciled: TXN123 (Amount: 1M, Confidence: 98%)`
  - `⚠️ Review needed: TXN456 (Amount: 5M, Confidence: 65%)`

#### **🔹 Node 5: Deterministic Matching Logic (Code Node)**
- **Logic mặc định:**
  - Khớp dựa trên **transaction_id**, **amount**, và **date**.
  - Nếu không khớp được, chuyển sang **AI Fuzzy Matching**.
- **Lưu ý:**
  - Nếu dữ liệu của bạn có **cách định danh khác** (ví dụ: sử dụng `invoice_number` thay vì `transaction_id`), cần **chỉnh sửa code** trong node này.
  - **Mở node Code** → **Edit** → **JavaScript** để xem logic:
    ```javascript
    // Ví dụ logic khớp dựa trên amount và date (tolerable difference)
    const amountDiff = Math.abs(data1.amount - data2.amount) / data1.amount * 100;
    const dateDiff = Math.abs(new Date(data1.date) - new Date(data2.date)) / (1000 * 60 * 60 * 24);
    return amountDiff < 5 && dateDiff < 3; // Khớp nếu amount khác nhau <5% và date khác nhau <3 ngày
    ```

---

### **3. Kích Hoạt ⚡️ Workflow**
1. **Test Run với Dữ Liệu Mẫu:**
   - Gửi **dữ liệu mẫu** qua Webhook (ví dụ như trong phần **Node 1**).
   - Kiểm tra **log** trong n8n Editor để xem workflow chạy như thế nào.
   - **Cập nhật các node cần thiết** (nếu có sai sót).

2. **Bật Active Workflow:**
   - Nhấn **Active** trên nút ở góc trên bên phải.
   - **Không quên** kiểm tra **Slack** và **Google Sheets** để xác nhận dữ liệu đã được khớp.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**
### **1. Tối Ưu Hóa AI Fuzzy Matching**
- **Cải thiện prompt** để AI khớp chính xác hơn:
  - Thêm **ví dụ cụ thể** về dữ liệu của bạn vào prompt.
  - Ví dụ:
    ```json
    {
      "instructions": "You are a financial reconciliation AI. Match these transactions based on:
      - Amount (tolerable difference: 5%)
      - Date (tolerable difference: 3 days)
      - Description (if amount/date not matching)
      Example:
      Input 1: { 'amount': 1000000, 'date': '2024-05-20', 'description': 'Thanh toán điện' }
      Input 2: { 'amount': 1050000, 'date': '2024-05-21', 'description': 'Payment for electricity' }
      Output: MATCH (Confidence: 95%)"
    }
    ```
- **Test với dữ liệu thực tế** trước khi áp dụng toàn bộ.

### **2. Lưu Log Chi Tiết**
- **Thêm node `Set`** sau `Log to Google Sheets` để lưu **dữ liệu chi tiết** vào một sheet khác:
  ```json
  {
    "jsonata": "$",
    "operation": "appendOrUpdate",
    "sheetName": "detailed_logs"
  }
  ```
- **Sử dụng node `Code`** để **xóa dữ liệu cũ** sau 30 ngày (để tránh sheet quá lớn).

### **3. Gửi Báo Cáo Định Kỳ**
- **Sử dụng node `Schedule`** (n8n Pro) để **gửi báo cáo hàng tháng**:
  1. Thêm node **Schedule** (nhập `0 0 1 1 * ?` để chạy hàng tháng ngày 1).
  2. Kết nối với **Google Sheets** để **tạo báo cáo tổng hợp**.
  3. Gửi **báo cáo PDF** qua **Email** hoặc **Slack**.

### **4. Kết Hợp Với ERP**
- **Nếu ERP của bạn có API** (SAP, Odoo, QuickBooks...), cấu hình **Webhook từ ERP** để tự động gửi dữ liệu vào workflow.
- **Ví dụ với Odoo:**
  - Tạo **Webhook** trong Odoo (Settings → Technical → Webhooks).
  - Chọn **event** là `invoice.create` hoặc `account.move.create`.
  - Gửi dữ liệu theo **format JSON** mà workflow hỗ trợ.

### **5. Cảnh Báo Sai Lệch**
- **Thêm node `Set`** sau `Calculate Confidence Scores` để **cảnh báo** khi điểm tin cậy thấp:
  ```json
  {
    "jsonata": "$[*].confidence_score < 70",
    "operation": "appendOrUpdate",
    "sheetName": "alerts"
  }
  ```
- **Gửi thông báo Slack** khi có **sai lệch lớn**:
  ```json
  {
    "text": "⚠️ High discrepancy detected: {{ $item.amount }} (Confidence: {{ $item.confidence_score }}%)",
    "username": "Finance Bot"
  }
  ```

---

## 📌 **Kết Luận: Áp Dụng Ngay Hôm Nay!**
Workflow này **giải phóng thời gian** cho bộ phận tài chính, **giảm sai sót**, và **tự động hóa khớp lại** hóa đơn, bảng cân đối, và ERP **không cần code**.

### **Bước Đầu Tiên:**
1. **Đăng ký VPS** với [TinoHost](https://tino.vn/vps-n8n?affid=388) (mã giảm **VPSN8N**) hoặc [BNIX](https://my.bnix.one/aff.php?aff=172).
2. **Import workflow** và cấu hình **OpenAI, Google Sheets, Slack**.
3. **Test với dữ liệu mẫu** và **bật Active**.
4. **Xem kết quả** trên Google Sheets và Slack!

**💡 Mẹo