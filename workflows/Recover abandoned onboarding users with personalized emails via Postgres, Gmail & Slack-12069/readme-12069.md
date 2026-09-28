---
title: "🚀 Tự Động Hồi Phục Người Dùng Bỏ Cuộc Onboarding Bằng Email Cá Nhân Hóa (Postgres + Gmail + Slack)"
description: "Workflow tự động hóa hoàn toàn để tìm kiếm và hồi phục người dùng đã bỏ dở quá trình onboarding, gửi email cá nhân hóa, cập nhật trạng thái và thông báo cho đội ngũ bán hàng - tiết kiệm thời gian và tăng tỷ lệ chuyển đổi cho SaaS."
slug: "tieu-dong-hoi-phuc-nguoi-dung-bo-cuoc-onboarding"
tags: [n8n, automation, lead-nurturing, saas, postgresql, gmail, slack, inboxplus, no-code]
keywords: [tự động hóa n8n, hồi phục người dùng saas, email cá nhân hóa, tự động hóa bán hàng, workflow postgresql, tự động hóa slack, giảm thiểu bỏ cuộc onboarding]
---

# 🚀 **Tự Động Hồi Phục Người Dùng Bỏ Cuộc Onboarding Bằng Email Cá Nhân Hóa**

### **Giải pháp hoàn toàn tự động hóa để hồi phục người dùng đã bỏ dở onboarding**
Có bao giờ các sếp cảm thấy đau đầu vì mất hàng chục giờ mỗi tuần để theo dõi và hồi phục người dùng bỏ dở quá trình onboarding? Hay phải nhớ nhắc nhở từng khách hàng cá nhân qua email, Slack, hoặc gọi điện? **Workflow này sẽ tự động hóa toàn bộ quy trình đó**, giúp các sếp:
- **Tìm kiếm và hồi phục người dùng bỏ dở onboarding** chỉ trong vài giây mỗi ngày.
- **Gửi email cá nhân hóa** với nội dung động, tăng tỷ lệ mở và tương tác.
- **Cập nhật trạng thái người dùng** trong cơ sở dữ liệu để tránh gửi email trùng lặp.
- **Thông báo ngay cho đội ngũ bán hàng** khi có người dùng cần hỗ trợ, giúp họ tập trung vào khách hàng tiềm năng có khả năng chuyển đổi cao nhất.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không phải theo dõi thủ công hàng trăm người dùng bỏ dở onboarding.
- **Tăng tỷ lệ hồi phục**: Email cá nhân hóa và thông báo Slack giúp đội ngũ bán hàng phản hồi kịp thời.
- **Tránh gửi email trùng lặp**: Cập nhật trạng thái người dùng trong cơ sở dữ liệu để tránh gửi nhiều lần.
- **Hoạt động liên tục**: Workflow chạy tự động hàng ngày, không cần can thiệp của con người.
- **Tăng doanh thu**: Hồi phục người dùng bỏ dở = tăng tỷ lệ chuyển đổi và giá trị trung bình mỗi khách hàng.
:::

---

## 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản và API Key**:
   - **PostgreSQL**: Địa chỉ server, tên database, tên bảng `Users`, và credentials để truy cập.
   - **Gmail**: Tài khoản Gmail để gửi email (cần kích hoạt **Less Secure Apps** hoặc sử dụng OAuth2).
   - **Slack**: Token OAuth2 và channel cụ thể để thông báo.
   - **InboxPlus** (nếu sử dụng): API Key để chuẩn bị email cá nhân hóa (nếu không có, có thể thay thế bằng **n8n-nodes-base.email** hoặc **n8n-nodes-base.llm**).

2. **Cấu trúc bảng `Users` trong PostgreSQL**:
   - Cần có các cột như: `user_id`, `email`, `onboarding_status` (ví dụ: `pending`, `completed`, `abandoned`), `last_activity_at`, `is_active`.

