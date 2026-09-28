---
title: "🔍 **Tự Động Quét CVE cho Chương Trình Bug Bounty với Nuclei & Project Discovery (N8n) - Giúp Các Sếp Tiết Kiệm 1000+ Giây/Ngày**"
description: "Workflow tự động hóa quét lỗ hổng (CVE) trên tất cả các domain từ HackerOne, Bugcrowd, Intigriti và YesWeHack bằng Nuclei và Project Discovery. Giúp các sếp phát hiện lỗ hổng mới chỉ trong vài giây thay vì thủ công mất hàng giờ."
slug: "tieu-dong-quet-cve-bug-bounty-nuclei-project-discovery"
tags: [n8n, automation, security, bug-bounty, offensive-cybersecurity, nuclei, project-discovery]
keywords: [n8n workflow security, tự động hóa quét CVE, Nuclei với n8n, Project Discovery API, bug bounty automation, quét lỗ hổng tự động]
---

# 🚀 **Tự Động Quét Lỗ Hổng (CVE) cho Chương Trình Bug Bounty - Giúp Các Sếp Phát Triển An Toàn Mạng 24/7**

Hiện nay, việc phát hiện lỗ hổng (CVE) trên các domain liên quan đến chương trình bug bounty như HackerOne, Bugcrowd, Intigriti hoặc YesWeHack vẫn là một công việc **mệt mỏi và tốn thời gian** đối với các sếp và đội ngũ SecOps. Thường thì các sếp phải:
- **Tải danh sách domain** từ nhiều nguồn khác nhau.
- **Tải xuống template mới** từ Project Discovery.
- **Cấu hình Nuclei** để quét từng domain một.
- **Xử lý kết quả** và gửi báo cáo qua email.

**Workflow này tự động hóa toàn bộ quy trình đó chỉ trong vài giây mỗi ngày!** Sử dụng **Nuclei** (công cụ quét lỗ hổng mạnh mẽ của Project Discovery) và **n8n**, các sếp có thể:
✅ **Quét tất cả domain** từ các chương trình bug bounty hàng ngày.
✅ **Áp dụng template mới nhất** từ Project Discovery.
✅ **Lọc và xử lý kết quả** tự động.
✅ **Gửi báo cáo qua email** một cách cá nhân hóa.

---
## 🎯 **Kết Quả Các Sếp Nhận Được**

:::tip[**LỢI ÍCH CỐT LÕI**]
- **Tiết kiệm thời gian**: Không còn phải quét thủ công hàng ngày (giảm từ 2-3 giờ xuống chỉ vài phút).
- **Phát hiện lỗ hổng nhanh chóng**: Áp dụng template mới nhất từ Project Discovery ngay lập tức.
- **Tự động hóa hoàn toàn**: Không cần can thiệp thủ công, workflow chạy 24/7.
- **Báo cáo tự động**: Kết quả được gửi qua email định kỳ, giúp đội ngũ SecOps theo dõi dễ dàng.
- **Cải thiện an toàn mạng**: Phát hiện lỗ hổng sớm trước khi hacker lợi dụng.
:::

---
## 🔧 **Yêu Cầu Cần Thiết**

