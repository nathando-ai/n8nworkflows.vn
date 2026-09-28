---
title: "💾 **Tự Động Hoàn Hảo: Backup Dữ Liệu Nextcloud 7 Ngày - Không Cần Code!**"
description: "Workflow n8n tự động sao lưu dữ liệu Nextcloud hàng ngày với thời gian lưu trữ 7 ngày, tối ưu hóa không gian và bảo mật thông tin. Giúp các sếp tiết kiệm thời gian và tránh rủi ro mất dữ liệu."
slug: "tieu-dong-hoan-hao-backup-nextcloud-7-ngay"
tags: [n8n, automation, nextcloud, backup, devops]
keywords: [n8n backup nextcloud, tự động hóa lưu trữ, sao lưu dữ liệu tự động, lưu trữ 7 ngày, nextcloud api]
---

# 🚀 **Tự Động Hoàn Hảo: Backup Dữ Liệu Nextcloud 7 Ngày - Không Cần Code!**

### **Nỗi Đau Của Các Sếp**
Các sếp đã bao giờ lo lắng về việc mất dữ liệu quan trọng trên Nextcloud chưa? Hay phải mất thời gian thủ công sao lưu hàng ngày để đảm bảo an toàn? Với **N8N Backup Flow**, các sếp có thể **tự động hóa quá trình sao lưu** dữ liệu Nextcloud một cách **liên tục, chính xác và tiết kiệm thời gian**, đồng thời **giảm thiểu rủi ro mất dữ liệu** nhờ thời gian lưu trữ 7 ngày.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn**: Không cần can thiệp thủ công hàng ngày.
- **Lưu trữ 7 ngày**: Giúp quản lý không gian lưu trữ hiệu quả.
- **Bảo mật dữ liệu**: Sao lưu liên tục, giảm thiểu rủi ro mất dữ liệu.
- **Tiết kiệm thời gian**: Các sếp có thể tập trung vào công việc quan trọng hơn.
- **Hoạt động liên tục**: Chạy 24/7 trên nền tảng VPS ổn định.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
- **Tài khoản Nextcloud**: Các sếp cần có quyền truy cập vào Nextcloud và **API Key** để kết nối.
- **n8n Self-hosted**: Cài đặt n8n trên VPS để workflow hoạt động liên tục.
- **Thư mục `/N8N-Backup`**: Tạo thủ công trên Nextcloud để lưu trữ backup.
- **Credentials Nextcloud API**: Cấu hình trong n8n với tên `nextCloudApi`.
- **Credentials n8n API**: Cấu hình trong n8n với tên `n8nApi` (nếu sử dụng n8n Cloud).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể **import workflow** từ file JSON hoặc **copy/paste JSON** vào n8n Editor:
1. Truy cập [n8n Editor](https://n8n.io/editor/) và chọn **Import Workflow**.
2. Chọn file JSON hoặc **copy toàn bộ mã JSON** từ [link gốc](https://n8n.io/workflows/4338) và dán vào.
3. Nhấn **Import** để hoàn tất.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
##### **a. Cấu Hình Credentials Nextcloud**
- Trong node **Nextcloud Directory**, **Nextcloud Upload**, và **Nextcloud - Delete old backups**, các sếp cần chọn **credentials** là `nextCloudApi`.
- Đảm bảo **API Key** của Nextcloud đã được cấu hình đúng trong **Credentials Manager** của n8n.

##### **b. Thiết Lập Thư Mục Backup**
- **Tạo thư mục `/N8N-Backup`** trên Nextcloud trước khi chạy workflow.
- Trong node **Backup Path**, các sếp cần **chỉnh sửa giá trị** của `$json.backup` thành tên thư mục chính xác (ví dụ: `N8N-Backup`).

##### **c. Cấu Hình Schedule Trigger**
- Node **Schedule Trigger** sẽ chạy **hàng ngày** (mặc định là 00:00 UTC).
- Các sếp có thể **chỉnh sửa lịch chạy** trong node này nếu cần (ví dụ: 22:00 giờ Việt Nam).

##### **d. Logic Xóa Backup Cũ (7 Ngày)**
- Node **Limits Backups** sử dụng **JavaScript** để xóa backup cũ hơn 7 ngày.
- Mở node này và **chỉnh sửa mã** nếu cần thay đổi thời gian lưu trữ (ví dụ: 14 ngày):
  ```javascript
  // Xóa backup cũ hơn 7 ngày
  const now = new Date();
  const sevenDaysAgo = new Date(now);
  sevenDaysAgo.setDate(now.getDate() - 7);

  return {
    json: {
      path: $input.all().filter(item => {
        const backupDate = new Date(item.json.date);
        return backupDate < sevenDaysAgo;
      }).map(item => item.json.path)
    }
  };
  ```

#### **3. Kích Hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu để đảm bảo workflow hoạt động.
2. **Bật Active** workflow để nó chạy tự động hàng ngày.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết Nối Slack/Telegram**: Thêm node **Slack** hoặc **Telegram** để thông báo khi backup thành công/thất bại.
2. **Lưu Log**: Sử dụng node **Sticky Note** hoặc **Google Sheets** để ghi lại lịch sử backup.
3. **Gửi Báo Cáo Định Kỳ**: Tạo một **email báo cáo** hàng tuần về số lượng backup và dung lượng sử dụng.
4. **Tối Ưu Hóa Thư Mục**: Sắp xếp backup theo ngày/tháng để dễ quản lý.

---

### 📌 **Kết Luận**
Với **N8N Backup Flow**, các sếp không chỉ **tự động hóa sao lưu Nextcloud** mà còn **tối ưu hóa không gian lưu trữ** và **bảo mật dữ liệu** một cách hiệu quả. **Không cần code**, chỉ cần **cấu hình và chạy** là xong!

👉 **Hãy áp dụng ngay và trải nghiệm sự tự động hóa hoàn hảo!** 🚀

---
**Ghi chú:** Workflow này được tối ưu cho **Nextcloud 20+**, các sếp có thể điều chỉnh nếu sử dụng phiên bản khác.