---
title: "🚀 Tự Động Xếp Hạng & Gửi Thông Báo Ứng Viên Việc Làm Bằng AI Gemini + Email (N8n)"
description: "Workflow tự động hóa HR sử dụng Google Forms + Google Gemini để đánh giá ứng viên, phân loại và gửi email tự động cho đội ngũ HR và ứng viên. Giúp tiết kiệm 80% thời gian đánh giá thủ công, giảm sai sót và cá nhân hóa thông báo."
slug: "tự-dộng-xếp-hạng-ứng-viên-việc-làm-bằng-ai-gemini-email"
tags: [n8n, automation, hr, ai-summarization, google-sheets, google-gemini, email-automation]
keywords: [n8n workflow hr, tự động hóa tuyển dụng, google gemini trong n8n, đánh giá cv tự động, gửi email ứng viên, tự động hóa google sheets]
---

# 🚀 **Tự Động Xếp Hạng Ứng Viên Việc Làm Bằng AI Gemini + Email (N8n)**

### **Giải pháp nào giúp các sếp:**
- **Tiết kiệm 80% thời gian** đánh giá hồ sơ ứng viên thủ công.
- **Đánh giá khách quan** với AI Gemini (cấp độ 1–10) thay vì chủ quan.
- **Gửi email tự động** cho ứng viên và đội ngũ HR với thông báo cá nhân hóa.
- **Lưu trữ kết quả** trong Google Sheets để theo dõi và phân tích sau này.
- **Hoạt động 24/7** mà không cần can thiệp của con người.

---
## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Xếp hạng và gửi email cho hàng trăm ứng viên chỉ trong vài phút.
- **Chính xác cao**: AI Gemini phân tích kỹ năng, kinh nghiệm và phù hợp với mô tả công việc.
- **Cá nhân hóa thông báo**: Email gửi cho ứng viên và HR đều được tự động hóa với nội dung phù hợp.
- **Theo dõi dễ dàng**: Tất cả kết quả được lưu trong Google Sheets với trạng thái "Đã xếp hạng" hoặc "Bị loại".
- **Tích hợp AI**: Sử dụng Google Gemini để phân tích và tổng hợp thông tin một cách nhanh chóng.
:::

---
## 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Google Sheets** với OAuth2 để kết nối với n8n:
   - Tạo một **Google Sheet** mới để lưu trữ dữ liệu ứng viên (cấu trúc chi tiết sau).
   - Cài đặt **OAuth2 Credential** trong n8n để truy cập Google Sheets.
