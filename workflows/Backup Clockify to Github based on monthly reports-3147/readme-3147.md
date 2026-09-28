---
title: "🚀 Tự Động Hoàn Hảo: Backup Báo Cáo Clockify Sang GitHub Mỗi Tháng (Không Cần Code)"
description: "Giải pháp tự động hóa hoàn toàn tự động sao lưu báo cáo thời gian làm việc từ Clockify sang GitHub hàng tháng, đảm bảo dữ liệu an toàn và dễ truy cập. Tiết kiệm thời gian, tránh mất mát thông tin quan trọng."
slug: "backup-clockify-to-github-monthly-reports"
tags: [n8n, automation, no-code, clockify, github, backup-data]
keywords: [tự động hóa clockify, backup báo cáo thời gian, sao lưu dữ liệu clockify, n8n workflow, tự động hóa hr, lưu trữ báo cáo hàng tháng]
---

# 🚀 **Tự Động Hoàn Hảo: Sao Lưu Báo Cáo Clockify Sang GitHub Mỗi Tháng (Không Cần Code)**

### **Nỗi Đau Của Các Sếp**
Làm thủ công sao lưu báo cáo thời gian từ **Clockify** sang **GitHub** hàng tháng là một công việc tẻ nhạt, dễ bị bỏ quên và tốn thời gian. Nếu không sao lưu kịp thời, dữ liệu quan trọng như **thời gian làm việc, dự án, và thẻ tag** có thể bị mất hoặc không đồng bộ. Kết quả là:
- **Rủi ro mất dữ liệu** khi không sao lưu định kỳ.
- **Tốn thời gian** để xuất báo cáo và chuyển sang GitHub.
- **Khó theo dõi lịch sử** vì dữ liệu phân tán trên nhiều nơi.

