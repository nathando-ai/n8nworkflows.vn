---
title: "💰 Tự Động Hóa Xử Lý Hóa Đơn Từ Outlook Bằng AI: Giảm 100+ Giờ Công Manual Cho Bộ Tài Chính"
description: "Workflow này tự động nhận, phân loại và trích xuất dữ liệu từ hóa đơn PDF trong Outlook, sau đó ghi vào Excel. Giúp bộ tài chính tiết kiệm thời gian, giảm sai sót và tự động hóa hoàn toàn quy trình xử lý hóa đơn."
slug: "tu-dong-hoa-xu-ly-hoa-don-tu-outlook-bang-ai"
tags: [n8n, automation, finance, ai, outlook, excel, gemini, no-code]
keywords: [tự động hóa hóa đơn, n8n workflow, ai trích xuất hóa đơn, gemini api, excel tự động, xử lý hóa đơn pdf]
---

# 🚀 **Tự Động Hóa Xử Lý Hóa Đơn Từ Outlook Bằng AI: Giảm 100+ Giờ Công Manual Cho Bộ Tài Chính**

### **Nỗi Đau Của Bộ Tài Chính**
Hàng ngày, bộ tài chính phải mất **giờ đồng hồ** để:
- **Lọc và tải** hóa đơn từ Outlook (trong đó có hàng chục email không liên quan).
- **Phân loại** hóa đơn từ các file đính kèm (PDF, image) giữa các loại tài liệu khác (đơn hàng, hợp đồng, báo cáo).
- **Nhập thủ công** dữ liệu vào Excel hoặc hệ thống kế toán, dẫn đến **sai sót và mất thời gian**.

**Workflow này giải quyết tất cả!** Dùng **AI Gemini** để:
✅ **Phân loại tự động** hóa đơn từ email.
✅ **Trích xuất dữ liệu** (số hóa đơn, ngày, tổng tiền, nhà cung cấp) từ PDF.
✅ **Ghi vào Excel** để bộ tài chính kiểm tra và nhập vào hệ thống kế toán.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7**, các sếp nên cài **n8n trên VPS riêng (Self-hosted)** để tránh giới hạn của phiên bản miễn phí.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 100+ giờ/năm** cho bộ tài chính (không cần nhập thủ công).
- **Giảm sai sót** do AI phân loại và trích xuất chính xác hơn con người.
- **Hoạt động liên tục** (không phụ thuộc vào giờ làm việc).
- **Dữ liệu sẵn sàng** để nhập vào hệ thống kế toán (Excel/ERP).
- **Cá nhân hóa** cho từng nhà cung cấp (không cần cấu hình lại).
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi chạy workflow, các sếp cần chuẩn bị:
1. **Tài khoản Microsoft 365** (Outlook + Excel Online) với quyền truy cập vào:
   - **Mailbox** nhận hóa đơn (cần **OAuth2 API Key**).
   - **File Excel** để lưu kết quả (cần **OAuth2 API Key**).
