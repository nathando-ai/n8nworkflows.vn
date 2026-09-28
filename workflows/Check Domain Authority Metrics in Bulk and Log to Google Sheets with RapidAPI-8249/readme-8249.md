---
title: "🚀 Tự Động Kiểm Tra Domain Authority (DA/PA) Bulk + Lưu Log Google Sheets - SEO & Marketing 24/7"
description: "Giải pháp tự động hóa hoàn toàn không cần code để kiểm tra Domain Authority (DA) và Page Authority (PA) cho hàng loạt domain, sau đó tự động lưu kết quả vào Google Sheets cho phân tích SEO, báo cáo và theo dõi liên tục. Tiết kiệm thời gian lên đến 80% so với cách làm thủ công!"
slug: "tu-dong-kiem-tra-domain-authority-da-pa-bulk-google-sheets"
tags: [n8n, automation, seo, market-research, rapidapi, google-sheets]
keywords: [n8n workflow domain authority, tự động hóa kiểm tra DA PA, lưu log SEO vào Google Sheets, bulk domain authority checker, API RapidAPI cho SEO]
---

# 🚀 **Tự Động Kiểm Tra DA/PA Bulk + Lưu Log Google Sheets - Giải Pháp SEO Cho Các Sếp**

### **Nỗi Đau Của Các Sếp SEO & Marketing**
Các sếp SEO, nhà quản lý nội dung hoặc chuyên gia marketing thường phải **tốn thời gian vô cùng** để:
- **Nhập thủ công** danh sách domain vào các công cụ như Moz, Ahrefs hay SEMrush.
- **Chờ đợi** kết quả DA/PA (Domain Authority và Page Authority) cho từng domain một.
- **Lưu trữ và theo dõi** kết quả trong Excel hoặc Google Sheets một cách rắc rối.
- **Không có báo cáo tự động** để theo dõi xu hướng DA/PA của các domain quan trọng.

**Kết quả?** Thời gian và năng suất bị "chôn vùi" trong công việc thủ công, trong khi các đối thủ đã tự động hóa toàn bộ quy trình!

---
### **🎯 Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian lên đến 80%** so với cách làm thủ công.
- **Kết quả chính xác và đồng bộ** từ API Bulk DA/PA Checker (RapidAPI).
- **Lưu trữ tự động** vào Google Sheets với định dạng sẵn sàng phân tích.
- **Hoạt động 24/7** mà không cần can thiệp của con người.
- **Dễ dàng chia sẻ và báo cáo** với đội ngũ hoặc khách hàng.
:::

