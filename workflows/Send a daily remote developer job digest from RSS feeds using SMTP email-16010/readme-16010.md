---
title: "🚀 Tự Động Hóa Email Tóm Tắt Công Việc Làm Remote Hàng Ngày Từ RSS (Không Cần Code)"
description: "Workflow này tự động thu thập và gửi email tổng hợp các công việc làm remote mới nhất từ 3 nguồn tin tức hàng đầu (RemoteOK, WeWorkRemotely, Himalayas) vào mỗi sáng 8h, loại bỏ trùng lặp và chỉ gửi những công việc phù hợp với kỹ thuật stack của bạn. Giúp tiết kiệm thời gian tìm kiếm và đảm bảo không bỏ lỡ cơ hội nào."
slug: "tieu-dong-hoa-email-tom-tat-cong-viec-lam-remote"
tags: [n8n, automation, remote-jobs, smtp, rss, no-code]
keywords: [n8n workflow remote jobs, tự động hóa tìm việc làm remote, email tổng hợp công việc, RSS feed automation, n8n self-hosted]
---

# 🚀 **Tự Động Hóa Email Tóm Tắt Công Việc Làm Remote Hàng Ngày (Không Cần Code)**

### **Giải quyết vấn đề gì?**
Các sếp phát triển phần mềm hoặc chuyên gia kỹ thuật thường phải mất **từ 30 phút đến 1 giờ mỗi ngày** để:
- Theo dõi nhiều trang tin tuyển dụng remote (RemoteOK, WeWorkRemotely, Himalayas, ...).
- Lọc ra những công việc phù hợp với kỹ thuật stack của mình (React, Python, DevOps, ...).
- Loại bỏ trùng lặp và bỏ qua những công việc đã xem trước đó.
- Ghi nhớ hoặc lưu trữ thông tin công việc để theo dõi sau.

**Workflow này tự động hóa toàn bộ quy trình đó!** Vào mỗi sáng 8h, hệ thống sẽ:
✅ **Thu thập** tất cả công việc mới từ 3 nguồn tin tức hàng đầu.
✅ **Lọc** theo từ khóa kỹ thuật stack của bạn (ví dụ: `react`, `python`, `aws`).
✅ **Loại bỏ trùng lặp** để không nhận được cùng một công việc nhiều lần.
✅ **Gửi email tổng hợp** vào hộp thư của bạn với nội dung sạch sẽ, dễ đọc.

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không phải mất giờ mỗi ngày để tìm kiếm và lọc công việc.
- **Chính xác và cá nhân hóa**: Email chỉ chứa công việc phù hợp với kỹ thuật stack của bạn.
- **Hoạt động liên tục 24/7**: Không cần nhớ hoặc nhắc nhở, hệ thống tự động chạy hàng ngày.
- **Không bị trùng lặp**: Công việc đã xem trước đó sẽ không xuất hiện lại, ngay cả sau nhiều ngày.
- **Dễ dàng mở rộng**: Thêm được nhiều nguồn tin tức hoặc từ khóa mới chỉ với vài thay đổi nhỏ.
:::

---

### 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Để workflow này hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản n8n Self-hosted** (không dùng phiên bản miễn phí trên cloud).
2. **Thông tin cấu hình cơ bản**:
   - **Từ khóa kỹ thuật stack** (ví dụ: `["react", "typescript", "aws"]`).
   - **Email nhận** (địa chỉ email của bạn).
   - **Email gửi** (địa chỉ email xuất phát, thường là email của bạn hoặc email SMTP).
3. **Thông tin SMTP** để gửi email:
   - **Host SMTP** (ví dụ: `smtp.gmail.com`, `smtp-relay.brevo.com`).
   - **Port** (thường là `587` với TLS hoặc `465` với SSL).
   - **Tên đăng nhập và mật khẩu** (hoặc mã ứng dụng cho Gmail).
