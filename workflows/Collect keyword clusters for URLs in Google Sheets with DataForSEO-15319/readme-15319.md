---
title: "🚀 Tự Động Hóa Nhận Dữ Liệu Cluster Từ Khóa SEO Cho URL Bằng Google Sheets & DataForSEO"
description: "Workflow tự động hóa 100% không code giúp các sếp thu thập top 100 từ khóa tự nhiên (organic keywords) mà website của mình đang xếp hạng trên Google, đồng thời lưu trữ dữ liệu SEO lịch sử chi tiết vào Google Sheets. Giúp tối ưu chiến lược SEO hiệu quả mà không cần viết một dòng code nào."
slug: "tự-dộng-hoa-thu-thap-cluster-tu-khóa-seo"
tags: [n8n, automation, seo, dataforseo, google-sheets, market-research]
keywords: [n8n workflow seo, tự động hóa thu thập từ khóa, dataforseo api, google sheets automation, keyword research automation]
---

# 🚀 **Tự Động Hóa Thu Thập Cluster Từ Khóa SEO Cho URL Bằng Google Sheets & DataForSEO**

### **🔍 Nỗi Đau Của Các Sếp SEO**
Bạn đã bao giờ phải:
- **Tìm kiếm thủ công** top từ khóa mà website của mình đang xếp hạng trên Google?
- **Lặp đi lặp lại** công việc này hàng tuần/mỗi tháng để theo dõi xu hướng?
- **Không có dữ liệu lịch sử** để so sánh hiệu suất SEO qua các thời điểm?
- **Phải sử dụng nhiều công cụ** khác nhau để thu thập và phân tích dữ liệu?

**Workflow này giải quyết tất cả!** Nó tự động hóa toàn bộ quy trình, giúp bạn:
✅ **Thu thập top 100 từ khóa tự nhiên** mà website của bạn đang xếp hạng.
✅ **Lưu trữ dữ liệu SEO lịch sử** vào Google Sheets (theo ngày/tháng).
✅ **Tối ưu chiến lược SEO** dựa trên dữ liệu chính xác và cập nhật.
✅ **Tiết kiệm thời gian** lên đến **90%** so với cách làm thủ công.

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Dữ liệu SEO chính xác**: Thu thập **top 100 từ khóa tự nhiên** mà website của bạn đang xếp hạng, bao gồm:
  - **Vị trí xếp hạng** (ranking position).
  - **Tổng lượng tìm kiếm** (search volume).
  - **Độ khó từ khóa** (keyword difficulty).
  - **Giá CPC** (Cost Per Click).
  - **Độ cạnh tranh** (competition).
  - **Ý định tìm kiếm** (search intent).
