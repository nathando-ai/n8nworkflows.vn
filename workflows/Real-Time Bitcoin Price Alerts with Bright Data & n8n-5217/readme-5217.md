---
title: "🚀 **Cảnh báo Giá Bitcoin Giảm 5% Thời Thực với Bright Data & n8n (Không Cần Code!)"**
description: "Workflow tự động hóa cảnh báo email khi giá Bitcoin giảm 5% so với giá trước đó, giúp trader và nhà đầu tư không bỏ lỡ cơ hội. Sử dụng Bright Data để lấy dữ liệu thời thực và Google Sheets để lưu trữ lịch sử."
slug: "canh-bao-gia-bitcoin-giam-5-ti-thuc-voi-n8n"
tags: [n8n, automation, crypto, bitcoin, bright-data, google-sheets, email-alert, no-code]
keywords: [n8n workflow bitcoin, tự động hóa cảnh báo giá crypto, cảnh báo giảm giá bitcoin, n8n không cần code, tự động hóa trader crypto]
---

# **🚀 Cảnh Báo Giá Bitcoin Giảm 5% Thời Thực với Bright Data & n8n**

## **🔥 Nỗi Đau Của Trader Bitcoin**
Bạn là một trader crypto, nhà đầu tư hay đơn giản là người quan tâm đến Bitcoin? Thì việc **bỏ lỡ những cơ hội giảm giá lớn** vì phải theo dõi giá liên tục 24/7 là một thách thức lớn. Thậm chí, nhiều trang web cung cấp API chính thức cũng có giới hạn hoặc phí cao.

**Workflow này giải quyết vấn đề đó bằng cách:**
✅ **Lấy giá Bitcoin thời thực** từ bất kỳ trang web nào (không cần API chính thức).
✅ **So sánh với giá trước đó** (lưu trong Google Sheets) để tính toán % giảm.
✅ **Gửi cảnh báo email tự động** khi giá giảm **5% trở lên**, giúp bạn không bỏ lỡ cơ hội.
✅ **Hoạt động 24/7** mà không cần can thiệp thủ công.

---
### **🎯 Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không phải theo dõi giá Bitcoin liên tục.
- **Cảnh báo chính xác**: Chỉ thông báo khi giá giảm **5% trở lên** (thiết lập được điều chỉnh).
- **Lịch sử dữ liệu**: Giá trước đó được lưu trong Google Sheets, giúp phân tích dài hạn.
- **Hoạt động tự động**: Chỉ cần kích hoạt workflow, nó sẽ làm việc cho bạn.
- **Dễ mở rộng**: Có thể kết nối với Slack, Telegram hoặc gửi báo cáo định kỳ.
:::

