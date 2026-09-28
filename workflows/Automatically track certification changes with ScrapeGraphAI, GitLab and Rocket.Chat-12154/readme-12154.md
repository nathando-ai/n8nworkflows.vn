---
title: "🔍 Tự Động Theo Dõi Thay Đổi Chứng Nhận Giấy Phiếu AI + GitLab + Rocket.Chat (Không Code)"
description: "Workflow tự động hóa theo dõi thay đổi yêu cầu chứng nhận từ các trang web công ty chứng nhận hàng ngày, so sánh với dữ liệu cũ, và thông báo ngay khi có sự thay đổi. Giúp các sếp tiết kiệm thời gian và tránh bỏ lỡ thông tin quan trọng."
slug: "tieu-dong-theo-doi-thay-doi-chung-nhan-gitlab-rocketchat"
tags: [n8n, automation, document-extraction, ai-summarization, gitlab, scrapegraphai, rocketchat]
keywords: [n8n workflow chứng nhận, tự động hóa theo dõi chứng nhận, ScrapeGraphAI, GitLab API, Rocket.Chat alert, AI so sánh dữ liệu]
---

# 🚀 **Tự Động Theo Dõi Thay Đổi Chứng Nhận Giấy Phiếu AI + GitLab + Rocket.Chat**

### **Giải pháp hoàn hảo cho các sếp quản lý chứng nhận công ty**
Hàng ngày, các sếp phải theo dõi thủ công các trang web chứng nhận để cập nhật yêu cầu mới nhất về chứng nhận, thời hạn, hoặc thay đổi quy trình. **Workflow này tự động hóa toàn bộ quy trình đó** bằng công nghệ AI ScrapeGraphAI, GitLab và Rocket.Chat, giúp bạn:
- **Không bao giờ bỏ lỡ** bất kỳ thay đổi nào về yêu cầu chứng nhận.
- **Tiết kiệm thời gian** lên đến 10 giờ/tuần (so với cách làm thủ công).
- **Cập nhật dữ liệu chính xác** và tự động lưu trữ lịch sử thay đổi.
- **Thông báo ngay lập tức** khi có sự thay đổi qua Rocket.Chat (hoặc Slack).

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%**: Không cần viết một dòng code nào.
- **Cập nhật liên tục**: Theo dõi hàng ngày (hoặc theo tuần/tháng tùy chọn).
- **So sánh thông minh**: AI so sánh dữ liệu mới vs. cũ và báo cáo sự khác biệt.
- **Thông báo tức thời**: Khi có thay đổi, hệ thống sẽ gửi tin nhắn ngay đến Rocket.Chat (hoặc Slack).
- **Lưu trữ dữ liệu**: Tất cả lịch sử thay đổi được lưu trên GitLab, dễ dàng tra cứu.
- **Không bị giới hạn API**: Sử dụng `Split In Batches` để tránh bị chặn bởi API.
:::

---

### 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản ScrapeGraphAI**:
   - [Đăng ký miễn phí ScrapeGraphAI](https://www.scrapegraph.ai/) và lấy **API Key**.
   - Cài đặt **credential** trong n8n: `Menu → Credentials → Add → ScrapeGraphAI`.

2. **Tài khoản GitLab**:
   - Một **repository** riêng để lưu trữ dữ liệu chứng nhận (ví dụ: `certifications-repo`).
   - **API Key** của GitLab (tạo tại `Settings → Access Tokens` với quyền `read_repository` và `write_repository`).
   - Cài đặt **credential** trong n8n: `Menu → Credentials → Add → GitLab`.

3. **Tài khoản Rocket.Chat (hoặc Slack)**:
   - Một **bot** hoặc **user** có quyền gửi tin nhắn vào kênh cảnh báo.
   - **Webhook URL** của Rocket.Chat (tạo tại `Admin → Apps → Webhooks`).
   - Cài đặt **credential** trong n8n: `Menu → Credentials → Add → Rocket.Chat`.

4. **Danh sách URL chứng nhận**:
   - Danh sách các trang web chứng nhận cần theo dõi (ví dụ: `https://example.com/certification1`, `https://example.com/certification2`).
   - Mỗi URL sẽ được gán một `certId` duy nhất (ví dụ: `cert1`, `cert2`).

5. **n8n Self-hosted (khuyến nghị)**:
   - Để workflow chạy 24/7 ổn định, các sếp nên cài n8n trên **VPS riêng**.
   - 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%).
   - 👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172).
