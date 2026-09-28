---
title: "🔄 **Chuyển Nhập Tự Động Workflow n8n Giúp Các Sếp Quản Lý Nhiều Instance Như Chơi Game**"
description: "Workflow này giúp các sếp tự động chọn lọc và chuyển nhật workflow giữa các instance n8n khác nhau **không cần export/import thủ công**, tránh lỗi bulk import và đảm bảo an toàn 100%. Hỗ trợ cả **chế độ đơn giản** (fixed credentials) và **chế độ động** (lấy từ Notion/DB)."
slug: "chuyen-nhap-workflow-n8n-giua-instance"
tags: [n8n, automation, file-management, api-integration, notion, self-hosted]
keywords: [n8n tự động hóa, chuyển nhật workflow n8n, import/export workflow, quản lý instance n8n, API n8n, Notion + n8n]
---

# 🚀 **Chuyển Nhập Workflow n8n Giúp Các Sếp Quản Lý Nhiều Instance Như Chơi Game**

Hãy tưởng tượng một tình huống: Các sếp đang quản lý **nhiều instance n8n** (ví dụ: dev, staging, production) và muốn **chuyển một số workflow cụ thể** từ instance này sang instance khác mà **không cần export/import thủ công**. Hoặc thậm chí, các sếp muốn **lấy danh sách workflow từ một database (Notion/Supabase) và chuyển nhật tự động** mà không cần nhớ API key nào là của instance nào.

**Workflow này giải quyết tất cả!** Nó cho phép các sếp:
✅ **Chọn lọc workflow** muốn chuyển (không bulk import gây lỗi).
✅ **Tự động loại bỏ trường dữ liệu không tương thích** với API.
✅ **Chuyển nhật an toàn** vào instance mục tiêu.
✅ **Hỗ trợ cả chế độ đơn giản (fixed credentials) và động (từ Notion/DB)**.

---
## 🎯 **Kết Quả Các Sếp Nhận Được**

:::tip[**LỢI ÍCH CỐT LÕI**]
- **Tiết kiệm thời gian**: Không cần export/import thủ công, tránh lỗi nhân sự.
- **An toàn tuyệt đối**: Không bulk import gây lỗi, chỉ chuyển workflow đã chọn.
- **Quản lý linh hoạt**: Hỗ trợ **chế độ động** lấy instance từ Notion/Supabase (không cần hardcode API key).
- **Hiển thị kết quả rõ ràng**: Báo cáo thành công/thất bại cho từng workflow.
- **Tích hợp Notion**: Lấy danh sách instance từ database (phù hợp cho các sếp quản lý nhiều instance).
:::

---
## 🔧 **Yêu Cầu Cần Thiết**

:::info[**CHUẨN BỊ**]
Các sếp cần chuẩn bị:
1. **Hai instance n8n** (source và target) với:
   - **API Key** của cả hai instance (để workflow có thể gọi API).
   - **URL base** của instance (ví dụ: `https://your-instance.n8n.io`).
2. **(Nếu dùng chế độ động)**:
   - **Notion/Supabase** chứa danh sách instance với các trường:
     - `instanceUrl` (URL của instance).
     - `apiKey` (API key của instance).
     - `displayName` (tên hiển thị, ví dụ: "Dev Instance").
   - **Credentials Notion** (để workflow có thể gọi API Notion).
3. **N8n API Key** (để workflow có thể gọi API của n8n).

