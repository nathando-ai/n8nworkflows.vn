---
title: "🚀 Tự Động Hóa Phản Hồi Khách Hàng từ NiceReply → MS Teams Theo Đội Ngũ & Tình Trạng (AI + No-Code)"
description: "Workflow tự động hóa hoàn toàn miễn phí giúp doanh nghiệp thu thập phản hồi từ NiceReply, phân loại theo tình trạng (hạnh phúc/không hạnh phúc), và gửi tự động đến các đội ngũ phù hợp trên MS Teams. Giảm 90% thời gian xử lý thủ công, tăng độ chính xác và phản hồi nhanh chóng cho khách hàng."
slug: "tieu-dong-hoa-phan-hoi-nicereply-ms-teams"
tags: [n8n, automation, no-code, ai-summarization, microsoft-teams, nicereply, ticket-management]
keywords: [n8n workflow tự động hóa, NiceReply MS Teams, phân loại phản hồi theo tình trạng, tự động hóa phản hồi khách hàng, no-code automation, AI sentiment analysis]
---

# 🚀 **Tự Động Hóa Phản Hồi Khách Hàng từ NiceReply → MS Teams Theo Đội Ngũ & Tình Trạng (AI + No-Code)**

### **Giải pháp cho doanh nghiệp bị "ngập" phản hồi khách hàng nhưng không biết phân loại và chuyển tiếp như thế nào?**
Hàng ngày, các sếp phải mất **3-5 giờ** để:
- Lọc và đọc hàng trăm phản hồi từ NiceReply.
- Phân loại chúng theo **đội ngũ** (Support, Docs, Consulting...) và **tình trạng** (hạnh phúc/không hạnh phúc).
- Chuyển tiếp đến các thành viên phù hợp trên MS Teams.
- **Không có thời gian** để tập trung vào việc cải thiện trải nghiệm khách hàng.

**Workflow này tự động hóa toàn bộ quy trình đó chỉ trong vài phút cài đặt!**
Không cần viết code, không cần kỹ sư IT. Chỉ cần **n8n + MS Teams + NiceReply**, bạn đã có một hệ thống **tự động phân loại và chuyển tiếp phản hồi** với độ chính xác cao, hoạt động **24/7** mà không tốn chi phí thêm.

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow này **chạy ổn định 24/7** và không bị gián đoạn, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** thay vì dùng phiên bản miễn phí trên cloud.
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 Mã giảm giá: **VPSN8N** - giảm tới **39%**)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (Đảm bảo tốc độ cao, không lag)
:::

---

## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm 90% thời gian** xử lý phản hồi thủ công (từ 5 giờ/ngày xuống còn 30 phút).
✅ **Phân loại chính xác** phản hồi theo **tình trạng (hạnh phúc/không hạnh phúc)** và **đội ngũ** (Support, Docs, Consulting...).
✅ **Gửi tự động** đến MS Teams với **các thông báo rõ ràng**, giúp đội ngũ phản hồi nhanh chóng.
✅ **AI tự động hóa** việc chuyển đổi số thành **text mô tả** (ví dụ: "Happiness: 1" → "Trạng thái: Xấu").
✅ **Hoạt động liên tục** 24/7, không phụ thuộc vào giờ làm việc của nhân viên.
✅ **Dễ dàng mở rộng** cho nhiều đội ngũ khác (Marketing, Sales, Tech Support...).
:::

---

## 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
### **1. Tài khoản và API Key**
- **Tài khoản NiceReply** (để lấy phản hồi).
- **Tài khoản MS Teams** (để gửi phản hồi đến các kênh/nhóm).
- **API Key của NiceReply** (nếu sử dụng API chính thức).
- **Credentials của n8n** (để kết nối với MS Teams).