:::info[**CHUẨN BỊ**]
Để workflow này hoạt động, các sếp cần chuẩn bị:
1. **Môi trường SSH**:
   - **VPS Linux** (gợi ý: [Hostinger](https://www.hostinger.com/vps-hosting), [DigitalOcean](https://www.digitalocean.com/pricing)) hoặc **máy chủ local** với OpenSSH.
   - **Nuclei** được cài đặt trên VPS (hướng dẫn: [Project Discovery Docs](https://docs.projectdiscovery.io/opensource/nuclei/install)).
   - **Tài khoản SSH** (có thể sử dụng **password** hoặc **private key**).

2. **Tài khoản Gmail** (để gửi báo cáo):
   - **API Key Gmail OAuth2** (cài đặt qua [Google Cloud Console](https://console.cloud.google.com/)).
   - **Enable Gmail API** và cấu hình OAuth Client ID.

3. **API Key OpenAI** (nếu muốn sử dụng tính năng tóm tắt kết quả):
   - Trích xuất từ [OpenAI API Keys](https://platform.openai.com/api-keys).
   - **Nạp tiền vào tài khoản** để sử dụng API.

---
## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
Các sếp có thể:
- **Tải file JSON** từ [n8n.io/workflows/10054](https://n8n.io/workflows/10054) và import vào **n8n Editor**.
- **Copy/Paste JSON** từ file vào **Import Workflow** trong n8n.

### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**

#### **A. Cấu Hình SSH (Trung Tâm Của Workflow)**
Workflow này **không thể chạy** nếu không có SSH được cấu hình đúng. Các bước chi tiết:

1. **Tạo tài khoản SSH**:
   - **VPS**: Sử dụng **root** hoặc tài khoản mới với quyền `sudo`.
   - **Local**: Cài đặt OpenSSH và cho phép **root login** (hướng dẫn: [Enable Root Login](https://linuxconfig.org/allow-ssh-root-login-on-ubuntu-20-04-focal-fossa-linux)).

2. **Cài đặt Nuclei**:
   ```bash
   curl -s https://raw.githubusercontent.com/projectdiscovery/nuclei/v3/install.sh | sh
   ```
   - Đảm bảo Nuclei được cài đặt ở `/tmp/nuclei` (đường dẫn mặc định trong workflow).

3. **Thêm SSH Credentials trong n8n**:
   - Trong **n8n Editor**, đi đến **Credentials → Add Credential → SSH Password** (hoặc **SSH Private Key** nếu sử dụng key).
   - Điền:
     - **Host**: IP/VPS của bạn.
     - **Port**: 22 (mặc định).
     - **Username**: `root` hoặc tên tài khoản SSH.
     - **Password/Private Key**: Theo cấu hình trên VPS.

#### **B. Cấu Hình Gmail (Gửi Báo Cáo)**
1. **Enable Gmail API**:
   - Trên [Google Cloud Console](https://console.cloud.google.com/), tạo **OAuth Client ID** với **Web Application**.
   - Thêm **Redirect URI** trong n8n (thường là `http://localhost` hoặc URI từ n8n).

2. **Thêm Credentials Gmail trong n8n**:
   - Đi đến **Credentials → Add Credential → Gmail OAuth2**.
   - Chọn **Client ID** và **Client Secret** từ Google Cloud Console.
   - **Refresh Token** sẽ tự động xuất hiện khi đăng nhập qua n8n.

#### **C. Cấu Hình OpenAI (Tóm Tắt Kết Quả - Tùy Chọn)**
Nếu muốn sử dụng tính năng **tóm tắt kết quả** bằng AI:
1. Trích xuất **API Key** từ [OpenAI](https://platform.openai.com/api-keys).
2. Thêm vào **Credentials → Add Credential → OpenAI** trong n8n.

#### **D. Các Node Quan Trọng Cần Chỉnh**
| **Node** | **Lưu Ý** |
|----------|-----------|
| **Schedule Trigger** | Đặt lịch chạy hàng ngày (ví dụ: `0 0 * * *` - chạy lúc 00:00 hàng ngày). |
| **Get All Bug Bounty Domains** | Đảm bảo **URL API** trả về danh sách domain chính xác (ví dụ: từ HackerOne, Bugcrowd). |
| **Loop Over CVEs** | Node này **split** danh sách CVE thành batch để quét. |
| **Execute Nuclei** | Đảm bảo **command** trong SSH là chính xác (ví dụ: `nuclei -l /tmp/nuclei/templates/template.yaml -o /tmp/nuclei/results.json`). |
| **Send a message (Gmail)** | Kiểm tra **template email** để đảm bảo nội dung rõ ràng. |

### **3. Kích Hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Chạy **Manual Trigger** để kiểm tra workflow có hoạt động không.
   - Kiểm tra **log SSH** trên VPS để đảm bảo Nuclei chạy đúng.
2. **Bật Active**:
   - Sau khi test thành công, **bật Schedule Trigger** để workflow chạy tự động hàng ngày.

---
## ✍️ **Mẹo & Gợi Ý Nâng Cao**

:::info[**MỘT SỐ Ý TƯỞNG MỞ RỘNG**]
1. **Gửi báo cáo qua Slack/Telegram**:
   - Thay thế node **Gmail** bằng **Slack Webhook** hoặc **Telegram Bot** để nhận thông báo tức thời.

2. **Lưu log quét vào Google Sheets**:
   - Sử dụng node **Google Sheets** để ghi lại tất cả kết quả quét vào một bảng dữ liệu.

3. **Kết hợp với GitHub Actions**:
   - Nếu các sếp muốn **push template mới** từ GitHub vào Nuclei tự động, có thể thêm node **GitHub API** vào workflow.

4. **Lọc kết quả nghiêm trọng**:
   - Sử dụng node **Filter** để chỉ giữ lại CVE có **severity = Critical/High**.

5. **Báo cáo định kỳ cho CEO**:
   - Tạo một **dashboard** từ Google Sheets hoặc Looker Studio để CEO theo dõi tình trạng an toàn.
:::

---
## 📌 **Kết Luận**

Workflow này **giúp các sếp tự động hóa quy trình quét lỗ hổng bug bounty một cách hoàn toàn**, tiết kiệm thời gian và cải thiện hiệu quả SecOps. **Không cần code**, chỉ cần cấu hình SSH và API, các sếp có thể **phát hiện lỗ hổng mới chỉ trong vài giây** thay vì mất hàng giờ thủ công.

**👉 Hãy áp dụng ngay workflow này và bảo vệ mạng của công ty 24/7!**

---
:::info[**GỢI Ý HẠN CHẾ**]
Để workflow chạy ổn định, các sếp nên:
- **Chọn VPS có tài nguyên đủ** (tối thiểu 2GB RAM, 2 CPU core).
- **Backup dữ liệu** trên VPS định kỳ.
- **Cập nhật Nuclei** thường xuyên để tránh lỗi.
:::

---
**🔗 [Xem workflow gốc](https://n8n.io/workflows/10054) | 📧 [Liên hệ Javier Rieiro](mailto:pyus3r@gmail.com) để hỗ trợ tùy chỉnh.**