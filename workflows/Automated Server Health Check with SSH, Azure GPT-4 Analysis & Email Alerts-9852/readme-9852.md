---
title: "🚀 **Tự Động Hóa Kiểm Tra Trạng Thái Server Với SSH + AI Azure GPT-4 & Thông Báo Email Tự Động**"
description: "Giải pháp tự động hóa 100% không code để giám sát hệ thống server 24/7, phát hiện sự cố CPU/memory/disk, phân tích bằng AI GPT-4 và gửi cảnh báo email tự động. Giúp các sếp DevOps tiết kiệm thời gian và giảm thiểu rủi ro."
slug: "tieu-dong-hoa-kiem-tra-trang-thai-server-ssh-ai-email"
tags: [n8n, automation, devops, ssh, azure-openai, email-alerts]
keywords: [n8n workflow server monitoring, tự động hóa kiểm tra server, SSH + AI GPT-4, cảnh báo email tự động, giám sát hệ thống 24/7]
---

# 🚀 **Tự Động Hóa Kiểm Tra Trạng Thái Server Với SSH + AI Azure GPT-4 & Thông Báo Email Tự Động**

## **🔥 Nỗi Đau Của Các Sếp DevOps & Sysadmin**
Hàng ngày, các sếp phải:
- **Thủ công** kiểm tra CPU, memory, disk, và các dịch vụ trên server bằng các lệnh SSH.
- **Phân tích** dữ liệu thô từ `top`, `df`, `free` để phát hiện sự cố như CPU overloaded, disk full, hoặc dịch vụ ngừng hoạt động.
- **Gọi điện/email** đồng nghiệp khi phát hiện vấn đề, gây mất thời gian và dễ bỏ sót.

