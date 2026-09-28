---
title: "🛡️ CI Artifact Completeness Gate: Kiểm Tra Tự Động Tệp Build Trước Khi Merge Code (GitHub + Sentry)"
description: "Workflow tự động hóa kiểm tra toàn bộ các tệp build cần thiết (dSYM, ProGuard, Mapping) trên Sentry trước khi cho phép merge PR trên GitHub. Giúp các sếp tránh tình trạng merge code không đầy đủ artifact, tiết kiệm thời gian debug và đảm bảo chất lượng CI/CD."
slug: "ci-artifact-completeness-gate-github-sentry"
tags: [n8n, automation, DevOps, CI/CD, GitHub, Sentry, no-code, code-node]
keywords: [n8n workflow CI/CD, tự động hóa kiểm tra artifact, GitHub trigger, Sentry API, dSYM ProGuard, kiểm tra merge PR]
---

# 🚀 **Kiểm Tra Tự Động Tệp Build Trước Khi Merge Code: CI Artifact Completeness Gate**

Hãy tưởng tượng một tình huống phổ biến trong các dự án phần mềm: các sếp đã push code lên branch `main` nhưng quên upload các tệp build quan trọng như **dSYM** (iOS), **ProGuard** (Android), hoặc **Mapping files** (Firebase Crashlytics) lên **Sentry**. Kết quả? PR bị block, team phải debug lại, và tiến độ dự án bị trì hoãn. **Workflow này giải quyết vấn đề đó 100% tự động hóa, không cần viết code!**

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy 24/7 với hiệu suất tối ưu, các sếp nên **self-host n8n** trên VPS. Dưới đây là 2 lựa chọn đáng tin cậy:
👉 [**Đăng ký VPS TinoHost**](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới 39%)
👉 [**Đăng ký VPS Xeon 4GB chỉ 50k/tháng**](https://my.bnix.one/aff.php?aff=172) (đảm bảo ổn định cho CI/CD)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động block PR không đầy đủ artifact**: Ngăn chặn merge code thiếu tệp quan trọng như **dSYM**, **ProGuard**, hoặc **Mapping files**.
- **Tiết kiệm thời gian debug**: Không cần phải tra cứu thủ công trên Sentry sau khi merge.
- **Chất lượng CI/CD cao**: Đảm bảo mỗi commit chỉ được merge khi tất cả artifact cần thiết đã được upload.
- **Hỗ trợ multi-platform**: Kiểm tra cả iOS (dSYM), Android (ProGuard), và Firebase (Mapping files).
- **Hiển thị trạng thái rõ ràng**: Commit sẽ có **checkmark xanh** nếu artifact đầy đủ, **đỏ** nếu thiếu.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản GitHub**:
   - **GitHub Personal Access Token** (với quyền `repo` và `admin:repo_hook`).
   - **Repository** cần kiểm tra artifact (cấu hình trong **GithubPushTrigger**).
2. **Tài khoản Sentry**:
   - **API Token** của Sentry (tạo tại **Settings > API Tokens**).
   - **Project Slug** của dự án bạn đang sử dụng (ví dụ: `my-app-name`).
3. **Thông tin dự án**:
   - **Release Version Pattern**: Cách Sentry định danh phiên bản (thường là `commit_sha` hoặc `tag_name`).
   - **Danh sách tệp bắt buộc**:
     - **dSYM** (iOS): `*.dSYM/Contents/Resources/DWARF/*.dSYM`.
     - **ProGuard** (Android): `proguard.txt`.
     - **Mapping files** (Firebase): `mapping.txt`.

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
- **Bước 1**: Tải file JSON từ [n8n.io/workflows/11828](https://n8n.io/workflows/11828).
- **Bước 2**: Mở **n8n Editor** → Nhấn **Import** → Chọn file JSON.
- **Bước 3**: Chọn **Create New Workflow** và đặt tên (ví dụ: `CI Artifact Gate`).

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow gồm **6 node chính**, các sếp cần cấu hình kỹ lưỡng như sau:

##### **🔹 Node 1: GithubPushTrigger (GithubTrigger)**
- **Cấu hình**:
  - **Credentials**: Chọn `githubApi` (đã cấu hình trước).
  - **Repository**: Chọn repo cần kiểm tra.
  - **Branch**: Chỉ định branch (ví dụ: `main`).
  - **Trigger**: Chọn **Push Events** (hoặc Webhook nếu ưu tiên).
- **Lưu ý**:
  - Node này sẽ **bắt đầu workflow** khi có push mới.
  - **Output**: Sẽ chứa `commit_sha` và `repository` (sử dụng trong các node sau).

##### **🔹 Node 2 & 3: Check Sentry Artifacts Releases & Check Sentry Artifacts Files (HTTP Request)**
- **Cấu hình chung**:
  - **Credentials**: Không cần (sử dụng **API Token** trong header).
  - **URL**:
    - **Node 2**: `https://sentry.io/api/0/projects/{project_slug}/releases/`
    - **Node 3**: `https://sentry.io/api/0/projects/{project_slug}/releases/{{$json.version}}/files/`
  - **Headers**:
    ```json
    {
      "Authorization": "Bearer {{$credentials.sentryApiToken}}",
      "Content-Type": "application/json"
    }
    ```
  - **Interpolation**:
    - Thay `{{project_slug}}` bằng **Project Slug** của bạn (ví dụ: `my-app`).
    - Thay `{{$json.version}}` bằng **version** từ `GithubPushTrigger` (thường là `commit_sha`).
- **Lưu ý**:
  - **Node 2** lấy danh sách **tất cả releases** trên Sentry.
  - **Node 3** lấy **danh sách file** của release cụ thể (sử dụng `version` từ `GithubPushTrigger`).

##### **🔹 Node 4 & 6: Verify Artifacts & Artifacts Validation and Get Repository Data (Code)**
- **Cấu hình**:
  - **Code Node 4** (Verify Artifacts):
    ```javascript
    // Logic kiểm tra tệp bắt buộc
    const requiredFiles = {
      ios: ['*.dSYM/Contents/Resources/DWARF/*.dSYM'],
      android: ['proguard.txt'],
      firebase: ['mapping.txt']
    };

    const artifacts = $input.all()[0].json;
    let isValid = false;
    let message = '';

    // Kiểm tra dSYM (iOS)
    if (artifacts.some(file => file.filename.includes('.dSYM'))) {
      isValid = true;
      message = '✅ dSYM file found (iOS)';
    }
    // Nếu không có dSYM, kiểm tra ProGuard + Mapping (Android/Firebase)
    else if (artifacts.some(file => file.filename === 'proguard.txt') &&
             artifacts.some(file => file.filename === 'mapping.txt')) {
      isValid = true;
      message = '✅ ProGuard + Mapping files found (Android/Firebase)';
    }
    else {
      message = '❌ Missing required artifacts (dSYM OR proguard.txt + mapping.txt)';
    }

    return {
      json: {
        status: isValid ? 'success' : 'failure',
        message: message,
        commit_sha: $input.all()[0].json.commit_sha
      }
    };
    ```
  - **Code Node 6** (Artifacts Validation and Get Repository Data):
    - **Sử dụng kết quả từ Node 4** để quyết định tiếp tục hoặc dừng workflow.
    - **Output**: Nếu `status = failure`, workflow **dừng lại** (không update GitHub).
    - Nếu `status = success`, truyền `commit_sha` sang **Node 5**.

##### **🔹 Node 5: Update Status (HTTP Request)**
- **Cấu hình**:
  - **Credentials**: Chọn `githubApi`.
  - **URL**:
    ```plaintext
    https://api.github.com/repos/{owner}/{repo}/statuses/{commit_sha}
    ```
  - **Headers**:
    ```json
    {
      "Authorization": "Bearer {{$credentials.githubApi.token}}",
      "Accept": "application/vnd.github.v3+json"
    }
    ```
  - **Body (JSON)**:
    ```json
    {
      "state": "{{$json.status}}",
      "target_url": "https://sentry.io/project/{project_slug}/releases/{{$json.version}}/",
      "description": "{{$json.message}}",
      "context": "artifact-gate"
    }
    ```
  - **Interpolation**:
    - Thay `{{owner}}`, `{{repo}}` bằng tên repo của bạn.
    - Thay `{{project_slug}}` bằng **Project Slug** của Sentry.
    - Thay `{{$json.status}}` và `{{$json.message}}` từ **Code Node 4**.
- **Lưu ý**:
  - Nếu `status = success`, GitHub sẽ hiển thị **checkmark xanh**.
  - Nếu `status = failure`, PR sẽ **không thể merge** (do trạng thái commit là `failure`).

---

#### **3. Kích hoạt ⚡️**
- **Test Run**:
  - Push một commit lên branch `main` (hoặc kích hoạt Webhook).
  - Kiểm tra **Code Node 4** để đảm bảo logic kiểm tra hoạt động.
  - Xem trạng thái commit trên GitHub (nếu thành công, sẽ có checkmark).
- **Bật Active**:
  - Nhấn **Active** trên workflow để chạy liên tục.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Kết hợp với Slack/Telegram**:
   - Thêm **Slack/Telegram Node** để thông báo kết quả kiểm tra (thành công/thất bại).
   - Ví dụ: Nếu `status = failure`, gửi tin nhắn:
     ```
     ⚠️ **Artifact Gate Failed** for commit {{commit_sha}}!
     Missing: {{message}}
     ```

2. **Lưu log vào Google Sheets/Notion**:
   - Sử dụng **Google Sheets Node** để ghi lại lịch sử kiểm tra (commit, thời gian, trạng thái).
   - Cấu hình **Sheet Name** và **Range** (ví dụ: `Sheet1!A1`).

3. **Tự động tạo PR từ commit**:
   - Nếu workflow thành công, có thể thêm **GitHub Node** để tự động tạo PR từ branch `feature` sang `main`.

4. **Bộ lọc commit cụ thể**:
   - Thêm **Condition Node** trước `GithubPushTrigger` để chỉ chạy workflow cho commit trên branch `main` hoặc `release/*`.

5. **Cập nhật version động**:
   - Nếu Sentry sử dụng **tag_name** thay vì `commit_sha`, chỉnh sửa **Code Node 4** để lấy version từ tag:
     ```javascript
     const version = $input.all()[0].json.ref.split('/').pop(); // Lấy từ ref (ví dụ: refs/tags/v1.0.0)
     ```

---

### 📌 **Kết luận**
Workflow **CI Artifact Completeness Gate** là **giải pháp hoàn hảo** để các sếp tự động hóa kiểm tra artifact trước khi merge code, tránh tình trạng **merge thiếu tệp quan trọng** và **tiết kiệm thời gian debug**. Với chỉ **6 node** và một chút cấu hình, các sếp đã có thể:
✅ **Đảm bảo chất lượng CI/CD** với artifact đầy đủ.
✅ **Tự động block PR không hợp lệ**.
✅ **Hiển thị trạng thái rõ ràng** trên GitHub.

**Hành động ngay hôm nay!**
1. **Import workflow** và cấu hình theo hướng dẫn.
2. **Test với một commit mẫu** để đảm bảo hoạt động.
3. **Bật Active** và để workflow chạy tự động cho mọi push!

Nếu có bất kỳ câu hỏi hoặc gặp khó khăn, các sếp có thể **comment bên dưới** hoặc liên hệ với **WeblineIndia** (tác giả của workflow) qua [trang web](https://www.weblineindia.com/). **Chúc các sếp thành công với CI/CD tự động hóa!** 🚀