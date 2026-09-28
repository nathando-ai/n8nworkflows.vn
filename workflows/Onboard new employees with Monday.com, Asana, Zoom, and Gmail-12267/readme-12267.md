---
title: "🚀 Tự Động Hóa Quá Trình Nhập Nhân Viên với Monday.com, Asana, Zoom & Gmail - Giảm 90% Công Việc Thủ Công"
description: "Workflow này tự động hóa toàn bộ quá trình onboard mới nhân viên: tạo task Asana, gửi email chào mừng, lịch Zoom giới thiệu và cập nhật trạng thái trên Monday.com - chỉ cần chạy 1 lần/ngày. Giúp HR tiết kiệm 10+ giờ/tháng và tránh sai sót nhân sự."
slug: "tieu-dong-hoa-qua-trinh-nhap-nhan-vien-monday-asana-zoom-gmail"
tags: [n8n, automation, hr, monday-com, asana, zoom, gmail, no-code, self-hosted]
keywords: [tự động hóa nhân sự n8n, onboard mới nhân viên, monday.com automation, asana task tự động, zoom meeting tự động, email chào mừng tự động]
---

# 🚀 **Tự Động Hóa Quá Trình Nhập Nhân Viên với Monday.com, Asana, Zoom & Gmail**

## **Nỗi Đau Của Các Sếp HR**
Mỗi khi có nhân viên mới gia nhập, các sếp phải làm thủ công **3-5 bước** sau:
1. **Tạo task onboard** trên Asana với checklist chi tiết (thường quên một số bước).
2. **Gửi email chào mừng** với thông tin cá nhân và tài liệu cần thiết (rủi ro sai email hoặc nội dung).
3. **Lịch Zoom giới thiệu** với bộ phận (thường phải nhắc nhở nhiều lần).
4. **Cập nhật trạng thái** trên Monday.com để tránh xử lý lại (dễ bị quên).

**Kết quả?** Tốn **10-15 phút/người**, dễ xảy ra sai sót, và **không hoạt động 24/7** như cần thiết.

---
### **🎯 Giải Pháp: Workflow Tự Động Hóa 100% Không Code**
Workflow này **chạy tự động hàng ngày** (hoặc theo lịch bạn thiết lập) để:
✅ **Lấy danh sách nhân viên mới** từ Monday.com (trạng thái "Joined").
✅ **Tạo task onboard** trên Asana với checklist chuẩn hóa.
✅ **Gửi email chào mừng** cá nhân hóa từ Gmail.
✅ **Lịch Zoom giới thiệu** 30 phút với bộ phận.
✅ **Cập nhật trạng thái** thành "Processed" để tránh xử lý lại.
✅ **Tự động cập nhật link Zoom** vào Monday.com.

**Kết quả?** **Tiết kiệm 10+ giờ/tháng**, giảm sai sót, và **hoạt động liên tục** mà không cần can thiệp thủ công.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo tính riêng tư và hiệu suất cao.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

## **🎯 Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ/tháng** cho bộ phận HR.
- **Giảm sai sót** (không quên task, email sai người, hoặc lịch Zoom).
- **Cá nhân hóa** email và task cho từng nhân viên mới.
- **Hoạt động liên tục** (không phụ thuộc vào giờ làm việc của HR).
- **Dữ liệu đồng bộ** giữa Monday.com, Asana, Zoom và Gmail.
:::

---

## **🔧 Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
✔ **Tài khoản và API Key:**
   - **Monday.com:** Board ID, Column IDs (trạng thái "Joined" và "Processed").
   - **Asana:** OAuth2 API (tạo task onboard).
   - **Zoom:** OAuth2 API (lịch Zoom).
   - **Gmail:** OAuth2 (gửi email chào mừng).
✔ **Thông tin cấu hình:**
   - **Asana:** Project ID và Assignee (người phụ trách onboard).
   - **Gmail:** Nội dung email mẫu (có thể tùy chỉnh).
   - **Zoom:** Thời gian mặc định (30 phút) và chủ đề cuộc họp.

---

