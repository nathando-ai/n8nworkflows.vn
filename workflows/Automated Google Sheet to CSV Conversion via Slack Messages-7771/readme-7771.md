---
title: "🚀 Tự Động Chuyển Đổi Google Sheet Sang CSV & Gửi Slack Chỉ Với 1 Tin Nhắn"
description: "Workflow n8n giúp các sếp biến bất kỳ Google Sheet nào thành file CSV và gửi ngay vào kênh Slack chỉ bằng một lệnh chat, không cần code, tiết kiệm hàng giờ thao tác thủ công."
slug: "tu-dong-chuyen-google-sheet-sang-csv-gui-slack"
tags: [n8n, automation, no-code, google-sheets, slack, data-export]
keywords: [n8n workflow, tự động hóa dữ liệu, google sheet to csv, slack integration, export data]
---

# 🚀 Tự Động Chuyển Đổi Google Sheet Sang CSV & Gửi Slack Chỉ Với 1 Tin Nhắn

Trong môi trường làm việc hiện đại, việc xuất dữ liệu từ Google Sheets sang định dạng CSV để phân tích, nhập vào hệ thống CRM hoặc chia sẻ với đối tác là một thao tác lặp đi lặp lại rất tốn thời gian. Các sếp thường phải mở file, chọn "File > Download > Comma-separated values", lưu về máy, rồi lại đăng nhập Slack để upload file lên. Quy trình thủ công này không chỉ chậm mà còn dễ gây lỗi do sai sót con người (quên lưu, gửi nhầm file cũ...).

Workflow **"Automated Google Sheet to CSV Conversion via Slack Messages"** do Alok Singh phát triển chính là giải pháp "chốt hạ" cho bài toán này. Với n8n, các sếp chỉ cần nhắn một tin nhắn chứa ID của Sheet vào Slack, hệ thống sẽ tự động đọc dữ liệu, chuyển đổi sang CSV và gửi file ngay vào kênh làm việc. Toàn bộ quá trình diễn ra trong vài giây, hoàn toàn không cần viết một dòng code nào.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 100% thời gian thao tác thủ công:** Không cần mở trình duyệt, không cần tải file về máy, không cần upload lại.
- **Chính xác tuyệt đối:** Dữ liệu được đọc trực tiếp từ API Google Sheets, đảm bảo luôn là phiên bản mới nhất, tránh lỗi gửi nhầm file cũ.
- **Tương tác trực quan:** Chỉ cần chat trên Slack (công cụ làm việc chính) là có ngay file CSV, không cần chuyển đổi giữa các ứng dụng.
- **Mở rộng dễ dàng:** Có thể dễ dàng thêm bước gửi email hoặc lưu trữ file sau khi xuất.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản n8n:** Đã cài đặt và chạy (Self-hosted hoặc Cloud).
2. **Tài khoản Slack:** Có quyền quản trị hoặc thành viên trong workspace.
3. **Tài khoản Google:** Có quyền truy cập vào Google Sheets cần xuất.
4. **Credentials trong n8n:**
   - `slackApi`: Cho node Trigger (để nhận tin nhắn).
   - `googleSheetsOAuth2Api`: Cho node đọc dữ liệu (OAuth2).
   - `slackOAuth2Api`: Cho node gửi file (OAuth2).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Mở n8n Editor.
2. Chọn **Import from URL** và dán link: `https://n8n.io/workflows/7771` HOẶC copy toàn bộ JSON của workflow và dán vào màn hình import.
3. Sau khi import, các sếp sẽ thấy 5 nodes chính được kết nối sẵn.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Đây là phần quan trọng nhất. Các sếp cần cấu hình từng node cụ thể sau:

1. **Node: Slack Trigger**
   - Chọn credential `slackApi` đã tạo.
   - Chọn **Event**: `message`.
   - **Channel**: Chọn kênh Slack mà các sếp muốn gửi lệnh (ví dụ: `#data-export`).
   - *Lưu ý:* Đảm bảo Bot của n8n đã được mời vào kênh này.

