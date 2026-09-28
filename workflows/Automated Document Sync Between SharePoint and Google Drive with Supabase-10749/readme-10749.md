---
title: "🔄 **Tự Động Hóa Đồng Bộ Hóa Tệp Từ SharePoint Sang Google Drive Với Supabase - Không Cần Code!**"
description: "Workflow tự động đồng bộ hóa toàn bộ tập tin mới/được cập nhật từ SharePoint sang Google Drive, đồng thời ghi nhớ metadata vào cơ sở dữ liệu Supabase/PostgreSQL. Giúp các sếp tiết kiệm thời gian quản lý dữ liệu và đảm bảo an toàn sao lưu 24/7."
slug: "tieu-dong-bo-hoa-sharepoint-sang-google-drive-suabase"
tags: [n8n, automation, sharepoint, google-drive, supabase, file-management, no-code]
keywords: [tự động hóa sharepoint google drive, đồng bộ hóa tập tin, supabase n8n, lưu trữ an toàn dữ liệu, tự động hóa không code]
---

# 🚀 **Tự Động Hóa Đồng Bộ Hóa Tệp Từ SharePoint Sang Google Drive Với Supabase**

### **Giải Pháp Cho Nỗi Đau Của Các Sếp**
Các sếp đã từng phải **tốn thời gian thủ công** sao lưu tập tin từ SharePoint sang Google Drive? Hay phải **lo lắng dữ liệu bị mất** khi không có bản sao lưu tự động? Hoặc **không biết cách kiểm soát** tập tin đã được đồng bộ hóa trước đó?

