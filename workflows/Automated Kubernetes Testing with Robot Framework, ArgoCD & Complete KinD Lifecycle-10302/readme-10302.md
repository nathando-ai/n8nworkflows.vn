---
title: "🚀 Tự Động Hóa Test Kubernetes Tối Đa Với Robot Framework, ArgoCD & KinD - Không Cần Code!"
description: "Workflow này tự động hóa toàn bộ chu kỳ kiểm thử Kubernetes từ cài đặt Docker, tạo cluster KinD, chạy test tự động bằng Robot Framework đến việc dọn dẹp hoàn toàn. Giúp DevOps tiết kiệm 80% thời gian debug và giảm thiểu lỗi nhân sự."
slug: "tieu-dong-hoa-test-kubernetes-kin-d-robot-framework"
tags: [n8n, devops, automation, kubernetes, robot-framework, kind, argocd, gitlab, ssh, telegram]
keywords: [n8n workflow kubernetes, tự động hóa test docker, robot framework automation, kind cluster automation, devops automation, test kubernetes tự động]
---

# 🚀 **Tự Động Hóa Chu Kỳ Kiểm Thử Kubernetes Toàn Mặt: Từ Cài Đặt Đến Dọn Dẹp**

## **🔥 Nỗi Đau Của Các Sếp DevOps**
Hàng ngày, các sếp phải:
- **Cài đặt Docker và KinD** trên máy chủ từ đầu, mất 30-40 phút mỗi lần.
- **Chạy test thủ công** bằng Robot Framework, lo lắng về môi trường không ổn định.
- **Debug lỗi sau khi deploy**, mất thời gian tìm hiểu log và tái tạo môi trường.
- **Quên dọn dẹp** sau khi test, làm tràn disk và gây nhầm lẫn cho các team khác.

**Workflow này giải quyết tất cả!** Với **n8n**, các sếp có thể:
✅ **Tự động hóa toàn bộ chu kỳ test Kubernetes** (cài đặt → test → dọn dẹp).
✅ **Chạy test Robot Framework với browser automation** và nhận báo cáo kết quả qua Telegram.
✅ **Kiểm soát từng giai đoạn** (INIT, TEST, DESTROY) một cách linh hoạt.
✅ **Tiết kiệm 80% thời gian debug** và giảm thiểu lỗi nhân sự.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động hóa từ cài đặt đến dọn dẹp, chỉ cần 1 click.
- **Môi trường ổn định**: KinD cluster được tạo và phá hủy tự động, tránh xung đột.
- **Báo cáo chi tiết**: Kết quả test được gói gọn và gửi qua Telegram với logs, screenshots.
- **An toàn tuyệt đối**: Dọn dẹp hoàn toàn sau khi test, không để lại rác.
- **Hoàn toàn mở nguồn**: Tùy chỉnh được từng giai đoạn cho phù hợp với dự án.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Máy chủ remote** (Linux) với:
   - SSH port (thường là 22).
   - Quyền sudo để cài đặt Docker, KinD, Helm.
2. **GitLab OAuth2 API Key** (để tải file config, test script, ApplicationSet).
3. **Telegram Bot Token** và **Chat ID** (để nhận báo cáo kết quả).
4. **n8n-nodes-robotframework** (cần cài đặt từ **Community Nodes**).
5. **File mẫu** (được cung cấp trong workflow):
   - `config.yaml` (cấu hình KinD cluster).
   - `test.robot` (script test Robot Framework).
   - `demo-applicationSet.yaml` (ArgoCD ApplicationSet).
