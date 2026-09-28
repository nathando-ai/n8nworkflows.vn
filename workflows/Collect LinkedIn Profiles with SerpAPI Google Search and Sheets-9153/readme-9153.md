---
title: "🔍 **Tự Động Hái LinkedIn Profiles Từ Google Search Sử Dụng SerpAPI & Google Sheets - Lead Generation Siêu Tốc**"
description: "Workflow tự động hóa thu thập hồ sơ LinkedIn của các chuyên gia, nhà lãnh đạo theo từ khóa cụ thể, lưu trữ vào Google Sheets với định dạng chuyên nghiệp - tiết kiệm thời gian lên đến 90% cho công việc tìm kiếm lead."
slug: "tieu-thu-hop-so-linkedin-voi-serpapi-google-search"
tags: [n8n, automation, lead-generation, serpapi, google-sheets, no-code]
keywords: [tự động hóa thu thập lead LinkedIn, serpapi n8n, tự động hóa tìm kiếm hồ sơ chuyên gia, google sheets automation, workflow lead generation]
---

# 🚀 **Tự Động Hái LinkedIn Profiles Từ Google Search - Giải Pháp Lead Generation Siêu Tốc**

### **Nỗi Đau Của Các Sếp Trong Tìm Kiếm Lead**
Bạn đã từng phải:
- **Tìm kiếm thủ công** trên Google hoặc LinkedIn để tìm các chuyên gia, nhà lãnh đạo phù hợp với ngành nghề?
- **Lặp đi lặp lại** cùng một công việc tìm kiếm từ khóa, sao chép thông tin và lưu vào bảng Excel?
- **Mất thời gian** vì kết quả tìm kiếm không chính xác hoặc quá nhiều dữ liệu rác?

