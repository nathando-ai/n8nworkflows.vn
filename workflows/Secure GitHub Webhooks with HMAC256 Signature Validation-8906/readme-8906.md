---
title: "🔒 **Bảo mật Webhook GitHub với HMAC256: Hướng dẫn tự động hóa an toàn 100% không code**"
description: "Workflow này giúp các sếp xác thực và bảo mật webhook GitHub bằng HMAC256, ngăn chặn tấn công giả mạo và đảm bảo tính toàn vẹn dữ liệu. Giúp tự động hóa các tác vụ liên quan đến GitHub an toàn và hiệu quả."
slug: "bao-mat-webhook-github-hmac256"
tags: [n8n, automation, no-code, github-webhook, security, hmac256]
keywords: [n8n workflow github, bảo mật webhook, tự động hóa gitlab, xác thực HMAC256, an toàn webhook]
---

# 🔒 **Bảo mật Webhook GitHub bằng HMAC256: Xác thực và tự động hóa an toàn**

### **Nỗi đau thực tế của các sếp**
Các sếp đang gặp khó khăn khi tự động hóa các tác vụ liên quan đến GitHub mà không đảm bảo tính an toàn. Khi webhook GitHub được kích hoạt, dữ liệu có thể bị giả mạo hoặc tấn công từ bên ngoài, dẫn đến:
- **Tác vụ tự động hóa bị lỗi** do dữ liệu không chính xác.
- **Rủi ro bảo mật** khi không xác thực nguồn gốc của webhook.
- **Thời gian và công sức** bị lãng phí khi phải kiểm tra thủ công mỗi lần webhook được kích hoạt.

Workflow này giải quyết vấn đề này bằng cách **xác thực HMAC256**, đảm bảo rằng chỉ có webhook từ GitHub chính thức mới được xử lý, từ đó **tự động hóa an toàn và hiệu quả**.

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Bảo mật tuyệt đối**: Xác thực HMAC256 ngăn chặn webhook giả mạo, đảm bảo dữ liệu đến từ GitHub chính thức.
- **Tự động hóa an toàn**: Chỉ cho phép webhook hợp lệ tiếp tục xử lý, tránh lỗi do dữ liệu không chính xác.
- **Tiết kiệm thời gian**: Không cần kiểm tra thủ công mỗi lần webhook được kích hoạt.
- **Hỗ trợ mở rộng**: Sau khi xác thực, các sếp có thể thêm logic tự động hóa tùy chỉnh (ví dụ: gửi thông báo Slack, cập nhật cơ sở dữ liệu...).
:::

---

### 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị:
- **Tài khoản GitHub** và một repository.
- **Secret key cho webhook GitHub**:
  - Đăng nhập vào GitHub → Repository → **Settings** → **Webhooks** → **Add webhook**.
  - Thêm URL webhook của n8n (ví dụ: `https://tên-doman-n8n.com/github-test`).
  - Nhập **Secret key** (cần tạo một secret bất kỳ, ví dụ: `abc123xyz`).
- **Credentials GitHub API** trong n8n:
  - Tạo credentials mới trong n8n với loại **GitHub API** và nhập **Personal Access Token** (có quyền `repo`).
