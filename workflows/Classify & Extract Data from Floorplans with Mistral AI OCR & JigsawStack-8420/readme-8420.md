---
title: "🏠 Tự Động Hóa Xác Minh & Trích Xuất Dữ Liệu Từ Bản Vẽ Nhà (Floorplans) Với AI OCR & JigsawStack – N8N"
description: "Workflow tự động hóa 100% không code để phân loại và trích xuất thông tin từ file PDF/ảnh bản vẽ nhà, loại bỏ những file không phù hợp sớm, tiết kiệm chi phí API và thời gian xử lý. Giúp các sếp xây dựng hệ thống đo lường và phân tích không gian sống thông minh."
slug: "tieu-dong-hoa-xac-minh-trich-xuat-du-lieu-tu-ban-vay-nha"
tags: [n8n, automation, ai-ocr, jigsawstack, multimodal-ai, no-code]
keywords: [n8n workflow floorplan, tự động hóa bản vẽ nhà, phân loại file pdf ảnh, ai ocr trích xuất dữ liệu, jigsawstack api, tự động hóa đo lường không gian]
---

# 🚀 **Tự Động Hóa Xác Minh & Trích Xuất Dữ Liệu Từ Bản Vẽ Nhà (Floorplans) Với AI OCR & JigsawStack**

## **🔍 Nỗi Đau Của Các Sếp Khi Làm Thủ Công**
Hiện nay, khi nhận được hàng trăm file bản vẽ nhà (PDF/ảnh) từ khách hàng, các sếp phải:
- **Làm thủ công** phân loại file: Loại bỏ những file không phải bản vẽ nhà (ảnh cảnh quan, bản vẽ kỹ thuật khác).
- **Tốn thời gian** để kiểm tra từng file, dẫn đến hiệu suất thấp và chi phí nhân lực cao.
- **Rủi ro sai sót** khi phân loại không chính xác, gây mất niềm tin với khách hàng.
- **Tốn kém API** vì phải xử lý file không phù hợp, ảnh hưởng đến ngân sách dự án.

