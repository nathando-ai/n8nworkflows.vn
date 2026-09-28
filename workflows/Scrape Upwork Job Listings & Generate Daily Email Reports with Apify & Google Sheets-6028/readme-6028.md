---
title: "🚀 Tự Động Hóa Scrape Cập Nhật Vị Trí Làm Việc Upwork & Gửi Báo Cáo Email Hàng Ngày Với Apify & Google Sheets"
description: "Workflow tự động hóa scrape tất cả các công việc mới trên Upwork theo danh sách từ khóa, loại bỏ trùng lặp, tổng hợp thống kê và gửi báo cáo email hàng ngày cho đội ngũ. Giúp các sếp tiết kiệm 10+ giờ/tháng và cập nhật thông tin tuyển dụng chính xác 24/7."
slug: "tieu-dong-hoa-scrape-upwork-va-gui-bao-cao-email-hang-ngay"
tags: [n8n, automation, market-research, apify, google-sheets, email-automation]
keywords: [scrape upwork, tự động hóa tìm việc, báo cáo hàng ngày, apify scraper, google sheets automation, email tự động hóa]
---

# 🚀 **Tự Động Hóa Scrape Vị Trí Làm Việc Upwork & Gửi Báo Cáo Email Hàng Ngày**

### **Nỗi Đau Của Các Sếp Khi Tìm Vị Trí Làm Việc Upwork**
Hàng ngày, các sếp phải:
- **Tìm kiếm thủ công** trên Upwork để cập nhật danh sách công việc mới theo từ khóa.
- **Lọc và sao chép** thông tin từ hàng trăm trang kết quả.
- **Loại bỏ trùng lặp** giữa các ngày, gây mất thời gian và sai sót.
- **Gửi báo cáo** cho đội ngũ bằng email, nhưng lại phải làm thủ công mỗi ngày.

**Kết quả?** Thời gian và năng suất bị "chôn vùi" trong công việc lặp đi lặp lại, trong khi thông tin tuyển dụng lại không được cập nhật kịp thời.

### **Workflow Này Giải Quyết Gì?**
Workflow này **tự động hóa toàn bộ quy trình** từ scrape dữ liệu Upwork đến gửi báo cáo email hàng ngày, giúp các sếp:
✅ **Tiết kiệm 10+ giờ/tháng** bằng cách loại bỏ công việc thủ công.
✅ **Cập nhật thông tin chính xác** 24/7, không phụ thuộc vào thời gian làm việc.
✅ **Lọc và tổng hợp dữ liệu** tự động, loại bỏ trùng lặp và dữ liệu cũ.
✅ **Gửi báo cáo email tự động** với thống kê chi tiết, giúp đội ngũ cập nhật nhanh chóng.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không phải tìm kiếm và sao chép dữ liệu mỗi ngày.
- **Dữ liệu sạch và chính xác**: Loại bỏ trùng lặp, chỉ giữ lại thông tin mới nhất.
- **Báo cáo tự động**: Email hàng ngày với thống kê chi tiết, giúp đội ngũ cập nhật nhanh chóng.
- **Hoạt động liên tục**: Workflow chạy 24/7, không phụ thuộc vào giờ làm việc.
- **Tối ưu chi phí**: Giảm thiểu chi phí tuyển dụng bằng cách cập nhật thông tin kịp thời.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
1. **Tài khoản Google Sheets**:
   - Một file Google Sheets với **2 sheet**:
     - `All Keywords`: Danh sách từ khóa cần scrape (mỗi hàng là một từ khóa).
     - `Daily Jobs`: Sheet để lưu trữ công việc mới scrape mỗi ngày.
     - `Summary Sheet`: Sheet để lưu trữ thống kê tổng hợp.
   - **Chia sẻ quyền truy cập** cho n8n với quyền "Sửa" (`googleApi` credentials).

2. **Tài khoản Apify**:
   - Một tài khoản **Apify** để sử dụng scraper Upwork.
   - **API Token** của Apify (để cấu hình `httpHeaderAuth` credentials).

3. **Tài khoản Gmail**:
   - Một tài khoản Gmail để gửi báo cáo email tự động (`gmailOAuth2` credentials).

4. **API Key của Upwork (nếu cần)**:
   - Một số scraper Apify yêu cầu API Key của Upwork. Nếu không có, có thể sử dụng scraper công khai trên Apify.

