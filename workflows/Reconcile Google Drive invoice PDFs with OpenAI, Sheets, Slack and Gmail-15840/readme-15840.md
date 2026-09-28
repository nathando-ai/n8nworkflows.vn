---
title: "📄 Tự Động Hóa Xác Nhận Hoá Đơn PDF từ Google Drive: AI + Sheets + Slack + Email (N8N)"
description: "Workflow tự động hóa hoàn toàn không cần code để trích xuất dữ liệu từ hóa đơn PDF trên Google Drive, tự động ghi nhật ký, cảnh báo hóa đơn quá hạn trên Slack và gửi báo cáo tuần cho bộ phận Tài chính. Giúp tiết kiệm 10-15 giờ công mỗi tháng cho bộ phận kế toán."
slug: "tieu-dong-hoa-xac-nhan-hoa-don-pdf-google-drive"
tags: [n8n, automation, invoice processing, ai-summarization, google-drive, google-sheets, slack, gmail, openai]
keywords: [tự động hóa hóa đơn PDF, n8n workflow, trích xuất dữ liệu hóa đơn, AI xử lý hóa đơn, báo cáo tự động hóa tài chính]
---

# 🚀 **Tự Động Hóa Xác Nhận Hoá Đơn PDF: Từ Google Drive Đến Báo Cáo Tài Chính Mỗi Tuần**

### **🔥 Nỗi Đau Của Các Sếp Kế Toán**
Hàng ngày, bộ phận Tài chính phải:
- **Tải xuống và phân loại** hàng chục hóa đơn PDF từ Google Drive.
- **Nhập thủ công** dữ liệu vào Google Sheets, gây ra sai sót và mất thời gian.
- **Quên kiểm tra hóa đơn quá hạn**, dẫn đến phạt lãi và mất uy tín.
- **Tạo báo cáo tuần** để báo cáo cho lãnh đạo, nhưng lại phải làm thủ công mỗi tuần.

**Workflow này giải quyết tất cả!** Với AI + N8N, các sếp sẽ:
✅ **Tự động trích xuất** dữ liệu từ hóa đơn PDF (vendor, số hóa đơn, ngày hết hạn, tổng tiền).
✅ **Ghi nhật ký** tất cả hóa đơn vào Google Sheets với định dạng chuẩn.
✅ **Cảnh báo Slack** khi có hóa đơn quá hạn.
✅ **Gửi báo cáo tuần tự động** qua email cho bộ phận Tài chính.

---
## 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10-15 giờ công/tháng** cho bộ phận kế toán.
- **Giảm sai sót** do nhập liệu thủ công xuống 0%.
- **Cảnh báo kịp thời** hóa đơn quá hạn, tránh phạt lãi.
- **Báo cáo tự động** mỗi tuần, không cần làm thủ công.
- **Hoạt động 24/7** mà không cần can thiệp của con người.
:::

---
## 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Google Drive** (để lưu hóa đơn và kích hoạt trigger).
2. **Google Sheets** (để lưu nhật ký hóa đơn, có sẵn 1 sheet mẫu).
3. **Tài khoản Slack** (để gửi cảnh báo hóa đơn quá hạn).
4. **Tài khoản Gmail** (để gửi báo cáo tuần cho bộ phận Tài chính).
5. **API Key OpenAI** (để sử dụng AI trích xuất dữ liệu).
6. **VPS Self-hosted n8n** (để workflow chạy 24/7, không bị giới hạn free plan).

