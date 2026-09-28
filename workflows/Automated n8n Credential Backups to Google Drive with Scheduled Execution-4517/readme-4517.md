---
title: "🛡️ Tự Động Sao Lưu Credential n8n Lên Google Drive Hàng Ngày"
description: "Workflow n8n giúp tự động xuất toàn bộ thông tin xác thực (credentials) của bạn ra file JSON và lưu trữ an toàn trên Google Drive theo lịch trình định kỳ, ngăn chặn mất dữ liệu quan trọng."
slug: "tu-dong-sao-luu-credential-n8n-google-drive"
tags: [n8n, automation, devops, google-drive, backup, security]
keywords: [n8n backup credentials, tự động hóa sao lưu, n8n devops, google drive automation, backup n8n]
---

# 🛡️ Tự Động Sao Lưu Credential n8n Lên Google Drive Hàng Ngày

Trong quá trình vận hành các workflow phức tạp bằng n8n, **Credentials** (thông tin xác thực) là "xương sống" kết nối n8n với các dịch vụ bên ngoài như Gmail, Slack, OpenAI, Database... Tuy nhiên, nhiều sếp thường chỉ sao lưu toàn bộ instance n8n (dùng Docker volume hoặc database dump) mà quên mất một rủi ro cực lớn: **Mất kết nối hoặc cần di chuyển n8n sang server mới.**

