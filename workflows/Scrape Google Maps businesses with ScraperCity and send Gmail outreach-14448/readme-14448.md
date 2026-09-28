---
title: "🚀 Tự Động Hoá Scrape Dữ Liệu Google Maps + Gửi Email Outreach Cho Khách Hàng Tiềm Năng (N8n + ScraperCity)"
description: "Workflow tự động hóa scrape danh sách doanh nghiệp từ Google Maps, tìm kiếm email liên lạc và gửi email outreach cá nhân hóa qua Gmail - tiết kiệm 100% thời gian thủ công cho việc lead generation."
slug: "tieu-dong-hoa-scrape-google-maps-va-email-outreach"
tags: [n8n, automation, lead-generation, scraping, gmail, no-code, business-automation]
keywords: [n8n workflow scrape google maps, tự động hóa tìm kiếm email doanh nghiệp, lead generation tự động, scrape google maps api, email outreach tự động]
---

# 🚀 **Tự Động Hoá Scrape Google Maps + Gửi Email Outreach Cho Khách Hàng Tiềm Năng**

### **Giải pháp hoàn hảo cho các sếp muốn tự động hóa việc tìm kiếm và liên lạc với khách hàng tiềm năng mà không cần code!**

Hãy tưởng tượng: Bạn chỉ cần **nhấp một nút**, workflow sẽ tự động:
✅ **Scrape** danh sách doanh nghiệp từ Google Maps theo ngành nghề và vị trí cụ thể.
✅ **Tìm kiếm email** liên lạc của mỗi doanh nghiệp (thông qua ScraperCity).
✅ **Gửi email outreach cá nhân hóa** qua Gmail cho tất cả khách hàng tiềm năng.

**Kết quả?** Tiết kiệm **hàng giờ/tháng** cho công việc thủ công, tăng **tỷ lệ chuyển đổi** nhờ email cá nhân hóa, và **hoạt động liên tục 24/7** mà không cần can thiệp của bạn!

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo tính bảo mật và hiệu suất cao.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần scrape thủ công trên Google Maps hoặc tìm kiếm email trên LinkedIn/Apollo.
- **Dữ liệu chính xác**: Scrape từ nguồn chính thức (Google Maps) và email được xác thực.
- **Cá nhân hóa cao**: Email outreach được tự động hóa với nội dung tùy chỉnh.
- **Hoạt động liên tục**: Workflow chạy tự động mỗi khi kích hoạt, không phụ thuộc vào thời gian làm việc của bạn.
- **Tăng tỷ lệ chuyển đổi**: Email cá nhân hóa giúp doanh nghiệp của bạn được chú ý hơn.
:::

---

