---
title: "🍽️ **Tự Động Hóa Thư Viện Đánh Giá Khách Hàng Quán Ăn: Nhận Feedback → Lưu Trữ → Gửi Thông Báo Email (N8n + Google Sheets)""
description: "Workflow tự động hóa thu thập đánh giá khách hàng về trải nghiệm ăn uống, lưu trữ dữ liệu vào Google Sheets và gửi thông báo email cho đội ngũ quản lý. Giúp quán ăn theo dõi sự hài lòng của khách hàng và cải thiện dịch vụ một cách hiệu quả, không cần viết code."
slug: "tu-dong-hoa-thu-thap-danh-gia-khach-hang-quan-an"
tags: [n8n, automation, google-sheets, email-marketing, market-research, no-code]
keywords: [tự động hóa n8n, thu thập feedback khách hàng, google sheets tự động, gửi email tự động, cải thiện dịch vụ quán ăn, workflow n8n market research]
---

# 🚀 **Tự Động Hóa Thư Viện Đánh Giá Khách Hàng Quán Ăn: Từ Feedback → Dữ Liệu → Thông Báo Email**

### **Nỗi Đau Của Các Sếp Quán Ăn**
Hàng ngày, các sếp quán ăn phải mất thời gian quét qua hàng chục phản hồi từ khách hàng trên Google Form, Facebook, hoặc email để:
- **Lưu trữ** dữ liệu một cách rắc rối vào Google Sheets.
- **Phân tích** sự hài lòng của khách hàng và phát hiện điểm yếu.
- **Gửi thông báo** cho đội ngũ khi có phản hồi mới, nhưng thường bị quên hoặc làm thủ công.

Kết quả? **Thông tin quan trọng bị bỏ lỡ**, dịch vụ không được cải thiện kịp thời, và khách hàng cảm thấy không được quan tâm.

---
### **🎯 Kết Quả Các Sếp Nhận Được**
Với workflow này, các sếp sẽ:
✅ **Tự động thu thập** tất cả phản hồi từ khách hàng qua **Google Form** (hoặc email) và lưu vào **Google Sheets** một cách chính xác.
✅ **Nhận thông báo email tự động** khi có phản hồi mới, giúp đội ngũ phản hồi kịp thời.
✅ **Tiết kiệm thời gian** lên đến **50%** so với cách làm thủ công.
✅ **Cải thiện dịch vụ** bằng cách theo dõi xu hướng phản hồi và điều chỉnh ngay lập tức.

---
### **🔧 Yêu Cầu Cần Thiết**
Để workflow hoạt động, các sếp cần chuẩn bị:
📌 **Tài khoản Google** (để kết nối với Google Sheets và Google Form).
📌 **API Key OAuth 2.0** của Google (để truy cập Google Sheets và Form).
📌 **Tài khoản Email SMTP** (để gửi thông báo email, ví dụ: Gmail, SendGrid, hoặc SMTP của nhà cung cấp hosting).
📌 **Google Sheet** đã tạo sẵn với **cột phù hợp** (ví dụ: Tên khách hàng, Đánh giá, Ghi chú, Email).

