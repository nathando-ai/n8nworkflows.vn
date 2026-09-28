---
title: "🚀 Tự Động Hóa Proposal AI + Thanh Toán Stripe Sau Cuộc Hẹn Calendly - Giảm 90% Thời Gian Làm Thủ Công"
description: "Workflow tự động hóa hoàn toàn từ cuộc hẹn Calendly đến proposal AI cá nhân hóa, liên kết thanh toán Stripe và email follow-up tự động. Giúp các sếp bán hàng, tư vấn viên và doanh nghiệp dịch vụ đóng gói và thu tiền nhanh hơn chỉ trong vài giây sau mỗi cuộc gọi."
slug: "tieu-dong-hoa-proposal-ai-stripe-calendly"
tags: [n8n, automation, ai-summarization, crm, stripe, google-sheets, google-slides]
keywords: [n8n workflow tự động hóa, proposal AI, Calendly tự động hóa, Stripe thanh toán tự động, CRM Google Sheets, tự động hóa bán hàng]
---

# 🚀 **Tự Động Hóa Proposal AI + Thanh Toán Stripe Sau Cuộc Hẹn Calendly**

## **🔥 Nỗi Đau Của Các Sếp Khi Làm Thủ Công**
Hãy tưởng tượng:
- Sau mỗi cuộc gọi hẹn trên **Calendly**, các sếp phải:
  - **Tìm kiếm thông tin khách hàng** trong Google Sheets (hoặc CRM khác) để nhớ lại chi tiết cuộc trò chuyện.
  - **Viết proposal từ đầu** bằng tay, mất từ 30 phút đến 2 giờ cho mỗi khách hàng.
  - **Tạo liên kết thanh toán Stripe** và gửi email follow-up cá nhân hóa, dễ bị quên hoặc trễ hạn.
- Kết quả? **Khách hàng mất niềm tin**, doanh thu chậm, và quá trình bán hàng trở nên **rườn rãi, không chuyên nghiệp**.

**Workflow này giải quyết tất cả!** Với **AI + tự động hóa 100% không code**, các sếp sẽ:
✅ **Tạo proposal AI cá nhân hóa** chỉ trong vài giây sau cuộc gọi.
✅ **Tạo liên kết thanh toán Stripe tự động** và gửi email follow-up.
✅ **Đóng gói và thu tiền nhanh hơn**, giảm thời gian từ **30 phút/lần** xuống **5 giây/lần**.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS riêng.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (đủ sức mạnh cho workflow này)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian** so với viết proposal thủ công.
- **Tăng tỷ lệ chuyển đổi** với proposal AI cá nhân hóa và email follow-up tự động.
- **Thu tiền nhanh hơn** với liên kết Stripe được tạo tự động.
- **Chuyển đổi quá trình bán hàng** từ rườn rãi sang **máy móc**, giảm sai sót và tăng chuyên nghiệp.
- **Hoạt động 24/7** mà không cần can thiệp của con người.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
✔ **Tài khoản Calendly** (để nhận trigger khi khách hàng đặt lịch).
✔ **Google Sheets CRM** (để lưu thông tin khách hàng, ví dụ: tên, email, nhu cầu).
✔ **Google Drive** (để lưu template proposal Google Slides).
✔ **Tài khoản Stripe** (để tạo liên kết thanh toán).
✔ **Tài khoản Gmail** (để gửi email follow-up).
✔ **API Key OpenAI** (để AI tạo nội dung proposal).
✔ **Credentials OAuth2** cho:
   - Google Sheets
   - Google Slides
   - Google Drive
   - Calendly