**Workflow này giải quyết tất cả!** Với **SerpAPI** và **Google Sheets**, bạn có thể tự động hóa quy trình thu thập hồ sơ LinkedIn theo từ khóa, lưu trữ vào bảng tính và **tích hợp hoàn toàn không cần code**.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow hoạt động 24/7 mà không bị gián đoạn, các sếp nên **self-host n8n** trên VPS chuyên dụng:
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (đảm bảo tốc độ cao cho SerpAPI)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian lên đến 90%** so với cách làm thủ công.
✅ **Tìm kiếm chính xác** theo từ khóa, loại bỏ kết quả không liên quan.
✅ **Lưu trữ tự động** vào Google Sheets với định dạng chuyên nghiệp (Ngày, Hồ sơ, Từ khóa).
✅ **Hoạt động liên tục** 24/7, không cần can thiệp của con người.
✅ **Dễ dàng mở rộng** cho nhiều ngành nghề khác nhau.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản SerpAPI** (đăng ký tại [serpapi.com](https://serpapi.com/)) và **API Key**.
2. **Tài khoản Google Cloud** (để OAuth2 với Google Sheets).
3. **Google Sheet** đã được thiết lập với **3 cột**:
   - **Date** (Ngày thu thập)
   - **Profile** (Hồ sơ LinkedIn)
   - **Keywords** (Từ khóa tìm kiếm)
4. **Form (Google Form hoặc Typeform)** để nhập từ khóa tìm kiếm (nếu sử dụng trigger form).

---
### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/9153](https://n8n.io/workflows/9153).
- **Mở n8n Editor** → Nhấn **Import** → Chọn file JSON vừa tải.
- **Hoặc copy/paste** JSON từ file vào **Import Workflow** trong n8n.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
##### **A. Cấu Hình SerpAPI**
- **Node: SerpAPI Search**
  - Điền **API Key** từ tài khoản SerpAPI vào **Credentials**.
  - **Query Format**: Workflow tự động chuyển đổi từ khóa từ dạng `"elemnt1 element2"` thành `("elemnt1") ("element2")` (theo hướng dẫn trong canvas).
  - **Example Query**:
    ```
    ("Chief Technology Officer") ("Vietnam") site:linkedin.com
    ```
  - **Tham số quan trọng**:
    - `engine`: `google`
    - `q`: Query từ từ khóa người dùng nhập.
    - `hl`: `vi-VN` (để kết quả hiển thị tiếng Việt).

##### **B. Cấu Hình Google Sheets**
- **Node: Append profile in sheet**
  - **Credentials**: Chọn `googleSheetsOAuth2Api` và **đăng nhập tài khoản Google**.
  - **Sheet Name**: Điền tên bảng Google Sheets đã chuẩn bị.
  - **Range**: `Sheet1!A1` (hoặc tùy chỉnh theo cấu trúc của bạn).
  - **Data Format**:
    - `Date`: `{{ $node["Build Page List"].json["$date"] }}` (định dạng ngày hiện tại).
    - `Profile`: `{{ $node["Get Full Name to property of object"].json["profile"] }}`.
    - `Keywords`: `{{ $node["Format Keywords"].json["keywords"] }}`.

##### **C. Cấu Hình Trigger (Form Submission)**
- **Node: On form submission**
  - Nếu sử dụng **Google Form**, kết nối với **Google Sheets** để nhận dữ liệu từ khóa.
  - **Key Parameters**:
    - `operation`: `completion` (để workflow chạy khi form được submit).

##### **D. Node Code (Cần Chỉnh Sửa)**
- **Node: Build Page List**
  - Mở **Code Editor** và chỉnh sửa để đảm bảo query SerpAPI đúng định dạng:
    ```javascript
    // Example: Chuyển đổi từ khóa thành query SerpAPI
    const keywords = $input.all().keywords.split(" ");
    const query = keywords.map(kw => `("${kw}")`).join(" ");
    return [{ json: { query } }];
    ```
- **Node: Get Full Name to property of object**
  - Chỉnh sửa để trích xuất thông tin hồ sơ từ kết quả SerpAPI:
    ```javascript
    // Example: Lấy tên và liên kết LinkedIn từ kết quả
    const profile = $input.item().organic_results[0]?.title || "Không tìm thấy";
    return [{ json: { profile } }];
    ```

#### **3. Kích Hoạt ⚡️**
- **Test Run**:
  - Nhập **từ khóa mẫu** (ví dụ: `"Chief Marketing Officer Vietnam"`).
  - Chạy **Manual Test** để kiểm tra kết quả.
- **Bật Active**:
  - Sau khi kiểm tra thành công, **bật Active** workflow.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tích Hợp Slack/Telegram**
   - Sử dụng **node Slack Webhook** hoặc **Telegram Bot** để thông báo khi thu thập hồ sơ thành công.
   - **Cách làm**:
     - Thêm **node Slack** sau **Append profile in sheet**.
     - Gửi tin nhắn: `📌 Hồ sơ mới được thu thập: {{ $node["Append profile in sheet"].json["profile"] }}`.

2. **Lưu Log Thu thập**
   - Sử dụng **node Set** hoặc **Google Drive** để lưu lịch sử tìm kiếm.
   - **Cách làm**:
     - Thêm **node Google Drive** sau **Append profile in sheet**.
     - Lưu file CSV hoặc JSON với dữ liệu thu thập.

3. **Tự Động Gửi Báo Cáo Định Kỳ**
   - Sử dụng **node Schedule** (n8n Premium) hoặc **Google Calendar** để gửi báo cáo hàng tuần.
   - **Cách làm**:
     - Thêm **node Schedule** chạy hàng tuần.
     - Gửi email báo cáo bằng **node Email** hoặc **node Slack**.

4. **Lọc Kết Quả Theo Địa Phần**
   - Thêm **node Code** để lọc kết quả theo vị trí (ví dụ: `site:linkedin.com/in/vietnam`).
   - **Example**:
     ```javascript
     const filtered = $input.item().organic_results.filter(result =>
       result.url.includes("linkedin.com/in/") && result.title.includes("Vietnam")
     );
     return [{ json: filtered }];
     ```

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc tìm kiếm lead thủ công, đồng thời **cung cấp dữ liệu chính xác và tự động hóa hoàn toàn**. Bắt đầu **tự động hóa lead generation** ngay hôm nay và **tăng hiệu suất bán hàng** của doanh nghiệp!

**Bước đầu tiên**: Đăng ký **SerpAPI** và **Google Sheets**, sau đó import workflow và **chạy thử ngay!** 🚀

---
**🔗 [Xem workflow gốc tại n8n.io](https://n8n.io/workflows/9153)**
**💡 Cần hỗ trợ?** Đăng ký **VPS n8n** tại [TinoHost](https://tino.vn/vps-n8n?affid=388) để chạy 24/7!