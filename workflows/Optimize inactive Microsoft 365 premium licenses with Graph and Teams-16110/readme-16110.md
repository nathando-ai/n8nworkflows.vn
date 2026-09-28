---
title: "💰 Tự Động Hóa Giảm Giá Gói Premium Microsoft 365 Cho Người Dùng Inactive - Giảm Chi Phí Hàng Tháng"
description: "Workflow tự động hóa 100% không code để phát hiện và giảm cấp phép Microsoft 365 premium cho người dùng inactive, tiết kiệm hàng trăm triệu đồng/năm cho doanh nghiệp. Kết hợp Microsoft Graph API và Microsoft Teams để báo cáo tự động."
slug: "tieu-dong-hoa-giam-gia-microsoft-365-premium"
tags: [n8n, automation, microsoft-365, crm, microsoft-graph-api, microsoft-teams]
keywords: [tự động hóa microsoft 365, giảm chi phí m365, downgrade license premium, n8n workflow microsoft, tự động hóa quản lý gói phép]
---

# 🚀 **Tự Động Hóa Giảm Giá Gói Premium Microsoft 365 Cho Người Dùng Inactive**

### **Giải pháp tiết kiệm hàng trăm triệu đồng/năm cho doanh nghiệp**
Bạn đã bao giờ lo lắng về chi phí cao của **Microsoft 365 Premium** khi nhiều người dùng không sử dụng đầy đủ quyền lợi? Hoặc phải mất thời gian thủ công để kiểm tra và giảm cấp phép cho những tài khoản inactive? **Workflow này tự động hóa toàn bộ quy trình** bằng cách:
✅ **Phát hiện người dùng inactive** (không sử dụng trong 30+ ngày) đang giữ gói Premium.
✅ **Lọc bỏ ngoại lệ** (nhóm người dùng đặc quyền, mới gia nhập).
✅ **Giảm cấp phép tự động** (hoặc mô phỏng với chế độ dry-run).
✅ **Báo cáo kết quả** trên Microsoft Teams cho IT Manager.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo tính bảo mật và không phụ thuộc vào cloud.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm chi phí**: Giảm hàng chục triệu đồng/năm bằng cách downgrade gói Premium cho người dùng inactive.
- **Tự động hóa hoàn toàn**: Không cần can thiệp thủ công, chạy hàng tháng tự động lúc 6h sáng.
- **Báo cáo minh bạch**: Microsoft Teams tự động thông báo kết quả cho IT Manager.
- **An toàn và kiểm soát**: Chế độ **dry-run** để thử nghiệm trước khi thực hiện downgrade thật.
- **Tuân thủ chính sách**: Lọc bỏ ngoại lệ (nhóm đặc quyền, mới gia nhập) theo quy định nội bộ.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Microsoft 365 Admin** với quyền:
   - Đọc danh sách **SKUs** (gói phép) đã đăng ký.
   - Đọc danh sách **người dùng** và **nhóm ngoại lệ**.
   - **Cập nhật gói phép** (nếu không chạy chế độ dry-run).
2. **Microsoft Graph API OAuth Credentials**:
   - **Permissions** cần thiết:
     - `User.Read.All` (đọc người dùng)
     - `UserLicenseDetails.Read.All` (đọc gói phép)
     - `UserLicenseDetails.Update.All` (cập nhật gói phép - **không cần** nếu dry-run)
3. **Microsoft Teams Webhook**:
   - **Channel** để nhận thông báo:
     - Khi **không cần downgrade**.
     - **Lỗi downgrade** (nếu có).
     - **Báo cáo tổng kết** cuối workflow.
