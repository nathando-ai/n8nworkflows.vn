---
title: "🔍 Tự Động Hóa OCR PDF, DOCX & Hình Ảnh qua Mistral + Google Drive + Slack (Không Cần Code)"
description: "Workflow tự động hóa OCR cho PDF, DOCX và hình ảnh từ Google Drive, xử lý bằng Mistral AI, lưu kết quả vào Google Drive và báo cáo Slack. Giúp tiết kiệm thời gian 80% trong việc chuẩn bị dữ liệu cho RAG, dịch vụ AI hoặc phân tích nội dung."
slug: "tieu-dong-hoa-ocr-pdf-docx-hinh-anh-google-drive-mistral-slack"
tags: [n8n, automation, no-code, mistral-ai, google-drive, slack, ocr, content-creation, multimodal-ai]
keywords: [n8n workflow ocr, tự động hóa OCR PDF, Mistral AI Google Drive, tự động hóa nội dung, lưu trữ Markdown từ OCR, báo cáo Slack tự động]
---

# 🚀 **Tự Động Hóa OCR PDF, DOCX & Hình Ảnh với Mistral + Google Drive + Slack**

## **Giải Pháp Cho Nỗi Đau Của Các Sếp**
Bạn đã bao giờ phải tốn **giờ đồng hồ** để quét, chuyển đổi và chuẩn bị dữ liệu từ PDF, DOCX hoặc hình ảnh để sử dụng trong **RAG (Retrieval-Augmented Generation)**, dịch vụ AI, hoặc phân tích nội dung? Hoặc phải **lặp đi lặp lại** việc kiểm tra độ chính xác của OCR bằng tay?

