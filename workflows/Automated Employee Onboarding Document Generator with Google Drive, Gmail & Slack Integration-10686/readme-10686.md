---
title: "🚀 Tự Động Hóa Gói Tài Liệu Nhập Công Ty Cho Nhân Viên - Khóa Nhanh Với Google Drive, Gmail & Slack"
description: "Giải pháp tự động hóa hoàn toàn không cần code để tạo gói tài liệu nhập công ty cá nhân hóa cho nhân viên mới, bao gồm thư chào mừng, hướng dẫn lợi ích, cài đặt IT và biểu mẫu pháp lý. Tiết kiệm thời gian cho bộ phận HR lên đến 80% và đảm bảo tính nhất quán trong quy trình nhập công ty."
slug: "tieu-dong-hoa-goi-ta-lieu-nhap-cong-ty-voi-n8n"
tags: [n8n, automation, hr, google-drive, gmail, slack, no-code, workflow, pdf-generator]
keywords: [tự động hóa nhật ký nhập công ty, tạo tài liệu nhân viên mới, n8n workflow hr, google drive automation, gmail automation, slack notification]
---

# 🚀 **Tự Động Hóa Gói Tài Liệu Nhập Công Ty Cho Nhân Viên - Khóa Nhanh Với Google Drive, Gmail & Slack**

### **Giải pháp cho nỗi đau của bộ phận HR:**
Hàng tuần, bộ phận HR phải mất **từ 5-10 giờ** để thủ công tạo và gửi gói tài liệu nhập công ty cho nhân viên mới. Các gói tài liệu này bao gồm:
- **Thư chào mừng** với thông tin ngày đầu tiên và liên lạc với quản lý.
- **Hướng dẫn lợi ích** (bảo hiểm, ưu đãi, thời hạn đăng ký).
- **Hướng dẫn cài đặt IT** (thiết bị, quyền truy cập, phần mềm cần thiết).
- **Biểu mẫu pháp lý** (thông tin khẩn cấp, ủy quyền chuyển khoản).