- **Lịch sử dữ liệu chi tiết**: Mỗi lần chạy workflow sẽ **tạo một cột mới** trong Google Sheets, giúp bạn so sánh hiệu suất SEO qua các thời điểm.
- **Tự động hóa hoàn toàn**: Không cần can thiệp thủ công, workflow chạy theo **lịch trình tự động** (hoặc kích hoạt thủ công).
- **Tiết kiệm thời gian**: Thay vì mất **giờ đồng hồ** để thu thập dữ liệu, bạn chỉ cần **cài đặt 1 lần** và workflow sẽ làm tất cả.
- **Cá nhân hóa**: Dữ liệu được lưu theo **mỗi URL riêng biệt**, giúp phân tích chi tiết cho từng trang web.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản DataForSEO**:
   - Đăng ký tại [DataForSEO](https://app.dataforseo.com/) và lấy **API Key** từ [API Access](https://app.dataforseo.com/api-access).
   - **Lưu ý**: API Key này sẽ được sử dụng trong workflow để gọi API.

2. **Tài khoản Google**:
   - **Google Sheets**: Để lưu trữ dữ liệu đầu vào (danh sách URL) và đầu ra (dữ liệu từ khóa).
   - **Google OAuth 2.0**: Để kết nối với Google Sheets (cần tạo **credentials** trong n8n).

3. **Google Sheets mẫu**:
   - **Sheet đầu vào (Input)**: Chứa danh sách URL cần phân tích (cấu trúc chi tiết ở phần sau).
   - **Sheet đầu ra (Output)**: Workflow sẽ tự động tạo các sheet mới để lưu dữ liệu lịch sử.

4. **n8n Workflow**:
   - Cài đặt n8n trên **VPS** (khuyến nghị) hoặc sử dụng phiên bản cloud (n8n.io).
   - **Mã giảm giá VPS**: [TinoHost](https://tino.vn/vps-n8n?affid=388) với mã **VPSN8N** (giảm 39%).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải workflow từ n8n.io**:
  - Truy cập [link workflow gốc](https://n8n.io/workflows/15319) và nhấn **"Import"** để tải file JSON.
- **Import vào n8n Editor**:
  - Mở n8n Editor → Nhấn **"Import"** → Chọn file JSON vừa tải → **"Import Workflow"**.
  - **Hoặc** copy toàn bộ JSON từ [đây](https://n8n.io/workflows/15319) và dán vào **"Import Workflow"** trong n8n.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này gồm **15 node** và cần cấu hình cẩn thận các phần sau:

##### **A. Cấu Hình Credentials**
1. **DataForSEO API**:
   - Tạo **credentials mới** trong n8n:
     - **Node**: `Get ranked keywords` (n8n-nodes-dataforseo.dataForSeoLabsApi).
     - **Credentials**: `dataForSeoApi`.
     - **Tham số**:
       - `API Key`: Nhập API Key từ [DataForSEO](https://app.dataforseo.com/api-access).
       - **Lưu ý**: Nếu API Key bị hạn chế, liên hệ DataForSEO để mở rộng giới hạn.

2. **Google Sheets OAuth 2.0**:
   - Tạo **credentials mới** trong n8n:
     - **Node**: `Create sheet`, `Get URLs`, `Append row in sheet`, `Append row in sheet1`.
     - **Credentials**: `googleSheetsOAuth2Api`.
     - **Cách tạo**:
       - Trong n8n, nhấn **"Add"** → **"Google Sheets"** → **"OAuth 2.0"** → Theo hướng dẫn để kết nối tài khoản Google.

##### **B. Cấu Hình Sheet Google**
1. **Sheet đầu vào (Input)**:
   - **Tên sheet**: Bạn tự đặt (ví dụ: `URLs_Input`).
   - **Cấu trúc cột**:
     - **Cột bắt buộc**: `URL` (chứa danh sách URL cần phân tích).
     - **Cột tùy chọn**: `Active` (nếu có, để lọc URL đang hoạt động).
     - **Dữ liệu mẫu**:
       | URL                     | Active |
       |-------------------------|--------|
       | https://example.com/seo | TRUE   |
       | https://example.com/blog | FALSE  |
   - **Lưu ý**: Sheet phải có **cột `URL`** và **cột `Active`** (nếu muốn lọc URL hoạt động).

2. **Sheet đầu ra (Output)**:
   - Workflow sẽ **tự động tạo sheet mới** cho mỗi URL khi chạy.
   - **Tên sheet mặc định**: `Ranked_Keywords_[Date]` (ví dụ: `Ranked_Keywords_2024-05-20`).
   - **Cấu trúc cột tự động**:
     - `Keyword`, `Rank`, `Search Volume`, `Keyword Difficulty`, `CPC`, `Competition`, `Search Intent`, và **cột theo ngày** (ví dụ: `2024-05-20_Rank_1`).

##### **C. Cấu Hình Node Quan Trọng**
1. **Schedule Trigger**:
   - **Thiết lập lịch chạy**:
     - Ví dụ: **"Every day at 8:00 AM"** (hoặc chạy thủ công).
     - **Lưu ý**: Nếu chạy thủ công, bạn có thể kích hoạt bằng **Webhook** hoặc **"Run Now"** trong n8n.

2. **Get URLs**:
   - **Chọn sheet đầu vào**: Sheet chứa danh sách URL (ví dụ: `URLs_Input`).
   - **Chọn range**: `Sheet1!A:B` (nếu sheet có 2 cột: `URL` và `Active`).

3. **Loop Over Items (each URL)**:
   - **Batch size**: Đặt **100** (mặc định) để xử lý từng URL một cách hiệu quả.

4. **Get ranked keywords**:
   - **API Key**: Đã cấu hình trong credentials `dataForSeoApi`.
   - **Tham số mặc định**:
     - `url`: URL từ sheet đầu vào.
     - `country`: `US` (hoặc thay đổi theo nhu cầu).
     - `language`: `en` (tiếng Anh).
     - `limit`: `100` (top 100 từ khóa).

5. **If a new sheet created**:
   - **Điều kiện**: Nếu sheet mới được tạo (ví dụ: `Ranked_Keywords_[Date]`), workflow sẽ **append dữ liệu** vào sheet đó.

6. **Append row in sheet1**:
   - **Chọn sheet đầu ra**: Sheet mới được tạo (ví dụ: `Ranked_Keywords_2024-05-20`).
   - **Format**: Chọn **"JSON"** để dữ liệu được append đúng cấu trúc.

##### **D. Các Node Khác**
- **Normalize URL**: Chuyển đổi URL thành dạng chuẩn (ví dụ: thêm `https://` nếu thiếu).
- **Prepare data for GS**: Chuẩn hóa dữ liệu trước khi append vào Google Sheets.
- **Filter (only active)**: Lọc URL có `Active = TRUE` (nếu sheet đầu vào có cột này).

#### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Nhấn **"Run Workflow"** để thử với **1-2 URL** và kiểm tra kết quả trong Google Sheets.
   - **Kiểm tra**:
     - Sheet đầu ra có được tạo không?
     - Dữ liệu từ khóa có đầy đủ không?

2. **Bật Active**:
   - Sau khi test thành công, nhấn **"Active"** để workflow chạy tự động theo lịch trình.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tự động tạo sheet mới hàng tháng**:
   - Sử dụng **node `Schedule Trigger`** với lịch trình **"Every month on the 1st"** để tạo sheet mới cho mỗi tháng.

2. **Gửi báo cáo định kỳ qua Email/Slack**:
   - **Kết hợp với node `Email`** hoặc **`Slack`** để gửi báo cáo tự động khi workflow chạy.
   - **Ví dụ**:
     - Sau khi append dữ liệu vào sheet, sử dụng node `Email` để gửi link sheet mới cho team.

3. **Lưu log hoạt động**:
   - Sử dụng **node `Set`** hoặc **`Code`** để lưu log vào một sheet riêng (ví dụ: `Workflow_Logs`), bao gồm:
     - Thời gian chạy.
     - Số URL được xử lý.
     - Số từ khóa thu thập được.
     - Lỗi (nếu có).

4. **Tối ưu API Key**:
   - Nếu API Key bị giới hạn, liên hệ **DataForSEO** để mở rộng giới hạn hoặc sử dụng **node `Set`** để chia nhỏ batch size.

5. **Tự động xóa sheet cũ**:
   - Sử dụng **node `Google Sheets`** với **operation = `delete`** để xóa sheet cũ sau 12 tháng (để tránh sheet quá nhiều).

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp SEO muốn:
✔ **Tự động hóa thu thập từ khóa** mà không cần viết code.
✔ **Lưu trữ dữ liệu lịch sử** để theo dõi xu hướng SEO.
✔ **Tiết kiệm thời gian** và tập trung vào chiến lược tối ưu hóa.

**Hành động ngay!**
1. **Cài đặt n8n** trên VPS (khuyến nghị) hoặc sử dụng phiên bản cloud.
2. **Import workflow** và cấu hình credentials.
3. **Chạy test** với 1-2 URL và kiểm tra kết quả.
4. **Bật tự động** và theo dõi dữ liệu SEO của mình mỗi ngày!

**🚀 Hãy bắt đầu tự động hóa SEO của bạn ngay hôm nay!** 🚀

---
**🔗 Tài liệu tham khảo**:
- [DataForSEO API Docs](https://app.dataforseo.com/api-access)
- [Google Sheets API](https://developers.google.com/sheets/api/guides/overview)
- [n8n Workflow Example](https://n8n.io/workflows/15319)