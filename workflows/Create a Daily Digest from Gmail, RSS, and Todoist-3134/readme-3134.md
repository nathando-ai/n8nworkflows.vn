---
title: "📧 Tự Động Hoàn Thành Báo Cáo Hàng Ngày Từ Email, RSS & Todoist - Không Cần Code!"
description: "Workflow này tự động tổng hợp tin tức từ RSS (Times of India), email quan trọng và công việc Todoist thành một báo cáo hàng ngày định kỳ, gửi trực tiếp vào email cá nhân. Giúp các sếp tiết kiệm 2+ giờ mỗi ngày và không bỏ lỡ bất kỳ thông tin quan trọng nào."
slug: "tieu-dong-hoan-thanh-bao-cao-hang-ngay-tu-email-rss-todoist"
tags: [n8n, automation, no-code, gmail, todoist, rss, email-digest, productivity]
keywords: [n8n workflow tự động hóa, báo cáo hàng ngày tự động, tổng hợp tin tức RSS, tự động hóa Todoist, gửi email định kỳ, tiết kiệm thời gian]
---

# 🚀 **Tự Động Hoàn Thành Báo Cáo Hàng Ngày Từ Email, RSS & Todoist**

### **Giải pháp hoàn hảo cho các sếp bị "ngập" thông tin mỗi ngày**
Hiện nay, việc theo dõi email, tin tức từ RSS và công việc Todoist thường khiến các sếp mất **2-3 giờ mỗi ngày** để tổng hợp, lọc và gửi báo cáo. Kết quả? Thông tin quan trọng bị bỏ lỡ, năng suất giảm, và sự căng thẳng tăng cao.

**Workflow này tự động hóa toàn bộ quy trình:**
✅ **Tự động lấy tin tức** từ RSS (Times of India) và email quan trọng.
✅ **Tổng hợp công việc Todoist** vào báo cáo.
✅ **Định dạng và gửi báo cáo hàng ngày** vào email cá nhân.
✅ **Không cần code** – chỉ cần cấu hình vài bước đơn giản.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo tính riêng tư và hiệu suất cao.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 2-3 giờ mỗi ngày** để tập trung vào công việc chiến lược.
- **Không bỏ lỡ tin tức quan trọng** từ RSS và email.
- **Báo cáo Todoist tự động** – không cần nhớ ghi nhớ công việc.
- **Định kỳ và tự động hóa hoàn toàn** – không cần nhớ bật dây chuyền.
- **Cá nhân hóa** – báo cáo được định dạng theo sở thích cá nhân.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
✔ **Tài khoản Gmail** (để lấy email và gửi báo cáo).
✔ **Tài khoản Todoist** (để lấy công việc hàng ngày).
✔ **API Key Todoist** (mã API từ Todoist để kết nối).
✔ **Thời gian định kỳ** (ví dụ: 8h sáng hàng ngày).