👉 **🎁 Mã giảm giá VPS cho n8n:**
- [TinoHost](https://tino.vn/vps-n8n?affid=388) (Mã: **VPSN8N** - giảm tới 39%)
- [BNIX](https://my.bnix.one/aff.php?aff=172) (VPS Xeon 4GB chỉ **50k/tháng**)
:::

---
## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
Các sếp có thể:
- **Tải file JSON** từ [n8n.io/workflows/15840](https://n8n.io/workflows/15840) và import vào n8n Editor.
- **Copy JSON** từ link trên và dán vào **Import Workflow** trong n8n.

:::note[LƯU Ý]
- **Không sử dụng free plan** của n8n.io vì workflow này cần chạy liên tục.
- **Cài đặt n8n trên VPS** để đảm bảo hoạt động 24/7.
:::

---

### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này gồm **11 node**, các sếp cần chú ý cấu hình các node sau:

#### **🔹 Node 1: Google Drive Trigger1 (Google Drive Trigger)**
- **Chọn credentials**: `googleDriveOAuth2Api`.
- **Cấu hình**:
  - **Folder ID**: Thay bằng ID của folder lưu hóa đơn trên Google Drive.
  - **File types**: Chỉ chọn `PDF` (`.pdf`).
  - **Event types**: Chỉ chọn `File created`.

#### **🔹 Node 2 & 3: Download file1 (Google Drive) + Extract from File1 (Extract from File)**
- **Credentials**: `googleDriveOAuth2Api`.
- **Lưu ý**:
  - Node **Extract from File** chỉ hoạt động với **PDF có văn bản** (không phải scanned PDF).
  - Nếu hóa đơn là scanned, cần sử dụng **OCR** (như Google Vision API) trước khi trích xuất.

#### **🔹 Node 4 & 7: Code Split PDF + Code Parse and Enrich Invoice Data**
- **Không cần chỉnh sửa** nếu các sếp đã import file JSON chính xác.
- **Lưu ý**:
  - Node **Code Split PDF** chia hóa đơn thành từng mục riêng.
  - Node **Code Parse and Enrich** tự động tính toán ngày quá hạn và trạng thái thanh toán.

#### **🔹 Node 5 & 6: AI Agent + OpenAI Chat Model**
- **Credentials**: Không cần (sử dụng API Key OpenAI).
- **Cấu hình**:
  - **Model**: Chọn `gpt-4o-mini` (nếu có) hoặc `gpt-3.5-turbo` (mặc định).
  - **API Key**: Điền vào **Settings > OpenAI API Key** trong n8n.

#### **🔹 Node 8: Google Sheets Append to Invoice Log**
- **Credentials**: `googleSheetsOAuth2Api`.
- **Cấu hình**:
  - **Sheet Name**: Điền tên sheet lưu nhật ký (ví dụ: `Invoice_Log`).
  - **Headers**: Đảm bảo các cột trong sheet phù hợp với dữ liệu AI trích xuất (vendor, invoice number, due date, amount, status).

#### **🔹 Node 10: Slack Alert Finance on Overdue Invoices**
- **Credentials**: `slackOAuth2Api`.
- **Cấu hình**:
  - **Channel**: Chọn `#finance-alerts` (hoặc channel tương tự).
  - **Message Template**: Có thể chỉnh sửa để phù hợp với cách thông báo của bộ phận.

#### **🔹 Node 11 & 12: Code Generate Weekly Summary Stats + Gmail Email Weekly Report**
- **Credentials**:
  - **Gmail**: `gmailOAuth2`.
  - **Email**: Điền địa chỉ email của bộ phận Tài chính (ví dụ: `finance@company.com`).
- **Lưu ý**:
  - Node **Code Generate Weekly Summary Stats** tự động tính toán tổng số hóa đơn, tổng tiền, số hóa đơn quá hạn.
  - Node **Gmail** sẽ gửi báo cáo **mỗi thứ 7** (hoặc ngày tùy chỉnh).

---

### **3. Kích Hoạt ⚡️**
1. **Test Run** với 1-2 hóa đơn mẫu để kiểm tra:
   - AI có trích xuất dữ liệu chính xác không?
   - Slack có cảnh báo hóa đơn quá hạn không?
   - Email báo cáo có gửi đúng không?
2. **Bật Active** workflow sau khi kiểm tra thành công.

---
## ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::tip[CÁCH LÀM NGOÀI THƯỜNG]
1. **Kết hợp với Google Calendar**:
   - Sử dụng **Google Drive Trigger** để kích hoạt workflow vào ngày đầu tuần (thứ 7) để gửi báo cáo.
2. **Lưu log hoạt động**:
   - Thêm node **StickyNote** để ghi lại lỗi hoặc thông tin debug.
3. **Cảnh báo qua Telegram**:
   - Thay vì Slack, có thể sử dụng **Telegram Bot** để cảnh báo qua tin nhắn.
4. **Tích hợp với ERP**:
   - Nếu công ty sử dụng **SAP, QuickBooks, hoặc Zoho Books**, có thể kết nối node **HTTP Request** để đẩy dữ liệu vào hệ thống.
5. **Tự động thanh toán**:
   - Nếu có API thanh toán (như **Stripe, PayPal**), có thể thêm node **HTTP Request** để tự động tạo đơn thanh toán.
:::

---
## 📌 **Kết Luận**
Workflow này **giải phóng bộ phận Tài chính** khỏi công việc nhắc nhở, nhập liệu và báo cáo thủ công. Với **AI + N8N**, các sếp sẽ:
✔ **Tiết kiệm thời gian** (10-15 giờ/tháng).
✔ **Giảm sai sót** (0% lỗi nhập liệu).
✔ **Cảnh báo kịp thời** hóa đơn quá hạn.
✔ **Báo cáo tự động** mỗi tuần.

**Hãy thử ngay!** Import workflow, cấu hình và **bắt đầu tự động hóa hóa đơn của mình** trong vòng 15 phút.

---
**🚀 Cần hỗ trợ kỹ thuật?**
- **Đăng ký VPS n8n** với mã giảm giá: [TinoHost](https://tino.vn/vps-n8n?affid=388) (Mã: **VPSN8N**)
- **Hỏi đáp cộng đồng n8n**: [n8n Community](https://community.n8n.io/)