:::

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/12154](https://n8n.io/workflows/12154) hoặc copy toàn bộ JSON từ link trên.
- Trong **n8n Editor**, nhấn `Import` → Dán JSON hoặc tải file `.json` lên.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
##### **A. Cấu hình Credentials**
- **ScrapeGraphAI**:
  - Điền `API Key` vào credential đã tạo trước đó.
  - Trong node **`Scrape Requirement Data`**, kiểm tra `prompt` để đảm bảo AI trích xuất đúng thông tin (`certName`, `requirementText`, `lastUpdated`, `renewalIntervalYears`).

- **GitLab**:
  - Chọn credential GitLab đã tạo.
  - Trong node **`Fetch Previous Data`** và **`Save Updated Requirement`**, điền:
    - **Repository URL**: `https://gitlab.com/username/certifications-repo.git` (thay `username` bằng tên tài khoản GitLab của bạn).
    - **Branch**: `main`.
    - **File Path**: `/certifications/{certId}.json` (sẽ tự động tạo file theo `certId`).

- **Rocket.Chat**:
  - Chọn credential Rocket.Chat.
  - Trong node **`Send a message`**, điền:
    - **Channel**: Tên kênh cảnh báo (ví dụ: `#alerts`).
    - **Message Template**: Thay đổi nội dung tin nhắn tùy ý (ví dụ: `🚨 Thay đổi yêu cầu chứng nhận: {certName} | {diff}`).

##### **B. Cấu hình "Certification URL Config" (Code Node)**
- Mở node **`Certification URL Config`** và chỉnh sửa mã như sau:
  ```javascript
  [
    { certId: "cert1", url: "https://example.com/certification1" },
    { certId: "cert2", url: "https://example.com/certification2" },
    // Thêm các URL chứng nhận khác...
  ]
  ```
  - **Lưu ý**: Mỗi `certId` phải duy nhất và khớp với file JSON trên GitLab (`/certifications/{certId}.json`).

##### **C. Cấu hình Schedule Trigger**
- Mở node **`Daily Trigger`** và chỉnh:
  - **Frequency**: `Daily` (hoặc `Weekly`/`Monthly` tùy chọn).
  - **Time**: Thời gian chạy (ví dụ: `09:00` sáng).

##### **D. Cấu hình "Detect Changes" (Code Node)**
- Mở node **`Detect Changes`** và chỉnh sửa logic so sánh (nếu cần):
  ```javascript
  // Ví dụ: So sánh `requirementText` và `renewalIntervalYears`
  const changed = JSON.stringify(oldData.requirementText) !== JSON.stringify(newData.requirementText) ||
                  oldData.renewalIntervalYears !== newData.renewalIntervalYears;

  return {
    changed: changed,
    diff: changed ? `Yêu cầu mới: ${newData.requirementText}\nThời gian tái chứng nhận: ${newData.renewalIntervalYears} năm` : "Không có thay đổi"
  };
  ```

#### **3. Kích hoạt ⚡️**
- **Test Run**:
  - Chọn node **`Daily Trigger`** → Nhấn `Run Workflow` để kiểm tra.
  - Kiểm tra kết quả trên **GitLab** và **Rocket.Chat** để đảm bảo thông báo đúng.
- **Bật Active**:
  - Sau khi test thành công, nhấn `Active` trên node **`Daily Trigger`**.

---

### ✍️ **Mẹo & gợi ý nâng cao**
:::info[NHỮNG Ý TƯỞNG TIẾP THEO]
1. **Kết hợp với Slack**:
   - Thay vì Rocket.Chat, các sếp có thể sử dụng **Slack Webhook** để nhận cảnh báo.
   - Cài đặt credential Slack và thay đổi node **`Send a message`** sang `n8n-nodes-base.slack`.

2. **Lưu log chi tiết**:
   - Thêm node **`n8n-nodes-base.stickyNote`** để ghi lại thông tin debug (ví dụ: lỗi scraping, thời gian chạy).

3. **Gửi báo cáo định kỳ**:
   - Sử dụng node **`n8n-nodes-base.email`** để gửi email tổng hợp thay đổi hàng tuần cho đội ngũ.

4. **Tự động tạo issue GitLab**:
   - Khi có thay đổi, workflow có thể tự động tạo **issue** trong GitLab để theo dõi.

5. **Cập nhật prompt AI**:
   - Nếu ScrapeGraphAI không trích xuất đầy đủ, các sếp có thể chỉnh sửa `prompt` trong node **`Scrape Requirement Data`** để yêu cầu AI lấy thêm thông tin (ví dụ: `lastUpdatedDate`, `renewalFee`).

6. **Bảo mật dữ liệu**:
   - Nếu dữ liệu chứng nhận nhạy cảm, các sếp có thể **mã hóa** file JSON trên GitLab trước khi lưu.
:::

---

### 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp quản lý chứng nhận công ty, giúp tự động hóa toàn bộ quy trình theo dõi, so sánh và thông báo thay đổi. **Không cần viết code**, chỉ cần cấu hình một số bước đơn giản là có thể tiết kiệm hàng giờ làm việc mỗi tuần.

👉 **Hành động ngay**:
1. **Cài đặt n8n Self-hosted** trên VPS (để workflow chạy 24/7).
2. **Import workflow** và cấu hình credentials.
3. **Bật Active** và theo dõi kết quả trên GitLab & Rocket.Chat!

**Nếu có vấn đề**, các sếp có thể để lại comment bên dưới hoặc liên hệ với cộng đồng n8n tại [n8n Community](https://community.n8n.io/). Chúc các sếp thành công! 🚀

---