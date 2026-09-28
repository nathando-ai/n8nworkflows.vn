---
title: "🚀 Tự Động Hóa Từ Notion Sang GitHub Với Thông Báo Email Tự Động - Giảm 90% Thời Gian Quản Lý Project"
description: "Workflow này tự động chuyển đổi các task từ Notion sang GitHub Issues, cập nhật trạng thái và gửi thông báo email cho team khi có sự thay đổi. Giúp các sếp tiết kiệm 90% thời gian quản lý project, giảm thiểu lỗi nhân sự và duy trì tính nhất quán trong quá trình phát triển."
slug: "tieu-dong-hoa-notion-sang-github-voi-email-notification"
tags: [n8n, automation, project-management, notion, github, gmail, no-code]
keywords: [tự động hóa notion github, quản lý project tự động, workflow n8n notion, gửi email tự động từ notion, tự động hóa github issue]
---

# 🚀 **Tự Động Hóa Từ Notion Sang GitHub Với Thông Báo Email Tự Động**

### **Giải Pháp Cho Các Sếp Bị Chán Nản Với Quá Trình Quản Lý Project Thủ Công**
Các sếp đã từng phải **lặp đi lặp lại** việc:
- **Chuyển task từ Notion sang GitHub** một cách thủ công?
- **Cập nhật trạng thái** sau khi tạo Issue trên GitHub?
- **Gửi email thông báo** cho team khi có sự thay đổi?
- **Lo lắng về tính nhất quán** giữa Notion và GitHub?

Workflow này **giải quyết tất cả** bằng cách **tự động hóa toàn bộ quy trình** chỉ trong **vài phút cấu hình**. Không cần viết code, không cần là dev – chỉ cần **n8n** và một chút kiến thức cơ bản.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS riêng.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** – giảm tới **39%**)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (đủ sức mạnh cho workflow này)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm 90% thời gian** quản lý project (không cần copy-paste thủ công).
✅ **Tránh lỗi nhân sự** (không còn quên cập nhật trạng thái giữa Notion và GitHub).
✅ **Cập nhật tự động** trạng thái từ "To develop" → "In progress" khi Issue được tạo.
✅ **Thông báo email tự động** cho team khi có sự thay đổi (không cần nhớ gửi).
✅ **Duy trì tính nhất quán** giữa Notion và GitHub (không còn "trạng thái mơ hồ").
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
✔ **Tài khoản Notion** (đã tạo database chứa task/feature request).
✔ **Tài khoản GitHub** (đã cấu hình OAuth2 API trong n8n).
✔ **Tài khoản Gmail** (đã cấu hình OAuth2 trong n8n để gửi email).
✔ **API Key Notion** (trong n8n, credentials `notionApi`).
✔ **OAuth2 GitHub** (trong n8n, credentials `githubOAuth2Api`).
✔ **OAuth2 Gmail** (trong n8n, credentials `gmailOAuth2`).