---
### **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Truy cập [n8n.io](https://n8n.io/) và đăng nhập vào tài khoản.
2. Nhấp vào **"Create Workflow"** → **"Import Workflow"** và chọn file JSON (hoặc paste JSON từ [link gốc](https://n8n.io/workflows/5848)).
3. Hoặc copy toàn bộ JSON từ [đây](https://n8n.io/workflows/5848) và paste vào **"Import Workflow"**.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này bao gồm **6 node chính**, các sếp cần chú ý cấu hình như sau:

##### **🔹 Node 1: Trigger: Form Submitted (Google Form)**
- **Cấu hình**:
  - Chọn **Google Form** đã tạo sẵn (ví dụ: "Đánh Giá Trải Nghiệm Quán Ăn").
  - Đảm bảo **các cột trong Form** phù hợp với **cột trong Google Sheet** (ví dụ: `Tên`, `Đánh Giá`, `Ghi Chú`, `Email`).
  - **Credentials**: Chọn `googleSheetsTriggerOAuth2Api` (đã cấu hình trước khi import).

##### **🔹 Node 2: Wait: Pause Before Processing**
- **Cấu hình**:
  - Thời gian chờ mặc định là **5 giây** (có thể điều chỉnh nếu cần).
  - Dùng để đảm bảo dữ liệu từ Form được xử lý đầy đủ trước khi tiếp tục.

##### **🔹 Node 3: Append or Update Row in Google Sheet**
- **Cấu hình**:
  - **Google Sheet**: Chọn sheet đã tạo sẵn (ví dụ: "Feedback Khách Hàng").
  - **Range**: Chọn **Sheet Name + Range** (ví dụ: `Feedback!A1`).
  - **Operation**: Chọn `appendOrUpdate` (lưu hoặc cập nhật dòng mới).
  - **Credentials**: Chọn `googleSheetsOAuth2Api` (đã cấu hình trước).
  - **Mapping Data**: Đảm bảo các trường trong Form **khớp với cột trong Sheet** (ví dụ: `{{ $json["Tên"] }}` → `Tên`).

##### **🔹 Node 4: Wait for All Data (Code)**
- **Cấu hình**:
  - Node này sử dụng **JavaScript** để chờ tất cả dữ liệu từ Form được xử lý hoàn tất.
  - **Code mặc định**:
    ```javascript
    return {
      json: {
        allData: $input.all()
      }
    };
    ```
  - **Không cần chỉnh sửa** nếu muốn sử dụng mặc định.

##### **🔹 Node 5: Send Email: Notify Team About Feedback**
- **Cấu hình**:
  - **From Email**: Điền địa chỉ email gửi (ví dụ: `quananh@gmail.com`).
  - **To Email**: Điền email của đội ngũ quản lý (ví dụ: `quanly@quananh.com`).
  - **Subject**: Ví dụ: **"Có phản hồi mới từ khách hàng: {{ $json["Tên"] }}"** (sử dụng `{{ $json["Tên"] }}` để hiển thị tên khách hàng).
  - **Body Email**: Nội dung email tự động, ví dụ:
    ```
    Xin chào đội ngũ,

    Đã có phản hồi mới từ khách hàng:
    - **Tên**: {{ $json["Tên"] }}
    - **Đánh Giá**: {{ $json["Đánh Giá"] }}/5
    - **Ghi Chú**: {{ $json["Ghi Chú"] }}
    - **Email**: {{ $json["Email"] }}

    Xin vui lòng phản hồi kịp thời để cải thiện dịch vụ!
    ```
  - **Credentials**: Chọn `smtp` (đã cấu hình trước với thông tin SMTP của email).

##### **🔹 Node 6: Sticky Note (Ghi Chú)**
- **Cấu hình**:
  - Node này **không bắt buộc**, nhưng có thể dùng để **ghi chú** về quá trình hoạt động của workflow.
  - Ví dụ: `"Workflow đang hoạt động: Thu thập feedback từ Form và gửi email thông báo."`

---
#### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Nhấp vào **"Execute"** để thử nghiệm với dữ liệu mẫu từ Google Form.
   - Kiểm tra **Google Sheet** và **email** để đảm bảo dữ liệu được lưu và gửi đúng.
2. **Bật Active**:
   - Sau khi test thành công, nhấp vào **"Active"** để workflow chạy liên tục.

---
### **✍️ Mẹo & Gợi Ý Nâng Cao**
🔹 **Kết Nối Slack/Telegram**:
   - Thêm **node Slack/Telegram** sau node `Send Email` để thông báo phản hồi mới trên kênh nhóm.

🔹 **Lưu Log Dữ Liệu**:
   - Sử dụng **node `n8n-nodes-base.airtable`** để lưu dữ liệu phản hồi vào Airtable (để phân tích sâu hơn).

🔹 **Gửi Báo Cáo Định Kỳ**:
   - Tạo **workflow mới** sử dụng **node `n8n-nodes-base.googleSheets`** để tổng hợp dữ liệu từ Sheet và gửi báo cáo email hàng tuần.

🔹 **Cải Thiện Trải Nghiệm Khách Hàng**:
   - Thêm **node `n8n-nodes-base.llm`** (ví dụ: ChatGPT) để tự động phân tích cảm xúc từ phản hồi và đề xuất cải thiện.

---
### **📌 Kết Luận**
Workflow này giúp các sếp **tự động hóa hoàn toàn** quá trình thu thập, lưu trữ và thông báo phản hồi khách hàng, tiết kiệm thời gian và cải thiện dịch vụ một cách hiệu quả. **Không cần viết code**, chỉ cần import và cấu hình vài bước đơn giản.

**🚀 Hãy áp dụng ngay và bắt đầu cải thiện trải nghiệm của khách hàng từ hôm nay!**

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**💡 Lưu ý**: Nếu gặp vấn đề khi cấu hình, các sếp có thể tham khảo [hướng dẫn cài đặt OAuth 2.0 cho Google](https://docs.n8n.io/integrations/builtins/nodes/googleSheets/#authentication) hoặc liên hệ với **Oneclick AI Squad** qua [website](https://oneclickai.squad).