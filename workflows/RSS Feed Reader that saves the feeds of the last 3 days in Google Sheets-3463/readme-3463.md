---
title: "📰 **Tự Động Hóa Đọc RSS Feed & Lưu Lịch Sử 3 Ngày Trên Google Sheets (N8n)**"
description: "Workflow tự động hóa đọc RSS feed từ các nguồn tin tức, blog, hoặc website, sau đó lưu trữ nội dung mới nhất trong 3 ngày vào Google Sheets. Giúp các sếp tiết kiệm thời gian theo dõi tin tức liên tục mà không cần check thủ công."
slug: "tieu-dong-hoa-doc-rss-feed-luu-3-ngay-tren-google-sheets"
tags: [n8n, automation, RSS feed, Google Sheets, no-code, IT Ops]
keywords: [n8n workflow RSS, tự động hóa đọc tin tức, lưu RSS feed Google Sheets, tự động hóa IT, n8n self-hosted]
---

# 🚀 **Tự Động Hóa Đọc RSS Feed & Lưu Lịch Sử 3 Ngày Trên Google Sheets**

Hiện nay, việc theo dõi tin tức, blog, hoặc các nguồn RSS feed thủ công không chỉ tốn thời gian mà còn dễ bỏ lỡ thông tin quan trọng. **Workflow này giúp các sếp tự động hóa quá trình này**, đọc tất cả các bài viết mới từ các nguồn RSS được cấu hình, sau đó **lưu trữ chúng vào Google Sheets** với lịch sử duy trì **3 ngày mới nhất**, đồng thời **xóa tự động các bài viết cũ hơn** để tránh trùng lặp và tiết kiệm tài nguyên.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted) để đảm bảo tính liên tục và an toàn dữ liệu.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần check RSS feed thủ công hàng ngày.
- **Dữ liệu sạch**: Xóa tự động các bài viết cũ hơn 3 ngày, tránh trùng lặp.
- **Tính liên tục**: Workflow chạy tự động hàng ngày (24/7) trên VPS.
- **Dễ dàng theo dõi**: Tất cả tin tức mới nhất được lưu vào Google Sheets, có thể phân tích hoặc chia sẻ dễ dàng.
- **Tránh bị chặn API**: Thời gian chờ giữa các request đến Google Sheets để tránh bị chặn do quá nhiều yêu cầu.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Google** với quyền truy cập vào **Google Sheets** (để lưu trữ RSS feed).
2. **API Key của Google Sheets OAuth2** (cấu hình trong n8n):
   - Tạo **Google Cloud Project** và kích hoạt **Google Sheets API**.
   - Tạo **OAuth 2.0 Client ID** và cấp quyền cho **Google Sheets**.
   - Thêm **credentials** trong n8n với tên `googleSheetsOAuth2Api`.
3. **Danh sách các liên kết RSS** (cần lưu trong một **Google Sheet** riêng biệt để workflow đọc):
   - Tạo một **Google Sheet** mới với **cột "RSS Links"** (ví dụ: `https://example.com/rss`, `https://blog.com/feed`).
   - Lưu sheet này vào một **folder chia sẻ** để workflow có thể đọc.

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/3463) hoặc copy toàn bộ mã JSON từ trang này.
- Mở **n8n Editor** → Nhấn **Import** → Dán hoặc tải file JSON.
- Workflow sẽ tự động hiển thị trên canvas với **16 node** đã sắp xếp.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này hoạt động theo **4 bước chính**:
1. **Đọc danh sách RSS từ Google Sheets** (node `Read Links`).
2. **Đọc từng bài viết mới từ RSS feed** (node `RSS`).
3. **Lưu bài viết mới vào Google Sheets** (node `Save News`).
4. **Xóa bài viết cũ hơn 3 ngày** (node `Delete News`).

##### **Cấu hình chi tiết các node quan trọng:**
| **Node**               | **Lưu ý cấu hình**                                                                 | **Tham số cần điền**                          |
|------------------------|------------------------------------------------------------------------------------|-----------------------------------------------|
| **Schedule Trigger**   | Cài đặt **lịch trình chạy hàng ngày** (ví dụ: 8h sáng).                          | `cron`: `0 8 * * *` (8h00 hàng ngày)         |
| **RSS**                | Thiết lập **URL RSS** từ sheet `RSS-Links`.                                       | `url`: `$json["RSS Links"]` (đọc từ sheet)   |
| **Google Sheets (Read Links)** | Đọc sheet chứa **danh sách RSS links**.                                      | `Sheet Name`: `RSS-Links`                     |
| **Google Sheets (Save News)** | Lưu bài viết mới vào sheet `RSS-Feeds`.                                      | `Sheet Name`: `RSS-Feeds`                     |
| **Google Sheets (Delete News)** | Xóa bài viết cũ hơn 3 ngày.                                                   | `Sheet Name`: `RSS-Feeds`                     |
| **Code (Filter & Format)** | Các node `Code` được sử dụng để **lọc và định dạng dữ liệu** trước khi lưu. | Cần kiểm tra logic trong code (nếu cần sửa). |

##### **Cách cấu hình Google Sheets OAuth2:**
1. Trong **n8n Credentials**, thêm một **Google Sheets OAuth2** với tên `googleSheetsOAuth2Api`.
2. Chọn **Google Sheets API** và cấp quyền cho:
   - `https://www.googleapis.com/auth/spreadsheets`
   - `https://www.googleapis.com/auth/drive`
3. Sau khi cấu hình xong, **lưu credentials** và áp dụng cho các node `Google Sheets`.

##### **Lưu ý về thời gian chờ (Wait):**
- Workflow sử dụng **node `Wait`** giữa các request đến Google Sheets để **tránh bị chặn API**.
- Thời gian chờ mặc định là **1 giây**, nhưng có thể điều chỉnh nếu gặp lỗi.

---

#### **3. Kích hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Chọn **Schedule Trigger** → Nhấn **Run Workflow**.
   - Kiểm tra **Google Sheets** xem có dữ liệu mới được lưu không.
2. **Bật Active**:
   - Sau khi test thành công, **bật chế độ Active** để workflow chạy tự động hàng ngày.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Kết hợp với Slack/Telegram**:
   - Thêm node **Slack/Telegram Bot** sau `Save News` để **gửi thông báo tin tức mới** vào kênh chat.
2. **Lưu log hoạt động**:
   - Sử dụng node **Markdown** hoặc **Google Drive** để lưu **log hoạt động** của workflow (ngày chạy, số bài viết mới).
3. **Tự động gửi báo cáo định kỳ**:
   - Sử dụng **node `Schedule Trigger`** khác để **tính toán thống kê** (ví dụ: số bài viết mới trong tuần) và gửi qua email.
4. **Cập nhật nhiều nguồn RSS**:
   - Nếu muốn thêm nhiều nguồn RSS, chỉ cần **thêm vào sheet `RSS-Links`** và workflow sẽ tự động đọc tất cả.

---

### 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn **tự động hóa việc theo dõi tin tức, blog, hoặc RSS feed** mà không cần code. Với **cấu hình đơn giản** và **chạy tự động hàng ngày**, nó giúp tiết kiệm thời gian và đảm bảo không bỏ lỡ bất kỳ tin tức quan trọng nào.

**Hãy import ngay và bắt đầu tự động hóa công việc của mình!** 🚀
Nếu gặp vấn đề, các sếp có thể **comment bên dưới** hoặc liên hệ với cộng đồng n8n để hỗ trợ.