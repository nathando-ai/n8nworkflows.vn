---
title: "🔄 Tự Động Hoàn Hảo: Backup Workflows n8n Sang GitHub Mỗi Ngày - Không Lo Lại Mất Dữ Liệu!"
description: "Giải pháp tự động hóa hoàn hảo để sao lưu tất cả workflows n8n của các sếp lên GitHub mỗi ngày, đảm bảo an toàn và dễ dàng phục hồi. Khắc phục hoàn toàn nỗi lo mất dữ liệu do lỗi người dùng hoặc hệ thống."
slug: "tự-dộng-hoàn-hảo-backup-workflows-n8n-sang-github"
tags: [n8n, automation, backup, github, no-code, self-hosted]
keywords: [backup workflows n8n, tự động hóa sao lưu, lưu trữ an toàn workflow, n8n git repository, sao lưu định kỳ]
---

# 🔄 **Tự Động Hoàn Hảo: Sao Lưu Tất Cả Workflows n8n Sang GitHub Mỗi Ngày**

---

### **😫 Nỗi Đau Của Các Sếp Khi Làm Thủ Công**
Các sếp đã từng gặp phải tình huống kinh hoàng khi:
- **Lỗi người dùng**: Xóa nhầm workflow quan trọng trong n8n Editor.
- **Hệ thống crash**: Dữ liệu workflow bị mất do lỗi server hoặc cập nhật không ổn định.
- **Không có bản sao**: Phải mất nhiều giờ để tái tạo lại workflow từ đầu.

**Giải pháp?** Một **workflow tự động hóa hoàn hảo** sao lưu tất cả workflows n8n lên **GitHub** mỗi ngày, **không cần code**, **không cần kỹ thuật**, và **miễn phí**!

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **An toàn tuyệt đối**: Tất cả workflows được sao lưu định kỳ lên GitHub.
- **Khôi phục nhanh chóng**: Nếu xảy ra lỗi, chỉ cần pull từ GitHub là xong.
- **Dễ dàng theo dõi lịch sử**: Theo dõi tất cả thay đổi workflow qua commit trên GitHub.
- **Không phụ thuộc vào hệ thống**: Dữ liệu lưu trữ trên GitHub, không bị ảnh hưởng bởi lỗi server.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Các sếp cần chuẩn bị:
✅ **Tài khoản GitHub** (và **Personal Access Token** với quyền `repo`).
✅ **n8n Self-hosted** (để workflow chạy 24/7).
✅ **Repository GitHub** để lưu trữ backup (ví dụ: `n8n-workflows-backup`).
✅ **API Key của n8n** (để lấy danh sách workflows).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể:
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/2532) và import vào n8n Editor.
- **Copy JSON** từ link trên và dán vào **n8n Editor** (tab `Import`).

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này hoạt động dựa trên **Schedule Trigger** (khởi động hàng ngày) và **GitHub API**. Các bước quan trọng cần chỉnh:

##### **A. Cấu Hình GitHub Credentials**
- **Node "GitHub" (lấy file)** và **"Create new file and commit"**:
  - Đi đến **Credentials** → **Add GitHub API**.
  - Nhập **Personal Access Token** (tạo ở [GitHub Settings → Developer Settings → Personal Access Tokens](https://github.com/settings/tokens)).
  - Chọn quyền `repo` (để push/pull file).

##### **B. Cấu Hình n8n API Key**
- **Node "n8n" (lấy danh sách workflows)**:
  - Đi đến **Credentials** → **Add n8n API**.
  - Nhập **API Key** của n8n (tìm ở `Settings → API` trong n8n Dashboard).

##### **C. Thiết Lập Repository GitHub**
- **Node "Create new file and commit"**:
  - Điền **Repository Name** (ví dụ: `n8n-workflows-backup`).
  - Điền **File Path** (ví dụ: `workflows/backup_$(date +%Y-%m-%d).json`).
  - **Branch** mặc định là `main`.

##### **D. Kiểm Tra Logic**
- **Node "If" và "If1"**:
  - Đảm bảo **condition** trong `If` là `$node["n8n"]["json"]["workflows"]` (kiểm tra có workflow mới không).
  - **Node "Code"** (nếu cần xử lý đặc biệt, ví dụ: loại bỏ workflow cũ).

#### **3. Kích Hoạt ⚡️**
- **Test Run**:
  - Chạy **Manual Trigger** để kiểm tra workflow có tạo file JSON trên GitHub không.
  - Kiểm tra **GitHub Repository** xem có file mới được commit không.
- **Bật Active**:
  - Đặt **Schedule Trigger** chạy hàng ngày (ví dụ: `0 0 * * *` - mỗi ngày 00:00).

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::note[CẤP NHẬT & QUẢN LÝ]
- **Tên file tự động**: Sử dụng `$(date +%Y-%m-%d)` để tạo tên file theo ngày (ví dụ: `workflows/backup_2024-05-20.json`).
- **Lọc workflow quan trọng**: Trong **Node "If"**, thêm điều kiện để chỉ backup workflow có tên bắt đầu từ `important_`.
- **Gửi thông báo Slack/Email**: Thêm **Node Slack/Email** sau **Schedule Trigger** để báo cáo khi backup thành công/thất bại.
- **Lưu log**: Sử dụng **Node StickyNote** để ghi lại lỗi hoặc thông tin debug.
:::

---

### 📌 **Kết Luận**
**Không còn lo mất dữ liệu nữa!** Với workflow này, các sếp sẽ:
✔ **Sao lưu tự động** tất cả workflows n8n lên GitHub mỗi ngày.
✔ **Khôi phục nhanh chóng** nếu xảy ra lỗi.
✔ **Dễ dàng theo dõi lịch sử** thay đổi qua GitHub.

**Hành động ngay!**
1. **Import workflow** từ [đây](https://n8n.io/workflows/2532).
2. **Cấu hình GitHub & n8n API Key**.
3. **Bật Schedule Trigger** và **chờ backup tự động**!

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**Chia sẻ workflow này với đồng nghiệp để cùng tránh rủi ro mất dữ liệu!** 🚀