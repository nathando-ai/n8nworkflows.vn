---
title: "💾 **Tự Động Hoàn Hảo: Backup Workflows n8n Sang Git Repository Trên Gitea - Không Cần Code!**"
description: "Giải pháp tự động hóa hoàn toàn để sao lưu tất cả workflows n8n của các sếp vào Gitea, bảo vệ dữ liệu và đảm bảo tính liên tục 24/7. Khắc phục nỗi lo mất dữ liệu khi cập nhật hoặc lỗi hệ thống."
slug: "backup-workflows-n8n-gitea"
tags: [n8n, automation, backup, git, gitea, no-code, self-hosted]
keywords: [backup workflow n8n, tự động hóa lưu trữ, sao lưu dữ liệu n8n, gitea n8n, tự động hóa không code, lưu trữ an toàn workflow]
---

# 🚀 **Backup Workflows n8n Sang Gitea: Bảo Vệ Dữ Liệu Của Các Sếp Với Tự Động Hóa 100%**

### **Nỗi Đau Thực Tế Của Các Sếp**
Các sếp đã từng gặp phải tình huống nào sau đây chưa?
- **Lỗi hệ thống** khiến tất cả workflows n8n bị mất hoặc bị hỏng sau khi cập nhật phiên bản mới.
- **Không có bản sao lưu** khi muốn thử nghiệm một workflow mới nhưng sợ làm hỏng hệ thống chính.
- **Quá phiền phức** khi phải sao lưu thủ công mỗi khi có thay đổi, dẫn đến quên hoặc làm sai.

**Workflow này giải quyết tất cả!** Với **Backup Workflows to Git Repository on Gitea**, các sếp có thể **tự động sao lưu tất cả workflows n8n** vào một **repository Git trên Gitea**, đảm bảo dữ liệu an toàn và có thể khôi phục nhanh chóng khi cần.

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Bảo vệ dữ liệu**: Sao lưu tự động tất cả workflows, khắc phục mọi trường hợp mất dữ liệu do lỗi hệ thống hoặc cập nhật.
- **Khôi phục nhanh chóng**: Khi cần, các sếp chỉ cần **pull** lại từ Gitea và **import** vào n8n trong vài phút.
- **Tự động hóa hoàn toàn**: Không cần can thiệp thủ công, workflow chạy định kỳ (ví dụ: hàng ngày) mà không tốn thời gian.
- **Dễ dàng theo dõi thay đổi**: Gitea cho phép xem lịch sử commit, giúp các sếp **hiểu rõ từng bước thay đổi** của workflow.
- **An toàn và bảo mật**: Dữ liệu lưu trữ trên Gitea (hoặc GitLab/GitHub) với **tùy chọn quyền hạn** cao.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Gitea** (hoặc GitLab/GitHub nếu thay thế):
   - Đăng ký tại [Gitea](https://gitea.io/) hoặc sử dụng phiên bản tự host.
   - **Khuyến nghị**: Sử dụng Gitea vì nó **nhẹ nhàng, tự host dễ dàng** và phù hợp với n8n.
2. **Token quyền hạn cao**:
   - **Phải có quyền `repo:write` và `repo:read`** để push/pull workflows.
   - **Cách tạo token**:
     - Mở **Settings → Applications → Generate Token** trên Gitea.
     - Chọn **Scope**: `repo` (đảm bảo có `read` và `write`).
3. **Repository trống** để lưu workflows:
   - Tạo một repo mới (ví dụ: `workflows-backup`) và **không cần init với README** (n8n sẽ tự tạo file).
4. **n8n Self-hosted** (không dùng n8n.cloud):
   - Workflow này **không hoạt động** trên n8n.cloud vì cần quyền API đầy đủ.

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể **import** workflow từ file JSON hoặc **copy/paste** JSON vào **n8n Editor**:
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/2820).
- **Mở n8n Editor** → **Import Workflow** → Chọn file JSON.
- **Hoặc**:
  - Mở **n8n Editor** → **Create New Workflow** → Chọn **Import from JSON**.
  - Dán toàn bộ nội dung JSON vào ô **Paste JSON** và nhấn **Import**.

---

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Sau khi import, các sếp **phải cấu hình** các phần sau để workflow hoạt động:

##### **A. Cấu Hình Global Variables (Globals Node)**
Mở node **Globals** và cập nhật các biến sau:
| Biến | Giá Trị | Ghi Chú |
|------|---------|---------|
| `repo.url` | `https://<tên-máy-chủ-gitea>/gitea` | Thay `<tên-máy-chủ-gitea>` bằng địa chỉ Gitea của các sếp (ví dụ: `https://git.example.com`). |
| `repo.name` | `workflows` | Tên repository lưu workflows (không cần có `.git` ở cuối). |
| `repo.owner` | `<tên-tài-khoản-gitea>` | Tên tài khoản chủ sở hữu repo (không cần `@`). |

**Ví dụ**:
```yaml
repo.url: https://gitea.example.com
repo.name: workflows-backup
repo.owner: octoleo
```

##### **B. Thiết Lập Token Gitea (Credentials)**
1. **Tạo Token Gitea**:
   - Trên Gitea, đi đến **Settings → Applications → Generate Token**.
   - Chọn **Scope**: `repo` (đảm bảo có `read` và `write`).
   - Copy **Personal Access Token** (không bao giờ chia sẻ token này!).