6. **Tham số cấu hình** (điền vào workflow):
   ```yaml
   target_host: "IP_máy_chủ_remote"  # Ví dụ: 192.168.1.100
   target_port: 22
   target_user: "root"
   target_password: "mật_khẩu_ssh"
   progress: "INIT"  # hoặc "TEST" hoặc "DESTROY"
   progress_only: false  # true để debug từng giai đoạn
   KIND_CONFIG: "path_đến_config.yaml_trong_GitLab"
   ROBOT_SCRIPT: "path_đến_test.robot_trong_GitLab"
   ARGOCD_APPSET: "path_đến_demo-applicationSet.yaml_trong_GitLab"
   ```

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/10302](https://n8n.io/workflows/10302) hoặc copy/paste JSON vào **n8n Editor**.
- **Cách import nhanh**:
  ```bash
  curl -X POST https://n8n.yourdomain.com/webhook/import -H "Content-Type: application/json" -d @workflow.json
  ```

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này **phức tạp** và có nhiều node cần cấu hình cẩn thận. Dưới đây là **các bước quan trọng**:

##### **A. Cấu Hình GitLab (3 Node)**
- **Node "Get a file - ROBOT Script"**:
  - **Credentials**: Chọn `gitlabOAuth2Api` (đã cấu hình trước).
  - **Parameters**:
    - `owner`: Tên owner repository (ví dụ: `xsreality`).
    - `repository`: Tên repo (ví dụ: `n8n-kind-test`).
    - `branch`: Branch chứa file (ví dụ: `main`).
    - `filePath`: Đường dẫn file trong repo (ví dụ: `test.robot`).
- **Node "Get a file - KinD Config"**:
  - Cấu hình tương tự, nhưng `filePath` là `config.yaml`.
- **Node "Get a file - ArgoCD ApplicationSet"**:
  - `filePath` là `demo-applicationSet.yaml`.

##### **B. Cấu Hình SSH (Các Node `executeCommand`)**
Workflow sử dụng **SSH** để điều khiển máy chủ remote. Các node quan trọng:
- **Node "Check Sshpass Exist Local"**:
  - Kiểm tra xem `sshpass` có cài đặt không. Nếu không, node sau sẽ tự động cài đặt.
- **Node "Check Docker on Target"**:
  - Kiểm tra Docker có cài đặt không. Nếu không, workflow sẽ cài đặt.
- **Node "Create KinD Cluster on Target"**:
  - Thực hiện lệnh:
    ```bash
    kind create cluster --config=/tmp/config.yaml
    ```
  - **Lưu ý**: File `config.yaml` đã được tải từ GitLab và lưu tạm tại `/tmp/config.yaml`.

##### **C. Cấu Hình Robot Framework (Node `n8n-nodes-robotframework`)**
- **Yêu cầu bắt buộc**:
  - Trong script Robot Framework (`test.robot`), **phải chỉ định đường dẫn Chromium**:
    ```robotframework
    New Browser    browser=${BROWSER}    headless=True    executablePath=/usr/bin/chromium-browser
    ```
  - Nếu không, test sẽ thất bại vì không tìm thấy trình duyệt.
- **Node "Robot Framework"**:
  - Tham số `command` sẽ tự động xây dựng từ file `test.robot` và các biến cấu hình.

##### **D. Cấu Hình Telegram (Node "Send ROBOT Script Export Pack")**
- **Tham số cần điền**:
  - `chatId`: ID chat Telegram của bạn (lấy từ `/getUpdates` trong Telegram Bot).
  - `telegramApi`: Credentials Telegram OAuth2 (cấu hình trong n8n).
- **File gửi đi**:
  - Workflow sẽ gói gọn **logs, reports, screenshots** thành một file `.zip` và gửi qua Telegram.

##### **E. Cấu Hình Giai Đoạn (Node "Switch")**
- **Tham số `progress`** quyết định workflow chạy giai đoạn nào:
  - `INIT`: Cài đặt Docker, KinD, Helm, ArgoCD.
  - `TEST`: Chạy test Robot Framework.
  - `DESTROY`: Xóa cluster và dọn dẹp.
- **Tham số `progress_only`**:
  - `false`: Chạy toàn bộ chu kỳ (INIT → TEST → DESTROY).
  - `true`: Dừng sau khi hoàn thành giai đoạn hiện tại (để debug).

---

#### **3. Kích Hoạt ⚡️**
- **Test Run**:
  - Chọn **Manual Trigger** và nhấn **"Execute workflow"**.
  - Kiểm tra log để đảm bảo các giai đoạn chạy đúng.
- **Bật Active**:
  - Sau khi test thành công, chuyển workflow sang **Active**.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[TIPS THỰC TIỆN]
1. **Sử dụng Schedule Trigger** để chạy workflow hàng ngày (ví dụ: 1 AM) để test tự động.
2. **Kết hợp với Slack**:
   - Thêm node **Slack** để báo cáo kết quả ngay khi test thất bại.
   - Cài đặt node `n8n-nodes-slack` từ **Community Nodes**.
3. **Lưu log vào GitLab CI**:
   - Sử dụng node **GitLab** để push logs test vào một repository.
4. **Tự động deploy ứng dụng sau khi test**:
   - Sau khi ArgoCD deploy thành công, thêm node **Kubernetes** để deploy ứng dụng thực tế.
5. **Sử dụng SSH Key thay vì mật khẩu**:
   - Thay vì nhập `target_password`, cấu hình SSH key để an toàn hơn.
6. **Tùy chỉnh KinD config**:
   - Thay đổi `config.yaml` để phù hợp với môi trường Kubernetes của bạn (ví dụ: thêm node worker).
:::

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp DevOps muốn:
✔ **Tự động hóa toàn bộ chu kỳ test Kubernetes** một cách an toàn và hiệu quả.
✔ **Giảm thiểu thời gian debug** và tăng cường tin cậy vào môi trường test.
✔ **Tích hợp với GitLab CI/CD** để chạy test tự động trên mỗi commit.

**Hãy áp dụng ngay và tiết kiệm hàng giờ mỗi tuần!** 🚀

---
:::note[CHÚ Ý CUỐI CÙNG]
- **Nếu gặp lỗi**, kiểm tra log của node `executeCommand` để xác định nguyên nhân.
- **Đối với môi trường sản xuất**, hãy **backup** máy chủ remote trước khi chạy giai đoạn `INIT`.
- **N8n Self-hosted** là lựa chọn tốt nhất để workflow chạy 24/7 ổn định.
:::

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::