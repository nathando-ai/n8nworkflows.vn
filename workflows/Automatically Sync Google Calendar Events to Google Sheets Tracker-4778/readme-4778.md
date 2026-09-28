---
title: "📅 Đồng bộ Google Calendar sang Google Sheets Tự động 100% với n8n"
description: "Giải pháp tự động hóa theo dõi lịch hẹn, sự kiện và công việc bằng cách sync dữ liệu từ Google Calendar vào Google Sheets theo thời gian thực, không cần code."
slug: "dong-bo-google-calendar-sang-google-sheets"
tags: [n8n, automation, google-calendar, google-sheets, no-code, it-ops]
keywords: [n8n workflow, tự động hóa lịch, sync google calendar, google sheets tracker, quản lý công việc]
---

# 📅 Đồng bộ Google Calendar sang Google Sheets Tự động 100% với n8n

Quản lý lịch trình, các cuộc họp và deadline bằng Google Calendar là điều quen thuộc. Tuy nhiên, khi cần tổng hợp dữ liệu để báo cáo, phân tích xu hướng hoặc theo dõi tiến độ dự án, việc sao chép thủ công từng sự kiện vào Google Sheets là một cơn ác mộng. Nó tốn thời gian, dễ sai sót và không thể phản ánh trạng thái cập nhật mới nhất của lịch.

