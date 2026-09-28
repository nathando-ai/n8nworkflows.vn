---
title: "🚀 Tự động cài đặt LAMP Stack trên server Linux chỉ với một click"
description: "Workflow n8n tự động thiết lập đầy đủ môi trường LAMP (Linux, Apache, MySQL, PHP) trên máy chủ VPS, giảm thời gian cấu hình từ giờ sang phút."
slug: "tu-dong-cai-dat-lamp-stack-tren-vps"
tags: [n8n, automation, no-code, devops, server-setup, lamp]
keywords: [n8n workflow, tự động hóa server, LAMP stack, cài đặt Apache MySQL PHP, devops automation]
---

# 🚀 Tự động cài đặt LAMP Stack trên server Linux chỉ với một click

Bạn đã từng phải **cài đặt thủ công** Apache, MySQL, PHP, cấu hình firewall, tạo user…?  
Mỗi bước lại đòi hỏi kiến thức dòng lệnh, thời gian chờ đợi và rủi ro sai cấu hình.  
Workflow **Complete LAMP Stack Automated Server Setup** của n8n giải quyết mọi rắc rối này: chỉ cần một lần click, toàn bộ môi trường LAMP sẽ được chuẩn bị, cài đặt và cấu hình hoàn chỉnh trên VPS của bạn – **không cần viết một dòng code nào**.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Cài đặt LAMP trong vòng 5‑10 phút thay vì vài giờ.  
- **Độ chính xác 100%**: Các lệnh được kiểm thử, không còn lỗi “quên cài module”.  
- **Mở rộng nhanh**: Thêm các công cụ dev, tạo user chỉ bằng một node.  
- **Hoạt động liên tục**: Workflow có thể chạy tự động mỗi khi tạo server mới.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Máy chủ Linux** (Ubuntu 20.04/22.04 hoặc Debian) có quyền SSH root.  
- **SSH Private Key** đã được thêm vào n8n (Credentials → SSH Private Key).  
- **Kết nối internet** trên server để tải gói apt.  
- **Port 22 mở** để n8n có thể SSH vào server.  
- (Tùy chọn) **Domain name** nếu muốn cấu hình VirtualHost cho Apache.  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Vào **n8n → Workflows → Import**.  
2. Chọn **Upload JSON** và tải file `complete-lamp-stack.json` (được cung cấp trong mục Release).  
   *Hoặc* copy toàn bộ JSON từ trang nguồn và dán vào **Import from Clipboard**.  
3. Nhấn **Import** → Workflow sẽ xuất hiện trên canvas.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Dưới đây là danh sách các node quan trọng và cách cấu hình chúng:

| Node | Loại | Cấu hình cần chỉnh |
|------|------|--------------------|
| **Start** | `manualTrigger` | Không cần thay đổi, dùng để khởi động workflow. |
| **Set Parameters** | `set` | Đặt các biến: <br>• `host` – địa chỉ IP hoặc hostname của server <br>• `sshUser` – thường là `root` <br>• `sshPort` – mặc định `22` <br>• `domain` – (nếu có) tên miền sẽ dùng cho Apache. |
| **System Preparation** | `ssh` | Credentials: **SSH Private Key** đã tạo. <br>Command: `sudo apt update && sudo apt upgrade -y && sudo apt install -y curl wget gnupg2 software-properties-common`. |
| **Install Apache** | `ssh` | Command: `sudo apt install -y apache2 && sudo systemctl enable apache2 && sudo systemctl start apache2`. |
| **Install MySQL** | `ssh` | Command: `sudo apt install -y mysql-server phpmyadmin && sudo systemctl enable mysql && sudo systemctl start mysql`. <br>*(Nếu muốn đặt mật khẩu root MySQL, thêm lệnh `sudo mysql_secure_installation` và chỉnh `debconf-set-selections`.)* |
| **Install PHP** | `ssh` | Command: `sudo apt install -y php libapache2-mod-php php-mysql php-cli php-curl php-gd php-mbstring php-xml php-zip`. |
| **Install Dev Tools** | `ssh` | Command: `sudo apt install -y git unzip build-essential`. |
| **Create Dev User** | `ssh` | Command: `sudo adduser --disabled-password --gecos "" devuser && sudo usermod -aG sudo devuser`. |
| **Final Configuration** | `ssh` | Command: <br>`sudo a2enmod rewrite && sudo systemctl restart apache2` <br>*(Nếu có domain, thêm VirtualHost config ở đây.)* |
| **Setup Complete** | `set` | Tạo output tóm tắt: `LAMP Stack đã được cài đặt thành công trên {{ $json["host"] }}`. |

> **Lưu ý:**  
> - Đảm bảo **SSH Private Key** có quyền `chmod 600`.  
> - Kiểm tra lại biến `host` trong node **Set Parameters** để tránh SSH tới sai server.  
> - Nếu server dùng `sudo` không yêu cầu password, hãy chắc chắn user SSH có quyền `NOPASSWD` trong `/etc/sudoers`.

#### 3. Kích hoạt ⚡️
1. Nhấn **Execute Workflow** → chọn **Run** trên node **Start**.  
2. Kiểm tra log từng node trong tab **Execution** để xác nhận không có lỗi.  
3. Khi mọi thứ ổn, bật **Active** (Toggle ở góc phải) để workflow có thể được gọi lại bất kỳ lúc nào (hoặc tích hợp với webhook).

### ✍️ Mẹo & gợi ý nâng cao
- **Tự động tạo SSL**: Thêm node SSH chạy `certbot --apache -d {{ $json["domain"] }}` sau `Final Configuration`.  
- **Gửi báo cáo**: Dùng node **Email** hoặc **Slack** để gửi bản tóm tắt cài đặt và log lỗi cho admin.  
- **Backup MySQL**: Thêm node SSH thực hiện `mysqldump` và lưu file vào S3/Google Drive.  
- **Template đa server**: Sử dụng **Loop** (SplitInBatches) để cài đặt đồng thời trên nhiều server.

### 📌 Kết luận
Với workflow **Complete LAMP Stack Automated Server Setup**, các sếp có thể **đưa môi trường phát triển lên production chỉ trong vài phút**, giảm thiểu sai sót và tập trung vào việc phát triển ứng dụng thực tế. Hãy import ngay, cấu hình SSH key và để n8n lo phần còn lại – tự động, nhanh chóng, không lỗi! 🚀