---
## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
Các sếp có thể:
- **Tải file JSON** từ [n8n.io/workflows/13425](https://n8n.io/workflows/13425) và import vào **n8n Editor**.
- **Copy/paste JSON** từ file vào **Import Workflow** trong n8n.

:::note[**Lưu ý**]
- Workflow này **không tự động chạy** khi import. Các sếp cần **cấu hình credentials** và **bật chế độ hoạt động**.
- **Không xóa node nào** trong workflow, chỉ chỉnh sửa các phần cần thiết.
:::

---

### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**

#### **A. Cấu Hình Credentials**
Workflow hỗ trợ **hai chế độ**:
1. **Chế độ đơn giản (Simple Mode)**:
   - **Source Instance**: Điền `n8nApi` (credentials của instance nguồn).
   - **Target Instance**: Điền `n8nApi` (credentials của instance đích).
   - **Notion (nếu dùng chế độ động)**: Điền `notionApi`.

2. **Chế độ động (Dynamic Mode)**:
   - **Notion**: Điền `notionApi` để lấy danh sách instance từ database.
   - **Source/Target**: Chọn từ danh sách instance trong Notion.

#### **B. Cấu Hình Node Quan Trọng**
1. **Node `Get Instance Information` (chế độ động)**:
   - **Credentials**: Chọn `notionApi`.
   - **Operation**: `getAll`.
   - **Resource**: `databasePage`.
   - **Database ID**: Điền ID của database Notion chứa instance (tham khảo [Notion API Docs](https://developers.notion.com/docs/getting-started)).

2. **Node `Create Workflow(s)` và `Create Workflow(s)1`**:
   - **Credentials**: Chọn `n8nApi` (credentials của instance đích).
   - **Operation**: `create`.
   - **Headers**: Đảm bảo có `Authorization: Bearer {API_KEY}`.

3. **Node `Set Workflow Display Name`**:
   - **Dynamic Mode**: Sử dụng `{{ $node["Set Source Name and URL"].json["name"] }}` để tự động đặt tên.
   - **Static Mode**: Điền tên cố định (ví dụ: `"Workflow từ Instance Nguồn"`).

4. **Node `Filter Our Archived Items` và `Filter Our Archived Items1`**:
   - **Lọc bỏ workflow đã archived**: Đặt điều kiện `{{ $json["isArchived"] }} === false`.

#### **C. Chọn Chế Độ Hoạt Động**
Workflow có **hai nhánh chính**:
- **Simple Mode**: Sử dụng credentials cố định (nhánh `Set Source` và `Set Target`).
- **Dynamic Mode**: Lấy instance từ Notion (nhánh `Get Instance Information`).

Các sếp cần **chỉnh node `Route Mode` (Switch)** để chọn chế độ:
- **Dynamic**: Chọn nhánh `dynamic`.
- **Static**: Chọn nhánh `static`.

---
### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Chọn **Test Tab** và nhấn **Run Workflow**.
   - Điền **workflow IDs** từ instance nguồn (nếu chế độ đơn giản) hoặc chọn instance từ Notion (nếu chế độ động).
2. **Bật Active**:
   - Sau khi test thành công, chuyển sang **Active** và bật **Webhook** (nếu cần).

---
## ✍️ **Mẹo & Gợi Ý Nâng Cao**

:::tip[**Tips Cho Các Sếp**]
1. **Lưu log hoạt động**:
   - Thêm node **Slack/Telegram** sau `Results (Dynamic)` và `Results (Static)` để báo cáo kết quả.
   - Ví dụ: `{{ $json["status"] }}: {{ $json["workflowName"] }} đã chuyển thành công!`

2. **Tự động chuyển định kỳ**:
   - Sử dụng **n8n Cron Trigger** để chạy workflow hàng ngày/tuần.
   - Ví dụ: Chuyển workflow từ `dev` sang `staging` vào mỗi thứ 7.

3. **Kết hợp với GitHub**:
   - Sau khi chuyển workflow, **push JSON vào GitHub** để backup.
   - Sử dụng node **GitHub** và `Create/Update File`.

4. **Tự động rename workflow**:
   - Thêm node **Code** sau `Set Workflow Display Name` để tự động thêm prefix/suffix (ví dụ: `Dev_` + tên workflow).

5. **Quản lý nhiều instance**:
   - Nếu dùng **chế độ động**, các sếp có thể thêm nhiều instance vào Notion và chuyển nhật giữa chúng một cách dễ dàng.
   - Ví dụ: Chuyển workflow từ `staging` sang `production` khi cần.
:::

---
## 📌 **Kết Luận**

Workflow này là **công cụ vàng** cho các sếp quản lý **nhiều instance n8n** mà không muốn mất thời gian export/import thủ công. Nó hỗ trợ cả **chế độ đơn giản** (fixed credentials) và **chế độ động** (lấy từ Notion), giúp các sếp:
✔ **Tiết kiệm thời gian** với tự động hóa hoàn toàn.
✔ **Tránh lỗi bulk import** bằng cách chọn lọc workflow.
✔ **Quản lý an toàn** với API key được lưu trong Notion/Supabase.
✔ **Hiển thị kết quả rõ ràng** cho từng workflow.

**Hãy áp dụng ngay và làm việc với n8n như một chuyên gia!** 🚀

---
:::info[**Gợi Ý Hạ Tầng Cho n8n**]
Để workflow chạy **ổn định 24/7**, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**Bạn có câu hỏi về cách cấu hình? Hãy để lại comment bên dưới!** 👇