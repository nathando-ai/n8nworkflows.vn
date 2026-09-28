---
title: "🚀 Tự Động Hóa Thông Báo Nhóm Dự Án Redmine Trên Slack Khi Đồng Nghiệp Đăng Ký Nghỉ Phê Duyệt Trên Odoo"
description: "Workflow tự động hóa 24/7 cảnh báo đồng nghiệp và quản lý dự án trên Slack khi nhân viên có ngày nghỉ phê duyệt vào ngày mai, giúp tránh tình trạng "đồng nghiệp mất tích" bất ngờ và tối ưu hóa quản lý dự án. Giúp các sếp tiết kiệm thời gian lên tới 10 giờ/tuần và giảm thiểu rủi ro trong quản lý dự án."
slug: "tieu-dong-hoa-thong-bao-redmine-slack-odoo"
tags: [n8n, automation, project-management, redmine, odoo, slack, no-code, workflow]
keywords: [n8n workflow redmine slack, tự động hóa thông báo nghỉ phép, cảnh báo dự án redmine, tự động hóa quản lý dự án, n8n tự động hóa odoo, cảnh báo đồng nghiệp trên slack]
---

# 🚀 **Tự Động Hóa Thông Báo Nhóm Dự Án Redmine Trên Slack Khi Đồng Nghiệp Đăng Ký Nghỉ Phê Duyệt Trên Odoo**

## **🔥 Bạn đã từng gặp phải tình trạng nào sau đây?**
- **Đồng nghiệp "mất tích" bất ngờ** vì không thông báo nghỉ phép, khiến các dự án bị gián đoạn?
- **Phải nhắc nhở liên tục** về lịch nghỉ phép, mất thời gian và gây mất tập trung?
- **Quản lý dự án không kịp thời** vì không biết ai sẽ vắng mặt ngày mai?
- **Nhóm dự án bị "đóng băng"** khi không ai biết ai sẽ có mặt vào ngày hôm sau?

Workflow này **giải quyết tất cả những vấn đề trên** bằng cách tự động **cảnh báo đồng nghiệp và quản lý dự án trên Slack** khi nhân viên có ngày nghỉ phê duyệt vào ngày mai. **Không cần code, chỉ cần cấu hình và chạy 24/7!**

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động **ổn định và không ngắt kết nối**, các sếp nên cài đặt n8n trên **VPS riêng (Self-hosted)** thay vì dùng phiên bản miễn phí trên cloud.
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (Đảm bảo tốc độ cao, phù hợp cho workflow phức tạp)
:::

---

### **🎯 Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian lên tới 10 giờ/tuần** (không phải nhắc nhở thủ công về nghỉ phép).
✅ **Cảnh báo đồng nghiệp và quản lý dự án kịp thời** (tránh tình trạng "đồng nghiệp mất tích").
✅ **Tối ưu hóa quản lý dự án** (biết ai sẽ vắng mặt, phân công lại công việc một cách logic).
✅ **Giảm thiểu rủi ro** (không có dự án bị gián đoạn do nhân viên không báo trước).
✅ **Tự động hóa hoàn toàn** (chạy 24/7, không cần can thiệp thủ công).
✅ **Cá nhân hóa thông báo** (chỉ cảnh báo những người thực sự liên quan đến dự án).
:::

---

### **🔧 Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
- **Tài khoản Odoo 18** (API Key và URL API).
- **Tài khoản Redmine 6** (API Key và URL API).
- **Slack Bot Token** hoặc **Incoming Webhook URL** (để gửi thông báo).
- **Subflows** (được tạo riêng trong n8n, không cần active, chỉ cần gọi từ workflow chính).

---

