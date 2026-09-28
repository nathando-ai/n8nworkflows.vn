---
title: "💾 **Tự Động Lưu Workflow n8n Vào GitLab – Giải Pháp DevOps Không Cần Code**"
description: "Hướng dẫn tự động lưu tất cả workflow n8n của bạn vào kho lưu trữ GitLab một cách tự động, an toàn và định kỳ. Giúp các sếp quản lý phiên bản, theo dõi thay đổi và khôi phục nhanh chóng mà không cần viết một dòng code nào."
slug: "tự-dộng-lưu-workflow-n8n-vao-gitlab"
tags: [n8n, automation, devops, gitlab, version-control]
keywords: [tự động hóa n8n, lưu workflow gitlab, quản lý phiên bản workflow, devops không code, tự động hóa gitlab]
---

# 🚀 **Tự Động Lưu Workflow n8n Vào GitLab – Khắc Phục Nỗi Lo "Làm Sao Để Bảo Vệ Workflow Của Tôi?"**

Hãy tưởng tượng một tình huống: Sau nhiều ngày xây dựng một workflow phức tạp trên n8n, bạn vô tình **xóa nó** hoặc **cài đặt lại máy chủ**, và tất cả công sức của bạn biến mất trong một giây. Hoặc khi muốn **so sánh phiên bản cũ mới**, bạn phải thủ công tìm kiếm và so sánh file JSON một cách mệt mỏi.

**Workflow này giải quyết tất cả những vấn đề đó!** Nó tự động:
✅ **Lưu tất cả workflow n8n** vào kho GitLab của bạn.
✅ **Tạo phiên bản mới** mỗi khi có thay đổi.
✅ **So sánh phiên bản** để theo dõi lịch sử thay đổi.
✅ **Khôi phục nhanh chóng** nếu workflow bị lỗi hoặc mất.

Không cần viết code, không cần kiến thức lập trình – chỉ cần **cài đặt và chạy**, workflow sẽ tự động hoạt động 24/7.

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động **ổn định và an toàn**, các sếp nên cài đặt n8n trên **VPS riêng** (Self-hosted) để tránh rủi ro mất dữ liệu khi máy chủ bị reset.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (Đảm bảo tốc độ và ổn định)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Bảo vệ workflow**: Không còn lo sợ mất dữ liệu khi máy chủ bị reset hoặc xóa nhầm.
- **Quản lý phiên bản**: Mỗi lần thay đổi workflow sẽ tự động tạo phiên bản mới trong GitLab.
- **So sánh thay đổi**: Xem được sự khác biệt giữa các phiên bản để theo dõi lịch sử.
- **Khôi phục nhanh**: Khôi phục bất kỳ phiên bản nào trong kho lưu trữ một cách dễ dàng.
- **Tự động hóa hoàn toàn**: Chỉ cần chạy workflow một lần, nó sẽ hoạt động liên tục mà không cần can thiệp.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản GitLab**:
   - Một **repository GitLab** để lưu workflow (có thể là private hoặc public).
   - **Personal Access Token** (API Key) của GitLab với quyền:
     - `api` (để đọc và tạo file).
     - `write_repository` (để chỉnh sửa file).
   - **Thư mục trong repo** (ví dụ: `n8n-workflows/`) để lưu workflow.

2. **Tài khoản n8n**:
   - **API Key của n8n** (để lấy danh sách workflow hiện tại).
   - **Credentials "n8nApi"** trong n8n đã được cấu hình với API Key này.

3. **Node GitLab trong n8n**:
   - Cần cài đặt **n8n-node-gitlab** (nếu chưa có).
   - **Credentials "gitlabApi"** trong n8n đã được cấu hình với:
     - **URL GitLab** (ví dụ: `https://gitlab.com`).
     - **Personal Access Token** (API Key) của GitLab.

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow bằng cách:
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/2385) và import vào n8n Editor.
- **Copy JSON** từ link trên và paste vào n8n Editor (đường dẫn: `https://n8n.io/workflows/2385` → Nhấn "Copy JSON").

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này hoạt động theo **2 phần chính**: **Lấy workflow từ n8n** và **Lưu vào GitLab**. Dưới đây là các bước cấu hình quan trọng:

##### **A. Cấu hình Credentials**
1. **Credentials "n8nApi"**:
   - Đi đến **Settings → Credentials** trong n8n.
   - Tạo một **new credential** với tên `n8nApi`.
   - Chọn **n8n API** và điền:
     - **API Key**: API Key của n8n (tìm trong `Settings → General → API Key`).
     - **Host**: `http://localhost:5678` (nếu n8n chạy trên localhost) hoặc URL của VPS nếu self-hosted.

2. **Credentials "gitlabApi"**:
   - Tạo một **new credential** với tên `gitlabApi`.
   - Chọn **GitLab** và điền:
     - **URL**: `https://gitlab.com` (hoặc URL của GitLab self-hosted).
     - **Personal Access Token**: API Key của GitLab (tạo trong `Settings → Access Tokens`).
     - **Project ID**: ID của repository bạn muốn lưu workflow (tìm trong URL của repo: `https://gitlab.com/username/repo/-/tree/main` → ID là `username/repo`).