Khi đó, việc phải nhập lại hàng chục, thậm chí hàng trăm credentials thủ công là một cơn ác mộng. Workflow này giải quyết bài toán đó bằng cách **tự động trích xuất toàn bộ credentials**, định dạng lại thành file JSON sạch sẽ và **tự động upload lên Google Drive** theo lịch trình (ví dụ: mỗi ngày 1 lần). Đây là lớp bảo vệ thứ hai (2FA cho dữ liệu cấu hình) giúp các sếp yên tâm tuyệt đối.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 và đảm bảo tính bảo mật khi thực thi lệnh (Execute Command), các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Sao lưu tự động 100%:** Không cần nhớ thủ công, hệ thống tự chạy theo lịch (Daily/Weekly).
- **Dữ liệu sạch sẽ:** File JSON được định dạng chuẩn, dễ đọc và dễ import lại.
- **An toàn & Tách biệt:** Dữ liệu credentials được lưu trên Google Drive (điện toán đám mây), tách biệt khỏi server n8n, tránh mất dữ liệu khi server gặp sự cố.
- **Tiết kiệm thời gian khôi phục:** Khi cần setup lại n8n mới, chỉ cần tải file JSON về và import, hoàn tất trong vài phút.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n:** Đã cài đặt và chạy ổn định.
- **Tài khoản Google:** Để tạo Credentials cho Google Drive.
- **Quyền truy cập Terminal/SSH:** Workflow sử dụng node `Execute Command` để đọc dữ liệu credentials từ hệ thống file của n8n. Các sếp cần đảm bảo user chạy n8n có quyền đọc thư mục chứa credentials (thường là `/home/node/.n8n` hoặc thư mục volume mount).
- **Google Drive OAuth2:** Đã tạo và cấu hình xong trong n8n.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Mở n8n Editor.
2. Nhấn nút **"Import from File"** hoặc **"Import from URL"**.
3. Chọn file JSON của workflow hoặc dán link gốc: [https://n8n.io/workflows/4517](https://n8n.io/workflows/4517).
4. Workflow sẽ hiện ra với các node đã được kết nối sẵn.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

Đây là phần quan trọng nhất. Workflow này sử dụng cơ chế **Execute Command** để truy cập trực tiếp vào file hệ thống của n8n, do đó cần cấu hình chính xác đường dẫn.

**Node 1: `Execute Command Get All Cridentials`**
- **Mục đích:** Chạy lệnh shell để đọc file credentials.
- **Cấu hình:**
  - Trong trường **Command**, các sếp cần điền lệnh `cat` (hoặc `ls` nếu muốn list) trỏ đến file credentials của n8n.
  - **Đường dẫn mặc định (Docker/Linux):** Thường là `/home/node/.n8n/credentials.json` hoặc `/home/node/.n8n/credentials.sqlite` (tùy phiên bản n8n, phiên bản mới dùng SQLite).
  - *Lưu ý:* Nếu các sếp dùng Docker, hãy kiểm tra volume mount. Nếu n8n chạy trên local, đường dẫn có thể là `~/.n8n/credentials.json`.
  - *Mẹo:* Chạy thử node này trước để xem output có chứa dữ liệu JSON credentials không.

**Node 2: `JSON Formatting Data`**
- **Mục đích:** Làm sạch dữ liệu thô từ lệnh shell.
- **Cấu hình:**
  - Node Code này sẽ parse string từ node trước thành object JSON.
  - Các sếp có thể kiểm tra lại code trong node này nếu cấu trúc file credentials của n8n phiên bản mới có thay đổi (ví dụ: thêm trường `id`, `name`, `type`, `data`).
  - Đảm bảo output là một mảng (array) hoặc object chứa danh sách credentials.

**Node 3: `Aggregate Cridentials`**
- **Mục đích:** Gom tất cả các items (credentials) thành 1 item duy nhất để tạo file.
- **Cấu hình:**
  - Chọn **Operation**: `Aggregate`.
  - Chọn **Mode**: `All Items` (để gom toàn bộ danh sách).
  - Đặt tên output key (ví dụ: `credentialsList`) để node sau nhận diện.

**Node 4: `Convert To File`**
- **Mục đích:** Chuyển dữ liệu JSON thành file binary.
- **Cấu hình:**
  - **Operation**: `To JSON`.
  - **File Name**: Đặt tên file có chứa ngày tháng để dễ quản lý, ví dụ: `n8n-credentials-backup-{{ $now.format('YYYY-MM-DD') }}.json`.
  - **Data**: Chọn key chứa dữ liệu credentials từ node Aggregate (ví dụ: `credentialsList`).

**Node 5: `Google Drive Upload File`**
- **Mục đích:** Upload file lên Google Drive.
- **Cấu hình:**
  - **Credentials**: Chọn credentials Google Drive OAuth2 đã tạo.
  - **Resource**: `File`.
  - **Operation**: `Upload`.
  - **Folder**: Chọn thư mục đích trên Google Drive (ví dụ: `Backups/n8n`).
  - **File Name**: Tham chiếu tên file từ node `Convert To File`.
  - **File Content**: Chọn binary data từ node `Convert To File`.

**Node 6: `Schedule Trigger`**
- **Mục đích:** Kích hoạt workflow tự động.
- **Cấu hình:**
  - Chọn **Interval**: `Day` (Hàng ngày) hoặc `Week` (Hàng tuần).
  - Chọn **Time**: Giờ chạy (ví dụ: 02:00 sáng để tránh giờ cao điểm).
  - *Lưu ý:* Bật **Active** cho node này sau khi test thành công.

#### 3. Kích hoạt ⚡️
1. Nhấn nút **Execute Workflow** (hoặc click vào node `On Click Trigger` nếu muốn test thủ công).
2. Kiểm tra output của node `Google Drive Upload File`. Nếu thấy link file trên Google Drive, nghĩa là thành công.
3. Kiểm tra trên Google Drive xem file JSON có tồn tại và nội dung có đúng không.
4. Bật **Active** cho workflow để nó tự chạy theo lịch.

### ✍️ Mẹo & gợi ý nâng cao

- **🔒 Mã hóa File Backup:**
  File JSON chứa thông tin nhạy cảm (API Keys, Passwords). Các sếp nên thêm một node `Code` hoặc `Execute Command` để **encrypt** file trước khi upload lên Google Drive. Hoặc, hãy đảm bảo thư mục Google Drive đó **không chia sẻ công khai** (Private).

- **📧 Thông báo qua Email/Slack:**
  Thêm node `Send Email` hoặc `Slack` sau node `Google Drive Upload File` để gửi thông báo: "✅ Backup credentials thành công lúc [Thời gian]". Nếu lỗi, gửi thông báo đỏ để sếp biết ngay.

- **🗑️ Xóa File Cũ (Retention Policy):**
  Nếu chạy hàng ngày, sau 1 năm sẽ có 365 file. Các sếp có thể thêm logic để xóa các file backup cũ hơn 30 ngày trên Google Drive để tiết kiệm dung lượng và giữ gọn gàng.

- **🔄 Kết hợp với Database Backup:**
  Workflow này chỉ backup credentials. Các sếp nên kết hợp thêm workflow backup **Database n8n** (nếu dùng Postgres/SQLite) để có bộ sao lưu hoàn chỉnh (Credentials + Workflow Data + History).

### 📌 Kết luận

Việc sao lưu credentials n8n là bước bảo mật cơ bản nhưng cực kỳ quan trọng mà nhiều người hay bỏ qua. Với workflow này, các sếp có thể yên tâm ngủ ngon vì dữ liệu cấu hình quan trọng luôn được sao lưu tự động lên đám mây mỗi ngày. Hãy import, chỉnh sửa đường dẫn file credentials cho đúng môi trường của mình và bật Active ngay hôm nay!