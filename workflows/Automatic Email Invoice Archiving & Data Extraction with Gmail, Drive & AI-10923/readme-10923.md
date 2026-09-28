---
title: "💰 **Tự Động Hoá Lưu Trữ & Trích Xuất Dữ Liệu Hóa Đơn qua Email, Google Drive & AI (N8n)**"
description: "Workflow tự động hóa hoàn toàn không cần code để tự động thu thập hóa đơn từ email, lưu trữ PDF lên Google Drive/SFTP, trích xuất dữ liệu quan trọng bằng AI, và ghi log vào Google Sheets. Giúp các sếp tiết kiệm 10+ giờ/tháng và giảm thiểu lỗi thủ công."
slug: "tieu-dong-hoa-luu-tru-trich-xuat-hoa-don-gmail-google-drive-ai"
tags: [n8n, automation, invoice processing, ai-summarization, google-sheets, gmail, google-drive, sftp]
keywords: [n8n workflow hóa đơn, tự động hóa hóa đơn, trích xuất dữ liệu hóa đơn bằng AI, lưu trữ hóa đơn Google Drive, lưu hóa đơn SFTP, tự động hóa tài chính]
---

# 🚀 **Tự Động Hoá Lưu Trữ & Trích Xuất Dữ Liệu Hóa Đơn qua Email, Google Drive & AI**

## **🔥 Nỗi Đau Của Các Sếp Và Giải Pháp Tự Động Hóa**
Hàng tháng, các sếp phải mất **10-15 giờ** để:
- **Lọc và tải xuống** hóa đơn từ email (thường là từ ISP, nhà cung cấp dịch vụ, hoặc nhà cung cấp vật liệu).
- **Lưu trữ** hóa đơn PDF vào thư mục rối ren trên máy tính hoặc Google Drive.
- **Nhập thủ công** dữ liệu (ngày, nhà cung cấp, tổng tiền, chi tiết) vào Excel/Google Sheets.
- **Lo lắng** về việc mất hóa đơn hoặc nhập sai dữ liệu, dẫn đến sai sót trong kế toán.

**Workflow này giải quyết tất cả!** Nó tự động:
✅ **Thu thập** hóa đơn từ email (chỉ lọc những email có PDF).
✅ **Lưu trữ** hóa đơn lên **Google Drive** (và **SFTP** nếu cần).
✅ **Trích xuất dữ liệu** (ngày, nhà cung cấp, tổng tiền, chi tiết) bằng **AI**.
✅ **Ghi log** vào **Google Sheets** để theo dõi và phân tích.

---
### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**LỢI ÍCH CỐT LÕI**]
- **Tiết kiệm 10-15 giờ/tháng** (hoặc hơn) cho việc xử lý hóa đơn.
- **Giảm thiểu lỗi 100%** (không còn nhập sai ngày, tên nhà cung cấp, hoặc tổng tiền).
- **Dữ liệu sẵn sàng phân tích** trên Google Sheets (vẽ biểu đồ tiêu thụ, theo dõi chi phí định kỳ).
- **Lưu trữ an toàn** trên Google Drive + SFTP (nếu cần sao lưu).
- **Hoạt động 24/7** mà không cần can thiệp của con người.
:::

---
### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Gmail** (để lấy hóa đơn từ email).
2. **Tài khoản Google Drive** (để lưu trữ PDF).
3. **Tài khoản SFTP** (tùy chọn, nếu muốn sao lưu lên máy chủ).
4. **API Key của OpenRouter/OpenAI** (để sử dụng AI trích xuất dữ liệu).
5. **Google Sheets** (để ghi log dữ liệu trích xuất).

:::info[**Gợi ý hạ tầng cho n8n**]
Để workflow chạy **ổn định 24/7**, các sếp nên cài **n8n trên VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới **39%**).
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172).
:::

