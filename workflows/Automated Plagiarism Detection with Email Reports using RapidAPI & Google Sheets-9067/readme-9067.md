---
title: "🚀 Tự Động Hóa Kiểm Tra Plagiarism Bằng Email + Google Sheets (Không Cần Code)"
description: "Workflow tự động hóa kiểm tra plagiarism cho nội dung mới được gửi qua Google Sheets, tự động gửi báo cáo chi tiết qua email và cập nhật trạng thái thành công/thất bại. Giúp tiết kiệm thời gian và đảm bảo chất lượng nội dung 100%."
slug: "tieu-dong-hoa-kiem-tra-plagiarism-google-sheets-email"
tags: [n8n, automation, plagiarism detection, content creation, google-sheets, email-automation]
keywords: [n8n plagiarism checker, tự động hóa kiểm tra trùng lặp, báo cáo plagiarism email, workflow n8n content creation, tự động hóa nội dung không code]
---

# 🚀 **Tự Động Hóa Kiểm Tra Plagiarism Cho Nội Dung Bằng Email + Google Sheets**

## 🔍 **Nỗi Đau Của Các Sếp**
Các sếp trong lĩnh vực **giáo dục, biên tập, marketing nội dung** hay phải chịu những vấn đề sau khi kiểm tra plagiarism thủ công:
- **Tốn thời gian**: Phải copy-paste từng đoạn văn bản vào các công cụ kiểm tra, chờ đợi kết quả và ghi chép lại.
- **Không đồng bộ**: Kết quả kiểm tra không tự động cập nhật vào hệ thống quản lý nội dung (ví dụ: Google Sheets).
- **Không cá nhân hóa**: Báo cáo plagiarism thường là dạng văn bản khô khan, khó đọc và không thể gửi trực tiếp cho người dùng.
- **Không theo dõi được**: Không biết được liệu quá trình kiểm tra có thành công hay thất bại, dẫn đến việc phải kiểm tra lại thủ công.

