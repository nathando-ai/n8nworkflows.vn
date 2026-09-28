---
title: "📄 **Tự Động Hóa Phân Loại & Theo Dõi Hạn Hết Hợp Đồng với Easybits, Google Drive & Sheets (Không Cần Code!)**"
description: "Workflow tự động phân loại hợp đồng (SaaS, Lease, Service, Insurance, Other) và theo dõi hạn hết bằng AI + Google Drive, giúp các sếp tiết kiệm 10+ giờ/tháng kiểm tra thủ công. Kết quả: Dữ liệu hợp đồng được tự động phân loại, tính toán ngày hết hạn và cảnh báo kịp thời."
slug: "tieu-dong-hoa-phan-loai-va-theo-doi-han-het-hop-dong"
tags: [n8n, automation, no-code, google-drive, google-sheets, easybits, ai, contract-management]
keywords: [n8n workflow hợp đồng, tự động hóa hợp đồng, phân loại hợp đồng AI, theo dõi hạn hết hợp đồng, easybits n8n, google drive tự động hóa]
---

# 🚀 **Tự Động Hóa Phân Loại & Theo Dõi Hạn Hết Hợp Đồng với Easybits, Google Drive & Sheets**

### **Giải pháp cho nỗi đau "Hợp đồng rơi vào quên lãng" của các sếp**
Hàng ngày, các sếp phải:
- **Tìm kiếm thủ công** hợp đồng trong Google Drive, Excel hay email để kiểm tra hạn hết.
- **Phân loại sai loại** hợp đồng (SaaS, Lease, Insurance...) dẫn đến mất thời gian và rủi ro.
- **Quên cảnh báo** trước khi hợp đồng hết hạn, gây mất tiền hoặc vi phạm pháp luật.
- **Cập nhật dữ liệu thủ công** vào Google Sheets, dễ bị lỗi và không đồng bộ.