## **🚀 Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
#### **Cách 1: Từ file JSON**
1. Tải workflow từ [n8n.io/workflows/12267](https://n8n.io/workflows/12267) (chọn "Export as JSON").
2. Trên n8n Editor, nhấn **"Import"** và chọn file JSON tải xuống.
3. Chọn **"Create new workflow"** và nhấn **"Import"**.

#### **Cách 2: Copy/Paste JSON**
1. Copy toàn bộ JSON từ [n8n.io/workflows/12267](https://n8n.io/workflows/12267).
2. Trên n8n Editor, nhấn **"Import"** → **"Paste JSON"** và dán nội dung.
3. Chọn **"Create new workflow"** và nhấn **"Import"**.

---

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow gồm **8 node chính**, các sếp cần cấu hình kỹ lưỡng:

#### **🔹 Node 1: "Fetch joined employees from Monday.com"**
- **Cấu hình:**
  - **Board ID:** ID của board nhân sự trên Monday.com.
  - **Column Name:** Cột chứa trạng thái "Joined" (ví dụ: "Status").
  - **Filter:** Chỉ lấy những nhân viên **không** có trạng thái "Processed".

#### **🔹 Node 2: "Filter – Skip Already Processed Employees"**
- **Lưu ý:** Node này **bắt buộc** để tránh xử lý lại nhân viên đã onboard.
- **Cấu hình:** Đảm bảo cột "Processed" được kiểm tra đúng.

#### **🔹 Node 3: "Check for newly joined employees" (Schedule Trigger)**
- **Cấu hình:**
  - **Lịch chạy:** Thiết lập chạy **hàng ngày** (ví dụ: 8h sáng) hoặc theo lịch cụ thể.
  - **Test run:** Nhấn **"Run"** để kiểm tra workflow trước khi kích hoạt.

#### **🔹 Node 4: "Create onboarding task in Asana"**
- **Cấu hình:**
  - **Project ID:** ID của project onboard trên Asana.
  - **Assignee:** Người phụ trách (ví dụ: "HR Team").
  - **Checklist:** Thêm các bước cần thiết (ví dụ: "Setup email", "Join Zoom intro").

#### **🔹 Node 5: "Schedule Zoom intro meeting"**
- **Cấu hình:**
  - **Thời gian:** 30 phút (có thể điều chỉnh).
  - **Chủ đề:** "Onboarding Intro - [Tên nhân viên]".
  - **Tham gia:** Thêm link Zoom vào email chào mừng.

#### **🔹 Node 6: "Send welcome email"**
- **Cấu hình:**
  - **Nội dung email:** Tùy chỉnh với thông tin cá nhân (tên, ngày nhập việc, link Zoom).
  - **Đính kèm:** Có thể thêm file PDF hướng dẫn onboard.

#### **🔹 Node 7: "Update Employee Zoom Link"**
- **Cấu hình:**
  - **Column Name:** Cột trên Monday.com để lưu link Zoom (ví dụ: "Zoom Link").
  - **Dynamic Value:** Sử dụng `$node["Schedule Zoom intro meeting"].json["join_url"]` để lấy link từ Zoom.

#### **🔹 Node 8: "Mark employee as processed"**
- **Cấu hình:**
  - **Column Name:** Cột "Processed" trên Monday.com.
  - **Giá trị:** Đặt thành **"Yes"** hoặc **"Completed"**.

---

### **3. Kích hoạt ⚡️**
1. **Test run:** Nhấn **"Run"** với dữ liệu mẫu để kiểm tra workflow.
2. **Kích hoạt:** Đặt **"Active"** thành **"On"** và chọn **"Run on schedule"**.
3. **Monitor:** Theo dõi log trong **"Execution"** để đảm bảo không có lỗi.

---

## **✍️ Mẹo & gợi ý nâng cao**
### **1. Tự động gửi báo cáo định kỳ**
- **Thêm node "Schedule Trigger"** mới để chạy **tối hằng tuần** và gửi **báo cáo tổng hợp** về số lượng nhân viên onboard thành công qua **Slack/Email**.

### **2. Kết hợp với Telegram/Slack**
- **Thêm node "Webhook"** để gửi thông báo khi có nhân viên mới được onboard qua **Telegram/Slack**.

### **3. Lưu log hoạt động**
- **Thêm node "StickyNote"** để lưu lại **log hoạt động** (ví dụ: "Nhân viên [Tên] đã được onboard thành công vào [Ngày]").

### **4. Tùy chỉnh email động**
- **Sử dụng node "Function"** để động thái hóa email với **thông tin cá nhân** (ví dụ: tên, vị trí, ngày nhập việc).

### **5. Xử lý lỗi tự động**
- **Thêm node "If"** để kiểm tra lỗi (ví dụ: nếu Zoom không tạo được cuộc họp, gửi email cảnh báo).

---

## **📌 Kết luận**
Workflow này **giải phóng HR khỏi công việc thủ công lặp lại**, giúp **tiết kiệm thời gian, giảm sai sót** và **cải thiện trải nghiệm onboard** cho nhân viên mới. **Chỉ cần cài đặt 1 lần**, workflow sẽ **hoạt động tự động hàng ngày** mà không cần can thiệp.

**🚀 Hành động ngay:**
1. **Cài đặt n8n trên VPS** (để tự động hóa 24/7).
2. **Import workflow** và cấu hình theo hướng dẫn.
3. **Kích hoạt và theo dõi kết quả!**

**Nếu có vấn đề, hãy để lại comment bên dưới hoặc liên hệ với chúng tôi để hỗ trợ!** 💡