---
title: "📄 **Tự Động Hóa Trích Xuất Dữ Liệu Từ Thư Chính Phủ Thái Lan Với OCR Mistral & Lưu Trữ Trên Google Sheets**"
description: "Workflow tự động hóa 100% không code giúp các sếp trích xuất thông tin từ các tệp PDF/JPG/PNG gửi qua LINE hoặc Google Drive, xử lý bằng AI Mistral và OpenAI, sau đó lưu kết quả vào Google Sheets. Giúp tiết kiệm thời gian lên đến 90% trong việc xử lý hồ sơ hành chính."
slug: "tieu-dung-hoa-trich-xuat-du-lieu-thu-chinh-phu-thai-lan"
tags: [n8n, automation, OCR, AI, Google Sheets, LINE Bot, Mistral AI, OpenAI, no-code]
keywords: [n8n workflow tự động hóa, trích xuất dữ liệu từ PDF, OCR Mistral, lưu dữ liệu Google Sheets, tự động hóa LINE Bot, xử lý hồ sơ hành chính]
---

# 🚀 **Tự Động Hóa Trích Xuất Dữ Liệu Từ Thư Chính Phủ Thái Lan Với OCR Mistral & Lưu Trữ Trên Google Sheets**

### **Nỗi Đau Của Các Sếp**
Hàng ngày, các sếp phải mất **giờ đồng hồ** để:
- **Quét và đọc thủ công** các tệp PDF/JPG/PNG từ thư chính phủ Thái Lan.
- **Nhập liệu sai sót** do phải đọc nhiều trang giấy.
- **Quản lý hồ sơ rối loạn** giữa LINE Bot và Google Drive.
- **Không có cách nào tự động** để trích xuất thông tin quan trọng như `book_id`, `subject`, `to`, `date`,...

