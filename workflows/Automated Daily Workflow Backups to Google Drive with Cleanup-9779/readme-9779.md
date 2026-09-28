---
title: "🚀 Tự Động Hoàn Chỉnh & Backup Workflow n8n Hàng Ngày Sang Google Drive (Với Lọc Giữa Dữ Liệu & Xóa Dư Liệu)"
description: "Workflow tự động hóa hoàn chỉnh giúp các sếp backup tất cả workflow n8n hàng ngày sang Google Drive, đồng thời tự động xóa backup cũ để tiết kiệm không gian. Hoạt động 24/7 với lịch trình tự động, không cần can thiệp thủ công."
slug: "tự-dộng-hoàn-chỉnh-backup-workflow-n8n-sang-google-drive"
tags: [n8n, automation, no-code, google-drive, backup-automation]
keywords: [tự động hóa n8n, backup workflow n8n, tự động xóa file cũ google drive, tự động hóa hàng ngày, n8n google drive integration]
---

# 🚀 **Tự Động Hoàn Chỉnh & Backup Workflow n8n Hàng Ngày Sang Google Drive**

### **Giải pháp hoàn hảo cho các sếp quản lý nhiều workflow n8n**
Làm thủ công backup workflow n8n hàng ngày không chỉ tốn thời gian mà còn dễ bị lỗi nhân sự hoặc quên. **Workflow này tự động hóa toàn bộ quy trình**, bao gồm:
- **Backup tất cả workflow** sang Google Drive dưới dạng JSON.
- **Tạo thư mục mới** với định dạng rõ ràng (`Workflow Backups [Ngày-Tháng-Năm]`).
- **Xóa tự động backup cũ** để tiết kiệm không gian lưu trữ.
- **Hoạt động hàng ngày** (cấu hình được thay đổi) mà không cần can thiệp.

Không cần viết code, chỉ cần **cài đặt và chạy** – workflow sẽ tự động hoạt động 24/7!

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo tính liên tục và bảo mật.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần backup thủ công hàng ngày.
- **An toàn dữ liệu**: Backup tự động với định dạng JSON dễ đọc.
- **Tối ưu không gian**: Xóa tự động backup cũ sau 30 ngày (cấu hình được điều chỉnh).
- **Hoạt động liên tục**: Lịch trình tự động (4:00 AM hàng ngày) không cần can thiệp.
- **Dễ dàng phục hồi**: Tất cả workflow được lưu trữ trên Google Drive, có thể khôi phục nhanh chóng.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Google Drive** với quyền chỉnh sửa.
2. **API Key của n8n** (nếu self-hosted) hoặc **URL API của n8n Cloud**.
   - **URL API**: `https://[tên-máy-chủ-n8n].n8n.io/api/v1` (hoặc `https://[tên-doman].n8n.cloud/api/v1`).
3. **Thư mục Google Drive** để lưu backup (không bắt buộc, workflow sẽ tự tạo).

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n.io/workflows/9779](https://n8n.io/workflows/9779) và import vào **n8n Editor**.
- **Cách 2**: Copy toàn bộ JSON từ [đây](link-json) và dán vào **Create Workflow** trong n8n.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này có **hai đường dẫn chính**:
- **Đường dẫn trên (Cleanup)**: Xóa backup cũ.
- **Đường dẫn dưới (Backup)**: Tạo backup mới.

##### **A. Cấu hình n8n API (2 node)**
- **Node `n8n1` và `n8n2`**:
  - **Credentials**: Chọn `n8nApi`.
  - **URL API**: Điền `https://[tên-máy-chủ].n8n.io/api/v1` (hoặc URL của n8n Cloud).
  - **Authentication**: Chọn `Bearer Token` và điền **API Key** từ n8n (tìm ở `Settings > API`).

##### **B. Cấu hình Google Drive (6 node)**
- **Node `create new folder1` và `create new folder2`**:
  - **Credentials**: Chọn `googleDriveOAuth2Api`.
  - **Folder Name**: Đặt định dạng: `Workflow Backups [Ngày-Tháng-Năm]` (ví dụ: `Workflow Backups 15-10-2024`).
    *Lưu ý*: Sử dụng **`{{ $node["Schedule Trigger1"]["json"]["date"] }}`** để tự động lấy ngày tháng.

- **Node `Google Drive1` và `Google Drive2`**:
  - **Credentials**: Chọn `googleDriveOAuth2Api`.
  - **Folder ID**: Chọn thư mục mới tạo ở trên.
  - **File Name**: Đặt định dạng: `[[workflow-name]].json` (ví dụ: `my-workflow.json`).

- **Node `delete folder1` và `delete folder2`**:
  - **Credentials**: Chọn `googleDriveOAuth2Api`.
  - **Filter**: Chỉ xóa thư mục **không phải thư mục mới nhất** (cấu hình ở node `Filter1` và `Filter2`).
    *Lưu ý*: Cần **định rõ tuổi thư mục** để xóa (ví dụ: xóa thư mục >30 ngày).

##### **C. Cấu hình Lịch Triggers (2 node)**
- **Node `Schedule Trigger1` và `Schedule Trigger2`**:
  - **Cron Expression**: Đặt `0 0 4 * * *` để chạy **lúc 4:00 AM hàng ngày**.
  - *Lưu ý*: Thay đổi thời gian theo nhu cầu (ví dụ: `0 0 10 * * *` để chạy lúc 10:00 AM).

##### **D. Cấu hình Filter (2 node)**
- **Node `Filter1` và `Filter2`**:
  - **Condition**: Lọc thư mục **không phải thư mục mới nhất** (đặt điều kiện `folder.name != "Workflow Backups [Ngày-Hiện-Tại]"`).

---

#### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Chạy **manual test** với một workflow mẫu để kiểm tra backup và xóa thư mục.
2. **Active Workflow**:
   - Bật **Active** và lưu workflow.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Tăng độ an toàn**:
   - **Mã hóa API Key**: Sử dụng **n8n Secrets Manager** để lưu trữ API Key an toàn.
   - **Lọc backup theo ngày**: Thêm điều kiện trong `Filter` để chỉ xóa backup >60 ngày.

2. **Tích hợp Slack/Telegram**:
   - Thêm **node `slack`** hoặc **`telegram`** để thông báo khi backup thành công/thất bại.
   - *Ví dụ*: Gửi tin nhắn: `🔄 Backup workflow n8n thành công vào [Ngày-Tháng]`.

3. **Lưu log hoạt động**:
   - Thêm **node `googleSheets`** để ghi log tất cả backup (thời gian, số lượng workflow, trạng thái).

4. **Backup định kỳ khác**:
   - Sử dụng **cron expression** khác để backup vào cuối tuần (ví dụ: `0 0 22 * * 0` để chạy vào 22:00 thứ Bảy).

---

### 📌 **Kết luận**
Workflow này **giải phóng hoàn toàn thời gian** của các sếp khỏi việc backup thủ công, đồng thời **tối ưu hóa không gian lưu trữ** bằng cách xóa tự động backup cũ. **Chỉ cần import, cấu hình và bật Active** – workflow sẽ tự động hoạt động hàng ngày!

**Hành động ngay**:
1. Import workflow vào n8n.
2. Cấu hình API và Google Drive theo hướng dẫn.
3. **Bật Active** và quan sát kết quả!

---
**💡 Chia sẻ & cải tiến**:
Nếu các sếp muốn **thêm tính năng** như backup vào Dropbox hoặc OneDrive, hãy liên hệ với tôi để tôi giúp **tái cấu trúc workflow**! 🚀