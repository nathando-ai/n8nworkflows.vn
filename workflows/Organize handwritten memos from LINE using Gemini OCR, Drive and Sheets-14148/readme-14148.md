---
title: "📝 **Tự Động Hóa Sách Vở Tay Viết qua LINE với OCR AI, Google Drive & Sheets - Không Cần Code!**"
description: "Workflow này tự động nhận, quét, tóm tắt và lưu trữ sách vở tay viết gửi qua LINE thành dữ liệu có cấu trúc trên Google Sheets, giúp các sếp tiết kiệm thời gian quản lý và tìm kiếm thông tin hiệu quả."
slug: "tieu-dong-hoa-sach-vo-tay-viet-line-ocr-ai"
tags: [n8n, automation, no-code, google-drive, google-sheets, ai-ocr, line-bot, gemini-ai]
keywords: [tự động hóa n8n, quét sách vở tay viết, gemini ocr, lưu trữ google sheets, tự động hóa line bot, workflow n8n google drive]
---

# 🚀 **Tự Động Hóa Sách Vở Tay Viết qua LINE với OCR AI, Google Drive & Sheets**

### **Giải pháp hoàn hảo cho các sếp quản lý thông tin tay viết**
Có bao giờ các sếp phải mất nhiều thời gian để ghi chép, quét và tổ chức lại những cuốn sách vở tay viết từ học sinh, nhân viên hay khách hàng? Hay phải lo lắng khi mất mát hoặc khó tìm kiếm thông tin quan trọng? **Workflow này sẽ tự động hóa toàn bộ quá trình** – từ nhận tin nhắn qua LINE, quét nội dung bằng AI OCR, tóm tắt và lưu trữ vào Google Sheets, đến phản hồi kết quả cho người dùng – **không cần viết một dòng code nào!**

:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động 24/7 mà không gián đoạn, các sếp nên **self-host n8n trên VPS riêng** để đảm bảo tính bảo mật và hiệu suất tối ưu.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian**: Không cần quét thủ công hoặc nhập liệu lại.
✅ **Tự động phân loại**: Sách vở được tự động chia sẻ vào các bảng Google Sheets theo danh mục.
✅ **Tóm tắt thông minh**: AI Gemini tự động trích xuất tiêu đề, nội dung tóm tắt và thẻ từ sách vở tay viết.
✅ **Báo cáo ngay lập tức**: Người dùng nhận phản hồi tức thời qua LINE khi xử lý xong.
✅ **Tìm kiếm dễ dàng**: Dữ liệu được lưu trữ có cấu trúc, giúp tìm kiếm nhanh chóng.
✅ **Hoạt động liên tục**: Workflow chạy 24/7 trên VPS, không phụ thuộc vào máy tính cá nhân.
:::

---

