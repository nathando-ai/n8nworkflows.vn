---
title: "🏠 **Tự Động Hóa Lấy Dữ Liệu Bất Động Sản Từ Idealista Với ScrapeGraph AI (Không Cần Code!)**"
description: "Giải pháp tự động hóa lấy danh sách bất động sản từ Idealista với độ chính xác cao, tiết kiệm thời gian so sánh thị trường và tìm kiếm nhà đất. Khả năng hoạt động 24/7, cập nhật liên tục, không phụ thuộc vào thủ công."
slug: "tieu-dong-hoa-lay-du-lieu-bat-dong-san-tu-idealista"
tags: [n8n, automation, no-code, scrapegraph-ai, real-estate, bất động sản]
keywords: [tự động hóa lấy dữ liệu bất động sản, scrape idealista, n8n workflow bất động sản, tìm nhà đất tự động, scrapegraph ai]
---

# 🚀 **Tự Động Hóa Lấy Dữ Liệu Bất Động Sản Từ Idealista Với ScrapeGraph AI**

### **Nỗi Đau Của Các Sếp Trong Thị Trường Bất Động Sản**
Hàng ngày, các nhà đầu tư, môi giới bất động sản và chuyên gia thị trường phải mất **giờ đồng hồ** để:
- **Tìm kiếm thủ công** trên Idealista, Metfone, Batdongsan.vn...
- **So sánh giá** giữa các khu vực, loại nhà, diện tích...
- **Lưu trữ dữ liệu** vào Excel/Google Sheets để phân tích sau.
- **Cập nhật liên tục** khi có nhà đất mới phù hợp với yêu cầu.

**Kết quả?** Thời gian làm việc bị "chôn vùi" trong công việc lặp đi lặp lại, còn cơ hội đầu tư bị bỏ lỡ vì không kịp thời.

### **🎯 Giải Pháp: Tự Động Hóa 100% Với ScrapeGraph AI + n8n**
Workflow này **không cần code**, sử dụng **ScrapeGraph AI** để:
✅ **Lấy dữ liệu bất động sản** từ Idealista **tự động**, bao gồm:
- Giá bán/mướn
- Diện tích, số phòng
- Vị trí, khu vực
- Link chi tiết
✅ **Cập nhật liên tục** (dùng Webhook hoặc lịch trình định kỳ)
✅ **Xuất dữ liệu** vào **Google Sheets, Airtable, hoặc API của bạn**
✅ **Gửi báo cáo** qua **Slack/Email** khi có nhà đất mới phù hợp
✅ **Hoạt động 24/7** trên **VPS riêng** (không phụ thuộc vào máy tính cá nhân)

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7**, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### **🎯 Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10-20 giờ/tuần** so với cách làm thủ công.
- **Dữ liệu chính xác, cập nhật thời gian thực** (không bị lỗi copy-paste).
- **So sánh thị trường nhanh chóng** với Excel/Google Sheets tự động.
- **Nhận thông báo ngay** khi có nhà đất phù hợp (ví dụ: giá < 500 triệu, diện tích > 100m²).
- **Không phụ thuộc vào nhân viên** (hoạt động 24/7).
:::

---

### **🔧 Yêu Cầu Cần Thiết**
Trước khi chạy workflow, các sếp cần chuẩn bị:
1. **Tài khoản Idealista** (để xác thực scrape).
2. **API Key của ScrapeGraph** (miễn phí cho lượng scrape nhỏ).
3. **Google Sheets/Airtable** (để lưu dữ liệu).
4. **Credentials cho Slack/Email** (nếu muốn gửi báo cáo).
5. **VPS n8n** (để workflow chạy liên tục).

---
:::note[LƯU Ý]
- ScrapeGraph AI **không yêu cầu API key của Idealista** (khác với cách scrape thủ công).
- Workflow **không cần node nào** (do ScrapeGraph AI tự xử lý scrape), nhưng cần **cấu hình URL và lọc dữ liệu** phù hợp.
:::

---

### **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Workflow này **không có file JSON** (do là workflow cộng đồng), nhưng các sếp có thể:
- **Tạo từ đầu** bằng các node sau:
  - **ScrapeGraph AI** (node chính để lấy dữ liệu)
  - **HTTP Request** (nếu cần gọi API khác)
  - **Google Sheets/Airtable** (để lưu dữ liệu)
  - **Slack/Email** (nếu muốn gửi báo cáo)

