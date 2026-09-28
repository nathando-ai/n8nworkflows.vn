---
title: "🚀 Tự Động Hóa Kiểm Tra An Toàn APK + Báo Cáo PDF Tự Động Với MobSF, AI & Google Drive"
description: "Giải pháp hoàn toàn tự động hóa kiểm tra an toàn APK bằng MobSF, tổng hợp báo cáo bằng AI, chuyển đổi sang PDF và lưu trữ tự động trên Google Drive - tiết kiệm 100% thời gian kiểm tra thủ công."
slug: "tieu-dong-hoa-kiem-tra-an-toan-apk-va-tao-bao-cao-pdf"
tags: [n8n, automation, security, mobsf, ai, google-drive, pdf, no-code, secop, android-security]
keywords: [tự động hóa kiểm tra an toàn apk, mobsf n8n, báo cáo an toàn app pdf, tự động hóa secop, kiểm tra tracker app, báo cáo an toàn android]
---

# 🚀 **Tự Động Hóa Kiểm Tra An Toàn APK + Báo Cáo PDF Tự Động Với MobSF, AI & Google Drive**

### **Giải pháp hoàn toàn tự động hóa kiểm tra an toàn APK, tổng hợp báo cáo bằng AI và lưu trữ PDF trên Google Drive – không cần viết một dòng code nào!**

:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động 24/7 ổn định, các sếp nên **self-host n8n** trên VPS riêng để đảm bảo bảo mật và hiệu suất tối ưu.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 100% thời gian thủ công**: Không cần kiểm tra từng APK một, workflow tự động xử lý từ upload đến báo cáo PDF.
- **Báo cáo an toàn chuyên nghiệp**: AI tổng hợp kết quả MobSF thành báo cáo HTML sạch sẽ, sau đó chuyển đổi thành PDF dễ đọc.
- **Lưu trữ tự động**: Tất cả báo cáo PDF được lưu trực tiếp vào Google Drive, dễ dàng chia sẻ hoặc truy cập.
- **Phát hiện toàn diện**: Kiểm tra permissions, vulnerabilities, trackers và các vấn đề an toàn khác trong APK.
- **Hoạt động liên tục**: Workflow tự động kích hoạt khi có APK mới được upload vào Google Drive.
:::

---

## 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Google Drive**:
   - Một folder riêng để upload APK (workflow sẽ theo dõi folder này).
   - **Credentials OAuth2** cho Google Drive (cấu hình trong n8n).
2. **MobSF (Mobile Security Framework)**:
   - Cài đặt Docker và chạy MobSF trên cục bộ (cổng 8000).
   - **API Key** của MobSF (để upload và scan APK).
