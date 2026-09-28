---
title: "🚀 Tự Động Hoàn Chỉnh & Lưu Lịch Sử Workflow n8n Với Versioning + Theo Dõi Notion (Backup 24/7)"
description: "Workflow này tự động sao lưu tất cả workflow n8n từ instance nguồn sang instance đích, thêm prefix ngày tháng để quản lý versioning, đồng thời ghi chép lịch sử vào Notion. Giúp các sếp bảo mật dữ liệu, theo dõi lịch sử thay đổi và quản lý backup hiệu quả mà không cần code."
slug: "tieu-dong-hoan-chinh-luu-lich-su-workflow-n8n"
tags: [n8n, automation, devops, backup, notion, versioning]
keywords: [tự động hóa n8n, backup workflow n8n, versioning workflow, theo dõi lịch sử n8n, lưu trữ workflow định kỳ, notion integration n8n]
---

# 🚀 **Tự Động Hoàn Chỉnh & Lưu Lịch Sử Workflow n8n Với Versioning + Theo Dõi Notion**

## **🔥 Nỗi Đau Của Các Sếp Khi Quản Lý Workflow n8n**
Các sếp thường gặp phải những vấn đề sau khi làm việc với n8n:
- **Mất dữ liệu khi instance n8n bị lỗi hoặc xóa nhầm**: Một lần xóa workflow không cẩn thận có thể khiến toàn bộ quy trình tự động hóa bị mất.
- **Không theo dõi được lịch sử thay đổi**: Không biết workflow đã được cập nhật bao nhiêu lần và khi nào.
- **Quản lý versioning thủ công**: Phải tự đặt tên phiên bản (v1, v2,...) và lưu trữ riêng biệt, tốn thời gian và dễ nhầm lẫn.
- **Không có báo cáo tự động**: Muốn biết bao nhiêu workflow đã được sao lưu mỗi ngày, phải kiểm tra thủ công.

**Workflow này giải quyết tất cả những vấn đề trên bằng cách:**
✅ **Sao lưu tự động** tất cả workflow từ instance nguồn sang instance đích.
✅ **Thêm prefix ngày tháng** (vd: `2025_08_03_PDF_Summarizer`) để quản lý versioning một cách logic.
✅ **Ghi chép vào Notion** bao gồm ngày thực hiện, số lượng workflow được sao lưu.
✅ **Xóa phiên bản cũ tự động** (ví dụ: giữ lại 2 phiên bản gần nhất).
✅ **Hoạt động 24/7** mà không cần can thiệp của con người.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo tính ổn định và bảo mật.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Bảo mật dữ liệu**: Sao lưu tự động hàng ngày, giảm thiểu rủi ro mất dữ liệu.
- **Quản lý versioning dễ dàng**: Mỗi phiên bản workflow được đặt tên theo ngày (vd: `2025_08_03_WorkflowName`), giúp theo dõi lịch sử thay đổi một cách rõ ràng.
- **Báo cáo tự động**: Số lượng workflow được sao lưu mỗi ngày được ghi vào Notion, giúp theo dõi hiệu suất.
- **Tiết kiệm thời gian**: Không cần làm thủ công, workflow chạy tự động mỗi khi kích hoạt.
- **Hoạt động liên tục**: Dù server ngủ, workflow vẫn hoạt động nhờ VPS.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
1. **Hai instance n8n**:
   - **Instance nguồn (Source)**: Instance chứa workflow cần sao lưu.
   - **Instance đích (Destination)**: Instance lưu trữ phiên bản sao lưu.
2. **API Keys cho cả hai instance**:
   - Tạo **credentials** trong n8n với quyền:
     - `read:workflows` (đọc workflow)
     - `create:workflows` (tạo workflow mới)
     - `delete:workflows` (xóa workflow cũ).
3. **Notion Database**:
   - Tạo một **database Notion** với 3 trường:
     - `sequence` (giá trị cố định: `"prefix"`).
     - `Value` (định dạng: `YYYY-MM-DD_`).
     - `Comment` (số lượng workflow được sao lưu).
4. **Thiết lập quyền API**:
   - Đảm bảo instance nguồn và đích có quyền truy cập API đầy đủ.
