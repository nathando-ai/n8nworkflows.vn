---
title: "🚀 Tự Động Hóa Báo Cáo BGV Hàng Ngày: Theo Dõi Xác Minh Tài Năng qua Email từ Google Sheets"
description: "Workflow tự động hóa gửi báo cáo tổng hợp hàng ngày về trạng thái xác minh BGV (Background Verification) cho các quản lý, giúp tiết kiệm thời gian và đảm bảo tính chính xác 100%. Dữ liệu được lấy từ Google Sheets và gửi qua email cá nhân hóa theo thời gian biểu cố định."
slug: "tu-dong-hoa-bao-cao-bgv-hang-ngay"
tags: [n8n, automation, hr, google-sheets, gmail, no-code, ai-multimodal]
keywords: [n8n workflow bgv, tự động hóa báo cáo hr, gửi email tự động từ google sheets, theo dõi xác minh nhân sự, tiết kiệm thời gian quản lý bgv]
---

# 🚀 **Tự Động Hóa Báo Cáo BGV Hàng Ngày: Theo Dõi Xác Minh Tài Năng qua Email**

### **Nỗi Đau Của Các Sếp**
Quản lý quá trình **Xác Minh Tài Năng (BGV)** là một công việc tốn thời gian và dễ mắc lỗi khi phải:
- **Lấy dữ liệu thủ công** từ Google Sheets hàng ngày.
- **Tổng hợp và phân loại** các hồ sơ đã hoàn thành, đang chờ, hoặc quá hạn.
- **Gửi báo cáo cá nhân hóa** cho từng quản lý, dễ bị bỏ sót hoặc sai lệch.
- **Phải làm lại** nếu có thay đổi cuối cùng.

Workflow này **giải quyết tất cả** bằng cách tự động hóa toàn bộ quy trình, giúp các sếp **tiết kiệm 5-10 giờ/lần** và đảm bảo **tính chính xác cao**.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần tổng hợp dữ liệu thủ công hàng ngày.
- **Tính chính xác cao**: Dữ liệu được tự động phân loại và gửi chính xác.
- **Cá nhân hóa hoàn toàn**: Mỗi quản lý nhận báo cáo riêng với thông tin liên quan.
- **Hoạt động liên tục**: Báo cáo được gửi tự động vào mỗi đêm (23:00 IST).
- **Đa dạng định dạng**: Báo cáo bao gồm cả **dữ liệu đã hoàn thành** và **dữ liệu quá hạn** (được đánh dấu ⚠️).
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Google Sheets**:
   - Một bảng Google Sheets với **tab "BGV Tracker"** chứa dữ liệu BGV (cột cần thiết: `bgv_completion_date`, `last_follow_up`, `bgv_exe_email`).
   - **Quản lý quyền**: Cung cấp quyền "Đọc" cho n8n để truy cập bảng.
2. **Tài khoản Gmail**:
   - Một tài khoản Gmail để n8n gửi email báo cáo (không phải tài khoản cá nhân).
   - **Quản lý quyền OAuth**: Cấu hình OAuth 2.0 cho n8n truy cập Gmail.