##### **B. Cấu hình Node "Retrieve all workflows"**
- Node này **lấy danh sách tất cả workflow** từ n8n.
- **Không cần chỉnh sửa gì** nếu credentials `n8nApi` đã được cấu hình đúng.

##### **C. Cấu hình Node "Get file" và "Create file"**
- Node này **tải file workflow** từ GitLab (nếu đã tồn tại) hoặc **tạo file mới**.
- **Không cần chỉnh sửa** nếu credentials `gitlabApi` đã đúng.
- **Tham số quan trọng**:
  - **File Path**: Đặt là `n8n-workflows/{{$node["Loop Over Workflows"].json["$.name"]}}.json` (để lưu workflow vào thư mục `n8n-workflows/` với tên là tên workflow).
  - **Content**: Sử dụng dữ liệu từ node `Extract From File` (sẽ được xử lý tự động).

##### **D. Cấu hình Node "Switch" (So sánh phiên bản)**
- Node này **so sánh phiên bản cũ và mới** của workflow.
- **Không cần chỉnh sửa** nếu muốn sử dụng logic mặc định:
  - Nếu **file không tồn tại** → Tạo file mới.
  - Nếu **file tồn tại** → So sánh và cập nhật.

##### **E. Cấu hình Node "New file version" (Cập nhật phiên bản)**
- Node này **chỉnh sửa file** trong GitLab nếu có thay đổi.
- **Không cần chỉnh sửa** nếu credentials `gitlabApi` đã đúng.

##### **F. Cấu hình Node "Save each version in a different field"**
- Node này **lưu phiên bản mới** vào một trường riêng biệt trong file JSON.
- **Không cần chỉnh sửa** nếu muốn sử dụng logic mặc định (tự động thêm trường `versions` để lưu lịch sử).

---

#### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Nhấn **"Test Workflow"** để chạy thử với dữ liệu mẫu.
   - Kiểm tra **GitLab** để xem workflow đã được lưu chưa.
   - Nếu có lỗi, kiểm tra:
     - Credentials `n8nApi` và `gitlabApi` có đúng không?
     - Thư mục `n8n-workflows/` có tồn tại trong repo không?
     - API Key của GitLab có quyền đủ không?

2. **Bật Active**:
   - Sau khi test thành công, bật **Active** để workflow chạy tự động định kỳ.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Chạy định kỳ với Cron Job**:
   - Sử dụng **Cron Job** (nếu n8n chạy trên VPS) để chạy workflow mỗi ngày/lần một tuần:
     ```bash
     0 0 * * * curl -X POST http://<IP_VPS>:5678/webhook/your-webhook-id -H "Content-Type: application/json" -d '{}'
     ```
   - Thay `<IP_VPS>` bằng IP của VPS và `your-webhook-id` bằng ID của node `manualTrigger` trong workflow.

2. **Lưu log hoạt động**:
   - Thêm node **Slack/Telegram** để báo cáo khi workflow được lưu hoặc có lỗi:
     ```json
     {
       "name": "Notify on Slack",
       "type": "slack",
       "credentials": ["slackApi"],
       "keyParameters": {
         "text": "Workflow {{$node["Loop Over Workflows"].json["$.name"]}} đã được lưu thành công!"
       }
     }
     ```

3. **Tạo báo cáo phiên bản**:
   - Sử dụng node **Google Sheets** hoặc **Notion** để tự động tạo báo cáo phiên bản mới:
     ```json
     {
       "name": "Update Version Report",
       "type": "googleSheets",
       "credentials": ["googleSheetsApi"],
       "keyParameters": {
         "sheetName": "Version Report",
         "range": "A1",
         "values": [
           ["Workflow", "{{$node["Loop Over Workflows"].json["$.name"]}}"],
           ["Version", "{{$node["Status new"].json["version"]}}"],
           ["Date", "{{$node["Status new"].json["date"]}}"]
         ]
       }
     }
     ```

4. **Khôi phục phiên bản cũ**:
   - Nếu workflow bị lỗi, bạn có thể **tải phiên bản cũ** từ GitLab và import vào n8n:
     ```bash
     curl -X GET https://gitlab.com/username/repo/-/raw/main/n8n-workflows/old-workflow.json -o workflow.json
     ```
     Sau đó import vào n8n.

---

### 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** để các sếp **bảo vệ, quản lý và khôi phục** workflow n8n một cách tự động. Không cần viết code, không cần kiến thức phức tạp – chỉ cần **cài đặt và chạy**, workflow sẽ tự động lưu tất cả phiên bản của bạn vào GitLab.

**Hành động ngay hôm nay!**
1. **Cài đặt n8n trên VPS** (nếu chưa có).
2. **Import workflow** và cấu hình credentials.
3. **Bật Active** và bắt đầu tự động hóa quản lý workflow của mình!

**Nếu có vấn đề**, hãy để lại comment bên dưới hoặc liên hệ với cộng đồng n8n để được hỗ trợ. Chúc các sếp thành công! 🚀