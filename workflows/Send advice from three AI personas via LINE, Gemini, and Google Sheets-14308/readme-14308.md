---
title: "🚀 Tự Động Hóa Bot LINE Trả Lời Như 3 Nhân Vật AI Khác Nhau (Fortune Teller, Business Coach & Best Friend) Với Gemini & Google Sheets"
description: "Workflow này giúp các sếp xây dựng một bot LINE thông minh trả lời mọi câu hỏi/lo lắng của khách hàng bằng 3 nhân vật AI khác biệt (phù thủy, cố vấn kinh doanh và bạn thân), đồng thời tự động lưu lịch sử vào Google Sheets. Giúp cải thiện trải nghiệm khách hàng và phân tích hành vi 24/7 mà không cần code."
slug: "tieu-dong-hoa-bot-line-3-nhan-vat-ai-voi-gemini"
tags: [n8n, automation, no-code, ai-chatbot, line-bot, google-sheets, google-gemini]
keywords: [tự động hóa bot LINE, AI trả lời tự động, Google Gemini n8n, lưu lịch sử chatbot, chatbot 3 nhân vật, n8n workflow LINE]
---

# 🚀 **Bot LINE Trả Lời Như 3 Nhân Vật AI Khác Nhau: Fortune Teller, Business Coach & Best Friend**

Hiện nay, khi khách hàng gửi tin nhắn đến bot LINE của doanh nghiệp, họ thường chỉ nhận được câu trả lời chung chung từ một AI duy nhất. Điều này khiến trải nghiệm trở nên **lặp đi lặp lại và thiếu cá nhân hóa**. Workflow này là giải pháp **tự động hóa 100% không cần code** giúp các sếp:
✅ **Tạo ra 3 nhân vật AI khác biệt** (phù thủy, cố vấn kinh doanh và bạn thân) trả lời cùng một câu hỏi với phong cách riêng.
✅ **Lưu tất cả lịch sử tương tác** vào Google Sheets để phân tích hành vi khách hàng.
✅ **Tiết kiệm thời gian** lên đến **90%** so với cách làm thủ công.
✅ **Hoạt động liên tục 24/7** mà không cần can thiệp của con người.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động ổn định và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS riêng để đảm bảo tính bảo mật và hiệu suất cao.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Trải nghiệm khách hàng nâng cao**: Khách hàng cảm thấy được **lắng nghe và hiểu rõ hơn** nhờ 3 nhân vật AI khác biệt.
- **Tiết kiệm thời gian**: Không cần phải viết code hoặc quản lý nhiều bot riêng lẻ.
- **Dữ liệu phân tích chi tiết**: Tất cả lịch sử chat được lưu vào Google Sheets, giúp các sếp **hiểu rõ hành vi khách hàng** và cải thiện chiến lược.
- **Hoạt động tự động**: Bot hoạt động **24/7** mà không cần can thiệp của con người.
- **Cá nhân hóa cao**: Mỗi nhân vật AI có **phong cách trả lời riêng**, từ nghiêm túc (Business Coach) đến thân mật (Best Friend).
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản LINE Developer**:
   - Đăng ký tại [LINE Developers](https://developers.line.biz/) và tạo **Channel Access Token**.
   - Cài đặt **Messaging API** cho bot LINE của mình.
2. **API Key Google Gemini**:
   - Đăng ký tại [Google AI Studio](https://aistudio.google.com/) và lấy **API Key** cho Gemini.
3. **Google Sheets**:
   - Tạo một bảng Google Sheets với **tên Sheet là `advice_history`**.
   - Cột đầu tiên phải có các tiêu đề sau:
     ```
     Timestamp | User ID | Message | Fortune Teller | Business Coach | Best Friend
     ```
4. **n8n Self-hosted**:
   - Cài đặt n8n trên VPS (không dùng phiên bản cloud để đảm bảo bảo mật).

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Tải workflow từ [n8n.io/workflows/14308](https://n8n.io/workflows/14308).
2. Nhấn **Import** trong n8n Editor và chọn file JSON.
3. Hoặc copy toàn bộ JSON và dán vào **Import Workflow** trong giao diện.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Sau khi import, các sếp cần **cấu hình các node quan trọng** như sau:

##### **A. Node "Set config" (Cấu hình chung)**
- **Điền các tham số sau**:
  - `LINE_TOKEN`: Channel Access Token từ LINE Developers.
  - `GEMINI_API_KEY`: API Key từ Google AI Studio.
  - `SHEET_ID`: ID của Google Sheets (tham khảo cách lấy ở [Google Sheets API Guide](https://developers.google.com/sheets/api/quickstart/python)).
  - `WEBHOOK_PATH`: Đặt là `line-three-advisors` (không thay đổi).

##### **B. Node "Receive LINE message" (Nhận tin nhắn LINE)**
- **Không cần chỉnh sửa**, chỉ đảm bảo **webhook URL** của LINE được liên kết đúng với n8n.

##### **C. Node "Google Gemini Chat Model" (Gọi API Gemini)**
- **Không cần cấu hình thêm**, chỉ cần đảm bảo `GEMINI_API_KEY` đã điền đúng trong node "Set config".

##### **D. Node "Save advice to Sheets" (Lưu vào Google Sheets)**
- **Kiểm tra credentials**:
  - Chọn `googleSheetsOAuth2Api` (nếu chưa có, tạo mới trong n8n).
  - Đảm bảo **Google Sheets** đã được chia sẻ với tài khoản OAuth2 của n8n.

##### **E. Node "Send Flex Message to LINE" (Gửi phản hồi Flex Message)**
- **Không cần chỉnh sửa**, chỉ cần đảm bảo `LINE_TOKEN` đã điền đúng.

#### **3. Kích hoạt ⚡️**
1. **Test run dữ liệu mẫu**:
   - Gửi một tin nhắn test đến bot LINE (ví dụ: *"Tôi đang lo lắng về việc kinh doanh"*).
   - Kiểm tra phản hồi từ bot có phải là **3 nhân vật AI khác biệt** không.
2. **Bật Active workflow**:
   - Nhấn **Active** trên workflow để bot hoạt động liên tục.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Thêm Slack/Telegram Notifications**:
   - Sử dụng node **Slack** hoặc **Telegram Bot** để thông báo khi có tin nhắn mới.
2. **Lưu log chi tiết**:
   - Thêm node **Set** sau "Save advice to Sheets" để lưu thêm thông tin như **thời gian phản hồi** vào Sheets.
3. **Cập nhật nhân vật AI**:
   - Sử dụng **LangChain** để thay đổi prompt cho mỗi nhân vật (ví dụ: phong cách nghiêm túc hơn cho Business Coach).
4. **Phân tích dữ liệu tự động**:
   - Sử dụng **Google Apps Script** để tự động tạo báo cáo từ Sheets hàng tuần.

---

### 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn **tự động hóa bot LINE** với **3 nhân vật AI khác biệt**, đồng thời **lưu dữ liệu chi tiết** để phân tích. Không cần code, không cần chuyên gia AI, chỉ cần **cấu hình vài bước đơn giản** là bot đã hoạt động 24/7, mang lại **trải nghiệm khách hàng cá nhân hóa** và **dữ liệu phân tích mạnh mẽ**.

**Hãy áp dụng ngay và nâng cao hiệu suất bot LINE của mình!** 🚀

---
**🔗 [Tải workflow từ n8n.io](https://n8n.io/workflows/14308)**
**📌 [Hướng dẫn chi tiết trên GitHub](https://github.com/n8n-io/workflows/tree/main/workflows/14308)**