---
title: "🌟 Tự Động Hệ Thống Nhận Đánh Giá Sao (1-5★) Cho Khách Hàng - Không Cần Code!"
description: "Workflow n8n hoàn toàn tự chứa (self-contained) giúp doanh nghiệp thu thập đánh giá sao từ khách hàng qua form HTML đơn giản, lưu dữ liệu vào bảng Data Table và hiển thị trang cảm ơn tự động. Giúp cải thiện trải nghiệm khách hàng và tích lũy phản hồi thực tế chỉ trong vài phút."
slug: "tieu-thu-danh-gia-sao-khach-hang-voi-n8n"
tags: [n8n, automation, no-code, feedback-collection, data-table]
keywords: [tự động hóa nhận đánh giá sao, n8n workflow feedback, thu thập phản hồi khách hàng, form đánh giá sao tự động, lưu dữ liệu vào data table]
---

# 🚀 **Tự Động Hệ Thống Nhận Đánh Giá Sao (1-5★) Cho Khách Hàng - Không Cần Code!**

### **Giải quyết vấn đề gì?**
Các sếp đang gặp khó khăn khi phải:
- **Làm thủ công** thu thập đánh giá sao từ khách hàng qua email, form Google, hoặc phiếu giấy.
- **Không có hệ thống tự động** để lưu trữ và phân tích phản hồi một cách khoa học.
- **Phải phụ thuộc vào các dịch vụ bên thứ ba** (như Typeform, Google Forms) để thu thập dữ liệu, gây ra chi phí và rủi ro bảo mật.

**Workflow này là giải pháp hoàn hảo** cho các sếp muốn:
✅ **Tự động hóa** quá trình thu thập đánh giá sao từ khách hàng.
✅ **Lưu trữ dữ liệu** một cách an toàn vào **Data Table** của n8n.
✅ **Hiển thị trang cảm ơn** tự động sau khi khách hàng gửi phản hồi.
✅ **Không cần code** hoặc phụ thuộc vào dịch vụ bên thứ ba.

---
### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian** lên đến **90%** so với cách làm thủ công.
- **Dữ liệu chính xác và dễ phân tích** với Data Table tích hợp.
- **Trải nghiệm khách hàng tốt hơn** nhờ trang cảm ơn chuyên nghiệp.
- **Hoạt động 24/7** mà không cần can thiệp của con người.
- **Không phụ thuộc vào dịch vụ bên thứ ba**, đảm bảo bảo mật và độc lập.
:::

---
### 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi sử dụng workflow, các sếp cần:
1. **Tài khoản n8n** (cài đặt trên máy chủ riêng hoặc sử dụng phiên bản cloud).
2. **Không cần API key hoặc dịch vụ bên thứ ba** (workflow hoàn toàn tự chứa).
3. **Kiến thức cơ bản về n8n Editor** để cấu hình các node.
:::

---
### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Mở **n8n Editor** trên máy chủ của mình.
2. Nhấp vào **Import Workflow** (hoặc **Create New Workflow** và chọn **Import from JSON**).
3. Dán hoặc upload file JSON từ [đây](https://n8n.io/workflows/9787) (hoặc copy từ link trên).
4. Chọn **Import** để tải workflow vào.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflows này gồm **11 node**, nhưng các sếp chỉ cần chú ý đến các phần sau:

##### **A. Cấu hình Form Feedback (Form Configuration)**
- Mở node **"Form Configuration"** (type: `set`).
- **Cập nhật các thông tin sau**:
  - `title`: Tiêu đề của form (ví dụ: *"Đánh giá dịch vụ của chúng tôi"*).
  - `text`: Nội dung hướng dẫn (ví dụ: *"Xin vui lòng đánh giá trải nghiệm của bạn với chúng tôi bằng cách chọn số sao từ 1 đến 5"*).
  - `PostFeedbackLink`: **URL Webhook POST** của node **"Post Feedback"** (sẽ được tạo tự động khi publish webhook).

##### **B. Cấu hình Webhook (Post Feedback & Input Feedback)**
- Mở node **"Post Feedback"** (type: `webhook`) và **"Input Feedback"** (type: `webhook`).
- **Bật Publish** cho cả hai webhook để tạo URL.
- **Lưu ý**:
  - **Path** của cả hai webhook phải là `/feedback`.
  - **HTTP Method** của **"Post Feedback"** phải là `POST`.
  - **Copy URL POST** từ node **"Post Feedback"** và dán vào trường `PostFeedbackLink` trong node **"Form Configuration"**.

##### **C. Cấu hình Data Table (Save Feedback to Data Table)**
- Mở node **"Save Feedback to Data Table"** (type: `dataTable`).
- **Kiểm tra và cập nhật schema** để đảm bảo dữ liệu được lưu chính xác:
  - **Rating**: Số sao (1-5).
  - **Message**: Nội dung phản hồi (nếu có).
  - **Query Params**: Thông tin thêm từ URL (ví dụ: `?userId=123&source=email`).

##### **D. Cấu hình Theme (Theme Configuration)**
- Mở node **"Theme Configuration - Feedback Input"** và **"Theme Configuration - Feedback Submitted"**.
- **Tùy chỉnh giao diện** bằng cách thay đổi các thuộc tính CSS như:
  - Màu sắc (`backgroundColor`, `color`).
  - Font (`fontFamily`).
  - Kích thước (`fontSize`).

#### **3. Kích hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Nhấp vào nút **Execute Workflow** và thử gửi phản hồi từ form HTML.
   - Kiểm tra dữ liệu đã được lưu vào **Data Table** chưa.
2. **Bật Active Workflow**:
   - Sau khi kiểm tra thành công, nhấp vào **Active** để workflow hoạt động liên tục.

---
### ✍️ **Mẹo & gợi ý nâng cao**
:::info[MỞ RỘNG THÊM TÍNH NĂNG]
1. **Kết hợp với Slack/Telegram**:
   - Thêm node **Slack** hoặc **Telegram** để thông báo phản hồi mới cho team.
2. **Lưu log hoạt động**:
   - Sử dụng node **Sticky Note** để ghi lại lịch sử phản hồi.
3. **Gửi báo cáo định kỳ**:
   - Tạo một workflow khác để tự động gửi báo cáo tổng hợp đánh giá qua email (sử dụng node **Email**).
4. **Tùy chỉnh trang cảm ơn**:
   - Thêm hình ảnh logo hoặc thông tin liên hệ vào trang **"Feedback Submitted HTML"**.
5. **Phân tích dữ liệu**:
   - Sử dụng **Data Table** kết hợp với node **Google Sheets** hoặc **Airtable** để phân tích sâu hơn.
:::

---
### 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn tự động hóa quá trình thu thập đánh giá sao từ khách hàng **một cách đơn giản, không cần code và không phụ thuộc vào dịch vụ bên thứ ba**. Với **Data Table tích hợp**, các sếp có thể dễ dàng theo dõi và phân tích phản hồi để cải thiện dịch vụ.

**Hãy áp dụng ngay và bắt đầu thu thập phản hồi từ khách hàng một cách tự động hóa!** 🚀

---
:::note[LƯU Ý CUỐI CUNG]
- Nếu gặp vấn đề, hãy kiểm tra:
  - **URL Webhook POST** có đúng không?
  - **Data Table schema** có khớp với dữ liệu đầu vào không?
  - **Webhook đã publish** chưa?
- Nếu cần hỗ trợ thêm, liên hệ với tác giả qua email: **office@sus-tech.at**.
:::