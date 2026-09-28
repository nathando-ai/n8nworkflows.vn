---
title: "📊 Tự Động Hóa Báo Cáo Tình Trạng Dự Án Tuần Tuần Cho Smenso Với Email - Không Cần Code"
description: "Hàng tuần, workflow này tự động lấy tất cả dự án đang hoạt động từ smenso, tổng hợp thành báo cáo HTML và gửi qua email cho quản lý - tiết kiệm 10+ giờ công mỗi tháng cho các sếp. Đặc biệt phù hợp cho các team quản lý dự án cần báo cáo định kỳ."
slug: "tu-dong-hoa-bao-cao-tinh-trang-du-an-tuan-tuan-smenso-email"
tags: [n8n, automation, project-management, smenso, gmail, email-automation]
keywords: [n8n workflow smenso, tự động hóa báo cáo dự án, gửi email tự động hàng tuần, quản lý dự án không code, báo cáo định kỳ smenso]
---

# 🚀 **Tự Động Hóa Báo Cáo Tình Trạng Dự Án Tuần Tuần Cho Smenso Với Email**

### **Nỗi Đau Của Các Sếp**
Hàng tuần, các sếp phải mất **30-60 phút** để:
- Lấy danh sách dự án từ smenso
- Tính toán tiến độ, tình trạng, và chỉ số KPI
- Chuyển đổi dữ liệu thành báo cáo đẹp mắt
- Gửi qua email cho team hoặc lãnh đạo

Kết quả? **Báo cáo không đồng bộ, thiếu chính xác, và tốn nhiều thời gian** mà lại không được cá nhân hóa. **Workflow này giải quyết tất cả!**

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7** và không bị gián đoạn, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### **🎯 Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm 10+ giờ công/tháng** – Không cần làm thủ công báo cáo tuần.
✅ **Báo cáo chính xác 100%** – Dữ liệu tự động lấy từ smenso, không sai sót.
✅ **Cá nhân hóa & chuyên nghiệp** – Báo cáo HTML đẹp mắt, dễ đọc.
✅ **Hoạt động liên tục** – Gửi tự động hàng tuần, không phụ thuộc vào người.
✅ **Dễ mở rộng** – Thêm các chỉ số KPI khác (ngân sách, tiến độ, người tham gia...).
:::

---

### **🔧 Yêu Cầu Cần Thiết**
Trước khi chạy workflow, các sếp cần chuẩn bị:
1. **Tài khoản smenso** và **API Key** của smenso (để kết nối với node `smenso`).
2. **Tài khoản Gmail** (hoặc Outlook/SMTP) với **OAuth2** để gửi email.
3. **Địa chỉ email nhận** (điền vào node `Send Email`).
4. **n8n Self-hosted** (không dùng phiên bản miễn phí trên cloud).

---

