---
title: "💾 **Tự Động Hoàn Hảo: Backup Workflow n8n Sang GitHub Với Thông Báo Email + Telegram (Không Cần Code!)**"
description: "Giải pháp tự động hóa hoàn toàn backup tất cả workflow n8n lên GitHub hàng ngày, đồng thời gửi thông báo tự động qua Email và Telegram. Đảm bảo an toàn dữ liệu và dễ dàng phục hồi khi cần."
slug: "tự-dộng-hoàn-hảo-backup-workflow-n8n-sang-github"
tags: [n8n, automation, devops, github, backup, telegram, email, no-code]
keywords: [backup workflow n8n, tự động hóa devops, lưu trữ workflow git, thông báo telegram email, tự động hóa n8n, backup dữ liệu n8n]
---

# 🚀 **Backup Workflow n8n Sang GitHub Với Thông Báo Tự Động (Email + Telegram)**

### **🔥 Nỗi Đau Của Các Sếp Khi Làm Thủ Công**
Các sếp đã từng gặp phải tình huống nào sau đây chưa?
- **Sợ mất dữ liệu workflow** khi máy chủ bị lỗi hoặc n8n bị reset?
- **Không biết cách backup workflow** một cách an toàn và tự động?
- **Phải làm thủ công** mỗi khi muốn sao lưu, tốn thời gian và dễ quên?
- **Không có hệ thống thông báo** khi backup thất bại hoặc hoàn tất?

**Giải pháp này sẽ giúp các sếp:**
✅ **Backup toàn bộ workflow n8n** lên GitHub một cách tự động hàng ngày.
✅ **Nhận thông báo ngay lập tức** qua Email và Telegram khi backup thành công/thất bại.
✅ **Không cần viết code** – chỉ cần cấu hình và chạy.
✅ **Dễ dàng phục hồi workflow** khi cần, từ bất kỳ máy chủ nào.

---

## 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**LỢI ÍCH CỐT LÕI**]
- **An toàn tuyệt đối**: Dữ liệu workflow được sao lưu hàng ngày lên GitHub, không phụ thuộc vào máy chủ hiện tại.
- **Tiết kiệm thời gian**: Không cần làm thủ công mỗi khi muốn backup.
- **Thông báo tức thời**: Nhận báo cáo trạng thái backup qua Email và Telegram.
- **Dễ dàng chia sẻ**: Workflow có thể được chia sẻ với team hoặc phục hồi trên môi trường khác.
- **Hoạt động 24/7**: Dùng trigger lịch trình (`Daily`) để backup tự động hàng ngày.
:::

---