---
---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/6028) hoặc copy toàn bộ JSON từ trang này.
- Mở **n8n Editor** và chọn **Import Workflow** → Dán JSON hoặc tải file JSON.
- Workflow sẽ được import với tất cả các node và kết nối.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này được chia thành **3 phần chính**: Scrape, Lọc Dữ liệu, và Gửi Báo Cáo. Dưới đây là hướng dẫn chi tiết cho các node quan trọng:

##### **📄 Phần 1: Scrape Dữ Liệu Upwork**
- **Trigger Manual Run**:
  - **Lưu ý**: Workflow được kích hoạt thủ công. Các sếp cần **click vào nút "Run"** mỗi ngày để bắt đầu scrape.

- **Fetch Keywords from Google Sheet**:
  - **Cấu hình**:
    - **Credentials**: Chọn `googleApi` (đã cấu hình trước khi import).
    - **Sheet Name**: Đặt là `All Keywords`.
    - **Range**: Đặt là `A:A` (cột A chứa danh sách từ khóa).

- **Loop Through Keywords**:
  - **Lưu ý**: Node này sẽ **lặp qua từng từ khóa** trong danh sách và gửi yêu cầu scrape cho Apify.

- **Trigger Apify Scraper**:
  - **Cấu hình**:
    - **URL**: Đặt là URL của **Apify Actor** scrape Upwork (ví dụ: `https://api.apify.com/v2/actors/<actor-id>/runs`).
    - **Headers**:
      - `Authorization`: Đặt là `Bearer <API_TOKEN_APIFY>` (thay thế `<API_TOKEN_APIFY>` bằng token của bạn).
      - `Content-Type`: `application/json`.
    - **Body**:
      ```json
      {
        "input": {
          "keywords": "{{$node["Loop Through Keywords"].json["$.currentItem"]}}",
          "maxJobs": 100
        }
      }
      ```
      - `$node["Loop Through Keywords"].json["$.currentItem"]` sẽ tự động thay đổi từ khóa khi lặp.

- **Wait for Apify Completion**:
  - **Cấu hình**:
    - **HTTP Method**: `GET`.
    - **URL**: Đặt là URL của **Apify Run** (cần lấy từ response của node `Trigger Apify Scraper`).
    - **Headers**: Giữ nguyên `Authorization: Bearer <API_TOKEN_APIFY>`.

- **Delay Before Dataset Read**:
  - **Cấu hình**:
    - **Time**: Đặt **10-30 giây** để chắc chắn dữ liệu đã sẵn sàng.

- **Fetch Scraped Job Dataset**:
  - **Cấu hình**:
    - **URL**: Đặt là URL của **Apify Dataset** (cần lấy từ response của node `Wait for Apify Completion`).
    - **Headers**: Giữ nguyên `Authorization: Bearer <API_TOKEN_APIFY>`.

##### **🧹 Phần 2: Lọc và Làm Sạch Dữ Liệu**
- **Process Raw Job Data** (Node Code):
  - **Lưu ý**: Node này **lọc các công việc mới trong 24 giờ** và định dạng dữ liệu.
  - **Mã JavaScript mặc định**:
    ```javascript
    // Lọc công việc mới trong 24 giờ
    const today = new Date();
    today.setHours(0, 0, 0, 0);
    const yesterday = new Date(today);
    yesterday.setDate(today.getDate() - 1);

    const filteredJobs = $input.all().filter(job => {
      const jobDate = new Date(job.postedDate);
      return jobDate >= yesterday;
    });

    return filteredJobs;
    ```
  - **Lưu ý**: Nếu cần thay đổi logic, các sếp có thể chỉnh sửa mã này.

- **Save Jobs to Daily Sheet**:
  - **Cấu hình**:
    - **Credentials**: `googleApi`.
    - **Sheet Name**: `Daily Jobs`.
    - **Range**: `A2` (để dữ liệu bắt đầu từ hàng 2).

- **Update Keyword Job Count**:
  - **Cấu hình**:
    - **Sheet Name**: `All Keywords`.
    - **Range**: `B:A` (cột B sẽ lưu số lượng công việc cho từng từ khóa).

- **Load Today’s Daily Jobs**:
  - **Cấu hình**:
    - **Sheet Name**: `Daily Jobs`.
    - **Range**: `A:Z` (lấy toàn bộ dữ liệu trong sheet).

- **Remove Duplicates by Title/Desc** (Node Code):
  - **Mã JavaScript mặc định**:
    ```javascript
    const seen = new Set();
    const uniqueJobs = $input.all().filter(job => {
      const key = `${job.title}_${job.description}`;
      if (!seen.has(key)) {
        seen.add(key);
        return true;
      }
      return false;
    });
    return uniqueJobs;
    ```
  - **Lưu ý**: Node này loại bỏ trùng lặp dựa trên **tiêu đề và mô tả**.

