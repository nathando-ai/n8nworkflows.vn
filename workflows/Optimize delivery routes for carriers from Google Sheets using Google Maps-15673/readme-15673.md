---
title: "🚚 Tự Động Hóa & Tối Ưu Hóa Con Đường Giao Hàng Cho Doanh Nghiệp Logistics - Sử Dụng Google Sheets & Google Maps API"
description: "Workflow này tự động chuyển đổi địa chỉ giao hàng thành tọa độ địa lý, tối ưu hóa lộ trình giao hàng vòng tròn cho từng xe vận chuyển bằng Google Maps API, giúp doanh nghiệp tiết kiệm thời gian và chi phí vận hành. Kết quả là JSON cấu trúc rõ ràng, dễ tích hợp với hệ thống quản lý giao hàng."
slug: "tieu-uu-hoa-con-duong-giao-hang-google-sheets-google-maps"
tags: [n8n, logistics, automation, google-sheets, google-maps-api, route-optimization, no-code]
keywords: [tự động hóa giao hàng, tối ưu lộ trình vận chuyển, google maps api n8n, quản lý xe vận chuyển, logistics automation, google sheets n8n]
---

# 🚀 **Tối Ưu Hóa Con Đường Giao Hàng Cho Xe Vận Chuyển - Từ Google Sheets Đến Google Maps API**

### **📌 Nỗi Đau Của Doanh Nghiệp Logistics**
Hàng ngày, các doanh nghiệp vận chuyển phải đối mặt với những thách thức như:
- **Tốn thời gian** để nhập liệu và tính toán lộ trình giao hàng thủ công.
- **Không tối ưu hóa** con đường, dẫn đến thời gian giao hàng lâu, chi phí nhiên liệu cao.
- **Không theo dõi được** hiệu suất của từng xe vận chuyển.
- **Không tích hợp** với hệ thống quản lý hiện có (ERP, CRM, hoặc dashboard riêng).

