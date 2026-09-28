---
title: "🚀 Tự Động Hoàn Tất & Sắp Lại Nhiệm Vụ Quá Hạn Asana - Giúp Các Sếp Tiết Kiệm 10+ Giờ/Tháng"
description: "Workflow tự động hóa hoàn tất và sắp lại nhiệm vụ quá hạn trên Asana, giữ không gian làm việc sạch sẽ và tránh quên nhiệm vụ quan trọng. Giúp các sếp tập trung vào công việc chiến lược thay vì quản lý công việc hàng ngày."
slug: "tự-dộng-hoàn-tất-sắp-lại-nhiệm-vụ-asana"
tags: [n8n, automation, asana, no-code, quản lý công việc]
keywords: [tự động hóa asana, sắp lại nhiệm vụ quá hạn, quản lý công việc hiệu quả, n8n workflow asana, tự động hoàn tất công việc]
---

# 🚀 **Tự Động Hoàn Tất & Sắp Lại Nhiệm Vụ Quá Hạn Asana - Giải Pháp Cho Các Sếp Bận Rộn**

### **Nỗi Đau Của Các Sếp Hiện Nay**
Các sếp thường phải mất **giờ đồng hồ** mỗi tuần để:
- **Lọc và sắp lại** nhiệm vụ quá hạn trên Asana.
- **Xóa bỏ** những nhiệm vụ đã hoàn tất nhưng vẫn còn dính lại trong danh sách.
- **Nhắc nhở** đồng nghiệp về nhiệm vụ quá hạn để tránh tình trạng "quên" và ảnh hưởng đến hiệu suất nhóm.

**Kết quả?** Công việc trở nên rối loạn, năng suất giảm, và các sếp phải mất thời gian quý giá để quản lý công việc thay vì tập trung vào chiến lược và phát triển doanh nghiệp.

---
### **🎯 Kết Quả Các Sếp Nhận Được**
Dùng workflow này, các sếp sẽ:
✅ **Tự động hóa hoàn tất** nhiệm vụ quá hạn (đặt ngày hoàn thành là ngày hôm nay).
✅ **Xóa bỏ** nhiệm vụ đã hoàn tất để giữ không gian làm việc sạch sẽ.
✅ **Tiết kiệm tối thiểu 10 giờ/Tháng** cho việc quản lý công việc thủ công.
✅ **Giảm stress** vì không còn lo quên nhiệm vụ quan trọng.
✅ **Cập nhật tự động** mỗi ngày (hoặc theo lịch trình tùy chọn).

---
### **🔧 Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
🔹 **Tài khoản Asana** với quyền **Admin** (để có thể cập nhật và xóa nhiệm vụ).
🔹 **API Key Asana** (cài đặt trong n8n dưới **Credentials**).
🔹 **Tên Workspace** và **Tên Người Giao Nhiệm (Assignee)** trong Asana (để lọc nhiệm vụ của người đó).
🔹 **Thời gian chạy tự động** (ví dụ: hàng ngày lúc 7h sáng).

---
### **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Mở **n8n Workflow Editor**.
2. Nhấn **Import** và chọn file JSON (hoặc **Paste JSON**).
3. **Kích hoạt** workflow sau khi import xong.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này hoạt động theo **7 node chính**, các sếp cần chú ý cấu hình như sau:

##### **🔹 Node 1: Everyday at 7am (ScheduleTrigger)**
- **Chỉnh thời gian chạy** theo nhu cầu (ví dụ: hàng ngày lúc 7h sáng).
- **Lưu ý:** Nếu muốn chạy theo lịch khác (ví dụ: hàng tuần), chỉnh ở đây.

##### **🔹 Node 2 & 3: Get user tasks & Get task infos (Asana)**
- **Thêm Credentials Asana**:
  - Vào **Credentials** → **Add New** → Chọn **Asana API**.
  - Nhập **Personal Access Token** từ Asana (tạo tại [Asana Developer](https://developers.asana.com/)).
- **Chọn Workspace Name & Assignee Name**:
  - Trong node **Get user tasks**, chọn **Workspace Name** (tên Workspace Asana của các sếp).
  - Trong node **Get task infos**, chọn **Assignee Name** (tên người giao nhiệm vụ, ví dụ: tên của mình hoặc nhóm).

##### **🔹 Node 4: Task is open? (If)**
- **Lọc nhiệm vụ chưa hoàn tất** (status = "open").
- **Lưu ý:** Nếu muốn thêm điều kiện khác (ví dụ: chỉ lọc nhiệm vụ có ngày hoàn thành > 30 ngày), chỉnh ở đây.

##### **🔹 Node 5: Due date in the past? (If)**
- **Kiểm tra ngày hoàn thành đã quá hạn**.
- **Lưu ý:** Nếu muốn thay đổi logic (ví dụ: chỉ xử lý nhiệm vụ quá hạn > 7 ngày), chỉnh ở đây.

##### **🔹 Node 6: Set due date to Today (Asana)**
- **Cập nhật ngày hoàn thành** thành ngày hôm nay cho nhiệm vụ quá hạn.
- **Lưu ý:** Nếu muốn đặt ngày hoàn thành là ngày khác (ví dụ: ngày mai), chỉnh ở đây.

##### **🔹 Node 7: Clean up task (Asana)**
- **Xóa nhiệm vụ đã hoàn tất** (nếu status = "completed").
- **Lưu ý:** **Không xóa nhiệm vụ quan trọng!** Các sếp nên **test run** trước khi bật workflow.

#### **3. Kích Hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Chạy workflow với **1-2 nhiệm vụ mẫu** để kiểm tra logic.
   - Kiểm tra xem:
     - Nhiệm vụ quá hạn có được cập nhật ngày hoàn thành không?
     - Nhiệm vụ đã hoàn tất có được xóa không?
2. **Bật Active workflow**:
   - Sau khi test thành công, **bật workflow** để chạy tự động hàng ngày.

---
### **✍️ Mẹo & Gợi Ý Nâng Cao**
Các sếp có thể **tối ưu hóa workflow** thêm bằng cách:
🔸 **Gửi thông báo Slack/Telegram** khi có nhiệm vụ quá hạn:
   - Thêm node **Slack Webhook** hoặc **Telegram Bot** sau node **Due date in the past?**.
   - Gửi thông báo tự động cho đồng nghiệp.

🔸 **Lưu log hoạt động** để theo dõi:
   - Thêm node **StickyNote** (hoặc **Google Sheets**) để ghi lại lịch sử cập nhật nhiệm vụ.

🔸 **Chỉnh lịch chạy linh hoạt**:
   - Nếu các sếp muốn chạy workflow **chỉ vào thứ 2-5** (tránh cuối tuần), chỉnh ở **ScheduleTrigger**.

🔸 **Kết hợp với Google Calendar**:
   - Thêm node **Google Calendar** để tự động tạo sự kiện cho nhiệm vụ quá hạn.

---
### **📌 Kết Luận**
Workflow này **giúp các sếp tự động hóa hoàn tất và sắp lại nhiệm vụ quá hạn trên Asana**, tiết kiệm thời gian và giữ không gian làm việc sạch sẽ. **Không cần code, chỉ cần import và cấu hình vài bước đơn giản!**

**Hành động ngay:**
1. **Import workflow** từ [đây](https://n8n.io/workflows/2701).
2. **Cấu hình Asana API** và **lịch chạy**.
3. **Bật workflow** và **quên đi lo lắng về nhiệm vụ quá hạn!**

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

**Chúc các sếp thành công!** 🚀