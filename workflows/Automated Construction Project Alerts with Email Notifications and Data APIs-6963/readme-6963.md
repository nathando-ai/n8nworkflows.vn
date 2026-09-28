---
title: "🚀 Tự Động Hóa Thông Báo Dự Án Xây Dựng với Email Cảnh Báo & API Dữ Liệu - Giúp Các Sếp Theo Dõi Dự Án Mới Mà Không Cần Code"
description: "Workflow tự động hóa nhận email yêu cầu thông tin dự án xây dựng, tra cứu dữ liệu chính phủ và cơ sở dữ liệu công nghiệp, sau đó gửi báo cáo chi tiết qua email. Giúp các sếp tiết kiệm thời gian theo dõi dự án mới, giảm thiểu rủi ro bỏ lỡ cơ hội đầu tư hoặc hợp tác."
slug: "tieu-dong-hoa-thong-bao-du-an-xay-dung"
tags: [n8n, automation, market-research, email-notification, api-integration]
keywords: [tự động hóa n8n, cảnh báo dự án xây dựng, tra cứu API dữ liệu chính phủ, email tự động, công cụ nghiên cứu thị trường]
---

# 🚀 **Tự Động Hóa Thông Báo Dự Án Xây Dựng: Giúp Các Sếp Theo Dõi Dự Án Mới Mà Không Cần Code**

### **Nỗi Đau Của Các Sếp Trong Nghiên Cứu Dự Án Xây Dựng**
Các sếp trong lĩnh vực bất động sản, đầu tư hoặc quản lý dự án thường phải mất nhiều thời gian để:
- **Tra cứu thủ công** thông tin về dự án xây dựng mới từ các nguồn dữ liệu chính phủ, cơ quan quản lý hoặc cơ sở dữ liệu công nghiệp.
- **Bỏ lỡ cơ hội** vì không nhận được thông báo kịp thời khi có dự án mới phù hợp với nhu cầu của mình.
- **Tốn công sức** để tổng hợp và phân tích dữ liệu từ nhiều nguồn khác nhau, dẫn đến sai sót hoặc mất thời gian.

Workflow này **giải quyết tất cả những vấn đề trên** bằng cách tự động hóa toàn bộ quy trình từ nhận yêu cầu đến gửi báo cáo chi tiết qua email, **không cần viết một dòng code nào!**

---
### **🎯 Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần tra cứu thủ công trên nhiều trang web hoặc cơ sở dữ liệu.
- **Tính chính xác cao**: Dữ liệu được lấy từ API chính thức của chính phủ và cơ sở dữ liệu uy tín.
- **Cảnh báo kịp thời**: Nhận email báo cáo ngay khi có dự án mới phù hợp với yêu cầu.
- **Hoạt động liên tục**: Dùng **Schedule Trigger** để chạy tự động hàng ngày (thời gian mặc định: 9h sáng, thứ 2 đến thứ 6).
- **Cá nhân hóa**: Báo cáo được tạo động với thông tin chi tiết về dự án, giúp các sếp đưa ra quyết định nhanh chóng.
:::

---
### **🔧 Yêu Cầu Cần Thiết**
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản email IMAP** (để nhận yêu cầu từ khách hàng hoặc đồng nghiệp):
   - Thông tin IMAP (Server, Port, Username, Password, SSL/TLS).
   - **Lưu ý**: Email này phải **không bị spam** và có thể nhận email từ bên ngoài (ví dụ: Gmail, Outlook, Yahoo).
2. **Tài khoản SMTP** (để gửi email báo cáo):
   - Thông tin SMTP (Server, Port, Username, Password, SSL/TLS).
   - **Lưu ý**: SMTP phải hỗ trợ gửi email từ bên ngoài (ví dụ: Gmail SMTP, SMTP của nhà cung cấp hosting).
3. **API Key cho truy cập dữ liệu chính phủ** (nếu cần):
   - Một số cơ quan chính phủ yêu cầu API key để truy cập dữ liệu (ví dụ: API của Bộ Xây Dựng Việt Nam, API của các thành phố lớn).
   - **Nếu không có API key**, workflow vẫn có thể hoạt động với các nguồn dữ liệu công khai khác (ví dụ: Google Search API, Scraper API).
4. **Dữ liệu mẫu** (để test workflow):
   - Một email mẫu với chủ đề **"Construction Alert Request"** và nội dung chứa thông tin vị trí (ví dụ: *"Tôi muốn biết các dự án xây dựng mới ở quận Tân Bình, TP.HCM"*).