**Workflow này giải quyết tất cả những vấn đề trên bằng cách:**
✅ **Phân loại tự động** file PDF/ảnh thành 3 loại: **Không phù hợp**, **Cần kiểm tra thủ công**, hoặc **Đủ chất lượng để xử lý**.
✅ **Trích xuất dữ liệu** (diện tích phòng, chiều dài tường) bằng AI OCR, tiết kiệm thời gian so với cách làm thủ công.
✅ **Lọc sớm file không phù hợp**, giảm chi phí API và tối ưu hóa quy trình.
✅ **Cung cấp phản hồi tự động** cho khách hàng, cải thiện trải nghiệm dịch vụ.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Loại bỏ việc kiểm tra thủ công hàng trăm file mỗi ngày.
- **Tăng chính xác**: AI phân loại với độ chính xác cao (thRESHOLD 85%).
- **Giảm chi phí API**: Không phải xử lý file không phù hợp, tiết kiệm ngân sách.
- **Cải thiện trải nghiệm khách hàng**: Phản hồi tức thời và rõ ràng.
- **Dữ liệu sạch**: Chỉ giữ lại file bản vẽ nhà chất lượng cao cho bước xử lý tiếp theo.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
- **API Key JigsawStack** (để lưu trữ và phân loại file).
- **API Key Mistral Cloud** (để trích xuất dữ liệu bằng OCR).
- **n8n Instance** (self-hosted hoặc n8n Cloud).
- **Endpoint Webhook** (để nhận file upload từ khách hàng).
- **Tài khoản n8n** (để cấu hình credential và import workflow).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/8420](https://n8n.io/workflows/8420) hoặc copy/paste JSON vào **n8n Editor**.
- **Cách import**:
  1. Mở **n8n Editor** trên trang web hoặc self-hosted.
  2. Nhấn **"Import"** và chọn file JSON.
  3. Chọn **"Import"** để hoàn tất.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflows này có **17 node** với logic phân loại phức tạp. Các bước quan trọng cần chú ý:

##### **🔹 Node "Webhook – Receive Upload"**
- **Cấu hình**:
  - **Path**: `fp-mvp` (không đổi).
  - **HTTP Method**: `POST`.
  - **Credentials**: Sử dụng `httpBasicAuth` (cấu hình trong **Credentials Manager** của n8n).
- **Lưu ý**:
  - Đảm bảo **endpoint webhook** được mở và có thể tiếp nhận file từ bên ngoài.

##### **🔹 Node "Check – GDPR Consent"**
- **Cấu hình**:
  - Nếu khách hàng upload file mà chưa đồng ý GDPR, workflow sẽ **từ chối tự động**.
  - **Lưu ý**: Nếu không cần GDPR, có thể bỏ qua node này hoặc cấu hình lại logic.

##### **🔹 Node "Process – Multiple File Uploads" (Code Node)**
- **Lưu ý**:
  - Node này xử lý trường hợp khách hàng upload **nhiều file cùng lúc**.
  - **Không cần chỉnh sửa** nếu không hiểu code, nhưng đảm bảo **credentials API** đã được cài đặt đúng.

##### **🔹 Node "Check – File Type (PDF/Image)"**
- **Cấu hình**:
  - Node này phân loại file thành **PDF** hoặc **Ảnh (JPG/PNG)**.
  - **Không cần chỉnh sửa**, nhưng nếu muốn hỗ trợ file khác, cần cập nhật logic trong **Code Node**.

##### **🔹 Node "Extract – PDF Metadata/Text"**
- **Cấu hình**:
  - **Operation**: `pdf` (không đổi).
  - **Lưu ý**: Nếu file PDF không có metadata, node này sẽ trích xuất **nội dung văn bản** để phân tích.

##### **🔹 Node "Analyze – Confidence Score (Heuristics)" (Code Node)**
- **Lưu ý**:
  - Node này sử dụng **heuristic rules** (các từ khóa như "living room", "m²", "WCD") để đánh giá độ tin cậy của file.
  - **Không cần chỉnh sửa** nếu muốn sử dụng mặc định, nhưng có thể **cập nhật từ khóa** phù hợp với thị trường của bạn.

##### **🔹 Node "Route – Confidence Levels" (Switch Node)**
- **Cấu hình**:
  - **Thresholds**:
    - **< 40%**: File **không phải bản vẽ nhà** → Trả lời "Unable to Process Your Floorplan".
    - **40-85%**: File **có thể không rõ ràng** → Trả lời "Manual Review Required".
    - **≥ 85%**: File **đủ chất lượng** → Tiếp tục xử lý bằng AI OCR.
  - **Lưu ý**: Có thể **cập nhật ngưỡng** (ví dụ: từ 85% sang 90%) nếu muốn **chặt chẽ hơn**.

##### **🔹 Node "Classify – Image Files" & "Classify – PDF Text" (HTTP Request)**
- **Cấu hình**:
  - **Credentials**: Sử dụng `httpHeaderAuth` (đăng ký API key JigsawStack).
  - **Lưu ý**:
    - Đảm bảo **API key JigsawStack** đã được cài đặt trong **Credentials Manager**.
    - Nếu muốn thay đổi provider AI (ví dụ: AWS Textract), cần **cập nhật URL API** trong node này.

##### **🔹 Node "Upload – JigsawStack (Storage)"**
- **Cấu hình**:
  - **Credentials**: `httpHeaderAuth` (API key JigsawStack).
  - **Lưu ý**:
    - Node này **lưu file** vào JigsawStack để xử lý tiếp theo.
    - Nếu muốn lưu vào **Google Drive/Notion**, cần thay đổi node này thành **HTTP Request** mới.

##### **🔹 Node "Respond – [Tên Trả Lời]" (RespondToWebhook)**
- **Cấu hình**:
  - **Lưu ý**: Các node này **trả lời tự động** cho khách hàng khi upload file.
  - **Cập nhật nội dung phản hồi** nếu muốn thay đổi thông điệp (ví dụ: thêm link hỗ trợ).

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run** với file mẫu:
   - Upload một file **PDF bản vẽ nhà** và một file **ảnh không phải bản vẽ** để kiểm tra logic.
   - Kiểm tra **trả lời tự động** của workflow.
2. **Bật Active**:
   - Chuyển trạng thái workflow từ **"Inactive"** sang **"Active"**.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[CÁCH LÀM TIẾP THEO]
- **Gửi kết quả lên Slack/Email**:
  - Thêm node **Slack Webhook** hoặc **Email Node** sau node **"Upload – JigsawStack"** để thông báo kết quả cho team.
- **Lưu log vào Database**:
  - Sử dụng node **Database (PostgreSQL/MySQL)** để lưu lịch sử xử lý file.
- **Tích hợp với CRM (HubSpot/Salesforce)**:
  - Sau khi trích xuất dữ liệu, có thể **cập nhật thông tin khách hàng** trong CRM.
- **Tự động tạo báo cáo**:
  - Sử dụng node **Google Sheets** hoặc **Notion** để tổng hợp dữ liệu từ nhiều file.
- **Cập nhật từ khóa phân loại**:
  - Nếu làm việc với **ngành khác** (nhà hàng, văn phòng), cập nhật **heuristic rules** trong **Code Node** để phù hợp.
:::

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn **tự động hóa quy trình phân loại và trích xuất dữ liệu từ bản vẽ nhà**, tiết kiệm thời gian và chi phí. Bằng cách **lọc sớm file không phù hợp**, bạn không chỉ **tăng hiệu suất** mà còn **cải thiện trải nghiệm khách hàng** với phản hồi tức thời.

**👉 Bắt đầu ngay!**
1. **Import workflow** vào n8n của bạn.
2. **Cấu hình API key** và **credentials**.
3. **Test với file mẫu** và **bật Active**.
4. **Tích hợp thêm** các node như Slack, Email, hoặc Database để tối ưu hóa hơn.

**💡 Lưu ý cuối cùng**:
- **Không hardcode API key** → luôn sử dụng **Credentials Manager** của n8n.
- **Cập nhật logic** theo nhu cầu thực tế của doanh nghiệp.
- **Monitor workflow** để đảm bảo hoạt động ổn định 24/7.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**🚀 Hãy tự động hóa ngay hôm nay và làm việc thông minh hơn!** 🚀