- **Save Clean Job Data**:
  - **Cấu hình**:
    - **Sheet Name**: `Daily Jobs`.
    - **Range**: `A2` (ghi đè dữ liệu cũ).

##### **📊 Phần 3: Tạo Báo Cáo và Gửi Email**
- **Generate Keyword Summary Stats** (Node Code):
  - **Mã JavaScript mặc định**:
    ```javascript
    const keywordStats = {};
    $input.all().forEach(job => {
      if (job.keyword) {
        keywordStats[job.keyword] = (keywordStats[job.keyword] || 0) + 1;
      }
    });
    return Object.entries(keywordStats).map(([keyword, count]) => ({ keyword, count }));
    ```
  - **Lưu ý**: Node này **tính số lượng công việc cho từng từ khóa**.

- **Update Summary Sheet**:
  - **Cấu hình**:
    - **Sheet Name**: `Summary Sheet`.
    - **Range**: `A2` (ghi đè dữ liệu cũ).

- **Build Email Body** (Node Code):
  - **Mã JavaScript mặc định**:
    ```javascript
    const summaryData = $input.all();
    const sheetLink = "https://docs.google.com/spreadsheets/d/<SPREADSHEET_ID>/edit#gid=0";

    const emailBody = `
    <h2>Báo Cáo Công Việc Upwork Hôm Nay</h2>
    <p>Ngày: ${new Date().toLocaleDateString()}</p>
    <table border="1">
      <tr>
        <th>Từ Khóa</th>
        <th>Số Công Việc</th>
      </tr>
      ${summaryData.map(item => `<tr><td>${item.keyword}</td><td>${item.count}</td></tr>`).join('')}
    </table>
    <p><a href="${sheetLink}">Xem chi tiết trên Google Sheets</a></p>
    `;
    return { html: emailBody };
    ```
  - **Lưu ý**: Thay thế `<SPREADSHEET_ID>` bằng ID của file Google Sheets của bạn.

- **Send Daily Report Email**:
  - **Cấu hình**:
    - **Credentials**: `gmailOAuth2`.
    - **To**: Đặt email của người nhận (ví dụ: `team@company.com`).
    - **Subject**: `Báo Cáo Công Việc Upwork Hôm Nay`.
    - **HTML Body**: Sử dụng output từ node `Build Email Body`.

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Chạy **Manual Trigger** và kiểm tra:
     - Dữ liệu scrape có đúng không?
     - Dữ liệu trên Google Sheets có được cập nhật không?
     - Email có được gửi thành công không?

2. **Bật Active Workflow**:
   - Sau khi test thành công, **bật Active** và đặt lịch chạy hàng ngày (ví dụ: 8h sáng).

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tự Động Hóa Lịch Chạy**:
   - Sử dụng **n8n Cron Trigger** để chạy workflow hàng ngày mà không cần kích hoạt thủ công.

2. **Gửi Báo Cáo Đến Slack/Telegram**:
   - Thay vì email, các sếp có thể **gửi thông báo Slack/Telegram** bằng cách thêm node `slack` hoặc `telegram`.

3. **Lưu Log Dữ Liệu**:
   - Thêm node `googleSheets` để lưu **log hoạt động** (ngày scrape, số lượng công việc, lỗi nếu có).

4. **Cập Nhật Từ Khóa Tự Động**:
   - Sử dụng **Google Forms** để đội ngũ **nộp yêu cầu thêm/loại bỏ từ khóa**, sau đó tự động cập nhật vào `All Keywords`.

5. **Kết Hợp với AI (LLM)**:
   - Sử dụng node `n8n-nodes-base.llm` để **tóm tắt mô tả công việc** hoặc **phân loại công việc** theo ngành nghề.

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc lặp đi lặp lại, đồng thời **cung cấp dữ liệu tuyển dụng chính xác và cập nhật**. Bằng cách tự động hóa scrape Upwork, lọc dữ liệu và gửi báo cáo email hàng ngày, các sếp có thể **quan tâm đến việc tuyển dụng chất lượng hơn** thay vì mất thời gian trong công việc thủ công.

**Hành động ngay hôm nay!**
1. **Import workflow** và cấu hình theo hướng dẫn.
2. **Test và điều chỉnh** nếu cần.
3. **Bật Active** và bắt đầu tự động hóa!

Nếu có bất kỳ câu hỏi hoặc gặp khó khăn, hãy để lại comment bên dưới. Chúc các sếp thành công! 🚀