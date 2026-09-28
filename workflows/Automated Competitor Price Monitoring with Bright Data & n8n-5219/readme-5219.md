---
title: "🚀 **Hệ Thống Theo Dõi Giá Của Thương Hiệu Đối Thủ Tự Động - Bright Data + n8n (Không Cần Code!)""
description: "Workflow tự động hóa theo dõi giá sản phẩm của đối thủ hàng ngày, phát hiện thay đổi và gửi cảnh báo email tự động. Giúp doanh nghiệp cạnh tranh hiệu quả mà không cần viết code."
slug: "thuo-doi-thu-gia-cua-thuong-hieu-doi-thu-tu-dong"
tags: [n8n, automation, no-code, bright-data, google-sheets, gmail, scraping]
keywords: [n8n workflow theo dõi giá, tự động hóa giá đối thủ, bright data n8n, cảnh báo giá thay đổi, google sheets n8n, email tự động n8n]
---

# **🚀 Hệ Thống Theo Dõi Giá Của Thương Hiệu Đối Thủ Tự Động - Bright Data + n8n**

## **🔍 Nỗi Đau Của Doanh Nghiệp Khi Theo Dõi Giá Thương Hiệu Đối Thủ**
Bạn đã bao giờ phải **tốn thời gian thủ công** để tra cứu giá sản phẩm của đối thủ hàng ngày? Hay phải **quên kiểm tra** vì bận rộn, dẫn đến mất cơ hội cạnh tranh? Hoặc phải **chờ đợi email từ nhân viên** mới biết giá đã thay đổi?

**Workflow này giải quyết tất cả!** Nó tự động:
✅ **Scraping** giá từ trang web của đối thủ (thậm chí là những trang có bảo vệ chống bot)
✅ **So sánh** với giá cũ đã lưu trong Google Sheets
✅ **Gửi cảnh báo email tự động** khi có thay đổi
✅ **Lưu lịch sử** để theo dõi xu hướng giá trong thời gian dài

Không cần viết một dòng code nào! Chỉ cần **cài đặt và chạy**, hệ thống sẽ làm tất cả cho bạn.

---
### **🎯 Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không phải thủ công tra cứu giá hàng ngày.
- **Cảnh báo tức thời**: Nhận email ngay khi giá thay đổi (thậm chí là giảm giá).
- **Dữ liệu chính xác**: So sánh tự động với giá cũ để tránh sai sót.
- **Lịch sử đầy đủ**: Google Sheets lưu tất cả lịch sử giá để phân tích.
- **Hoạt động 24/7**: Không cần can thiệp của con người.
:::