**Bước chi tiết:**
1. Mở **n8n Editor** → Tạo workflow mới.
2. Thêm **node ScrapeGraph AI**:
   - **URL**: `https://idealista.com/vi/ban-nha/` (hoặc URL cụ thể của bạn).
   - **Selector**: Chọn các phần tử cần scrape (giá, diện tích, địa chỉ...).
   - **API Key**: Điền vào `ScrapeGraph API Key` (mua tại [scrapegraph.ai](https://scrapegraph.ai/)).
3. Thêm **node HTTP Request** (nếu cần gọi API khác).
4. Thêm **node Google Sheets** (để lưu dữ liệu):
   - Chọn **Credentials** → Thêm Google Sheets.
   - Chọn **Sheet Name** và **Range** (ví dụ: `Sheet1!A1`).
5. Thêm **node Slack/Email** (nếu muốn gửi báo cáo):
   - Cấu hình **Webhook URL** của Slack hoặc **Email API**.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
| **Node**               | **Cần Chỉnh Sửa Gì?**                                                                 | **Hướng Dẫn**                                                                 |
|------------------------|--------------------------------------------------------------------------------------|-------------------------------------------------------------------------------|
| **ScrapeGraph AI**     | URL scrape và selector.                                                             | - Sử dụng **Inspect Tool** (F12) trên Idealista để lấy **XPath/CSS Selector**. |
|                        |                                                                                      | - Ví dụ: `//div[@class="property-card"]` để lấy danh sách nhà.               |
| **Google Sheets**      | Sheet Name và Range.                                                              | - Đảm bảo **Google Sheets** đã chia sẻ với n8n.                              |
| **Slack/Email**        | Webhook URL hoặc API Key.                                                          | - Cấu hình **Incoming Webhook** trên Slack.                                  |
| **Webhook (nếu dùng)**| URL để nhận dữ liệu từ bên ngoài.                                                 | - Sử dụng **n8n Webhook** để kích hoạt workflow khi có yêu cầu.              |

#### **3. Kích Hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Chạy workflow với **1-2 trang** Idealista để kiểm tra.
   - Kiểm tra **Google Sheets** có xuất dữ liệu không.
2. **Bật Active**:
   - Đặt workflow vào **chế độ Active**.
   - Nếu muốn **cập nhật định kỳ**, sử dụng **node Schedule Trigger**.

---

### **✍️ Mẹo & Gợi Ý Nâng Cao**
1. **Lọc Dữ Liệu Theo Yêu Cầu**:
   - Sử dụng **node Filter** để chỉ lấy nhà đất **giá < 500 triệu** hoặc **diện tích > 100m²**.
   - Ví dụ:
     ```json
     {{ $item.price }} < 500000000
     ```

2. **Gửi Báo Cáo Định Kỳ**:
   - Sử dụng **node Schedule Trigger** (cài đặt chạy hàng ngày).
   - Kết hợp với **node Email/Slack** để gửi báo cáo.

3. **Lưu Log Dữ Liệu**:
   - Thêm **node Database (MongoDB/PostgreSQL)** để lưu lịch sử scrape.
   - Tránh trùng lặp dữ liệu.

4. **Kết Hợp Với AI Chatbot**:
   - Sử dụng **node LLM (n8n AI)** để **tóm tắt thị trường** từ dữ liệu scrape.
   - Ví dụ: "Hiện có 5 nhà đất dưới 500 triệu tại quận 1, trung bình giá là 450 triệu."

5. **Tự Động Cập Nhật Giá**:
   - Sử dụng **node HTTP Request** để gọi API của Idealista (nếu có) để lấy giá mới nhất.

---

### **📌 Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp trong ngành bất động sản, giúp:
✔ **Tìm kiếm nhà đất nhanh chóng** mà không cần copy-paste.
✔ **So sánh thị trường chính xác** với dữ liệu tự động.
✔ **Nhận thông báo ngay** khi có cơ hội đầu tư phù hợp.

**Hành động ngay!**
1. **Cài n8n trên VPS** (để workflow chạy 24/7).
2. **Tạo workflow** theo hướng dẫn trên.
3. **Cấu hình URL và lọc dữ liệu** phù hợp với nhu cầu.
4. **Bật Active** và **nhận dữ liệu bất động sản tự động mỗi ngày!**

---
**💡 Cần hỗ trợ kỹ thuật?**
- Trên **n8n Community** ([forum.n8n.io](https://forum.n8n.io/)).
- Trên **Discord n8n** ([discord.gg/n8n](https://discord.gg/n8n)).