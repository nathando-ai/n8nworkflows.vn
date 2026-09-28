---
title: "🤖 **Tự Động Hóa Phân Loại & Báo Cáo Tickets Hỗ Trợ bằng Gemini AI + Typeform + Google Sheets**"
description: "Workflow này tự động phân loại tickets hỗ trợ từ Typeform bằng trí tuệ nhân tạo Gemini, lưu trữ dữ liệu vào Google Sheets và gửi báo cáo tổng hợp qua email hàng ngày. Giúp các sếp tiết kiệm 10+ giờ/tháng và giảm thiểu sai sót trong phân loại."
slug: "tu-dong-hoa-phan-loai-ticket-gemini-typeform-google-sheets"
tags: [n8n, automation, ai, google-sheets, typeform, gemini-ai, support-ticket]
keywords: [tự động hóa tickets hỗ trợ, gemini ai phân loại, typeform tự động, báo cáo hàng ngày google sheets, n8n workflow hỗ trợ khách hàng]
---

# 🚀 **Tự Động Hóa Phân Loại & Báo Cáo Tickets Hỗ Trợ bằng AI Gemini**

### **Nỗi Đau Của Các Sếp Hiện Nay**
Hàng ngày, các sếp phải:
- **Làm thủ công** phân loại hàng trăm tickets hỗ trợ từ Typeform (hoặc Google Form).
- **Tìm kiếm và tổng hợp** dữ liệu từ nhiều nguồn khác nhau để báo cáo cho đội ngũ.
- **Lo lắng về sai sót** khi phân loại thủ công, dẫn đến phản hồi chậm và mất uy tín với khách hàng.
- **Tốn thời gian** để gửi báo cáo hàng ngày cho quản lý, trong khi dữ liệu có thể được tự động hóa hoàn toàn.

**Workflow này giải quyết tất cả đó!** Dùng trí tuệ nhân tạo **Gemini AI** để phân loại tự động, **Google Sheets** để lưu trữ và **email tự động** để báo cáo hàng ngày—**không cần viết một dòng code nào!**

---
### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**3 Lợi Ích Cốt Lõi**]
✅ **Tiết kiệm 10+ giờ/tháng** – Dữ liệu được phân loại và báo cáo tự động.
✅ **Chính xác 100%** – Gemini AI phân loại dựa trên ngữ nghĩa, giảm thiểu sai sót.
✅ **Báo cáo tự động hàng ngày** – Email tổng hợp số lượng tickets theo danh mục được gửi tự động.
✅ **Dữ liệu trung tâm** – Tất cả tickets được lưu vào Google Sheets, dễ dàng phân tích sau này.
:::

---
### 🔧 **Yêu Cầu Cần Thiết**
Trước khi chạy workflow, các sếp cần chuẩn bị:
1. **Tài khoản Typeform** (để lấy dữ liệu tickets mới).
2. **Google Sheets** (để lưu trữ và tổng hợp dữ liệu).
   - **Sheet cần có 2 tab**:
     - `Tickets` (để lưu tickets mới).
     - `Report` (để lưu báo cáo tổng hợp).
   - **Cấu trúc cột trong `Tickets`**:
     | ID | Ticket Text | Category (do AI phân loại) | Timestamp |
     |----|------------|----------------------------|-----------|
   - **Cấu trúc cột trong `Report`**:
     | Category | Count (Today) | Count (Total) |
     |----------|--------------|----------------|
3. **Tài khoản email** (để gửi báo cáo tự động).
4. **API Key của Google Sheets** (để n8n có quyền truy cập).
5. **API Key của Typeform** (để lấy dữ liệu mới).

---
### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n.io/workflows/4447](https://n8n.io/workflows/4447) và import vào **n8n Editor**.
- **Cách 2**: Copy toàn bộ JSON từ link trên và paste vào **Import Workflow** trong n8n.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow gồm **8 node** chính, các sếp cần cấu hình kỹ lưỡng như sau:

##### **🔹 Node 1: Form Trigger (Typeform)**
- **Chọn Credential**: Tạo mới trong **Typeform** và điền `API Key`.
- **Form ID**: Chọn form hỗ trợ của bạn (đã cấu hình để gửi dữ liệu ticket).
- **Trigger**: Chọn `New Submission` (mỗi khi có ticket mới).

##### **🔹 Node 2: Google Gemini Chat Model**
- **Chọn Credential**: Tạo mới trong **Google AI** và điền `API Key`.
- **Model**: Chọn `gemini-1.0-pro`.
- **Prompt**: Sử dụng template mặc định (cần chỉnh sửa nếu muốn phân loại theo danh mục riêng):
  ```
  You are a support ticket categorizer. Classify the following ticket text into one of these categories:
  - Billing Issues
  - Technical Problems
  - Feature Requests
  - Account Management
  - Other
  Return ONLY the category name in plain text.
  Ticket: {ticketText}
  ```