---
### **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. **Tải workflow** từ [đây](https://n8n.io/workflows/6963) (nếu có link JSON).
2. **Trên n8n Editor**:
   - Nhấn **Import** → Chọn file JSON hoặc **Paste JSON**.
   - **Hoặc**:
     - Copy toàn bộ JSON từ [n8n.io/workflows/6963](https://n8n.io/workflows/6963) (ấn **Export** trên canvas).
     - Dán vào **Import** → **Paste JSON**.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này gồm **12 node** quan trọng, các sếp cần cấu hình kỹ lưỡng như sau:

##### **A. Cấu Hình Email Trigger (n8n-nodes-base.emailReadImap)**
- **Credentials**:
  - Chọn **IMAP** đã thiết lập trước (nếu chưa có, thêm mới trong **Credentials** → **Add Credential** → **IMAP**).
  - Điền thông tin:
    - **Server**: `imap.gmail.com` (nếu dùng Gmail) hoặc `imap.yourdomain.com` (nếu dùng SMTP khác).
    - **Port**: `993` (SSL) hoặc `143` (TLS).
    - **Username/Password**: Tài khoản email IMAP.
    - **SSL/TLS**: Chọn **SSL** (nếu dùng port 993).
- **Filter**:
  - Trong node **Email Trigger**, thêm **Filter** để chỉ lấy email có chủ đề chứa **"Construction Alert Request"** (ví dụ: `subject*Construction Alert Request*`).

##### **B. Cấu Hình Search Government Data (n8n-nodes-base.httpRequest)**
- **Credentials**:
  - Chọn **HTTP Query Auth** (nếu yêu cầu API key).
  - Nếu không cần API key, bỏ qua bước này.
- **URL & Query**:
  - Thay thế URL mẫu bằng API chính thức của cơ quan quản lý dự án (ví dụ:
    - API của **Bộ Xây Dựng Việt Nam**: `https://data.gov.vn/api/v1/projects?location={location}`
    - API của **Sở Xây Dựng TP.HCM**: `https://sxdt.tphcm.gov.vn/api/projects?zip={zip_code}`
  - **Tham số động**: Sử dụng `$json["location"]` (được lấy từ node **Extract Location Info**).
  - **Headers**:
    - `Content-Type: application/json`
    - `Authorization: Bearer {API_KEY}` (nếu cần).

##### **C. Cấu Hình Search Construction Sites (n8n-nodes-base.httpRequest)**
- **URL & Query**:
  - Thay thế bằng API của cơ sở dữ liệu công nghiệp (ví dụ:
    - **API của Công ty Dự Án ABC**: `https://api.abcconstruction.com/search?city={city}&state={state}`
    - **Google Search API** (nếu không có API riêng):
      ```json
      {
        "q": "$json['location'] + 'construction projects'",
        "cx": "YOUR_CX_ID" // ID của Google Custom Search Engine
      }
      ```
- **Headers**:
  - `Content-Type: application/json`
  - `API Key`: Nếu cần, thêm vào headers.

##### **D. Cấu Hình Email Send (n8n-nodes-base.emailSend)**
- **Credentials**:
  - Chọn **SMTP** đã thiết lập trước (nếu chưa có, thêm mới trong **Credentials** → **SMTP**).
  - Điền thông tin:
    - **Server**: `smtp.gmail.com` (nếu dùng Gmail) hoặc `smtp.yourdomain.com`.
    - **Port**: `587` (TLS) hoặc `465` (SSL).
    - **Username/Password**: Tài khoản SMTP.
    - **SSL/TLS**: Chọn **TLS** (nếu dùng port 587).
- **Thông tin email**:
  - **From**: Địa chỉ email gửi (ví dụ: `no-reply@dothi.vn`).
  - **To**: `$json["email"]` (được lấy từ email yêu cầu).
  - **Subject**:
    - Nếu có kết quả: `"Báo cáo dự án xây dựng mới tại {location}"`.
    - Nếu không có kết quả: `"Không tìm thấy dự án tại {location}"`.

##### **E. Cấu Hình Schedule Trigger (n8n-nodes-base.scheduleTrigger)**
- **Thiết lập lịch chạy**:
  - **Cron Expression**: `0 9 * * 1-5` (chạy hàng ngày lúc 9h sáng, từ thứ 2 đến thứ 6).
  - **Time Zone**: Chọn múi giờ phù hợp (ví dụ: `Asia/Ho_Chi_Minh`).
- **Lưu ý**:
  - Nếu muốn chạy thường xuyên hơn, thay đổi cron expression (ví dụ: `0 9 * * 1-7` để chạy cả chủ nhật).

##### **F. Cấu Hình Node Code (n8n-nodes-base.code)**
Các node **Extract Location Info**, **Process Construction Data**, và **Generate Email Report** sử dụng **JavaScript**. Các sếp có thể chỉnh sửa code như sau:

1. **Extract Location Info**:
   ```javascript
   // Lấy thông tin vị trí từ email body
   const body = $input.all()[0].json.body;
   const locationRegex = /(quận|phường|tỉnh|thành phố|địa chỉ)\s*(.+?)(,|$)/gi;
   const locationInfo = {
     area: null,
     city: null,
     state: null,
     zip: null
   };

   let match;
   while ((match = locationRegex.exec(body)) !== null) {
     const key = match[1].toLowerCase();
     const value = match[2].trim();

     if (key.includes("quận") || key.includes("phường")) locationInfo.area = value;
     else if (key.includes("tỉnh") || key.includes("thành phố")) locationInfo.city = value;
     else if (key.includes("địa chỉ")) {
       // Xử lý mã zip (nếu có)
       const zipMatch = value.match(/\d{5}/);
       if (zipMatch) locationInfo.zip = zipMatch[0];
     }
   }

   return { json: { locationInfo } };
   ```

2. **Process Construction Data**:
   ```javascript
   // Gộp và loại bỏ dữ liệu trùng lặp
   const data1 = $input.all()[0].json; // Dữ liệu từ API chính phủ
   const data2 = $input.all()[1].json; // Dữ liệu từ API công nghiệp

   const combinedData = [...data1, ...data2];
   const uniqueData = combinedData.filter((item, index, self) =>
     index === self.findIndex((t) => (
       t.name === item.name &&
       t.location === item.location
     ))
   );

   return { json: uniqueData };
   ```

3. **Generate Email Report**:
   ```javascript
   // Tạo email HTML với dữ liệu dự án
   const projects = $input.all()[0].json;
   let htmlContent = `
     <h1>Báo cáo dự án xây dựng mới</h1>
     <p>Địa điểm: ${$input.all()[0].json.locationInfo.city || "Không xác định"}</p>
     <table border="1">
       <tr>
         <th>Tên Dự Án</th>
         <th>Địa Chỉ</th>
         <th>Loại Dự Án</th>
         <th>Trạng Thái</th>
       </tr>
   `;

   projects.forEach(project => {
     htmlContent += `
       <tr>
         <td>${project.name || "N/A"}</td>
         <td>${project.location || "N/A"}</td>
         <td>${project.type || "N/A"}</td>
         <td>${project.status || "N/A"}</td>
       </tr>
     `;
   });

   htmlContent += `</table>`;
   return { json: { html: htmlContent } };
   ```

##### **G. Cấu Hình Node Wait (n8n-nodes-base.wait)**
- **Thời gian chờ**: Đặt từ **30 giây đến 5 phút** để đảm bảo dữ liệu được xử lý hoàn toàn trước khi gửi email.

---
### **✍️ Mẹo & Gợi Ý Nâng Cao**
1. **Kết hợp với Slack/Telegram**:
   - Thêm node **Slack Webhook** hoặc **Telegram Bot** để gửi thông báo tức thời khi có dự án mới.
   - **Cách làm**:
     - Thêm node **Slack Webhook** sau **Send Alert Email**.
     - Điền **Webhook URL** từ Slack (Settings → Custom Integrations → Incoming Webhooks).
     - Nội dung thông báo:
       ```json
       {
         "text": `🚧 Dự án mới tại ${$json["location"]}: ${$json["projectName"]}`,
         "attachments": [{
           "title": $json["projectName"],
           "title_link": $json["link"],
           "text": $json["description"]
         }]
       }
       ```

2. **Lưu log dữ liệu**:
   - Thêm node **Google Sheets** hoặc **Notion API** để lưu tất cả yêu cầu và kết quả vào bảng dữ liệu.
   - **Cách làm**:
     - Thêm node **Google Sheets** sau **Send Alert Email**.
     - Điền **Sheet Name** và **Credentials** (nếu chưa có, thêm mới).
     - **Data to Insert**:
       ```json
       {
         "email": $json["email"],
         "location": $json["locationInfo"]["city"],
         "projectsFound": $json["projects"].length > 0,
         "timestamp": new Date().toISOString()
       }
       ```

3. **Gửi báo cáo định kỳ**:
   - Sử dụng **Schedule Trigger** để gửi báo cáo tổng hợp hàng tuần/tháng.
   - **Cách làm**:
     - Tạo một workflow mới với **Schedule Trigger** (ví dụ: `0 10 * * 1` để chạy hàng tuần lúc 10h sáng thứ hai).
     - Thêm node **Google Sheets** để lấy dữ liệu từ tuần trước.
     - Thêm node **Email Send** để gửi báo cáo tổng hợp.

4. **Tối ưu API**:
   - Nếu API trả về dữ liệu quá lớn, thêm node **Set** để giới hạn số lượng dự án trả về (ví dụ: chỉ lấy 10 dự án mới nhất).
   - **Cách làm**:
     ```javascript
     // Trong node Process Construction Data
     return { json: projects.slice(0, 10) };
     ```

---
### **📌 Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi việc tra cứu thủ công và theo dõi dự án xây