2. **API Key Google Gemini** (miễn phí trong giới hạn):
   - [Đăng ký API Key Gemini](https://makersuite.google.com/app/apikey) (nên chọn **Gemini Pro**).
3. **File Excel mẫu** (cần **tên Sheet** để append dữ liệu).

---
:::info[CHUẨN BỊ]
- **N8n Self-hosted** (không dùng phiên bản miễn phí).
- **Node LangChain** (cần cài đặt từ [n8n.io](https://n8n.io/)).
- **Node HTTP Request** (để gọi API Gemini hiệu quả).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/3396](https://n8n.io/workflows/3396).
- **Nhấn "Import"** trong n8n Editor.
- **Hoặc copy/paste JSON** từ file vào Editor.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow gồm **18 node**, các sếp cần chú ý cấu hình **các node quan trọng** sau:

##### **A. Cấu Hình Outlook (Lấy Email & Đính Kèm)**
- **Node: "Get Recent Messages"** (Microsoft Outlook)
  - **Credentials**: Chọn `microsoftOutlookOAuth2Api`.
  - **Tham số**:
    - `folderId`: ID của folder nhận hóa đơn (thường là `inbox`).
    - `filter`: `"isRead eq false"` (lọc email chưa đọc) **hoặc** `"receivedDateTime ge datetime'2024-01-01T00:00:00Z'"` (lọc email mới nhất).
  - **Lưu ý**: Nếu dùng **folder chia sẻ**, bật `shared folder` và nhập **email chủ folder**.

- **Node: "Download Attachments"** (Microsoft Outlook)
  - **Credentials**: Cùng với `Get Recent Messages`.
  - **Tham số**:
    - `operation`: `get` (tải tất cả đính kèm).
    - **Lưu ý**: Nếu email có nhiều đính kèm, **node "Split Attachments"** sẽ chia thành batch.

##### **B. Phân Loại Hóa Đơn Bằng AI (Gemini)**
- **Node: "Message Classifier"** (Text Classifier)
  - **Prompt mẫu** (cần chỉnh sửa):
    ```plaintext
    Is this email an invoice? Reply with "YES" if it contains an invoice attachment, otherwise "NO".
    ```
  - **Lưu ý**: Nếu AI phân loại sai, **cần điều chỉnh prompt** hoặc thêm **keyword cụ thể** (ví dụ: "INVOICE", "FACTURE").

- **Node: "Invoice Classifier With Gemini 2.0"** (HTTP Request)
  - **URL API**: `https://generativelanguage.googleapis.com/v1/models/gemini-pro:generateContent`
  - **Headers**:
    ```json
    {
      "Content-Type": "application/json",
      "Authorization": "Bearer YOUR_GOOGLE_API_KEY"
    }
    ```
  - **Body (JSON)**:
    ```json
    {
      "contents": [
        {
          "parts": [
            {
              "text": "Is this PDF an invoice? Extract key details if yes."
            }
          ]
        },
        {
          "parts": [
            {
              "inlineData": {
                "mimeType": "application/pdf",
                "data": "{{$node["Extract from File"].json["binary"]}}"
              }
            }
          ]
        }
      ]
    }
    ```
  - **Lưu ý**:
    - **Node "Extract from File"** phải được cấu hình trước để lấy **binary của PDF**.
    - **`generationConfig`** (để AI trả về JSON) cần được cấu hình trong **body API**.

##### **C. Trích Xuất Dữ Liệu & Ghi Vào Excel**
- **Node: "Microsoft Excel 365"** (Append)
  - **Credentials**: `microsoftExcelOAuth2Api`.
  - **Tham số**:
    - `resource`: `worksheet` (tên sheet trong Excel).
    - **Cấu trúc dữ liệu**: Dữ liệu từ Gemini phải được **format thành JSON** để Excel nhận được (ví dụ: `{"invoiceNumber": "INV-123", "amount": 1000000}`).

---
#### **3. Kích Hoạt ⚡️**
1. **Test Run** với **email mẫu** (có hóa đơn PDF đính kèm).
2. **Kiểm tra**:
   - AI có phân loại đúng không?
   - Dữ liệu trích xuất có chính xác không?
   - Excel có append dữ liệu không?
3. **Bật Active** workflow.

---
### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Lọc Email Trùng Lặp**
   - Thêm **node "Filter"** sau `Get Recent Messages` với điều kiện:
     ```json
     {{ $json["subject"].toLowerCase().includes("invoice") }}
     ```
   - **Hoặc** dùng **node "Remove Duplicates"** (nếu email cùng nội dung).

2. **Gửi Báo Cáo Định Kỳ**
   - Thêm **node "Schedule Trigger"** để gửi **báo cáo hàng tuần** về số hóa đơn đã xử lý qua **Slack/Email**.
   - **Ví dụ**:
     ```json
     {
       "cron": "0 0 * * 1", // Thứ 2 hàng tuần
       "payload": {
         "message": "Tổng số hóa đơn xử lý tuần trước: {{ $node["Microsoft Excel 365"].json.length }}"
       }
     }
     ```

3. **Kết Nối Với Hệ Thống Kế Toán**
   - Thay **Excel** bằng **node "HTTP Request"** để gửi dữ liệu đến **API của QuickBooks/Xero** hoặc **ERP nội bộ**.

4. **Optimize API Gemini**
   - Nếu workflow bị **rate limit**, chia **batch PDF** nhỏ hơn (sử dụng **node "Split In Batches"**).

---
### 📌 **Kết Luận**
Workflow này **giải phóng bộ tài chính khỏi công việc nhàn nhạt**, giúp:
✔ **Tiết kiệm thời gian** (không cần nhập thủ công).
✔ **Tăng độ chính xác** (AI phân loại và trích xuất tốt hơn con người).
✔ **Hoạt động tự động** (không phụ thuộc vào giờ làm).

**Hành động ngay!**
1. **Import workflow** từ [n8n.io/workflows/3396](https://n8n.io/workflows/3396).
2. **Cấu hình Outlook + Gemini API**.
3. **Test với email mẫu** và **bật Active**.

**Cần hỗ trợ?**
- **Join Discord n8n**: [https://discord.com/invite/XPKeKXeB7d](https://discord.com/invite/XPKeKXeB7d)
- **Hỏi trên Forum**: [https://community.n8n.io/](https://community.n8n.io/)

---
**Happy Automating!** 🚀