##### **🔹 Node 3: AI Categorization (Chain LLM)**
- **Input**: Kết nối từ **Google Gemini Chat Model**.
- **Output**: Dữ liệu phản hồi của AI (cần xử lý trong node tiếp theo).

##### **🔹 Node 4: Extract Category (Code Node)**
- **Mã JavaScript**:
  ```javascript
  // Lấy phản hồi từ AI và trích xuất category
  const response = $input.all();
  const category = response[0].json.output.text.split('\n')[0].trim();
  return { json: { category } };
  ```
- **Lưu ý**: Nếu AI trả về nhiều dòng, cần chỉnh sửa mã để lấy dòng đầu tiên.

##### **🔹 Node 5: Store Data (Google Sheets - Append)**
- **Credential**: Chọn Google Sheets với quyền chỉnh sửa.
- **Spreadsheet ID**: ID của Google Sheets của bạn (tìm trong URL: `https://docs.google.com/spreadsheets/d/[ID]/edit`).
- **Sheet Name**: Chọn tab `Tickets`.
- **Headers**: Chọn `ID, Ticket Text, Category, Timestamp`.

##### **🔹 Node 6: Fetch Support Ticket Data (Google Sheets)**
- **Credential**: Cùng với node trước.
- **Spreadsheet ID**: Cùng với node trước.
- **Sheet Name**: Chọn tab `Tickets`.
- **Query**: Lấy tất cả dữ liệu mới nhất (cần chỉnh sửa nếu có điều kiện lọc).

##### **🔹 Node 7: Increment Counter (Code Node)**
- **Mã JavaScript**:
  ```javascript
  // Đếm số lượng tickets theo category
  const data = $input.all();
  const categoryCounts = {};

  data.forEach(item => {
    const category = item.json.category;
    categoryCounts[category] = (categoryCounts[category] || 0) + 1;
  });

  return { json: { categoryCounts } };
  ```
- **Lưu ý**: Nếu muốn tính tổng số lượng, cần thêm logic tính toán.

##### **🔹 Node 8: Email Ticket Summary (Email Send)**
- **Credential**: Tạo mới trong **Email** (SMTP hoặc Gmail).
- **To**: Địa chỉ email của quản lý hoặc team.
- **Subject**: `Báo cáo Tickets Hôm Nay - [Ngày Tháng]`.
- **Body**: Sử dụng template:
  ```
  Xin chào,
  Đây là báo cáo tổng hợp tickets hỗ trợ hôm nay:
  - Billing Issues: {countBilling}
  - Technical Problems: {countTech}
  - Feature Requests: {countFeature}
  - Account Management: {countAccount}
  - Other: {countOther}
  ```

---
### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết nối với Slack/Telegram**:
   - Thêm node **Slack Webhook** hoặc **Telegram Bot** để thông báo tức thời khi có ticket mới.
2. **Lưu Log Dữ liệu**:
   - Thêm node **Google Drive** để lưu bản sao dữ liệu hàng ngày.
3. **Báo Cáo Định Kỳ**:
   - Sử dụng **n8n Scheduler** để chạy workflow hàng tuần/month để báo cáo tổng hợp dài hạn.
4. **Cải Thiện Prompt AI**:
   - Nếu Gemini phân loại sai, hãy **cập nhật prompt** để rõ ràng hơn (ví dụ: thêm ví dụ cụ thể).
5. **Tích Hợp với Zendesk/Help Scout**:
   - Nếu đang dùng hệ thống ticket khác, thay thế **Typeform Trigger** bằng node tương ứng (ví dụ: `zendeskTrigger`).

---
### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc phân loại và báo cáo tickets thủ công. Với **Gemini AI**, dữ liệu được phân loại chính xác, và **Google Sheets + Email tự động** đảm bảo báo cáo luôn cập nhật.

**Hành động ngay!**
1. **Cài đặt n8n Self-hosted** trên VPS để workflow chạy 24/7 (không phụ thuộc vào n8n.io).
   👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
2. **Import workflow** và cấu hình theo hướng dẫn trên.
3. **Bật Active** và xem dữ liệu tự động phân loại!

**Cần hỗ trợ?** Liên hệ với tác giả Yaron Been qua:
- [YouTube](https://www.youtube.com/@YaronBeen/videos)
- [LinkedIn](https://www.linkedin.com/in/yaronbeen/)

---
**Chúc các sếp thành công!** 🚀