---
:::note[LƯU Ý QUAN TRỌNG]
Nếu chưa có **API Key OpenAI**, các sếp có thể đăng ký miễn phí tại [OpenAI](https://platform.openai.com/) và tạo **API Key** trong tài khoản.
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể:
- **Tải file JSON** từ [n8n.io/workflows/12530](https://n8n.io/workflows/12530) và import vào **n8n Editor**.
- **Copy JSON** từ link trên và dán vào **Import Workflow** trong n8n.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này gồm **7 node chính**, các sếp cần cấu hình kỹ lưỡng như sau:

##### **🔹 Node 1: Calendly Trigger (Calendly Trigger Booked Meeting)**
- **Chọn Credentials**: `calendlyOAuth2Api` (đã cấu hình trước khi import).
- **Lưu ý**:
  - Đảm bảo **webhook URL** của n8n được đăng ký trong Calendly.
  - Node này sẽ **triggers** khi khách hàng đặt lịch.

##### **🔹 Node 2: Find Client Details From CRM (Google Sheets)**
- **Chọn Credentials**: `googleSheetsOAuth2Api`.
- **Cấu hình**:
  - **Sheet Name**: Tên sheet chứa dữ liệu khách hàng (ví dụ: "CRM").
  - **Range**: `Sheet1!A:Z` (hoặc cột chứa thông tin khách hàng).
  - **Query**: `SELECT * WHERE Email = "{{$json['email']}}"` (lấy thông tin khách hàng từ email trong cuộc gọi).

##### **🔹 Node 3: Generate Proposal Copy (OpenAI)**
- **Chọn Credentials**: `openAiApi`.
- **Cấu hình**:
  - **Model**: `gpt-3.5-turbo` (hoặc `gpt-4` nếu có).
  - **Prompt**: Sử dụng template mặc định (có thể tùy chỉnh):
    ```plaintext
    Tóm tắt cuộc gọi với khách hàng {{$json['name']}} (Email: {{$json['email']}}).
    Nội dung cuộc gọi: "{{$json['notes']}}".
    Viết một proposal bán hàng chuyên nghiệp, bao gồm:
    1. Giới thiệu dịch vụ.
    2. Giải pháp phù hợp với nhu cầu của khách hàng.
    3. Báo giá và ưu đãi.
    4. Hành động tiếp theo (Call-to-Action).
    ```
  - **Temperature**: `0.7` (để AI không quá ngẫu nhiên).

##### **🔹 Node 4: Create Proposal Template (Google Drive)**
- **Chọn Credentials**: `googleDriveOAuth2Api`.
- **Cấu hình**:
  - **File ID**: ID của template Google Slides (có thể copy từ URL file).
  - **Operation**: `copy` (tạo bản sao mới).

##### **🔹 Node 5: Customize Proposal (Google Slides)**
- **Chọn Credentials**: `googleSlidesOAuth2Api`.
- **Cấu hình**:
  - **File ID**: File Slides mới tạo ở node trước.
  - **Replace Text**:
    - **Old Text**: `{{PROPOSAL_CONTENT}}` (hoặc placeholder tùy chỉnh).
    - **New Text**: `${{$json['proposal']}}` (nội dung AI tạo).

##### **🔹 Node 6: Create Stripe Payment Link (HTTP Request)**
- **Chọn Credentials**: `stripeApi`.
- **Cấu hình**:
  - **Method**: `POST`.
  - **URL**: `https://api.stripe.com/v1/checkout/sessions`.
  - **Headers**:
    ```json
    {
      "Authorization": "Bearer {{$credentials['stripeApi']['apiKey']}}",
      "Content-Type": "application/x-www-form-urlencoded"
    }
    ```
  - **Body**:
    ```json
    {
      "payment_method_types[]": "card",
      "line_items[][price]": "{{$json['price_id']}}", // ID sản phẩm/giá trong Stripe
      "line_items[][quantity]": 1,
      "success_url": "https://bandoanhnghiep.com/thank-you?session_id={{CHECKOUT_SESSION_ID}}",
      "cancel_url": "https://bandoanhnghiep.com/cancel"
    }
    ```
  - **Lưu ý**: Thay `{{$json['price_id']}}` bằng ID sản phẩm thực tế trong Stripe.

##### **🔹 Node 7: Email Follow-up (Gmail)**
- **Chọn Credentials**: `gmailOAuth2`.
- **Cấu hình**:
  - **To**: `{{$json['email']}}` (email khách hàng).
  - **Subject**: `Proposal & Payment Link for {{$json['name']}}`.
  - **HTML Body**:
    ```html
    <p>Xin chào {{$json['name']}},</p>
    <p>Tôi đã tự động tạo proposal cho bạn sau cuộc gọi hôm nay:</p>
    <a href="{{$json['slides_link']}}">Xem Proposal</a><br>
    <a href="{{$json['stripe_link']}}">Thanh toán ngay</a><br>
    <p>Nếu có thắc mắc, hãy liên hệ tôi qua email hoặc số điện thoại.</p>
    <p>Trân trọng,</p>
    <p>Tên của bạn</p>
    ```
  - **Lưu ý**: Thay `{{$json['slides_link']}}` và `{{$json['stripe_link']}}` bằng liên kết thực tế từ node trước.

#### **3. Kích Hoạt ⚡️**
- **Test Run**: Chạy thử với dữ liệu mẫu (ví dụ: một cuộc gọi giả).
- **Bật Active**: Sau khi kiểm tra, bật **Active** để workflow chạy tự động.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết hợp với Slack/Telegram**:
   - Thêm node **Slack Webhook** hoặc **Telegram Bot** để thông báo khi proposal được tạo thành công.
   - Ví dụ:
     ```json
     {
       "text": `Proposal for {{$json['name']}} đã được tạo: <${$json['slides_link']}|Xem Proposal>`
     }
     ```

2. **Lưu Log Tất Cả Các Cuộc Gọi**:
   - Thêm node **StickyNote** để ghi lại tất cả thông tin cuộc gọi (email, tên, nội dung, thời gian) vào một sheet Google Sheets riêng.

3. **Gửi Báo Cáo Định Kỳ**:
   - Sử dụng **n8n + Google Sheets** để tạo báo cáo hàng tuần về:
     - Số lượng proposal tạo.
     - Tỷ lệ chuyển đổi thanh toán.
     - Thời gian phản hồi trung bình.

4. **Tùy Chỉnh Prompt AI**:
   - Nếu muốn proposal **chuyên nghiệp hơn**, thay đổi prompt ở node OpenAI:
     ```plaintext
     Tôi là một chuyên gia bán hàng. Viết một proposal bán hàng chuyên nghiệp, ngắn gọn và thuyết phục cho khách hàng {{$json['name']}}.
     Nội dung cuộc gọi: "{{$json['notes']}}".
     ```

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp từ việc làm thủ công, giúp **tăng tỷ lệ chuyển đổi** và **tự động hóa toàn bộ quy trình bán hàng** từ cuộc gọi đến thanh toán. **Chỉ cần đặt lịch trên Calendly, mọi thứ sẽ tự động xảy ra!**

**Hành động ngay**:
1. **Import workflow** vào n8n của mình.
2. **Cấu hình các credentials** (Google, Stripe, OpenAI).
3. **Test run** và bật **Active** để bắt đầu tự động hóa!

**🚀 CÓ THỂ CẦN GỌI TRỢ GIÚP?**
Nếu gặp khó khăn trong quá trình setup, các sếp có thể liên hệ tác giả **Cliss Zhang** qua email: [qufeizzz@gmail.com](mailto:qufeizzz@gmail.com).

---
**💡 Mẹo cuối**: Nếu muốn **tăng hiệu quả**, các sếp có thể kết hợp với **CRM khác** như Airtable hoặc HubSpot bằng cách thay thế node Google Sheets.