## 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản LINE Developer**:
   - Tạo **Channel** trên [LINE Developers Console](https://developers.line.biz/) và lấy **Channel Access Token**.
   - Cấu hình **Webhook URL** từ workflow này vào LINE Developers Console.
2. **Google Drive**:
   - Tạo một **folder** để lưu trữ ảnh sách vở (ví dụ: `Memo_Images`).
   - Cấu hình **Google Drive OAuth 2.0** trong n8n với quyền `Drive` và `Files`.
3. **Google Sheets**:
   - Tạo một **bảng Google Sheets** để lưu trữ dữ liệu (ví dụ: `Memo_Organization`).
   - Cấu hình **Google Sheets OAuth 2.0** trong n8n với quyền `Edit Spreadsheets`.
4. **Google Gemini API**:
   - Đăng ký API key từ [Google AI Studio](https://aistudio.google/) và thêm vào n8n với tên `googlePalmApi`.
5. **n8n Workflow**:
   - Cài đặt **n8n** (self-hosted hoặc dùng phiên bản cloud miễn phí).

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Tải file JSON từ [đây](https://n8n.io/workflows/14148) (hoặc copy JSON từ link trên).
2. Mở **n8n Editor** → Nhấn `Import` → Dán JSON và nhấn `Import`.

:::note[Lưu ý]
- **Không** nhấn `Active` ngay lập tức! Các sếp cần cấu hình các node quan trọng trước.
:::

---

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**

#### **A. Cấu hình Webhook LINE (Node: `LINE_Receive_Webhook`)**
- **Path**: Giá trị mặc định là `=e89b4943-1f2e-4d37-84ad-0fce0b78175e` (không cần thay đổi).
- **HTTP Method**: Đặt là `POST`.
- **Cấu hình LINE Developers Console**:
  - Trên [LINE Developers Console](https://developers.line.biz/), chọn **Messaging API** → **Webhook**.
  - Nhập **Webhook URL** từ n8n (ví dụ: `https://tên-domain.com/webhook/e89b4943-1f2e-4d37-84ad-0fce0b78175e`).
  - Chọn **POST** và lưu lại.

#### **B. Cấu hình Google Drive (Node: `Drive_Upload_Image`)**
- **Credentials**: Chọn `googleDriveOAuth2Api` (đã cấu hình trước).
- **Folder ID**: Nhập ID của folder Google Drive bạn tạo (lấy từ liên kết folder: `https://drive.google.com/drive/folders/FOLDER_ID`).

#### **C. Cấu hình Google Sheets (Node: `Sheets_Get_Metadata` và `Sheets_Append_Row`)**
- **Credentials**: Chọn `googleSheetsOAuth2Api`.
- **Spreadsheet ID**: Lấy từ liên kết Google Sheets (ví dụ: `1AbCdEfGhIjKlMnOpQrStUvWxYz`).
- **Sheet Name**: Đặt tên cho sheet (ví dụ: `Memo_2024`).

#### **D. Cấu hình Google Gemini AI (Node: `AI_Model_Gemini`)**
- **Credentials**: Chọn `googlePalmApi` (đã cấu hình API key).
- **Prompt**: Để mặc định (AI sẽ tự động trích xuất tiêu đề, nội dung và thẻ từ ảnh).

#### **E. Cấu hình Node `Data_Parse_OCR_JSON` (Code Node)**
- **Mã code**: Các sếp không cần chỉnh sửa, nhưng có thể kiểm tra logic ở đây để hiểu cách xử lý JSON từ Gemini:
  ```javascript
  // Example logic (check n8n canvas for exact code)
  const jsonData = JSON.parse($input.all().json);
  return {
    json: jsonData,
    title: jsonData.title,
    summary: jsonData.summary,
    tags: jsonData.tags || []
  };
  ```

#### **F. Cấu hình Node `Sheets_Check_Category_Exists` (Code Node)**
- **Mã code**: Kiểm tra xem sheet đã tồn tại chưa:
  ```javascript
  // Example logic (check n8n canvas for exact code)
  const sheetName = $input.all().sheetName;
  const sheets = $input.all().sheets;
  const exists = sheets.some(s => s.properties.title === sheetName);
  return { exists };
  ```

---

### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Gửi một ảnh sách vở tay viết qua LINE (đảm bảo là ảnh chứ không phải text).
   - Kiểm tra **n8n Editor** để xem workflow có chạy đúng không.
2. **Active Workflow**:
   - Sau khi kiểm tra thành công, nhấn `Active` để workflow hoạt động liên tục.

---

## ✍️ **Mẹo & gợi ý nâng cao**
1. **Tự động tạo sheet mới cho mỗi danh mục**:
   - Nếu sách vở thuộc nhiều danh mục khác nhau (ví dụ: Toán, Văn, Lịch sử), workflow sẽ tự động tạo sheet mới khi danh mục chưa tồn tại.

2. **Gửi báo cáo định kỳ**:
   - Sử dụng **n8n Trigger** (ví dụ: `cron`) để gửi báo cáo tổng hợp về số lượng sách vở đã lưu trữ qua LINE hoặc Email hàng tuần.

3. **Kết hợp với Slack/Telegram**:
   - Thay vì chỉ phản hồi qua LINE, các sếp có thể thêm node `httpRequest` để gửi kết quả lên Slack/Telegram để theo dõi.

4. **Lưu log cho việc debug**:
   - Thêm node `Set` hoặc `Code` để lưu log vào Google Sheets hoặc một file JSON để theo dõi lỗi nếu workflow gặp vấn đề.

5. **Tối ưu hóa AI OCR**:
   - Nếu chất lượng OCR không tốt, các sếp có thể điều chỉnh **prompt** trong node `AI_Model_Gemini` để AI hiểu rõ hơn nội dung sách vở.

---

## 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** để tự động hóa việc quản lý sách vở tay viết, giúp các sếp:
✔ **Tiết kiệm thời gian** không cần quét hoặc nhập liệu thủ công.
✔ **Tổ chức dữ liệu** một cách logic và dễ tìm kiếm.
✔ **Tận dụng AI** để tóm tắt và phân loại thông tin tự động.

**Hãy áp dụng ngay workflow này trên VPS của mình và bắt đầu tự động hóa quản lý sách vở từ hôm nay!** 🚀

---
**🔗 [Xem workflow gốc](https://n8n.io/workflows/14148) | 📌 [Cài đặt n8n trên VPS](https://docs.n8n.io/hosting/self-hosting-on-a-vps/)**