**Workflow này giải quyết tất cả!** Sử dụng **OCR Mistral AI** để đọc văn bản từ tệp, **OpenAI Information Extractor** để trích xuất dữ liệu chính xác, và **Google Sheets** để lưu trữ tự động. **Không cần viết một dòng code nào!**

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7**, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo tính riêng tư và hiệu suất cao.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới **39%**)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian lên đến 90%** so với cách làm thủ công.
✅ **Trích xuất dữ liệu chính xác** từ PDF/JPG/PNG bằng AI Mistral.
✅ **Lưu trữ tự động** vào Google Sheets với định dạng chuẩn.
✅ **Tự động trả lời LINE Bot** khi nhận được tệp mới.
✅ **Sắp xếp hồ sơ** vào thư mục lưu trữ trên Google Drive.
✅ **Hoạt động liên tục 24/7** mà không cần can thiệp người dùng.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
#### **1. Thông Tin API & Key**
| **Tên**               | **Mô Tả**                                                                 | **Nơi lấy**                                                                 |
|-----------------------|---------------------------------------------------------------------------|-----------------------------------------------------------------------------|
| `LINE_CHANNEL_ACCESS_TOKEN` | Token để kết nối với LINE Bot.                                           | [LINE Developer Console](https://developers.line.biz/)                     |
| `GDRIVE_INVOICE_FOLDER_ID` | ID của thư mục Google Drive để theo dõi tệp mới.                     | [Google Drive API](https://developers.google.com/drive/api/v3/quickstart/python) |
| `MISTRAL_API_KEY`     | API Key để sử dụng Mistral OCR.                                           | [Mistral AI](https://mistral.ai/)                                           |
| `GSHEET_ID`           | ID của Google Sheet để lưu dữ liệu.                                      | [Google Sheets API](https://developers.google.com/sheets/api/guides/quickstart) |

#### **2. Credentials Cần Thiết**
| **Tên**                     | **Mô Tả**                                                                 |
|-----------------------------|---------------------------------------------------------------------------|
| `googleDriveOAuth2Api`      | Credentials để truy cập Google Drive.                                     |
| `googleSheetsOAuth2Api`     | Credentials để truy cập Google Sheets.                                    |
| `openAiApi`                 | Credentials để sử dụng OpenAI Information Extractor.                      |
| `mistralCloudApi`          | Credentials để sử dụng Mistral OCR.                                       |
| `httpHeaderAuth` (LINE)     | Credentials để xác thực với LINE API.                                     |

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể:
- **Tải file JSON** từ [n8n.io/workflows/6702](https://n8n.io/workflows/6702) và import vào **n8n Editor**.
- **Copy JSON** từ trang trên và dán vào **n8n Editor** (tab `Import`).

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
##### **A. Cấu Hình LINE Webhook**
- **Path:** `/line-invoice` (không thay đổi).
- **HTTP Method:** `POST`.
- **Credentials:** Chọn `httpHeaderAuth` (đã cấu hình trước khi import).
- **Test:** Gửi một tệp từ LINE Bot để kiểm tra phản hồi.

##### **B. Cấu Hình Google Drive Trigger**
- **Folder ID:** Điền `$env.GDRIVE_INVOICE_FOLDER_ID` (đã set trong **Environment Variables**).
- **Event:** Chọn `fileCreated`.
- **Test:** Đăng nhập Google Drive và thêm một tệp vào thư mục để kích hoạt workflow.

##### **C. Cấu Hình Mistral OCR**
- **API Key:** Điền `MISTRAL_API_KEY` từ **Environment Variables**.
- **Model:** Sử dụng `mistral-large-latest` (mặc định).
- **Test:** Upload một tệp PDF/JPG để kiểm tra kết quả OCR.

##### **D. Cấu Hình OpenAI Information Extractor**
- **API Key:** Điền `openAiApi` (đã cấu hình trước).
- **Model:** Chọn `gpt-4o-mini` (hoặc `gpt-4-turbo` nếu có).
- **Fields to Extract:** Đảm bảo các trường như `book_id`, `subject`, `to`, `date` được định nghĩa rõ.

##### **E. Cấu Hình Google Sheets**
- **Sheet ID:** Điền `GSHEET_ID` từ **Environment Variables**.
- **Sheet Name:** `data` (mặc định).
- **Columns:** Đảm bảo các cột trong Sheet phù hợp với dữ liệu trích xuất.

##### **F. Cấu Hình LINE Reply**
- **Credentials:** Chọn `httpHeaderAuth` (đã cấu hình).
- **Test:** Sau khi xử lý tệp, LINE Bot sẽ tự động trả lời với thông tin trích xuất.

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run:** Chạy workflow với một tệp mẫu (PDF/JPG) từ LINE hoặc Google Drive.
2. **Kiểm tra Google Sheets:** Đảm bảo dữ liệu đã được lưu chính xác.
3. **Bật Active:** Chuyển workflow sang **Active** để hoạt động liên tục.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết Nối Slack/Telegram:**
   - Thêm node `slack` hoặc `telegramBot` để báo cáo kết quả xử lý.
   - Ví dụ: Khi có tệp mới, gửi thông báo đến Slack với link Google Sheet.

2. **Lưu Log Lịch Sử:**
   - Sử dụng node `set` để lưu thông tin tệp (ngày giờ, người gửi, trạng thái) vào một Google Sheet riêng.
   - Cách làm: Thêm node `googleSheets` mới với Sheet `logs` và cấu hình `operation: append`.

3. **Gửi Báo Cáo Định Kỳ:**
   - Sử dụng **n8n Scheduler** để chạy workflow hàng ngày/tuần để tổng hợp báo cáo từ Google Sheets.
   - Ví dụ: Tạo một báo cáo tổng hợp số lượng tệp xử lý thành công/thất bại.

4. **Xử Lý Tệp Nhiều Trang:**
   - Nếu tệp PDF có nhiều trang, sử dụng **Mistral OCR** kết hợp với **OpenAI** để trích xuất từng trang riêng biệt.
   - Thêm node `split` để chia tệp thành các phần trước khi OCR.

5. **Tự Động Xóa Tệp Sau Xử Lý:**
   - Thêm node `googleDrive` với `operation: delete` để xóa tệp sau khi đã trích xuất dữ liệu.
   - **Lưu ý:** Chỉ áp dụng nếu không cần lưu trữ tệp gốc.

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp cần tự động hóa việc xử lý hồ sơ hành chính từ Thái Lan. Bằng cách kết hợp **OCR Mistral**, **AI OpenAI**, và **Google Sheets**, các sếp không chỉ **tiết kiệm thời gian** mà còn **giảm thiểu sai sót** trong quá trình nhập liệu.

**Hành động ngay hôm nay!**
1. **Import workflow** vào n8n của mình.
2. **Cấu hình các API Key** và credentials.
3. **Test với một tệp mẫu** và bắt đầu tự động hóa!

**Chia sẻ ý kiến** của các sếp về cách tối ưu workflow này thêm nữa! 🚀

---
**🔗 [Tải workflow nguyên bản](https://n8n.io/workflows/6702)**
**📌 [Cài đặt n8n Self-hosted](https://docs.n8n.io/)**