5. **n8n Version**: Workflow được test trên **n8n 1.103.2 (Ubuntu)**. Nếu dùng phiên bản khác, có thể cần điều chỉnh.
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/6947) hoặc copy toàn bộ JSON từ canvas.
- Mở **n8n Editor** → Nhấn **Import Workflow** → Dán JSON và nhấn **Import**.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Sau khi import, các sếp cần cấu hình các node quan trọng sau:

##### **A. Cấu Hình Credentials cho n8n API**
- **Node "GET - Workflows"**, **"CREATE - Workflow"**, **"n8n_destination"**:
  - Chọn **credentials** tương ứng với **instance nguồn** và **instance đích**.
  - Đảm bảo API Key đã được thêm vào trong **Credentials** của n8n.

##### **B. Cấu Hình Notion Database**
- **Node "Notion" (update)** và **"Notion1" (get)**:
  - Thêm **credentials Notion API** (tạo từ Notion Developer Console).
  - Chọn **database Notion** đã tạo trước đó.
  - Đảm bảo trường `sequence` có giá trị `"prefix"`.

##### **C. Cấu Hình Ngày Thực Hiện**
- **Node "today"**, **"yesterday"**, **"today_prefix"**, **"yesterday_prefix"**:
  - Các node này tự động tính toán ngày tháng, **không cần chỉnh sửa** trừ khi muốn thay đổi định dạng.
  - Ví dụ: `today_prefix` sẽ tự động tạo ra `2025_08_03_`.

##### **D. Cấu Hình Xóa Phiên Bản Cũ**
- **Node "Subtract From Date"**:
  - Thiết lập **số ngày muốn giữ lại** (ví dụ: `2` để giữ 2 phiên bản gần nhất).
  - Node này sẽ tính toán ngày **trước đó 2 ngày** để xóa phiên bản cũ.
- **Node "Limit"**:
  - Đặt **limit = 1** để test, sau đó tăng lên số lượng workflow muốn xử lý.

##### **E. Cấu Hình Tên Workflow**
- **Node "Split Out Workflows"**:
  - Workflow sẽ được đặt tên theo định dạng: `YYYY-MM-DD_workflowname`.
  - Ví dụ: `2025_08_03_PDF_Summarizer`.

##### **F. Kích Hoạt Workflow**
- Nhấn **Test Workflow** để chạy thử với dữ liệu mẫu.
- Sau khi kiểm tra thành công, bật **Active** để workflow hoạt động tự động.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết Nối Slack/Telegram để báo cáo**:
   - Thêm node **Slack** hoặc **Telegram** sau node **Notion** để thông báo khi sao lưu thành công.
   - Ví dụ: `"Sao lưu workflow thành công! Số lượng: [{{ $json["$.length"] }}]"`.
2. **Lưu Log vào File**:
   - Sử dụng node **File System** để ghi log vào file CSV/JSON, giúp theo dõi lịch sử dài hạn.
3. **Báo Cáo Định Kỳ**:
   - Tạo một workflow khác sử dụng **n8n Schedule Node** để gửi báo cáo hàng tuần/month đến email.
4. **Quản Lý Nhiều Instance**:
   - Nếu có nhiều instance đích, có thể thêm **node "If"** để chọn instance sao lưu dựa trên điều kiện.
5. **Tự Động Cập Nhật Notion**:
   - Nếu muốn cập nhật Notion mỗi khi có thay đổi, thêm node **Webhook** để kích hoạt workflow khi có sự kiện mới.

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn:
✔ **Bảo mật dữ liệu** với sao lưu tự động hàng ngày.
✔ **Quản lý versioning** một cách logic và tự động.
✔ **Theo dõi lịch sử thay đổi** thông qua Notion.
✔ **Tiết kiệm thời gian** bằng tự động hóa hoàn toàn.

**Hãy áp dụng ngay để tránh mất dữ liệu và quản lý workflow hiệu quả hơn!**
👉 **Bắt đầu import workflow và cấu hình ngay bây giờ!**

---
**Có vấn đề?** Liên hệ tác giả trên [LinkedIn](https://www.linkedin.com/in/stheheckel/) hoặc [Forum n8n](https://community.n8n.io/).