---
### **🔧 Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi sử dụng workflow này, các sếp cần chuẩn bị:
1. **Tài khoản Google Sheets** (để lưu kết quả).
2. **API Key của Bulk DA PA Checker** (mua trên [RapidAPI](https://rapidapi.com/skdeveloper/api/bulk-da-pa-checker2)).
3. **Credentials Google API** (cài đặt trong n8n để kết nối với Google Sheets).
4. **VPS hoặc máy chủ n8n** (để workflow hoạt động liên tục).
:::

---
### **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Bước 1:** Tải file JSON của workflow từ [đây](https://n8n.io/workflows/8249) hoặc copy toàn bộ JSON từ trang gốc.
- **Bước 2:** Mở **n8n Editor** và chọn **"Import"** → Dán JSON vào hoặc tải file JSON lên.
- **Bước 3:** Chọn **"Create Workflow"** để lưu vào dự án của mình.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này bao gồm **4 node chính**, các sếp cần cấu hình kỹ lưỡng như sau:

##### **🔹 Node 1: "On form submission" (n8n-nodes-base.formTrigger)**
- **Chức năng:** Hiển thị một **biểu mẫu công khai** cho người dùng nhập danh sách domain (cách nhau bằng dấu phẩy).
- **Lưu ý:**
  - Đảm bảo **URL của form** được chia sẻ với đội ngũ hoặc khách hàng.
  - Ví dụ: `https://tên-dự-án.n8n.cloud/form/your-workflow-id`.

##### **🔹 Node 2: "Check DA PA Bulk" (n8n-nodes-base.httpRequest)**
- **Chức năng:** Gửi yêu cầu POST đến **API Bulk DA/PA Checker** để lấy kết quả DA/PA cho danh sách domain.
- **Cấu hình cần thiết:**
  - **Method:** `POST`
  - **URL:** `https://bulk-da-pa-checker2.p.rapidapi.com/`
  - **Headers:**
    - `x-rapidapi-key`: Điền **API Key** của bạn (mua trên RapidAPI).
    - `x-rapidapi-host`: `bulk-da-pa-checker2.p.rapidapi.com`
  - **Body (JSON):**
    ```json
    {
      "domains": "{{ $node["On form submission"].json["domains"] }}"
    }
    ```
    (Lấy giá trị từ node trước đó, ở đây là `$node["On form submission"].json["domains"]`.)

##### **🔹 Node 3: "Re Format" (n8n-nodes-base.code)**
- **Chức năng:** **Tái định dạng** dữ liệu từ API để chuẩn hóa và tách riêng mỗi domain thành một hàng.
- **Lưu ý:**
  - Mở **Code Editor** và sửa code để đảm bảo dữ liệu được **flatten** (dẹp) thành dạng sẵn sàng lưu vào Google Sheets.
  - Ví dụ code cơ bản:
    ```javascript
    return {
      json: {
        domains: $input.all().map(item => {
          return item.json.data.map(domain => ({
            domain: domain.domain,
            domainAuthority: domain.domainAuthority,
            pageAuthority: domain.pageAuthority,
            // Thêm các trường khác nếu cần
          }));
        }).flat()
      }
    };
    ```
  - **Nếu không chắc chắn**, các sếp có thể **copy code từ workflow gốc** và chỉnh sửa theo cấu trúc dữ liệu của API.

##### **🔹 Node 4: "Append In Google Sheets" (n8n-nodes-base.googleSheets)**
- **Chức năng:** **Thêm dữ liệu** vào Google Sheets với định dạng **append** (thêm hàng mới).
- **Cấu hình cần thiết:**
  - **Credentials:** Chọn `googleApi` (đã cấu hình trước trong n8n).
  - **Spreadsheet ID:** ID của Google Sheet bạn muốn lưu kết quả (tìm trong URL của sheet).
  - **Sheet Name:** Tên tab trong Google Sheet (ví dụ: `DA_PA_Report`).
  - **Operation:** `append` (thêm hàng mới).
  - **Data:** Chọn `$node["Re Format"].json` (dữ liệu đã được định dạng sẵn).

---
### **⚡️ Kích Hoạt Workflow**
1. **Test Run** với dữ liệu mẫu:
   - Nhập vào form công khai (ví dụ: `google.com, facebook.com, n8n.io`).
   - Chạy **manual test** trong n8n để kiểm tra kết quả.
2. **Bật Active:**
   - Đảm bảo tất cả node hoạt động bình thường.
   - Chuyển trạng thái workflow sang **Active**.

---
### **✍️ Mẹo & Gợi Ý Nâng Cao**
:::info[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Gửi báo cáo tự động qua Email/Slack:**
   - Sử dụng **node Email** hoặc **Slack Webhook** để thông báo khi có kết quả mới.
2. **Lưu log lịch sử:**
   - Tạo một **Google Sheet mới** cho mỗi tháng/năm để theo dõi xu hướng DA/PA.
3. **Kết hợp với LLM (AI) để phân tích:**
   - Sử dụng **node LLM** (n8n-nodes-ai) để tự động phân tích và tổng kết kết quả.
4. **Tự động cập nhật định kỳ:**
   - Sử dụng **node Schedule** để chạy workflow hàng tuần/tháng.
5. **Tạo dashboard SEO:**
   - Kết nối với **Google Data Studio** hoặc **Power BI** để tạo báo cáo trực quan.
:::

---
### **📌 Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp SEO, marketing và nhà quản lý nội dung khỏi công việc thủ công mệt mỏi. **Chỉ cần nhập danh sách domain vào form, hệ thống sẽ tự động:**
✅ Lấy DA/PA từ API.
✅ Định dạng và chuẩn hóa dữ liệu.
✅ Lưu vào Google Sheets sẵn sàng phân tích.

**🚀 Hãy tự động hóa ngay hôm nay!**
- **Cài đặt n8n trên VPS** để workflow hoạt động 24/7.
- **Mua API Key** từ RapidAPI (nếu chưa có).
- **Chia sẻ form công khai** với đội ngũ hoặc khách hàng.

**🎁 Đăng ký VPS cho n8n với giảm giá đặc biệt:**
👉 [TinoHost - Mã giảm giá: **VPSN8N**](https://tino.vn/vps-n8n?affid=388) (Giảm tới 39%)
👉 [BNIX - Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)

**Hãy bắt đầu tự động hóa SEO của mình ngay bây giờ!** 🚀