Workflow này **giải quyết tất cả** bằng cách:
✅ **Tự động đồng bộ hóa** tất cả tập tin mới/được cập nhật từ SharePoint sang Google Drive.
✅ **Ghi nhớ metadata** (thông tin chi tiết về tập tin) vào cơ sở dữ liệu **Supabase/PostgreSQL** để theo dõi lịch sử.
✅ **Lọc bỏ tập tin không cần thiết** (tệp hệ thống, tạm thời) để tránh lãng phí dung lượng.
✅ **Chạy tự động theo lịch** (ngày/ngày, tuần/tuần) để không phải nhớ nhắc.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS riêng.
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (đảm bảo tốc độ cao, không lag)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần sao lưu thủ công hàng ngày.
- **An toàn dữ liệu**: Sao lưu tự động lên Google Drive và Supabase.
- **Dễ quản lý**: Theo dõi lịch sử cập nhật tập tin qua cơ sở dữ liệu.
- **Tự động hóa hoàn toàn**: Chỉ cần bật workflow, nó sẽ làm việc 24/7.
- **Không phụ thuộc vào người dùng**: Không lo quên hoặc làm sai.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
✔ **Tài khoản SharePoint** (để truy cập thư mục cần đồng bộ).
✔ **Tài khoản Google Drive** (để lưu tập tin sao lưu).
✔ **Cơ sở dữ liệu Supabase/PostgreSQL** (để lưu metadata).
✔ **API Keys/Credentials** của các dịch vụ trên (cách lấy ở [n8n docs](https://docs.n8n.io/)).
✔ **Thư mục SharePoint cụ thể** (URL của thư mục cần đồng bộ).
✔ **Tên bảng trong Supabase** (mặc định là `n8n_metadata`, có thể thay đổi).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có **2 cách** để import workflow này:
- **Tải file JSON** từ [n8n.io/workflows/10749](https://n8n.io/workflows/10749) và import vào **n8n Editor**.
- **Copy toàn bộ JSON** từ link trên và **paste** vào **Import Workflow** trong n8n.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này có **15 node**, nhưng các sếp chỉ cần chú ý đến **các node quan trọng sau**:

##### **A. Cấu Hình Credentials (Bắt Buộc)**
| Node | Yêu Cầu Cần Chỉnh |
|------|-------------------|
| **Microsoft SharePoint HTTP Request** | Thêm **URL SharePoint** (ví dụ: `https://tendoanhnghiep.sharepoint.com/sites/TenSite/Thumuc`) |
| **Supabase** | Chọn **supabaseApi** (đã cấu hình trước) và **tên bảng** (`n8n_metadata`). |
| **Google Drive** | Chọn **googleDriveOAuth2Api** (đã cấu hình OAuth2). |
| **Schedule Trigger** | Chọn **thời gian chạy** (ví dụ: hàng ngày 2 giờ sáng). |

##### **B. Cấu Hình Node Code (Lọc Tệp)**
Node **"filter files"** (Code) có **mã lọc mặc định** để bỏ các tập tin không cần thiết như:
```javascript
// Lọc bỏ các tập tin hệ thống và tạm thời
const excludedExtensions = ['~$', '.db', '.msg', '.xlsx', '.pptx', '.tmp'];
return items.filter(item =>
  !excludedExtensions.some(ext => item.name.toLowerCase().endsWith(ext))
);
```
**Các sếp có thể chỉnh sửa** danh sách `excludedExtensions` nếu cần.

##### **C. Node "Compare Datasets" (So Sánh Dữ Liệu)**
Node này **so sánh** tập tin mới/được cập nhật từ SharePoint với dữ liệu đã lưu trong Supabase.
- Nếu **tập tin mới**, nó sẽ đồng bộ hóa.
- Nếu **tập tin đã tồn tại**, nó sẽ **bỏ qua** (trừ khi có thay đổi).

##### **D. Node "Upload file" (Google Drive)**
- **Tên tập tin trên Google Drive** sẽ được **đổi tên** theo tên gốc từ SharePoint (node `rename files`).
- **Metadata** (thông tin như ngày cập nhật, kích thước) sẽ được **ghi vào Supabase**.

##### **E. Node "Insert Document Metadata" (Supabase)**
- **Upsert** (Update hoặc Insert) dữ liệu vào bảng `n8n_metadata`.
- Các trường cần thiết:
  - `sharepoint_url` (URL SharePoint)
  - `google_drive_url` (URL Google Drive)
  - `last_modified_date` (ngày cập nhật cuối cùng)
  - `loading_done` (trạng thái đã đồng bộ hóa)

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run** với **1-2 tập tin mẫu** để kiểm tra:
   - Tập tin có được tải xuống từ SharePoint không?
   - Tập tin có được upload lên Google Drive không?
   - Metadata có được ghi vào Supabase không?
2. **Bật Active** workflow sau khi kiểm tra thành công.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::tip[CÁCH LÀM NGOÀI THƯỜNG]
- **Gửi thông báo Slack/Telegram** khi đồng bộ hóa hoàn tất:
  - Sử dụng **node `n8n-nodes-base.slack`** hoặc **`n8n-nodes-base.telegram`** sau node `Upload file`.
  - Ví dụ: `Tập tin [Tên tập tin] đã được đồng bộ hóa từ SharePoint sang Google Drive!`.
- **Lưu log vào Google Sheets** để theo dõi lịch sử:
  - Thêm **node `n8n-nodes-base.googleSheets`** sau node `Insert Document Metadata`.
- **Tự động xóa tập tin cũ** trong Google Drive (nếu không cần):
  - Sử dụng **node `n8n-nodes-base.googleDrive`** với **operation: delete** (cần cẩn thận để không xóa nhầm).
- **Kết hợp với AI** để tự động **tên tập tin** hoặc **tạo mô tả**:
  - Sử dụng **node `n8n-nodes-base.llm`** (OpenAI, Mistral) để tự động **tên tập tin** dựa trên nội dung.
:::

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** của các sếp khỏi công việc **sao lưu thủ công**, đồng thời **đảm bảo dữ liệu an toàn** với **hai bản sao lưu** (SharePoint + Google Drive + Supabase).

**Hành động ngay hôm nay:**
1. **Import workflow** và cấu hình theo hướng dẫn.
2. **Bật Schedule Trigger** để chạy tự động hàng ngày.
3. **Quên đi lo lắng về mất dữ liệu**!

---
**Cần hỗ trợ?** Liên hệ với **Digital Biz Tech** qua:
📩 Email: [shilpa.raju@digitalbiz.tech](mailto:shilpa.raju@digitalbiz.tech)
🔗 Website: [https://www.digitalbiz.tech](https://www.digitalbiz.tech)
💬 DM LinkedIn: [Digital Biz Tech](https://www.linkedin.com/company/digitalbiztech/)