2. **API Key của Google Gemini**:
   - Đăng ký tại [Google AI Studio](https://aistudio.google/) để lấy API Key.
3. **Thông tin email**:
   - Cấu hình **Gmail SMTP** hoặc **Google Workspace** để gửi email tự động.
   - Cập nhật `fromEmail` (địa chỉ gửi) và `toEmail` (địa chỉ nhận) trong các node `emailSend`.
4. **Mô tả công việc (Job Description - JD)**:
   - Cập nhật danh sách các vị trí tuyển dụng trong `JD_MAP` (node `Extract Fields & Load JD`).
5. **Google Sheet mẫu**:
   - Sử dụng **ID Sheet** từ ví dụ: `1iv-8fToAzxBm8ht5vg-UP_p_hQzK4-...` (cập nhật sau khi tạo sheet mới).
:::

---
## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. **Tải workflow** từ [đây](https://n8n.io/workflows/14138) (nếu có link trực tiếp) hoặc sử dụng file JSON đã cung cấp.
2. Trong **n8n Editor**, nhấn **Import** và chọn file JSON.
3. **Hoặc** copy toàn bộ JSON và dán vào **Import Workflow** trong menu.

:::note[LƯU Ý]
- Nếu import từ file JSON, đảm bảo **không có lỗi syntax** (kiểm tra bằng cách paste vào [JSONLint](https://jsonlint.com/)).
- Sau khi import, **không kích hoạt workflow** ngay mà phải cấu hình các node quan trọng trước.
:::

---

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**

#### **A. Cấu hình Google Sheets**
1. **Google Sheets Trigger**:
   - Chọn **OAuth2 Credential** đã tạo trước đó.
   - Cập nhật **Sheet ID** (địa chỉ của Google Sheet) trong `googleSheetsTrigger`.
   - Chọn **Sheet Name** và **Range** (ví dụ: `Sheet1!A:Z`).
   - **Thiết lập polling interval**: Cài đặt thời gian refresh (ví dụ: **60 giây** để kiểm tra mới).

2. **Read All Rows**:
   - Sử dụng cùng **OAuth2 Credential** như trên.
   - Chọn **Sheet ID** và **Range** tương tự.

3. **Update Sheet Row**:
   - Cấu hình **HTTP Request** với OAuth2 để cập nhật dữ liệu.
   - Đảm bảo **URL** và **Headers** đúng định dạng của Google Sheets API.

#### **B. Cấu hình Google Gemini**
1. **Google Gemini Chat Model**:
   - Điền **API Key** từ Google AI Studio vào `apiKey` trong node `lmChatGoogleGemini`.
   - Cập nhật **model** (ví dụ: `gemini-pro`).
   - **Prompt template** đã được tối ưu trong workflow, nhưng các sếp có thể chỉnh sửa nếu cần.

#### **C. Cấu hình Email**
1. **Alert HR Team / Notify Shortlisted Candidate / Notify Rejected Candidate**:
   - Cấu hình **SMTP** trong `emailSend`:
     - **Host**: `smtp.gmail.com` (hoặc `smtp.yourdomain.com`).
     - **Port**: `587` (hoặc `465`).
     - **Username/Password**: Tài khoản email có quyền gửi.
     - **From Email**: Địa chỉ email gửi (ví dụ: `hr@company.com`).
     - **To Email**: Địa chỉ email nhận (đối với ứng viên hoặc HR).
   - **Chú ý**: Nếu sử dụng Gmail, bật **Less Secure Apps** (nếu cần) hoặc sử dụng **App Password**.

#### **D. Cấu hình Node Code**
1. **Filter Unprocessed Rows**:
   - Kiểm tra cột `col_18` (trong ví dụ) để đánh dấu đã xử lý (`'1'`).
   - Các sếp cần **đồng bộ cột** trong Google Sheet với ví dụ.

2. **Extract Fields & Load JD**:
   - Cập nhật `JD_MAP` (danh sách vị trí tuyển dụng và mô tả công việc):
     ```javascript
     const JD_MAP = {
       "Developer": "Mô tả công việc Developer...",
       "Designer": "Mô tả công việc Designer...",
       // Thêm các vị trí khác...
     };
     ```
   - Đảm bảo **các cột** trong Google Sheet phù hợp với mã trong code (ví dụ: `name`, `email`, `position`, `experience`, `skills`).

3. **Parse AI Output**:
   - Node này chuyển đổi kết quả JSON của Gemini thành định dạng dễ đọc.
   - **Không cần chỉnh sửa** trừ khi AI trả về định dạng khác.

#### **E. Cấu hình Node If (Check Score ≥ 7)**
- Node này **chia nhánh** workflow dựa trên điểm số:
  - **Nếu score ≥ 7**: Gửi email cho ứng viên và HR.
  - **Nếu score < 7**: Gửi email từ chối.

---
### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Thêm **một dòng mẫu** vào Google Sheet (ví dụ: tên, email, vị trí, kinh nghiệm, kỹ năng).
   - Chạy **Test** trong n8n để kiểm tra workflow hoạt động như thế nào.
   - Kiểm tra **log** và **email** để đảm bảo không có lỗi.

2. **Bật Active**:
   - Sau khi test thành công, **bật Active** cho workflow.
   - **Monitor** trong **n8n Dashboard** để theo dõi hoạt động.

---
## ✍️ **Mẹo & gợi ý nâng cao**

### **1. Tối ưu hóa Google Sheets**
- **Tạo template** cho ứng viên với các cột:
  - `Name`, `Email`, `Position`, `Experience`, `Skills`, `Resume Link` (nếu có).
  - `Score` (được AI tính), `Grade`, `Strengths`, `Weaknesses`, `Recommendation`, `Status` (`Shortlisted`/`Rejected`).
  - `col_18` (đánh dấu đã xử lý).

### **2. Kết hợp với Slack/Telegram**
- Thêm node **Slack Webhook** hoặc **Telegram Bot** để thông báo kết quả thực thời.
- Ví dụ:
  ```javascript
  // Thêm vào node `Alert HR Team` hoặc `Notify Shortlisted Candidate`
  const slackWebhook = "https://hooks.slack.com/services/...";
  await $node.setCredentials("slack", { webhookUrl: slackWebhook });
  ```

### **3. Lưu log hoạt động**
- Sử dụng node **Sticky Note** hoặc **HTTP Request** để lưu log vào Google Sheets/Google Drive.
- Ví dụ:
  ```javascript
  // Thêm vào node `Update Sheet Row`
  const logRow = {
    "Log": `Processed ${$input.all().name} at ${new Date().toISOString()}`,
    "Status": "Completed"
  };
  $node.set("logRow", logRow);
  ```

### **4. Gửi báo cáo định kỳ**
- Tạo một **workflow mới** để tổng hợp dữ liệu từ Google Sheets và gửi báo cáo email hàng tuần/tháng.
- Sử dụng node **Google Sheets** + **Pandas** (n8n Code) để tính toán thống kê.

### **5. Cập nhật mô tả công việc (JD)**
- Nếu công ty có nhiều vị trí tuyển dụng, **cập nhật `JD_MAP`** thường xuyên để AI đánh giá chính xác.

---
## 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn tự động hóa quy trình tuyển dụng, giảm thiểu công việc thủ công và tăng cường hiệu quả. Với **Google Gemini**, ứng viên sẽ được đánh giá khách quan, và **email tự động** giúp tiết kiệm thời gian gửi thông báo.

**Hành động ngay!**
1. **Cài đặt n8n** trên VPS (Self-hosted) để workflow hoạt động 24/7.
2. **Cấu hình Google Sheets, API Key và email** theo hướng dẫn.
3. **Import workflow** và **bật Active** sau khi test thành công.

:::success[🚀 KẾT QUẢ]
- **Tiết kiệm 80% thời gian** đánh giá hồ sơ.
- **Cải thiện trải nghiệm ứng viên** với thông báo cá nhân hóa.
- **Tối ưu hóa quy trình tuyển dụng** với AI và tự động hóa.

**Bắt đầu tự động hóa tuyển dụng của bạn ngay hôm nay!** 💼🤖
:::

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::