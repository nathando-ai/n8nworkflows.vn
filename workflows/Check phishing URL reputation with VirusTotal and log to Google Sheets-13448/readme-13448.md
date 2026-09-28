---
title: "🚨 Kiểm tra danh tiếng URL phishing bằng VirusTotal & Log kết quả lên Google Sheets (Tự động hóa Cybersecurity)"
description: "Workflow tự động hóa 100% không code để kiểm tra danh tiếng URL phishing bằng VirusTotal, trả về kết quả phân loại (SAFE/SUSPICIOUS/PHISHING) và lưu log vào Google Sheets. Giúp các sếp bảo mật tự động phát hiện và theo dõi URL nguy hiểm 24/7."
slug: "kiem-tra-url-phishing-virus-total-google-sheets"
tags: [n8n, automation, cybersecurity, virus-total, google-sheets, no-code, secops]
keywords: [n8n workflow phishing, tự động hóa kiểm tra URL, virus total api, log phishing google sheets, bảo mật mạng tự động]
---

# 🚨 **Tự động hóa kiểm tra URL phishing bằng VirusTotal & lưu log vào Google Sheets**

## **Nỗi đau thực tế của các sếp bảo mật**
Trong môi trường làm việc hiện nay, **phishing** là mối đe dọa hàng đầu, gây ra mất mát tài chính và danh tiếng cho doanh nghiệp. Các sếp thường phải:
- **Kiểm tra thủ công** từng URL trên VirusTotal (mất thời gian và dễ bỏ lỡ).
- **Phải theo dõi log** kết quả phân tích trên nhiều tab, làm giảm hiệu quả phản ứng.
- **Không có cảnh báo tự động** khi phát hiện URL nguy hiểm mới.

**Workflow này giải quyết tất cả vấn đề trên bằng cách:**
✅ **Tự động kiểm tra danh tiếng URL** qua VirusTotal (multi-engine scanning).
✅ **Phân loại URL** thành **SAFE/SUSPICIOUS/PHISHING** với logic tự động.
✅ **Lưu log kết quả** vào Google Sheets để theo dõi và phân tích dài hạn.
✅ **Báo lỗi ngay lập tức** nếu URL không hợp lệ hoặc VirusTotal bị lỗi.

---
### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần kiểm tra thủ công, tự động hóa 100%.
- **Chính xác cao**: Sử dụng dữ liệu từ VirusTotal (trusted by 100M+ users).
- **Cảnh báo ngay**: Phát hiện URL phishing trong giây lát.
- **Theo dõi dài hạn**: Log kết quả trên Google Sheets để phân tích xu hướng.
- **Bảo mật toàn diện**: Phân loại URL theo mức độ nguy hiểm (SAFE → PHISHING).
:::