4. **Nếu dùng Gmail**:
   - **Bật 2FA** trên tài khoản Google.
   - **Tạo mã ứng dụng** (App Password) tại [Google Account → Security → App Passwords](https://myaccount.google.com/security).
   - **Không dùng mật khẩu chính** của tài khoản Gmail, mà dùng mã ứng dụng này.
:::

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow này từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. **Tải file JSON** từ [liên kết gốc](https://n8n.io/workflows/16010) hoặc sử dụng file đã cung cấp.
2. Trong **n8n Editor**, nhấn **Import Workflow** và chọn file JSON.
3. Hoặc copy toàn bộ nội dung JSON và dán vào **Import Workflow** → **Paste JSON**.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này có **14 node** và cần cấu hình một số node quan trọng sau:

##### **A. Cấu hình Config Node (Thiết lập cơ bản)**
- Mở node **"Config"** (node thứ 2).
- Cập nhật các tham số sau:
  ```json
  {
    "keywords": ["react", "python", "aws"], // Thêm hoặc thay đổi từ khóa kỹ thuật stack
    "recipientEmail": "email-cua-ban@example.com", // Email nhận
    "senderEmail": "email-gui@example.com", // Email xuất phát (có thể là email SMTP)
    "jobBoards": [
      "https://remoteok.com/remote-dev-jobs.rss",
      "https://weworkremotely.com/remote-jobs.rss",
      "https://himalayas.app/jobs/rss"
    ],
    "maxAgeHours": 72 // Thời gian tối đa để xem công việc (giá trị mặc định)
  }
  ```
  - **Lưu ý**: Nếu muốn nhận **tất cả công việc** từ các nguồn tin tức (không lọc theo từ khóa), đặt `keywords` thành `[]` (mảng rỗng).

##### **B. Cấu hình SMTP Credential**
- Mở **Settings → Credentials → Add Credential**.
- Tìm và chọn **SMTP**.
- Nhập thông tin SMTP:
  - **Host**: `smtp.gmail.com` (nếu dùng Gmail) hoặc `smtp-relay.brevo.com` (nếu dùng Brevo).
  - **Port**: `587` (TLS) hoặc `465` (SSL).
  - **Username**: Email của bạn.
  - **Password**: Mật khẩu hoặc mã ứng dụng (nếu dùng Gmail).
- Lưu credential và chọn nó trong node **"Send Digest Email"**.

##### **C. Cấu hình Schedule Trigger**
- Mở node **"Every Day at 8 AM"** (node thứ 1).
- Đảm bảo thời gian được đặt là **8h sáng** theo múi giờ của máy chủ n8n.
- Nếu muốn thay đổi thời gian, chỉnh sửa tại đây.

##### **D. Cấu hình các node Code (Lọc và Loại bỏ trùng lặp)**
- **Node "Filter by Keyword & Recency"**:
  - Đảm bảo **`alwaysOutputData: ON`** (để loop tiếp tục ngay cả khi không có kết quả).
- **Node "Deduplicate Jobs"**:
  - Đảm bảo **`alwaysOutputData: ON`** (để loop tiếp tục ngay cả khi không có công việc mới).
  - **Lưu ý**: Node này sử dụng **dữ liệu tĩnh** (`$getWorkflowStaticData('global')`) để lưu trữ lịch sử công việc đã xem. Nếu workflow bị xóa và import lại, dữ liệu này sẽ mất.

##### **E. Node "Log Fetch Error"**
- Node này **bắt lỗi** khi RSS feed không trả về dữ liệu. Đảm bảo nó được kết nối với node **"Split Job Boards"** để loop không bị ngắt khi một nguồn tin tức bị lỗi.

---

#### **3. Kích hoạt ⚡️**
1. **Test Run** (để kiểm tra workflow):
   - Nhấn **Test Workflow** để chạy một lần và kiểm tra email nhận được.
   - Nếu email không đến, kiểm tra lại **SMTP credential** và **Config node**.
2. **Bật Active**:
   - Sau khi test thành công, nhấn **Toggle Active** để workflow chạy hàng ngày.

---

### ✍️ **Mẹo & gợi ý nâng cao**
:::tip[CÁCH LÀM NÂNG CAO]
1. **Thêm nguồn tin tức mới**:
   - Mở node **"Config"** và thêm URL RSS mới vào mảng `jobBoards`.
   - Ví dụ:
     ```json
     "jobBoards": [
       "https://remoteok.com/remote-dev-jobs.rss",
       "https://weworkremotely.com/remote-jobs.rss",
       "https://himalayas.app/jobs/rss",
       "https://jobs.remotework.tech/rss" // Thêm nguồn mới
     ]
     ```
   - **Lưu ý**: Trước khi thêm, kiểm tra URL RSS trong trình duyệt để đảm bảo nó trả về dữ liệu XML.

2. **Tăng hoặc giảm thời gian lọc công việc mới**:
   - Thay đổi giá trị `maxAgeHours` trong node **"Config"**:
     - Giá trị cao hơn (ví dụ: `168` giờ = 7 ngày) sẽ lọc công việc mới hơn.
     - Giá trị thấp hơn (ví dụ: `24` giờ = 1 ngày) sẽ chỉ lọc công việc mới nhất trong ngày.

3. **Gửi email báo cáo định kỳ**:
   - Nếu muốn gửi email tổng hợp **hàng tuần** thay vì hàng ngày, chỉnh sửa node **"Every Day at 8 AM"** thành **"Every Sunday at 8 AM"**.

4. **Lưu log hoạt động**:
   - Thêm node **Slack** hoặc **Telegram** sau node **"Send Digest Email"** để nhận thông báo khi email được gửi thành công hoặc gặp lỗi.
   - Ví dụ:
     ```json
     {
       "operation": "sendMessage",
       "text": "Email tổng hợp công việc remote đã được gửi thành công!",
       "channel": "#n8n-alerts"
     }
     ```

5. **Tự động xóa công việc cũ trong dữ liệu tĩnh**:
   - Nếu muốn **xóa dữ liệu cũ** (công việc đã xem trước 30 ngày) một cách thủ công, mở node **"Deduplicate Jobs"** và thêm dòng code sau trước khi `return`:
     ```javascript
     staticData.seenJobs = Object.fromEntries(
       Object.entries(staticData.seenJobs || {}).filter(([_, timestamp]) => {
         const date = new Date(timestamp);
         const now = new Date();
         const diffTime = now - date;
         const diffDays = diffTime / (1000 * 60 * 60 * 24);
         return diffDays < 30;
       })
     );
     ```
   - Sau khi chạy, xóa dòng code này và lưu lại.

6. **Sử dụng AI để tổng hợp nội dung email**:
   - Thay vì sử dụng node **"Build Email HTML"** mặc định, các sếp có thể kết nối với một **LLM node** (ví dụ: n8n-nodes-ai) để tự động viết nội dung email cá nhân hóa.
   - Ví dụ:
     ```json
     {
       "operation": "generateText",
       "prompt": "Tóm tắt {{$json.job.title}} với kỹ thuật stack {{$json.keywords}} trong email tổng hợp công việc remote.",
       "model": "gpt-3.5-turbo"
     }
     ```

---

### 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp phát triển phần mềm hoặc chuyên gia kỹ thuật muốn **tự động hóa việc tìm kiếm và lọc công việc làm remote**. Bằng cách chỉ cần **cấu hình một lần**, các sếp sẽ nhận được **email tổng hợp công việc mới nhất** hàng ngày, phù hợp với kỹ thuật stack của mình, **không bị trùng lặp** và **không mất thời gian**.

**Hành động ngay hôm nay!**
1. **Cài đặt n8n Self-hosted** trên VPS (nếu chưa có).
2. **Import workflow** và cấu hình theo hướng dẫn trên.
3. **Bật Active** và bắt đầu nhận email tổng hợp công việc mỗi sáng!

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**Chúc các sếp thành công với việc tự động hóa công việc tìm việc làm remote!** 🚀