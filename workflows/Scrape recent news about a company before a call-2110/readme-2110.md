---
title: "📰 **Tự Động Hóa Lấy Tin Tức Mới Nhất Về Công Ty Trước Cuộc Gặp (N8n Workflow)**"
description: "Workflow tự động hóa lấy tin tức mới nhất về công ty đối tác trước mỗi cuộc họp, giúp các sếp cập nhật thông tin nhanh chóng và chuẩn bị tốt hơn cho cuộc gọi. Giúp tiết kiệm thời gian, tăng cường sự chuyên nghiệp và cạnh tranh trong giao dịch."
slug: "tieu-dong-hoa-lay-tin-tuc-moi-nhat-ve-cong-ty-truoc-cuoc-gap"
tags: [n8n, automation, sales, no-code, google-calendar]
keywords: [n8n workflow tự động hóa, lấy tin tức công ty, tự động hóa cuộc họp, cập nhật tin tức trước cuộc gọi, n8n sales automation]
---

# 🚀 **Tự Động Hóa Lấy Tin Tức Mới Nhất Về Công Ty Trước Mỗi Cuộc Gặp**

### **Giải Phẫu Nỗi Đau Của Các Sếp Trong Cuộc Gặp**
Bạn có bao giờ phải ngồi trước một cuộc họp quan trọng với một công ty đối tác, nhưng lại không có thời gian để cập nhật tin tức mới nhất về họ? Hay phải mất nhiều giờ để tìm kiếm thông tin trên Google, chỉ để phát hiện ra rằng công ty đối tác vừa có một sự kiện quan trọng, thay đổi lãnh đạo, hoặc phát triển sản phẩm mới? **Workflow này sẽ giải quyết vấn đề đó 100% tự động hóa, chỉ trong vài giây mỗi sáng!**

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần tìm kiếm thủ công trước mỗi cuộc họp.
- **Cập nhật tin tức mới nhất**: Nhận được thông tin chính xác về công ty đối tác trong vòng 24h.
- **Chuẩn bị chuyên nghiệp**: Bắt đầu cuộc họp với kiến thức sâu về đối tác, tăng cường uy tín.
- **Hoạt động tự động**: Workflow chạy hàng ngày, không cần can thiệp thủ công.
- **Tối ưu hóa giao dịch**: Nhận biết cơ hội hoặc rủi ro mới từ tin tức, giúp quyết định sáng suốt hơn.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **API Key của News API** (đăng ký miễn phí tại [newsapi.org](https://newsapi.org)).
2. **Tài khoản Gmail** (để gửi email tự động).
3. **Tài khoản Google Calendar** (để lấy danh sách cuộc họp).
4. **Danh sách email** (các địa chỉ email cần nhận tin tức, cách nhau bởi dấu phẩy).
5. **Tham số tùy chỉnh**:
   - `newsAge`: Tuổi tin tức (tính bằng ngày, ví dụ: 3 ngày).
   - `maxArticles`: Số bài báo tối đa gửi (không quá 100).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Bước 1**: Tải file JSON của workflow từ [n8n.io/workflows/2110](https://n8n.io/workflows/2110).
- **Bước 2**: Mở n8n Editor và nhấn **"Import"** → Chọn file JSON vừa tải.
- **Bước 3**: Workflow sẽ hiển thị trên canvas với 9 node.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
##### **a. Cấu Hình Node "Setup" (Set)**
- Điền các tham số cơ bản:
  - `apiKey`: API Key của News API (đăng ký tại [newsapi.org](https://newsapi.org)).
  - `newsAge`: Số ngày tin tức được lấy (ví dụ: `3` để lấy tin tức trong 3 ngày qua).
  - `maxArticles`: Số bài báo tối đa gửi (không quá 100).
  - `emails`: Danh sách email (ví dụ: `sếp1@example.com,sếp2@example.com`).

##### **b. Cấu Hình Node "Get meetings for today" (Google Calendar)**
- **Credentials**: Chọn `googleCalendarOAuth2Api` (cần cấu hình OAuth2 cho Google Calendar trước).
- **Operation**: Đảm bảo chọn `getAll`.
- **Filter**: Workflow mặc định lấy cuộc họp bắt đầu với từ khóa *"Meeting with"* hoặc *"Call with"*. Các sếp có thể chỉnh sửa filter này trong node **Filter meetings** (If) nếu cần.

##### **c. Cấu Hình Node "Send news" (Gmail)**
- **Credentials**: Chọn `gmailOAuth2` (cần cấu hình OAuth2 cho Gmail trước).
- **Email To**: Sẽ tự động lấy từ danh sách `emails` trong node Setup.
- **Subject**: Mặc định là *"Latest News for [Company Name]"*.
- **Body**: Nội dung email sẽ được format tự động từ node **Format for email** (Code).

##### **d. Node "Filter meetings" (If)**
- **Condition**: Workflow sẽ chỉ gửi email nếu có cuộc họp trong ngày. Nếu không có cuộc họp, node **No meetings today** (NoOp) sẽ hoạt động và không gửi email.

##### **e. Node "Get latest news" (HTTP Request)**
- **URL**: Workflow sẽ tự động xây dựng URL lấy tin tức từ API News API dựa trên công ty được lấy từ node **Extract company name** (Set).
- **Headers**: Đảm bảo thêm `Authorization: Bearer {apiKey}`.

##### **f. Node "Format for email" (Code)**
- **Script**: Workflow sử dụng mã JavaScript để format tin tức thành email dễ đọc. Các sếp không cần chỉnh sửa nếu không muốn.

#### **3. Kích Hoạt ⚡️**
- **Bước 1**: Nhấn **"Test Run"** để kiểm tra workflow với dữ liệu mẫu.
- **Bước 2**: Sau khi kiểm tra thành công, nhấn **"Active"** để bật workflow.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tùy Chỉnh Filter Cuộc Hợp**:
   - Nếu muốn lấy cuộc họp với từ khóa khác (ví dụ: *"Business Meeting"* hoặc *"Client Call"*), chỉnh sửa node **Filter meetings** (If) bằng cách thay đổi điều kiện:
     ```json
     "condition": {
       "jsonPath": "$[*]",
       "operator": "contains",
       "value": "Business Meeting"
     }
     ```

2. **Gửi Tin Tức Đến Slack/Telegram**:
   - Thay thế node **Send news** (Gmail) bằng node **Slack Webhook** hoặc **Telegram Bot** để gửi tin tức qua kênh thông báo khác.

3. **Lưu Log Tin Tức**:
   - Thêm node **Google Sheets** hoặc **Notion** sau node **Format for email** để lưu tin tức vào bảng tính hoặc trang wiki cho tham khảo lâu dài.

4. **Tùy Chỉnh Thời Gian Gửi Email**:
   - Thay đổi node **Every morning @ 7** (Schedule Trigger) để gửi email vào thời gian phù hợp (ví dụ: 6h sáng hoặc 17h chiều).

5. **Kết Hợp Với CRM**:
   - Nếu sử dụng CRM như HubSpot, Salesforce, hoặc Zoho, các sếp có thể thêm node **CRM API** để cập nhật tin tức mới nhất vào hồ sơ công ty đối tác.

---

### 📌 **Kết Luận**
Workflow này là **công cụ không thể thiếu** cho các sếp, doanh nhân, hoặc chuyên gia bán hàng muốn bắt đầu mỗi cuộc họp với kiến thức sâu về đối tác. **Chỉ cần cấu hình một lần, workflow sẽ tự động chạy hàng ngày**, giúp bạn **tiết kiệm thời gian, tăng cường chuyên nghiệp và cạnh tranh** trong giao dịch.

**Hãy áp dụng ngay và bắt đầu cuộc họp với sự tự tin hơn!** 🚀

---
**Ghi chú**: Nếu gặp vấn đề trong quá trình cấu hình, các sếp có thể tham khảo [hướng dẫn OAuth2 cho Gmail](https://docs.n8n.io/integrations/builtins/nodes/Gmail/) và [Google Calendar](https://docs.n8n.io/integrations/builtins/nodes/GoogleCalendar/).