---
:::note[LƯU Ý QUAN TRỌNG]
- **Database Notion** phải có các trường: **Title, Status, Labels, Repository** (hoặc tương tự).
- **GitHub Repository** phải được chỉ định trong trường `Repository` của Notion.
- **Email của team** phải được lưu trong Notion (trường `Email` hoặc `Assignee`).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có **2 cách** để import workflow này:
- **Tải file JSON** từ [n8n.io/workflows/5889](https://n8n.io/workflows/5889) và import vào **n8n Editor**.
- **Copy JSON** từ link trên và **paste** vào **Import Workflow** trong n8n.

:::tip[Mẹo nhanh]
- Mở **n8n Editor** → **Import Workflow** → **Paste JSON** → **Import**.
- Sau đó, **Active workflow** để bắt đầu.
:::

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này được chia thành **3 phần chính**, các sếp cần **cấu hình kỹ** các node sau:

##### **🔹 PHẦN 1: Phát Hiện & Sắp Xếp Task Từ Notion**
| Node | Tác vụ | Cần chỉnh gì? |
|------|---------|----------------|
| **Schedule Trigger** | Khởi động workflow theo lịch | Chọn **interval** (ví dụ: **5 phút**) để kiểm tra Notion thường xuyên. |
| **Get Many Database Pages (Notion)** | Lấy tất cả task từ Notion | Chọn **Database ID** (tìm trong URL Notion: `https://www.notion.so/workspace/.../.../...` → phần cuối). |
| **Sort Issues Fields (Set)** | Sắp xếp lại dữ liệu | Đảm bảo **Title, Status, Labels, Repository** được map chính xác. |
| **Switch (Issue Status Decision)** | Phân loại task theo trạng thái | Cấu hình **condition**:
   - **If status = "To develop"** → Tạo Issue GitHub.
   - **Else** → Gửi email thông báo. |

##### **🔹 PHẦN 2: Tạo Issue GitHub (Nếu Trạng Thái "To Develop")**
| Node | Tác vụ | Cần chỉnh gì? |
|------|---------|----------------|
| **Create an Issue (GitHub)** | Tạo Issue trên GitHub | Chọn **Repository** trong Notion (trường `Repository`) và **labels** (trường `Labels`). |
| **Set Status and Issue URL (Notion Update)** | Cập nhật trạng thái Notion | Chọn **Database ID** và **Page ID** của task cần cập nhật. |

##### **🔹 PHẦN 3: Thông Báo Email Cho Team (Nếu Không Phải "To Develop")**
| Node | Tác vụ | Cần chỉnh gì? |
|------|---------|----------------|
| **Get Many Users (Notion)** | Lấy danh sách team | Chọn **Database Users** (nếu có) hoặc **trường Email** trong task. |
| **Map Notion Users (Set)** | Định dạng email | Đảm bảo **Email** được map từ Notion. |
| **Exclude Bot (Switch)** | Loại bỏ email bot | Thêm **condition**: `email !== "notifications@noreply.com"`. |
| **Group Recipients (Aggregate)** | Nhóm email | Đảm bảo **output** là mảng email. |
| **Send a Message (Gmail)** | Gửi email thông báo | Chọn **From Email** (gmail OAuth2) và **Template Email** (ví dụ: `"Task đã được xử lý: {{title}}"`). |

---
#### **3. Kích Hoạt ⚡️**
- **Test Run** với **1 task mẫu** để kiểm tra:
  - Task "To develop" → **Tạo Issue GitHub thành công** và cập nhật Notion.
  - Task khác → **Gửi email thông báo** cho team.
- **Active workflow** sau khi test thành công.

---
### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Thêm Webhook (nếu không dùng Schedule Trigger)**
   - Nếu các sếp **không muốn chạy theo lịch**, có thể thay thế **Schedule Trigger** bằng **Webhook** (n8n-nodes-base.http).
   - Cấu hình **Notion Webhook** để gửi request khi task được cập nhật.

2. **Lưu Log Cập Nhật**
   - Thêm **Sticky Note** (n8n-nodes-base.stickyNote) sau **Set Status and Issue URL** để ghi lại **URL Issue GitHub** và **thời gian cập nhật**.

3. **Gửi Báo Cáo Định Kỳ**
   - Sử dụng **Schedule Trigger** khác để **tổng hợp và gửi báo cáo** về số lượng task đã xử lý, số Issue mới tạo, và tình trạng team.

4. **Kết Hợp Slack/Telegram**
   - Thay thế **Gmail** bằng **Slack/Telegram Bot** để thông báo nhanh hơn.
   - Sử dụng **n8n-nodes-base.slack** hoặc **n8n-nodes-base.telegram**.

5. **Tự Động Phân Loại Task**
   - Thêm **Switch** thêm để phân loại task theo **Labels** (ví dụ: "Bug" → gửi cho dev, "Feature" → gửi cho PM).

---
### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** của các sếp khỏi việc **quản lý project thủ công**, đồng thời **giảm thiểu lỗi** và **tăng tính nhất quán** giữa Notion và GitHub.

**Hành động ngay hôm nay:**
1. **Import workflow** và cấu hình theo hướng dẫn.
2. **Test với 1 task mẫu** để đảm bảo hoạt động.
3. **Active workflow** và **quên đi việc copy-paste**!

👉 **[Tải workflow nguyên bản](https://n8n.io/workflows/5889)** và bắt đầu tự động hóa ngay!

---
**Cần hỗ trợ?** Để lại comment bên dưới hoặc liên hệ với **Fady Bekkar** (tác giả workflow) qua [n8n Community](https://community.n8n.io/). 🚀