3. **Tài khoản OpenAI** (để sử dụng AI tổng hợp báo cáo HTML).
4. **Tài khoản PDF.co** (để chuyển đổi HTML thành PDF).
5. **API Key** của các dịch vụ trên (OpenAI, PDF.co).

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/12024](https://n8n.io/workflows/12024) hoặc copy toàn bộ JSON từ link trên.
- Mở **n8n Editor**, nhấn **Import Workflow** và dán JSON vào.
- **Lưu workflow** với tên **"APK Security Scanner"** (hoặc tên phù hợp).

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**

#### **🔹 Node 1: Watch APK Uploads (Google Drive Trigger)**
- **Chọn credentials**: `googleDriveOAuth2Api` (đã cấu hình trước).
- **Chọn folder**: Chọn folder Google Drive đã tạo để upload APK.
- **Lưu ý**:
  - Folder phải có **quyền đọc/ghi** cho tài khoản OAuth2.
  - Chỉ kích hoạt khi có file mới (APK) được upload.

#### **🔹 Node 2: Download APK File (Google Drive)**
- **Sử dụng credentials**: `googleDriveOAuth2Api`.
- **File ID**: Auto lấy từ node trước (Watch APK Uploads).
- **Lưu ý**: Đảm bảo file là APK (kích thước > 0MB).

#### **🔹 Node 3 & 4: Upload & Scan APK (HTTP Request)**
- **Node "Upload APK to Analyzer"**:
  - **URL**: `http://localhost:8000/uploadapk` (MobSF cục bộ).
  - **Headers**:
    - `Authorization: Bearer <API_KEY_MOBSF>`
    - `Content-Type: multipart/form-data`
  - **Body**: Chọn `File` từ node Download APK File.
- **Node "Start Security Scan"**:
  - **URL**: `http://localhost:8000/scanapk` (MobSF).
  - **Headers**:
    - `Authorization: Bearer <API_KEY_MOBSF>`
  - **Body**:
    ```json
    {
      "hash": "{{$node["Upload APK to Analyzer"].json()["hash"]}}"
    }
    ```
  - **Lưu ý**: Hash được trả về từ node Upload APK.

#### **🔹 Node 5: Summarize MobSF Report1 (Code)**
- **Mã JavaScript** (copy từ workflow gốc):
  ```javascript
  const jsonData = $input.all();
  const findings = jsonData[0].json.findings || [];

  // Lọc các vấn đề nghiêm trọng
  const criticalFindings = findings.filter(finding =>
    finding.severity === "High" || finding.severity === "Critical"
  );

  // Trả về JSON tóm tắt
  return {
    json: {
      title: "Security Findings Summary",
      findings: criticalFindings.map(f => ({
        module: f.module,
        severity: f.severity,
        description: f.description,
        file: f.file
      }))
    }
  };
  ```
- **Lưu ý**: Đảm bảo JSON input từ MobSF có cấu trúc đúng (trong trường hợp không, cần điều chỉnh mã).

#### **🔹 Node 6: Generate HTML Report (OpenAI)**
- **Model**: Chọn `gpt-4` (hoặc `gpt-3.5-turbo` nếu tiết kiệm chi phí).
- **Prompt**:
  ```plaintext
  Tóm tắt báo cáo an toàn APK từ dữ liệu sau:
  {{$inputItem.json}}

  Yêu cầu:
  1. Đặt tiêu đề: "Báo Cáo Kiểm Tra An Toàn APK - {{$inputItem.json.title}}"
  2. Cấu trúc:
     - Phần 1: Tóm tắt vấn đề (High/Critical)
     - Phần 2: Chi tiết từng vấn đề (module, severity, description)
     - Phần 3: Kiến nghị cải thiện
  3. Sử dụng HTML để định dạng:
     - Tiêu đề: `<h1>...</h1>`
     - Danh sách vấn đề: `<ul><li>...</li></ul>`
     - Màu nền cho severity High/Critical: `<span style="background: #ff4444;">...</span>`
  4. Trả về HTML sạch, không có code ngoài thẻ HTML.
  ```
- **Lưu ý**:
  - Đảm bảo `$inputItem.json` có dữ liệu từ node Summarize MobSF Report1.
  - Nếu OpenAI trả về HTML không sạch, sử dụng node **Clean HTML Output** (node 7) để xử lý.

#### **🔹 Node 7: Clean HTML Output (Code)**
- **Mã JavaScript** (xóa các thẻ không cần thiết):
  ```javascript
  const html = $input.all()[0].json.html;
  const cleanedHtml = html
    .replace(/<pre>/g, "") // Xóa thẻ <pre>
    .replace(/<\/pre>/g, "")
    .replace(/```/g, "")   // Xóa code block
    .trim();

  return { json: { html: cleanedHtml } };
  ```

#### **🔹 Node 8 & 9: Generate & Download PDF (HTTP Request)**
- **Node "Generate PDF"**:
  - **URL**: `https://api.pdf.co/v1/pdf/convert/url` (PDF.co).
  - **Headers**:
    - `x-api-key: <API_KEY_PDF_CO>`
  - **Body**:
    ```json
    {
      "url": "https://pdf.co/doc/generate?data={{$inputItem.json.html}}"
    }
    ```
