---
title: "🚀 Hệ Thống Trả Lời Lead Tự Động Theo Giờ Làm Việc (Gmail + Google Sheets + Telegram Alert)"
description: "Tự động hóa trả lời lead qua email (theo giờ làm việc) và gửi thông báo Telegram cho team, giảm thiểu thời gian phản hồi và cải thiện trải nghiệm khách hàng. Workflow hoạt động 24/7, không cần code."
slug: "huyet-thong-lead-tran-lai-gio-lam-viec"
tags: [n8n, automation, no-code, gmail, google-sheets, telegram, business-hours]
keywords: [n8n workflow lead response, tự động hóa trả lời email, giờ làm việc tự động, google sheets trigger, telegram alert]
---

# 🚀 **Hệ Thống Trả Lời Lead Tự Động Theo Giờ Làm Việc (Gmail + Google Sheets + Telegram Alert)**

### **Giải pháp cho các sếp:**
Bạn đã bao giờ phải chờ đợi phản hồi từ khách hàng trong giờ nghỉ hoặc cuối tuần? Hoặc phải lo lắng rằng lead mới sẽ bị bỏ qua khi team không trực? **Workflow này sẽ giải quyết tất cả những vấn đề đó!**

Với **Business Hours Lead Response System**, các sếp có thể:
✅ **Tự động trả lời lead** qua email ngay lập tức (nếu trong giờ làm việc) hoặc thông báo sẽ trả lời vào ngày làm việc tiếp theo (nếu ngoài giờ).
✅ **Gửi thông báo Telegram** cho team ngay khi có lead mới, giúp không một lead nào bị bỏ qua.
✅ **Quản lý lead hiệu quả** bằng Google Sheets, đồng thời theo dõi tất cả các tương tác tự động.
✅ **Tiết kiệm thời gian** cho team, giảm thiểu công việc lặp lại và cải thiện trải nghiệm khách hàng.

---
### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Phản hồi nhanh chóng** (trong giờ làm việc) hoặc **quản lý kỳ vọng khách hàng** (ngoài giờ làm việc).
- **Không bỏ qua lead nào** nhờ thông báo Telegram tức thời cho team.
- **Dữ liệu lead được tự động cập nhật** trên Google Sheets, dễ dàng theo dõi và phân tích.
- **Hoạt động 24/7** mà không cần can thiệp thủ công.
- **Tiết kiệm thời gian** cho team, tập trung vào công việc có giá trị cao hơn.
:::

---
### 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Gmail** (đã cấp quyền OAuth2 cho n8n):
   - Tạo **OAuth2 Credential** trong n8n với tài khoản Gmail chính thức của doanh nghiệp.
   - Đảm bảo email này có thể gửi và nhận email tự động (không bị đánh dấu là spam).
2. **Google Sheets** (đã tạo và chia sẻ):
   - Một bảng Google Sheets để lưu trữ lead (cấu trúc bao gồm cột: **Name, Email, Timestamp, Status**).
   - **Chia sẻ bảng với n8n** bằng cách cấp quyền "Sửa" cho `googleSheetsTriggerOAuth2Api`.
3. **Tài khoản Telegram Bot**:
   - Tạo một bot Telegram mới tại [@BotFather](https://t.me/BotFather) và lấy **API Token**.
   - Thêm bot vào một **chat group** hoặc **channel** riêng để nhận thông báo lead.
4. **n8n Self-hosted** (khuyến nghị):
   - Workflow này hoạt động ổn định nhất khi cài trên **VPS riêng** (self-hosted).
   - 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
   - 👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/8282) hoặc copy toàn bộ JSON từ trang này.
- Trong **n8n Editor**, chọn **Import Workflow** và dán JSON vào.
- **Kiểm tra cấu trúc** trước khi kích hoạt:
  ```json
  {
    "nodes": [
      // Danh sách nodes sẽ tự động hiện ra khi import
    ],
    "connections": [
      // Các kết nối giữa nodes
    ]
  }
  ```

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
##### **🔹 Node 1: Google Sheets Trigger1**
- **Cấu hình OAuth2**:
  - Chọn **googleSheetsTriggerOAuth2Api** trong **Credentials**.
  - Chọn **Sheet Name** (tên bảng Google Sheets bạn đã tạo).
  - **Chọn cột trigger**: Bạn cần chỉ định **cột nào sẽ kích hoạt workflow** (ví dụ: cột `Status` khi được cập nhật từ `New` sang `Processed`).
- **Lưu ý**:
  - Workflow sẽ **poll (lấy dữ liệu) mỗi 1 phút**, nên không cần lo lắng về lead bị bỏ qua.

##### **🔹 Node 3: Check Business Hours**
- **Mở Function Node** và chỉnh sửa mã JavaScript (nếu cần):
  ```javascript
  // Giờ làm việc mặc định: Thứ 2-Thứ 6, 9:00-18:00
  const isBusinessHours = (date) => {
    const day = date.getDay(); // 1 (Thứ 2) - 5 (Thứ 6)
    const hour = date.getHours();
    return day >= 1 && day <= 5 && hour >= 9 && hour <= 18;
  };

  const timestamp = $input.all()[0].json.timestamp; // Lấy timestamp từ Google Sheets
  const date = new Date(timestamp * 1000); // Chuyển đổi từ Excel timestamp sang JS Date

  $node.setOutputData({
    isBusinessHours: isBusinessHours(date),
    formattedTime: date.toLocaleString('vi-VN', { weekday: 'long', hour: '2-digit', minute: '2-digit' })
  });
  ```
  - **Thay đổi giờ làm việc** theo nhu cầu của doanh nghiệp (ví dụ: 8:00-17:00).

