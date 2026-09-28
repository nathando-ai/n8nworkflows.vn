---
title: "📄 **Tự Động Hóa Phân Loại & Chuyển Đổi Hóa Đơn Sang Google Drive Với Slack & AI (Không Cần Code!)**"
description: "Giải pháp tự động hóa hoàn toàn phân loại hóa đơn PDF/PNG/JPEG thành 6 loại: Y tế, Khách sạn, Nhà hàng, Thương mại, Di động và yêu cầu kiểm tra. Tự động lưu vào Google Drive và báo cáo qua Slack khi cần. Tiết kiệm 10+ giờ công mỗi tháng cho bộ phận tài chính!"
slug: "tieu-dong-hoa-phan-loai-hoa-don-google-drive-slack"
tags: [n8n, automation, no-code, google-drive, slack, ai-classification, easybits]
keywords: [tự động hóa hóa đơn, phân loại hóa đơn AI, google drive tự động, slack báo cáo tự động, easybits n8n, workflow n8n không code]
---

# 🚀 **Tự Động Hóa Phân Loại Hóa Đơn & Chuyển Đổi Sang Google Drive Với Slack (Không Cần Code!)**

## **🔥 Nỗi Đau Của Các Sếp Tài Chính Hàng Ngày**
Hàng tháng, bộ phận tài chính phải:
✅ **Phân loại hàng trăm hóa đơn** (PDF/PNG/JPEG) theo loại (y tế, khách sạn, nhà hàng, thương mại, di động...)
✅ **Tìm kiếm và lưu vào Google Drive** theo folder riêng biệt (tốn thời gian và dễ sai sót)
✅ **Kiểm tra lại hóa đơn không rõ ràng** (low confidence) và gửi yêu cầu review qua Slack/Email
✅ **Báo cáo lỗi hoặc hóa đơn chưa phân loại** cho team quản lý

**Kết quả?** Tốn **10-15 giờ công** mỗi tháng, dễ mắc sai sót, và không thể hoạt động 24/7.

---
### **🎯 Giải Pháp Của Chúng Ta: Workflow Tự Động Hóa 100% Không Code**
Dùng **n8n + easybits AI + Google Drive + Slack**, workflow này sẽ:
✔ **Phân loại tự động** hóa đơn thành **6 loại chính** (Y tế, Khách sạn, Nhà hàng, Thương mại, Di động, và "Yêu cầu kiểm tra")
✔ **Lưu tự động** vào **Google Drive** theo folder tương ứng
✔ **Báo cáo qua Slack** khi hóa đơn không rõ ràng (confidence ≤ 50%)
✔ **Hoạt động liên tục 24/7** (không cần can thiệp thủ công)
✔ **Tiết kiệm 80% thời gian** so với cách làm thủ công

---
### **🎯 Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10-15 giờ công/tháng** cho bộ phận tài chính.
- **Giảm sai sót** do phân loại thủ công (AI có độ chính xác >90% với confidence >0.7).
- **Hoạt động tự động 24/7** (không cần can thiệp vào cuối tuần hoặc đêm).
- **Báo cáo tự động** qua Slack khi cần review, giúp team quản lý theo dõi kịp thời.
- **Cá nhân hóa lưu trữ** (mỗi loại hóa đơn vào folder riêng trong Google Drive).
- **Dễ dàng mở rộng** (thêm loại hóa đơn mới chỉ cần cập nhật easybits pipeline).
:::

---