Workflow **"Automatically Sync Google Calendar Events to Google Sheets Tracker"** do *Shi Varong* phát triển chính là giải pháp hoàn hảo. Nó hoạt động như một "cầu nối" thông minh, tự động quét lịch của bạn và cập nhật dữ liệu vào bảng tính Google Sheets một cách chính xác, liên tục và hoàn toàn không cần viết một dòng code nào.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian tuyệt đối:** Loại bỏ hoàn toàn thao tác nhập liệu thủ công, tự động cập nhật mỗi khi có sự kiện mới hoặc thay đổi.
- **Dữ liệu chính xác & nhất quán:** Logic so khớp (Match) đảm bảo không tạo trùng lặp, chỉ cập nhật khi có thay đổi thực sự.
- **Bảng theo dõi (Tracker) sống động:** Biến lịch cá nhân/nhóm thành một bảng dữ liệu có cấu trúc, dễ dàng dùng cho Pivot Table, báo cáo hay phân tích.
- **Hoạt động liên tục:** Chạy nền theo lịch trình (Schedule Trigger), đảm bảo dữ liệu luôn mới nhất.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n:** Đã đăng nhập và có quyền tạo workflow.
- **Google Calendar:** Tài khoản Google có lịch cần đồng bộ.
- **Google Sheets:** Một file Google Sheets đã được tạo sẵn với các cột phù hợp (ví dụ: Tên sự kiện, Thời gian bắt đầu, Thời gian kết thúc, Địa điểm, Ghi chú, ID sự kiện...).
- **Credentials n8n:**
  - Google Calendar OAuth2 API.
  - Google Sheets OAuth2 API.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập trang [n8n.io/workflows/4778](https://n8n.io/workflows/4778).
2. Click nút **"Copy to clipboard"** hoặc tải file JSON về.
3. Mở n8n Editor, click **"Import from File"** hoặc **"Import from URL"** và dán link/file JSON.
4. Workflow sẽ hiện ra với 9 nodes chính.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Đây là phần quan trọng nhất. Các sếp cần cấu hình kỹ các node sau:

**1. Node `Schedule Trigger1`**
- Chọn tần suất chạy. Ví dụ: *"Every 5 minutes"* hoặc *"Every 1 hour"*. Tần suất càng cao, dữ liệu càng mới, nhưng tiêu tốn resource hơn.

**2. Node `Get Events1` (Google Calendar)**
- **Credential:** Chọn tài khoản Google Calendar của bạn.
- **Calendar ID:** Chọn lịch cụ thể (thường là `primary` hoặc ID của lịch nhóm).
- **Time Min / Time Max:** Cấu hình khoảng thời gian cần lấy. Ví dụ: Lấy sự kiện từ hôm nay đến 1 tuần tới. *Lưu ý: Nếu muốn lấy toàn bộ lịch, hãy để trống hoặc thiết lập khoảng thời gian rộng.*

**3. Node `Get Rows1` (Google Sheets)**
- **Credential:** Chọn tài khoản Google Sheets.
- **Document ID:** ID của file Sheets.
- **Sheet Name:** Tên tab chứa dữ liệu.
- **Range:** Phạm vi dữ liệu cần đọc (ví dụ: `A1:F100`).

**4. Node `Match Events vs Rows1` (Code)**
- Đây là "bộ não" của workflow. Nó so sánh sự kiện từ Calendar với các dòng có sẵn trong Sheets.
- **Logic mặc định:** Nó sẽ kiểm tra xem sự kiện có tồn tại trong Sheet chưa (dựa trên `event.id` hoặc `event.summary`).
- **Chỉnh sửa (nếu cần):** Nếu các sếp muốn so khớp dựa trên tiêu đề sự kiện thay vì ID, hãy mở node Code và chỉnh sửa logic JavaScript bên trong.

**5. Node `Update Sheet1` & `Add to Sheet1` (Google Sheets)**
- **Update Sheet1:** Chạy khi sự kiện đã tồn tại trong Sheet nhưng có thay đổi (thời gian, địa điểm...). Cần đảm bảo cột `ID` hoặc `Key` trong Sheet khớp với logic so khớp ở bước trên.
- **Add to Sheet1:** Chạy khi phát hiện sự kiện mới chưa có trong Sheet.
- **Lưu ý:** Đảm bảo thứ tự cột trong Google Sheets khớp với mapping trong node này.

**6. Node `Check for Empty Events1` & `Check for Match1` (IF)**
- Các node này giúp lọc dữ liệu rỗng và phân luồng (branching) để quyết định là **Cập nhật** hay **Thêm mới**. Thường không cần chỉnh sửa gì thêm nếu cấu hình đúng ở các bước trên.

#### 3. Kích hoạt ⚡️
1. Click **"Test Workflow"** để chạy thử với dữ liệu mẫu.
2. Kiểm tra kết quả:
   - Sự kiện mới có được thêm vào Sheet không?
   - Sự kiện đã có có được cập nhật thông tin không?
3. Nếu mọi thứ ổn, click nút **"Active"** ở góc trên bên phải để bật workflow chạy nền.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Slack/Telegram:** Thêm node `Slack` hoặc `Telegram` sau bước `Add to Sheet1` để gửi thông báo "Sự kiện mới đã được ghi nhận" vào kênh làm việc.
- **Lọc sự kiện theo Tag/Label:** Sử dụng node `Filter` hoặc chỉnh Code node để chỉ đồng bộ các sự kiện có chứa từ khóa nhất định (ví dụ: "Client", "Deadline").
- **Xóa sự kiện đã hủy:** Hiện tại workflow chủ yếu là thêm/cập nhật. Các sếp có thể thêm logic để xóa dòng trong Sheet nếu sự kiện bị xóa khỏi Calendar (cần thêm node `Delete Row` và logic so khớp ngược).
- **Báo cáo định kỳ:** Kết hợp thêm node `Email` hoặc `Google Docs` để tự động gửi báo cáo tổng hợp các sự kiện trong tuần vào thứ Hai hàng tuần.

### 📌 Kết luận
Workflow này là công cụ "vô địch" cho những ai cần biến lịch trình hỗn tạp thành dữ liệu có cấu trúc. Với khả năng tự động hóa hoàn toàn, nó giúp các sếp tập trung vào công việc thay vì loay hoay với việc sao chép dữ liệu. Hãy import và thiết lập ngay hôm nay để trải nghiệm sự khác biệt!