---
title: "🚀 Tự Động Hóa Cập Nhật Công Việc Làm Remote Từ RemoteOK → Airtable → Telegram (Không Code)"
description: "Workflow tự động hóa lấy dữ liệu công việc làm remote từ RemoteOK, xử lý và lưu vào Airtable, đồng thời gửi thông báo định kỳ qua Telegram. Giúp các sếp tiết kiệm thời gian theo dõi thị trường công việc 24/7."
slug: "tieu-dong-hoa-cap-nhat-cong-viec-lam-remote-remoteok-airtable-telegram"
tags: [n8n, automation, remote-jobs, airtable, telegram-bot, no-code]
keywords: [n8n workflow remote jobs, tự động hóa công việc làm remote, lấy dữ liệu RemoteOK, Airtable API, Telegram bot tự động]
---

# 🚀 **Tự Động Hóa Cập Nhật Công Việc Làm Remote: Từ RemoteOK → Airtable → Telegram**

### **Nỗi Đau Của Các Sếp**
Bạn có bao giờ phải **quét hàng chục trang** trên RemoteOK, **copy-paste** thông tin công việc vào Airtable, rồi **gửi tin nhắn** cho đồng nghiệp để cập nhật mới nhất? Thời gian và công sức này có thể được **tự động hóa hoàn toàn** với một workflow n8n đơn giản!

Workflow này sẽ:
✅ **Lấy dữ liệu công việc làm remote** từ RemoteOK API
✅ **Xử lý và sắp xếp** thông tin (xóa HTML, định dạng lương, kiểm tra port)
✅ **Lưu vào Airtable** để quản lý dễ dàng
✅ **Gửi thông báo qua Telegram** khi có công việc mới

---
### **🎯 Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 5+ giờ/tuần** không phải thủ công cập nhật dữ liệu.
- **Dữ liệu chính xác và sạch** (xóa HTML, định dạng lương tự động).
- **Cập nhật liên tục** (không phụ thuộc vào thời gian làm việc).
- **Gửi báo cáo tự động** qua Telegram cho đội nhóm.
- **Quản lý dễ dàng** với Airtable (sắp xếp, lọc, theo dõi).
:::

---
### **🔧 Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi chạy workflow, các sếp cần chuẩn bị:
1. **Tài khoản RemoteOK** (để lấy API key nếu cần).
2. **Airtable API Key** (để kết nối với bảng dữ liệu).
   - **Hướng dẫn lấy API Key Airtable**:
     - Truy cập [Airtable API Docs](https://airtable.com/api) → Tạo một **API Key** mới.
     - Thêm **Base ID** của bảng bạn muốn lưu dữ liệu (có thể tìm trong URL của bảng Airtable).
3. **Telegram Bot Token** (để gửi thông báo).
   - **Hướng dẫn tạo Bot Telegram**:
     - Gửi tin nhắn cho [@BotFather](https://t.me/BotFather) → Tạo bot mới → Nhận **API Token**.
     - Tạo **Chat ID** của nhóm/đối tượng nhận tin nhắn (có thể lấy bằng cách gửi tin nhắn cho bot và check URL).
4. **n8n Self-hosted** (để chạy 24/7).
   - 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%).
   - 👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172).
:::

---
### **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n Workflow](https://n8n.io/workflows/4383) hoặc copy toàn bộ JSON từ trang này.
- Mở **n8n Editor** → Nhấn **Import** → Dán hoặc tải file JSON.
- **Kích hoạt workflow** bằng cách bật **Active** ở góc trên bên phải.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này có **10 node**, nhưng các bước quan trọng nhất cần chú ý:

##### **A. Schedule Trigger (Định thời gian chạy)**
- **Cấu hình**:
  - Thiết lập **interval** (ví dụ: chạy hàng ngày lúc 8h sáng).
  - Ví dụ: `0 8 * * *` (lúc 8h00 hàng ngày).

##### **B. RemoteOK (HTTP Request) → Lấy Dữ liệu**
- **Node**: `Remote ok` (type: `httpRequest`)
- **Cấu hình**:
  - **Method**: `GET`
  - **URL**: `https://remoteok.com/api`
  - **Headers** (nếu cần):
    - `Accept: application/json`
  - **Lưu ý**: Nếu RemoteOK yêu cầu API Key, thêm vào **Headers** với key `Authorization`.

