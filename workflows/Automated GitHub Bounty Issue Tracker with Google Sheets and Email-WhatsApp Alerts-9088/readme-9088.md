---
title: "🚀 **Tự Động Hóa Theo Dõi Bounty GitHub Với Google Sheets + Thông Báo Email/WhatsApp - Giúp Các Sếp Tiết Kiệm 100h/Năm**"
description: "Workflow tự động hóa theo dõi các issue có thưởng (bounty) trên GitHub, cập nhật tự động vào Google Sheets và gửi thông báo qua Email/WhatsApp khi có sự thay đổi mới nhất. Giúp các sếp quản lý dự án open-source hiệu quả mà không cần code."
slug: "tieu-dong-hoa-theo-doi-bounty-github-google-sheets-email-whatsapp"
tags: [n8n, automation, github, google-sheets, email-whatsapp, open-source, no-code]
keywords: [tự động hóa bounty github, theo dõi issue có thưởng, google sheets automation, email whatsapp alert, workflow n8n github]
---

# 🚀 **Tự Động Hóa Theo Dõi Bounty GitHub Với Google Sheets + Thông Báo Email/WhatsApp**

## 🔍 **Nỗi Đau Của Các Sếp Khi Theo Dõi Bounty GitHub Thủ Công**
Các sếp quản lý dự án open-source hay là nhà phát triển thường phải **tốn thời gian hàng giờ mỗi tuần** để:
- **Tra cứu thủ công** các issue có thưởng (bounty) mới trên GitHub.
- **Cập nhật danh sách** vào Google Sheets để theo dõi tiến độ.
- **Gửi thông báo** cho đội nhóm khi có sự thay đổi (mở/đóng issue, thêm bình luận).
- **Lo lắng bỏ lỡ** những bounty mới hoặc cập nhật quan trọng.

**Kết quả?** Thời gian và năng suất bị "chôn vùi" trong công việc lặp đi lặp lại, trong khi các dự án open-source cần sự chú ý kịp thời để tối ưu hóa.

---
## 🎯 **Kết Quả Các Sếp Nhận Được**
Sau khi áp dụng workflow này, các sếp sẽ:
✅ **Tiết kiệm 100+ giờ/năm** không phải tra cứu thủ công.
✅ **Cập nhật tự động** danh sách bounty vào Google Sheets với thông tin chi tiết (tên, trạng thái, ngày tạo, link).
✅ **Nhận thông báo kịp thời** qua Email/WhatsApp khi có:
   - Bounty mới được tạo.
   - Trạng thái issue thay đổi (mở/đóng).
   - Số lượng bình luận tăng (hiệu ứng "hot").
✅ **Quản lý dự án hiệu quả** với dữ liệu thống kê tự động.
✅ **Không cần code** – chỉ cần cấu hình và chạy 24/7.

---
## 🛠️ **Yêu Cầu Cần Thiết**
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản GitHub** (với quyền truy cập API).
2. **Google Sheets** (đã tạo 2 bảng: `Sheet1` và `Sheet2` theo cấu trúc sau):
   - **Sheet1**: Danh sách tất cả bounty (cột: `Issue Name`, `Status`, `Last Updated`, `Link`, `Comments`).
   - **Sheet2**: Bounty gần đây (trong 5 ngày) để gửi thông báo (cột: `Issue Name`, `Notification Sent`).