**Workflow này giải quyết tất cả những vấn đề trên bằng cách:**
✅ **Tự động hóa hoàn toàn** khi có nội dung mới được gửi qua Google Sheets.
✅ **Sử dụng API Plagiarism** để kiểm tra nhanh chóng và chính xác.
✅ **Tạo báo cáo HTML đẹp mắt** và gửi trực tiếp qua email cho người dùng.
✅ **Cập nhật trạng thái** thành công/thất bại trên Google Sheets để theo dõi dễ dàng.
✅ **Gửi cảnh báo đến IT** khi có lỗi xảy ra, giúp giải quyết nhanh chóng.

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động **24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS riêng. Với chi phí thấp nhưng hiệu suất cao, các sếp có thể lựa chọn:
👉 **[VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 **[VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (Đảm bảo tốc độ nhanh, ổn định cho API và email)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần kiểm tra plagiarism thủ công, tự động hóa từ khi có nội dung mới.
- **Báo cáo chuyên nghiệp**: Sử dụng **HTML email** với thiết kế đẹp mắt, bao gồm liên kết đến nguồn trùng lặp và tỷ lệ plagiarism.
- **Quản lý dễ dàng**: Trạng thái "Đã kiểm tra" hoặc "Thất bại" được cập nhật tự động trên Google Sheets.
- **Hỗ trợ IT**: Khi có lỗi, hệ thống sẽ tự động gửi email cảnh báo cho IT để xử lý.
- **Dễ mở rộng**: Có thể kết hợp với **Slack/Telegram** để thông báo kết quả hoặc lưu log vào **Google Drive**.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Google Sheets**:
   - Một **Google Sheet** với cột chứa nội dung cần kiểm tra (ví dụ: `Content`).
   - Cột `Status` để lưu trạng thái "Success" hoặc "Failed".
   - Cột `Report` (tùy chọn) để lưu link báo cáo (nếu muốn).

2. **API Plagiarism**:
   - Một **API Plagiarism** (ví dụ: [RapidAPI](https://rapidapi.com/) hoặc [PlagiarismAPI](https://www.plagiarismapi.com/)) với:
     - **API Key** (để gửi request).
     - **Endpoint** (URL API để gọi).
     - **Headers** (thường bao gồm `Content-Type: application/json` và `x-rapidapi-key`).

3. **SMTP cho Email**:
   - Thông tin **SMTP** để gửi email báo cáo (ví dụ: Gmail, SendGrid, hoặc SMTP của nhà cung cấp hosting).
   - **Tài khoản email** để gửi báo cáo (ví dụ: `no-reply@domain.com`).
   - **Mật khẩu ứng dụng** (nếu sử dụng Gmail, cần tạo mật khẩu ứng dụng tại [My Account Google](https://myaccount.google.com/apppasswords)).

4. **Google API Credentials**:
   - **Google Cloud Project** với API **Google Sheets API** được kích hoạt.
   - **Service Account Key** (JSON) để truy cập Google Sheets.

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### 1. **Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
- **Tải file JSON** từ [n8n.io/workflows/9067](https://n8n.io/workflows/9067) (nếu có quyền).
- **Copy JSON** từ trang trên và dán vào **n8n Editor** (trong tab "Import/Export").
- **Nhấn "Import"** để thêm workflow vào dự án của mình.

#### 2. **Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này gồm **9 node**, các sếp cần cấu hình kỹ các node sau:

##### **A. Trigger - New Row in Google Sheet**
- **Chọn Credentials**: `googleSheetsTriggerOAuth2Api` (đã cấu hình sẵn trong n8n).
- **Chọn Sheet và Tab**:
  - **Google Sheet ID**: Tìm trong URL của Google Sheet (ví dụ: `https://docs.google.com/spreadsheets/d/1AbCdEfGhIjKlMnOpQrStUvWxYz/` → `1AbCdEfGhIjKlMnOpQrStUvWxYz`).
  - **Sheet Name**: Tên của tab trong Google Sheet (ví dụ: `Sheet1`).
  - **Trigger Column**: Cột chứa nội dung cần kiểm tra (ví dụ: `Content`).
  - **Status Column**: Cột lưu trạng thái (ví dụ: `Status`).
  - **Report Column** (tùy chọn): Cột lưu link báo cáo (ví dụ: `Report`).

##### **B. Send Content to Plagiarism API**
- **Method**: `POST`.
- **URL**: Endpoint API của dịch vụ plagiarism (ví dụ: `https://api.plagiarismapi.com/v1/check`).
- **Headers**:
  - `Content-Type: application/json`
  - `x-rapidapi-key`: Điền **API Key** của dịch vụ plagiarism.
  - `x-rapidapi-host`: Điền **Host** của API (thường là tên miền của API).
- **Body**:
  ```json
  {
    "text": "{{$node["Trigger - New Row in Google Sheet"].json["$object"]["Content"]}}"
  }
  ```
  (Lấy nội dung từ cột `Content` trong Google Sheet).

##### **C. Check API Response Success**
- **Condition**: Kiểm tra `json["status"] === "success"` (hoặc tương tự, tùy API).
- Nếu thành công → tiếp tục đến node **Extract Plagiarism Results**.
- Nếu thất bại → chuyển đến node **Send Failure Alert to IT**.

##### **D. Extract Plagiarism Results**
- **Code Node**: Sử dụng JavaScript để extraxt dữ liệu từ API response.
  ```javascript
  // Ví dụ: Lấy mảng kết quả plagiarism
  return {
    json: {
      results: $node["Check API Response Success"].json["data"]["results"]
    }
  };
  ```
  (Các sếp cần điều chỉnh dựa trên cấu trúc response của API).

##### **E. Generate HTML Plagiarism Report**
- **Code Node**: Tạo HTML email với báo cáo plagiarism.
  ```javascript
  // Ví dụ: Tạo HTML báo cáo
  const results = $node["Extract Plagiarism Results"].json["results"];
  let html = `
    <h2>Plagiarism Report</h2>
    <p>Tổng tỷ lệ plagiarism: ${results.plagiarismPercentage}%</p>
    <h3>Nguồn trùng lặp:</h3>
    <ul>
  `;

  results.matches.forEach(match => {
    html += `<li><a href="${match.url}" target="_blank">${match.url}</a>: "${match.text}"</li>`;
  });

  html += `</ul>`;
  return { json: { html: html } };
  ```
  (Các sếp cần điều chỉnh dựa trên cấu trúc dữ liệu của API).

##### **F. Send Report to User via Email**
- **Credentials**: Chọn `smtp` đã cấu hình.
- **From Email**: Điền email gửi (ví dụ: `no-reply@domain.com`).
- **To Email**: Lấy từ cột `Email` trong Google Sheet (nếu có) hoặc điền địa chỉ cố định.
- **Subject**: `Plagiarism Report for Your Submission`.
- **HTML Body**: Sử dụng biến `{{$node["Generate HTML Plagiarism Report"].json["html"]}}`.

##### **G. Mark Status: Success / Failed in Google Sheet**
- **Credentials**: `googleApi`.
- **Sheet ID**: Điền ID của Google Sheet.
- **Range**: `Sheet1!A2` (địa chỉ ô chứa dữ liệu, điều chỉnh theo cấu trúc của sếp).
- **Values**:
  - **Success**:
    ```json
    [
      ["Success"],
      ["https://example.com/report.pdf"] // Link báo cáo (tùy chọn)
    ]
    ```
  - **Failed**:
    ```json
    [
      ["Failed"],
      ["Error: API failed"]
    ]
    ```

##### **H. Send Failure Alert to IT**
- **Credentials**: `smtp`.
- **From Email**: `alert@domain.com`.
- **To Email**: Email của IT (ví dụ: `it-support@domain.com`).
- **Subject**: `Plagiarism Check Failed`.
- **HTML Body**:
  ```html
  <p>Content: {{$node["Trigger - New Row in Google Sheet"].json["$object"]["Content"]}}</p>
  <p>Error: API returned failure.</p>
  ```

---

#### 3. **Kích Hoạt ⚡️**
- **Test Run**:
  - Thêm một dòng mới vào Google Sheet với nội dung mẫu.
  - Kiểm tra email và Google Sheet để xác nhận workflow hoạt động.
- **Bật Active**:
  - Nhấn **Active** trên workflow để bắt đầu tự động hóa.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết hợp với Slack/Telegram**:
   - Thêm node **Slack Webhook** hoặc **Telegram Bot** để thông báo kết quả ngay khi workflow hoàn thành.
   - Ví dụ: Gửi tin nhắn như:
     ```
     🚀 Plagiarism Check Complete!
     Status: {{$node["Mark Status: Success in Google Sheet"].json["status"]}}
     Report: {{$node["Mark Status: Success in Google Sheet"].json["report"]}}
     ```

2. **Lưu Log vào Google Drive**:
   - Sử dụng node **Google Drive** để lưu file báo cáo PDF hoặc log chi tiết.

3. **Gửi Báo Cáo Định Kỳ**:
   - Tạo một workflow riêng để tổng hợp tất cả báo cáo plagiarism trong ngày và gửi báo cáo tổng hợp qua email.

4. **Cập Nhật API Key Bằng Sticky Note**:
   - Sử dụng node **Sticky Note** để lưu API Key và dễ dàng cập nhật khi cần.

5. **Thêm Cột "Priority"**:
   - Nếu nội dung có độ ưu tiên khác nhau, thêm cột `Priority` vào Google Sheet và điều khiển thứ tự xử lý trong workflow.

---

### 📌 **Kết Luận**
Workflow **Tự Động Hóa Kiểm Tra Plagiarism Bằng Email + Google Sheets** là giải pháp **hoàn hảo** cho các sếp cần kiểm tra plagiarism **một cách tự động, nhanh chóng và chuyên nghiệp**. Bằng cách kết hợp **Google Sheets, API Plagiarism và Email Automation**, các sếp không chỉ tiết kiệm thời gian mà còn đảm bảo **chất lượng nội dung** cao hơn.

**Hành động ngay hôm nay!**
1. **Import workflow** vào n8n của mình.
2. **Cấu hình các credentials** (Google Sheets, SMTP, API Plagiarism).
3. **Test với nội dung mẫu** và bắt đầu tự động hóa!
4. **Mở rộng** bằng các tính năng nâng cao như Slack, Google Drive hoặc báo cáo định kỳ.

👉 **[Tải workflow từ n8n.io](https://n8n.io/workflows/9067)** và bắt đầu tự động hóa plagiarism hôm nay! 🚀