##### **🔹 Node 5 & 7: Send Gmail (Business Hours / After Hours)**
- **Chọn tài khoản Gmail**:
  - Trong **Credentials**, chọn `gmailOAuth2` (đã cấu hình trước).
- **Tùy chỉnh nội dung email**:
  - Mở **Email Template** trong node và chỉnh sửa:
    - **Business Hours**:
      ```html
      <p>Xin chào {{ $json.firstName }},</p>
      <p>Cảm ơn bạn đã liên hệ với chúng tôi! Chúng tôi sẽ phản hồi trong vòng 24 giờ.</p>
      ```
    - **After Hours**:
      ```html
      <p>Xin chào {{ $json.firstName }},</p>
      <p>Cảm ơn bạn đã liên hệ! Do đang ngoài giờ làm việc, chúng tôi sẽ phản hồi vào ngày mai ({{ $json.formattedTime }})</p>
      ```
  - **Thêm các biến** như `lastName`, `email` nếu cần.

##### **🔹 Node 8: Notify Telegram**
- **Cấu hình bot**:
  - Trong **Credentials**, chọn `telegramApi` và điền **API Token** từ BotFather.
  - **Chọn chat ID**: Nhập **ID của chat/group** bạn muốn nhận thông báo (có thể tìm bằng cách gửi tin nhắn từ bot và copy link chat).
- **Tùy chỉnh thông báo**:
  ```markdown
  **📩 Lead mới được xử lý!**
  - **Tên**: {{ $json.firstName }} {{ $json.lastName }}
  - **Email**: {{ $json.email }}
  - **Thời gian**: {{ $json.formattedTime }}
  - **Trạng thái**: {{ $json.isBusinessHours ? "Trong giờ làm việc" : "Ngoài giờ" }}
  ```

---
#### **3. Kích hoạt ⚡️**
1. **Test Run** với một lead mẫu:
   - Thêm một lead vào Google Sheets (cột `Status = New`).
   - Kiểm tra email và Telegram để đảm bảo workflow hoạt động.
2. **Bật Active**:
   - Chuyển trạng thái workflow từ **Inactive** sang **Active**.

---
### ✍️ **Mẹo & gợi ý nâng cao**
:::info[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Kết hợp với Slack**:
   - Thêm node **Slack** để gửi thông báo cho team thay vì Telegram (hoặc cả hai).
   ```javascript
   // Thêm vào Node 8 (Notify Telegram)
   const slackMessage = {
     text: `📩 Lead mới: ${json.firstName} ${json.lastName} (${json.email})`,
     attachments: [{
       title: "Trạng thái",
       text: json.isBusinessHours ? "🔴 Trong giờ làm việc" : "🟢 Ngoài giờ",
       color: json.isBusinessHours ? "#FF0000" : "#00FF00"
     }]
   };
   $node.setOutputData(slackMessage);
   ```

2. **Lưu log hoạt động**:
   - Thêm node **Google Sheets (Append Row)** để ghi lại tất cả các lead đã xử lý, bao gồm:
     - Thời gian phản hồi.
     - Trạng thái (trong/ngoài giờ).
     - Người xử lý (nếu team có nhiều người).

3. **Gửi báo cáo định kỳ**:
   - Sử dụng **n8n Cron Trigger** để gửi báo cáo hàng tuần về số lead, thời gian phản hồi trung bình qua email.

4. **Tích hợp với CRM**:
   - Thay vì Google Sheets, bạn có thể sử dụng **HubSpot**, **Zoho CRM** hoặc **Salesforce** để quản lý lead.

5. **Tự động phân loại lead**:
   - Sử dụng **AI Node** (n8n-nodes-ai) để phân loại lead theo nội dung email (ví dụ: lead mua hàng, hỗ trợ kỹ thuật).
:::

---
### 📌 **Kết luận**
**Workflow này không chỉ tiết kiệm thời gian mà còn cải thiện trải nghiệm khách hàng** bằng cách đảm bảo phản hồi nhanh chóng và quản lý kỳ vọng một cách chuyên nghiệp. **Không cần code, không cần chuyên gia IT**, các sếp chỉ cần import và cấu hình một chút là có thể tự động hóa toàn bộ quy trình trả lời lead!

👉 **Bắt đầu ngay hôm nay**:
1. **Import workflow** từ [đây](https://n8n.io/workflows/8282).
2. **Cấu hình Gmail, Google Sheets và Telegram**.
3. **Bật Active** và xem team của bạn không còn phải lo lắng về lead nữa!

**Cần hỗ trợ?** Đừng ngần ngại comment bên dưới hoặc liên hệ với cộng đồng n8n tại [Discord](https://discord.gg/n8n). 🚀