---
title: "🚀 Tự Động Hàng Ngày Lấy Dữ Liệu Vốn Đầu Tư Mới Nhất Từ Crunchbase Vào Google Sheets"
description: "Workflow tự động hóa 24/7 lấy thông tin các vòng vốn mới nhất (Seed, Serie A, Serie B) từ Crunchbase và cập nhật tự động vào Google Sheets, giúp các sếp Sales/Investor tiết kiệm 10+ giờ/tháng tra cứu thủ công."
slug: "tieu-dung-von-dau-tu-crunchbase-google-sheets"
tags: [n8n, automation, sales, crunchbase, google-sheets]
keywords: [tự động hóa crunchbase, lấy dữ liệu vốn đầu tư tự động, google sheets crunchbase, n8n workflow sales, tự động hóa tra cứu công ty mới vốn]
---

# 🚀 **Tự Động Hàng Ngày Lấy Dữ Liệu Vốn Đầu Tư Mới Nhất Từ Crunchbase Vào Google Sheets**

### **Nỗi Đau Của Các Sếp Sales/Investor**
Tra cứu thông tin các công ty mới vốn (Seed, Serie A, Serie B) trên **Crunchbase** là công việc **mệt mỏi và tốn thời gian** của các sếp Sales, Investor hoặc Analyst. Thường xuyên phải:
- **Tìm kiếm thủ công** trên trang web Crunchbase hoặc các công cụ như Piloterr.
- **Chuyển dữ liệu** vào Google Sheets để theo dõi và phân tích.
- **Cập nhật hàng ngày** để không bỏ lỡ cơ hội mới.

**Workflow này giải quyết tất cả bằng cách tự động hóa toàn bộ quy trình!**

---

### **🎯 Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ/tháng** tra cứu thủ công.
- **Dữ liệu chính xác và cập nhật liên tục** (Seed, Serie A, Serie B).
- **Tự động lưu vào Google Sheets** với định dạng sẵn sàng phân tích.
- **Hoạt động 24/7** mà không cần can thiệp.
- **Dễ dàng mở rộng** để kết nối với Slack/Email báo cáo.
:::

---

### **🔧 Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi chạy workflow, các sếp cần:
1. **Tài khoản Piloterr** (để lấy API Key):
   - Đăng ký tại [Piloterr](https://piloterr.com/) (miễn phí cho phiên bản cơ bản).
   - **Lấy API Key** từ Dashboard → API Keys.
2. **Google Sheets OAuth2 API Key**:
   - Cài đặt [Google Sheets OAuth2](https://developers.google.com/sheets/api/quickstart/python) và tạo một sheet mới để lưu dữ liệu.
3. **n8n Self-hosted** (không dùng phiên bản cloud):
   - **👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (Mã giảm giá: **VPSN8N** - giảm tới 39%)**
   - **👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)**
:::

---

### **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/2076) hoặc copy JSON từ [Notion Guide](https://lempire.notion.site/Get-recent-fundraising-in-Google-Sheets-dafbbda2635544b4925c4fb04abac8f5?pvs=74).
- **Dán vào n8n Editor** (File → Import Workflow → Paste JSON).
- **Kích hoạt chế độ "Active"** sau khi import.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow gồm **11 node**, nhưng các sếp có thể **xóa node không cần thiết** (ví dụ: chỉ giữ **Serie A** và xóa **Seed/Serie B**).

##### **A. Cấu Hình Piloterr API Key**
- **Node "Piloterr - Get Recent Fundraise - Serie A"**, **"Serie B"**, **"Seed"**:
  - **Credentials**: Chọn `httpHeaderAuth`.
  - **Điền API Key** từ Piloterr vào trường `Authorization` (dạng `Bearer YOUR_API_KEY`).
  - **Tham số quan trọng**:
    - `stage`: `seed`, `serieA`, `serieB` (tùy chọn).
    - `limit`: Số lượng kết quả lấy (mặc định 50).

##### **B. Cấu Hình Google Sheets**
- **Node "Google Sheets"**:
  - **Credentials**: Chọn `googleSheetsOAuth2Api`.
  - **Sheet Name**: Điền tên sheet muốn lưu (ví dụ: `Fundraising_Data`).
  - **Range**: `A1` (để ghi từ ô A1).
  - **Operation**: `appendOrUpdate` (tự động thêm hoặc cập nhật dữ liệu).

##### **C. Node "Prepare data" & "Prepare data before importing to Gsheets"**
- **Node "Prepare data"**:
  - Chỉnh sửa **JSON Path** nếu cần (mặc định lấy dữ liệu từ Piloterr).
- **Node "Get Linkedin URL from object"**:
  - **Code JavaScript** (nếu cần trích xuất URL LinkedIn từ dữ liệu):
    ```javascript
    return {
      linkedinUrl: item.company?.linkedin_url || null
    };
    ```

##### **D. Schedule Trigger**
- **Node "Schedule Trigger - Run Workflow Every Day"**:
  - **Chọn thời gian chạy** (ví dụ: 8h sáng hàng ngày).
  - **Kích hoạt** để workflow chạy tự động.

---

### **✍️ Mẹo & Gợi Ý Nâng Cao**
1. **Kết nối với Slack/Email**:
   - Thêm node **Slack Webhook** hoặc **Email** để báo cáo kết quả hàng ngày.
2. **Lưu Log Dữ Liệu**:
   - Sử dụng node **Google Drive** để lưu bản sao dữ liệu trước khi cập nhật Sheets.
3. **Lọc Dữ Liệu Theo Địa Phương**:
   - Thêm node **Code** để lọc công ty theo quốc gia (ví dụ: `item.company?.country === "Vietnam"`).
4. **Tự Động Xóa Dữ Liệu Cũ**:
   - Sử dụng **Google Apps Script** để xóa dữ liệu cũ trước khi append mới.

---

### **📌 Kết Luận**
Workflow này **giúp các sếp Sales/Investor tự động hóa việc tra cứu và cập nhật dữ liệu vốn đầu tư mới nhất từ Crunchbase vào Google Sheets**, tiết kiệm thời gian và tăng hiệu quả phân tích.

**🚀 Hành động ngay!**
1. **Cài đặt n8n trên VPS** (để chạy 24/7).
2. **Import workflow** và cấu hình API Key.
3. **Kích hoạt Schedule Trigger** để dữ liệu tự động cập nhật hàng ngày.

**💡 Lưu ý**: Nếu cần hỗ trợ, tham khảo [Notion Guide](https://lempire.notion.site/Get-recent-fundraising-in-Google-Sheets-dafbbda2635544b4925c4fb04abac8f5?pvs=74) hoặc liên hệ cộng đồng n8n.

---