---
### **🔧 Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
1. **Tài khoản Google** (để sử dụng Google Sheets và Gmail).
2. **API Key Bright Data** (để lấy dữ liệu Bitcoin từ trang web).
   - 👉 [Đăng ký miễn phí Bright Data](https://get.brightdata.com/1tndi4600b25) (tôi sẽ nhận một khoản hoa hồng nhỏ để hỗ trợ tạo nội dung miễn phí).
3. **Google Sheet** để lưu trữ lịch sử giá Bitcoin (cấu trúc đơn giản: 1 cột `Date` và 1 cột `Price`).
4. **Tài khoản Gmail** (để gửi cảnh báo email).
:::

---
## **🚀 Cách Import & Cấu Hình Workflow**

### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
- **Tải file JSON** từ [đây](https://n8n.io/workflows/5217) (n8n.io).
- **Trên n8n Editor**, nhấn `Import` và chọn file JSON.
- **Hoặc**, copy toàn bộ JSON từ [link trên](#) và paste vào `Import` → `Paste JSON`.

:::note[LƯU Ý]
- Nếu import từ file, **không cần chỉnh sửa** phần `credentials` (n8n sẽ tự động liên kết).
- Nếu copy/paste, **cần điền lại `credentials`** sau khi import.
:::

---

### **2. Các Bước Cấu Hình BẮT BUỘC**
Workflow gồm **9 node**, nhưng chỉ có **3 node quan trọng** cần cấu hình kỹ:

#### **🔹 Node 1: Fetch Bitcoin Price (Lấy Giá Bitcoin)**
- **Loại Node**: `httpRequest`
- **Cấu Hình**:
  - **Method**: `POST`
  - **URL**: Sử dụng API của Bright Data để scrape giá Bitcoin từ trang web (ví dụ: [CoinMarketCap](https://coinmarketcap.com/)).
    - **Ví dụ URL**:
      ```
      https://bright-data.com/api/scrape?url=https://coinmarketcap.com/&selector=#price-value
      ```
  - **Headers**:
    ```
    {
      "User-Agent": "Mozilla/5.0",
      "Accept": "text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8"
    }
    ```
  - **Body**:
    ```
    {
      "selector": "#price-value" // Thay đổi selector theo trang web
    }
    ```
  - **Credentials**:
    - Chọn `bright-data` (nếu đã cấu hình API Key Bright Data trong n8n).

#### **🔹 Node 2: Extract Price (Trích Xuất Giá)**
- **Loại Node**: `html`
- **Cấu Hình**:
  - **Operation**: `extractHtmlContent`
  - **Selector**: Điền selector CSS của phần hiển thị giá Bitcoin (ví dụ: `#price-value`).
  - **Result Path**: `$$.json.body.price` (hoặc tùy chỉnh theo cấu trúc trả về của Bright Data).

#### **🔹 Node 3: Get Last Recorded Price (Lấy Giá Trước Đó)**
- **Loại Node**: `googleSheets`
- **Cấu Hình**:
  - **Credentials**: Chọn `googleSheetsOAuth2Api`.
  - **Sheet Name**: Tên của Google Sheet bạn đã tạo.
  - **Range**: `Sheet1!A2` (giả sử dữ liệu từ hàng 2).
  - **Query**: `SELECT * FROM [Sheet Name] WHERE Date IS NOT NULL ORDER BY Date DESC LIMIT 1`.

#### **🔹 Node 4: If droppercentage >= 5 (Kiểm Tra Giá Giảm)**
- **Loại Node**: `if`
- **Cấu Hình**:
  - **Condition**: `{{ $json.droppercentage }} >= 5`
  - **True Path**: Tiếp tục đến `Send Alert Email`.
  - **False Path**: Đi đến `No Alert Needed`.

#### **🔹 Node 5: Send Alert Email (Gửi Cảnh Báo)**
- **Loại Node**: `gmail`
- **Cấu Hình**:
  - **Credentials**: Chọn `gmailOAuth2`.
  - **To**: Địa chỉ email của bạn (hoặc nhóm).
  - **Subject**: `🚨 Bitcoin Giá Giảm 5% Trở Lên! Giá Hiện Tại: {{ $json.currentPrice }}`
  - **Body**:
    ```
    Giá Bitcoin hiện tại: {{ $json.currentPrice }}
    Giá trước đó: {{ $json.previousPrice }}
    % Giảm: {{ $json.droppercentage }}%
    ```
  - **Attachments**: (Tùy chọn) Gửi file Google Sheet hoặc log.

---
### **3. Kích Hoạt Workflow ⚡️**
1. **Test Run**:
   - Nhấn `Run Workflow` và kiểm tra kết quả.
   - Đảm bảo giá được trích xuất đúng và % giảm tính toán chính xác.
2. **Active Workflow**:
   - Sau khi test thành công, chuyển trạng thái sang `Active`.

---
## **✍️ Mẹo & Gợi Ý Nâng Cao**
:::tip[MỞ RỘNG TỐI ĐA]
1. **Chạy Tự Động với Cron Trigger**:
   - Thay thế `Manual Trigger` bằng `Cron Trigger` để workflow chạy định kỳ (ví dụ: mỗi 30 phút).
   - Cấu hình trong `Cron Trigger`:
     ```
     0 */30 * * * * // Chạy mỗi 30 phút
     ```
2. **Gửi Cảnh Báo đến Slack/Telegram**:
   - Thay `gmail` bằng `slack` hoặc `telegramBot` để nhận thông báo nhanh hơn.
3. **Lưu Log vào Google Sheets**:
   - Thêm node `googleSheets` sau `Send Alert Email` để ghi lại lịch sử cảnh báo.
4. **Tính Toán Giá Trung Bình**:
   - Sử dụng node `code` để tính giá trung bình trong 7 ngày và so sánh.
5. **Kết Nối với API CoinGecko**:
   - Thay vì scrape, sử dụng API CoinGecko (miễn phí) để lấy giá chính xác hơn.
:::

---
## **📌 Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho những ai muốn **tự động hóa cảnh báo giá Bitcoin** mà không cần viết code. Với chỉ **vài bước cấu hình**, các sếp có thể:
✔ **Bỏ lỡ không còn cơ hội giảm giá**.
✔ **Tiết kiệm thời gian** theo dõi giá liên tục.
✔ **Mở rộng** để cảnh báo cho nhiều coin khác (Ethereum, Solana...).

**Hãy áp dụng ngay và bắt đầu tự động hóa đầu tư crypto của mình!** 🚀

---
### **🔗 Tài Liệu Tham Khảo**
- [Bright Data API](https://brightdata.com/)
- [n8n Workflow Gốc](https://n8n.io/workflows/5217)
- [Cách Cấu Hình Google Sheets trong n8n](https://docs.n8n.io/integrations/builtins/nodes/googleSheets/)
- [Cách Sử Dụng Cron Trigger](https://docs.n8n.io/integrations/trigger/n8n-nodes-base.cron/)

---
:::info[GỢI Ý HẠ TẦNG]
Để workflow **chạy ổn định 24/7**, các sếp nên cài n8n trên **VPS riêng** (Self-hosted) thay vì dùng phiên bản miễn phí.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**Cảm ơn các sếp đã đọc đến cuối!** Nếu có thắc mắc, hãy để lại bình luận hoặc liên hệ qua [LinkedIn](https://www.linkedin.com/in/yaronbeen/). 😊