**Workflow này giải quyết tất cả!** Nó tự động:
✅ **Lấy dữ liệu** từ server qua SSH (CPU, memory, disk, services, network, top processes).
✅ **Phân tích bằng AI GPT-4** để phát hiện sự cố và đưa ra khuyến nghị.
✅ **Gửi email cảnh báo** tự động khi có vấn đề (hoặc tổng kết trạng thái bình thường).

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần kiểm tra thủ công hàng giờ.
- **Phát hiện sự cố sớm**: AI GPT-4 phân tích chi tiết và cảnh báo ngay khi có dấu hiệu bất thường.
- **Cá nhân hóa cảnh báo**: Email bao gồm tổng kết trạng thái server + khuyến nghị sửa chữa.
- **Hoạt động 24/7**: Dựa trên **Schedule Trigger**, workflow chạy tự động theo lịch (ví dụ: mỗi 5 phút).
- **Dễ mở rộng**: Thêm server hoặc thay đổi lệnh SSH một cách đơn giản.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
1. **Tài khoản SSH** vào server cần giám sát (đảm bảo có quyền `sudo` để chạy lệnh `systemctl`).
2. **API Key Azure OpenAI**:
   - Đăng ký tại [Azure OpenAI](https://azure.microsoft.com/en-us/products/cognitive-services/openai-service/) và tạo **API Key**.
   - Thêm vào **Credentials** của n8n với tên `azure-openai` (cấu hình chi tiết ở phần **Cách import**).
3. **Thông tin SMTP** để gửi email:
   - **Host** (ví dụ: `smtp.gmail.com`).
   - **Port** (ví dụ: `587`).
   - **Tên người dùng & mật khẩu** (sử dụng **App Password** nếu là Gmail).
   - Thêm vào **Credentials** của n8n với tên `smtp`.
4. **Email nhận cảnh báo**: Địa chỉ email của bạn hoặc nhóm đồng nghiệp.
5. **n8n Self-Hosted** (không dùng phiên bản cloud để đảm bảo dữ liệu an toàn).
:::

---

## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Từ File JSON**
1. Tải workflow từ [đây](https://n8n.io/workflows/9852) (ấn **Export**).
2. Trên **n8n Editor**, nhấn **Import** → Chọn file JSON vừa tải.
3. Chọn **Self-Hosted Instance** của bạn và nhấn **Import**.

#### **Phương pháp 2: Copy/Paste JSON**
1. Mở **n8n Editor** → Tạo workflow mới.
2. Nhấn **Import** → Chọn **Paste JSON** và dán toàn bộ mã từ [link gốc](https://n8n.io/workflows/9852).
3. Chọn **Self-Hosted Instance** và nhấn **Import**.

---

### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**

#### **🔹 Node 1: Schedule Trigger**
- **Cấu hình**:
  - **Cron Expression**: Thay đổi theo lịch kiểm tra (ví dụ: `*/5 * * * *` để chạy mỗi 5 phút).
  - **Time Zone**: Chọn múi giờ phù hợp (ví dụ: `Asia/Ho_Chi_Minh`).
- **Lưu ý**:
  - Nếu workflow chạy quá nhiều, có thể điều chỉnh thời gian để tránh quá tải server.

#### **🔹 Node 2: Execute a Command (SSH)**
- **Cấu hình**:
  - **Host**: Địa chỉ IP hoặc tên miền của server (ví dụ: `your-server-ip`).
  - **Port**: Cổng SSH (mặc định là `22`).
  - **Username**: Tên người dùng SSH (ví dụ: `root` hoặc `ubuntu`).
  - **Password/Private Key**: Chọn **Private Key** (an toàn hơn) và điền nội dung từ file `~/.ssh/id_rsa` (nếu dùng SSH key).
  - **Commands**: Các lệnh đã có sẵn trong workflow (không cần chỉnh sửa trừ khi muốn thêm/bỏ lệnh).
    ```bash
    echo "---SYSTEM INFO---"; hostname; uptime;
    echo "---CPU---"; top -bn1 | grep "Cpu(s)";
    echo "---MEMORY---"; free -m;
    echo "---DISK---"; df -h;
    echo "---SERVICES---"; systemctl list-units --type=service --state=running;
    echo "---NETWORK---"; ip -s link;
    echo "---TOP PROCESSES---"; ps -eo pid,comm,%cpu,%mem --sort=-%cpu | head -n 10
    ```
- **Lưu ý**:
  - Nếu server có **firewall**, đảm bảo cổng `22` mở cho IP của bạn.
  - Nếu lệnh `systemctl` không hoạt động, thử thay bằng `service --status-all`.

#### **🔹 Node 3: Azure OpenAI Chat Model**
- **Cấu hình**:
  - **Credentials**: Chọn `azure-openai` (đã thêm ở phần **Yêu cầu cần thiết**).
  - **Model**: Để mặc định là `gpt-4.1` (hoặc chọn `gpt-4` nếu có).
  - **Temperature**: Để `0.7` (giá trị cân bằng giữa sáng tạo và logic).
  - **Prompt**: Workflow tự động sử dụng template phân tích hệ thống. **Không cần chỉnh sửa** trừ khi muốn thay đổi cách AI trả lời.
- **Lưu ý**:
  - **Giá tiền**: Azure OpenAI tính phí theo số token. Để tiết kiệm, có thể giảm **Temperature** xuống `0.3` nếu không cần AI quá sáng tạo.
  - **Rate Limit**: Nếu gặp lỗi `429`, giảm số lần gọi API hoặc tăng thời gian giữa các lần chạy.

#### **🔹 Node 4: AI Agent**
- **Cấu hình**:
  - **Model**: Chọn `Azure OpenAI Chat Model` (node trước đó).
  - **Output Parser**: Chọn `Structured Output Parser` (node tiếp theo).
  - **Lưu ý**: Workflow tự động cấu hình. **Không cần chỉnh sửa** trừ khi muốn thay đổi logic phân tích.

#### **🔹 Node 5: Structured Output Parser**
- **Cấu hình**:
  - **Schema**: Workflow tự động định dạng output thành JSON. **Không cần chỉnh sửa**.
  - **Lưu ý**: Nếu AI trả lời không rõ ràng, có thể chỉnh sửa **Prompt** trong node `Azure OpenAI Chat Model` để yêu cầu format cụ thể.

#### **🔹 Node 6: Send Email**
- **Cấu hình**:
  - **Credentials**: Chọn `smtp` (đã thêm ở phần **Yêu cầu cần thiết**).
  - **To**: Địa chỉ email nhận cảnh báo (ví dụ: `devops-team@example.com`).
  - **Subject**: Để mặc định hoặc thay đổi thành `"[ALERT] Trạng Thái Server: {{ $node["Execute a command"].json["hostname"] }}"`.
  - **HTML Content**: Workflow tự động lấy nội dung từ AI. **Không cần chỉnh sửa** trừ khi muốn thay đổi định dạng email.
- **Lưu ý**:
  - **Nếu email không gửi được**:
    - Kiểm tra **SMTP credentials** (đặc biệt là **App Password** cho Gmail).
    - Thử gửi email test từ **n8n** trước khi chạy workflow.
    - Nếu dùng **Gmail**, đảm bảo **Less Secure Apps** được bật (hoặc sử dụng **App Password**).

---

### **3. Kích Hoạt ⚡️**
1. **Test Run** (để kiểm tra trước khi chạy thực tế):
   - Nhấn **Run Workflow** và chọn **Test Execution**.
   - Kiểm tra **Output** của mỗi node để đảm bảo:
     - Lệnh SSH chạy thành công.
     - AI phân tích dữ liệu và trả về kết quả hợp lý.
     - Email được gửi đúng định dạng.
2. **Bật Active**:
   - Sau khi test thành công, nhấn **Active** để workflow chạy tự động theo lịch.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**

### **1. Thêm Server Khác**
- **Cách 1**: Sao chép **Execute a Command** node và chỉnh sửa thông tin SSH (Host, Username, Private Key).
- **Cách 2**: Tạo **Workflow mới** và sử dụng cùng một **AI Agent** và **Email** node.

### **2. Lưu Log Lịch Sử**
- Thêm **n8n-nodes-base.database** (SQLite) để lưu dữ liệu kiểm tra server vào cơ sở dữ liệu.
- Sau đó, có thể tạo **Báo cáo định kỳ** (ví dụ: mỗi ngày) bằng **Google Sheets** hoặc **Slack**.

### **3. Kết Nối Với Slack/Telegram**
- Thay vì email, có thể gửi cảnh báo qua **Slack** hoặc **Telegram Bot** bằng node `n8n-nodes-base.slack` hoặc `n8n-nodes-base.telegram`.
- **Mẹo**: Sử dụng **Webhook** của Slack/Telegram để nhận thông báo tức thời.

### **4. Thay Đổi Threshold Cảnh Báo**
- Nếu muốn AI cảnh báo khi **CPU > 90%** hoặc **Disk > 85%**, chỉnh sửa **Prompt** trong node `Azure OpenAI Chat Model` như sau:
  ```plaintext
  Analyze the server data and return structured JSON with:
  - "status": "healthy" or "warning" or "critical"
  - "issues": [
      {"type": "high_cpu", "severity": "critical", "recommendation": "..."},
      {"type": "low_disk", "severity": "warning", "recommendation": "..."}
  ]
  Only mark as "critical" if CPU > 90% or disk < 10% free.
  ```

### **5. Sử Dụng AI Local (Nếu Azure OpenAI Đắt)**
- Thay thế node `lmChatAzureOpenAi` bằng `n8n-nodes-base.llm` (nếu cài đặt mô hình AI local như Ollama).
- **Lưu ý**: Chất lượng phân tích có thể kém hơn GPT-4.

---

## 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp DevOps muốn:
✔ **Giám sát server 24/7** mà không cần cài phần mềm phức tạp.
✔ **Phát hiện sự cố sớm** nhờ AI GPT-4 phân tích chi tiết.
✔ **Tiết kiệm thời gian** bằng cách tự động hóa cảnh báo email.

**🚀 Hành động ngay!**
1. **Import workflow** và cấu hình theo hướng dẫn.
2. **Test run** để đảm bảo mọi thứ hoạt động.
3. **Bật Active** và quên đi lo lắng về server!

---
**💡 Gợi ý thêm**: Nếu cần **giám sát nhiều server**, có thể sử dụng **n8n Workflow Templates** để tạo nhiều phiên bản riêng biệt cho từng server.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**📌 Chú ý**: Nếu gặp vấn đề, hãy kiểm tra **Logs** trong n8n và chia sẻ ở [Community n8n](https://community.n8n.io/) để được hỗ trợ!