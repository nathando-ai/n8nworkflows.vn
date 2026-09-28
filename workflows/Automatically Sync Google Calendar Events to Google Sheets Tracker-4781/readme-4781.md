---
title: "📅 Đồng bộ Google Calendar sang Google Sheets Tự động 100%"
description: "Workflow n8n tự động quét lịch Google Calendar và cập nhật trạng thái sự kiện vào Google Sheets theo thời gian thực, giúp quản lý công việc chính xác và không bỏ sót."
slug: "dong-bo-calendar-sang-sheets"
tags: [n8n, google-calendar, google-sheets, automation, no-code]
keywords: [n8n workflow, đồng bộ google calendar, tự động hóa google sheets, quản lý lịch làm việc, n8n integration]
---

# 📅 Đồng bộ Google Calendar sang Google Sheets Tự động 100%

Các sếp có bao giờ cảm thấy mệt mỏi khi phải mở Google Calendar để xem lịch, rồi lại mở Google Sheets để cập nhật lại trạng thái các sự kiện (đã hoàn thành, đang diễn ra, hay bị hủy)? Việc này không chỉ tốn thời gian mà còn dễ dẫn đến sai sót dữ liệu, khiến bảng theo dõi (tracker) không phản ánh đúng thực tế.

Workflow **"Automatically Sync Google Calendar Events to Google Sheets Tracker"** do Alex Halfborg (một chuyên gia marketing technology với hơn 20 năm kinh nghiệm) phát triển chính là giải pháp hoàn hảo. Nó tự động quét các sự kiện trong lịch của bạn và đối chiếu với dữ liệu có sẵn trong Google Sheets. Nếu có sự kiện mới, nó sẽ thêm vào; nếu sự kiện đã thay đổi trạng thái, nó sẽ cập nhật lại. Mọi thứ diễn ra hoàn toàn tự động, không cần viết một dòng code nào.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian thủ công:** Loại bỏ hoàn toàn bước nhập liệu thủ công giữa Calendar và Sheets.
- **Dữ liệu luôn nhất quán:** Bảng theo dõi (Tracker) luôn phản ánh chính xác trạng thái mới nhất của lịch.
- **Phát hiện sự kiện mới tự động:** Bất kỳ sự kiện nào được thêm vào Calendar sẽ tự động xuất hiện trong Sheets.
- **Cập nhật trạng thái thông minh:** Workflow tự động nhận diện và cập nhật các sự kiện đã tồn tại thay vì tạo trùng lặp.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Google:** Đã đăng nhập và có quyền truy cập vào Google Calendar và Google Sheets.
2. **Google Sheet Tracker:** Một bảng tính đã được tạo với các cột tương ứng (ví dụ: Tên sự kiện, Thời gian bắt đầu, Trạng thái, v.v.).
3. **Credentials n8n:**
   - *Google Calendar OAuth2 API*
   - *Google Sheets OAuth2 API*
4. **VPS hoặc n8n Cloud:** Môi trường chạy n8n (khuyến nghị Self-hosted trên VPS để tối ưu chi phí và bảo mật).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Mở n8n Editor.
2. Chọn **Import from File** hoặc **Import from URL**.
3. Dán link gốc: `https://n8n.io/workflows/4781` hoặc tải file JSON về và import.
4. Sau khi import, các sếp sẽ thấy 9 nodes được kết nối sẵn.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Đây là phần quan trọng nhất. Các sếp cần cấu hình từng node cụ thể sau:

*   **Node: `Schedule Trigger1`**
    *   Đây là node khởi động workflow.
    *   **Cấu hình:** Chọn tần suất chạy. Ví dụ: Mỗi 15 phút hoặc Mỗi 1 giờ. Tần suất càng cao, dữ liệu càng cập nhật nhanh nhưng tốn tài nguyên hơn.

*   **Node: `Get Events1` (Google Calendar)**
    *   **Credentials:** Chọn credentials Google Calendar đã tạo.
    *   **Calendar ID:** Điền ID của lịch cần đồng bộ (thường là `primary` hoặc email của tài khoản).
    *   **Time Min/Max:** Thiết lập khoảng thời gian quét (ví dụ: từ hôm nay đến 7 ngày tới) để tránh tải quá nhiều dữ liệu cũ.

*   **Node: `Get Rows1` (Google Sheets)**
    *   **Credentials:** Chọn credentials Google Sheets.
    *   **Document ID:** ID của file Google Sheets.
    *   **Sheet Name:** Tên tab chứa dữ liệu tracker.
    *   **Range:** Xác định vùng dữ liệu cần đọc (ví dụ: `A2:D100`).

*   **Node: `Match Events vs Rows1` (Code Node)**
    *   Node này chứa logic JavaScript để so sánh sự kiện từ Calendar với các dòng trong Sheets.
    *   **Lưu ý:** Các sếp cần kiểm tra lại logic trong code nếu cấu trúc cột trong Sheets của mình khác với mẫu gốc. Đảm bảo các trường (fields) như `summary`, `start`, `status` được map đúng.

*   **Node: `Update Sheet1` & `Add to Sheet1` (Google Sheets)**
    *   Hai node này xử lý kết quả từ bước so sánh.
    *   **Update Sheet1:** Chạy khi sự kiện đã tồn tại trong Sheets nhưng cần cập nhật trạng thái.
    *   **Add to Sheet1:** Chạy khi phát hiện sự kiện mới chưa có trong Sheets.
    *   **Cấu hình:** Đảm bảo các cột (Columns) trong node này khớp với tiêu đề cột trong Google Sheets của các sếp.

#### 3. Kích hoạt ⚡️
1. **Test Run:** Nhấn nút **Execute Workflow** (hoặc chọn một node cụ thể để test riêng) để đảm bảo dữ liệu được đọc và ghi đúng.
2. **Active:** Bật công tắc **Active** ở góc trên bên phải để workflow bắt đầu chạy tự động theo lịch đã đặt.

### ✍️ Mẹo & gợi ý nâng cao
- **Gửi thông báo qua Telegram/Slack:** Thêm node `Telegram` hoặc `Slack` sau bước `Add to Sheet1` để nhận thông báo ngay khi có sự kiện quan trọng mới được thêm vào tracker.
- **Lọc sự kiện theo Tag:** Trong node `Get Events1`, các sếp có thể thêm bộ lọc (Filter) để chỉ đồng bộ những sự kiện có chứa từ khóa nhất định (ví dụ: "Client", "Deadline").
- **Lưu Log lịch sử:** Tạo một tab riêng trong Google Sheets để lưu lại lịch sử các lần cập nhật, giúp truy vết khi có lỗi dữ liệu.
- **Định dạng tự động:** Sử dụng tính năng Conditional Formatting trong Google Sheets để tô màu các sự kiện dựa trên trạng thái (Đã hoàn thành, Chậm, v.v.) sau khi workflow cập nhật.

### 📌 Kết luận
Việc đồng bộ hóa dữ liệu giữa các nền tảng là bước đi tất yếu để tối ưu hóa quy trình làm việc. Với workflow này, các sếp không còn phải lo lắng về việc quên cập nhật bảng theo dõi hay nhập liệu sai sót. Hãy import ngay và thiết lập credentials để trải nghiệm sự tiện lợi của tự động hóa n8n!