##### **C. Airtable (Lưu Dữ liệu)**
- **Node**: `RemoteOK Jobs` (type: `airtable`)
- **Cấu hình**:
  - **Credentials**: Chọn `airtableTokenApi` (đã tạo trước).
  - **Table Name**: Tên bảng Airtable bạn muốn lưu (ví dụ: `RemoteJobs`).
  - **Operation**: `upsert` (cập nhật hoặc thêm mới).
  - **Key Parameters**:
    - `job_id` (sử dụng làm **Primary Key** để tránh trùng lặp).
    - **Fields cần lưu**:
      ```json
      {
        "title": "$json.title",
        "company": "$json.company",
        "location": "$json.location",
        "description": "$json.description",
        "salary_min": "$json.salary_min",
        "salary_max": "$json.salary_max",
        "remote_port": "$json.remote_port",
        "url": "$json.url"
      }
      ```

##### **D. Telegram (Gửi Thông Báo)**
- **Node**: `Telegram1` (type: `telegram`)
- **Cấu hình**:
  - **Credentials**: Chọn `telegramApi` (API Token đã tạo).
  - **Chat ID**: ID của nhóm/đối tượng nhận tin nhắn (lấy từ URL khi gửi tin nhắn cho bot).
  - **Message Format**: Sử dụng node `Table to a single message` (type: `code`) để định dạng tin nhắn.
    - **Ví dụ mã JavaScript trong node**:
      ```javascript
      // Dữ liệu đầu vào từ Airtable
      const jobs = $input.all();

      // Định dạng tin nhắn Telegram
      let message = `🚀 **Cập Nhật Công Việc Làm Remote**\n\n`;
      jobs.forEach(job => {
        message += `📌 **${job.title}**\n`;
        message += `🏢 **Công Ty**: ${job.company}\n`;
        message += `📍 **Địa Điểm**: ${job.location}\n`;
        message += `💰 **Lương**: ${job.salary_min} - ${job.salary_max}\n`;
        message += `🔗 **Link**: ${job.url}\n\n`;
      });

      return { json: { text: message } };
      ```

##### **E. Các Node Code (Xử Lý Dữ Liệu)**
Workflow có **4 node code** để xử lý dữ liệu:
1. **Cleaning the received input** (xóa ký tự đặc biệt, HTML).
2. **Salary to string** (định dạng lương thành chuỗi).
3. **Text-clean** (sạch hóa mô tả công việc).
4. **Table to a single message** (định dạng tin nhắn Telegram).

- **Lưu ý**:
  - Các node code này **không cần chỉnh sửa** nếu bạn muốn giữ nguyên logic gốc.
  - Nếu muốn **thêm logic mới**, mở node code → chỉnh sửa mã JavaScript.

---
### **✍️ Mẹo & Gợi Ý Nâng Cao**
:::info[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Thêm Slack Notification**:
   - Thay vì Telegram, bạn có thể **kết nối với Slack** bằng node `slack` để gửi thông báo.
   - **Hướng dẫn**: Tạo bot Slack → Lấy **API Token** → Cấu hình node `slack` tương tự như Telegram.

2. **Lưu Log Lịch Sử**:
   - Thêm node `stickyNote` để **ghi lại lịch sử chạy** (giúp theo dõi lỗi hoặc cập nhật).
   - **Cách làm**:
     - Thêm node `stickyNote` vào cuối workflow.
     - Cấu hình **key**: `remote_jobs_update_${date}`.
     - **Value**: `$json` (dữ liệu công việc mới).

3. **Báo Cáo Định Kỳ**:
   - Sử dụng **node `scheduleTrigger`** để chạy workflow **hàng tuần** và gửi báo cáo tổng hợp qua Email/Telegram.
   - **Ví dụ**:
     - Thêm node `email` (n8n-nodes-base.email) để gửi báo cáo định kỳ.

4. **Lọc Công Việc Theo Địa Điểm**:
   - Trong node `code` (Cleaning the received input), bạn có thể **lọc chỉ công việc ở Việt Nam** bằng mã:
     ```javascript
     return $input.all().filter(job => job.location.includes("Vietnam"));
     ```

5. **Kết Nối với Google Sheets**:
   - Thay vì Airtable, bạn có thể **lưu vào Google Sheets** bằng node `googleSheets`.
   - **Hướng dẫn**: Tạo **API Key Google Sheets** → Cấu hình node tương tự Airtable.
:::

---
### **📌 Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp để tập trung vào việc **tìm kiếm và đánh giá ứng viên** thay vì phải **quét dữ liệu thủ công**. Với **n8n self-hosted**, bạn có thể **chạy 24/7** mà không lo mất dữ liệu.

**Bắt đầu ngay hôm nay!**
1. **Import workflow** từ link trên.
2. **Cấu hình API Keys** (Airtable, Telegram).
3. **Kích hoạt và chạy** để tự động cập nhật công việc làm remote!

---
**💡 Chia sẻ ý kiến** của bạn về workflow này trong phần **Comments** dưới đây! Các sếp có thể **mở rộng** nó thêm nhiều tính năng khác như **dự báo thị trường công việc** hay **gửi báo cáo cho CEO** hàng tháng. 🚀