**Kết quả?** Nhân viên mới nhận được tài liệu **không nhất quán**, **chậm trễ**, và **không cá nhân hóa**, trong khi bộ phận HR phải **lặp lại công việc** hàng tuần. **Workflow này giải quyết tất cả những vấn đề đó!**

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS riêng. Với chi phí thấp nhưng hiệu suất cao, các sếp có thể **tự động hóa toàn bộ quy trình HR** mà không lo downtime.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (đủ sức mạnh cho workflow HR)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian:** **80% công việc thủ công** được tự động hóa, cho phép HR tập trung vào **quản lý nhân sự chất lượng cao**.
- **Tài liệu cá nhân hóa:** Mỗi nhân viên mới nhận được **gói tài liệu riêng**, với thông tin chính xác về vị trí, lợi ích và thiết bị IT.
- **Tính nhất quán:** **Không còn sai sót** trong thông tin (ngày đầu tiên, quản lý, lợi ích).
- **Quản lý dễ dàng:** Tất cả tài liệu được **lưu trữ trên Google Drive**, dễ dàng theo dõi và tra cứu.
- **Thông báo tự động:** **Slack & Gmail** giúp HR **biết ngay khi gói tài liệu đã được gửi** và **nhân viên đã nhận**.
- **Tuân thủ pháp lý:** **Biểu mẫu pháp lý** được tự động tạo và lưu trữ, giảm rủi ro vi phạm.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Google Drive** (để lưu trữ tài liệu PDF).
2. **Tài khoản Gmail** (để gửi gói tài liệu cho nhân viên).
3. **Webhook Slack** (để thông báo cho bộ phận HR khi gói tài liệu hoàn thành).
4. **API Key từ [htmlcsstoimage.com](https://htmlcsstoimage.com/)** (để chuyển đổi HTML thành PDF, **miễn phí cho 1-5¢/tài liệu**).
5. **Dữ liệu nhân viên mới** (cần có các trường: `firstName`, `lastName`, `email`, `jobTitle`, `department`, `startDate`).

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Cách 1:** Tải file JSON từ [n8n.io/workflows/10686](https://n8n.io/workflows/10686) và import vào **n8n Editor**.
- **Cách 2:** Copy toàn bộ JSON từ [đây](https://github.com/n8n-io/workflows/blob/main/workflows/10686.json) và **paste** vào **Import Workflow** trong n8n.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này gồm **15 node**, nhưng có **3 node quan trọng nhất** cần cấu hình cẩn thận:

##### **A. Node Webhook Trigger2 (n8n-nodes-base.webhook)**
- **Cấu hình:**
  - **Path:** `onboard-employee` (không đổi).
  - **HTTP Method:** `POST`.
  - **Credentials:** Chọn **New Credential** (tên tùy ý, ví dụ: `HR_Webhook`).
  - **Lưu ý:** Nếu kết nối từ **HRIS (BambooHR/Workday)** hoặc **ATS**, cần **cấu hình webhook trong hệ thống đó** để gửi dữ liệu nhân viên mới đến URL webhook này.

##### **B. Node HTML to PDF (n8n-nodes-htmlcsstopdf.htmlcsstopdf)**
- **Cấu hình:**
  - **API Key:** Nhập **API Key** từ [htmlcsstoimage.com](https://htmlcsstoimage.com/) (miễn phí cho 1-5¢/tài liệu).
  - **Lưu ý:** Nếu không có API Key, **tài liệu PDF sẽ không được tạo**.

##### **C. Node Google Drive (n8n-nodes-base.googleDrive)**
- **Cấu hình:**
  - **Credentials:** Chọn **New Credential** (tên tùy ý, ví dụ: `Google_Drive_HR`).
  - **Folder ID:** Tạo **một thư mục mới** trong Google Drive (ví dụ: `HR - Employee Onboarding`) và **copy Folder ID** từ URL.
  - **Lưu ý:** Nếu không cấu hình đúng, **tài liệu sẽ không được lưu** vào Google Drive.

##### **D. Node Gmail (n8n-nodes-base.gmail)**
- **Cấu hình:**
  - **Credentials:** Chọn **New Credential** (tên tùy ý, ví dụ: `Gmail_HR`).
  - **From Email:** Điền **email chính thức** của bộ phận HR (ví dụ: `hr@congty.com`).
  - **Lưu ý:** Nếu email không được **xác thực 2FA**, **gói tài liệu sẽ không được gửi**.

##### **E. Node Slack (n8n-nodes-base.httpRequest)**
- **Cấu hình:**
  - **URL:** Nhập **URL webhook Slack** (tạo từ **Apps > Create App > Incoming Webhooks** trong Slack).
  - **Headers:**
    - `Content-Type: application/json`
  - **Body:**
    ```json
    {
      "text": "📄 Gói tài liệu nhập công ty cho {{ $node["Validate & Enrich Data2"].json["firstName"] }} {{ $node["Validate & Enrich Data2"].json["lastName"] }} đã được gửi thành công!"
    }
    ```
  - **Lưu ý:** Nếu không cấu hình đúng, **Slack sẽ không nhận được thông báo**.

##### **F. Node Code (Validate & Enrich Data2)**
- **Cấu hình:**
  - Mở node này và **chỉnh sửa dữ liệu cá nhân hóa** (ví dụ: tên công ty, logo, thông tin lợi ích, thiết bị IT).
  - **Lưu ý:** Nếu không chỉnh sửa, **tài liệu sẽ không phản ánh thông tin chính xác** của công ty.

---

#### **3. Kích hoạt ⚡️**
1. **Test Run với dữ liệu mẫu:**
   - Gửi **1 request POST** đến webhook với dữ liệu mẫu:
     ```json
     {
       "firstName": "John",
       "lastName": "Doe",
       "email": "john.doe@congty.com",
       "jobTitle": "Developer",
       "department": "Tech",
       "startDate": "2024-07-15"
     }
     ```
   - Kiểm tra **các node** có chạy không lỗi hay không.

2. **Bật Active workflow:**
   - Sau khi test thành công, **bật Active** workflow.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Kết hợp với CRM (HubSpot/Zoho):**
   - Nếu công ty sử dụng **HubSpot/Zoho CRM**, có thể **tích hợp thêm node CRM** để cập nhật trạng thái nhập công ty tự động.

2. **Lưu log vào Google Sheets:**
   - Thêm **node Google Sheets** để **ghi lại lịch sử gửi tài liệu**, giúp theo dõi và báo cáo cho lãnh đạo.

3. **Gửi báo cáo định kỳ cho lãnh đạo:**
   - Sử dụng **node Gmail** để gửi **báo cáo tuần/Tháng** về số lượng nhân viên mới nhập công ty và tình trạng hoàn thành.

4. **Tự động gửi reminder cho nhân viên:**
   - Thêm **node Gmail** để gửi **email nhắc nhở** cho nhân viên về **ngày đầu tiên** hoặc **hạn cuối đăng ký lợi ích**.

5. **Cá nhân hóa thêm:**
   - Trong node **Generate Welcome Letter2**, có thể thêm **thông tin cá nhân** như:
     - **Quản lý trực tiếp** của nhân viên.
     - **Lịch họp giới thiệu** với team.
     - **Link tài liệu nội bộ** (ví dụ: Manual, Policy).

---

### 📌 **Kết luận**
Workflow này **giải phóng bộ phận HR** khỏi công việc thủ công, **tăng tính nhất quán** và **cải thiện trải nghiệm nhập công ty** cho nhân viên mới. **Chỉ cần 1-2 giờ setup**, công ty đã có thể **tự động hóa toàn bộ quy trình nhập công ty** mà không cần viết một dòng code!

**Hành động ngay:**
1. **Import workflow** và cấu hình theo hướng dẫn.
2. **Test với dữ liệu mẫu** trước khi áp dụng cho nhân viên thực.
3. **Bật Active** và **nhận gói tài liệu tự động hóa**!

**Cần hỗ trợ?** Đăng ký **khóa học tự động hóa HR với n8n** tại [n8n.io/learn](https://n8n.io/learn) để học cách **tối ưu hóa workflow** của mình!

---