4. **Cấu hình workflow** (điền trong node **"Set Configuration Parameters"**):
   - `premiumSkuPartNumbers`: Danh sách mã gói Premium cần downgrade (ví dụ: `["E3", "E5"]`).
   - `baselineSkuId`: Mã gói cơ bản (ví dụ: `["F1"]`).
   - `inactivityThresholdDays`: Ngưỡng inactive (ví dụ: `90` ngày).
   - `newHireThresholdDays`: Thời gian bảo vệ cho người dùng mới (ví dụ: `30` ngày).
   - `exemptionGroupId`: ID nhóm ngoại lệ (nếu có).
   - `dryRun`: `true` (để thử nghiệm) hoặc `false` (thực hiện downgrade thật).

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/16110](https://n8n.io/workflows/16110) hoặc copy toàn bộ JSON từ canvas.
- **Trên n8n Editor**:
  - Nhấn **"Import"** → Dán JSON hoặc tải file `.json`.
  - Chọn **"Import"** để tạo workflow mới.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
##### **A. Cấu hình Microsoft Graph API**
- **Node "Fetch Subscribed SKUs"** và **"Retrieve Exemption Group Members"**:
  - Điền **Client ID** và **Client Secret** từ **Azure AD App Registration**.
  - Chọn **scope** phù hợp (xem yêu cầu trên).
  - **Test connection** để đảm bảo kết nối thành công.

##### **B. Cấu hình Microsoft Teams**
- **Node "Notify No Downgrades Required"**, **"Alert License Error"**, **"Deliver Summary to IT Manager"**:
  - Chọn **Microsoft Teams** như **credentials**.
  - Điền **Webhook URL** của channel tương ứng (tạo từ **Connectors** trong Teams).
  - **Customize message template** (ví dụ: thay đổi tiêu đề, nội dung báo cáo).

##### **C. Cấu hình tham số trong "Set Configuration Parameters"**
| Tham số | Giá trị gợi ý | Ghi chú |
|---------|--------------|---------|
| `premiumSkuPartNumbers` | `["E3", "E5"]` | Danh sách gói Premium cần downgrade |
| `baselineSkuId` | `["F1"]` | Gói cơ bản (ví dụ: F1) |
| `inactivityThresholdDays` | `90` | Người dùng inactive >90 ngày |
| `newHireThresholdDays` | `30` | Bảo vệ người dùng mới 30 ngày |
| `exemptionGroupId` | `""` (trống) | ID nhóm ngoại lệ (nếu có) |
| `dryRun` | `true` | Thử nghiệm trước khi downgrade thật |

##### **D. Cấu hình lịch chạy**
- **Node "Monthly Schedule Trigger at 6am"**:
  - Chọn **lịch chạy hàng tháng** vào **6h sáng** (thời gian UTC hoặc theo múi giờ của doanh nghiệp).
  - **Test schedule** để đảm bảo workflow chạy đúng thời gian.

#### **3. Kích hoạt ⚡️**
- **Test run** với chế độ **dry-run** (`dryRun: true`):
  - Chạy workflow và kiểm tra **Microsoft Teams** để xác nhận:
    - Danh sách người dùng inactive được lọc chính xác.
    - Báo cáo không có lỗi.
- **Bật Active workflow**:
  - Sau khi kiểm tra thành công, **bật chế độ Active**.
  - **Không quên** chuyển `dryRun: false` khi muốn downgrade thật.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Lưu log chi tiết**:
   - Thêm **node "code"** sau **"Log Downgrade Success"** để ghi log vào **Google Sheets** hoặc **Notion** để theo dõi lịch sử downgrade.
   - **Cú pháp gợi ý**:
     ```javascript
     // Node "code" sau "Log Downgrade Success"
     $input.all().forEach(item => {
       const logEntry = {
         timestamp: new Date().toISOString(),
         userEmail: item.json.userPrincipalName,
         oldSku: item.json.oldSku,
         newSku: item.json.newSku,
         status: "SUCCESS"
       };
       // Gửi log đến Google Sheets (ví dụ)
       return [{ json: { logEntry } }];
     });
     ```

2. **Kết hợp với Slack/Telegram**:
   - Thay thế **Microsoft Teams** bằng **Slack Webhook** hoặc **Telegram Bot** để báo cáo nhanh hơn.
   - **Node "microsoftTeams"** → Thay bằng **"httpRequest"** gửi đến API của Slack/Telegram.

3. **Tự động gửi báo cáo định kỳ**:
   - Sử dụng **node "scheduleTrigger"** để gửi **báo cáo hàng tuần** cho CEO/IT Manager.
   - **Ví dụ**: Chạy workflow thứ 2 hàng tuần và gửi báo cáo qua email (sử dụng **node "email"**).

4. **Cập nhật danh sách ngoại lệ tự động**:
   - Nếu nhóm ngoại lệ thay đổi thường xuyên, **tích hợp với Active Directory** hoặc **Google Sheets** để cập nhật danh sách tự động.

---

### 📌 **Kết luận**
Workflow này **giải quyết vấn đề chi phí cao của Microsoft 365 Premium** bằng cách tự động hóa quy trình downgrade cho người dùng inactive, **tiết kiệm hàng trăm triệu đồng/năm** mà không cần viết một dòng code. **Chỉ cần import, cấu hình và chạy** – toàn bộ quy trình được tự động hóa hoàn toàn!

👉 **Hành động ngay**:
1. **Import workflow** và cấu hình theo hướng dẫn.
2. **Test dry-run** trước khi downgrade thật.
3. **Bật chế độ Active** và **quên đi lo lắng về chi phí Premium**!

---
**Cần hỗ trợ?** Liên hệ với tác giả Mychel Garzon qua [AutomiQ](info@automiq.fi) để tùy chỉnh workflow phù hợp với chính sách của doanh nghiệp!