**Workflow này giải quyết tất cả những vấn đề trên bằng cách:**
✅ **Tự động hóa** quá trình chuyển đổi địa chỉ thành tọa độ (geocoding).
✅ **Tối ưu hóa lộ trình** bằng thuật toán Nearest Neighbor + 2-Opt.
✅ **Cung cấp kết quả dưới dạng JSON** dễ tích hợp với bất kỳ hệ thống nào.
✅ **Hoạt động 24/7** khi được tự động hóa trên VPS.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian** lên đến **90%** so với tính toán thủ công.
- **Giảm chi phí nhiên liệu** nhờ lộ trình tối ưu.
- **Cá nhân hóa lộ trình** cho từng xe vận chuyển (carrier).
- **Hoạt động tự động** hàng ngày, không cần can thiệp.
- **Kết quả JSON cấu trúc** dễ tích hợp với hệ thống quản lý giao hàng.
- **Báo cáo hiệu suất** cho từng xe và toàn bộ đội vận chuyển.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Google** và **Google Sheets** với các cột:
   - `Name Carrier` (Tên xe vận chuyển)
   - `Date Delivery` (Ngày giao hàng)
   - `Address` (Địa chỉ giao hàng)
   *(Clone mẫu sheet từ [đây](https://docs.google.com/spreadsheets/d/1iQHlKJOfAI_9OeKaemW21n82IEbMVsvuaQqSLIKw2n8/edit?usp=sharing))*

2. **Google Maps API Key** với hai dịch vụ được kích hoạt:
   - [Places API](https://developers.google.com/maps/documentation/places/web-service/overview)
   - [Routes API](https://developers.google.com/maps/documentation/routes)
   *(Hướng dẫn kích hoạt [tại đây](https://console.developers.google.com/apis/api/mapstools.googleapis.com/overview?project=1063614113399))*

3. **Credentials trong n8n**:
   - `googleSheetsOAuth2Api` (để kết nối với Google Sheets).
   - `httpQueryAuth` (để sử dụng Google Maps API).

4. **Tham số cần thiết**:
   - `documentId` của Google Sheet.
   - `Sheet Name` (tên tab trong sheet).
   - `START_ADDRESS` (địa chỉ kho/nhà máy để bắt đầu lộ trình).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/15673](https://n8n.io/workflows/15673) hoặc copy toàn bộ JSON từ trang này.
- Trong **n8n Editor**, chọn **Import Workflow** và dán JSON vào.
- **Hoặc** tạo workflow mới và sao chép từng node theo thứ tự dưới đây.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow gồm **16 node**, các sếp cần chú ý cấu hình các node sau:

| **Node**                     | **Loại Node**               | **Lưu Ý Cần Thiết**                                                                 |
|------------------------------|-----------------------------|--------------------------------------------------------------------------------------|
| **Get addresses**            | `googleSheets`              | Chọn `documentId` và `sheetName` đúng trong sheet của bạn.                          |
| **Get Lat and Lng**          | `httpRequest`               | Điền `GOOGLE_API_KEY` vào `httpQueryAuth` và cấu hình URL: `https://maps.googleapis.com/maps/api/geocode/json?address={$json["Address"]}&key={$GOOGLE_API_KEY}` |
| **Start address**            | `set`                       | Điền `START_ADDRESS` (ví dụ: `"1600 Amphitheatre Parkway, Mountain View, CA"`).       |
| **Get Lat and Lng of Start address** | `httpRequest` | Cấu hình giống như `Get Lat and Lng` nhưng với `START_ADDRESS`.                     |
| **Delivery Algorithm**       | `code`                      | Không cần chỉnh sửa nếu sử dụng mã mặc định (Nearest Neighbor + 2-Opt).             |
| **Group by Carrier**        | `code`                      | Cung cấp logic nhóm giao hàng theo tên xe vận chuyển.                               |
| **Schedule Trigger**         | `scheduleTrigger`           | Cấu hình chạy hàng ngày (ví dụ: `0 8 * * *` để chạy lúc 8h sáng).                   |

**Mã trong node `Delivery Algorithm` (nếu cần chỉnh sửa):**
```javascript
// Nearest Neighbor + 2-Opt (không cần thay đổi)
const { nearestNeighbor, twoOpt } = require('route-optimization-algorithms');
const optimizedRoute = twoOpt(nearestNeighbor(points));
return { json: { optimizedRoute } };
```

#### **3. Kích Hoạt ⚡️**
- **Test Run** với dữ liệu mẫu:
  - Chọn **Manual Trigger** và nhấn **Execute Workflow**.
  - Kiểm tra kết quả trong **Google Sheets** (cột `Lat` và `Lng` sẽ được cập nhật).
  - Kiểm tra **JSON output** trong node cuối cùng (cấu trúc lộ trình tối ưu).
- **Bật Active** khi đã kiểm tra thành công.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tích Hợp với Slack/Telegram**:
   - Sử dụng node `slack` hoặc `telegramBot` để gửi báo cáo lộ trình tối ưu hàng ngày cho đội vận chuyển.

2. **Lưu Log & Báo Cáo**:
   - Sử dụng node `set` hoặc `googleSheets` để lưu lịch sử lộ trình và hiệu suất của từng xe.

3. **Tự Động Hoá Hàng Ngày**:
   - Cấu hình `scheduleTrigger` chạy vào giờ giao hàng (ví dụ: 6h sáng) để cập nhật lộ trình mới.

4. **Hiển Thị Trên Google Maps**:
   - Tích hợp JSON kết quả vào một **dashboard Google Maps** hoặc ứng dụng web riêng (ví dụ như [n8n Dashboard](https://docs.n8n.io/integrations/builtins/n8n-dashboard/)).

5. **Kết Hợp với ERP/CRM**:
   - Gửi JSON kết quả qua **webhook** để tích hợp với hệ thống quản lý giao hàng hiện có (ví dụ: Shippo, Sendcloud, hoặc ERP nội bộ).

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các doanh nghiệp logistics muốn **tự động hóa và tối ưu hóa lộ trình giao hàng** một cách hiệu quả. Bằng cách kết hợp **Google Sheets** (để quản lý dữ liệu) và **Google Maps API** (để tính toán lộ trình), bạn sẽ:
✔ **Tiết kiệm thời gian** và chi phí vận hành.
✔ **Cải thiện hiệu suất** của đội vận chuyển.
✔ **Tích hợp dễ dàng** với hệ thống hiện có.

**Hãy thử ngay!**
1. Import workflow vào n8n của bạn.
2. Cấu hình các credentials và tham số.
3. Chạy và theo dõi kết quả.

**Nếu có vấn đề**, các sếp có thể liên hệ tác giả Davide Boizza qua [LinkedIn](https://www.linkedin.com/in/davideboizza/) hoặc [YouTube](https://www.youtube.com/@n3witalia) để hỗ trợ!

---
**🚀 Chúc các sếp thành công với việc tự động hóa logistics!** 🚚💨