2. **Thêm Credential trong n8n**:
   - Mở **Credentials Manager** (nhấn vào biểu tượng **⚙️** ở góc phải trên n8n Editor).
   - Nhấn **Add Credential** → Chọn **HTTP Header Auth**.
   - **Name**: `httpHeaderAuth` (phải trùng với tên trong nodes).
   - **Value**:
     ```
     Authorization: Bearer <TOKEN_GITEA>
     ```
     **Lưu ý**: Phải có **khoảng trắng sau `Bearer`** trước token!

3. **Gán Credential cho các Node HTTP**:
   - Mở các node sau: **GetGitea**, **PutGitea**, **PostGitea**.
   - Trong phần **Credentials**, chọn `httpHeaderAuth`.

##### **C. Cấu Hình Node Schedule Trigger**
- Mở node **Schedule Trigger**.
- Cập nhật **Schedule** để workflow chạy định kỳ (ví dụ: **0 0 * * *** = hàng ngày lúc 00:00).
- **Lưu ý**: Nếu muốn chạy ngay lập tức, chọn **Manual Trigger** và nhấn **Run Workflow**.

##### **D. Kiểm Tra Node Code (Base64 Encode)**
- Mở node **Base64EncodeCreate** và **Base64EncodeUpdate**.
- **Không cần chỉnh sửa gì** (n8n tự động mã hóa dữ liệu JSON thành Base64 để push lên Gitea).

##### **E. Kiểm Tra Node If (Exist & Changed)**
- Node **Exist** kiểm tra file đã tồn tại trên Gitea chưa.
- Node **Changed** kiểm tra workflow có thay đổi so với phiên bản cũ.
- **Không cần chỉnh sửa**, n8n tự động xử lý.

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Nhấn **Run Workflow** để kiểm tra.
   - Kiểm tra **log** để xem có lỗi nào không.
   - **Kiểm tra repo Gitea**: File workflows nên xuất hiện ở `workflows-backup/`.

2. **Bật Active**:
   - Sau khi test thành công, **bật Active** cho workflow.
   - **Enable Schedule Trigger** để workflow chạy tự động.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Lưu Log Lịch Sử**:
   - Thêm node **Slack/Telegram** để nhận thông báo khi backup thành công/thất bại.
   - **Cách làm**:
     - Thêm node **Slack Webhook** sau **PostGitea** và **PutGitea**.
     - Gửi tin nhắn như:
       ```
       🚀 Backup workflows thành công! (ID: {{ $node["GetGitea"].jsonpath("$.id") }})
       ```

2. **Backup Định Kỳ Theo Lịch**:
   - Thay đổi **Schedule Trigger** để backup vào giờ phù hợp (ví dụ: **0 3 * * *** = 3h sáng).
   - **Không backup vào giờ làm việc** để tránh ảnh hưởng đến hiệu suất.

3. **Khôi Phục Workflow**:
   - Khi cần khôi phục:
     - **Pull** file từ Gitea.
     - **Import** vào n8n bằng cách:
       - Mở **n8n Editor** → **Import Workflow** → Chọn file JSON từ Gitea.

4. **Sử Dụng GitLab/GitHub**:
   - Nếu các sếp dùng **GitLab/GitHub**, thay đổi:
     - `repo.url` thành `https://gitlab.com` hoặc `https://github.com`.
     - **Token** phải có quyền `repo` (trên GitHub là **Personal Access Token** với scope `repo`).

5. **Backup Nhiều Repository**:
   - Sử dụng **node ForEach** để backup nhiều repo khác nhau.
   - **Cách làm**:
     - Thêm node **Set** trước **ForEach** để định nghĩa danh sách repo.
     - Ví dụ:
       ```json
       {
         "repo1": {
           "url": "https://gitea.example.com",
           "name": "workflows1",
           "owner": "octoleo"
         },
         "repo2": {
           "url": "https://gitea.example.com",
           "name": "workflows2",
           "owner": "octoleo"
         }
       }
       ```

---

### 📌 **Kết Luận**
Với **Backup Workflows to Git Repository on Gitea**, các sếp đã **xóa bỏ hoàn toàn nỗi lo mất dữ liệu** khi làm việc với n8n. Workflow này **tự động hóa hoàn toàn**, không cần can thiệp thủ công, và **khôi phục dữ liệu chỉ trong vài giây**.

**Hành động ngay hôm nay!**
1. **Setup Gitea** và tạo repo.
2. **Import workflow** và cấu hình theo hướng dẫn.
3. **Bật Schedule Trigger** để backup tự động.
4. **Quên mất lo lắng** về mất dữ liệu!

**Cần hỗ trợ?** Trên diễn đàn [n8n](https://community.n8n.io/) hoặc liên hệ với tác giả **<<ewe>>yn** qua [GitHub](https://github.com/eweyn).

---
**💡 Mẹo cuối**: Nếu các sếp dùng **n8n.cloud**, có thể **tạo một repo trên GitHub/GitLab** và thay đổi `repo.url` tương ứng. Tuy nhiên, **self-hosted vẫn là lựa chọn an toàn nhất**!