Workflow này **tự động hóa toàn bộ quy trình** từ khi file mới được tải lên Google Drive đến khi kết quả OCR được lưu trữ sẵn trong Google Drive và báo cáo Slack. **Không cần viết một dòng code**, chỉ cần cấu hình và chạy 24/7!

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian 80%** so với cách làm thủ công.
- **Chuẩn bị dữ liệu sẵn sàng** cho RAG, dịch vụ AI, hoặc phân tích nội dung.
- **Lưu trữ kết quả** trong Google Drive với định dạng **Markdown (MD)** và **JSON** để dễ dàng xử lý tiếp.
- **Báo cáo tự động** trên Slack khi hoàn thành hoặc gặp lỗi.
- **Theo dõi tiến trình** qua Google Sheets với thời gian bắt đầu, hoàn thành và trạng thái.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Google** với quyền truy cập API (để sử dụng Google Drive & Sheets).
2. **Tài khoản Mistral Cloud** và **API Key** (để thực hiện OCR).
3. **Tài khoản Slack** và **OAuth Credentials** (để gửi thông báo).
4. **Google Drive Folder** để theo dõi file mới (input) và lưu kết quả (output).
5. **Google Sheet** với cấu trúc đã định sẵn (xem [Google Sheets Configuration](#google-sheets-configuration)).
6. **n8n Self-hosted** (để chạy workflow 24/7 ổn định).
   :::info[Gợi ý hạ tầng cho n8n]
   Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
   👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
   👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
   :::
:::

---

## **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Tải workflow từ [n8n.io/workflows/9084](https://n8n.io/workflows/9084).
2. Nhấn **Import Workflow** và chọn file JSON.
3. Hoặc copy toàn bộ JSON và dán vào **Import Workflow** trong n8n.

---

### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**

#### **A. Cấu Hình Credentials**
Workflow sử dụng **5 loại credentials** chính:
1. **Google Drive OAuth2** (để theo dõi file mới và lưu kết quả).
2. **Google Sheets OAuth2** (để ghi log vào bảng tính).
3. **Mistral Cloud API** (để thực hiện OCR).
4. **Slack OAuth2** (để gửi thông báo).

👉 **Hướng dẫn chi tiết**:
- **Google Drive & Sheets**:
  - Tạo **Google OAuth Credentials** trong n8n (n8n.io → Credentials → Add Credential → Google OAuth2).
  - Chọn **Google Drive API** và **Google Sheets API**.
  - Cấu hình quyền truy cập: `https://www.googleapis.com/auth/drive` và `https://www.googleapis.com/auth/spreadsheets`.
- **Mistral Cloud**:
  - Tạo **Mistral Cloud Credentials** trong n8n.
  - Điền **API Key** từ tài khoản Mistral Cloud.
- **Slack**:
  - Tạo **Slack OAuth2 Credentials** trong n8n.
  - Chọn **Slack Workspace** và cấp quyền `chat:write` (để gửi thông báo).

#### **B. Cấu Hình Node Quan Trọng**
| **Node** | **Cần Chỉnh Sửa Gì?** | **Lưu Ý** |
|----------|----------------------|------------|
| **File Created / File Updated** | Thiết lập `Folder` (ID của folder Google Drive cần theo dõi). | Lấy ID folder từ URL: `https://drive.google.com/drive/folders/abc123...` |
| **Workflow Configuration** | Điền `google_sheet_id` và `dest_folder_id`. | `google_sheet_id` lấy từ URL Google Sheet: `https://docs.google.com/spreadsheets/d/abc123...` |
| **OCR Document** | Chọn `mistralCloudApi` credentials. | Đảm bảo API Key Mistral đúng và có hạn mức sử dụng. |
| **Slack Nodes** | Chọn channel Slack và cấu hình credentials. | Có thể chọn channel khác cho `Send Success Message` và `Send Error Message`. |

#### **C. Cấu Trúc Google Sheets**
Workflow yêu cầu **Google Sheet** có tên là **"Files"** với các cột sau:
| **Cột** | **Mô Tả** |
|---------|------------|
| **File Name** | Tên file input. |
| **File** | Link copy file input. |
| **Directory** | Link folder output. |
| **JSON File** | Link file JSON kết quả OCR. |
| **MD File** | Link file Markdown kết quả OCR. |
| **Started** | Thời gian bắt đầu xử lý. |
| **Completed** | Thời gian hoàn thành. |
| **Status** | Trạng thái (`Started`, `Done`, `Unsupported Type`). |

👉 **Cách lấy `google_sheet_id`**:
1. Mở Google Sheet trong trình duyệt.
2. URL sẽ có dạng: `https://docs.google.com/spreadsheets/d/abc123.../edit`.
3. `abc123...` là `google_sheet_id`.

👉 **Cách lấy `dest_folder_id`**:
1. Mở folder Google Drive trong trình duyệt.
2. URL sẽ có dạng: `https://drive.google.com/drive/folders/abc123...`.
3. `abc123...` là `dest_folder_id`.

---

### **3. Kích Hoạt ⚡️**
1. **Test Run** với một file mẫu (PDF/DOCX/Hình ảnh) để kiểm tra workflow.
2. **Bật Active** workflow sau khi cấu hình xong.
3. **Kiểm tra Slack** và Google Sheets để xác nhận kết quả.

---

## **✍️ Mẹo & Gợi Ý Nâng Cao**
1. **Tách file lớn thành nhiều trang**:
   - Nếu file PDF/DOCX quá lớn, workflow sẽ tự động **tách thành nhiều trang** và lưu từng trang thành file Markdown riêng.
2. **Lưu log chi tiết**:
   - Kết quả OCR được lưu dưới dạng **JSON** và **Markdown** trong Google Drive, dễ dàng xử lý tiếp.
3. **Báo cáo định kỳ**:
   - Có thể kết hợp với **n8n Schedule Node** để gửi báo cáo tổng hợp hàng tuần.
4. **Kết hợp với AI khác**:
   - Sau khi OCR xong, có thể **gửi dữ liệu vào LLM** (như Mistral, Llama) để tổng hợp hoặc dịch văn bản.
5. **Tự động xóa file cũ**:
   - Thêm **Google Drive Node** để xóa file input sau khi xử lý xong (nếu không cần lưu lại).

---

## **📌 Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc lặp đi lặp lại trong việc OCR và chuẩn bị dữ liệu. **Không cần code**, chỉ cần cấu hình và chạy 24/7.

👉 **Bắt đầu ngay hôm nay!**
1. Cài đặt **n8n Self-hosted** trên VPS.
2. Import workflow và cấu hình credentials.
3. **Chạy và theo dõi kết quả** trên Slack & Google Sheets.

**Nếu gặp vấn đề**, các sếp có thể liên hệ tác giả Yves Tkaczyk qua [LinkedIn](https://www.linkedin.com/in/ytkaczyk/) hoặc [Forum n8n](https://community.n8n.io/).

---
**🚀 Hãy tự động hóa OCR ngay hôm nay và tập trung vào những việc quan trọng hơn!**