---
title: "🔒 Tự Động Hoàn Hảo: Backup Tất Cả Credentials N8n Sang GitHub Miễn Phí (Không Cần Code)"
description: "Giải pháp tự động hóa 24/7 sao lưu tất cả API keys, secrets và credentials của n8n lên GitHub với định dạng JSON an toàn, giúp các sếp tránh mất dữ liệu và bảo mật hiệu quả."
slug: "backup-credentials-n8n-github"
tags: [n8n, automation, devops, git, backup, no-code]
keywords: [backup credentials n8n, tự động hóa sao lưu GitHub, lưu trữ an toàn API keys, n8n workflow devops, sao lưu tự động]
---

# 🔒 **Backup Tất Cả Credentials N8n Sang GitHub - Giải Pháp An Toàn Cho Các Sếp Tech**

### **🚨 Nỗi Đau Thực Tế Của Các Sếp**
Các sếp đã từng gặp phải tình huống này chưa?
- **Mất credentials** khi máy tính bị lỗi, bị xóa hoặc bị hacker tấn công.
- **Không có bản sao lưu** khi phải chuyển đổi máy chủ hoặc nâng cấp hệ thống.
- **Phải nhớ hoặc ghi chép thủ công** hàng loạt API keys, secrets và thông tin đăng nhập, dễ bị quên hoặc lộ ra ngoài.
- **Rủi ro bảo mật** khi lưu trữ credentials trong file local hoặc email.