### **2. Cấu hình trước**
- **Xác định các đội ngũ** cần nhận phản hồi (ví dụ: Support, Docs, Consulting).
- **Mã hóa các Survey ID** từ NiceReply thành tên dễ đọc (ví dụ: `abcd-123` → "Hỗ trợ kỹ thuật").
- **Cấu hình các kênh MS Teams** tương ứng với mỗi đội ngũ.

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. **Tải workflow** từ [n8n.io/workflows/10113](https://n8n.io/workflows/10113) (ấn nút "Download").
2. **Mở n8n Editor** trên máy chủ của bạn.
3. **Nhấn "Import"** → Chọn file JSON vừa tải.
4. **Chọn "Import"** để workflow xuất hiện trên canvas.

#### **Phương pháp 2: Copy/Paste JSON**
1. **Tải file JSON** từ link trên.
2. **Mở n8n Editor** → Nhấn **"Import"** → Chọn **"Paste JSON"**.
3. **Dán toàn bộ nội dung JSON** vào ô và nhấn **"Import"**.

---

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này có **17 node**, nhưng chỉ có **5 node quan trọng** cần cấu hình kỹ lưỡng:

#### **🔹 Node 1: Schedule Trigger (Đặt lịch chạy)**
- **Cấu hình**:
  - **Frequency**: Chọn **"Every day"** (hoặc tùy chỉnh theo nhu cầu).
  - **Time**: Đặt giờ chạy (ví dụ: **8h sáng** để xử lý phản hồi mới nhất).
  - **Time Zone**: Chọn **GMT+7** (hoặc khu vực của bạn).

#### **🔹 Node 2: Get Feedback (Lấy phản hồi từ NiceReply)**
- **Cấu hình**:
  - **Method**: Chọn **"GET"**.
  - **URL**: Sử dụng **API của NiceReply** (nếu có) hoặc **URL của NiceReply** để lấy dữ liệu.
    - **Ví dụ**:
      ```
      https://api.nicereply.com/v1/surveys/{survey_id}/responses
      ```
  - **Headers**:
    - `Authorization`: Điền **API Key** của NiceReply.
    - `Content-Type`: `application/json`.
  - **Credentials**: Chọn **NiceReply API Key** (đã tạo trước).

#### **🔹 Node 3: Change survey ID according to NiceReply (Chuyển đổi Survey ID)**
- **Cấu hình**:
  - **AI Transform**: Sử dụng **mapping rule** để chuyển đổi **Survey ID** thành tên đội ngũ.
    - **Ví dụ**:
      ```json
      {
        "SurveyID": "362ea713-8867-47fe-bcbf-7394b7ce419a" → "Documentation"
      }
      ```
  - **Cách thực hiện**:
    1. Nhấn **"Edit"** trên node này.
    2. Chọn **"AI Transform"** → **"Code"**.
    3. Điền **lệnh JavaScript** như sau:
       ```javascript
       // Dữ liệu đầu vào (input)
       const input = $input.all();

       // Mapping Survey ID
       const surveyMapping = {
         "362ea713-8867-47fe-bcbf-7394b7ce419a": "Documentation",
         "12345678-90ab-cdef-1234-567890abcdef": "Support",
         "87654321-fedc-ba98-7654-3210fedcba98": "Consulting"
       };

       // Chuyển đổi
       const output = input.map(item => {
         item.SurveyID = surveyMapping[item.SurveyID] || item.SurveyID;
         return item;
       });

       // Trả về kết quả
       return output;
       ```

#### **🔹 Node 4: Change happiness value (Chuyển đổi giá trị hạnh phúc)**
- **Cấu hình**:
  - **AI Transform**: Chuyển đổi **số thành text** để dễ đọc.
    - **Ví dụ**:
      - **Input**: `"Happiness": 1`
      - **Output**: `"Happiness": "Xấu"`
  - **Cách thực hiện**:
    1. Nhấn **"Edit"** trên node này.
    2. Chọn **"AI Transform"** → **"Code"**.
    3. Điền **lệnh JavaScript** như sau:
       ```javascript
       const input = $input.all();

       const happinessMapping = {
         1: "Xấu",
         2: "Trung bình",
         3: "Tốt"
       };

       const output = input.map(item => {
         item.Happiness = happinessMapping[item.Happiness] || item.Happiness;
         return item;
       });

       return output;
       ```

#### **🔹 Node 5: Send to [Team Name] (Gửi phản hồi đến MS Teams)**
- **Cấu hình**:
  - **Resource**: Chọn **"channelMessage"** (nếu gửi đến kênh) hoặc **"chatMessage"** (nếu gửi riêng lẻ).
  - **Teams Webhook URL**: Điền **URL Webhook** của kênh MS Teams tương ứng.
    - **Cách lấy URL Webhook**:
      1. Mở kênh MS Teams cần gửi.
      2. Nhấn **"..."** → **"Connectors"** → **"Incoming Webhook"**.
      3. Nhấn **"Configure"** → **"Create"** → **Copy URL**.
  - **Message Format**: Sử dụng **template** như sau:
    ```json
    {
      "text": "📢 **Phản hồi mới từ NiceReply**\n\n" +
              "- **Khách hàng**: {{ $json["Respondent"] || "Khách hàng ẩn" }}\n" +
              "- **Survey**: {{ $json["SurveyID"] }}\n" +
              "- **Tình trạng**: {{ $json["Happiness"] }}\n" +
              "- **Nội dung**: {{ $json["Comment"] || "Không có bình luận" }}\n\n" +
              "🔗 [Xem chi tiết trên NiceReply]({{ $json["Link"] }})"
    }
    ```
  - **Credentials**: Chọn **MS Teams Webhook** (đã tạo trước).

---

### **3. Kích hoạt ⚡️**
1. **Test Run** (kiểm tra dữ liệu mẫu):
   - Nhấn **"Run Workflow"** trên n8n Editor.
   - Kiểm tra **log** để đảm bảo phản hồi được lấy và gửi đúng.
2. **Bật Active**:
   - Sau khi kiểm tra thành công, **đánh dấu workflow thành "Active"**.

---

## ✍️ **Mẹo & gợi ý nâng cao**
### **1. Tự động gửi báo cáo hàng ngày**
- **Sử dụng node Schedule Trigger** để chạy workflow vào **cuối ngày**.
- **Thêm node Microsoft Teams** để gửi **báo cáo tổng hợp** về số lượng phản hồi, tình trạng trung bình, đội ngũ nào nhận nhiều nhất.

### **2. Kết hợp với Slack/Telegram**
- **Thêm node Webhook** của Slack/Telegram để **báo động** khi có phản hồi **tình trạng xấu**.
- **Ví dụ**:
  ```json
  {
    "text": "⚠️ **Phản hồi xấu mới** từ NiceReply!\n\n" +
            "- **Khách hàng**: {{ $json["Respondent"] }}\n" +
            "- **Tình trạng**: {{ $json["Happiness"] }}\n" +
            "- **Nội dung**: {{ $json["Comment"] }}"
  }
  ```

### **3. Lưu log phản hồi vào Google Sheets/Excel**
- **Thêm node Google Sheets** để **ghi lại tất cả phản hồi** vào bảng Excel.
- **Cách cấu hình**:
  - **Sheet Name**: Điền tên bảng (ví dụ: "Phản hồi NiceReply").
  - **Headers**: Chọn các cột cần ghi (Respondent, SurveyID, Happiness, Comment, Timestamp).

### **4. Phân loại phản hồi theo độ ưu tiên**
- **Thêm node Filter** để **lọc phản hồi tình trạng xấu** và gửi **ưu tiên** đến **Quản lý cấp cao**.
- **Ví dụ**:
  ```javascript
  // Node Filter (lọc Happiness = "Xấu")
  $node["filter"].json = {
    "json": {
      "Happiness": "Xấu"
    }
  };
  ```

### **5. Tự động gửi email thông báo**
- **Thêm node Email** để gửi **email thông báo** cho đội ngũ khi có phản hồi mới.
- **Ví dụ**:
  ```json
  {
    "to": "team@example.com",
    "subject": "📢 Phản hồi mới từ NiceReply",
    "text": "Xin chào đội ngũ,\n\nCó phản hồi mới từ NiceReply:\n- Khách hàng: {{ $json["Respondent"] }}\n- Tình trạng: {{ $json["Happiness"] }}\n- Nội dung: {{ $json["Comment"] }}\n\nXin vui lòng xử lý.\nTrân trọng,"
  }
  ```

---

## 📌 **Kết luận**
Workflow này **giải quyết hoàn toàn vấn đề "ngập" phản hồi khách hàng** mà các sếp gặp phải hàng ngày. Bằng cách **tự động hóa phân loại và chuyển tiếp**, bạn:
✔ **Tiết kiệm thời gian** để tập trung vào việc cải thiện trải nghiệm khách hàng.
✔ **Giảm thiểu lỗi** trong quá trình chuyển tiếp thủ công.
✔ **Tăng tốc độ phản hồi** của đội ngũ, làm hài lòng khách hàng hơn.

**Bắt đầu ngay hôm nay!**
1. **Import workflow** từ [n8n.io/workflows/10113](https://n8n.io/workflows/10113).
2. **Cấu hình các node quan trọng** (NiceReply, MS Teams, AI Transform).
3. **Test Run** và **bật Active**.
4. **Mở rộng** với các tính năng nâng cao như gửi báo cáo, Slack alert...

**Nếu có vấn đề**, các sếp có thể liên hệ với **Easy8.ai** qua:
- [Community n8n](https://community.n8n.io/u/easy8.ai)
- [YouTube Easy8.ai](https://www.youtube.com/@easy8ai)

**🚀 Hãy tự động hóa ngay hôm nay và làm việc thông minh hơn!**