**Workflow này tự động hóa toàn bộ quá trình:**
✅ **Phân loại hợp đồng** bằng AI (Easybits) chỉ trong vài giây.
✅ **Tính toán tự động** ngày hết hạn và ngày cảnh báo.
✅ **Lưu trữ dữ liệu** vào Google Sheets theo loại hợp đồng (SaaS, Lease, Service...).
✅ **Hoạt động 24/7** mà không cần can thiệp của con người.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo tính riêng tư và không bị giới hạn tài nguyên.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ/tháng** kiểm tra hợp đồng thủ công.
- **Phân loại chính xác** hợp đồng (SaaS, Lease, Service, Insurance, Other) bằng AI.
- **Tính toán tự động** ngày hết hạn và ngày cảnh báo (cảnh báo 60-90 ngày trước).
- **Dữ liệu đồng bộ** vào Google Sheets, dễ theo dõi và báo cáo.
- **Không lo quên hạn** nhờ hệ thống cảnh báo tự động.
- **Giảm rủi ro pháp lý** do không bỏ qua hợp đồng nào.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Easybits**:
   - [Đăng ký miễn phí tại Easybits](https://extractor.easybits.tech/) và tạo **Pipeline ID**.
   - API Key từ Easybits (cần để kết nối với n8n).
2. **Google Drive**:
   - **Folder theo dõi hợp đồng** (ví dụ: "Incoming Contracts") để workflow tự động lấy file mới.
   - **Quản lý quyền** cho folder này (n8n cần quyền đọc/thêm file).
3. **Google Sheets**:
   - **1 bảng Google Sheets** với **5 tab** (SaaS, Lease, Service, Insurance, Other).
   - **Cột tiêu đề** bắt buộc (xem mẫu dưới đây).
4. **Credentials cho n8n**:
   - **Google Drive OAuth** (để trigger và tải file).
   - **Google Sheets OAuth** (để ghi dữ liệu).
   - **Easybits API Key** (để phân loại hợp đồng).

---
---
### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/15230) hoặc copy toàn bộ JSON từ canvas.
- **Mở n8n Editor** → Nhấn **"Import"** → Dán JSON hoặc tải file JSON.
- **Kích hoạt workflow** sau khi import xong.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow gồm **12 node**, các sếp cần chú ý cấu hình **các node sau**:

##### **📁 Node 1: Watch Contract Folder (Google Drive Trigger)**
- **Chọn folder** theo dõi hợp đồng (ví dụ: "Incoming Contracts").
- **Cài đặt Polling Interval**: 1 phút (default) để nhanh chóng phát hiện file mới.
- **Lưu ý**: File mới sẽ được tải xuống và xử lý trong vòng **1 phút** sau khi upload.

##### **🤖 Node 2: easybits: Classify & Extract Contract**
- **Paste Pipeline ID** từ Easybits vào trường `Pipeline ID`.
- **Điền Easybits API Key** vào `Credentials`.
- **Lưu ý**:
  - Easybits sẽ trả về `contract_class` là `null` nếu file **không phải hợp đồng**.
  - Nếu muốn **cảnh báo hợp đồng không hợp lệ**, các sếp có thể thêm **Slack/Email Alert** vào node `Skip: Not a Contract`.

##### **📊 Node 3-7: Log SaaS/Lease/Service/Insurance/Other (Google Sheets)**
- **Chọn Sheet ID** của Google Sheets (cùng một Sheet với 5 tab).
- **Chọn tab tương ứng** (SaaS, Lease, Service, Insurance, Other).
- **Lưu ý**:
  - **Cột tiêu đề bắt buộc** (xem mẫu dưới đây).
  - **Chế độ ghi**: `Append` (không ghi đè dữ liệu cũ).

##### **📅 Node 8: Calculate End Date & Deadline (Set)**
- **Công thức tính toán**:
  - `end_date` = `start_date` + `initial_term_months`.
  - `cancellation_deadline` = `end_date` - `notice_period_days`.
- **Lưu ý**:
  - Nếu `notice_period_days` không được điền, `cancellation_deadline` sẽ bằng `end_date` (không cảnh báo kịp thời).

##### **⚡ Node 9: Skip: Not a Contract (noOp)**
- **Lưu ý**: Nếu hợp đồng **không được phân loại**, workflow sẽ **bỏ qua** (không cảnh báo).
- **Mở rộng**: Các sếp có thể thêm **Slack/Email Alert** để báo lỗi nếu muốn.

##### **🔄 Node 10: Route by Contract Class (Switch)**
- **Chọn `contract_class`** từ Easybits để định tuyến đến tab đúng trong Google Sheets.
- **Lưu ý**: Cấu hình này **bắt buộc** để dữ liệu được ghi vào tab chính xác.

---
#### **3. Kích hoạt ⚡️**
- **Test Run**:
  - Upload một file hợp đồng (PDF/JPG/PNG) vào folder theo dõi.
  - Kiểm tra **Google Sheets** để xem dữ liệu có được ghi vào tab đúng không.
- **Bật Active**:
  - Sau khi test thành công, **bật workflow** để hoạt động liên tục.

---
---
### ✍️ **Mẹo & gợi ý nâng cao**
1. **Cảnh báo Slack/Email khi hợp đồng sắp hết hạn**:
   - Thêm **node Slack/Email** sau `Calculate End Date & Deadline` để gửi thông báo khi `cancellation_deadline` sắp đến.
   - Ví dụ: Nếu `cancellation_deadline` < 30 ngày, gửi cảnh báo.

2. **Lưu log hoạt động**:
   - Thêm **node Google Sheets** để ghi log tất cả hoạt động (thành công/thất bại) vào một tab riêng.

3. **Tích hợp với CRM (Salesforce/Zoho)**:
   - Sau khi hợp đồng được phân loại, có thể **tích hợp với CRM** để cập nhật thông tin khách hàng.

4. **Phân loại file theo định dạng**:
   - Nếu muốn **chỉ xử lý PDF/JPG/PNG**, thêm **node Filter** trước `easybits: Classify & Extract Contract` để loại bỏ file khác.

5. **Tự động gửi báo cáo hàng tháng**:
   - Sử dụng **node Google Sheets** để tạo **báo cáo tổng hợp** tất cả hợp đồng sắp hết hạn.

---
---
### 📌 **Kết luận**
Workflow này **giải phóng các sếp khỏi công việc thủ công mệt mỏi** khi theo dõi hợp đồng. Với **AI phân loại + Google Drive + Sheets**, dữ liệu hợp đồng được **tự động phân loại, tính toán và cảnh báo kịp thời**, giúp các sếp:
✔ **Tiết kiệm thời gian** (không phải kiểm tra thủ công).
✔ **Tránh rủi ro pháp lý** (không bỏ qua hợp đồng nào).
✔ **Quản lý hiệu quả** (dữ liệu đồng bộ, dễ theo dõi).

**🚀 Hãy áp dụng ngay workflow này và tự động hóa quản lý hợp đồng của mình!**
Nếu có vấn đề, các sếp có thể **comment dưới bài** hoặc liên hệ với Easybits/n8n để hỗ trợ.

---
**🔗 [Tải workflow nguyên bản tại đây](https://n8n.io/workflows/15230)**