- **n8n Self-hosted** (không dùng phiên bản miễn phí để đảm bảo webhook hoạt động 24/7).

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Tải workflow từ [n8n.io/workflows/8906](https://n8n.io/workflows/8906) hoặc sử dụng file JSON đã cung cấp.
2. Trong **n8n Editor**, nhấn **Import** và chọn file JSON.
3. Hoặc copy toàn bộ JSON và nhấn **Paste JSON** trong menu.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này bao gồm **7 node** chính, các sếp cần cấu hình như sau:

##### **A. Cấu hình Webhook GitHub**
- **Node: "GitHub Webhook"**
  - **Path**: Đặt thành `github-test` (hoặc tên tùy ý, nhưng phải khớp với URL webhook trong GitHub).
  - **HTTP Method**: Đặt thành `POST`.
  - **Credentials**: Không cần thiết (webhook sẽ tự động nhận dữ liệu từ GitHub).

##### **B. Xác thực HMAC256**
- **Node: "Compute HMAC256" (type: crypto)**
  - **Secret**: Nhập **Secret key** tương tự như trong cấu hình webhook GitHub (ví dụ: `abc123xyz`).
  - **Message**: Sử dụng `$json.body` (n8n sẽ tự động lấy nội dung body của webhook).
  - **Algorithm**: Đặt thành `HMAC-SHA256`.

- **Node: "Validate HMAC256" (type: if)**
  - **Condition**: So sánh giá trị HMAC tính toán với giá trị trong header `x-hub-signature-256` của webhook.
    - **Expression**: `$node["Compute HMAC256"].json.hmac === $header["x-hub-signature-256"]`.
  - Nếu đúng, workflow tiếp tục; nếu sai, trả về **401 Unauthorized**.

##### **C. Trả lời cho GitHub**
- **Node: "Respond 200 OK"**
  - Chỉ hoạt động khi HMAC hợp lệ.
- **Node: "Respond 401 Unauthorized"**
  - Hoạt động khi HMAC không hợp lệ (các sếp có thể bỏ node này nếu không cần log lỗi).

##### **D. Cấu hình GitHub API (nếu cần)**
- **Node: "Get the profile of a repository"**
  - **Credentials**: Chọn `githubApi` (credentials đã tạo trước đó).
  - **Operation**: Đặt thành `getProfile`.
  - **Resource**: Đặt thành `repository`.
  - **Repository**: Nhập tên repository cần lấy thông tin (ví dụ: `tên-repo/tên-user`).

##### **E. Node "Stop and Error" (tùy chọn)**
- Các sếp có thể **bỏ node này** nếu không cần log lỗi. Nếu giữ lại, nó sẽ dừng workflow khi HMAC không hợp lệ.

#### **3. Kích hoạt ⚡️**
1. **Test run dữ liệu mẫu**:
   - Tạo một **webhook test** trong GitHub (ví dụ: push một commit vào repository).
   - Kiểm tra trong **n8n Editor** xem workflow có trả về **200 OK** hay **401 Unauthorized**.
2. **Bật Active workflow**:
   - Sau khi kiểm tra thành công, nhấn **Active** để workflow hoạt động liên tục.

---

### ✍️ **Mẹo & gợi ý nâng cao**
:::tip[CÁCH MỞ RỘNG THÊM LOGIC TỰ ĐỘNG HÓA]
Sau khi xác thực HMAC256 thành công, các sếp có thể thêm các node tùy chỉnh để tự động hóa thêm:
1. **Gửi thông báo Slack/Telegram**:
   - Sử dụng node **Slack** hoặc **Telegram Bot** để báo cáo khi có sự kiện webhook.
   - Ví dụ: Khi có push mới, gửi thông báo đến Slack với chi tiết commit.
2. **Lưu log vào cơ sở dữ liệu**:
   - Sử dụng node **Google Sheets**, **Airtable**, hoặc **Database** để lưu lịch sử webhook.
3. **Xử lý tự động repository**:
   - Sử dụng node **GitHub API** để tự động tạo branch, pull request, hoặc deploy.
4. **Gửi email báo cáo**:
   - Sử dụng node **Email** (ví dụ: Gmail, SendGrid) để gửi báo cáo định kỳ.
5. **Kết hợp với LLM (AI)**:
   - Sử dụng node **LLM** (ví dụ: Mistral, OpenAI) để phân tích nội dung commit và tự động tạo PR review.

**Ví dụ mở rộng**:
- Khi webhook được kích hoạt (push code mới), workflow:
  1. Xác thực HMAC256.
  2. Lấy thông tin repository từ GitHub.
  3. Gửi thông báo Slack với chi tiết commit.
  4. Lưu log vào Google Sheets.
  5. Nếu có từ khóa cụ thể trong commit (ví dụ: `deploy`), tự động chạy script deploy.

---

### 📌 **Kết luận**
Workflow này là **cơ sở an toàn** cho việc tự động hóa webhook GitHub. Bằng cách xác thực HMAC256, các sếp đảm bảo rằng chỉ có dữ liệu từ GitHub chính thức mới được xử lý, từ đó **tránh lỗi, tiết kiệm thời gian và nâng cao bảo mật**.

**Hành động ngay**:
1. **Import workflow** và cấu hình theo hướng dẫn.
2. **Test với webhook test** để đảm bảo hoạt động.
3. **Mở rộng logic tự động hóa** theo nhu cầu của doanh nghiệp.

🚀 **Bắt đầu tự động hóa an toàn với n8n ngay hôm nay!**

---
**Cần hỗ trợ?**
- Trả lời trên [Forum n8n](https://community.n8n.io/).
- Liên hệ tác giả Yves Tkaczyk trên [LinkedIn](https://www.linkedin.com/in/ytkaczyk/).