3. **Tài khoản Email** (để gửi thông báo qua Gmail).
4. **Số điện thoại WhatsApp** (nếu muốn sử dụng thông báo WhatsApp – mặc định là tắt).
5. **API Key GitHub** (tạo tại [Settings > Developer Settings > Personal Access Tokens](https://github.com/settings/tokens) với quyền `repo`).
6. **VPS Self-hosted n8n** (để workflow chạy 24/7).

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
- **Tải file JSON** từ [đây](https://n8n.io/workflows/9088) (hoặc sao chép từ link trên).
- Mở **n8n Editor** → Nhấn `Import` → Dán JSON → Chọn `Import`.

### **2. Các Lưu Ý Bắt Buộc Phải Chỉnh 📌**
Workflow này có **hai phần chính**:
- **Phần 1: Theo dõi bounty mới** (chạy mỗi giờ).
- **Phần 2: Cập nhật trạng thái bounty** (chạy mỗi 6 giờ).

#### **A. Cấu Hình Credentials**
Các sếp cần thiết lập **credentials** cho các node quan trọng:
| **Node**               | **Credentials Cần Thiết**          | **Hướng Dẫn Cấu Hình**                                                                 |
|------------------------|-------------------------------------|----------------------------------------------------------------------------------------|
| GitHub Search          | `httpBearerAuth`                    | Dán **Personal Access Token** của GitHub (tạo tại [Settings > Developer Settings](https://github.com/settings/tokens)). |
| Google Sheets          | `googleSheetsOAuth2Api`             | Thiết lập OAuth 2.0 cho Google Sheets (sử dụng email Gmail của các sếp).              |
| Gmail                  | `gmailOAuth2`                       | Thiết lập OAuth 2.0 cho Gmail (sử dụng email chính thức).                            |
| WhatsApp (nếu sử dụng)| `whatsAppApi`                       | Cần **API Key WhatsApp Business** (hiện tại node này được tắt mặc định).              |

#### **B. Cấu Trúc Google Sheets**
Các sếp cần tạo **2 bảng Google Sheets** với cấu trúc sau:

**Sheet1 (Danh sách tất cả bounty):**
| Issue Name       | Status   | Last Updated | Link                          | Comments |
|------------------|----------|--------------|-------------------------------|----------|
| Fix critical bug | Open     | 2024-05-20   | [GitHub Link](...)            | 5        |

**Sheet2 (Bounty gần đây cho thông báo):**
| Issue Name       | Notification Sent |
|------------------|-------------------|
| New feature      | False             |

#### **C. Cấu Hình Node Quan Trọng**
1. **Schedule Trigger** (2 node):
   - **Node 1**: Chạy **mỗi giờ** để tìm bounty mới.
   - **Node 2**: Chạy **mỗi 6 giờ** để cập nhật trạng thái.
   - **Lưu ý**: Đặt thời gian phù hợp (ví dụ: 8h và 14h).

2. **GitHub Search HTTP Request**:
   - **URL**: `https://api.github.com/search/issues?q=label:"💎 Bounty"&sort=updated-asc&order=asc&per_page=100`
   - **Headers**: Thêm `Accept: application/vnd.github.v3+json`.

3. **Filter New Bounties Only**:
   - **Cấu trúc filter**: Chỉ giữ lại issue **không có trong cột "Issue Name" của Sheet1**.

4. **Format Email Template (HTML)**:
   - Sửa nội dung HTML để phù hợp với brand của các sếp (thêm logo, màu sắc, link website).

5. **Update Row in Sheet**:
   - **Cột cần cập nhật**: `Status`, `Last Updated`, `Comments`.

#### **D. Kích Hoạt Workflow ⚡️**
- **Test Run**:
  - Chạy **manual test** với dữ liệu mẫu từ GitHub để kiểm tra logic.
  - Kiểm tra **Google Sheets** và **Email/WhatsApp** có nhận được thông báo không.
- **Bật Active**:
  - Sau khi kiểm tra thành công, **bật Active** cho cả hai Schedule Trigger.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết hợp với Slack/Telegram**:
   - Thêm node **Slack** hoặc **Telegram Bot** để gửi thông báo nhanh chóng cho đội nhóm.

2. **Lưu Log Cập Nhật**:
   - Thêm node **Sticky Note** hoặc **Google Drive** để lưu lịch sử cập nhật.

3. **Báo Cáo Định Kỳ**:
   - Sử dụng **Google Sheets + Apps Script** để tự động tạo báo cáo tuần/month về số lượng bounty mới và trạng thái.

4. **Tự Động Xóa Bounty Cũ**:
   - Thêm logic **xóa tự động** bounty đã đóng (status = "closed") sau 30 ngày không hoạt động.

5. **Cập Nhật Thông Tin Chi Tiết**:
   - Thêm node **GitHub API** để lấy **comment mới** hoặc **PR liên quan** cho bounty.

---

## 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp quản lý dự án open-source, giúp:
✔ **Tiết kiệm thời gian** với tự động hóa hoàn toàn.
✔ **Cập nhật kịp thời** với thông báo Email/WhatsApp.
✔ **Quản lý hiệu quả** với dữ liệu thống kê tự động.

**Hành động ngay hôm nay!**
1. **Import workflow** vào n8n của các sếp.
2. **Cấu hình credentials** và Google Sheets.
3. **Bật Active** và theo dõi kết quả.

**Chia sẻ kết quả** của các sếp sau khi sử dụng workflow này để cùng nhau tối ưu hóa! 🚀

---
**🔹 Cần hỗ trợ?** Đăng ký hỗ trợ tại [n8n Community](https://community.n8n.io/) hoặc liên hệ với tác giả Jeffrey W. qua [GitHub](https://github.com/jeffreyw).