## 🔧 **Yêu Cầu Cần Thiết**
:::info[**CHUẨN BỊ TRƯỚC KHI BẮT ĐẦU**]
Các sếp cần chuẩn bị:
1. **Tài khoản GitHub** (để tạo repository và upload workflow).
2. **Token GitHub Personal Access Token** (có quyền `repo` để push code).
   - **Cách tạo**:
     - Truy cập [GitHub Settings](https://github.com/settings/tokens) → **Personal Access Tokens** → Tạo mới.
     - Chọn quyền `repo` (không cần quyền cao).
     - Lưu token này **an toàn** (không chia sẻ).
3. **Tài khoản Email** (để gửi thông báo backup).
   - **Credentials Gmail**:
     - Tạo **App Password** (nếu sử dụng 2FA) tại [My Account](https://myaccount.google.com/apppasswords).
     - Cấu hình trong n8n với:
       - **Email**: `your-email@gmail.com`
       - **Password**: `app-password-just-created`
4. **Bot Telegram** (để nhận thông báo).
   - Tạo bot tại [@BotFather](https://t.me/BotFather) và lấy **API Token**.
   - Thêm bot vào chat cá nhân và lưu **Chat ID** (cách lấy [tại đây](https://core.telegram.org/bots/api#how-do-i-get-my-user-id)).
5. **n8n Self-hosted** (để chạy workflow 24/7).
   - 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%).
   - 👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172).

---

## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
Các sếp có **2 cách** để import workflow này:
#### **Cách 1: Import từ file JSON**
1. Tải workflow từ [đây](https://n8n.io/workflows/4923) (ấn **Export**).
2. Trên n8n Editor, nhấn **Import** → Chọn file JSON vừa tải.
3. Chọn **Create new workflow** và nhấn **Import**.

#### **Cách 2: Copy/Paste JSON**
1. Mở file JSON từ [đây](https://n8n.io/workflows/4923) (ấn **Export**).
2. Trên n8n Editor, nhấn **Import** → Chọn **Paste JSON**.
3. Dán toàn bộ nội dung JSON và nhấn **Import**.

---

### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Sau khi import, các sếp cần **cấu hình lại các node quan trọng** như sau:

#### **🔹 Node `Backup_Config` (Code)**
- Mở node này và **cập nhật các biến sau** trong code:
  ```javascript
  const config = {
    github: {
      token: "YOUR_GITHUB_TOKEN", // Thay bằng token GitHub của bạn
      repoName: "n8n-workflows-backup", // Tên repository trên GitHub
      branch: "backup", // Branch để lưu backup
      owner: "YOUR_GITHUB_USERNAME" // Tên tài khoản GitHub
    },
    email: {
      from: "your-email@gmail.com", // Email gửi
      to: "your-email@gmail.com" // Email nhận
    },
    telegram: {
      botToken: "YOUR_TELEGRAM_BOT_TOKEN", // Token bot Telegram
      chatId: "YOUR_TELEGRAM_CHAT_ID" // Chat ID của bot
    }
  };
  ```
  - **Lưu ý**: Không chia sẻ token GitHub hoặc Telegram!

#### **🔹 Node `Check_Repository_Exists` (HTTP Request)**
- Đảm bảo **URL** trong node này trỏ đến API GitHub kiểm tra repository:
  ```
  https://api.github.com/repos/YOUR_GITHUB_USERNAME/n8n-workflows-backup
  ```
  - Thay `YOUR_GITHUB_USERNAME` bằng tên tài khoản GitHub của bạn.

#### **🔹 Node `Create_Repository` (HTTP Request)**
- Nếu repository chưa tồn tại, node này sẽ tạo mới.
- **Headers** phải có:
  - `Authorization: token YOUR_GITHUB_TOKEN`
  - `Accept: application/vnd.github.v3+json`

#### **🔹 Node `Upload_Workflow_Files` (HTTP Request)**
- **Headers** phải có:
  - `Authorization: token YOUR_GITHUB_TOKEN`
  - `Content-Type: application/json`
- **Payload** sẽ tự động được tạo bởi node `Split_Workflow_Files` (Code).

#### **🔹 Node `Gmail - Notification` (Gmail)**
- **Credentials**:
  - **Email**: `your-email@gmail.com`
  - **Password**: `app-password` (nếu sử dụng 2FA).
- **Subject** và **Body** có thể tùy chỉnh:
  ```
  Subject: Backup Workflow n8n - [Thành công/Không thành công]
  Body: Workflow đã được backup vào {{ $node["Backup_Complete_Summary"].json["date"] }}.
  ```

#### **🔹 Node `Send_Backup_Notification` (Telegram)**
- **Credentials**:
  - **Bot Token**: `YOUR_TELEGRAM_BOT_TOKEN`
  - **Chat ID**: `YOUR_TELEGRAM_CHAT_ID`
- **Message** có thể tùy chỉnh:
  ```
  Workflow backup status: {{ $node["Backup_Complete_Summary"].json["status"] }}
  Date: {{ $node["Backup_Complete_Summary"].json["date"] }}
  ```

#### **🔹 Node `Daily` (Schedule Trigger)**
- Đảm bảo **lịch trình** được đặt là **hàng ngày** (ví dụ: `0 0 * * *` – mỗi ngày 00:00).

---

### **3. Kích Hoạt ⚡️ Workflow**
1. **Test Run** với dữ liệu mẫu:
   - Nhấn **Run Workflow** và kiểm tra các node có hoạt động không.
   - Kiểm tra Email và Telegram có nhận được thông báo không.
2. **Bật Active**:
   - Sau khi test thành công, nhấn **Active** để workflow chạy tự động hàng ngày.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[**CÁC Ý TƯỞNG MỞ RỘNG**]
1. **Lưu log backup vào Google Sheets/Notion**:
   - Sử dụng node `n8n-nodes-base.googleSheets` hoặc `n8n-nodes-base.notion` để ghi lại lịch sử backup.
   - Cấu hình node `Backup_Complete_Summary` (Code) để xuất dữ liệu vào file CSV hoặc JSON, sau đó upload lên Google Sheets.

2. **Gửi báo cáo định kỳ qua Slack**:
   - Thêm node `n8n-nodes-base.slack` để gửi thông báo vào channel Slack của team.
   - Ví dụ:
     ```
     Workflow backup thành công vào {{ $node["Backup_Complete_Summary"].json["date"] }}!
     ```

3. **Backup vào nhiều repository**:
   - Sử dụng node `n8n-nodes-base.code` để định nghĩa nhiều cấu hình GitHub khác nhau và sử dụng node `splitInBatches` để backup vào nhiều repo.

4. **Xóa workflow cũ sau backup**:
   - Thêm node `n8n-nodes-base.delete` để xóa workflow cũ trên n8n sau khi backup thành công (nếu không cần).

5. **Kiểm tra dung lượng GitHub**:
   - Thêm node `n8n-nodes-base.httpRequest` để gọi API GitHub kiểm tra dung lượng và gửi cảnh báo nếu gần hết.

---

## 📌 **Kết Luận**
### **🚀 Đừng Bỏ Qua Giải Pháp Này Nữa!**
Backup workflow n8n là **bước đầu tiên** để bảo vệ dữ liệu quan trọng của các sếp. Với workflow này:
✔ **Không cần viết code** – chỉ cần cấu hình.
✔ **Hoạt động tự động** hàng ngày.
✔ **Nhận thông báo tức thời** qua Email và Telegram.
✔ **Dễ dàng phục hồi** khi cần.

**Hành động ngay hôm nay!**
1. **Chuẩn bị tài khoản** (GitHub, Email, Telegram).
2. **Import workflow** và cấu hình.
3. **Bật Active** và **quên đi lo lắng về mất dữ liệu!**

---
**💡 Gợi ý thêm**: Nếu các sếp muốn **backup nhiều workflow** từ nhiều máy chủ, có thể sử dụng **n8n Cloud** hoặc **self-hosted trên nhiều VPS** và kết nối chúng với nhau. 🚀