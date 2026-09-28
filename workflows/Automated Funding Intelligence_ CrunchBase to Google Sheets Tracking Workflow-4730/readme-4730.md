---
title: "🚀 Tự Động Hóa Theo Dõi Vốn Đầu Tư Mới Nhất Từ Crunchbase Sang Google Sheets (Không Cần Code)"
description: "Workflow tự động hóa lấy dữ liệu vốn đầu tư mới nhất từ Crunchbase (Fintech, Healthtech,...) và ghi vào Google Sheets để phân tích thị trường, theo dõi đối thủ, hoặc hỗ trợ quyết định đầu tư. Giúp các sếp tiết kiệm 10+ giờ/tháng và có thông tin cập nhật 24/7."
slug: "tieu-dong-ho-tra-crunchbase-sang-google-sheets"
tags: [n8n, automation, no-code, marketing, startup, crunchbase, google-sheets]
keywords: [tự động hóa crunchbase, theo dõi vốn đầu tư, google sheets tự động, n8n workflow, phân tích thị trường startup]
---

# 🚀 **Tự Động Hóa Theo Dõi Vốn Đầu Tư Từ Crunchbase Sang Google Sheets (Không Cần Code)**

## **🔥 Nỗi Đau Của Các Sếp Và Giải Pháp Tự Động Hóa**
Hiện nay, việc theo dõi vốn đầu tư mới nhất của các startup trong ngành **Fintech, Healthtech, hoặc các lĩnh vực hot khác** là một công việc tốn thời gian và dễ bị bỏ lỡ. Các sếp thường phải:
- **Tra cứu thủ công** trên Crunchbase hàng ngày, mất từ **30 phút đến 2 giờ/tuần**.
- **Bị bỏ lỡ thông tin** vì không cập nhật thường xuyên.
- **Không có dữ liệu hệ thống** để phân tích xu hướng thị trường hoặc so sánh đối thủ.
- **Phải ghi chép lại** dữ liệu vào Google Sheets hoặc Excel, dễ xảy ra lỗi.

**Workflow này giải quyết tất cả vấn đề trên bằng cách:**
✅ **Tự động lấy dữ liệu** từ Crunchbase mỗi ngày (hoặc theo lịch bạn chọn).
✅ **Lọc và định dạng** thông tin quan trọng (tên công ty, vòng đầu tư, số tiền, nhà đầu tư, ngày công bố).
✅ **Ghi tự động vào Google Sheets** để bạn có thể **tạo báo cáo, phân tích, hoặc chia sẻ** với đội ngũ.
✅ **Hoạt động 24/7** mà không cần can thiệp của con người.

---
### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ/tháng** so với cách làm thủ công.
- **Dữ liệu chính xác và cập nhật** mỗi ngày, không bị bỏ lỡ.
- **Tạo cơ sở dữ liệu đầu tư** để phân tích xu hướng, theo dõi đối thủ, hoặc hỗ trợ quyết định đầu tư.
- **Chia sẻ dễ dàng** với đội ngũ hoặc đối tác thông qua Google Sheets.
- **Không cần kỹ năng code** – chỉ cần drag-and-drop trong n8n.
:::