---
## 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
✔ **Tài khoản VirusTotal** (miễn phí hoặc premium) và **API Key**.
✔ **Google Sheets** (để lưu log kết quả).
✔ **n8n Self-hosted** (không dùng phiên bản cloud để đảm bảo bảo mật).
✔ **VPS** (để chạy workflow 24/7, không bị gián đoạn).

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. Tải workflow từ [n8n.io/workflows/13448](https://n8n.io/workflows/13448) (chọn **Export as JSON**).
2. Trên n8n Editor, nhấn **Import** → Chọn file JSON vừa tải.
3. Chọn **Create Workflow** và đặt tên (ví dụ: **"Phishing Checker"**).

#### **Phương pháp 2: Copy/Paste JSON**
1. Copy toàn bộ mã JSON từ [n8n.io/workflows/13448](https://n8n.io/workflows/13448).
2. Trên n8n Editor, nhấn **Import** → Chọn **Paste JSON**.
3. Nhấn **Create Workflow**.

---
### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**

#### **🔐 Cấu hình VirusTotal API**
- **Node:** `VirusTotal - Submit URL for Scan` và `VirusTotal - Get Scan Analysis`
- **Thao tác:**
  1. Nhấn **Add** trên **HTTP Header Auth** (credentials).
  2. Điền:
     - **Name:** `VirusTotal API Key`
     - **Type:** `Header`
     - **Key:** `x-apikey`
     - **Value:** `YOUR_VIRUSTOTAL_API_KEY` (thay bằng API Key của bạn).
  3. Lặp lại cho cả hai node `httpRequest` liên quan.

#### **📊 Cấu hình Google Sheets**
- **Node:** `Log Scan Result`
- **Thao tác:**
  1. Nhấn **Add** trên **googleSheetsOAuth2Api** (credentials).
  2. Đăng nhập Google và cấp quyền cho n8n truy cập Sheets.
  3. Điền tham số:
     - **Spreadsheet ID:** ID của file Google Sheets (tìm trong URL: `https://docs.google.com/spreadsheets/d/SPREADSHEET_ID/edit`).
     - **Sheet Name:** Tên tab muốn lưu log (ví dụ: **"Phishing_Logs"**).
     - **Operation:** `append` (để thêm dữ liệu mới vào cuối).

#### **🔄 Cấu hình Webhook (để nhận URL từ bên ngoài)**
- **Node:** `Webhook - Submit URL for Analysis`
- **Thao tác:**
  1. Nhấn **Add** trên **Webhook**.
  2. Điền:
     - **Path:** `phishing-check` (không đổi).
     - **HTTP Method:** `POST`.
  3. **Lưu ý:** Sau khi import, **không** cần thay đổi gì nếu dùng mặc định.

#### **🔄 Cấu hình logic phân loại phishing (nếu cần thay đổi)**
- **Node:** `Build Phishing Verdict` (Code Node)
- **Thao tác:**
  - Mở node này và chỉnh sửa logic nếu muốn thay đổi ngưỡng phân loại (ví dụ: tăng giảm tỷ lệ `suspicious` thành `phishing`).
  - **Dữ liệu mẫu logic hiện tại:**
    ```javascript
    // Ví dụ (cần chỉnh sửa theo yêu cầu)
    if (detectionStats.positives >= 3 && detectionStats.positives / detectionStats.total > 0.7) {
      verdict = "PHISHING";
    } else if (detectionStats.positives >= 1 && detectionStats.positives / detectionStats.total > 0.3) {
      verdict = "SUSPICIOUS";
    } else {
      verdict = "SAFE";
    }
    ```

---
### **3. Kích hoạt ⚡️ Workflow**
1. **Test Run với dữ liệu mẫu:**
   - Gửi request POST đến webhook với payload:
     ```json
     {
       "url": "https://example.com"
     }
     ```
   - Kiểm tra kết quả trả về (nên là `SAFE` nếu URL an toàn).
2. **Bật Active:**
   - Nhấn **Active** trên workflow để chạy liên tục.

---
## ✍️ **Mẹo & gợi ý nâng cao**

### **🔄 Kết hợp với Slack/Telegram để cảnh báo ngay**
- **Cách làm:**
  1. Thêm node **Slack** hoặc **Telegram Bot** sau node `Build Phishing Verdict`.
  2. Cấu hình gửi tin nhắn khi `verdict = "PHISHING"` hoặc `verdict = "SUSPICIOUS"`.
  3. **Dữ liệu mẫu:**
     ```json
     {
       "text": `🚨 PHISHING DETECTED: ${url}\nVerdict: ${verdict}\nRisk Score: ${detectionStats.positives}/${detectionStats.total}`
     }
     ```

### **📈 Tự động gửi báo cáo định kỳ**
- **Cách làm:**
  1. Thêm node **n8n-nodes-base.schedule** (nếu dùng phiên bản mới).
  2. Cấu hình chạy hàng ngày (ví dụ: 8h sáng) để tổng hợp log từ Google Sheets.
  3. Gửi báo cáo qua **Email** hoặc **Slack** với dữ liệu:
     - Số lượng URL phishing mới.
     - Top 5 URL nguy hiểm nhất.

### **🔒 Defang URL để ngăn người dùng nhấp vô tình**
- **Cách làm:**
  - Thêm node **Code** sau `Build Phishing Verdict` để defang URL:
    ```javascript
    if (verdict === "PHISHING") {
      defangedUrl = url.replace(/[a-zA-Z0-9]/g, 'x');
      return { ...$inputAll, defangedUrl };
    }
    ```
  - Sau đó, trả về `defangedUrl` thay vì URL gốc trong response.

### **📊 Tạo dashboard theo dõi trên Google Data Studio**
- **Cách làm:**
  1. Kết nối Google Sheets lưu log với **Google Data Studio**.
  2. Tạo biểu đồ:
     - Số lượng URL phishing theo ngày.
     - Phân bố nguy cơ (SAFE/SUSPICIOUS/PHISHING).
  3. Chia sẻ dashboard với team bảo mật.

---
## 📌 **Kết luận**
Workflow này là **giải pháp tự động hóa hoàn chỉnh** để các sếp bảo mật:
✔ **Kiểm tra URL phishing 24/7** mà không cần can thiệp thủ công.
✔ **Lưu log dài hạn** để phân tích xu hướng.
✔ **Cảnh báo ngay** khi phát hiện URL nguy hiểm.
✔ **Tích hợp với Slack/Email** để phản ứng nhanh chóng.

**Hành động ngay:**
1. **Import workflow** và cấu hình VirusTotal + Google Sheets.
2. **Test với URL mẫu** để đảm bảo hoạt động.
3. **Kết nối với Slack/Email** để cảnh báo tự động.
4. **Tạo dashboard** để theo dõi hiệu quả.

**🚀 Bắt đầu tự động hóa bảo mật hôm nay!** Nếu có vấn đề, hãy để lại comment bên dưới. 👇