3. **Thời gian biểu (Schedule)**:
   - Workflow sẽ chạy hàng đêm vào **23:00 IST** (giả sử các sếp ở Việt Nam, có thể điều chỉnh theo múi giờ).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/8114](https://n8n.io/workflows/8114) (hoặc copy JSON từ trang này).
- **Mở n8n Editor** → Nhấn **"Import"** → Dán JSON và nhấn **"Import"**.
- **Kiểm tra cấu trúc**: Workflow sẽ hiển thị 6 node như mô tả dưới đây.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này sử dụng **5 node chính**, mỗi node đều cần cấu hình cẩn thận:

##### **1. Schedule Trigger**
- **Cấu hình**:
  - **Time**: Đặt thành **23:00** (múi giờ IST). Nếu các sếp ở Việt Nam, có thể điều chỉnh thành **22:00** (IST = UTC+5:30).
  - **Time Zone**: Chọn **Asia/Kolkata** (hoặc **Asia/Ho_Chi_Minh** nếu cần).
  - **Active**: Bật để workflow chạy tự động hàng đêm.

##### **2. Google Sheets**
- **Cấu hình**:
  - **Credentials**: Chọn `"googleSheetsOAuth2Api"` (đã cấu hình trước khi import).
  - **Operation**: Chọn **"Get rows"**.
  - **Sheet Name**: Nhập **"BGV Tracker"** (hay tên tab chứa dữ liệu BGV).
  - **Range**: Chọn toàn bộ bảng (hoặc chỉ cột cần thiết).
  - **Active**: Bật để workflow đọc dữ liệu từ Google Sheets.

##### **3. Code Node (Normalize & Parse)**
- **Cấu hình**:
  - **JavaScript Code** (sử dụng mã gốc từ workflow, nhưng các sếp có thể chỉnh sửa nếu cần):
    ```javascript
    // Chuyển đổi tên cột thành lowercase
    const normalizedData = $input.all().map(row => {
      const normalizedRow = {};
      Object.keys(row).forEach(key => {
        normalizedRow[key.toLowerCase()] = row[key];
      });

      // Parse ngày tháng
      if (normalizedRow.bgv_completion_date) {
        normalizedRow.iscompletedtoday = new Date(normalizedRow.bgv_completion_date).toDateString() === new Date().toDateString();
      }

      if (normalizedRow.last_follow_up) {
        const lastFollowUpDate = new Date(normalizedRow.last_follow_up);
        const daysSinceFollowUp = Math.ceil((new Date() - lastFollowUpDate) / (1000 * 60 * 60 * 24));
        normalizedRow.isstale = normalizedRow.status === "Pending" && daysSinceFollowUp >= 3;
      }

      return normalizedRow;
    });
    return { json: normalizedData };
    ```
  - **Lưu ý**:
    - Đảm bảo cột `bgv_completion_date` và `last_follow_up` tồn tại trong Google Sheets.
    - Nếu dữ liệu ngày tháng có định dạng khác, chỉnh sửa phần `parse` tương ứng.

##### **4. Code Node (Group & Filter)**
- **Cấu hình**:
  - **JavaScript Code** (tương tự, nhưng nhóm theo `bgv_exe_email`):
    ```javascript
    const groupedData = {};
    $input.all().forEach(row => {
      const email = row.bgv_exe_email;
      if (!groupedData[email]) {
        groupedData[email] = {
          completedToday: [],
          pending: [],
          stale: []
        };
      }

      if (row.iscompletedtoday) {
        groupedData[email].completedToday.push(row);
      } else if (row.status === "Pending" && row.isstale) {
        groupedData[email].stale.push(row);
      } else if (row.status === "Pending" && !row.isstale) {
        groupedData[email].pending.push(row);
      }
    });

    return { json: Object.values(groupedData) };
    ```
  - **Lưu ý**:
    - Đảm bảo cột `bgv_exe_email` (email của quản lý) tồn tại.
    - Nếu có cột khác cần nhóm, chỉnh sửa phần `email` trong mã.

##### **5. Code Node (Format Digest)**
- **Cấu hình**:
  - **JavaScript Code** (tạo email HTML cá nhân hóa):
    ```javascript
    const emails = [];
    $input.all().forEach(group => {
      const email = {
        to: group[0].bgv_exe_email,
        subject: `📊 Báo Cáo BGV Hôm Nay - ${new Date().toLocaleDateString('vi-VN')}`,
        html: `
          <h2>Báo Cáo BGV Hôm Nay</h2>
          <p>Xin chào,</p>
          <hr>

          <!-- Dữ liệu đã hoàn thành -->
          ${group.completedToday.length > 0 ? `
            <h3>🟢 Đã Hoàn Thành Hôm Nay</h3>
            <table border="1" cellpadding="5">
              <tr>
                <th>Tên Tài Năng</th>
                <th>Ngày Hoàn Thành</th>
                <th>Trạng Thái</th>
              </tr>
              ${group.completedToday.map(item => `
                <tr>
                  <td>${item.name || 'N/A'}</td>
                  <td>${item.bgv_completion_date || 'N/A'}</td>
                  <td>${item.status || 'N/A'}</td>
                </tr>
              `).join('')}
            </table>
          ` : ''}

          <!-- Dữ liệu đang chờ -->
          ${group.pending.length > 0 ? `
            <h3>🟡 Đang Chờ Xác Minh</h3>
            <table border="1" cellpadding="5">
              <tr>
                <th>Tên Tài Năng</th>
                <th>Ngày Cuối Cùng</th>
                <th>Trạng Thái</th>
                <th>Thao Tác</th>
              </tr>
              ${group.pending.map(item => `
                <tr>
                  <td>${item.name || 'N/A'}</td>
                  <td>${item.last_follow_up || 'N/A'}</td>
                  <td>${item.status || 'N/A'}</td>
                  <td>${item.isstale ? '<span style="color:red;">⚠️ QUÁ HẠN</span>' : ''}</td>
                </tr>
              `).join('')}
            </table>
          ` : ''}
        `
      };
      emails.push(email);
    });

    return { json: emails };
    ```
  - **Lưu ý**:
    - Đảm bảo cột `name`, `status`, `bgv_completion_date`, `last_follow_up` tồn tại.
    - Chỉnh sửa phần `html` để phù hợp với mẫu email của công ty.

##### **6. Gmail**
- **Cấu hình**:
  - **Credentials**: Chọn `"gmailOAuth2"` (đã cấu hình trước).
  - **Operation**: Chọn **"Send email"**.
  - **To**: Sử dụng giá trị từ `to` trong email được tạo ở node trước.
  - **Subject**: Sử dụng giá trị từ `subject` trong email.
  - **HTML**: Sử dụng giá trị từ `html` trong email.
  - **Active**: Bật để gửi email tự động.

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Nhấn **"Run Workflow"** để kiểm tra dữ liệu mẫu.
   - Kiểm tra email đã được gửi đúng không.
2. **Bật Active**:
   - Sau khi test thành công, bật **"Active"** trên node **Schedule Trigger**.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::tip[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Kết hợp với Slack/Telegram**:
   - Thêm node **Slack** hoặc **Telegram Bot** để gửi báo cáo đồng thời qua kênh nhóm.
   - Ví dụ: `{{ $json["html"] }}` có thể được gửi qua Slack với định dạng Markdown.

2. **Lưu Log Dữ Liệu**:
   - Thêm node **Google Drive** hoặc **Google Sheets (Append)** để lưu lịch sử báo cáo.
   - Giúp theo dõi và phân tích xu hướng BGV dài hạn.

3. **Báo Cáo Định Kỳ Theo Tuần/Tháng**:
   - Sửa node **Schedule Trigger** để chạy vào cuối tuần hoặc cuối tháng.
   - Ví dụ: `"0 0 0 * * 0"` (chạy vào Chủ Nhật 00:00).

4. **Tự Động Xử Lý Dữ Liệu Quá Hạn**:
   - Thêm logic trong **Code Node (Group & Filter)** để gửi email cảnh báo tự động cho nhân viên chậm tiến độ.
   - Ví dụ:
     ```javascript
     if (item.isstale) {
       // Gửi email cảnh báo qua Gmail hoặc Slack
     }
     ```

5. **Tích Hợp với CRM (Salesforce/Zoho)**:
   - Thay thế Google Sheets bằng **Salesforce** hoặc **Zoho CRM** để lấy dữ liệu BGV từ hệ thống quản lý khách hàng.
   - Sử dụng node **Salesforce API** hoặc **Zoho CRM** thay cho Google Sheets.
:::

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc thủ công, **tăng tính chính xác** và **cải thiện hiệu quả quản lý BGV**. Với chỉ **6 node đơn giản**, các sếp có thể tự động hóa toàn bộ quy trình, từ lấy dữ liệu đến gửi báo cáo cá nhân hóa.

**Hành động ngay hôm nay**:
1. **Import workflow** và cấu hình theo hướng dẫn.
2. **Test và điều chỉnh** nếu cần.
3. **Bật Active** để bắt đầu tự động hóa!

Nếu có bất kỳ vấn đề nào, hãy để lại bình luận hoặc liên hệ với **WeblineIndia** (tác giả gốc) qua [trang web](https://www.weblineindia.com/). Chúc các sếp thành công! 🚀

---