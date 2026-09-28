---
title: "🚀 Tự Động Hóa Nhập Workflow n8n Từ GitHub (Đa Nested Folder) - Không Cần Code"
description: "Workflow này giúp các sếp tự động hóa việc chọn lọc và nhập các workflow n8n từ GitHub, bao gồm cả thư mục con (nested folders), tiết kiệm thời gian và tránh sai sót thủ công. Hỗ trợ kiểm soát hoàn toàn quá trình import."
slug: "tu-dong-hoa-nhap-workflow-n8n-tu-github"
tags: [n8n, automation, file-management, github, no-code, workflow-import]
keywords: [n8n workflow từ GitHub, tự động hóa import workflow, nested folder automation, n8n API, GitHub API]
---

# 🚀 **Tự Động Hóa Nhập Workflow n8n Từ GitHub (Đa Nested Folder) - Không Cần Code**

## **🔥 Nỗi Đau Của Các Sếp Khi Làm Thủ Công**
Hiện nay, khi muốn nhập các **workflow n8n** từ **GitHub** vào môi trường tự động hóa của mình, các sếp thường phải:
✅ **Tải xuống từng file** từ các thư mục khác nhau trên GitHub.
✅ **Sắp xếp và chọn lọc** các workflow cần thiết (tránh nhầm lẫn giữa các thư mục con).
✅ **Chỉnh sửa thủ công** để loại bỏ các trường không tương thích với API n8n.
✅ **Nhập từng workflow một** vào hệ thống, dễ gây lỗi và mất thời gian.

**Kết quả?** Thời gian và công sức bị "phá hủy" vì quá trình thủ công, dễ xảy ra sai sót, và không thể kiểm soát được quy trình.

---
## **🎯 Kết Quả Các Sếp Nhận Được**
Sau khi áp dụng workflow này, các sếp sẽ:
✔ **Tiết kiệm thời gian** lên đến **90%** so với cách làm thủ công.
✔ **Nhập workflow chính xác** từ **tất cả thư mục con (nested folders)** mà không lo bỏ sót.
✔ **Lựa chọn linh hoạt** các workflow cần thiết thông qua **form động**.
✔ **Tự động loại bỏ trường không tương thích** với API n8n (tránh lỗi import).
✔ **Hoạt động liên tục** (24/7) khi cài đặt trên **VPS tự chủ**.

---
## **🔧 Yêu Cầu Cần Thiết**
Để workflow hoạt động, các sếp cần chuẩn bị:
🔹 **Tài khoản GitHub** với quyền truy cập vào các repository chứa workflow.
🔹 **Personal Access Token (PAT) GitHub** (có quyền `repo`).
🔹 **API Key của n8n** (để tạo workflow mới).
🔹 **Môi trường n8n** (cài đặt trên **Self-hosted** hoặc **n8n.cloud**).

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

## **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/13300) hoặc copy/paste JSON vào **n8n Editor**.
- **Nhấn "Import"** và chọn **Active** để kích hoạt.

### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
#### **🔹 Cấu Hình Form "Repo Owner" (Node: "On form submission")**
- **Không được đổi tên field** (`Repo Owner`) hoặc loại (`Dropdown`).
- **Chỉ cập nhật**:
  - **Default value**: Tên tổ chức/người dùng GitHub của bạn (ví dụ: `n8n-io`).
  - **Dropdown options**: Danh sách các tổ chức/người dùng GitHub bạn muốn truy cập (ví dụ: `["n8n-io", "my-org"]`).

#### **🔹 Thêm Credentials GitHub & n8n API**
- **GitHub API**:
  - Tạo **Personal Access Token** trên GitHub (quyền `repo`).
  - Thêm vào **Credentials** của node `Get repositories for an organization` và `Get a file`.
- **n8n API Key**:
  - Tạo **API Key** trong **Settings → API Keys** của n8n.
  - Thêm vào **Credentials** của node `Create a workflow`.

#### **🔹 Cấu Hình Node "Select Repos" (Form)**
- **Không thay đổi cấu trúc JSON** của form (được tự động sinh ra từ workflow).
- **Chỉ cần chọn tổ chức/người dùng** từ dropdown đã cấu hình ở trên.

#### **🔹 Node "Select Workflow(s)" (Form)**
- Sau khi workflow quét xong tất cả file, **form động** sẽ hiển thị danh sách workflow.
- **Chọn các workflow cần import** bằng cách nhấn vào checkbox.

#### **🔹 Node "Create a workflow" (n8n API)**
- **Không cần chỉnh sửa** (workflow tự động loại bỏ trường không tương thích).

---
### **3. Kích Hoạt ⚡️**
1. **Test run** với một repository nhỏ để kiểm tra.
2. **Bật Active** workflow.
3. **Chọn tổ chức/người dùng** trong form và **nhấn Submit**.
4. **Chọn các workflow** cần import và **xác nhận**.

---
## **✍️ Mẹo & Gợi Ý Nâng Cao**
🔹 **Lưu log hoạt động**:
- Sử dụng **node `stickyNote`** để ghi lại kết quả import (thành công/thất bại).
- **Gửi báo cáo định kỳ** qua **Slack/Email** bằng node `slack` hoặc `email`.

🔹 **Tự động import định kỳ**:
- Sử dụng **node `set`** để lưu trạng thái cuối cùng.
- **Kết hợp với `webhook`** để kích hoạt lại workflow khi có thay đổi trên GitHub.

🔹 **Xử lý lỗi tự động**:
- Thêm **node `if`** để kiểm tra lỗi và **gửi thông báo lỗi** qua Slack/Email.

🔹 **Nhập vào nhiều repository cùng lúc**:
- Sử dụng **node `merge`** để kết hợp dữ liệu từ nhiều tổ chức/người dùng.

---
## **📌 Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc **nhập workflow thủ công**, đồng thời **giảm thiểu sai sót** và **tăng cường kiểm soát**. Với **cấu trúc queue-based**, nó **không sử dụng recursion**, đảm bảo **ổn định và hiệu quả** ngay cả với repository lớn.

**Hãy thử ngay!** Import workflow này, cấu hình nhanh chóng và **tự động hóa quy trình import workflow n8n** của mình trong vài phút.

---
**🚀 Cần hỗ trợ thêm?** Hãy để lại comment bên dưới hoặc liên hệ với [n8n Community](https://community.n8n.io/)!