- **Node "Download Generated PDF"**:
  - **URL**: `https://pdf.co/doc/generate?data={{$inputItem.json.html}}` (hoặc URL trả về từ node trước).
  - **Headers**:
    - `x-api-key: <API_KEY_PDF_CO>`
  - **Lưu ý**: PDF.co sẽ trả về URL download, cần download file.

#### **🔹 Node 10: Upload PDF to Google Drive**
- **Credentials**: `googleDriveOAuth2Api`.
- **File**: Chọn file PDF từ node Download Generated PDF.
- **Folder**: Chọn folder Google Drive để lưu báo cáo (khác với folder upload APK).
- **Tên file**: `APK_<TEN_APK>_Report_<NGAY_LAM>.pdf` (cấu hình tự động bằng Expression).

---

### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Upload một APK mẫu vào folder Google Drive.
   - Chạy workflow và kiểm tra:
     - Báo cáo HTML có được tạo không?
     - PDF có được generate và upload lên Google Drive không?
2. **Bật Active**:
   - Sau khi test thành công, bật **Active** cho workflow.

---

## ✍️ **Mẹo & gợi ý nâng cao**
1. **Tự động chia sẻ báo cáo**:
   - Sử dụng **Google Drive Trigger** để phát hiện khi có PDF mới và gửi thông báo qua **Slack/Telegram** bằng node `httpRequest` hoặc `slack`.
   - **Mã gửi Slack**:
     ```javascript
     const webhookUrl = "https://hooks.slack.com/services/...";
     const payload = {
       text: `📄 Báo cáo an toàn APK mới: <${$inputItem.json.url}|Xem PDF>`
     };
     fetch(webhookUrl, {
       method: "POST",
       body: JSON.stringify(payload),
       headers: { "Content-Type": "application/json" }
     });
     ```

2. **Lưu log hoạt động**:
   - Thêm node **Sticky Note** (`n8n-nodes-base.stickyNote`) để ghi log:
     ```json
     {
       "text": `🔍 Scan APK: {{$inputItem.json.name}} - Kết quả: {{$inputItem.json.status}}`
     }
     ```
   - Lưu vào Google Sheets hoặc database để theo dõi lịch sử.

3. **Tự động xóa APK sau scan**:
   - Thêm node **Google Drive** với `operation: delete` để xóa APK sau khi scan xong (giảm bộ nhớ).

4. **Cập nhật AI prompt**:
   - Nếu báo cáo HTML không đẹp, điều chỉnh **prompt** trong node OpenAI để yêu cầu:
     - Sử dụng **CSS inline** cho màu sắc.
     - Thêm **table of contents** cho báo cáo dài.

5. **Bảo mật API Key**:
   - MASK API Key trong workflow bằng cách:
     - Chỉ lưu trong **n8n Credentials** (không hiển thị trong canvas).
     - Sử dụng biến môi trường (`$n8n.env.API_KEY`) nếu self-host.

---

## 📌 **Kết luận**
### **Tự động hóa kiểm tra an toàn APK là một trong những giải pháp hiệu quả nhất để:**
✅ **Tiết kiệm thời gian** của team DevOps/QA.
✅ **Phát hiện sớm** các lỗ hổng an toàn trong APK.
✅ **Cung cấp báo cáo chuyên nghiệp** cho stakeholder.
✅ **Hoạt động 24/7** mà không cần can thiệp thủ công.

**Hành động ngay!**
1. **Self-host n8n** trên VPS để đảm bảo bảo mật và hiệu suất.
2. **Cấu hình MobSF** và các API Key.
3. **Import workflow** và chạy thử với APK mẫu.
4. **Tích hợp vào pipeline CI/CD** của các sếp để kiểm tra tự động trước khi deploy.

🚀 **Nếu các sếp cần hỗ trợ cài đặt hoặc tối ưu workflow, hãy liên hệ với [WeblineIndia](https://www.weblineindia.com/) – nhà cung cấp giải pháp tự động hóa hàng đầu!**

---
**#n8n #Automation #MobSF #AndroidSecurity #AI #GoogleDrive #PDF #NoCode**