## 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
✔ **Tài khoản ScraperCity** (để scrape Google Maps và tìm kiếm email):
   - [Đăng ký miễn phí tại ScraperCity](https://app.scrapercity.com/)
   - **Lấy API Key** từ Dashboard ScraperCity.
✔ **Tài khoản Gmail** (để gửi email outreach):
   - **OAuth2 Credential** trong n8n (cài đặt trong phần **Credentials** của n8n).
✔ **Tham số search** cho Google Maps:
   - **Business Type** (vd: "Cafe", "Laptop Repair", "Marketing Agency").
   - **Location Query** (vd: "Hà Nội", "Đà Nẵng", hoặc "100m from 'Thanh Xuân District'").
   - **Max Results** (số lượng doanh nghiệp scrape mỗi lần).
   - **Sender Name** (họ tên người gửi email).

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Tải file JSON từ [n8n.io/workflows/14448](https://n8n.io/workflows/14448).
2. Trong **n8n Editor**, nhấn **Import Workflow** và chọn file JSON.
3. **Hoặc** copy toàn bộ JSON và dán vào **Import Workflow** trong n8n.

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**

#### **A. Cấu hình ScraperCity API Key**
- **Các node cần thiết**:
  - `Start Google Maps Scrape`
  - `Poll Maps Scrape Status`
  - `Download Maps Results`
  - `Start Email Finder Scrape`
  - `Poll Email Finder Status`
  - `Download Email Finder Results`

- **Hướng dẫn**:
  1. Trong **Credentials** của n8n, thêm **HTTP Header Auth** với tên `scrapercity-api-key`.
  2. Điền **API Key** từ ScraperCity vào trường `Authorization`.
  3. **Gắn credentials này** vào tất cả các node `httpRequest` liên quan đến ScraperCity.

#### **B. Cấu hình Gmail OAuth2**
- **Node cần thiết**:
  - `Send Outreach Email`

- **Hướng dẫn**:
  1. Trong **Credentials** của n8n, thêm **Gmail OAuth2** với tên `gmailOAuth2`.
  2. Theo hướng dẫn của n8n để **đăng nhập Gmail** và cấp quyền.
  3. **Gắn credentials này** vào node `Send Outreach Email`.

#### **C. Cấu hình tham số search (Configure Search Parameters)**
- **Node**: `Configure Search Parameters` (type: `set`)
- **Tham số cần điền**:
  ```json
  {
    "businessType": "Cafe", // Thay đổi theo ngành nghề mong muốn
    "locationQuery": "Hà Nội", // Vị trí scrape
    "maxResults": 100, // Số lượng doanh nghiệp scrape mỗi lần
    "senderName": "Tên của bạn" // Hiển thị trong email
  }
  ```
- **Lưu ý**: Tham số này sẽ được sử dụng trong toàn bộ workflow.

#### **D. Cấu hình batch size (Batch Businesses for Email Finding)**
- **Node**: `Batch Businesses for Email Finding` (type: `splitInBatches`)
- **Tham số cần chỉnh**:
  - **Batch Size**: Đặt theo **gói dịch vụ ScraperCity** của bạn (vd: 50-100 doanh nghiệp/lần).
  - **Lưu ý**: Nếu batch quá lớn, ScraperCity có thể từ chối hoặc giới hạn API.

#### **E. Tùy chỉnh email outreach (Send Outreach Email)**
- **Node**: `Send Outreach Email` (type: `gmail`)
- **Hướng dẫn**:
  1. Trong **Subject** và **Body**, thay thế nội dung mặc định bằng **template cá nhân hóa** của bạn.
  2. **Dùng biến động态** để hiển thị tên doanh nghiệp và email:
     ```plaintext
     Subject: [{{ $node["Filter Records With Valid Email"].json["email"] }}] - Chào mừng bạn!
     Body:
     Chào {{ $node["Filter Records With Valid Email"].json["businessName"] }},

     Tôi là [Tên của bạn] từ [Tên công ty của bạn]. Tôi thấy doanh nghiệp của bạn rất ấn tượng với [nêu điểm nổi bật].

     Tôi muốn đề xuất [giải pháp/dịch vụ] của chúng tôi có thể giúp [giải quyết vấn đề cụ thể]. Bạn có thể liên hệ với tôi qua email này để thảo luận chi tiết hơn!

     Trân trọng,
     [Tên của bạn]
     [Số điện thoại]
     [Website]
     ```
  3. **Test email** trước khi kích hoạt workflow để đảm bảo nội dung đúng định dạng.

#### **F. Kích hoạt workflow ⚡️**
1. **Test Run** với một batch nhỏ (vd: 5 doanh nghiệp) để kiểm tra:
   - Scrape Google Maps có thành công không?
   - Email được tìm kiếm và gửi đúng không?
   - Có lỗi nào trong log không?
2. Sau khi kiểm tra, **bật Active** workflow.

---

## ✍️ **Mẹo & gợi ý nâng cao**
### **1. Lưu log hoạt động vào Google Sheets**
- **Thêm node**: `n8n-nodes-base.googleSheets`
- **Cách làm**:
  1. Sau node `Send Outreach Email`, thêm **Google Sheets** để ghi log:
     - **Action**: `Create Spreadsheet Row`
     - **Credentials**: OAuth2 của Google Sheets.
     - **Sheet Name**: `Outreach Logs`
     - **Columns**: `Business Name`, `Email`, `Status`, `Sent At`.
  2. **Kết quả**: Bạn có thể theo dõi tất cả email đã gửi và trạng thái của chúng.

### **2. Gửi báo cáo định kỳ qua Slack/Telegram**
- **Thêm node**: `n8n-nodes-base.slack` hoặc `n8n-nodes-base.telegram`
- **Cách làm**:
  1. Sau khi hoàn thành batch, thêm **Slack/Telegram Bot** để thông báo:
     ```json
     {
       "text": `🚀 Batch hoàn thành! Tìm thấy {{ $node["Filter Records With Valid Email"].json.length }} email hợp lệ.`,
       "attachments": [
         {
           "title": "Danh sách email đã gửi",
           "text": `{{ $node["Filter Records With Valid Email"].json | jsonStringify }}`
         }
       ]
     }
     ```
  2. **Kết quả**: Bạn sẽ được thông báo ngay khi workflow hoàn thành.

### **3. Tăng tốc độ scrape bằng cách điều chỉnh thời gian chờ**
- **Node**: `Wait Before First Maps Poll` và `Wait Before First Email Poll`
- **Lưu ý**:
  - Nếu ScraperCity trả về kết quả nhanh, có thể **giảm thời gian chờ** (vd: từ 60s xuống 30s).
  - Nếu gặp lỗi timeout, **tăng thời gian chờ** (vd: 120s).

### **4. Lọc dữ liệu thêm để tăng chất lượng lead**
- **Node**: `Filter Businesses With a Website` và `Filter Records With Valid Email`
- **Cách làm**:
  - Thêm điều kiện lọc thêm, ví dụ:
    - **Chỉ lọc doanh nghiệp có website `.com` hoặc `.vn`**.
    - **Chỉ giữ email có domain `.com` hoặc `.vn`**.
  - **Mã lọc trong Code Node** (nếu cần logic phức tạp):
    ```javascript
    // Ví dụ: Chỉ giữ email có domain `.com` hoặc `.vn`
    $node["Filter Records With Valid Email"].json = $node["Filter Records With Valid Email"].json.filter(item =>
      item.email.includes('.com') || item.email.includes('.vn')
    );
    ```

---

## 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn tự động hóa **lead generation** từ Google Maps đến email outreach, **không cần viết một dòng code**. Bằng cách scrape dữ liệu chính xác từ Google Maps, tìm kiếm email liên lạc và gửi email cá nhân hóa, bạn sẽ **tiết kiệm thời gian, tăng tỷ lệ chuyển đổi** và **hoạt động liên tục** mà không cần can thiệp.

**Hãy thử ngay!**
1. **Import workflow** và cấu hình theo hướng dẫn.
2. **Test với một batch nhỏ** để đảm bảo hoạt động đúng.
3. **Bật Active** và để workflow làm việc tự động cho bạn!

**Nếu có vấn đề**, hãy để lại comment bên dưới hoặc liên hệ với cộng đồng n8n tại [n8n Community](https://community.n8n.io/). Chúc các sếp thành công! 🚀