## **🚀 Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
#### **Cách 1: Import từ file JSON**
1. **Tải workflow** từ [đây](https://n8n.io/workflows/12298) (hoặc copy JSON từ trang này).
2. **Mở n8n Editor** và chọn **"Import"** → **"From JSON"**.
3. **Dán JSON** và nhấn **"Import"**.

#### **Cách 2: Copy/Paste JSON**
1. **Mở n8n Editor** → **"Create New Workflow"**.
2. **Copy toàn bộ JSON** từ [trang n8n](https://n8n.io/workflows/12298) và **dán vào Editor**.
3. **Nhấn "Save"** (tên workflow: **"Notify Redmine Project Members in Slack"**).

---

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**

#### **🔹 Cấu hình API Keys & Credentials**
Workflow này sử dụng **3 loại API chính**:
1. **Odoo 18** (để lấy thông tin nghỉ phép).
2. **Redmine 6** (để lấy thông tin dự án và thành viên).
3. **Slack** (để gửi thông báo).

**Cách cấu hình:**
- **Tạo Credentials mới** trong n8n:
  - **Odoo**: `httpHeaderAuth` (điền `Authorization: Bearer <API_KEY>`).
  - **Redmine**: `httpHeaderAuth` (điền `Authorization: Basic <BASE64_ENCODED_CREDENTIALS>`).
  - **Slack**: `slackApi` (điền `Bot Token` hoặc `Incoming Webhook URL`).

#### **🔹 Cấu hình Subflows**
Workflow này sử dụng **2 Subflow** (không cần active, chỉ cần gọi từ workflow chính):
1. **"Get membership list of user in Redmine"** (lấy danh sách thành viên dự án).
2. **"Push message to member"** (gửi thông báo đến Slack).

**Cách tạo Subflow:**
1. **Tạo workflow mới** trong n8n.
2. **Copy các node** từ Subflow trong workflow chính và **dán vào workflow mới**.
3. **Không active Subflow**, chỉ cần gọi từ workflow chính.

#### **🔹 Cấu hình Schedule Trigger**
Workflow **chạy tự động hàng ngày lúc 17:15** (5:15 PM).
- **Không cần chỉnh gì** nếu import từ file JSON.
- **Nếu tạo mới**, thêm **`Schedule Trigger`** và cấu hình:
  - **Cron Expression**: `0 15 17 * * *` (lúc 17:15 hàng ngày).

#### **🔹 Cấu hình Node Quản Lý Dữ liệu**
Các node quan trọng cần **điền tham số chính xác**:
| **Node** | **Tham số cần điền** | **Ghi chú** |
|----------|----------------------|------------|
| **Step4: Get all user in Redmine6** | `URL API Redmine` | Ví dụ: `https://your-redmine.com/api/v3/users.json` |
| **Step5: Get a list of closed projects** | `URL API Redmine` | Ví dụ: `https://your-redmine.com/api/v3/projects.json` |
| **Step7: Get the list of members' leave records for tomorrow** | `URL API Odoo` | Ví dụ: `https://your-odoo.com/jsonrpc` |
| **Step11: Get leave record information** | `Domain: hr_leave` | Lọc theo ngày mai và trạng thái "approved" |
| **Step13: Get employee information in Odoo 18** | `Domain: hr_employee` | Lấy thông tin nhân viên |
| **Step15: Get information for this employee's manager** | `Domain: hr_employee` | Lấy thông tin quản lý |

#### **🔹 Cấu hình Node Slack**
- **Node `Step6: Get many users`** (lấy danh sách người dùng Slack).
- **Node `Step5.1/5.2: Send a message to the project team members`** (gửi thông báo).
  - **Tham số cần điền**:
    - `channel`: `#dieu-an` (hoặc channel cụ thể).
    - `text`: Thông điệp tự động (có thể chỉnh sửa trong **`Step28.1/28.2: Prepare information`**).

---

### **3. Kích hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Chạy workflow và kiểm tra **Slack** xem có nhận được thông báo không.
   - Nếu có lỗi, kiểm tra **Logs** trong n8n Editor.
2. **Bật Active**:
   - Chọn **"Active"** ở góc trên bên phải.

---

## **✍️ Mẹo & gợi ý nâng cao**

### **🔹 Tăng tính cá nhân hóa thông báo**
- **Chỉ cảnh báo những người thực sự liên quan** đến dự án (không phải toàn bộ nhóm).
- **Thêm thông tin chi tiết** như:
  - **Ngày nghỉ**: `Từ ngày 10/10 đến 15/10`.
  - **Lý do nghỉ**: `Đi du lịch`.
  - **Dự án liên quan**: `Dự án ABC, Dự án XYZ`.

### **🔹 Kết hợp với Google Calendar/Outlook**
- **Tự động đồng bộ lịch nghỉ phép** vào Google Calendar/Outlook.
- **Cách làm**:
  1. Sử dụng **node `Google Calendar`** trong n8n.
  2. **Tạo event mới** khi có ngày nghỉ phê duyệt.

### **🔹 Log thông báo để theo dõi**
- **Lưu lịch sử thông báo** vào **Google Sheets** hoặc **Database**.
- **Cách làm**:
  1. Thêm **node `Google Sheets`** sau khi gửi thông báo.
  2. **Ghi lại**:
    - Ngày giờ cảnh báo.
    - Tên nhân viên nghỉ.
    - Dự án liên quan.
    - Người nhận thông báo.

### **🔹 Báo cáo định kỳ cho quản lý**
- **Tạo báo cáo hàng tuần** về số lượng ngày nghỉ phê duyệt.
- **Cách làm**:
  1. Sử dụng **node `Schedule Trigger`** chạy hàng tuần.
  2. **Tính toán thống kê** và gửi **báo cáo PDF/Excel** qua email.

### **🔹 Chỉ cảnh báo cho vai trò quan trọng**
- **Chỉ gửi thông báo** cho:
  - **Quản lý dự án**.
  - **Nhóm kỹ thuật liên quan**.
  - **Những người có vai trò "Owner"** trên dự án.
- **Cách làm**:
  - Thêm **node `Filter`** trước khi gửi thông báo.
  - **Lọc theo role** (ví dụ: `role = "manager"`).

---

## **📌 Kết luận**

Workflow này **giải quyết triệt để vấn đề "đồng nghiệp mất tích"** bằng cách **tự động hóa cảnh báo nghỉ phép** trên Slack, giúp các sếp:
✔ **Tiết kiệm thời gian** (không phải nhắc nhở thủ công).
✔ **Quản lý dự án hiệu quả** (biết ai sẽ vắng mặt).
✔ **Tăng tính chuyên nghiệp** (cảnh báo kịp thời, không bị "bất ngờ").

**🚀 Hãy áp dụng ngay workflow này và trải nghiệm sự khác biệt!**
Nếu cần **cấu hình chi tiết hơn** hoặc **tùy chỉnh thêm**, các sếp có thể liên hệ với **BHSoft** qua:
🔗 [Website BHSoft](https://bachasoftware.com/bhsoft-contacts)
🔗 [LinkedIn BHSoft](https://www.linkedin.com/company/bac-ha-software/posts/?feedView=all)

---
**💡 Lưu ý cuối cùng:**
- **Không cần code**, chỉ cần cấu hình.
- **Chạy 24/7**, không ngắt kết nối.
- **Tối ưu hóa quản lý dự án**, giảm thiểu rủi ro.

**Bắt đầu tự động hóa ngay hôm nay!** 🚀