**Workflow này giải quyết tất cả vấn đề đó bằng cách tự động hóa hoàn toàn quá trình sao lưu, đảm bảo dữ liệu an toàn và dễ truy cập mọi lúc.**

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài **n8n trên VPS riêng (Self-hosted)** để tránh giới hạn của phiên bản miễn phí.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tự động hóa hoàn toàn** – Không cần can thiệp thủ công hàng tháng.
✅ **Dữ liệu an toàn** – Sao lưu báo cáo thời gian từ **3 tháng trở lại đây** (có thể điều chỉnh).
✅ **Dễ truy cập** – Tất cả báo cáo được lưu trên **GitHub**, có thể chia sẻ hoặc phân tích dễ dàng.
✅ **Không mất dữ liệu** – Thay vì xuất báo cáo thủ công, workflow tự động lấy dữ liệu từ **Clockify** và cập nhật lên **GitHub**.
✅ **Tiết kiệm thời gian** – Giải phóng thời gian cho công việc quan trọng hơn.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
1. **Tài khoản Clockify** với quyền truy cập API.
2. **Tài khoản GitHub** và một **repository** để lưu báo cáo.
3. **API Key của Clockify** (tạo tại [Clockify API Settings](https://clockify.me/api-settings)).
4. **Personal Access Token của GitHub** (tạo tại [GitHub Settings > Developer Settings > Personal Access Tokens](https://github.com/settings/tokens)).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/3147](https://n8n.io/workflows/3147) hoặc copy JSON từ trang này.
- Mở **n8n Editor** → Nhấn **"Import"** → Dán JSON hoặc tải file JSON.
- **Kích hoạt workflow** bằng cách bật nút **"Active"** ở góc trên bên phải.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này có **16 node** và cần cấu hình chính xác như sau:

##### **A. Cấu Hình Globals (Tham số toàn cục)**
- **Node: "Globals" (type: set)**
  - **Repository Owner**: Tên **username/organization** của GitHub.
  - **Repository Name**: Tên **repository** muốn lưu báo cáo.
  - **Clockify Workspace ID** (tùy chọn): Nếu muốn sử dụng **workspace cụ thể** thay vì lấy tự động.

##### **B. Cấu Hình Schedule Trigger (Lịch chạy tự động)**
- **Node: "Schedule Trigger" (type: scheduleTrigger)**
  - **Default**: Chạy **một lần mỗi ngày** (có thể điều chỉnh theo nhu cầu).
  - **Gợi ý**: Chạy vào **cuối tháng** để sao lưu báo cáo mới nhất.

##### **C. Cấu Hình Scope (Tùy Chọn: Thời gian sao lưu)**
- **Node: "Set month indexes" (type: set)**
  - **Default**: Sao lưu **3 tháng gần nhất** (`_0 = tháng hiện tại, _1 = tháng trước, _2 = tháng trước đó`).
  - **Cách chỉnh**: Thay đổi giá trị trong **JSON Expression** để sao lưu nhiều tháng hơn.

##### **D. Cấu Hình Clockify API**
- **Node: "Get first workspace" (type: clockify)**
  - **Credentials**: Chọn **clockifyApi** (đã cấu hình trước).
  - **Resource**: `workspace` (lấy ID workspace mặc định).

- **Node: "Get detailed monthly report" (type: httpRequest)**
  - **Credentials**: Chọn **clockifyApi**.
  - **URL**: `https://api.clockify.me/api/v1/workspaces/{workspaceId}/reports/monthly` (được tự động lấy từ node trước).
  - **Headers**: Thêm `Authorization: Bearer {clockifyApiToken}`.

##### **E. Cấu Hình GitHub**
- **Node: "Check if file exists in GitHub" (type: github)**
  - **Credentials**: Chọn **githubApi**.
  - **Operation**: `get` (kiểm tra file có tồn tại không).
  - **File Path**: `reports/{month}-{year}.json` (ví dụ: `reports/05-2024.json`).

- **Node: "Update file in GitHub" (type: github)**
  - **Credentials**: Chọn **githubApi**.
  - **Operation**: `edit` (cập nhật file nếu đã tồn tại).
  - **File Path**: `reports/{month}-{year}.json`.

- **Node: "Create file in GitHub" (type: github)**
  - **Credentials**: Chọn **githubApi**.
  - **Operation**: `create` (tạo file mới nếu chưa tồn tại).
  - **File Path**: `reports/{month}-{year}.json`.
  - **Content**: Dữ liệu JSON từ Clockify (được xử lý bởi node trước).

##### **F. Cấu Hình Lọc Báo Cáo Trống**
- **Node: "Skip empty reports" (type: filter)**
  - **Expression**: `{{ $json["data"].length > 0 }}` (bỏ qua báo cáo trống).

##### **G. Cấu Hình So Sánh Dữ Liệu (Nếu Có Thay Đổi)**
- **Node: "Compare Datasets" (type: compareDatasets)**
  - **So sánh dữ liệu mới vs cũ** để quyết định **cập nhật** hay **tạo file mới**.
  - **Expression**: `{{ $json["data"] !== $previousJson["data"] }}` (nếu dữ liệu khác nhau).

##### **H. Xử Lý Lỗi (Nếu File Không Tồn Tại)**
- **Node: "Check for 404 error message" (type: if)**
  - **Condition**: Kiểm tra lỗi `404` (file không tồn tại).
  - **Nếu có lỗi**: Chạy node **"Create file in GitHub"**.
  - **Nếu không có lỗi**: Chạy node **"Update file in GitHub"**.

---

#### **3. Kích Hoạt ⚡️**
- **Test Run**: Nhấn **"Run Workflow"** để kiểm tra với dữ liệu mẫu.
- **Bật Active**: Sau khi kiểm tra thành công, bật nút **"Active"** để workflow chạy tự động hàng ngày.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Lưu Log Lịch Sử Sao Lưu**
   - Thêm node **Slack/Telegram** để thông báo khi sao lưu thành công/thất bại.
   - Ví dụ: Gửi tin nhắn `"Sao lưu báo cáo tháng 5/2024 thành công!"` khi workflow hoàn tất.

2. **Tự Động Xóa Báo Cáo Cũ (Nếu Có Thiếu)**
   - Thêm node **GitHub (delete file)** để xóa báo cáo cũ hơn **6 tháng** để giữ gìn không gian.

3. **Kết Hợp Với Google Sheets**
   - Thêm node **Google Sheets** để tự động cập nhật báo cáo vào một bảng tính, giúp dễ theo dõi.

4. **Báo Cáo Định Kỳ Cho Quản Lý**
   - Sử dụng node **Email** để gửi báo cáo tổng hợp hàng tháng cho đội ngũ quản lý.

---

### 📌 **Kết Luận**
Workflow này **giải phóng hoàn toàn thời gian** của các sếp khỏi việc sao lưu báo cáo thủ công, đồng thời **đảm bảo dữ liệu an toàn và dễ truy cập** trên GitHub. **Không cần code**, chỉ cần cấu hình vài bước đơn giản là có thể tự động hóa hoàn toàn quá trình sao lưu báo cáo thời gian từ Clockify.

**Hãy áp dụng ngay để tránh mất dữ liệu và tiết kiệm thời gian cho công việc quan trọng hơn!** 🚀

---
**🔗 [Tải workflow nguyên bản](https://n8n.io/workflows/3147) | 📌 [Cài đặt n8n trên VPS](https://docs.n8n.io/hosting/installation/self-hosted)**