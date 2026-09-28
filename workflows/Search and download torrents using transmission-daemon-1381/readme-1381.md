---
title: "🚀 Tự Động Tìm & Tải Torrent Qua Telegram Với n8n"
description: "Workflow n8n giúp tìm kiếm torrent trên Transmission Daemon và tự động tải về máy chủ chỉ với một tin nhắn Telegram. Giải pháp hoàn toàn không cần code."
slug: "tu-dong-tim-tai-torrent-telegram-n8n"
tags: [n8n, automation, no-code, transmission, telegram, torrent]
keywords: [n8n workflow, tự động hóa torrent, transmission daemon, telegram bot, n8n tutorial]
---

# 🚀 Tự Động Tìm & Tải Torrent Qua Telegram Với n8n

Các sếp có hay gặp tình trạng muốn tải một file lớn (phim, phần mềm, dataset) nhưng lại lười vào trình quản lý torrent, hoặc muốn tải file ngay trên điện thoại mà không cần mở trình duyệt? Việc tìm kiếm torrent thủ công, copy link, rồi vào giao diện web của Transmission để dán link là một quy trình khá rườm rà và dễ gây lỗi do sai sót khi copy.

Workflow này giải quyết triệt để vấn đề đó. Chỉ cần gửi một tin nhắn chứa từ khóa tìm kiếm vào Telegram Bot, n8n sẽ tự động tìm kiếm torrent phù hợp, xác nhận với các sếp, và bắt đầu quá trình tải về máy chủ chạy Transmission Daemon. Mọi thứ diễn ra mượt mà, nhanh chóng và hoàn toàn tự động.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 và đảm bảo băng thông tải torrent không bị gián đoạn, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian tối đa**: Biến quy trình 5 bước thủcông xuống còn 1 tin nhắn Telegram.
- **Chính xác cao**: Loại bỏ lỗi copy/paste link torrent, n8n xử lý trực tiếp từ API.
- **Cá nhân hóa trải nghiệm**: Nhận thông báo trạng thái (tìm thấy/không tìm thấy) ngay trên điện thoại.
- **Hoạt động liên tục**: Tải file trong nền 24/7 ngay cả khi các sếp đang ngủ hoặc đi công tác.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Máy chủ (VPS)**: Chạy n8n và Transmission Daemon.
2. **Transmission Daemon**: Đã được cài đặt và cấu hình sẵn trên VPS. Cần biết:
   - IP/Domain của VPS.
   - Cổng RPC của Transmission (thường là 9091).
   - Username và Password của Transmission.
   - RPC Token (có thể lấy từ trình duyệt khi vào giao diện web của Transmission).
3. **Telegram Bot**:
   - Tạo bot qua @BotFather.
   - Lấy **Bot Token**.
   - Lấy **Chat ID** của các sếp (có thể dùng @userinfobot).
4. **n8n Instance**: Đã được cài đặt và chạy.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Mở n8n Editor.
2. Chọn **Import from URL** hoặc **Import from File**.
3. Dán link workflow gốc: `https://n8n.io/workflows/1381` hoặc tải file JSON về và import.
4. Sau khi import, các sếp sẽ thấy 8 nodes chính được kết nối sẵn.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

Đây là phần quan trọng nhất. Các sếp cần vào từng node để cấu hình thông tin của mình:

**A. Node `Webhook`**
- Mặc định workflow dùng Webhook để nhận dữ liệu. Tuy nhiên, trong cấu hình này, nó có thể được dùng để trigger từ Telegram hoặc một nguồn khác.
- **Lưu ý**: Nếu các sếp muốn trigger trực tiếp từ Telegram, hãy đảm bảo node Telegram (nếu có) hoặc cấu hình Webhook phù hợp với cách các sếp gửi lệnh. Trong workflow gốc, node `Webhook` có path `6be952e8-e30f-4dd7-90b3-bc202ae9f174`. Các sếp có thể giữ nguyên hoặc đổi path cho dễ nhớ.

**B. Node `SearchTorrent` (Function Item)**
- Node này chứa logic JavaScript để tìm kiếm torrent.
- **Kiểm tra**: Mở node này lên, đảm bảo URL tìm kiếm torrent (ví dụ: từ The Pirate Bay, RARBG, hoặc API torrent khác) còn hoạt động.
- **Tham số**: Các sếp có thể chỉnh sửa prompt hoặc từ khóa tìm kiếm mặc định nếu muốn.