**Workflow này giải quyết tất cả!** Với chỉ một lần cấu hình, các sếp sẽ tự động sao lưu **tất cả credentials** của n8n lên **GitHub** dưới dạng file JSON, **an toàn, định kỳ và tự động hóa 100%**.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Sao lưu tự động 24/7**: Không cần nhớ hoặc làm thủ công, workflow chạy định kỳ hoặc khi có thay đổi.
- **Bảo mật cao**: Credentials được mã hóa và lưu trữ trên GitHub (không phải là cloud public).
- **Dễ truy cập**: Tất cả credentials được tổ chức theo định dạng `ID.json`, giúp tìm kiếm và phục hồi nhanh chóng.
- **Tiết kiệm thời gian**: Không phải mất giờ để sao lưu thủ công, đặc biệt khi có nhiều credentials.
- **Hoàn toàn tự động**: Chỉ cần cấu hình 1 lần, workflow sẽ hoạt động độc lập.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản GitHub** (đã có quyền push vào repository).
2. **Repository GitHub** riêng để lưu trữ credentials (không nên dùng repo public).
3. **API Key của GitHub** (tạo tại [Settings > Developer Settings > Personal Access Tokens](https://github.com/settings/tokens) với quyền `repo`).
4. **Workflow n8n** đã cài đặt và chạy trên **Self-hosted** (khuyến nghị dùng VPS để workflow hoạt động 24/7).
5. **Các credentials cần sao lưu** (API keys, secrets, thông tin đăng nhập của các dịch vụ như Slack, Google Sheets, Stripe...).

👉 **Lưu ý bảo mật**:
- **Không bao giờ** push credentials vào repo public.
- Sử dụng **repository private** hoặc folder riêng trong repo.
- **Không** chia sẻ API key GitHub với bất kỳ ai.
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/2307) hoặc sử dụng mã JSON dưới đây:
  ```json
  {
    "nodes": [
      // Danh sách nodes đầy đủ (xem chi tiết dưới đây)
    ],
    "connections": [
      // Danh sách kết nối giữa nodes
    ]
  }
  ```
- **Cách import**:
  1. Mở **n8n Editor** trên trang web hoặc VPS.
  2. Nhấn **Import Workflow** (icon file +).
  3. Chọn file JSON hoặc dán mã JSON vào ô **Import from JSON**.
  4. Nhấn **Import**.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này sử dụng **subworkflow** để tối ưu hóa bộ nhớ. Các bước cấu hình quan trọng:

##### **A. Cấu Hình Node "Globals" (BẮT BUỘC)**
Node này xác định **repository và đường dẫn** để lưu credentials:
1. Mở node **"Globals"** (type: `set`).
2. Cập nhật các tham số sau:
   - **`repo.owner`**: Tên tài khoản GitHub của bạn (ví dụ: `john-doe`).
   - **`repo.name`**: Tên repository (ví dụ: `n8n-backups`).
   - **`repo.path`**: Đường dẫn folder trong repo (ví dụ: `credentials/`).
     - Nếu folder không tồn tại, nó sẽ được tạo tự động.
   - **`filePrefix`**: Tiền tố cho tên file (ví dụ: `credentials_`).
   - **`fileExtension`**: Kiểu file (giữ nguyên `.json`).

   **Ví dụ**:
   ```json
   {
     "repo.owner": "john-doe",
     "repo.name": "n8n-backups",
     "repo.path": "credentials/",
     "filePrefix": "credentials_",
     "fileExtension": ".json"
   }
   ```

##### **B. Cấu Hình Credentials GitHub**
1. Đi đến **Credentials** trong n8n (icon cài đặt ở góc trên phải).
2. Thêm **GitHub API** mới:
   - **Name**: `githubApi` (giữ nguyên để workflow hoạt động).
   - **Type**: `GitHub`.
   - **Token**: Dán **Personal Access Token** từ GitHub (tạo trước đó).
   - **Repository**: Chọn repository bạn muốn sử dụng.

##### **C. Kiểm Tra Node "Get File Data"**
Node này lấy dữ liệu file hiện tại từ GitHub để so sánh với credentials mới:
- **Credentials**: Chọn `githubApi` (đã cấu hình ở trên).
- **Operation**: `get`.
- **Resource**: `file`.
- **File Path**: Đặt thành `${$node["Globals"].json["repo.path"]}${$node["Execute Command"].json["fileName"]}` (sẽ được tự động hóa sau).

##### **D. Cấu Hình Node "Execute Command"**
Node này **tạo hoặc chỉnh sửa file** trên GitHub:
- **Command**: `echo "$json" > "$filePath"` (được tự động hóa bởi workflow).
- **File Path**: Đặt thành `${$node["Globals"].json["repo.path"]}${$node["Execute Command"].json["fileName"]}`.

##### **E. Kiểm Tra Node "Schedule Trigger" (Nếu Muốn Chạy Định Kỳ)**
Nếu các sếp muốn workflow chạy **tự động hàng ngày**, cấu hình node này:
- **Cron Expression**: `0 0 * * *` (chạy lúc 00:00 hàng ngày).
- **Active**: Bật để kích hoạt.

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Nhấn **Execute** trên node **"On clicking 'execute'"**.
   - Kiểm tra **GitHub repository** để xác nhận file đã được tạo/chia sẻ.
2. **Bật Active**:
   - Đặt **Active** thành `true` trên node **"On clicking 'execute'"** (nếu muốn chạy thủ công).
   - Hoặc bật **Schedule Trigger** nếu muốn chạy tự động.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[TIẾP CẬN HƠN]
1. **Lưu Log Lịch Sử**:
   - Thêm node **Slack/Telegram** để thông báo khi credentials được cập nhật.
   - Ví dụ: `"Backup thành công cho credentials [ID] vào lúc [time]"`.
2. **Chia Sẻ An Toàn**:
   - Sử dụng **GitHub Secrets** hoặc **encrypted environment variables** để bảo mật thêm.
3. **Sao Lưu Nhiều Credentials**:
   - Nếu có nhiều credentials, sử dụng **node `splitInBatches`** để xử lý từng batch.
4. **Kết Hợp Với Notion/Google Sheets**:
   - Lưu danh sách credentials vào **Notion** hoặc **Google Sheets** để theo dõi dễ dàng.
5. **Backup Định Kỳ**:
   - Sử dụng **Cron Job** để chạy workflow hàng tuần/tháng.
:::

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn **tránh mất dữ liệu, bảo mật credentials và tự động hóa sao lưu** một cách an toàn. Với chỉ **1 lần cấu hình**, các sếp sẽ có một **bản sao lưu tự động, định kỳ và an toàn** cho tất cả credentials của n8n.

**Hành động ngay hôm nay!**
1. **Cài đặt n8n trên VPS** (để workflow chạy 24/7).
2. **Import workflow** và cấu hình theo hướng dẫn.
3. **Bật Schedule Trigger** để sao lưu tự động hàng ngày.

👉 **Nếu cần hỗ trợ**, liên hệ với tác giả Solomon qua:
- Email: [automations.solomon@gmail.com](mailto:automations.solomon@gmail.com)
- Telegram: [@solomon_automations](https://t.me/solomon_automations)

---
:::note[CHÚ Ý]
- **Không bao giờ** push credentials vào repo public.
- **Không** chia sẻ API key GitHub với bất kỳ ai.
- **Test workflow** với dữ liệu mẫu trước khi sử dụng thực tế.
:::