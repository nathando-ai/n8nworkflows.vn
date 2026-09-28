---
title: "🔍 **Tự Động Tìm Kiếm & Cập Nhật LinkedIn Profile Cho Tất Cả Người Dùng Trên Google Sheets – Không Cần Code!**"
description: "Workflow tự động hóa tìm kiếm và cập nhật liên kết LinkedIn cho danh sách người dùng từ Google Sheets, tiết kiệm thời gian lên đến 80% cho bộ phận Sales, HR và Marketing. Sử dụng AI Airtop và Google Sheets để tra cứu chính xác và tự động hóa quy trình."
slug: "tu-dong-tim-kiem-linkedin-profile-google-sheets"
tags: [n8n, automation, sales, hr, marketing, ai, google-sheets, airtop, no-code]
keywords: [tự động hóa linkedin profile, tìm kiếm linkedin tự động, google sheets automation, airtop ai, n8n workflow linkedin, tự động hóa sales hr]
---

# 🚀 **Tự Động Tìm Kiếm LinkedIn Profile Cho Tất Cả Người Dùng Trên Google Sheets**

### **Giải Phóng Thời Gian Cho Bộ Phận Sales, HR & Marketing**
Bạn có bao giờ phải mất **giờ đồng hồ** để tra cứu LinkedIn profile cho hàng trăm người dùng trong danh sách? Hay phải **copy-paste** liên tục giữa Google Sheets và LinkedIn để cập nhật thông tin? Với **workflow này**, các sếp có thể **tự động hóa toàn bộ quy trình** chỉ trong vài phút, tiết kiệm thời gian lên đến **80%** và đảm bảo **độ chính xác cao** nhờ AI Airtop.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS riêng.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** – giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian**: Tự động tra cứu LinkedIn profile cho **tất cả người dùng** trong Google Sheets **không cần làm thủ công**.
✅ **Độ chính xác cao**: AI Airtop phân tích kết quả Google Search và **trích xuất liên kết LinkedIn chính xác** (nếu có).
✅ **Cập nhật tự động**: Thông tin được **ghi đè trực tiếp vào Google Sheets**, không cần can thiệp.
✅ **Hoạt động liên tục**: Chạy **24/7** trên VPS, không phụ thuộc vào thời gian làm việc.
✅ **Dễ dàng mở rộng**: Thêm người dùng mới vào Google Sheets, workflow **tự động xử lý** mà không cần cấu hình lại.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Google Sheets** (để lưu danh sách người dùng và kết quả).
2. **API Key Airtop** (để sử dụng node `airtop`).
   - **Lấy API Key Airtop**:
     - Đăng ký tại [Airtop AI](https://www.airtop.ai/) và tạo **API Key** trong tài khoản.
     - Thêm **credentials** trong n8n với tên `airtopApi` và gán API Key.
3. **Credentials OAuth2 cho Google Sheets** (để đọc và cập nhật bảng tính).
   - Cấu hình trong n8n với tên `googleSheetsOAuth2Api`.

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n.io/workflows/3477](https://n8n.io/workflows/3477) và import vào n8n Editor.
- **Cách 2**: Copy toàn bộ JSON từ [đây](https://n8n.io/workflows/3477) và **paste** vào n8n Editor → **Import Workflow**.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflows này bao gồm **5 node chính**, các sếp cần chú ý cấu hình như sau:

##### **🔹 Node 1: Manual Trigger (Kích Hoạt Bằng Tay)**
- **Chức năng**: Khởi động workflow khi bạn **nhấn "Test workflow"**.
- **Lưu ý**: Không cần thay đổi gì, chỉ dùng để **test** trước khi bật **Active**.

##### **🔹 Node 2: Person Info (Đọc Dữ Liệu Từ Google Sheets)**
- **Tham số cần điền**:
  - **Google Sheets Credentials**: Chọn `googleSheetsOAuth2Api` (đã cấu hình trước).
  - **Sheet Name**: Tên của **bảng tính** chứa danh sách người dùng (ví dụ: `Danh sách Người Dùng`).
  - **Range**: Phần dữ liệu muốn đọc (ví dụ: `Sheet1!A2:B100` – cột A là **Tên**, cột B là **Email**).
  - **Output Format**: Chọn `JSON` để dữ liệu được truyền sang node tiếp theo.

##### **🔹 Node 3: Search Profile (Tra Cứu LinkedIn Với AI Airtop)**
- **Tham số cần điền**:
  - **Airtop Credentials**: Chọn `airtopApi` (API Key đã cấu hình).
  - **Prompt (đã cấu hình sẵn)**:
    ```plaintext
    =This is Google Search results. The first results should be the LinkedIn Page of {{ $json['Person Info'] }}.
    Return the LinkedIn URL and nothing else.
    If you cannot find the LinkedIn URL, return an empty string.
    A valid LinkedIn profile URL starts with "https://www.linkedin.com/in/".
    ```
  - **Lưu ý**:
    - **`{{ $json['Person Info'] }}`** sẽ tự động lấy **tên người dùng** từ Google Sheets.
    - AI sẽ **tìm kiếm Google** và trích xuất **liên kết LinkedIn** (nếu có).

##### **🔹 Node 4: Parse Response (Xử Lý Kết Quả Trả Về)**
- **Mã JavaScript (đã cấu hình sẵn)**:
  ```javascript
  // Lấy dữ liệu từ node trước
  const linkedinUrl = $input.all().linkedinUrl[0];

  // Nếu kết quả trống, trả về null
  if (!linkedinUrl || linkedinUrl.trim() === "") {
    return null;
  }

  // Trả về kết quả có định dạng
  return {
    linkedinUrl: linkedinUrl.trim()
  };
  ```
  - **Lưu ý**: Node này **lọc bỏ kết quả trống** và đảm bảo chỉ trả về **liên kết LinkedIn hợp lệ**.

##### **🔹 Node 5: Update Row (Cập Nhật Vào Google Sheets)**
- **Tham số cần điền**:
  - **Google Sheets Credentials**: Chọn `googleSheetsOAuth2Api`.
  - **Sheet Name**: Tên cùng bảng tính ở **Node 2**.
  - **Range**: Phần dữ liệu muốn cập nhật (ví dụ: `Sheet1!C2:C100` – cột C sẽ lưu **LinkedIn URL**).
  - **Operation**: Chọn `update` (ghi đè giá trị mới).
  - **Value**: Chọn `$json['linkedinUrl']` (liên kết LinkedIn từ node trước).

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Nhấn **"Test workflow"** để chạy với **dữ liệu mẫu**.
   - Kiểm tra kết quả ở **Node 5** (Google Sheets) có cập nhật không.
2. **Bật Active**:
   - Sau khi test thành công, chuyển **Active** sang **ON** để workflow chạy tự động.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tự Động Chạy Hàng Ngày**:
   - Sử dụng **n8n Cron Trigger** để chạy workflow **mỗi ngày** (ví dụ: 8h sáng) thay vì kích hoạt thủ công.
   - Cấu hình tại **Node 1** → Chọn **Cron Trigger** với biểu thức `0 8 * * *` (8h mỗi ngày).

2. **Gửi Báo Cáo Kết Quả Sang Slack/Email**:
   - Thêm **node Slack** hoặc **node Email** sau **Node 5** để **báo cáo kết quả** cho team.
   - Ví dụ: Nếu không tìm thấy LinkedIn, gửi thông báo **"Không tìm thấy profile LinkedIn cho [Tên Người Dùng]"** sang Slack.

3. **Lưu Log Dữ Liệu**:
   - Thêm **node Database (SQL/NoSQL)** để lưu lịch sử tra cứu, giúp theo dõi và phân tích sau này.

4. **Kết Hợp Với CRM (HubSpot, Salesforce)**:
   - Nếu đang sử dụng **CRM**, có thể **export dữ liệu từ CRM** vào Google Sheets và **tự động cập nhật LinkedIn** vào hệ thống CRM.

5. **Tối Ưu Hóa Prompt AI**:
   - Nếu kết quả không chính xác, điều chỉnh **prompt** trong **Node 3** để AI hiểu rõ hơn:
     ```plaintext
     =Search for LinkedIn profile of {{ $json['Person Info'] }}.
     Only return the exact URL starting with "https://www.linkedin.com/in/".
     If not found, return "Not Found".
     ```

---

### 📌 **Kết Luận: Tự Động Hóa LinkedIn Profile – Không Cần Code!**
Với **workflow này**, các sếp đã **giải phóng thời gian** để tập trung vào công việc quan trọng hơn:
✔ **Không cần copy-paste** giữa Google Sheets và LinkedIn.
✔ **Tự động tra cứu** cho **tất cả người dùng** trong danh sách.
✔ **Cập nhật chính xác** và **không bị lỗi**.

**Hành động ngay hôm nay**:
1. **Import workflow** vào n8n của mình.
2. **Cấu hình Google Sheets và Airtop API**.
3. **Bật Active** và **nhận kết quả tự động**!

👉 **[Tải workflow nguyên bản](https://n8n.io/workflows/3477)** và bắt đầu tự động hóa ngay! 🚀

---
**Cần hỗ trợ?** Đăng ký **VPS n8n** tại [TinoHost](https://tino.vn/vps-n8n?affid=388) để workflow chạy **ổn định 24/7**! 💻⚡️