2. **Node: Extract Sheet ID**
   - Đây là node Function dùng để parse tin nhắn từ Slack.
   - Mặc định, workflow thường kỳ vọng tin nhắn có định dạng cụ thể (ví dụ: `sheet: [ID_SHEET]`).
   - Các sếp có thể mở node này ra để kiểm tra logic JavaScript. Nếu muốn thay đổi cú pháp lệnh (ví dụ: chỉ cần gửi ID thuần túy), hãy sửa code trong tab **JavaScript** của node này.
   - *Mẹo:* Hãy test bằng cách gửi tin nhắn mẫu vào Slack để xem node này có extract đúng ID không.

3. **Node: Read Google Sheet**
   - Chọn credential `googleSheetsOAuth2Api`.
   - **Document**: Chọn "Specify by ID".
   - **ID**: Ở đây, n8n sẽ tự động lấy giá trị từ node `Extract Sheet ID` (thường là `{{ $json.sheetId }}` hoặc tương tự). Các sếp không cần điền cứng ID ở đây.
   - **Sheet Name**: Mặc định là `Sheet1`. Nếu Sheet của các sếp có tên khác (ví dụ: `Data2024`), hãy sửa ô này thành tên Sheet chính xác.

4. **Node: Convert to CSV**
   - Node `spreadsheetFile` với operation `toFile`.
   - Đảm bảo rằng dữ liệu từ node trước được map đúng vào input của node này.
   - Các sếp có thể đặt tên file đầu ra (ví dụ: `data_export_{{ $now }}.csv`) để tránh trùng tên file khi xuất nhiều lần.

5. **Node: Upload to Slack**
   - Chọn credential `slackOAuth2Api`.
   - **Resource**: Chọn `file`.
   - **Channel**: Chọn kênh Slack đích để nhận file (có thể trùng với kênh gửi lệnh hoặc kênh riêng).
   - **File**: Chọn binary data từ node `Convert to CSV` (thường là `data`).
   - **Filename**: Đặt tên file CSV (ví dụ: `report.csv`).
   - **Initial Comment**: Các sếp có thể thêm chú thích ngắn gọn khi gửi file (ví dụ: "File dữ liệu vừa được xuất").

#### 3. Kích hoạt ⚡️
1. **Test Run:**
   - Nhấn nút **Test Workflow**.
   - Mở Slack, vào kênh đã cấu hình, gửi tin nhắn theo cú pháp yêu cầu (ví dụ: `sheet: 1AbC...xyz`).
   - Quan sát n8n: Node Trigger sẽ bắt sự kiện -> Node Function extract ID -> Node Google Sheets đọc dữ liệu -> Node CSV chuyển đổi -> Node Slack upload file.
   - Kiểm tra kênh Slack xem đã nhận được file CSV chưa.
2. **Bật Active:**
   - Sau khi test thành công, nhấn nút **Active** ở góc trên bên phải để workflow chạy liên tục.

### ✍️ Mẹo & gợi ý nâng cao
- **Thêm bước xác nhận:** Các sếp có thể thêm một node `Slack` (send message) trước khi upload file để báo "Đang xử lý..." nhằm tăng trải nghiệm người dùng.
- **Lọc dữ liệu:** Thay vì xuất toàn bộ Sheet, các sếp có thể thêm node `Code` hoặc `Filter` để chỉ xuất những dòng dữ liệu mới nhất hoặc theo điều kiện cụ thể.
- **Gửi Email kèm file:** Thêm node `Gmail` hoặc `SMTP` sau bước Upload to Slack để đồng thời gửi file CSV vào email của các sếp hoặc đồng nghiệp.
- **Định kỳ tự động:** Thay vì chờ lệnh từ Slack, các sếp có thể thêm node `Cron` để tự động xuất và gửi file CSV vào đầu mỗi ngày mà không cần thao tác thủ công.

### 📌 Kết luận
Workflow này là một ví dụ điển hình cho sức mạnh của n8n trong việc kết nối các dịch vụ SaaS phổ biến. Thay vì mất thời gian cho những thao tác lặp đi lặp lại, các sếp có thể tập trung vào việc phân tích dữ liệu và ra quyết định. Hãy import ngay workflow này, cấu hình credentials và trải nghiệm sự khác biệt trong quy trình làm việc hàng ngày. Chúc các sếp thành công!