3. **Email Template**:
   - Nếu sử dụng **InboxPlus**, cần chuẩn bị template email cá nhân hóa (có thể sử dụng **n8n-nodes-base.llm** để tự động tạo nội dung động).

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Truy cập [n8n Editor](https://n8n.io/editor/) và tạo một workflow mới.
2. Nhấp vào **Import** và chọn file JSON (hoặc copy/paste JSON từ [link gốc](https://n8n.io/workflows/12069)).
3. Sau khi import, workflow sẽ hiển thị trên canvas với 10 node như mô tả.

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
#### **A. Cấu hình Node `Find Abandoned Users` (PostgreSQL)**
- **Credentials**: Chọn `postgres` đã cấu hình trước.
- **SQL Query**:
  ```sql
  SELECT * FROM users
  WHERE onboarding_status = 'pending'
  AND last_activity_at < NOW() - INTERVAL '24 HOURS'
  AND is_active = TRUE;
  ```
  - **Lưu ý**: Các sếp cần điều chỉnh query phù hợp với cấu trúc bảng của mình. Ví dụ:
    - Thay `onboarding_status = 'pending'` thành trạng thái bỏ dở onboarding của mình.
    - Thay `last_activity_at < NOW() - INTERVAL '24 HOURS'` thành điều kiện inactivity phù hợp (ví dụ: 48 giờ).

#### **B. Cấu hình Node `PrepareEmail` (InboxPlus)**
- **Credentials**: Chọn `inboxPlusApi` (nếu sử dụng InboxPlus).
- **Template**:
  - Nếu không có InboxPlus, các sếp có thể thay thế bằng **n8n-nodes-base.email** hoặc **n8n-nodes-base.llm** để tự động tạo email động.
  - **Ví dụ template email động** (sử dụng **n8n-nodes-base.llm**):
    ```json
    {
      "subject": "Chào lại, {{firstName}}! Chúng tôi nhớ bạn đang chuẩn bị sử dụng {{productName}}",
      "body": "Xin chào {{firstName}},\n\nChúng tôi thấy bạn đã bắt đầu quá trình onboarding nhưng chưa hoàn thành. Đừng bỏ cuộc! Hãy hoàn thành chỉ trong vài phút để trải nghiệm đầy đủ tính năng của {{productName}}.\n\n[Hoàn thành onboarding ngay]({{onboardingLink}})\n\nTrân trọng,\nĐội ngũ {{companyName}}"
    }
    ```

#### **C. Cấu hình Node `Send a message` (Gmail)**
- **Credentials**: Chọn `gmailOAuth2` đã cấu hình.
- **Tham số**:
  - **To**: `{{email}}` (trích từ kết quả PostgreSQL).
  - **Subject**: `{{subject}}` (từ template email).
  - **Body**: `{{body}}` (từ template email).

#### **D. Cấu hình Node `Alert Sales Team` (Slack)**
- **Credentials**: Chọn `slackOAuth2Api`.
- **Message**:
  ```json
  {
    "text": "🚨 Người dùng bỏ dở onboarding cần hỗ trợ!\n\n- **Email**: {{email}}\n- **Tên**: {{firstName}}\n- **Liên kết hồi phục**: {{onboardingLink}}",
    "blocks": [
      {
        "type": "section",
        "text": {
          "type": "mrkdwn",
          "text": "*Người dùng bỏ dở onboarding*\n*Email*: <{{email}}|{{email}}>\n*Tên*: {{firstName}}"
        }
      },
      {
        "type": "actions",
        "elements": [
          {
            "type": "button",
            "text": {
              "type": "plain_text",
              "text": "Hỗ trợ ngay"
            },
            "url": "{{onboardingLink}}"
          }
        ]
      }
    ]
  }
  ```

#### **E. Cấu hình Node `Update rows in a table` (PostgreSQL)**
- **Credentials**: Chọn `postgres`.
- **SQL Query**:
  ```sql
  UPDATE users
  SET onboarding_status = 'recovered_attempted',
      last_recovery_attempt = NOW()
  WHERE user_id = '{{user_id}}';
  ```
  - **Lưu ý**: Các sếp cần điều chỉnh query để cập nhật trạng thái người dùng sau khi gửi email (ví dụ: `onboarding_status = 'recovered_attempted'`).

#### **F. Cấu hình Node `Schedule Trigger`**
- **Tham số**:
  - **Frequency**: `Daily` (hoặc tùy chỉnh theo nhu cầu).
  - **Time**: Ví dụ: `09:00 AM` (thời gian phù hợp với đội ngũ bán hàng).

---

### **3. Kích hoạt ⚡️**
1. **Test run dữ liệu mẫu**:
   - Chọn node `Find Abandoned Users` và nhấp **Execute Node** với một người dùng mẫu (đảm bảo email và Slack token đã cấu hình đúng).
   - Kiểm tra:
     - Email có được gửi thành công không?
     - Thông báo Slack có hiển thị không?
     - Trạng thái người dùng có được cập nhật không?

2. **Bật Active workflow**:
   - Sau khi test thành công, nhấp **Activate** trên workflow.

---

## ✍️ **Mẹo & gợi ý nâng cao**
1. **Kết hợp với Slack Bot**:
   - Tạo một **Slack Bot** riêng để thông báo người dùng bỏ dở onboarding một cách tự động, ví dụ:
     ```json
     {
       "text": ":wave: Chúng tôi đã gửi email hồi phục cho bạn, {{firstName}}! Hãy hoàn thành onboarding để tiếp tục.",
       "username": "Onboarding Assistant"
     }
     ```

2. **Lưu log hoạt động**:
   - Thêm node **n8n-nodes-base.stickyNote** để ghi lại lịch sử hoạt động của workflow, ví dụ:
     ```json
     {
       "note": "Email hồi phục đã được gửi cho {{email}} tại {{timestamp}}"
     }
     ```

3. **Gửi báo cáo định kỳ**:
   - Sử dụng node **n8n-nodes-base.scheduleTrigger** để gửi báo cáo hàng tuần về số lượng người dùng hồi phục thành công qua email hoặc Slack.

4. **Tăng cường cá nhân hóa email**:
   - Sử dụng **n8n-nodes-base.llm** (OpenAI) để tự động tạo nội dung email động dựa trên hành vi của người dùng:
     ```json
     {
       "prompt": "Tạo một email hồi phục cá nhân hóa cho người dùng bỏ dở onboarding. Người dùng này đã tương tác với tính năng {{lastFeatureUsed}} và chưa hoàn thành bước {{pendingStep}}. Đảm bảo email ngắn gọn và động viên họ hoàn thành.",
       "model": "gpt-3.5-turbo"
     }
     ```

5. **Thêm bước xác nhận**:
   - Sau khi gửi email, thêm node **n8n-nodes-base.delay** (5-10 phút) trước khi cập nhật trạng thái người dùng, để đảm bảo email đã được gửi thành công.

---

## 📌 **Kết luận**
Workflow này là **giải pháp hoàn toàn tự động hóa** để hồi phục người dùng bỏ dở onboarding, giúp các sếp:
✅ **Tiết kiệm thời gian** và tập trung vào chiến lược phát triển sản phẩm.
✅ **Tăng tỷ lệ chuyển đổi** bằng email cá nhân hóa và thông báo kịp thời.
✅ **Tránh gửi email trùng lặp** và tối ưu hóa nguồn lực bán hàng.

**Hãy import workflow này ngay hôm nay và bắt đầu hồi phục người dùng bỏ dở chỉ trong vài phút mỗi ngày!** 🚀
Nếu có bất kỳ câu hỏi hoặc cần hỗ trợ, các sếp có thể liên hệ với **Avkash Kakdiya** (Founder của iTechNotion) qua [LinkedIn](https://www.linkedin.com/in/avkashkakdiya/) hoặc [website](https://itechnotion.com/).