---
## **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
Các sếp có thể:
- **Tải file JSON** từ [n8n.io/workflows/10923](https://n8n.io/workflows/10923) và import vào **n8n Editor**.
- **Copy/paste JSON** từ file vào **n8n Editor** (tab `Import`).

### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này gồm **14 node** quan trọng, các sếp cần cấu hình như sau:

#### **📌 SECTION 1: Trigger (Bật/Dừng Lịch Làm Việc)**
- Node: **`Schedule Trigger`**
- **Cấu hình:**
  - Chọn **interval** (ví dụ: **daily at 8 AM** để chạy hàng ngày lúc 8h sáng).
  - Lưu ý: Nếu muốn chạy **ngay lập tức**, chọn **`Run now`**.

#### **📌 SECTION 2: Lọc Email Hóa Đơn & Kiểm Tra File PDF**
- Node: **`Gmail → Get Many Messages`** (lọc email từ nhà cung cấp hóa đơn).
- **Cấu hình:**
  - **Sender Email:** Nhập **email của nhà cung cấp** (ví dụ: `invoice@isp.com`).
  - **Credentials:** Chọn **`gmailOAuth2`** (cần thiết lập trước).
  - **Filter:** Chỉ lấy email có **PDF attachment** (node **`Filter-contains_attachment`** sẽ xử lý).

#### **📌 SECTION 3: Tải Xuống & Lưu Trữ PDF**
- **Node 1: `Gmail → Download File`** (tải PDF từ email).
- **Node 2: `Google Drive → Upload File`** (lưu PDF lên Google Drive).
  - **Cấu hình:**
    - **Folder ID:** Nhập **ID thư mục** của Google Drive (để lưu hóa đơn).
    - **Credentials:** Chọn **`googleDriveOAuth2Api`**.
- **Node 3 (Tùy Chọn): `FTP → Upload File`** (sao lưu lên SFTP).
  - **Cấu hình:**
    - **Host:** Địa chỉ SFTP của bạn.
    - **Path:** Thư mục lưu trữ (ví dụ: `/invoices/`).
    - **Credentials:** Chọn **`sftp`** (cần thiết lập trước).

#### **📌 SECTION 4: Trích Xuất Text từ PDF**
- Node: **`Extract from File1`** (chuyển PDF thành text).
  - **Lưu ý:** Chỉ hoạt động tốt với **PDF text-based** (không phải PDF hình ảnh).

#### **📌 SECTION 5: Trích Xuất Dữ Liệu Bằng AI**
- Node: **`OpenRouter Chat Model1`** (sử dụng AI trích xuất dữ liệu).
  - **Cấu hình:**
    - **API Key:** Nhập **OpenRouter API Key** (hoặc OpenAI).
    - **Model:** Chọn mô hình như **GPT-4.1** hoặc **Llama 3**.
    - **Prompt:** Workflow đã cấu hình sẵn, **không cần chỉnh sửa**.
- Node: **`Code_extractFields`** (sắp xếp dữ liệu thành JSON).
  - **Lưu ý:** Node này **không cần chỉnh sửa**, chỉ đảm bảo **AI trả về dữ liệu đúng định dạng**.

#### **📌 SECTION 6: Ghi Log vào Google Sheets**
- Node: **`GoogleSheets_save`** (ghi dữ liệu vào Sheets).
  - **Cấu hình:**
    - **Document ID:** Nhập **ID file Google Sheets** (tìm trong URL: `https://docs.google.com/spreadsheets/d/[ID]/edit`).
    - **Sheet Name:** Tên **tab** trong Sheets (ví dụ: `Hóa Đơn`).
    - **Columns cần thiết:**
      | **Vendor** (Nhà cung cấp) | **Type** (Loại hóa đơn) | **Date** (Ngày) | **Amount** (Tổng tiền) |
      |---------------------------|------------------------|-----------------|-----------------------|
    - **Credentials:** Chọn **`googleApi`**.

#### **📌 SECTION 7: Xóa Email & File (Tùy Chọn)**
- Node: **`Delete a message`** (xóa email sau khi xử lý).
- Node: **`Delete a file1`** (xóa file tạm trên Google Drive).
- **Lưu ý:** **Không bắt buộc**, nhưng giúp **giảm rác rưởi**.

---
### **⚡ Kích Hoạt Workflow**
1. **Test Run** với **1 email mẫu** để kiểm tra:
   - Dữ liệu trích xuất có chính xác không?
   - File PDF có lưu được không?
   - Dữ liệu có ghi vào Sheets không?
2. **Bật `Active`** nếu mọi thứ hoạt động ổn.

---
## **✍️ Mẹo & Gợi Ý Nâng Cao**
1. **Sử dụng nhiều nhà cung cấp khác nhau**
   - Thêm **nhiều email sender** vào node **`Gmail → Get Many Messages`** để xử lý hóa đơn từ nhiều nguồn (ISP, nhà cung cấp điện, nước, internet...).

2. **Lưu log hoạt động**
   - Thêm node **`Slack/Telegram Notification`** để nhận thông báo khi workflow chạy thành công/thất bại.

3. **Tạo báo cáo định kỳ**
   - Sử dụng **Google Sheets + Apps Script** để tự động tạo **báo cáo tiêu thụ chi phí** hàng tháng.

4. **Sao lưu dữ liệu**
   - Nếu lưu trữ trên **SFTP**, các sếp có thể **kết hợp với AWS S3** để sao lưu thêm.

5. **Cập nhật AI Model**
   - Nếu AI trích xuất sai, thử **mô hình khác** (ví dụ: **Llama 3** thay vì GPT-4).

---
## **📌 Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi việc **nhập thủ công hóa đơn**, đồng thời **giảm thiểu lỗi** và **tự động hóa toàn bộ quy trình tài chính**. Với **AI trích xuất dữ liệu**, các sếp có thể **theo dõi chi tiêu một cách chính xác** và **phân tích tiêu thụ** trên Google Sheets.

**🚀 Hãy áp dụng ngay và tiết kiệm thời gian cho công việc quan trọng hơn!**

---
### **🔗 Tài Liệu Tham Khảo**
- [Full Setup Guide (Tiếng Anh)](https://paoloronco.it/n8n-template-automated-invoice-archiving/)
- [Hướng Dẫn Cài Đặt Gmail Node](https://docs.n8n.io/integrations/builtin/app-nodes/n8n-nodes-base.gmail/)
- [Hướng Dẫn Cài Đặt Google Drive Node](https://docs.n8n.io/integrations/builtin/app-nodes/n8n-nodes-base.googledrive/)
- [Hướng Dẫn Cài Đặt OpenRouter API](https://openrouter.ai/docs)