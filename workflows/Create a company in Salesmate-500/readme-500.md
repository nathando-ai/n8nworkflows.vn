---
title: "🚀 Tự Động Hoàn Thành Công Ty Trên Salesmate - Không Cần Code!"
description: "Tiết kiệm 5 phút mỗi ngày bằng cách tự động tạo công ty mới trên Salesmate chỉ với một cú nhấp chuột. Workflow này giúp các sếp CRM không phải nhập liệu thủ công, giảm sai sót và tăng hiệu suất bán hàng."
slug: "tu-dong-tao-cong-ty-salesmate"
tags: [n8n, automation, salesmate, crm, no-code]
keywords: [tự động hóa Salesmate, tạo công ty tự động, n8n workflow sales, tiết kiệm thời gian CRM]
---

# 🚀 **Tự Động Tạo Công Ty Trên Salesmate - Không Cần Code!**

### **Nỗi Đau Của Các Sếp CRM**
Các sếp bán hàng và quản lý CRM thường phải mất **5-10 phút mỗi ngày** để nhập liệu thông tin công ty mới vào Salesmate. Đây là công việc **lặp đi lặp lại, nhàm chán**, dễ gây sai sót và làm giảm hiệu suất làm việc. Hơn nữa, khi có nhiều công ty mới cần nhập, công việc này trở nên **khó quản lý** và **tốn thời gian** hơn.

**Giải pháp?** **Tự động hóa hoàn toàn** với n8n! Workflow này sẽ giúp bạn **tạo công ty trên Salesmate chỉ với một cú nhấp chuột**, không cần viết một dòng code nào.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không phải nhập liệu thủ công, giảm thiểu công việc lặp đi lặp lại.
- **Chính xác 100%**: Không còn sai sót do nhập nhầm thông tin.
- **Tăng hiệu suất bán hàng**: Có thêm thời gian để tập trung vào chiến lược bán hàng thay vì nhập liệu.
- **Hoạt động liên tục**: Workflow có thể được kích hoạt tự động hoặc thủ công tùy ý.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Để workflow này hoạt động, các sếp cần:
- **Tài khoản Salesmate** (đã có API Key).
- **Credentials Salesmate** trong n8n (cấu hình trong **Credentials Manager** của n8n).
- **n8n Self-hosted** (để workflow hoạt động 24/7).

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/500) hoặc copy/paste JSON từ trang này.
- Mở **n8n Editor** → Nhấn **Import** → Dán JSON và nhấn **Import**.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflows này chỉ có **2 node**, nhưng cần cấu hình **Salesmate credentials** chính xác:
- **Node "Salesmate"**:
  - **Credentials**: Chọn **"salesmateApi"** (đã cấu hình trước trong **Credentials Manager** của n8n).
  - **Resource**: Đã mặc định là **"company"** (tạo công ty).
  - **Tham số cần điền**:
    - `name` (tên công ty)
    - `website` (website công ty, nếu có)
    - `industry` (ngành nghề)
    - `phone` (số điện thoại)
    - `email` (email liên hệ)
    - `address` (địa chỉ, nếu cần)

:::note[LƯU Ý QUAN TRỌNG]
- Nếu không có **credentials Salesmate**, workflow sẽ **không hoạt động**.
- Các sếp cần **đăng ký API Key** từ Salesmate và cấu hình trong **Credentials Manager** của n8n.
:::

#### **3. Kích Hoạt ⚡️**
- **Test Run**: Nhấn **"Execute"** để kiểm tra workflow với dữ liệu mẫu.
- **Bật Active**: Sau khi kiểm tra thành công, nhấn **"Active"** để workflow hoạt động.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
- **Tích hợp với Slack/Telegram**: Sau khi tạo công ty thành công, gửi thông báo tự động qua Slack/Telegram để các sếp biết.
- **Lưu log hoạt động**: Sử dụng **node "Set"** để lưu thông tin công ty mới vào một sheet Google Sheets hoặc database.
- **Tự động hóa từ email**: Kết hợp với **node "Email"** để tự động tạo công ty từ email mới nhận được (ví dụ: từ form liên hệ).

---

### 📌 **Kết Luận**
**Tự động hóa tạo công ty trên Salesmate chỉ với một cú nhấp chuột** là cách tối ưu hóa thời gian và giảm sai sót. **Không cần code**, không cần phải là chuyên gia IT, các sếp chỉ cần **cấu hình credentials và kích hoạt workflow** là xong!

**Hãy thử ngay và tiết kiệm thời gian cho công việc bán hàng của mình!** 🚀

---