---
### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Crunchbase** (đăng ký miễn phí tại [crunchbase.com](https://www.crunchbase.com/)).
2. **API Key của Crunchbase** (đăng ký tại [Crunchbase Developer Portal](https://developer.crunchbase.com/)).
3. **Tài khoản Google** và **Google Sheets** đã sẵn sàng để lưu dữ liệu.
4. **n8n Self-hosted** (để workflow chạy 24/7) hoặc n8n Cloud (nếu chỉ muốn test).
:::

---
## **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. **Tải workflow** từ [n8n.io/workflows/4730](https://n8n.io/workflows/4730) (chọn "Download JSON").
2. **Mở n8n Editor** và nhấn **"Import"** → Chọn file JSON vừa tải.
3. **Xác nhận import** và workflow sẽ xuất hiện trên canvas.

#### **Phương pháp 2: Copy/Paste JSON**
1. **Mở n8n Editor** và nhấn **"Create New Workflow"**.
2. **Nhấn "Import"** → Chọn **"Paste JSON"** và dán nội dung JSON từ workflow gốc.
3. **Xác nhận** và workflow sẽ được tạo.

---
### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này gồm **4 node chính**, các sếp cần cấu hình kỹ lưỡng như sau:

#### **🕒 Node 1: Daily Check for New Funding Rounds (Schedule Trigger)**
- **Cấu hình:**
  - **Schedule:** Chọn **"Daily"** (hoặc **"Weekdays"** nếu muốn chạy từ thứ 2 đến thứ 6).
  - **Time:** Đặt thời gian phù hợp (ví dụ: **8h sáng** để bắt đầu ngày mới).
  - **Time Zone:** Chọn **UTC+7** (hoặc khu vực của bạn).
- **Lưu ý:**
  - Nếu muốn chạy **mỗi giờ**, thay đổi thành `"0 * * * *"` (cú pháp Cron).
  - **Không cần code** – chỉ cần chọn thời gian trong UI.

#### **🌐 Node 2: Fetch Crunchbase Funding Rounds (HTTP Request)**
- **Cấu hình:**
  - **Method:** Chọn **"GET"**.
  - **URL:** Sử dụng endpoint Crunchbase:
    ```
    https://api.crunchbase.com/api/v4/organizations?location_country=US&industry=Fintech&sort_by=created_at&sort_order=desc
    ```
    *(Thay đổi `location_country` và `industry` theo nhu cầu, ví dụ: `Healthtech`, `Vietnam`)*
  - **Headers:**
    - Key: `X-cb-user-key`
    - Value: **API Key của bạn** (đăng ký tại [Crunchbase Developer](https://developer.crunchbase.com/)).
  - **Query Parameters (lọc dữ liệu):**
    - `location_country`: Nước bạn quan tâm (ví dụ: `US`, `VN`).
    - `industry`: Ngành nghề (ví dụ: `Fintech`, `Healthtech`, `EdTech`).
    - `funding_round_type`: Loại vòng đầu tư (ví dụ: `seed`, `series_a`).
    - `limit`: Số lượng kết quả trả về (ví dụ: `50`).
- **Lưu ý:**
  - Nếu **API Key không hoạt động**, kiểm tra lại tại [Crunchbase Developer](https://developer.crunchbase.com/).
  - **Test request** trước khi kết nối với node tiếp theo.

#### **🧮 Node 3: Extract & Format Funding Data (Code)**
- **Cấu hình:**
  - **Script JavaScript:** Sử dụng mã gốc từ workflow (không cần chỉnh sửa nếu muốn giữ nguyên).
  ```javascript
  // Mã gốc từ workflow (không cần thay đổi)
  return {
    json: {
      company_name: $input.all()[0].data.company_name,
      industry: $input.all()[0].data.industry,
      funding_round_type: $input.all()[0].data.funding_round_type,
      announced_date: $input.all()[0].data.announced_date,
      money_raised_usd: $input.all()[0].data.money_raised_usd,
      investors: $input.all()[0].data.investors.map(investor => investor.name).join(', '),
      crunchbase_url: `https://www.crunchbase.com/organization/${$input.all()[0].data.id}`
    }
  };
  ```
  - **Nếu muốn thêm trường dữ liệu khác**, mở node này và chỉnh sửa script.
- **Lưu ý:**
  - **Không cần hiểu code** – chỉ cần copy/paste.
  - Nếu muốn **thêm trường mới**, tham khảo cấu trúc JSON trả về từ Crunchbase.

#### **📄 Node 4: Log to Google Sheets (Google Sheets)**
- **Cấu hình:**
  - **Credentials:** Chọn **"googleSheetsOAuth2Api"** (nếu chưa có, tạo mới trong n8n).
  - **Operation:** Chọn **"Append"** (ghi thêm dữ liệu vào cuối sheet).
  - **Spreadsheet:** Chọn **Google Sheets** của bạn.
  - **Sheet:** Chọn **tab** muốn ghi dữ liệu (ví dụ: `Funding_Rounds`).
  - **Headers:** Chọn **"Use first row as headers"** (nếu sheet mới).
  - **Data:** Chọn **"JSON"** (do node Code đã định dạng).
- **Lưu ý:**
  - **Kiểm tra tên tab** trong Google Sheets để tránh ghi sai.
  - **Test run** trước khi bật workflow để đảm bảo dữ liệu ghi đúng.

---
### **3. Kích Hoạt ⚡️ Workflow**
1. **Test Run:**
   - Nhấn **"Run Workflow"** để kiểm tra dữ liệu có ghi vào Google Sheets không.
   - Kiểm tra **Google Sheets** để xác nhận dữ liệu đã được ghi.
2. **Bật Workflow:**
   - Nhấn **"Active"** (đèn chuyển từ **đỏ sang xanh**).
   - Workflow sẽ chạy tự động theo lịch đã đặt.

---
## **✍️ Mẹo & Gợi Ý Nâng Cao**
:::info[CÁC TỐC ĐỘNG THÊM]
- **Gửi thông báo Slack/Telegram khi có dữ liệu mới:**
  - Thêm **node Slack/Telegram Webhook** sau node **Google Sheets**.
  - Cấu hình gửi tin nhắn khi có **vòng đầu tư mới** (ví dụ: `"New funding round detected: [Company Name] raised $XM"`).
- **Lưu log vào Google Drive:**
  - Thêm **node Google Drive** để lưu file CSV/Excel của dữ liệu hàng ngày.
- **Tạo báo cáo tự động:**
  - Sử dụng **Google Apps Script** để tạo **báo cáo PDF** từ Google Sheets và gửi qua email.
- **Lọc dữ liệu theo ngưỡng tiền:**
  - Trong node **Code**, thêm điều kiện lọc chỉ giữ **vòng đầu tư trên $1M**.
  ```javascript
  if ($input.all()[0].data.money_raised_usd > 1000000) {
    return { json: { /* ... */ } };
  } else {
    return { json: null }; // Bỏ qua vòng đầu tư nhỏ
  }
  ```
- **Dùng n8n Cloud (miễn phí 1000 credit/tháng):**
  - Nếu không muốn self-host, có thể dùng **n8n Cloud** (tạm thời) để test.
  - [Đăng ký n8n Cloud](https://n8n.io/cloud/).
:::

---
## **📌 Kết Luận: Hãy Tự Động Hóa Ngay!**
Workflow này giúp các sếp:
✔ **Tiết kiệm thời gian** để tập trung vào chiến lược đầu tư.
✔ **Có dữ liệu chính xác** để phân tích thị trường.
✔ **Theo dõi đối thủ** một cách hiệu quả.
✔ **Không cần code** – chỉ cần drag-and-drop trong n8n.

**Bước đầu tiên:**
1. **Cài n8n trên VPS** (để workflow chạy 24/7).
   👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%).
   👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172).
2. **Import workflow** và cấu hình theo hướng dẫn.
3. **Bật workflow** và bắt đầu theo dõi vốn đầu tư tự động!

**🚀 Hành động ngay!** Dữ liệu là sức mạnh – hãy tự động hóa nó để có quyết định thông minh hơn!

---
:::note[Liên Hệ Nếu Có Thắc Mắc]
Nếu các sếp gặp khó khăn trong quá trình setup, có thể liên hệ với tác giả:
- **Yaron Been** (Tác giả workflow):
  - [LinkedIn](https://www.linkedin.com/in/yaronbeen/)
  - [YouTube](https://www.youtube.com/@YaronBeen/videos)
- **Hỗ trợ n8n Việt Nam:**
  - [Cộng đồng n8n Việt Nam](https://vi.n8n.io/) (Facebook Group).
  - [Diễn đàn tự động hóa](https://automation.vn/).
:::

---
**💡 Chúc các sếp thành công với workflow tự động hóa này!** 🚀