---
### **🔧 Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị:
✔ **Tài khoản Bright Data** (để scraping trang web):
   - [Đăng ký Bright Data](https://get.brightdata.com/1tndi4600b25) (mã giảm giá: **N8NBRIGHT** - giảm 10%)
   - **API Key** từ Bright Data (cần để cấu hình trong node `Fetch Page via Bright Data`).

✔ **Tài khoản Google Sheets**:
   - Một **Google Sheet** để lưu trữ giá cũ và mới.
   - **Credentials OAuth2** của Google Sheets (cấu hình trong n8n).

✔ **Tài khoản Gmail**:
   - **Credentials OAuth2** của Gmail (để gửi email cảnh báo).
   - **Địa chỉ email nhận cảnh báo** (cần thiết để test).

✔ **Trang web của đối thủ**:
   - **URL** của trang giá sản phẩm (ví dụ: `https://doithu.com/dich-vu/gia`).
   - **Cấu trúc HTML** của phần giá (cần chỉnh sửa trong node `Format & Isolate Price Block`).
:::

---
## **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
Các sếp có thể **import** workflow từ file JSON hoặc **copy/paste** JSON vào n8n Editor.

#### **Cách Import từ File JSON:**
1. **Tải workflow** từ [n8n.io/workflows/5219](https://n8n.io/workflows/5219).
2. **Nhấn vào "Import"** trong n8n Editor.
3. **Chọn file JSON** và nhấn **Import**.

#### **Cách Copy/Paste JSON:**
1. **Mở n8n Editor** và tạo một workflow mới.
2. **Nhấn vào "Import"** → Chọn **Paste JSON**.
3. **Dán JSON** từ [đây](https://n8n.io/workflows/5219) (hoặc file JSON đã tải).
4. **Nhấn "Import"**.

---
### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**

#### **🔹 Node 1: Check Pricing Every Day (Schedule Trigger)**
- **Thiết lập lịch chạy**:
  - Mặc định là **mỗi ngày** (có thể thay đổi thành **mỗi giờ** nếu cần).
  - **Lưu ý**: Nếu chạy quá thường, Bright Data có thể bị giới hạn. Thường xuyên **mỗi 1-2 giờ** là hợp lý.

#### **🔹 Node 2: Fetch Page via Bright Data (HTTP Request)**
- **Cấu hình Bright Data**:
  - **URL**: Điền **URL đầy đủ** của trang giá đối thủ (ví dụ: `https://doithu.com/dich-vu/gia`).
  - **Headers**:
    - `User-Agent`: `Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/91.0.4472.124 Safari/537.36`
    - `Accept`: `text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8`
  - **API Key**:
    - Điền **API Key** từ Bright Data (tìm trong tài khoản Bright Data → **API Keys**).
  - **Method**: `GET`
  - **Response Format**: `JSON`

#### **🔹 Node 3: Extract HTML Content (HTML)**
- **Operation**: `extractHtmlContent` (không cần chỉnh sửa).

#### **🔹 Node 4: Format & Isolate Price Block (Code)**
- **Lưu ý quan trọng**: Đây là **node code** cần chỉnh sửa để **trích xuất giá** từ HTML.
  - **Mẫu code mặc định** (có thể chỉnh sửa theo cấu trúc HTML của trang đối thủ):
    ```javascript
    // Lấy phần HTML chứa giá (ví dụ: class="price")
    const html = $input.all().html;
    const priceRegex = /<span class="price">(.*?)<\/span>/g;
    const priceMatch = html.match(priceRegex);

    if (priceMatch) {
      return {
        price: priceMatch[0].replace(/<span class="price">|<\/span>/g, ''),
        html: html
      };
    } else {
      return {
        error: "Không tìm thấy giá trong HTML",
        html: html
      };
    }
    ```
  - **Nếu trang đối thủ có cấu trúc khác**, các sếp cần **sử dụng Inspect Tool** (F12) để tìm **class/id** của phần giá, rồi **cập nhật regex** tương ứng.

#### **🔹 Node 5: Read Last Saved Price (Google Sheets)**
- **Chọn Sheet và Tab**:
  - **Google Sheet**: Chọn **file Google Sheets** đã tạo.
  - **Tab**: Chọn **tab** chứa dữ liệu (ví dụ: `Giá Cũ`).
  - **Range**: Điền **A1** (nếu dữ liệu ở ô A1).
- **Credentials**: Chọn **googleSheetsOAuth2Api** (đã cấu hình trước).

#### **🔹 Node 6: Has Price Changed? (If)**
- **Cấu hình so sánh**:
  - **Condition**: `JSON Path` của giá mới (`$.price`) vs giá cũ (`$.json[0].price`).
  - **Operator**: `!=` (khác nhau).
  - **Nếu giá khác nhau**: Workflow tiếp tục đến **Update Stored Price** và **Send Alert Email**.
  - **Nếu giá không thay đổi**: Workflow **dừng lại** (node `No Change Detected – Stop`).

#### **🔹 Node 7: Update Stored Price (Google Sheets)**
- **Chọn Sheet và Tab**:
  - **Google Sheet**: Cùng file như trước.
  - **Tab**: Cùng tab (`Giá Cũ`).
  - **Range**: Điền **A1** (để ghi đè giá cũ).
- **Credentials**: `googleSheetsOAuth2Api`.
- **Operation**: `update` (ghi đè giá mới).

#### **🔹 Node 8: Send Price Change Alert Email (Gmail)**
- **Chọn tài khoản Gmail**:
  - Chọn **gmailOAuth2** đã cấu hình.
- **Địa chỉ nhận email**:
  - Điền **email** của bạn hoặc team (ví dụ: `team@doanhnghiep.com`).
- **Tiêu đề email**:
  - Mẫu: `🚨 GIÁ ĐỐI THỦ ĐÃ THAY ĐỔI: [Tên Sản Phẩm]`.
- **Nội dung email**:
  - **Thêm biến** từ `$json` (ví dụ: `Giá mới: $${$.price}`).
  - **Link trang**: Thêm **URL** của trang giá đối thủ.
  - **Mẫu email**:
    ```html
    <p>🚨 Giá của đối thủ đã thay đổi!</p>
    <p><strong>Trang:</strong> <a href="$url">$url</a></p>
    <p><strong>Giá mới:</strong> $${$.price}</p>
    <p><strong>Thời gian:</strong> $date</p>
    ```

---
### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Nhấn **Run Workflow** để kiểm tra.
   - Kiểm tra **email** và **Google Sheets** xem có nhận được dữ liệu không.
2. **Bật Active**:
   - Sau khi test thành công, **bật Active** để workflow chạy tự động theo lịch.

---
## **✍️ Mẹo & Gợi Ý Nâng Cao**

### **1. Theo Dõi Nhiều Trang Giá**
- **Sử dụng node `Set`** để lưu nhiều URL và chạy vòng lặp.
- **Tạo nhiều workflow** riêng cho từng đối thủ.

### **2. Gửi Cảnh Báo Slack/Telegram**
- Thay thế node **Gmail** bằng **Slack** hoặc **Telegram Bot**.
- **Mẫu Slack**:
  ```json
  {
    "text": "🚨 Giá đối thủ thay đổi: <$url|Xem trang>",
    "attachments": [
      {
        "title": "Giá mới",
        "text": "$${$.price}",
        "color": "#FF0000"
      }
    ]
  }
  ```

### **3. Lưu Log Lịch Sử**
- **Thêm node `Set`** để lưu **tất cả lịch sử** vào Google Sheets.
- **Sử dụng node `Date/Time`** để ghi **ngày giờ** thay đổi.

### **4. Cảnh Báo Giá Giảm (Discount Alert)**
- **Chỉnh node `If`** để chỉ cảnh báo khi giá **giảm** (so sánh `$.price < $.json[0].price`).

### **5. Tự Động Cập Nhật Google Sheets**
- **Sử dụng node `Schedule Trigger`** để **cập nhật dữ liệu định kỳ** (ví dụ: mỗi tháng).

---
## **📌 Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các doanh nghiệp muốn **theo dõi giá đối thủ một cách tự động, chính xác và không cần code**. Bằng cách **cấu hình Bright Data, Google Sheets và Gmail**, các sếp có thể:
✔ **Tiết kiệm thời gian** so với cách thủ công.
✔ **Cảnh báo tức thời** khi giá thay đổi.
✔ **Phân tích xu hướng** từ lịch sử dữ liệu.

**Hãy áp dụng ngay và cạnh tranh hiệu quả hơn!** 🚀

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**🔗 Tài liệu tham khảo:**
- [Bright Data API Docs](https://brightdata.com/docs)
- [n8n Google Sheets Node](https://docs.n8n.io/integrations/builtins/googleSheets/)
- [n8n Gmail Node](https://docs.n8n.io/integrations/builtins/gmail/)