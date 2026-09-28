---
title: "🚀 Tự Động Hóa Pipeline Triển Khai Quy Tắc Wazuh: Từ GitHub → Kiểm Tra XML → Telegram Alerts (Không Code)"
description: "Workflow tự động hóa hoàn toàn triển khai quy tắc bảo mật Wazuh từ GitHub, kiểm tra tính hợp lệ XML và gửi thông báo Telegram tự động. Giúp đội SOC tiết kiệm 80% thời gian kiểm tra thủ công và giảm thiểu lỗi triển khai."
slug: "tieu-dong-hoa-pipeline-trien-khai-quy-tac-wazuh"
tags: [n8n, automation, secops, threat-hunting, github-actions, telegram-alerts, xml-validation, wazuh]
keywords: [tự động hóa wazuh, pipeline triển khai quy tắc bảo mật, n8n workflow secops, kiểm tra xml tự động, alert telegram bảo mật, giảm thiểu lỗi triển khai]
---

# 🚀 **Tự Động Hóa Pipeline Triển Khai Quy Tắc Wazuh: Từ GitHub → Kiểm Tra XML → Telegram Alerts**

### **Giải pháp cho đội SOC: Triển khai quy tắc bảo mật Wazuh chỉ trong vài giây, không cần code**
Hiện nay, đội SOC thường phải thực hiện thủ công việc **triển khai quy tắc bảo mật Wazuh** từ các thay đổi trên GitHub, kiểm tra tính hợp lệ của file XML, và khởi động lại dịch vụ. Quá trình này không chỉ tốn thời gian mà còn dễ xảy ra lỗi do con người. **Workflow này tự động hóa toàn bộ quy trình**, giúp các sếp:
- **Triển khai quy tắc mới** ngay khi có commit trên GitHub.
- **Kiểm tra tính hợp lệ XML** trước khi triển khai.
- **Gửi thông báo Telegram tự động** khi thành công/thất bại.
- **Khởi động lại Wazuh_manager** một cách an toàn.
- **Giảm thiểu 80% thời gian kiểm tra thủ công** và lỗi triển khai.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động 24/7 với độ tin cậy cao, các sếp nên **self-host n8n** trên VPS chuyên dụng:
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (đủ sức mạnh cho workflow SecOps)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian**: Triển khai quy tắc chỉ trong vài giây thay vì thủ công mất nhiều giờ.
✅ **Chính xác 100%**: Kiểm tra XML và logic triển khai tự động, không bị lỗi do con người.
✅ **Thông báo tức thời**: Nhận cảnh báo Telegram khi thành công/thất bại, không cần check thủ công.
✅ **An toàn**: Khởi động lại Wazuh_manager một cách tự động và kiểm soát.
✅ **Phù hợp với DevOps/SOC**: Hoàn toàn tự động hóa, không cần can thiệp người dùng.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản GitHub** với quyền push/pull vào repository chứa quy tắc Wazuh.
2. **Kết nối SSH** đến máy chủ Wazuh (cần **private key** và thông tin host).
3. **Token Telegram Bot** để gửi thông báo (tạo tại [@BotFather](https://t.me/BotFather)).
4. **API Key n8n** (nếu self-host, cần cấu hình trong n8n).
5. **File quy tắc Wazuh** được lưu trong repository GitHub (định dạng `.xml`).
6. **Wazuh_manager** đã cài đặt và chạy trên máy chủ.

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n Workflow gốc](https://n8n.io/workflows/7226).
- **Import vào n8n Editor**:
  - Mở n8n Dashboard → **Create Workflow** → **Import from JSON**.
  - Chọn file JSON đã tải và nhấn **Import**.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này gồm **14 node** với logic phức tạp. Dưới đây là hướng dẫn chi tiết để cấu hình:

##### **A. Cấu hình GitHub Trigger**
- Node: **"Github Trigger"**
  - **Repository URL**: Điền URL repo chứa quy tắc Wazuh (ví dụ: `https://github.com/doanhnghiep/wazuh-rules.git`).
  - **Branch**: Chọn branch cần theo dõi (ví dụ: `main`).
  - **Credentials**: Tạo mới trong n8n với **Personal Access Token** (PAT) từ GitHub (quyền: `repo`).
  - **Event**: Chọn `Push` để kích hoạt khi có commit mới.

##### **B. Cấu hình SSH (Upload & Restart Wazuh)**
- Node: **"Upload a file"**, **"Restart Wazuh_manager"**, **"Deploying the Rules"**, **"Rule Validation"**
  - **Host**: Điền IP hoặc domain của máy chủ Wazuh.
  - **Port**: Thường là `22` (SSH default).
  - **Credentials**: Tạo mới trong n8n với **Private Key** (lấy từ `~/.ssh/id_rsa` hoặc file tương tự).
  - **Commands**:
    - **Upload file**: `scp {{ $node["Extract Changed Files"].json["file_path"] }} user@host:/var/ossec/rules/` (đảm bảo đường dẫn đúng).
    - **Deploy rules**: `sudo /var/ossec/bin/wazuh-control restart`.
    - **Kiểm tra XML**: `sudo /var/ossec/bin/wazuh-control validate-rules`.

##### **C. Cấu hình Telegram Alerts**
- Node: **"❌ Failure Message"**, **"✅ Success Message"**
  - **Bot Token**: Điền token bot Telegram (ví dụ: `123456789:ABCdefGHIJKlmnOPQRstUVWxyz`).
  - **Chat ID**: Lấy từ [@userinfobot](https://t.me/userinfobot) và gửi tin nhắn `/start`.
  - **Message Template**:
    - **Thành công**:
      ```plaintext
      🚀 Quy tắc Wazuh mới đã triển khai thành công!
      File: {{ $node["Extract Changed Files"].json["file_name"] }}
      ```
    - **Thất bại**:
      ```plaintext
      ❌ Lỗi khi triển khai quy tắc Wazuh!
      Lỗi: {{ $node["Rule Validation"].json["error"] }}
      ```

##### **D. Cấu hình Logic If (Kiểm tra điều kiện)**
- Node: **"Valid Commit for Deployment"**, **"Rule Validation check"**, **"Final Confirmation check"**
  - **Điều kiện kiểm tra**:
    - **Valid Commit**: Kiểm tra commit có chứa từ khóa `wazuh-rule` trong message.
    - **XML Valid**: Kiểm tra output của `Rule Validation` có lỗi không.
    - **Final Confirmation**: Xác nhận cuối cùng trước khi triển khai.

##### **E. Node "No Operation" (Skip)**
- Node: **"No Operation, do nothing"**
  - Sử dụng khi không cần xử lý tiếp (ví dụ: commit không hợp lệ).

---

#### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Thực hiện một commit mới trên GitHub với message chứa `wazuh-rule`.
   - Kiểm tra workflow có chạy và gửi thông báo Telegram không.
2. **Bật Active**:
   - Sau khi test thành công, nhấn **Active** trên workflow.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Kết hợp với Slack**:
   - Thay thế Telegram bằng **Slack Webhook** để thông báo trong Slack Team.
   - Cấu hình node `httpRequest` với endpoint Slack Webhook.

2. **Lưu log triển khai**:
   - Thêm node `code` để ghi log vào file `~/wazuh-deploy.log` với thời gian và nội dung triển khai.

3. **Triển khai cho nhiều repo**:
   - Sử dụng **GitHub Multi-Trigger** bằng cách tạo nhiều workflow riêng hoặc sử dụng node `code` để lặp qua nhiều repo.

4. **Kiểm tra tự động hàng ngày**:
   - Sử dụng **n8n Cron Trigger** để chạy kiểm tra quy tắc định kỳ (ví dụ: mỗi ngày 3h sáng).

5. **Báo cáo tự động**:
   - Thêm node `email` để gửi báo cáo hàng tuần về quy tắc đã triển khai thành công/thất bại.

---

### 📌 **Kết luận**
Workflow này **tự động hóa hoàn toàn quy trình triển khai quy tắc Wazuh**, giúp đội SOC:
✔ **Tiết kiệm thời gian** lên đến 80% so với cách thủ công.
✔ **Giảm thiểu lỗi** nhờ kiểm tra XML tự động.
✔ **Nhận thông báo tức thời** qua Telegram.
✔ **Hoàn toàn an toàn** với logic kiểm tra trước triển khai.

**Hành động ngay!**
- Import workflow vào n8n của mình.
- Cấu hình theo hướng dẫn chi tiết trên.
- **Triển khai quy tắc Wazuh chỉ trong vài giây**, không cần can thiệp người dùng!

---
**💡 Cần hỗ trợ thêm?**
- Trả lời câu hỏi tại [n8n Community](https://community.n8n.io/).
- Liên hệ tác giả [@mariskarthick](https://github.com/mariskarthick) để đóng góp cải tiến.