**C. Node `Start download` (HTTP Request)**
- Đây là node chính để gửi lệnh tải torrent lên Transmission.
- **Method**: POST.
- **URL**: `http://[IP_VPS]:9091/transmission/rpc` (Thay `[IP_VPS]` bằng IP thực tế của các sếp).
- **Authentication**: Chọn **Basic Auth**.
  - Tạo một credential mới trong n8n:
    - **Username**: Username của Transmission.
    - **Password**: Password của Transmission.
- **Body**: Đảm bảo body JSON chứa `method: "add-torrent"` và `arguments: { "filename": "..." }` hoặc `url` tùy thuộc vào logic của node `SearchTorrent`.

**D. Node `IF` và `IF2`**
- Các node này dùng để kiểm tra kết quả tìm kiếm và trạng thái tải.
- **Kiểm tra điều kiện**: Đảm bảo điều kiện so sánh đúng với cấu trúc dữ liệu trả về từ API torrent và Transmission.

**E. Node `Torrent not found` (Telegram)**
- Gửi thông báo khi không tìm thấy torrent.
- **Credentials**: Chọn credential Telegram API đã tạo.
- **Chat ID**: Điền Chat ID của các sếp.
- **Message**: Chỉnh sửa nội dung thông báo cho phù hợp (ví dụ: "😢 Không tìm thấy torrent cho từ khóa: {{ $json.query }}").

**F. Node `Telegram1` (Telegram)**
- Gửi thông báo khi bắt đầu tải hoặc tải thành công.
- **Credentials**: Chọn credential Telegram API.
- **Chat ID**: Điền Chat ID của các sếp.
- **Message**: Chỉnh sửa nội dung (ví dụ: "✅ Đã bắt đầu tải: {{ $json.name }}").

**G. Node `Start download new token` (HTTP Request)**
- Node này có thể dùng để làm mới token RPC của Transmission nếu token hết hạn.
- **Authentication**: Basic Auth (giống node `Start download`).
- **URL**: `http://[IP_VPS]:9091/transmission/rpc`.
- **Body**: Gửi request để lấy token mới.

#### 3. Kích hoạt ⚡️
1. **Test Run**:
   - Gửi một tin nhắn mẫu từ Telegram (hoặc trigger Webhook) với từ khóa torrent phổ biến.
   - Quan sát các node chạy lần lượt: `SearchTorrent` -> `IF` -> `Start download` -> `Telegram1`.
   - Kiểm tra xem file có xuất hiện trong giao diện web của Transmission không.
2. **Bật Active**:
   - Sau khi test thành công, bật công tắc **Active** ở góc trên bên phải n8n.
   - Workflow sẽ sẵn sàng nhận lệnh 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Thêm xác nhận trước khi tải**: Chèn một node Telegram hỏi "Tải file này không?" và chờ phản hồi "Yes/No" trước khi gọi node `Start download`. Điều này giúp tránh tải nhầm file.
- **Gửi link tải trực tiếp**: Sau khi tải xong, các sếp có thể thêm node để gửi link HTTP của file (nếu Transmission cấu hình chia sẻ qua HTTP) hoặc thông báo hoàn thành.
- **Log lịch sử tải**: Thêm node `Google Sheets` hoặc `Airtable` để lưu lại lịch sử các torrent đã tải, giúp các sếp dễ dàng tra cứu lại.
- **Hỗ trợ nhiều torrent**: Chỉnh sửa node `SearchTorrent` để trả về top 5 kết quả, và gửi danh sách này lên Telegram để các sếp chọn số thứ tự muốn tải.

### 📌 Kết luận
Workflow này là một công cụ cực kỳ hữu ích cho các sếp hay làm việc với file lớn, đặc biệt là trong môi trường phát triển, nghiên cứu hoặc giải trí. Với sự kết hợp giữa n8n, Transmission và Telegram, các sếp có thể biến máy chủ thành một "trợ lý tải file" thông minh, luôn sẵn sàng phục vụ chỉ với một tin nhắn. Hãy thử ngay và trải nghiệm sự tiện lợi mà nó mang lại!