### **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Cách 1:** Tải file JSON từ [link gốc](https://n8n.io/workflows/15269) và import vào **n8n Editor**.
- **Cách 2:** Copy toàn bộ JSON từ [đây](https://n8n.io/workflows/15269) và paste vào **Import Workflow** trong n8n.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow gồm **4 node chính**, các sếp cần chú ý:

##### **Node 1: Every Monday at 8am (scheduleTrigger)**
- **Cấu hình:** Cron `0 8 * * 1` (8h sáng thứ 2).
- **Lưu ý:** Nếu muốn thay đổi thời gian, chỉnh ở đây (ví dụ: `0 9 * * 1` để 9h sáng).

##### **Node 2: Get All Projects (smenso)**
- **Credentials:** Chọn `smensoApi` (đã cấu hình trước).
- **Operation:** `getMany` (lấy tất cả dự án).
- **Resource:** `project` (dự án).
- **Lưu ý:**
  - Chạy **manual run** trước để kiểm tra dữ liệu lấy được.
  - Nếu cần lấy thêm trường (ví dụ: `status`, `budget`), chỉnh ở đây.

##### **Node 3: Build HTML Report (code)**
- **Mã nguồn mặc định:**
  ```javascript
  const html = `
  <html>
    <head>
      <style>
        body { font-family: Arial, sans-serif; }
        table { border-collapse: collapse; width: 100%; }
        th, td { border: 1px solid #ddd; padding: 8px; text-align: left; }
        th { background-color: #f2f2f2; }
      </style>
    </head>
    <body>
      <h1>Weekly Smenso Project Status Report</h1>
      <table>
        <tr>
          <th>Project Name</th>
          <th>Status</th>
          <th>Progress (%)</th>
          <th>Assigned To</th>
        </tr>
        ${$input.all().map(item => `
          <tr>
            <td>${item.json.name}</td>
            <td>${item.json.status}</td>
            <td>${item.json.progress}%</td>
            <td>${item.json.assignedTo}</td>
          </tr>
        `).join('')}
      </table>
    </body>
  </html>
  `;
  return { json: { html: html } };
  ```
- **Lưu ý:**
  - Nếu muốn **thêm trường dữ liệu**, chỉnh ở phần `item.json` (ví dụ: `item.json.budget`).
  - **Thay đổi style CSS** để báo cáo đẹp mắt hơn.

##### **Node 4: Send Email (gmail)**
- **Credentials:** Chọn `gmailOAuth2` (đã cấu hình OAuth2).
- **To:** Điền **địa chỉ email nhận** (ví dụ: `team@company.com`).
- **Subject:** Mặc định là `"Weekly Project Status Report"` (có thể thay đổi).
- **Body:** Chọn `HTML` và chọn `html` từ node trước.
- **Lưu ý:**
  - Nếu muốn **gửi cho nhiều người**, thêm địa chỉ vào trường `To` (ví dụ: `team1@company.com,team2@company.com`).
  - **Không dùng Gmail?** Thay thế bằng **Outlook** hoặc **SMTP node**.

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Chạy **manual run** để kiểm tra email có gửi đúng không.
2. **Bật Active workflow**:
   - Đảm bảo **scheduleTrigger** hoạt động và **gmail** có quyền gửi email.

---

### **✍️ Mẹo & Gợi Ý Nâng Cao**
1. **Thêm Log & Debugging**
   - Sử dụng **Sticky Note node** để ghi lại lỗi hoặc thông tin debug.
   - Ví dụ: `Error: ${$json.error}` (nếu có lỗi trong API smenso).

2. **Gửi Báo Cáo Cho Nhiều Người**
   - Thay vì gửi cho 1 email, **tách danh sách** và gửi từng người (ví dụ: quản lý dự án, CEO).

3. **Kết Hợp Với Slack/Telegram**
   - Thêm **Slack Webhook** hoặc **Telegram Bot** để thông báo khi báo cáo được gửi.

4. **Lưu Báo Cáo Vào Google Drive/Dropbox**
   - Sử dụng **Google Drive** hoặc **Dropbox node** để lưu bản sao báo cáo.

5. **Tự Động Cập Nhật Dữ Liệu**
   - Nếu cần **báo cáo hàng ngày**, chỉnh cron thành `0 8 * * *` (8h sáng mỗi ngày).

---

### **📌 Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp để tập trung vào việc **quản lý chiến lược** thay vì làm thủ công báo cáo. **Chỉ cần 5 phút setup**, workflow sẽ tự động:
✔ Lấy dữ liệu từ smenso
✔ Xây dựng báo cáo HTML đẹp mắt
✔ Gửi email tự động hàng tuần

**Hãy áp dụng ngay và tiết kiệm thời gian cho team của mình!** 🚀

---
**🔗 [Tải workflow nguyên bản](https://n8n.io/workflows/15269)**
**💡 Cần hỗ trợ?** Đăng ký **VPS n8n** từ [TinoHost](https://tino.vn/vps-n8n?affid=388) để chạy ổn định 24/7!**