---
:::info[CHUẨN BỊ]
1. **Cài đặt OAuth2 cho Gmail**:
   - Tạo **OAuth2 Credential** trong n8n với tài khoản Gmail.
   - Theo hướng dẫn [cài đặt OAuth2 cho Gmail](https://docs.n8n.io/integrations/builtins/nodes/Gmail.html#authentication) để n8n có quyền truy cập email.

2. **Lấy API Key Todoist**:
   - Đăng nhập Todoist → **Settings** → **Integrations** → **Create API Token**.
   - Sao chép mã API này để sử dụng trong workflow.

3. **Chọn RSS Feed**:
   - Workflow mặc định lấy tin tức từ **Times of India**, nhưng các sếp có thể thay đổi thành bất kỳ RSS Feed nào khác (ví dụ: TechCrunch, Bloomberg).
:::

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
- **Tải file JSON** từ [đây](https://n8n.io/workflows/3134) (hoặc sao chép JSON từ link trên).
- Trong **n8n Editor**, nhấn **Import** → Dán JSON → Chọn **Create Workflow**.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow gồm **7 node chính**, các sếp cần chú ý cấu hình như sau:

##### **A. Schedule Trigger (Định thời gian chạy)**
- Node này **khởi động workflow hàng ngày** tại thời gian đã chọn (ví dụ: 8h sáng).
- **Cấu hình**:
  - **Time**: Chọn giờ và ngày muốn chạy (ví dụ: `08:00:00` hàng ngày).
  - **Time Zone**: Chọn múi giờ phù hợp (ví dụ: `Asia/Ho_Chi_Minh`).
  - **Active**: Đảm bảo **bật** để workflow chạy tự động.

##### **B. RSS Feed: Times of India (Lấy tin tức)**
- Node này **tải tin tức từ RSS Feed** (mặc định là Times of India).
- **Cấu hình**:
  - **URL**: Đảm bảo URL RSS là chính xác (ví dụ: `https://timesofindia.indiatimes.com/rssfeeds/1000000000000000000000000000000000000000.rss`).
  - **Max Items**: Giới hạn số tin tức lấy (ví dụ: `5`).

##### **C. Gmail: Fetch Emails (Lấy email quan trọng)**
- Node này **lấy email từ Gmail** (cần cấu hình OAuth2 trước).
- **Cấu hình**:
  - **Credentials**: Chọn **gmailOAuth2** (đã tạo trước).
  - **Operation**: Chọn **getAll** (lấy tất cả email).
  - **Filter**: Các sếp có thể thêm **lọc email** (ví dụ: chỉ lấy email từ danh sách liên hệ quan trọng).
    - Ví dụ: `from:"support@example.com" OR from:"manager@example.com"`.

##### **D. Todoist: Fetch Tasks (Lấy công việc Todoist)**
- Node này **lấy công việc Todoist** (cần API Key Todoist).
- **Cấu hình**:
  - **Credentials**: Chọn **todoistApi** (đã tạo trước).
  - **Operation**: Chọn **getAll** (lấy tất cả công việc).
  - **Filter**: Các sếp có thể lọc công việc **chưa hoàn thành** (ví dụ: `status:open`).

##### **E. Merge (Kết hợp dữ liệu)**
- Node này **ghép tin tức, email và công việc Todoist** thành một danh sách duy nhất.
- **Cấu hình**:
  - **Merge Strategy**: Chọn **Array** (để kết hợp tất cả dữ liệu).
  - **Output**: Kiểm tra kết quả để đảm bảo dữ liệu được hợp nhất đúng.

##### **F. Format Digest: Merge & Style Data (Định dạng báo cáo)**
- Node này **sử dụng JavaScript để định dạng báo cáo** thành văn bản dễ đọc.
- **Cấu hình**:
  - **Code**:
    ```javascript
    // Dữ liệu đầu vào (tin tức, email, công việc Todoist)
    const rssItems = $input.all();
    const emails = $input.all();
    const todoItems = $input.all();

    // Định dạng báo cáo
    let digest = `📰 **BÁO CÁO HÀNG NGÀY** (${new Date().toLocaleDateString()})\n\n`;

    // Thêm tin tức RSS
    if (rssItems.length > 0) {
      digest += "📰 **TIN TỨC MỚI NHẤT:**\n";
      rssItems.forEach(item => {
        digest += `- [${item.title}](${item.link})\n`;
      });
      digest += "\n";
    }

    // Thêm email quan trọng
    if (emails.length > 0) {
      digest += "📧 **EMAIL QUAN TRỌNG:**\n";
      emails.forEach(email => {
        digest += `- Từ: ${email.from}\n`;
        digest += `  Chủ đề: ${email.subject}\n`;
        digest += `  Nội dung: ${email.snippet}\n\n`;
      });
    }

    // Thêm công việc Todoist
    if (todoItems.length > 0) {
      digest += "📋 **CÔNG VIỆC TODOIST:**\n";
      todoItems.forEach(task => {
        digest += `- ${task.content}\n`;
        digest += `  Trạng thái: ${task.status}\n\n`;
      });
    }

    return { json: { body: digest } };
    ```
  - **Lưu ý**: Nếu không quen với JavaScript, các sếp có thể **sao chép mã trên** và thay đổi nội dung theo ý muốn.

##### **G. Gmail: Send Digest (Gửi báo cáo)**
- Node này **gửi báo cáo đã định dạng** vào email cá nhân.
- **Cấu hình**:
  - **Credentials**: Chọn **gmailOAuth2** (đã tạo trước).
  - **To**: Điền email nhận báo cáo (ví dụ: `sếp@example.com`).
  - **Subject**: Thay đổi tiêu đề (ví dụ: `BÁO CÁO HÀNG NGÀY - ${new Date().toLocaleDateString()}`).
  - **Body**: Chọn **JSON Body** và chọn `body` từ node **Format Digest**.

---

#### **3. Kích hoạt ⚡️**
- **Test Run**: Nhấn **Run Workflow** để kiểm tra dữ liệu mẫu.
- **Active Workflow**: Sau khi kiểm tra, **bật Active** để workflow chạy tự động hàng ngày.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Thêm Slack/Telegram Notification**:
   - Sử dụng node **Slack** hoặc **Telegram Bot** để gửi báo cáo lên kênh chat.
   - Cấu hình:
     ```javascript
     // Thêm vào node Format Digest
     const slackMessage = `*BÁO CÁO HÀNG NGÀY* ${new Date().toLocaleDateString()}\n\n${digest}`;
     return { json: { body: digest }, slack: { text: slackMessage } };
     ```
   - Sau đó thêm node **Slack** hoặc **Telegram** để gửi thông báo.

2. **Lưu Log vào Google Sheets**:
   - Thêm node **Google Sheets** để lưu lịch sử báo cáo.
   - Cấu hình:
     - **Credentials**: Tạo **Google Sheets OAuth2**.
     - **Sheet Name**: Chọn sheet muốn lưu.
     - **Data**: Chọn `body` từ node **Format Digest**.

3. **Tùy chỉnh Thời Gian**:
   - Nếu các sếp muốn chạy workflow **2 lần/ngày** (ví dụ: sáng và chiều), thêm **Schedule Trigger** thứ 2 với thời gian khác.

4. **Lọc Email & Todoist Cẩn Thận**:
   - Để tránh **quá tải email**, các sếp có thể **lọc email** chỉ từ danh sách liên hệ quan trọng.
   - Ví dụ:
     ```javascript
     // Trong node Gmail: Fetch Emails
     const importantEmails = emails.filter(email =>
       email.from.includes("support@example.com") ||
       email.from.includes("manager@example.com")
     );
     return importantEmails;
     ```

---

### 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp để tập trung vào công việc chiến lược, đồng thời **không bỏ lỡ bất kỳ thông tin quan trọng nào** từ email, RSS và Todoist.

**Hành động ngay hôm nay:**
1. **Import workflow** vào n8n.
2. **Cấu hình OAuth2 Gmail** và **API Todoist**.
3. **Chạy test** và **bật Active**.
4. **Thưởng thức thời gian tự do** mỗi sáng!

---
**Chia sẻ và phản hồi:**
Nếu các sếp có **ý tưởng cải tiến** hoặc gặp **vấn đề trong quá trình setup**, hãy để lại bình luận bên dưới. Chúng tôi sẽ hỗ trợ miễn phí! 🚀

---
**#TựĐộngHóa #N8N #Productivity #NoCode**