## **🔧 Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
### **1. Tài Khoản & API Keys**
| **Dịch Vụ**               | **Thông Tin Cần Thiết**                                                                 | **Liên Kết Cài Đặt**                          |
|---------------------------|-----------------------------------------------------------------------------------------|-----------------------------------------------|
| **easybits Extractor**    | - Pipeline ID <br> - API Key <br> - Cấu hình 2 field: `document_class` & `confidence_score` | [extractor.easybits.tech](https://extractor.easybits.tech) |
| **Google Drive**          | - Client ID & Client Secret (OAuth 2.0) <br> - Google Drive API được kích hoạt          | [Google Cloud Console](https://console.cloud.google.com/) |
| **Slack**                 | - Slack Bot Token <br> - Channel `#n8n-invoice-review` (đã tạo)                          | [api.slack.com/apps](https://api.slack.com/apps) |

### **2. Folder Google Drive**
Tạo **6 folder** trong Google Drive:
- **Medical** (Hóa đơn y tế)
- **Restaurant** (Hóa đơn nhà hàng)
- **Hotel** (Hóa đơn khách sạn)
- **Trades** (Hóa đơn thương mại)
- **Telecom** (Hóa đơn di động)
- **Needs Review** (Hóa đơn cần kiểm tra)

### **3. Web Form (Để Người Dùng Upload File)**
- Workflow hỗ trợ **PDF, PNG, JPEG**.
- Các sếp có thể sử dụng **n8n Form Trigger** hoặc **Google Form** kết nối với workflow.

---
## **🚀 Cách Import & Cấu Hình Workflow**

### **1. Import Workflow từ File JSON**
:::info[BƯỚC 1: Tải Workflow]
1. Tải file JSON từ [n8n.io/workflows/14960](https://n8n.io/workflows/14960) (chọn **Export as JSON**).
2. Đăng nhập vào **n8n Self-hosted** (cài trên VPS).
3. Vào **Workflow** → **Import** → Dán JSON và nhấn **Import**.
:::

### **2. Cấu Hình Cần Thiết (BẮT BUỘC)**
#### **🔹 Node 1: On Form Submission (formTrigger)**
- **Không cần cấu hình** (sẵn sàng nhận file từ form).

#### **🔹 Node 2: easybits Extractor for Classification**
1. Vào **Settings → Credentials** → Tạo **easybits Extractor** credential:
   - **Pipeline ID**: Copy từ easybits dashboard.
   - **API Key**: Copy từ easybits dashboard.
2. Mở node **easybits Extractor** → Chọn credential vừa tạo.

#### **🔹 Node 3: Parse Result (set)**
- **Không cần cấu hình** (n8n tự động phân tách `document_type` và `confidence_score`).

#### **🔹 Node 4: Confidence Check (if)**
- **Điều kiện**: `confidence_score > 0.5` → Chuyển sang **Category Router**.
- Nếu `confidence_score ≤ 0.5` → Chuyển sang **Upload to Review Folder** + **Slack Notification**.

#### **🔹 Node 5-10: Upload to [Folder] (googleDrive)**
1. Mở mỗi node (Upload to Medical, Restaurant, Hotel, Trades, Telecom):
   - Chọn **Google Drive OAuth2 credential** (đã tạo trước).
   - Chọn **folder tương ứng** trong Google Drive.
   - **Lưu ý**: Node này chỉ hoạt động nếu `document_type` khớp (ví dụ: `medical_invoice` → Upload to Medical).

#### **🔹 Node 11: Upload to Review Folder (googleDrive)**
- Chọn **Google Drive OAuth2 credential**.
- Chọn **folder "Needs Review"**.
- **Hoạt động khi**:
  - `confidence_score ≤ 0.5` **hoặc**
  - `document_type = null` (không phân loại được).

#### **🔹 Node 12: Review Message (slack)**
1. Vào **Settings → Credentials** → Tạo **Slack API credential**:
   - Dán **Slack Bot Token** (từ Slack App).
2. Mở node **Review Message**:
   - Chọn **Slack API credential**.
   - Chọn **channel `#n8n-invoice-review`**.
   - **Thông báo mẫu**:
     ```
     🚨 **Invoice Needs Review**
     - **Type**: {{$node["easybits Extractor for Classification"].json()["document_type"]}}
     - **Confidence**: {{$node["easybits Extractor for Classification"].json()["confidence_score"]}}
     - **File**: {{$node["On form submission"].fileName}}
     - **Link**: [Google Drive Link]({{$node["Upload to Review Folder"].googleDriveFileUrl}})
     ```

#### **🔹 Node 13: Attach Original File (merge)**
- **Không cần cấu hình** (n8n tự động gộp file binary với kết quả phân loại).

---
### **3. Kích Hoạt Workflow**
1. Nhấn **Active** ở góc trên phải.
2. **Test Run**:
   - Upload một file mẫu (PDF/PNG/JPEG) qua form.
   - Kiểm tra **Execution Log** để xác nhận:
     - Hóa đơn được phân loại đúng loại.
     - File được lưu vào folder tương ứng.
     - Nếu confidence thấp, Slack báo cáo đúng.

---
## **✍️ Mẹo & Gợi Ý Nâng Cao**
### **1. Tối Ưu Hóa easybits Pipeline**
- **Cập nhật prompt** để tăng độ chính xác:
  - Ví dụ: `"Phân loại hóa đơn này là loại nào? Trả về: medical_invoice, restaurant_invoice, hotel_invoice, trades_invoice, telecom_invoice, hoặc null nếu không chắc chắn."`
- **Thêm field `source_document_name`** để lưu tên file gốc.

### **2. Lưu Log Lịch Sử Phân Loại**
- Thêm node **Google Sheets** sau **Category Router** để ghi lại:
  - Tên file, loại hóa đơn, confidence score, ngày upload.

### **3. Gửi Báo Cáo Định Kỳ**
- Sử dụng **n8n Schedule Node** để gửi báo cáo hàng tuần qua Slack/Email:
  - Tổng số hóa đơn được phân loại.
  - Số hóa đơn cần review.
  - Top 3 loại hóa đơn phổ biến.

### **4. Kết Nối Với CRM (CRM Integration)**
- Thêm node **Zapier/HubSpot** sau **Category Router** để tự động tạo record trong CRM khi hóa đơn được phân loại.

### **5. Xử Lý File Lớn (PDF >10MB)**
- Nếu hóa đơn quá lớn, sử dụng **AWS S3** hoặc **Google Cloud Storage** thay vì Google Drive.

---
## **📌 Kết Luận: Áp Dụng Ngay Hôm Nay!**
Workflow này **giải phóng bộ phận tài chính** khỏi công việc phân loại hóa đơn mòn mỏi, **tăng độ chính xác**, và **tự động hóa toàn bộ quy trình** chỉ với **một lần cài đặt**.

### **🔥 Bước Tiến Sau**
1. **Cài n8n Self-hosted** trên VPS (để workflow hoạt động 24/7).
   👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
   👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)

2. **Tạo easybits Pipeline** và cấu hình Google Drive/Slack.

3. **Import workflow** và **test run** với file mẫu.

4. **Bật Active** và **quên đi công việc phân loại hóa đơn thủ công!**

---
**🚀 Hãy tự động hóa ngay hôm nay và tiết kiệm thời gian cho team của bạn!** 🚀